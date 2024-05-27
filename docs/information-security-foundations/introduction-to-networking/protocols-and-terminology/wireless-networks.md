---
glightbox: true
icon: material/circle-small
---

# Wireless Networks

## WiFi Connection

Cihazlar, SSID ve parola gibi doğru ağ ayarlarıyla yapılandırılmalıdır. Bu nedenle dizüstü bilgisayarlar yönlendiriciye bağlanmak için IEEE 802.11 adı verilen bir kablosuz ağ protokolü kullanır. Bu protokol, kablosuz cihazların birbirleriyle ve WAP (Wireless Access Point) cihazlarıyla nasıl iletişim kurulacağının teknik ayrıntılarını tanımlar. Bir cihaz bir Wi-Fi ağına katılmak istediğinde bağlantı sürecini başlatmak için WAP cihazına bir istek gönderir. Bu istek Connection Request Frame ya da Association Request olarak bilinir ve IEEE 802.11 kablosuz ağ protokolü kullanılarak gönderilir.

## Wireless Hardening

### Disabling Broadcasting

SSID (Service Set Identifier) yayınının devre dışı bırakılması ağın keşfedilmesini zorlaştırır. Bu sayede WAP cihazı Beacon Frame iletmeyecek ve ağ, ağa bağlı olmayan cihazlar tarafından görülemeyecektir.

### WPA

WPA (Wi-Fi Protected Access), kablosuz iletişim için güçlü şifreleme ve kimlik doğrulama sağlayarak hassas verilerin ele geçirilmesine karşı koruma sağlar.

### MAC Filtering

MAC filtreleme, belirli cihazlardan gelen bağlantıları MAC adreslerine göre kabul etmeye veya reddetmeye olanak tanıyan bir güvenlik önlemidir.

### Deploying EAP-TLS

EAP-TLS, kablosuz iletişimlerin kimliğini doğrulamak ve şifrelemek için kullanılan bir güvenlik protokolüdür. Bu protokol, istemcilerin kimliğini doğrulamak ve güvenli bağlantılar kurmak için dijital sertifikalar ve PKI kullanır.
