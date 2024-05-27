---
glightbox: true
icon: material/circle-small
---

# Recursive Fuzzing

```bash
ffuf -ic -recursion -recursion-depth 1 -v -e .php -w /opt/useful/SecLists/Discovery/Web-Content/directory-list-2.3-small.txt:FUZZ -u http://SERVER_IP_ADDRESS:PORT/FUZZ
```

| Command | Description |
|---|---|
| `-recursion` | Özyinelemeli tarama gerçekleştir. Anahtar kelime olarak yalnızca `FUZZ` kelimesi kullanılabilir. Ayrıca bu kelime (`FUZZ`) URL kısmının sonuna eklenmelidir. |
| `-recursion-depth` | Maksimum özyineleme derinliğini belirtmek için kullanılır. |
| `-e` | Taranacak sayfa uzantılarını belirtmek için kullanılır. |
| `-v` | Ayrıntılı çıktı göster. Tam URL bilgisini gösterdiğinden faydalı bir seçenektir. |

```text title="Output"
        /'___\  /'___\           /'___\
       /\ \__/ /\ \__/  __  __  /\ \__/
       \ \ ,__\\ \ ,__\/\ \/\ \ \ \ ,__\
        \ \ \_/ \ \ \_/\ \ \_\ \ \ \ \_/
         \ \_\   \ \_\  \ \____/  \ \_\
          \/_/    \/_/   \/___/    \/_/

       v1.1.0-git
________________________________________________

 :: Method           : GET
 :: URL              : http://SERVER_IP_ADDRESS:PORT/FUZZ
 :: Wordlist         : FUZZ: /opt/useful/SecLists/Discovery/Web-Content/directory-list-2.3-small.txt
 :: Extensions       : .php
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: 200,204,301,302,307,401,403
________________________________________________

[Status: 200, Size: 986, Words: 423, Lines: 56] | URL | http://SERVER_IP_ADDRESS:PORT/
    * FUZZ:

[INFO] Adding a new job to the queue: http://SERVER_IP_ADDRESS:PORT/forum/FUZZ
[Status: 200, Size: 986, Words: 423, Lines: 56] | URL | http://SERVER_IP_ADDRESS:PORT/index.php
    * FUZZ: index.php

[Status: 301, Size: 326, Words: 20, Lines: 10] | URL | http://SERVER_IP_ADDRESS:PORT/blog | --> | http://SERVER_IP_ADDRESS:PORT/blog/
    * FUZZ: blog

...SNIP...

[Status: 200, Size: 0, Words: 1, Lines: 1] | URL | http://SERVER_IP_ADDRESS:PORT/blog/index.php
    * FUZZ: index.php

[Status: 200, Size: 0, Words: 1, Lines: 1] | URL | http://SERVER_IP_ADDRESS:PORT/blog/
    * FUZZ:

...SNIP...
```
