---
glightbox: true
icon: material/help
---

# File System Management

## Mounting File systems at Boot

Sistem açılışında hangi dosya sistemlerinin nereye mount edildiği bilgisini aşağıdaki komut ile öğrenebiliriz:

```bash
cat /etc/fstab
```

## List Mounted Drives

Eğer `mount` komutunu tek başına kullanırsak şu anda mount edilmiş dosya sistemlerini görüntüleyebiliriz.

Mount bilgilerini görüntüle:

```bash
mount
```

USB mount et:

```bash
sudo mount /dev/sdb1 /mnt/usb
```

USB unmount et:

```bash
sudo umount /mnt/usb
```

## Questions

```text
How many partitions exist in our Pwnbox? (Format: 0)
```

??? tip "Steps"

    ```bash
    sudo fdisk -l /dev/vda
    ```
