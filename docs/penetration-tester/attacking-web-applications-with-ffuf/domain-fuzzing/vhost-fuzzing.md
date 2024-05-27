---
glightbox: true
icon: material/circle-small
---

# Vhost Fuzzing

## Vhosts vs. Sub-domains

vHost, aslında bir alt alan adı olarak düşünülebilir. Farklı olarak vHost, aynı sunucudan ve aynı IP adresi ile kullanıma sunulur. Böylece tek bir IP adresi ile iki veya daha fazla web sitesi kullanılabilir.

!!! info "Public Record"

    vHost, bezen Public DNS kayıtlarında bulunabilir.

Çoğu durumda web siteleri, vHost sayfalarını Public DNS kayıtlarında yayınlamazlar. Bu nedenle bu sayfaları bir web tarayıcısında ziyaret edersek, bu sayfalara bağlantı kuramayız.

Böyle durumlarda vHost Fuzzing yöntemini kullanmak faydalı olabilir.

## Vhosts Fuzzing

Wordlist içerisinde bulunan kayıtların tamamını `/etc/hosts` dosyasına el ile eklemeden vHost fuzzing gerçekleştirebilmek için HTTP başlıkları (örneğin `Host: FUZZ.academy.htb`) kullanılabilir:

```bash
ffuf -ic -H 'Host: FUZZ.academy.htb' -w /opt/useful/SecLists/Discovery/DNS/subdomains-top1million-5000.txt:FUZZ -u http://academy.htb:PORT/
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
 :: URL              : http://academy.htb:PORT/
 :: Wordlist         : FUZZ: /opt/useful/SecLists/Discovery/DNS/subdomains-top1million-5000.txt
 :: Header           : Host: FUZZ
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: 200,204,301,302,307,401,403
________________________________________________

mail2                   [Status: 200, Size: 900, Words: 423, Lines: 56]
dns2                    [Status: 200, Size: 900, Words: 423, Lines: 56]
ns3                     [Status: 200, Size: 900, Words: 423, Lines: 56]
dns1                    [Status: 200, Size: 900, Words: 423, Lines: 56]
lists                   [Status: 200, Size: 900, Words: 423, Lines: 56]
webmail                 [Status: 200, Size: 900, Words: 423, Lines: 56]
static                  [Status: 200, Size: 900, Words: 423, Lines: 56]
web                     [Status: 200, Size: 900, Words: 423, Lines: 56]
www1                    [Status: 200, Size: 900, Words: 423, Lines: 56]

...SNIP...
```

Çıktıda karşılaşılan sonuçlar garip gelmiş olabilir. Çünkü tüm sayfalar 200 OK yanıtı döndürmektedir! Bu durum aslında normaldir. Çünkü fuzzing gerçekleştirmek için kullandığımız adres (`academy.htb:PORT`) aynı kalırken, HTTP başlığının (`Host: FUZZ.academy.htb`) içeriği değişmektedir.

Bununla birlikte, doğru vHost bilgisini HTTP başlığında gönderirsek, çıktıda farklı bir yanıt boyutu (`Size`) gözükecektir. Bu sayede gerçek sayfayı tespit etmemiz mümkün olabilir.
