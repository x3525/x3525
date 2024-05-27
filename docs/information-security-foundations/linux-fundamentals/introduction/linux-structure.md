---
glightbox: true
icon: material/circle-small
---

# Linux Structure

## Philosophy

Linux sistemleri aşağıda verilen 5 temel prensibi takip eder:

1. Her şey bir dosyadır.
2. Küçük, tek bir amaca hizmet eden birçok araç bulundurur.
3. Farklı amaçlara hizmet eden araçlar birleştirilerek daha kompleks görevler yürütülebilir.
4. Grafiksel kullanıcı arayüzlerinden mümkün olduğunca kaçınarak, işletim sistemi üzerinde daha fazla kontrol sağlayan terminal ile çalışmak tercih edilen yöntemdir.
5. Yapılandırma verileri metin dosyalarında saklanır.

## Components

| Component | Description |
|---|---|
| Bootloader | İşletim sistemini başlatmak için önyükleme işlemini yönlendirmek üzere çalışan bir kod parçasıdır. ParrotOS Linux Bootloader olarak GRUB (Grand Unified Bootloader) kullanır. |
| OS Kernel | Sistemin I/O kaynaklarını donanım düzeyinde yönetir. |
| Daemons | Arka plan hizmetlerine verilen isimdir. Bu küçük programlar bilgisayarda önyükleme yaptıktan veya oturum açtıktan sonra yüklenir. |
| OS Shell | Komut dili tercümanı ya da komut satırı, işletim sistemi ile kullanıcı arasındaki arayüzdür. Bu arayüz, kullanıcının işletim sistemine ne yapması gerektiğini söylemesine olanak tanır. En sık kullanılan shell tipleri: Bash, Tcsh/Csh, Ksh, Zsh ve Fish. |
| Graphics Server | Grafik programlarının yerel olarak veya uzaktan çalıştırılmasına olanak tanıyan ve X sunucusu adı verilen bir grafiksel alt sistem sağlar. |
| Window Manager | GUI olarak da bilinir. GNOME, KDE, MATE ve Cinnamon gibi birçok GUI seçeneği vardır. Bir masaüstü ortamında dosya ve web tarayıcıları gibi çeşitli uygulamalar bulunur. |
| Utilities | Uygulamalar veya yardımcı programlar, kullanıcı veya başka bir program için belirli işlevleri gerçekleştiren araçlardır. |

## File System Hierarchy

![](../assets/images/new-filesystem.png)

| Path | Description |
|---|---|
| `/` | Üst düzey dizin tüm dosya sistemleri için bağlantı noktasıdır. |
| `/bin` | Temel yürütülebilir dosyaları içerir. |
| `/boot` | Sistemi başlatmak için gereken dosyalardan oluşur. |
| `/dev` | Sisteme bağlı her donanım için aygıt dosyalarını içerir. |
| `/etc` | Yapılandırma dosyaları ve diğer her şeyi içerir. |
| `/home` | Sistemdeki her kullanıcıya ait depolama alanıdır. |
| `/kernel` | Kernel modüllerini ve kernel ile ilgili diğer dosyaları içerir. |
| `/lib` | Önyükleme için paylaşılan kütüphaneleri içerir. |
| `/lost+found` | Kurtarılan dosyaları depolamak için kullanılır. |
| `/media` | USB sürücüler gibi çıkarılabilir medya aygıtları buraya bağlanır. |
| `/mnt` | Normal dosya sistemleri için geçici bağlama noktasıdır. |
| `/opt` | Üçüncü taraf araçlar gibi dosyaları içerir. |
| `/proc` | Sistemdeki işlemlerin, sıradan dosyalar olarak tutulduğu dizindir. |
| `/root` | Kök kullanıcının ana dizinidir. |
| `/sbin` | Sistem yürütülebilir dosyalarını içerir. |
| `/tmp` | Geçici dosyaları depolamak için kullanır. |
| `/usr` | Yürütülebilir dosyalar, man dosyaları vb. içerir. |
| `/var` | Günlükler gibi değişken veri dosyalarını içerir. |
