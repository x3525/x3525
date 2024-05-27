---
glightbox: true
icon: material/help
---

# System Information

| Command | Description |
|---|---|
| `whoami` | Geçerli kullanıcı adını görüntüler. |
| `id` | Kullanıcı kimliğini görüntüler. |
| `hostname` | Mevcut makinenin adını ayarlar veya görüntüler. |
| `uname` | Sistem donanımı hakkındaki bilgileri görüntüler. |
| `pwd` | Çalışma dizini adını görüntüler. |
| `ifconfig` | Ağ arayüzü parametrelerini yapılandırmak için kullanılır. |
| `netstat` | Ağ durumunu görüntüler. |
| `ss` | Soketleri araştırmak için kullanılır. |
| `ps` | İşlem durumunu görüntüler. |
| `who` | Kimin oturum açtığını görüntüler. |
| `env` | Mevcut ortamı görüntüler. |
| `lsblk` | Blok cihazlarını listeler. |
| `lsusb` | USB cihazlarını listeler. |
| `lsof` | Açılan dosyaları listeler. |
| `lspci` | PCI cihazlarını listeler. |

## Questions

```text
Find out the machine hardware name and submit it as the answer.
```

??? tip "Steps"

    Öncelikle makineye SSH ile bağlanmalıyız:

    ```bash
    ssh htb-student@10.129.200.91
    ```

    Ardından aşağıdaki komutu girerek cevabı alabiliriz:

    ```bash
    uname -m
    ```

```text
What is the path to htb-student's home directory?
```

??? tip "Steps"

    ```bash
    cd ~
    pwd
    ```

```text
What is the path to the htb-student's mail?
```

??? tip "Steps"

    ```bash
    env | grep mail
    ```

```text
Which shell is specified for the htb-student user?
```

??? tip "Steps"

    Açık olan dosyalardan mevcut işlemin PID bilgisine göre listele:

    ```bash
    lsof -p $$
    ```

```text
Which kernel version is installed on the system? (Format: 1.22.3)
```

??? tip "Steps"

    ```bash
    uname -r
    ```

```text
What is the name of the network interface that MTU is set to 1500?
```

??? tip "Steps"

    ```bash
    ifconfig | grep "mtu 1500"
    ```
