---
glightbox: true
---

# SSH Key-based Authentication

Daha fazla yardım için [Microsoft](https://learn.microsoft.com/en-us/windows-server/administration/openssh/openssh_keymanagement) sitesine başvurabilirsiniz.

## Client Setup

İstemci bilgisayarda `OpenSSH Client` isteğe bağlı özelliğini (optional feature) yükle ve aşağıdaki komutları yönetici haklarıyla çalıştır:

```powershell
Set-Service ssh-agent -StartupType Automatic
Start-Service ssh-agent
```

Bir anahtar çifti oluştur:

```powershell
ssh-keygen -t ed25519
```

Varsayılan anahtar ismi değiştirilmediyse `id_ed25519` isimli gizli anahtar (private key) ve `id_ed25519.pub` isimli açık anahtar (public key) geçerli kullanıcının `.ssh` dizini altında oluşacaktır.

Aşağıdaki komut ile gizli anahtarı SSH agent servisine yükle. Bu işlemin ardından gizli anahtar silinebilir:

```powershell
ssh-add "$env:USERPROFILE\.ssh\id_ed25519"
```

## Server Setup

Sunucu bilgisayarda `OpenSSH Server` isteğe bağlı özelliğini (optional feature) yükle ve aşağıdaki komutları yönetici haklarıyla çalıştır:

```powershell
Set-Service sshd -StartupType Automatic
Start-Service sshd
```

Daha önceden istemci tarafında oluşturulan açık anahtar sunucuya gönderilmelidir. Bu işlem standart kullanıcı hesabı ve yönetici hesabı için farklılık göstermektedir.

Kullanıcı hesabı standart bir kullanıcıya ait ise, açık anahtar bilgisi, tam yolu aşağıdaki komut ile elde edilebilecek olan `authorized_keys` dosyasının içerisine eklenmelidir:

```powershell
Write-Output "$env:USERPROFILE\.ssh\authorized_keys"
```

Kullanıcı hesabı yöneticiye ait ise, açık anahtar bilgisi, `C:\ProgramData\ssh` dizini altında bulunan `administrators_authorized_keys` dosyasının içerisine eklenmelidir.

Buna ek olarak aşağıdaki komut çalıştırılmalıdır:

```powershell
icacls.exe "$env:ProgramData\ssh\administrators_authorized_keys" /inheritance:r /grant "Administrators:F" /grant "SYSTEM:F"
```

Bu komut sayesinde aşağıdaki değişiklikler gerçekleştirilir:

* Tüm miras alma kaldırılır.
* Sadece Administrators ve SYSTEM tam yetki alır.

## SSH Connection

Kurulumun ardından aşağıdaki komut ile SSH bağlantısı gerçekleştirilebilir:

```powershell
ssh user@server
```
