---
glightbox: true
icon: material/help
---

# POST

Web uygulamaları dosya aktarmaya ihtiyaç duyduğunda POST isteklerini kullanır. HTTP GET isteklerinden farklı olarak kullanıcı parametreleri URL içinde değil, istek gövdesinde bulunur.

## Login Forms

```bash
curl -i -X POST -d 'username=admin&password=admin' http://<SERVER_IP_ADDRESS>:<PORT>/
```

```text title="Output"
HTTP/1.1 200 OK
Date:
Server: Apache/2.4.41 (Ubuntu)
Set-Cookie: PHPSESSID=c1nsa6op7vtk7kdis7bcnbadf1; path=/

...SNIP...
```

## Authenticated Cookies

Elde edilen kimliği doğrulanmış çerezler sayesinde, her seferinde kimlik bilgilerini vermeye gerek kalmadan web uygulamasıyla etkileşim kurabiliriz.

Cookie kullanarak kimlik doğrula:

```bash
curl -b 'PHPSESSID=c1nsa6op7vtk7kdis7bcnbadf1' http://<SERVER_IP_ADDRESS>:<PORT>/
```

Header ile Cookie ayarla:

```bash
curl -H 'Cookie: PHPSESSID=c1nsa6op7vtk7kdis7bcnbadf1' http://<SERVER_IP_ADDRESS>:<PORT>/
```

## JSON Data

JSON tipinde veri göndermek ve karşılığında yanıt almak için:

```bash
curl -X POST -d '{"search":"london"}' -H 'Content-Type: application/json' -b 'PHPSESSID=c1nsa6op7vtk7kdis7bcnbadf1' http://<SERVER_IP_ADDRESS>:<PORT>/search.php
```

## Questions

```text
Obtain a session cookie through a valid login, and then use the cookie with cURL to search for the flag through a JSON POST request to '/search.php'
```

??? tip "Steps"

    Soruda verilen hedef makine adresini tarayıcı arama çubuğuna gir ve adrese git.

    Kullanıcı adı ve parola olarak `admin` bilgisini kullan.

    DevTools içinde `Storage` --> `Cookies` konumuna git.

    Başarılı giriş sonrası elde edilen cookie bilgisini kopyala.

    JSON formatını kullanarak flag kelimesi için bir arama gerçekleştir:

    ```bash
    curl -X POST -d '{"search":"flag"}' -H 'Content-Type: application/json' -b 'PHPSESSID=prathm7k958n2dc8ckb3f82eag' 94.237.59.206:47445/search.php
    ```

    Yanıt olarak flag bilgisi gönderilecektir.
