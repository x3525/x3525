---
glightbox: true
icon: material/circle-small
---

# Page Fuzzing

Bir web sitesinde bulunan sayfaların uzantısını (.html, .php, .aspx vs.) tespit edebilmek için `FUZZ` anahtar kelimesini sayfa isminin sonuna ekleyebiliriz. Örneğin `index` sayfasını ele alalım. Bu sayfa web sitelerinde sıklıkla karşılaşılan bir sayfa olduğundan, ilk olarak bu sayfa ismini denemekte fayda vardır.

Kullanılacak olan wordlist içerisinde bulunan uzantılar nokta işareti içeriyorsa, anahtar kelime direkt olarak sayfa isminin ardına eklenebilir (`indexFUZZ`).

Kullanılacak olan wordlist içerisinde bulunan uzantılar nokta işareti içermiyorsa, anahtar kelime ile sayfa ismi arasına nokta işareti eklenmelidir (`index.FUZZ`).

```bash
ffuf -ic -w /opt/useful/SecLists/Discovery/Web-Content/web-extensions.txt:FUZZ -u http://SERVER_IP_ADDRESS:PORT/blog/indexFUZZ
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
 :: URL              : http://SERVER_IP_ADDRESS:PORT/blog/indexFUZZ
 :: Wordlist         : FUZZ: /opt/useful/SecLists/Discovery/Web-Content/web-extensions.txt
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 5
 :: Matcher          : Response status: 200,204,301,302,307,401,403
________________________________________________

.php                    [Status: 200, Size: 0, Words: 1, Lines: 1]
.phps                   [Status: 403, Size: 283, Words: 20, Lines: 10]
:: Progress: [39/39] :: Job [1/1] :: 0 req/sec :: Duration: [0:00:00] :: Errors: 0 ::
```

Çıktıda görüldüğü üzere bu web sitesi, uzantısı .php olan dosyalar kullanıyor. Bundan sonra FFuF aracını normal şekilde (`FUZZ.php`) kullanarak PHP sayfalarını bulabiliriz:

```bash
ffuf -ic -w /opt/useful/SecLists/Discovery/Web-Content/directory-list-2.3-small.txt:FUZZ -u http://SERVER_IP_ADDRESS:PORT/blog/FUZZ.php
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
 :: URL              : http://SERVER_IP_ADDRESS:PORT/blog/FUZZ.php
 :: Wordlist         : FUZZ: /opt/useful/SecLists/Discovery/Web-Content/directory-list-2.3-small.txt
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: 200,204,301,302,307,401,403
________________________________________________

index                   [Status: 200, Size: 0, Words: 1, Lines: 1]
REDACTED                [Status: 200, Size: 465, Words: 42, Lines: 15]
:: Progress: [87651/87651] :: Job [1/1] :: 5843 req/sec :: Duration: [0:00:15] :: Errors: 0 ::
```
