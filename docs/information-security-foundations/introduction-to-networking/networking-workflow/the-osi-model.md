---
glightbox: true
icon: material/circle-small
---

# The OSI Model

ISO/OSI standardının tanımlanmasındaki amaç, farklı teknik sistemlerin, çeşitli cihaz ve teknolojiler aracılığıyla iletişimini sağlayan ve uyumluluk sağlayan bir referans modeli oluşturmaktır. OSI modeli bu amaca ulaşmak için birbirini temel alan yedi farklı katman kullanır. Bu katmanlar gönderilen paketlerin geçtiği her bağlantının kurulmasındaki aşamaları temsil eder.

| Layer Number | Layer Name | Function |
|---|---|---|
| 7 | Application | Veri girişini ve çıkışını kontrol eder ve uygulama işlevlerini sağlar. |
| 6 | Presentation | Verilerin sisteme bağlı sunumunu uygulamadan bağımsız bir forma aktarmak için kullanılır. |
| 5 | Session | İki sistem arasındaki mantıksal bağlantıyı kontrol eder ve bağlantı kesintilerini veya diğer sorunları önler. |
| 4 | Transport | Aktarılan verilerin uçtan uca kontrolü için kullanılır. Tıkanıklık durumlarını algılayıp önleyebilir ve veri akışlarını bölümlere ayırabilir. |
| 3 | Network | Devre anahtarlamalı ağlarda bağlantılar kurulur ve veri paketleri paket anahtarlamalı ağlarda iletilir. Veriler göndericiden alıcıya tüm ağ üzerinden iletilir. |
| 2 | Data Link | İlgili ortamda güvenilir ve hatasız iletim sağlar. Bu amaçla birinci katmandan gelen bit akışları bloklara veya çerçevelere bölünür. |
| 1 | Physical | Kullanılan iletim teknikleri elektrik sinyalleri, optik sinyaller veya elektromanyetik dalgalardır. İletim kablolu veya kablosuz iletim hatlarında gerçekleşir. |

Her katmanda kesin olarak tanımlanmış görevler gerçekleştirilir ve komşu katmanlara yönelik arayüzler tam olarak tanımlanır. Her katman, doğrudan üstündeki katmanın kullanımına yönelik hizmetler sunar. Bu hizmetleri kullanılabilir hale getirmek için ilgili katman, altındaki katmanın hizmetlerini kullanır ve kendi katmanının görevlerini gerçekleştirir.

OSI modelinin yedi katmanının tümü en az iki kez çalıştırılır. Bu nedenle iletişimin güvenliğini, güvenilirliğini ve performansını sağlamak için, ayrı katmanlarda çok sayıda farklı görevin gerçekleştirilmesi gerekir.

Bir uygulama diğer sisteme paket gönderdiğinde, sistem, yukarıda gösterilen katmanları yedinci katmandan birinci katmana kadar çalıştırır ve alıcı sistem, alınan paketi birinci katmandan yedinci katmana kadar açar.
