---
glightbox: true
icon: material/circle-small
---

# Backup and Restore

## Rsync - Backup a local Directory to our Backup-Server

Rsync aracı kullanılarak yerel klasörde bulunan dosyalar bir yedekleme sunucusuna aktarılabilir. Dosyaların yalnızca değiştirilen kısımlarını ilettiği için büyük miktarda veri aktarımının gerekli olduğu durumlarda kullanışlıdır.

```bash
rsync -avz -e ssh /path/to/mydir user@backup_server:/path/to/backup/dir
```

Verilen `-a/--archive` seçeneği izinler, zaman damgaları gibi dosya özelliklerini korumaya yarar. Verilen `-v/--verbose` seçeneği detaylı çıktı üretir. Verilen `-z/--compress` seçeneği dosyaları sıkıştırmaya yarar. Verilen `-e/--rsh` seçeneği dosya aktarımı sırasında şifrelenmiş SSH bağlantısını kullanabilmemizi sağlar.

## Rsync - Restore our Backup

Daha önceden yedeklediğimiz dosyaları tekrar yüklemek için:

```bash
rsync -av user@backup_server:/path/to/backup/dir /path/to/mydir
```
