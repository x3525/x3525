---
glightbox: true
icon: material/help
---

# CRUD API

## APIs

Birçok API, bir veri tabanıyla etkileşimde bulunmak için kullanılır. Böylece istenen tabloyu ve istenen satırı API sorgumuzda belirtebilir ve ardından gereken işlemi gerçekleştirmek için bir HTTP yöntemi kullanabiliriz.

## CRUD

Genel olarak CRUD API, talep edilen veri tabanı varlığı üzerinde 4 ana işlemi gerçekleştirir:

| Operation | HTTP Method | Description |
|---|---|---|
| Create | POST | Belirtilen verileri veri tabanı tablosuna ekler. |
| Read | GET | Belirtilen varlığı veri tabanı tablosundan okur. |
| Update | PUT | Belirtilen veri tabanı tablosunun verilerini günceller. |
| Delete | DELETE | Belirtilen satırı veri tabanı tablosundan kaldırır. |

### Read

API üzerinden, city tablosundan, tüm sonuçları getir:

```bash
curl http://<SERVER_IP_ADDRESS>:<PORT>/api.php/city/
```

API üzerinden, city tablosundan, London araması gerçekleştir:

```bash
curl http://<SERVER_IP_ADDRESS>:<PORT>/api.php/city/London
```

JSON çıktısını güzelleştir:

```bash
curl -s http://<SERVER_IP_ADDRESS>:<PORT>/api.php/city/London | jq
```

### Create

Istanbul şehrini ekle:

```bash
curl -X POST http://<SERVER_IP_ADDRESS>:<PORT>/api.php/city/ -H 'Content-Type: application/json' -d '{"city_name":"Istanbul", "country_name":"(TR)"}'
```

### Update

PUT, API girdilerini güncellemek ve ayrıntılarını değiştirmek için kullanılırken DELETE, belirli bir varlığı kaldırmak için kullanılır. API girdilerini güncellemek için PUT yerine PATCH de kullanılabilir. PATCH, bir girdiyi kısmen güncellemek için kullanılır. PUT ise tüm girdiyi güncellemek için kullanılır. Hangi yöntemin sunucu tarafından kabul edildiğini görmek için OPTIONS yöntemi kullanılabilir.

Istanbul şehrinin adını, Malatya olarak değiştir:

```bash
curl -X PUT http://<SERVER_IP_ADDRESS>:<PORT>/api.php/city/Istanbul -H 'Content-Type: application/json' -d '{"city_name":"Malatya", "country_name":"(TR)"}'
```

Bazı API servislerinde UPDATE, yeni girdiler oluşturmak için de kullanılabilir. Gönderilen veri kontrol edilir ve mevcut değilse oluşturulur.

### DELETE

Malatya şehrini sil:

```bash
curl -X DELETE http://<SERVER_IP_ADDRESS>:<PORT>/api.php/city/Malatya
```

## Questions

```text
First, try to update any city's name to be 'flag'. Then, delete any city. Once done, search for a city named 'flag' to get the flag.
```

??? tip "Steps"

    Mevcut şehirleri listele:

    ```bash
    curl 94.237.62.195:49108/api.php/city/
    ```

    London şehrinin adını flag olarak değiştir:

    ```bash
    curl -X PUT 94.237.62.195:49108/api.php/city/London -H 'Content-Type: application/json' -d '{"city_name":"flag","country_name":"(UK)"}'
    ```

    Birmingham şehrini sil:

    ```bash
    curl -X DELETE 94.237.62.195:49108/api.php/city/Birmingham
    ```

    Flag için sorgu gerçekleştir:

    ```bash
    curl 94.237.62.195:49108/api.php/city/flag
    ```
