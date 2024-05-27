---
glightbox: true
---

# APT Incompatible with Kernel

APT `full-upgrade` sırasında oluşabilecek örnek bir hata:

```text title="Output" hl_lines="4"
...SNIP...

Error! Bad return status for module build on kernel: 6.5.0-3parrot1-amd64 (x86_64)
Consult /var/lib/dkms/realtek-rtl8188eus/5.3.9~git20230101.f8ead57/build/make.log for more information.

...SNIP...
```

Bu durumda kernel ile uyumsuz olan paketi kaldırmak bir çözüm olabilir:

```bash
sudo dkms remove realtek-rtl8188eus/5.3.9~git20230101.f8ead57
```
