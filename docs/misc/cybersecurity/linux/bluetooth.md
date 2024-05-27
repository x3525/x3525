---
glightbox: true
---

# Bluetooth

Gerekli paketleri yükle:

```bash
pacman -S bluez bluez-utils
```

!!! info "Bluez Utils"

    Bazı platformlarda `bluez-utils` paketi mevcut olmayabilir. Bu durumda sadece `bluez` paketi yüklenebilir.

İlgili servisleri başlat:

```bash
sudo systemctl start bluetooth.service
```

Bluetooth kontrolcü gücünü etkin duruma getir:

```bash
bluetoothctl power on
```

Aracı interaktif modda başlat:

```bash
bluetoothctl
```

```text title="Output"
Waiting to connect to bluetoothd...[bluetooth]# hci0 new_settings: powered bondable ssp br/edr le secure-conn
[bluetooth]# Agent registered
[bluetooth]# [CHG] Controller F0:77:C3:XX:XX:XX Pairable: yes
[bluetooth]#
```

Keşif modunu başlat:

```text
scan on
```

```text title="Output"
[bluetooth]# SetDiscoveryFilter success
[bluetooth]# Discovery started
[bluetooth]# [CHG] Controller F0:77:C3:XX:XX:XX Discovering: yes
[bluetooth]# [NEW] Device D4:EA:57:XX:XX:XX Pebble M350s
[bluetooth]# [NEW] Device 4F:01:7A:XX:XX:XX 4F-01-7A-XX-XX-XX
[bluetooth]# [NEW] Device 55:9A:67:XX:XX:XX 55-9A-67-XX-XX-XX
[bluetooth]# [NEW] Device 4A:77:DA:XX:XX:XX 4A-77-DA-XX-XX-XX
[bluetooth]# [NEW] Device 75:47:91:XX:XX:XX 75-47-91-XX-XX-XX
[bluetooth]# [NEW] Device 7F:D8:8F:XX:XX:XX 7F-D8-8F-XX-XX-XX

...SNIP...
```

İstenilen cihazın MAC adresi çıktıda gözüktükten sonra keşfi sonlandır:

```text
scan off
```

Bluetooth cihazı ile bilgisayarı eşleştir:

```text
pair D4:EA:57:XX:XX:XX
```

Bluetooth cihazını güvenilen cihazlar listesine ekle:

```text
trust D4:EA:57:XX:XX:XX
```

Bluetooth cihazına bağlan:

```text
connect D4:EA:57:XX:XX:XX
```

Aracı kapat:

```text
exit
```
