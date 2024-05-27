---
glightbox: true
icon: material/circle-small
---

# Parameter Fuzzing - POST

!!! warning "Content-Type"

    PHP, POST sorgularında Content-Type değeri olarak sadece `application/x-www-form-urlencoded` değerini kabul etmektedir. Bu yüzden FFuF komutuna bu değer `-H` seçeneği ile eklenmelidir.

```bash
ffuf -ic -X POST -d 'FUZZ=key' -H 'Content-Type: application/x-www-form-urlencoded' -fs 785 -w /opt/useful/SecLists/Discovery/Web-Content/burp-parameter-names.txt:FUZZ -u http://admin.academy.htb:PORT/admin/admin.php
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

 :: Method           : POST
 :: URL              : http://admin.academy.htb:PORT/admin/admin.php
 :: Wordlist         : FUZZ: /opt/useful/SecLists/Discovery/Web-Content/burp-parameter-names.txt
 :: Header           : Content-Type: application/x-www-form-urlencoded
 :: Data             : FUZZ=key
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: 200,204,301,302,307,401,403
 :: Filter           : Response size: 785
________________________________________________

id                      [Status: 200, Size: 654, Words: 256, Lines: 65]

...SNIP...
```

Bulduğumuz parametreyi (`id`) kullanarak POST sorgusu gerçekleştirmek için cURL aracını kullanabiliriz:

```bash
curl -X POST -d 'id=key' -H 'Content-Type: application/x-www-form-urlencoded' http://admin.academy.htb:PORT/admin/admin.php
```
