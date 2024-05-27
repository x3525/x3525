---
glightbox: true
icon: material/help
---

# HyperText Transfer Protocol (HTTP)

İnternet iletişimlerinin çoğu HTTP protokolü kullanılarak gerçekleştirilir. HTTP, WWW kaynaklarına erişmek için kullanılan uygulama düzeyinde bir protokoldür. HyperText, bağlantı içeren metin anlamına gelir.

HTTP iletişiminde sunucu, istekleri işler ve istenen kaynağı döndürür. HTTP iletişimi için varsayılan port 80 olarak tanımlıdır. Ancak istenirse bu port numarası değiştirilebilir.

## URL

![](../assets/images/url-structure.png)

| Component | Example | Description |
|---|---|---|
| Schema | `http://` | İstemci tarafından erişilen protokolü tanımlamak için kullanılır ve iki nokta üst üste ve çift eğik çizgiyle biter. |
| User Info | `admin:password@` | Bu bileşen isteğe bağlıdır. Bilgisayarda kimlik doğrulaması yapmak için kullanılan kimlik bilgilerini (iki nokta üst üste işaretiyle ayrılmış) içerir. |
| Host | `inlanefreight.com` | Kaynak konumunu belirtir. Bilgisayar adı veya IP adresi olabilir. |
| Port | `:80` | Host kısmından iki nokta üst üste ile ayrılır. HTTP için varsayılan olarak port 80 ve HTTPS için varsayılan olarak port 443 kullanılır. |
| Path | `/dashboard.php` | Erişilen kaynağa işaret eder. Belirtilen bir yol yoksa sunucu varsayılan dizini döndürür. |
| Query String | `?login=true` | Sorgu dizesi bir soru işaretiyle başlar ve bir parametre ve bir değerden oluşur. Birden fazla parametre & işaretiyle ayrılabilir. |
| Fragments | `#status` | Birincil kaynak içindeki bölümleri bulmak için istemci tarafındaki tarayıcılar tarafından işlenir. |

## HTTP Flow

![](../assets/images/http-flow.png)

1. Kullanıcı, tarayıcıya URL bilgisini yazar.
2. Alan adını çözümlemek ve IP adresini almak için tarayıcı tarafından yerel dosyalarda bir eşleşme aranır. İstenen alan adı yerelde bulunamaz ise DNS sunucusuna bir istek gönderilir.
3. DNS sunucusu verilen domain için IP adresini arar ve sonucu döndürür.
4. Tarayıcı gerekli IP adresini aldığında, varsayılan HTTP portuna (80) kök yolunu talep eden bir GET isteği gönderir. Daha sonra web sunucusu isteği alır ve işler. Varsayılan olarak sunucular, kök yolu talep edildiğinde index dosyasını döndürecek şekilde yapılandırılmıştır.
5. Index dosyasının içeriği web sunucusu tarafından okunur ve bir HTTP yanıtı olarak döndürülür. Yanıt, aynı zamanda isteğin başarıyla işlendiğini gösteren durum kodunu da (200 OK) içerir. Web tarayıcısı daha sonra index dosyasını işler ve içeriğini kullanıcıya sunar.

## cURL

cURL (client URL), birçok protokolü destekleyen bir komut satırı aracıdır. Birçok web sızma testi için gerekli olan web isteklerini komut satırından göndermek için kullanılabilir.

HTTP isteği gönder:

```bash
curl inlanefreight.com
```

Sayfayı sunucu ismiyle kaydet:

```bash
curl -O inlanefreight.com/index.html
```

Sayfayı kaydet:

```bash
curl inlanefreight.com -o site.html
```

Sessiz mod ile çalış:

```bash
curl -s -O inlanefreight.com
```

## Questions

```text
To get the flag, start the above exercise, then use cURL to download the file returned by '/download.php' in the server shown above.
```

??? tip "Steps"

    ```bash
    curl 94.237.49.11:44321/download.php
    ```
