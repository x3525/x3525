---
glightbox: true
icon: material/circle-small
---

# Value Fuzzing

Parametre değerleri için fuzzing işlemi gerçekleştirmek söz konusu olduğunda, ihtiyaçlarımızı karşılayacak önceden hazırlanmış bir wordlist bulamayabiliriz. Bunun için kendi wordlist dosyamızı oluşturmamız gerekebilir.

Örneğin, bir GET sorgusunda kullanılan `id` parametresinin değerleri genelde sayısal değerlerden oluşur. 1 ile 1000 arasında sayılardan oluşan bir wordlist oluşturmak için aşağıdaki komutu kullanabiliriz:

```bash
for i in $(seq 1 1000); do echo "$i" >> ids.txt; done
```

Oluşturduğumuz wordlist ile parametre değerlerine fuzzing işlemi uygulayabiliriz:

```bash
ffuf -ic -X POST -d 'id=FUZZ' -w ids.txt:FUZZ -H 'Content-Type: application/x-www-form-urlencoded' -fs 768 -u http://admin.academy.htb:PORT/admin/admin.php
```

```text title="Output"
        /'___\  /'___\           /'___\
       /\ \__/ /\ \__/  __  __  /\ \__/
       \ \ ,__\\ \ ,__\/\ \/\ \ \ \ ,__\
        \ \ \_/ \ \ \_/\ \ \_\ \ \ \ \_/
         \ \_\   \ \_\  \ \____/  \ \_\
          \/_/    \/_/   \/___/    \/_/

       v1.0.2
________________________________________________

 :: Method           : POST
 :: URL              : http://admin.academy.htb:30794/admin/admin.php
 :: Header           : Content-Type: application/x-www-form-urlencoded
 :: Data             : id=FUZZ
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: 200,204,301,302,307,401,403
 :: Filter           : Response size: 768
________________________________________________

73                      [Status: 200, Size: 787, Words: 218, Lines: 54]
```

İlgili parametre (`id`) için bulduğumuz değeri (`73`) kullanarak POST sorgusu gerçekleştirmek için cURL aracını kullanabiliriz:

```bash
curl -X POST -d 'id=73' -H 'Content-Type: application/x-www-form-urlencoded' http://admin.academy.htb:PORT/admin/admin.php
```
