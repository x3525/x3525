---
glightbox: true
icon: material/circle-small
---

# IP Addresses

Ağda bulunan her bilgisayar MAC adı verilen adresle tanımlanabilir. Bu, tek bir ağ içerisinde veri alışverişine izin verir. Uzak bilgisayar başka bir ağda bulunuyorsa, MAC adresi bilgisi, bağlantı kurmak için yeterli değildir. İnternette adresleme IPv4 ve/veya IPv6 adresi aracılığıyla yapılır.

## IPv4 Structure

IP adreslerini atamanın en yaygın yöntemi, 0-255 arasında değişen 8 bitlik (octet) 4 adet gruptan oluşan 32 bitlik bir ikili sayıdan oluşan adreslerdir. Bunlar daha kolay okunabilen ondalık sayılara dönüştürülür, noktalarla ayrılır ve noktalı ondalık gösterimle gösterilir.

Bir IPv4 adresi şöyle görünebilir:

| Notation | Presentation |
|---|---|
| Binary | 01111111.00000000.00000000.00000001 |
| Decimal | 127.0.0.1 |

IPv4 formatı 4.294.967.296 adet benzersiz adrese izin verir. IP adresi iki kısımdan oluşur:

1. Host
2. Network

Router, IP adresinin host kısmını atar. Ağ yöneticisi, IP adresinin network kısmını atar. [IANA](https://www.iana.org/), bu benzersiz IP adreslerini tahsis eder ve yönetir.

| Class | First Address | Last Address | Subnet Mask |
|---|---|---|---|
| A | 1.0.0.1 | 127.255.255.255 | 255.0.0.0 |
| B | 128.0.0.1 | 191.255.255.255 | 255.255.0.0 |
| C | 192.0.0.1 | 223.255.255.255 | 255.255.255.0 |
| D | 224.0.0.1 | 239.255.255.255 | Multicast |
| E | 240.0.0.1 | 255.255.255.255 | Reserved |

## Subnet Mask

Sınıfların küçük ağlara ayrılması alt ağların yardımıyla yapılır. Bu ayırma ağ maskeleri kullanılarak yapılır. IP adresi içindeki hangi bit konumlarının network kısmı, hangi bit konumlarının host kısmı olacağını açıklar.

| Class | First Address | Last Address | Subnet Mask |
|---|---|---|---|
| A | 1.0.0.1 | 127.255.255.255 | {==255.0.0.0==} |
| B | 128.0.0.1 | 191.255.255.255 | {==255.255.0.0==} |
| C | 192.0.0.1 | 223.255.255.255 | {==255.255.255.0==} |
| D | 224.0.0.1 | 239.255.255.255 | {==Multicast==} |
| E | 240.0.0.1 | 255.255.255.255 | {==Reserved==} |

## Network and Gateway Addresses

Bir alt ağdaki ilk veya son atanabilir IPv4 adresi varsayılan ağ geçidine atanır. Bu, teknik bir gereklilik değildir ancak bir standart haline gelmiştir.

| Class | First Address | Last Address | Subnet Mask |
|---|---|---|---|
| A | {==1.0.0.1==} | 127.255.255.255 | 255.0.0.0 |
| B | {==128.0.0.1==} | 191.255.255.255 | 255.255.0.0 |
| C | {==192.0.0.1==} | 223.255.255.255 | 255.255.255.0 |
| D | {==224.0.0.1==} | 239.255.255.255 | Multicast |
| E | {==240.0.0.1==} | 255.255.255.255 | Reserved |

## Broadcast Address

Bu IP adresinin görevi bir ağdaki tüm cihazları birbirine bağlamaktır. Ağda yapılan bir yayın, ağdaki tüm katılımcılara iletilen ve herhangi bir yanıt gerektirmeyen bir mesajdır. Bu şekilde ağın tüm diğer katılımcılarına aynı anda bir veri paketi gönderilir ve bunu yaparken, alıcıların, yayıncı ile iletişim kurmak için kullanabileceği IP adresi iletilir. Yayın için kullanılan IP adresi son IPv4 adresidir.

| Class | First Address | Last Address | Subnet Mask |
|---|---|---|---|
| A | 1.0.0.1 | {==127.255.255.255==} | 255.0.0.0 |
| B | 128.0.0.1 | {==191.255.255.255==} | 255.255.0.0 |
| C | 192.0.0.1 | {==223.255.255.255==} | 255.255.255.0 |
| D | 224.0.0.1 | {==239.255.255.255==} | Multicast |
| E | 240.0.0.1 | {==255.255.255.255==} | Reserved |

## CIDR

CIDR, bir temsil yöntemidir ve IPv4 adresi ile ağ sınıfları (A, B, C, D, E) arasındaki sabit atamanın yerine geçer. CIDR son eki IPv4 adresinin başlangıcından itibaren kaç bitin ağa ait olduğunu gösterir.

Örneğin 192.168.10.39/24 CIDR gösteriminde 24 sayısı, subnet mask kısmında başlangıçtan itibaren 24 adet 1 olduğu anlamına gelir:

| Binary | Decimal |
|---|---|
| 11111111.11111111.11111111.00000000 | 255.255.255.0 |
