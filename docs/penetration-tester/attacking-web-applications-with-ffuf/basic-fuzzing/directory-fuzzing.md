---
glightbox: true
icon: material/circle-small
---

# Directory Fuzzing

Wordlist dosyasının sonuna `FUZZ` anahtar kelimesi eklenerek, wordlist ile anahtar kelime ilişkilendirilebilir. FFuF komutuna birden fazla wordlist tek seferde verilebilir.

!!! warning "Wordlist Comments"

    Bazı wordlist dosyalarında yorum satırları bulunmaktadır. FFuF taramasını başlatmadan önce bu satırları kaldırmak faydalı olacaktır. Bu işlem el ile veya FFuF aracının `-ic` seçeneğiyle gerçekleştirilebilir.

```bash
ffuf -ic -w /opt/useful/SecLists/Discovery/Web-Content/directory-list-2.3-small.txt:FUZZ -u http://SERVER_IP_ADDRESS:PORT/FUZZ
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
 :: URL              : http://SERVER_IP_ADDRESS:PORT/FUZZ
 :: Wordlist         : FUZZ: /opt/useful/SecLists/Discovery/Web-Content/directory-list-2.3-small.txt
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: 200,204,301,302,307,401,403
________________________________________________

...SNIP...

blog                    [Status: 301, Size: 326, Words: 20, Lines: 10]
:: Progress: [87651/87651] :: Job [1/1] :: 9739 req/sec :: Duration: [0:00:09] :: Errors: 0 ::
```
