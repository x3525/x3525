---
glightbox: true
icon: material/circle-small
---

# Network Services

## Install NFS

NFS, uzak sistemlerdeki dosyaları sanki yerel sistemde depolanmış gibi saklamamıza ve yönetmemize olanak tanıyan bir ağ protokolüdür. Ağlardaki dosyaların kolay ve verimli yönetilmesini sağlar.

```bash
sudo apt install -y nfs-kernel-server
```

## Server Status

```bash
sudo systemctl status nfs-kernel-server
```

NFS `/etc/exports` dosyası aracılığıyla yapılandırılabilir. Bu dosya hangi dizinlerin paylaşılması gerektiğini ve kullanıcılar ve sistemler için erişim haklarını belirtir. Aktarım hızı ve şifreleme kullanımı gibi ayarları yapılandırmak da mümkündür. NFS erişim hakları, hangi kullanıcıların ve sistemlerin paylaşılan dizinlere erişebileceğini ve hangi eylemleri gerçekleştirebileceklerini belirler. Bazı önemli erişim hakları şunlardır:

| Permissions | Description |
|---|---|
| `rw` | Paylaşılan dizine okuma ve yazma izinleri verir. |
| `ro` | Paylaşılan dizine salt okunur erişim sağlar. |
| `no_root_squash` | Kök kullanıcının haklarını sınırlamaz. |
| `root_squash` | Kök kullanıcısını normal kullanıcı haklarıyla sınırlar. |
| `sync` | Değişiklikler yalnızca sisteme kaydedildikten sonra aktarılır. |
| `async` | Veriler eşzamansız olarak aktarılır. Hızlıdır. Tutarsız olabilir. |

## Create NFS Share

Ağdaki başka bir bilgisayarla paylaşmak üzere makinemizde bir NFS Share klasörü oluşturabiliriz:

```bash
mkdir ~/shared
```

NFS yapılandırmasını ayarla:

```bash
echo '/home/estus/shared 10.0.2.5(rw,no_root_squash,sync)' >> /etc/exports
```

Burada 10.0.2.5 adresi `shared` klasörünü paylaşıma açtığımız bilgisayara ait adrestir.

## Mount NFS Share

NFS Share oluşturduktan sonra 10.0.2.4 makinesinde bulunan `shared` klasörüne erişim sağlayabiliriz. Bunun için öncelikle `shared` klasörünü mount etmeliyiz:

```bash
mkdir ~/target_nfs
mount 10.0.2.4:/home/estus/shared ~/target_nfs
```
