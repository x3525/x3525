---
glightbox: true
---

# Add Windows to GRUB Menu

Dual boot kurulumunun ardından GRUB menüsünde Windows seçeneği gözükmüyorsa, aşağıda verilen adımları uygulamak bu sorunu düzeltebilir.

Diskleri görüntüle:

```bash
sudo fdisk -l
```

```text title="Output" hl_lines="2"
Device             Start        End   Sectors   Size Type
/dev/nvme0n1p1      2048    1050623   1048576   512M EFI System
/dev/nvme0n1p2   1050624  874729471 873678848 416.6G Linux filesystem
/dev/nvme0n1p3 874729472  874762239     32768    16M Microsoft reserved
/dev/nvme0n1p4 874762240 1000214527 125452288  59.8G Microsoft basic data
```

Windows EFI bölümünün (`/dev/nvme0n1p1`) UUID bilgisini öğren:

```bash
sudo blkid /dev/nvme0n1p1
```

```text title="Output"
/dev/nvme0n1p1: UUID="3E1C-69EB" BLOCK_SIZE="512" TYPE="vfat" PARTLABEL="EFI system partition" PARTUUID="47bd502c-92fd-4782-882b-d4fc81e968ce"
```

Yönetici haklarıyla `/etc/grub.d/40_custom` dosyasını aç ve bu dosyaya aşağıda verilen satırları ekle:

```text title="/etc/grub.d/40_custom" linenums="1" hl_lines="2"
menuentry "Windows" {
    search --fs-uuid --no-floppy --set=root 3E1C-69EB
    chainloader (${root})/EFI/Microsoft/Boot/bootmgfw.efi
}
```

!!! warning "UUID"

    Dosyada bulunan `--set=root` ifadesinden sonra verilen değer UUID bilgisi olacaktır.

Değişiklikleri kaydedip dosyayı kapat ve ardından aşağıdaki komutu çalıştır:

```bash
sudo grub-mkconfig -o /boot/grub/grub.cfg
```

Bilgisayarı yeniden başlat:

```bash
reboot
```
