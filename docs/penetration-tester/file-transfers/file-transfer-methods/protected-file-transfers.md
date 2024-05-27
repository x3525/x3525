---
glightbox: true
icon: material/circle-small
---

# Protected File Transfers

Sızma testi uzmanları olarak kullanıcı listeleri, kimlik bilgileri ve kuruluşun ağ altyapısı gibi son derece hassas verilere sıklıkla erişim elde ederiz. Bu nedenle bu verilerin şifrelenmesi veya SSH, SFTP ve HTTPS gibi şifrelenmiş veri bağlantılarının kullanılması önemlidir. Ancak bazen bu seçenekleri kullanmak mümkün olmayabilir ve farklı bir yaklaşım gerekebilir.

## File Encryption on Windows

Windows sistemlerinde dosya ve bilgilerin şifrelenmesi için birçok farklı yöntem kullanılabilmektedir. En basit yöntemlerden biri [Invoke-AESEncryption.ps1](https://www.powershellgallery.com/packages/DRTools/4.0.2.3/Content/Functions/Invoke-AESEncryption.ps1) PowerShell script kullanmaktır. Bu script, dosyaların ve dizelerin şifrelenmesini sağlar:

```powershell title="Invoke-AESEncryption.ps1" linenums="1"
<#
.SYNOPSIS
Encryptes or Decrypts Strings or Byte-Arrays with AES

.DESCRIPTION
Takes a String or File and a Key and encrypts or decrypts it with AES256 (CBC)

.PARAMETER Mode
Encryption or Decryption Mode

.PARAMETER Key
Key used to encrypt or decrypt

.PARAMETER Text
String value to encrypt or decrypt

.PARAMETER Path
Filepath for file to encrypt or decrypt

.EXAMPLE
Invoke-AESEncryption -Mode Encrypt -Key "p@ssw0rd" -Text "Secret Text"

Description
-----------
Encrypts the string "Secret Test" and outputs a Base64 encoded cipher text.

.EXAMPLE
Invoke-AESEncryption -Mode Decrypt -Key "p@ssw0rd" -Text "LtxcRelxrDLrDB9rBD6JrfX/czKjZ2CUJkrg++kAMfs="

Description
-----------
Decrypts the Base64 encoded string "LtxcRelxrDLrDB9rBD6JrfX/czKjZ2CUJkrg++kAMfs=" and outputs plain text.

.EXAMPLE
Invoke-AESEncryption -Mode Encrypt -Key "p@ssw0rd" -Path file.bin

Description
-----------
Encrypts the file "file.bin" and outputs an encrypted file "file.bin.aes"

.EXAMPLE
Invoke-AESEncryption -Mode Encrypt -Key "p@ssw0rd" -Path file.bin.aes

Description
-----------
Decrypts the file "file.bin.aes" and outputs an encrypted file "file.bin"
#>
function Invoke-AESEncryption {
    [CmdletBinding()]
    [OutputType([string])]
    Param
    (
        [Parameter(Mandatory = $true)]
        [ValidateSet('Encrypt', 'Decrypt')]
        [String]$Mode,

        [Parameter(Mandatory = $true)]
        [String]$Key,

        [Parameter(Mandatory = $true, ParameterSetName = "CryptText")]
        [String]$Text,

        [Parameter(Mandatory = $true, ParameterSetName = "CryptFile")]
        [String]$Path
    )

    Begin {
        $shaManaged = New-Object System.Security.Cryptography.SHA256Managed
        $aesManaged = New-Object System.Security.Cryptography.AesManaged
        $aesManaged.Mode = [System.Security.Cryptography.CipherMode]::CBC
        $aesManaged.Padding = [System.Security.Cryptography.PaddingMode]::Zeros
        $aesManaged.BlockSize = 128
        $aesManaged.KeySize = 256
    }

    Process {
        $aesManaged.Key = $shaManaged.ComputeHash([System.Text.Encoding]::UTF8.GetBytes($Key))

        switch ($Mode) {
            'Encrypt' {
                if ($Text) {$plainBytes = [System.Text.Encoding]::UTF8.GetBytes($Text)}

                if ($Path) {
                    $File = Get-Item -Path $Path -ErrorAction SilentlyContinue
                    if (!$File.FullName) {
                        Write-Error -Message "File not found!"
                        break
                    }
                    $plainBytes = [System.IO.File]::ReadAllBytes($File.FullName)
                    $outPath = $File.FullName + ".aes"
                }

                $encryptor = $aesManaged.CreateEncryptor()
                $encryptedBytes = $encryptor.TransformFinalBlock($plainBytes, 0, $plainBytes.Length)
                $encryptedBytes = $aesManaged.IV + $encryptedBytes
                $aesManaged.Dispose()

                if ($Text) {return [System.Convert]::ToBase64String($encryptedBytes)}

                if ($Path) {
                    [System.IO.File]::WriteAllBytes($outPath, $encryptedBytes)
                    (Get-Item $outPath).LastWriteTime = $File.LastWriteTime
                    return "File encrypted to $outPath"
                }
            }

            'Decrypt' {
                if ($Text) {$cipherBytes = [System.Convert]::FromBase64String($Text)}

                if ($Path) {
                    $File = Get-Item -Path $Path -ErrorAction SilentlyContinue
                    if (!$File.FullName) {
                        Write-Error -Message "File not found!"
                        break
                    }
                    $cipherBytes = [System.IO.File]::ReadAllBytes($File.FullName)
                    $outPath = $File.FullName -replace ".aes"
                }

                $aesManaged.IV = $cipherBytes[0..15]
                $decryptor = $aesManaged.CreateDecryptor()
                $decryptedBytes = $decryptor.TransformFinalBlock($cipherBytes, 16, $cipherBytes.Length - 16)
                $aesManaged.Dispose()

                if ($Text) {return [System.Text.Encoding]::UTF8.GetString($decryptedBytes).Trim([char]0)}

                if ($Path) {
                    [System.IO.File]::WriteAllBytes($outPath, $decryptedBytes)
                    (Get-Item $outPath).LastWriteTime = $File.LastWriteTime
                    return "File decrypted to $outPath"
                }
            }
        }
    }

    End {
        $shaManaged.Dispose()
        $aesManaged.Dispose()
    }
}
```

Bu script ile çalışabilmek için öncelikle dosyayı import etmeliyiz:

```powershell
Import-Module "Invoke-AESEncryption.ps1"
```

Script import edildikten sonra dizeler veya dosyalar şifrelenebilir:

```powershell
Invoke-AESEncryption -Mode Encrypt -Key "p4ssw0rd" -Path "scan-results.txt"
```

```text title="Output"
File encrypted to C:\htb\scan-results.txt.aes
```

Sızma testi yapılan her firmaya özel çok güçlü ve benzersiz parolalar kullanılması gerekmektedir. Bu sayede, üçüncü bir tarafça sızdırılmış ve kırılmış olabilecek hassas dosya ve bilgilerin tek bir parola kullanılarak şifresinin çözülmesi önlenebilir.

## File Encryption on Linux

[OpenSSL](https://www.openssl.org/) güvenlik sertifikaları oluşturmak için kullanılabilir. OpenSSL kullanarak bir dosyayı şifrelemek için farklı [şifreler](https://www.openssl.org/docs/man1.1.1/man1/openssl-enc.html) seçebiliriz. Örnek olarak AES-256 kullanalım. Ayrıca varsayılan iterasyon sayılarını geçersiz kılabilir ve PBKDF2 (Password-Based Key Derivation Function 2) algoritmasını kullanabiliriz. Enter tuşuna bastığımızda bir parola girmemiz gerekecek:

```bash
openssl enc -aes256 -iter 100000 -pbkdf2 -in /etc/passwd -out passwd.enc
```

Yetkisiz kişilerin dosyayı ele geçirmesi durumunda kaba kuvvet saldırılarını önlemek için güçlü ve benzersiz bir parola kullanmayı unutmayın.

Dosyanın şifresini çözmek için ise aşağıdaki komutu kullanabiliriz:

```bash
openssl enc -d -aes256 -iter 100000 -pbkdf2 -in passwd.enc -out passwd
```
