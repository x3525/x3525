---
glightbox: true
icon: material/help
---

# GET

HTTP GET kullanıldığında kullanıcı parametreleri URL içine yerleştirilir.

## HTTP Basic Auth

Kullanıcı kimlik bilgilerini doğrulamak amacıyla HTTP POST parametrelerini kullanan oturum açma formlarının aksine, belirli bir sayfayı/dizini korumak için, web uygulaması ile etkileşime girmeden doğrudan web sunucusu tarafından işlenen temel bir HTTP kimlik doğrulamasıdır.

Yanıt başlıklarını talep et:

```bash
curl -i http://<SERVER_IP_ADDRESS>:<PORT>/
```

```text title="Output"
HTTP/1.1 401 Authorization Required
Date: Mon, 21 Feb 2022 13:11:46 GMT
Server: Apache/2.4.41 (Ubuntu)
Cache-Control: no-cache, must-revalidate, max-age=0
WWW-Authenticate: Basic realm="Access denied"
Content-Length: 13
Content-Type: text/html; charset=UTF-8

Access denied
```

Çıktıda görülen `Basic` kısmı, bu sayfanın, HTTP basic auth kullandığını bildirir.

## HTTP Authorization Header

Kullanıcı adı ve parola ayarla:

```bash
curl -v -u admin:admin http://<SERVER_IP_ADDRESS>:<PORT>/
```

URL User Info ile kullanıcı adı ve parola ayarla:

```bash
curl -v http://admin:admin@<SERVER_IP_ADDRESS>:<PORT>/
```

```text title="Output"
*   Trying <SERVER_IP_ADDRESS>:<PORT>...
* Connected to <SERVER_IP_ADDRESS> (<SERVER_IP_ADDRESS>) port PORT (#0)
* Server auth using Basic with user 'admin'
> GET / HTTP/1.1
> Host: <SERVER_IP_ADDRESS>
> Authorization: Basic YWRtaW46YWRtaW4=
> User-Agent: curl/7.77.0
> Accept: */*

...SNIP...
```

Çıktıda görülen `Basic` kısmı, verilen kimlik bilgilerinin Base64 ile kodlanmış halidir. Kullanıcı adı ve parola vermeden direkt bu değer ile kimlik denetimi gerçekleştirebiliriz:

```bash
curl -H 'Authorization: Basic YWRtaW46YWRtaW4=' http://<SERVER_IP_ADDRESS>:<PORT>/
```

## GET Parameters

DevTools kullanılarak GET isteği göndermek için gerekli olan cURL komutu ya da JavaScript Fetch metodu elde edilebilir:

* DevTools içinde `Copy Value` --> `Copy as cURL (Windows)` seçeneğini kullanarak.
* DevTools içinde `Copy Value` --> `Copy as cURL (POSIX)` seçeneğini kullanarak.
* DevTools içinde `Copy Value` --> `Copy as Fetch` seçeneğini kullanarak.

## Questions

```text
The exercise above seems to be broken, as it returns incorrect results. Use the browser devtools to see what is the request it is sending when we search, and use cURL to search for 'flag' and obtain the flag.
```

??? tip "Steps"

    Soruda verilen hedef makine adresini tarayıcı arama çubuğuna gir ve adrese git.

    Kullanıcı adı ve parola olarak `admin` bilgisini kullan.

    Arama kutusunu kullanarak flag kelimesi için bir arama gerçekleştir.

    DevTools içinde `Copy Value` --> `Copy as cURL (POSIX)` seçeneğini kullan.

    Elde edilen komut ile cURL çalıştır (User-Agent kısmını kaldır):

    ```bash
    curl -H 'Authorization: Basic YWRtaW46YWRtaW4=' 94.237.59.206:46374/search.php?search=flag
    ```

    Yanıt olarak flag bilgisi gönderilecektir.
