---
glightbox: true
icon: material/circle-small
---

# MAC Addresses

Bir ağdaki her bilgisayarın, 48 bitlik (6 sekizli) MAC adresi vardır. MAC, ağ arayüzlerinin fiziksel adresidir. MAC adresi için birkaç farklı standart vardır:

* Ethernet (IEEE 802.3)
* Bluetooth (IEEE 802.15)
* WLAN (IEEE 802.11)

Bunun nedeni, MAC adresinin bir bilgisayarın fiziksel bağlantısını adreslemesidir. Her ağ kartının bir kez yapılandırılan kendi MAC adresi vardır.

MAC adresi toplam 6 bayttan oluşur. MAC adresinin ilk yarısı (3 bayt) IEEE tarafından ilgili üreticiler için tanımlanan OUI kısmıdır. MAC adresinin son yarısı ise üreticilerin atadığı NIC kısmıdır. Üretici bu bit dizesini yalnızca bir kez ayarlar ve böylece tam adresin benzersiz olmasını sağlar.

IP hedef adresine sahip bir bilgisayar aynı alt ağda yer alıyorsa, teslimat, doğrudan hedef bilgisayarın fiziksel adresine yapılır. Ancak bu bilgisayar farklı bir alt ağa aitse, Ethernet çerçevesi, sorumlu router cihazın (default gateway) MAC adresine yönlendirilir.

## MAC Unicast

MAC adresinin ilk sekizli kısmında bulunan sondan 1. bit 0 (sıfır) ise, MAC adresi, Unicast olarak tanımlanır. Unicast ile gönderilen paket yalnızca belirli bir bilgisayara ulaşır.

## MAC Multicast

MAC adresinin ilk sekizli kısmında bulunan sondan 1. bit 1 ise, MAC adresi, Multicast olarak tanımlanır. Multicast ile gönderilen paket yerel ağdaki tüm bilgisayarlara yalnızca bir kez gönderilir ve daha sonra yapılandırmalarına göre paketin kabul edilip edilmeyeceğine karar verilir.

## Global OUI

MAC adresinin ilk sekizli kısmında bulunan sondan 2. bit 0 (sıfır) ise, MAC adresi, Global OUI olarak tanımlanır.

## Locally Administrated

MAC adresinin ilk sekizli kısmında bulunan sondan 2. bit 1 ise, MAC adresi, Locally Administrated olarak tanımlanır.
