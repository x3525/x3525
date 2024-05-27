---
glightbox: true
icon: material/circle-small
---

# Tcpdump Fundamentals

## Traffic Captures with Tcpdump

### Basic Capture Options

| Switch Command | Result |
|---|---|
| `-D` | Yakalama yapılabilecek tüm arayüzleri göster. |
| `-i` | Yakalamanın yapılacağı arayüzü seç. |
| `-n` | Bilgisayar adlarını çözümlemeyi devre dışı bırak. |
| `-nn` | Bilgisayar adlarını ve portları çözümlemeyi devre dışı bırak. |
| `-e` | Ethernet başlığını üst katman verileriyle birlikte yakala. |
| `-X` | Paket içeriğini Hex ve ASCII olara göster. |
| `-vv` | Gösterilen çıktının ayrıntı düzeyini artır. |
| `-c` | Belirli sayıda paket yakala ve çık. |
| `-s` | Bir paketin ne kadarının yakalanacağını belirle. |
| `-S` | Göreceli sıra numaralarını mutlak sıra numaralarına çevir. |
| `-q` | Daha az protokol bilgisi yazdır. |
| `-r` | Dosyadan oku. |
| `-w` | Dosyaya yaz. |

## File Input/Output with Tcpdump

### Save our PCAP Output to a File

```bash
sudo tcpdump -i eth0 -w ~/output.pcap
```

### Reading Output From a File

```bash
sudo tcpdump -i eth0 -r ~/output.pcap
```
