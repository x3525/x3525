---
glightbox: true
icon: material/circle-small
---

# HTTP Methods and Codes

## [Request Methods](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods)

| Method | Description |
|---|---|
| GET | Belirli bir kaynak ister. Sorgu dizeleri aracılığıyla sunucuya ek veriler aktarılabilir. |
| POST | Sunucuya veri gönderir. Birden çok girdi türünü işleyebilir. Bu veriler başlıklardan sonra bulunan istek gövdesine eklenir. POST yöntemi genellikle bilgi gönderirken (oturum açma bilgileri) veya bir web sitesine resim veya belge gibi veriler yüklenirken kullanılır. |
| HEAD | Sunucuya bir GET isteği yapıldığında döndürülecek başlıkları ister. İstek gövdesini döndürmez ve genellikle kaynakları indirmeden önce yanıt uzunluğunu kontrol etmek için yapılır. |
| PUT | Sunucuda yeni kaynaklar oluşturur. Bu yönteme uygun kontroller olmadan izin verilmesi kötü amaçlı kaynakların yüklenmesine yol açabilir. |
| DELETE | Web sunucusundaki bir kaynağı siler. Düzgün bir şekilde güvence altına alınmazsa web sunucusundaki kritik dosyaların silinmesiyle DoS (Denial of Service) saldırısına neden olabilir. |
| OPTIONS | Sunucu tarafından kabul edilen yöntemler gibi sunucu hakkındaki bilgileri döndürür. |
| PATCH | Belirtilen konumdaki kaynağa kısmi değişiklikler uygular. |

## [Response Codes](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status)

| Type | Description |
|---|---|
| 1xx | Bilgi sağlar ve talebin işlenmesini etkilemez. |
| 2xx | Bir istek başarılı olduğunda geri döndürülür. |
| 3xx | İstemci yeniden yönlendirildiğinde döndürülür. |
| 4xx | İstemciden gelen uygunsuz talepleri belirtir. |
| 5xx | HTTP sunucusunun kendisinde bir sorun olduğunda döndürülür. |
