---
glightbox: true
icon: material/circle-small
---

# Network Types

## WAN

WAN genellikle The Internet olarak adlandırılır. Ağ ile uğraşırken genellikle bir WAN adresine ve LAN adresine sahip oluruz. WAN olan adres genellikle internet tarafından erişilen adrestir. WAN, çok sayıda LAN ağının bir araya gelmesinden oluşur. Birçok büyük şirket veya devlet kurumu dahili bir WAN (Intranet olarak da adlandırılır) ağına sahiptir. Ağın bir WAN ağı olup olmadığını belirlemenin bir yolu, BGP gibi WAN ağına özel bir yönlendirme protokolü kullanmak ve kullanılan IP şemasının [RFC-1918](https://www.arin.net/reference/research/statistics/address_filters/) (10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16) aralığında olmadığından emin olmaktır.

## LAN / WLAN

LAN (Local Area Network) ve WLAN (Wireless Local Area Network), genellikle yerel kullanım için belirlenmiş IP adreslerini (RFC-1918) kullanır.

## VPN

VPN kullanan bir cihaz internete bağlanacağı zaman bağlantı, ISP yerine özel VPN sunucusu üzerinden yönlendirilir. Üç ana VPN tipi vardır ancak üçünün de amacı, kullanıcının, sanki farklı bir ağa bağlıymış gibi hissetmesini sağlamaktır.

### Site-To-Site VPN

Bu VPN bağlantısı türünde hem istemci hem de sunucu birer ağ cihazıdır. Yaygın olarak şirket ağlarını internet üzerinden bir araya getirmek için kullanılır ve birden fazla konumun internet üzerinden sanki yerel ortamdaymış gibi iletişim kurmasına olanak tanır.

### Remote Access VPN

Bu tür bir VPN bağlantısı, istemcinin bilgisayarının, istemcinin ağındaymış gibi davranan sanal bir arayüz oluşturması ile gerçekleşir. Bu tür bir VPN yapısını analiz ederken dikkate alınması gereken önemli bir nokta, VPN ağına katılırken oluşturulan yönlendirme tablosudur. VPN yalnızca belirli ağlar için rotalar oluşturuyorsa (örneğin 10.10.10.0/24) buna Split Tunnel VPN adı verilir. Bu, internet bağlantısının VPN ağından dışarı çıkmadığı anlamına gelir.

### SSL VPN

Web tarayıcıları içinde oluşturulan bir VPN bağlantısıdır ve giderek daha yaygın hale gelmektedir. Bu sayede uygulamalar veya masaüstü oturumları web tarayıcısına aktarılabilir.
