---
glightbox: true
icon: material/circle-small
---

# Parameter Fuzzing - GET

Bir web sitesine GET sorgusu gerçekleştirmek için kullanabilecek parametreleri öğrenmek için aşağıdaki gibi bir komut (`?FUZZ=key`) kullanabiliriz:

```bash
ffuf -ic -fs 786 -w /opt/useful/SecLists/Discovery/Web-Content/burp-parameter-names.txt:FUZZ -u 'http://admin.academy.htb:PORT/admin/admin.php?FUZZ=key'
```

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
 :: URL              : http://admin.academy.htb:PORT/admin/admin.php?FUZZ=key
 :: Wordlist         : FUZZ: /opt/useful/SecLists/Discovery/Web-Content/burp-parameter-names.txt
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: 200,204,301,302,307,401,403
 :: Filter           : Response size: 786
________________________________________________

user                    [Status: 200, Size: 783, Words: 221, Lines: 54]

...SNIP...
```
