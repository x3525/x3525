---
glightbox: true
icon: material/help
---

# HTTP Headers

## General Headers

Genel başlıklar hem HTTP isteklerinde hem de HTTP yanıtlarında kullanılır. Mesajı tanımlamak için kullanılırlar.

| Header | Description |
|---|---|
| Date | Mesajın geldiği tarih ve saati tutar. Standart UTC saat dilimi tercih edilmelidir. |
| Connection | İstek bittikten sonra mevcut ağ bağlantısının aktif kalıp kalmayacağını belirler. Bu başlık için yaygın olarak kullanılan iki değer, Close ve Keep-Alive değerleridir. |

## Entity Headers

Varlık başlıkları hem HTTP isteklerinde hem de HTTP yanıtlarında kullanılır. Bu başlıklar bir mesajın aktardığı içeriği (varlığı) tanımlamak için kullanılır. Genellikle yanıtlarda ve POST veya PUT isteklerinde bulunurlar.

| Header | Description |
|---|---|
| Content-Type | Aktarılan kaynağın türünü tanımlamak için kullanılır. Değer, istemci tarafındaki tarayıcılar tarafından otomatik olarak eklenir ve sunucu yanıtında döndürülür. |
| Content-Length | Varlığın boyutunu tutar. Sunucunun mesaj gövdesinden veri okuyabilmesi için gereklidir. Tarayıcılar tarafından otomatik olarak oluşturulur. |
| Content-Encoding | Veriler aktarılmadan önce birden fazla dönüşüme uğrayabilir. Örneğin mesaj boyutunu küçültmek için büyük miktarda veri sıkıştırılabilir. Verileri sıkıştırmak için kullanılan kodlamanın türü bu başlık kullanılarak belirtilmelidir. |
| Media-Type | Aktarılan verileri tanımlamak için kullanılır. Bu başlık, sunucunun girdimizi yorumlamasını sağlamada çok önemli bir rol oynayabilir. |
| Boundary | Aynı mesajda birden fazla içerik olduğunda içeriği ayırmak için işaretçi görevi görür. |

## Request Headers

İstek başlıkları, HTTP isteklerinde kullanılır ve mesajın içeriğiyle ilgili değildir.

| Header | Description |
|---|---|
| Host | Kaynak için sorgulanan bilgisayarı belirtmede kullanılır. Domain veya IP adresi olabilir. |
| User-Agent | İstekte bulunan istemciyi tanımlamak için kullanılır. |
| Referer | Geçerli isteğin nereden geldiğini belirtir. Bu başlığa güvenmek tehlikeli olabilir, çünkü kolayca değiştirilebilir ve istenmeyen sonuçlara yol açabilir. |
| Accept | İstemcinin hangi medya türlerini kabul ettiğini belirtir. |
| Cookie | Çerez, tanımlayıcı görevi gören bir veri parçasıdır. Hem istemci hem de sunucu tarafında saklanabilir. Çerezler istek başına sunucuya iletilir, böylece istemcinin erişimi korunur. Çerezler ayrıca kullanıcı tercihlerini kaydetmek veya oturum takibi gibi başka amaçlara da hizmet edebilir. |
| Authorization | Sunucunun istemcileri tanımlamasının başka bir yöntemidir. Başarılı kimlik doğrulamanın ardından sunucu, istemciye özel bir token döndürür. Çerezlerden farklı olarak token, yalnızca istemci tarafında depolanır ve istek başına sunucu tarafından alınır. |

## Response Headers

Yanıt başlıkları, HTTP yanıtlarında kullanılır ve içerikle ilişkili değildir.

| Header | Description |
|---|---|
| Server | İsteği işleyen HTTP sunucusu hakkındaki bilgileri içerir. |
| Set-Cookie | İstemcinin tanımlanması için gerekli çerezleri içerir. Tarayıcılar çerezleri ayrıştırır ve gelecekteki istekler için saklar. |
| WWW-Authenticate | İstenen kaynağa erişmek için gereken kimlik doğrulama türü hakkında bilgi verir. |

## Security Headers

Güvenlik başlıkları, web sitesine erişirken tarayıcının uyması gereken belirli kuralları ve politikaları belirtmek için kullanılan HTTP yanıt başlıkları sınıfıdır.

| Header | Description |
|---|---|
| Content-Security-Policy | Web sitesinin dışarıdan enjekte edilen kaynaklara yönelik politikasını belirler. Bu başlık, tarayıcıya, yalnızca belirli güvenilir alanlardan gelen kaynakları kabul etmesi talimatını verir, böylece XSS gibi saldırılar önlenmiş olur. |
| Strict-Transport-Security | Web sitelerine HTTP protokolü üzerinden erişilmesini engeller ve tüm iletişimin güvenli HTTPS protokolü üzerinden taşınmasını gerekli kılar. |
| Referrer-Policy | Tarayıcının Referer başlığı aracılığıyla belirtilen değeri içerip içermeyeceğini belirler. Web sitesinde gezinirken hassas bilgilerin ifşa edilmesini önlemeye yardımcı olabilir. |

## cURL

Yalnızca HEAD bilgisini talep et:

```bash
curl -I https://www.inlanefreight.com
```

User-Agent başlığını ayarla:

```bash
curl https://www.inlanefreight.com -A 'Mozilla/5.0'
```

## Questions

```text
The server above loads the flag after the page is loaded. Use the Network tab in the browser devtools to see what requests are made by the page, and find the request to the flag.
```

??? tip "Steps"

    Soruda verilen hedef makine adresini tarayıcı arama çubuğuna gir ve adrese git.

    Sayfayı yenile.

    DevTools aracındaki Network sekmesinde flag dosyasını bul.

    Dosyanın bulunduğu URL için cURL ile bir istek gönder:

    ```bash
    curl http://94.237.56.76:37822/flag_327a6c4304ad5938eaf0efb6cc3e53dc.txt
    ```

    Yanıt olarak flag bilgisi gönderilecektir.
