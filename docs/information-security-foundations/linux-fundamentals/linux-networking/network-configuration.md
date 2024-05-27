---
glightbox: true
icon: material/circle-small
---

# Network Configuration

## Configuring Network Interfaces

### Editing DNS Settings

DNS bilgileri aşağıda verilen dosyaya girilmelidir:

```text title="/etc/resolv.conf" linenums="1"
nameserver 8.8.8.8
nameserver 8.8.4.4
```

Ancak bu dosyada yapılan değişiklikler sadece mevcut oturum için geçerli olacaktır. Herhangi bir ağ yapılandırma değişikliğinde ya da sistemin yeniden başlatılmasının ardından dosyadaki son değişiklikler kaybolacaktır. Bu yüzden aşağıdaki dosya da kullanılmalıdır:

```text title="/etc/network/interfaces" linenums="1"
auto eth0
iface eth0 inet static
  address 192.168.1.2
  netmask 255.255.255.0
  gateway 192.168.1.1
  dns-nameservers 8.8.8.8 8.8.4.4
```

## Network Access Control

NAC (Network Access Control), ağ güvenliğinin önemli bir bileşenidir. Güvenlik önlemlerini geliştirmek için kullanılabilecek farklı NAC teknolojileri şunlardır:

* DAC (Discretionary Access Control)
* MAC (Mandatory Access Control)
* RBAC (Role-Based Access Control)

## Troubleshooting

Çeşitli araçlar Linux sistemlerinde ağ sorunlarını tanımlamamıza ve çözmemize yardımcı olabilir. En sık kullanılan araçlardan bazıları şunlardır:

* Ping
* Traceroute
* Netstat

### Ping

İki cihaz arasındaki bağlantıyı test etmek için kullanılan bir komut satırı aracıdır. Paketleri uzaktaki bir bilgisayara gönderir ve bunların geri gönderilme süresini ölçer.

```bash
ping 8.8.8.8
```

### Traceroute

Uzaktaki bir bilgisayara artan TTL (Time-to-Live) değerlerine sahip paketler gönderir ve paketlerin geçtiği cihazların IP adreslerini görüntüler.

```bash
traceroute www.inlanefreight.com
```

```text title="Output"
traceroute to www.inlanefreight.com (10.10.15.45), 30 hops max, 60 byte packets
 1  * * *
 2  172.16.152.4 (172.16.152.4)  2.716 ms  2.700 ms  2.730 ms
 3  * * *
 4  125.172.12.14 (125.172.12.14)  7.147 ms  7.132 ms 153.65.7.223 (153.65.7.223)  7.393 ms
```

* Bu örnekte hedef bilgisayar 10.10.15.45 IP adresine sahiptir ve izin verilen maksimum atlama (hop) sayısı 30 olarak görülmektedir.
* İkinci satır, 172.16.152.4 IP adresine sahip ilk atlamayı ve gönderilen paketlerin her birinin ağ geçidine ulaşması için geçen süreyi gösterir.
* Üçüncü satır, ikinci atlamayı gösterir. Burada IP adresi yerine üç yıldız işareti olduğu görülmektedir. Bu, cihazdan yanıt gelmediği manasına gelir.
* Dördüncü satır, 125.172.12.14 IP adresine sahip üçüncü atlamayı ve gönderilen paketlerin her birinin ağ geçidine ulaşması için geçen süreyi gösterir.

### Netstat

Aktif ağ bağlantılarını ve bunlarla ilişkili bağlantı noktalarını görüntülemek için kullanılır. Ağ trafiğini tanımlamak ve bağlantı sorunlarını gidermek için kullanılabilir.

```bash
netstat -a
```
