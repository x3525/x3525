---
glightbox: true
---

# OpenVPN TUN/TAP Error

Sorunu çözmek için character tipinde (`c`) bir cihaz oluşturmak gerekebilir. Bu tipteki cihazlar, fiziksel olarak adreslenebilir depolama ortamlarına sahip değillerdir. Diğer cihazlarla iletişim kurmak için tekil karakterler (bytes, octets) gönderir ve alırlar.

Aşağıdaki komutu çalıştırmadan önce sistemi yeniden başlatmak faydalı olabilir:

```bash
sudo mknod /dev/net/tun c 10 200
```

!!! info "Non-Permanent"

    Yapılan değişiklikler kalıcı değildir, sistem yeniden başlatıldığında oluşturulan cihaz yok olacaktır.

| Command | Description |
|---|---|
| `/dev/net/tun` | Oluşturulacak cihazın ismi. |
| `c` | Oluşturulacak cihazın tipi. |
| `10` | Oluşturulacak cihazın major numarası. |
| `200` | Oluşturulacak cihazın minor numarası. |

Oluşturulan cihazın niteliklerini kontrol edelim:

| File type | Owner | Group | Others | Number of hard links | User | Group | Major number | Minor number | Date | File name |
|---|---|---|---|---|---|---|---|---|---|---|
| `c` | `rw-` | `rw-` | `rw-` | `1` | `root` | `root` | `10` | `200` | `Mar 11 10:50` | `/dev/net/tun` |

Major ve minor numaralarını incelemek için [bu](https://www.kernel.org/doc/Documentation/admin-guide/devices.txt) site kullanılabilir. Bu örnek için bakacak olursak:

| Major number (10) | Minor number (200) |
|---|---|
| Non-serial mice, misc features | TAP/TUN network device |
