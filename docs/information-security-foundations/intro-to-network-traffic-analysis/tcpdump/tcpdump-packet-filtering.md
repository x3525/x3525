---
glightbox: true
icon: material/circle-small
---

# Tcpdump Packet Filtering

## Filtering and Advanced Syntax Options

### Helpful TCPDump Filters

| Filter | Result |
|---|---|
| `host` | Belirtilen bilgisayar için görünür trafiği filtrele. |
| `src` | Kaynak için kullanılır. |
| `dst` | Hedef için kullanılır. |
| `net` | Belirtilen ağdan kaynaklanan trafiği göster. |
| `proto` | Belirtilen protokol için filtre uygula. |
| `port` | Kaynak veya hedef için belirtilen port trafiğini göster. |
| `portrange` | Port aralığı belirle. |
| `less` | Belirli bir boyuttaki paketi ara. |
| `greater` | Belirli bir boyuttaki paketi ara. |
| `and` | İki farklı filtreyi birleştir. |
| `or` | İki koşuldan herhangi birinde eşleşmeye izin ver. |
| `not` | Filtreyi tersine çevir. |

## Interpreting Tips and Tricks

### Hunting For a SYN Flag

Aşağıdaki komut SYN bayrağı etkin olan sonuçları listeler:

```bash
sudo tcpdump -i eth0 'tcp[13] &2 != 0'
```

Açıklayacak olursak:

| Command | Description |
|---|---|
| `tcp[13]` | TCP başlığından 13. bayta (control bits) bak. |
| `&2` | Control bits kısmında 2. bite (SYN) bak. |
| `!= 0` | Değer sıfır değilse SYN bayrağı aktif demektir. |

Bu komutun tam olarak nasıl çalıştığını anlamak için TCP başlık yapısını bilmek gereklidir. Ayrıntılı bilgi için [RFC 793](https://www.rfc-editor.org/rfc/rfc793#section-3.1) metnine bakılabilir.
