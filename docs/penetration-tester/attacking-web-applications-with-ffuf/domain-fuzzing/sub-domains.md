---
glightbox: true
icon: material/circle-small
---

# Sub-domains

Bir alan adının (örneğin `google.com`) altında bulunan alt alan adlarını (örneğin `photos.google.com`) öğrenebilmek için FFuF aracını kullanabiliriz.

Eğer `/etc/hosts` dosyasında ilgili alan adı için bir kayıt bulunamazsa Public DNS kayıtlarına bakılır. İlgili alan adı, Public DNS kayıtlarında bulunmuyorsa (örneğin yerel ağda ise) FFuF taramasından herhangi bir sonuç dönmeyecektir (alt alan adı mevcut olsa bile).

!!! info "vHosts"

    Public DNS kayıtlarında bulunmayan alt alan adlarını elde edebilmek için vHost fuzzing yöntemi kullanılabilir.

```bash
ffuf -ic -w /opt/useful/SecLists/Discovery/DNS/subdomains-top1million-5000.txt:FUZZ -u http://FUZZ.inlanefreight.com/
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
 :: URL              : http://FUZZ.inlanefreight.com/
 :: Wordlist         : FUZZ: /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: 200,204,301,302,307,401,403,405,500
________________________________________________

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 381ms]
    * FUZZ: support

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 385ms]
    * FUZZ: ns3

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 402ms]
    * FUZZ: blog

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 180ms]
    * FUZZ: my

[Status: 200, Size: 22266, Words: 2903, Lines: 316, Duration: 589ms]
    * FUZZ: www

...SNIP...
```
