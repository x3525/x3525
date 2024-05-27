---
glightbox: true
icon: material/circle-small
---

# Linux

## LUKS Encryption

LUKS (Linux Unified Key Setup), Linux sistemleri için tasarlanmış bir disk şifreleme yöntemidir. Yeni bir sistem kurmadan önce diskimizi bu yöntemi kullanarak şifreleyebiliriz.

LUKS, LVM (Logical Volume Manager) yapısı ile kullanılabilir. LVM bir disk yapılandırma yöneticisidir. Boyut tahmini yapılamayan senaryolarda avantaj sağlamaktadır. Örneğin 3 GB boyutunda 3 adet diskimiz olsun ve ev dizini için 6 GB yer gerekli olsun. LVM sayesinde 2 adet 3 GB diski tek bir 6 GB disk gibi göstererek kullanabiliriz. Başka bir örnek olarak ev dizini için 100 GB yer ayrılmış ama sadece 50 GB kullanımda olsun. Başka bir dizin için 20 GB yer ihtiyacı olursa, ev dizinimizde kullanılmayan 50 GB alandan 20 GB alanı rahatlıkla bu dizine aktarabiliriz.

## Updates & Package Manager

### ParrotOS Sources List

APT paket yöneticisi, kaynak listesini kullanarak HTTP ve FTP sunucularına erişebilir ve gerektiğinde paketleri buradan kurabilir. Bu liste `/etc/apt` dizini altında `sources.list` dosyasında bulunur. ParrotOS için `/etc/apt/sources.list.d` dizini altında `parrot.list` dosyası da bulunmaktadır.

### Updating ParrotOS

Aşağıdaki komut ile sistem güncel duruma getirilebilir:

```bash
sudo apt update && sudo apt full-upgrade -y && sudo apt autoremove -y && sudo apt autoclean -y
```

Burada `autoremove` seçeneği, önceden kaldırılmış bir paketin bağımlılığı (dependency) olarak yüklenen paketleri kaldırır. Farklı olarak `autoclean` seçeneği ise, kaynak depoda daha yeni bir sürümü olan ya da kaynak depoda olmadığı için artık indirilemeyen paketlere ait önbellekte saklanan tüm arşivleri kaldırır.

### Installing Additional Tools from a List

Ayrı olarak kurmak isteğimiz bazı araçlar varsa bunları tek tek girmek yerine bir liste kullanabiliriz. Örneğin aşağıdaki gibi, içerisinde kuracağımız araç isimlerini içeren bir dosya olsun:

```text title="tools.list" linenums="1"
hashcat
ncat
netcat
nmap
wireshark
```

Aşağıdaki komutu kullanarak bu araçların kurulmasını sağlayabiliriz:

```bash
sudo apt install -y $(cat tools.list | tr "\n" " ")
```

Burada `tr` komutu dosya içindeki `\n` karakterlerini boşluk karakterlerine çevirir.

## Terminal Adjustment

### Customize Bash Prompt

Linux terminalini ilk açtığımızda gözüken Bash isteminin nasıl gözükeceğini PS1 değişkeni ile özelleştirebiliriz. Bu iş için [Bash Prompt Generator](https://bash-prompt-generator.org/) sitesini kullanabiliriz. Burada oluşturduğumuz örnek bir PS1 değişken değerini `.bashrc` dosyasına ekleyerek özelleştirmeyi kalıcı hale getirebiliriz.

Dosyanın (`.bashrc`) yedeğini al:

```bash
cp ~/.bashrc ~/.bashrc.bak
```

Bash istemini özelleştir:

```bash
echo 'export PS1="\[\e[32m\]┌──(\[\e[94m\]\u\[\e[0m\]@\[\e[94m\]\h\[\e[32m\])\[\e[0m\]-\[\e[32m\][\[\e[0m\]\w\[\e[32m\]]\[\e[0m\]-\[\e[32m\][\[\e[0m\]\j\[\e[32m\]]\n└─\[\e[94m\]\\$ \[\e[0m\]"' >> ~/.bashrc
```

### Customized Bash Prompt

Özelleştirme sonrası Bash istemi aşağıdaki gibi bir görünüme sahip olacaktır:

```text
┌──(username@hostname)-[~]-[0]
└─$
```

## Automation

### Bash Customization Script - Prompt.sh

Yeni bir sistem kurarken, Bash istemini özelleştirmek gibi birden fazla işlemi otomatik olarak gerçekleştiren bir script yazmak faydalı olacaktır. Örneğin aşağıda verilen script, Bash istemini özelleştirmek için kullanılabilir:

```bash title="Prompt.sh" linenums="1"
#!/bin/bash

# Dosyanın (.bashrc) yedeğini al
cp ~/.bashrc ~/.bashrc.bak

# Bash istemini özelleştir
echo 'export PS1="\[\e[32m\]┌──(\[\e[94m\]\u\[\e[0m\]@\[\e[94m\]\h\[\e[32m\])\[\e[0m\]-\[\e[32m\][\[\e[0m\]\w\[\e[32m\]]\[\e[0m\]-\[\e[32m\][\[\e[0m\]\j\[\e[32m\]]\n└─\[\e[94m\]\\$ \[\e[0m\]"' >> ~/.bashrc
```

### Request Prompt.sh

Script dosyasını kendimize ait olan bir VPS (Virtual Private Server) üzerinden ulaşılabilir duruma getirirsek, aşağıdaki komutla bu script dosyasına erişebilir ve çalıştırabiliriz:

```bash
curl -s http://myvps.vps-provider.net/Prompt.sh | bash
```

## VM Encryption

LVM şifreleme özelliğine ek olarak, kullandığımız sanal makinenin ayarlarından şifrelemeyi etkinleştirerek ekstra bir güvenlik katmanı ekleyebiliriz.
