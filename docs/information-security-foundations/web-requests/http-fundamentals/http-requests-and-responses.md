---
glightbox: true
icon: material/help
---

# HTTP Requests and Responses

## HTTP Request

![](../assets/images/raw-request.png)

| Field | Description |
|---|---|
| Method | Gerçekleştirilecek eylemin türünü belirten HTTP yöntemi. |
| Path | Erişilen kaynağın yolu. |
| Version | HTTP sürümünü belirtmek için kullanılır. HTTP sürüm 1.x istekleri metin olarak gönderir ve farklı alanları ve farklı istekleri ayırmak için yeni satır karakteri kullanır. HTTP sürüm 2.x ise istekleri sözlük biçiminde ikili veri olarak gönderir. |

## HTTP Response

![](../assets/images/raw-response.png)

HTTP yanıtının ilk satırı boşluklarla ayrılmış iki alan içerir:

1. HTTP sürümünü belirtir.
2. HTTP yanıt kodunu belirtir.

## cURL

```bash
curl inlanefreight.com -v
```

## Questions

```text
Send a GET request to the above server, and read the response headers to find the version of Apache running on the server, then submit it as the answer. (answer format: X.Y.ZZ)
```

??? tip "Steps"

    ```bash
    curl 94.237.53.115:34897 -v
    ```
