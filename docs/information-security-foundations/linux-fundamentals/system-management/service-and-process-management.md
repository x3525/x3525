---
glightbox: true
icon: material/help
---

# Service and Process Management

## Systemctl

Servisi el ile başlat:

```bash
sudo systemctl start ssh
```

Servis durumunu görüntüle:

```bash
sudo systemctl status ssh
```

Servisi, sistem açılışında otomatik başlayacak şekilde ayarla:

```bash
sudo systemctl enable ssh
```

Servislere ait günlük kayıtlarına erişmek için `journalctl` aracı kullanılabilir:

```bash
journalctl -u ssh.service
```

## Kill a Process

Bir işlem aşağıdaki durumlardan birinde bulunabilir:

* Running (Çalışıyor)
* Waiting (Bir olayı ya da sistem kaynağını bekliyor)
* Stopped (Çalışmıyor)
* Zombie (Çalışmıyor ancak işlem tablosunda girdileri mevcut)

Bir işlem `kill` komutuyla sonlandırılabilir. Bunun için işleme bir sinyal gönderilmelidir. En yaygın kullanılan sinyaller aşağıda verilmiştir:

| Signal | Value | Description |
|---|---|---|
| SIGHUP | 1 | Denetleyen uçbirimde Hang Up saptandı. |
| SIGINT | 2 | Kullanıcı bir işlemi kesmek için terminalde ++control+c++ tuş kombinasyonuna bastığında gönderilir. |
| SIGQUIT | 3 | Kullanıcı çıkmak için ++control+d++ tuş kombinasyonuna bastığında gönderilir. |
| SIGKILL | 9 | Bir işlemi derhal sonlandırır. |
| SIGTERM | 15 | Program sonlandırma sinyali. |
| SIGSTOP | 19 | Programı durdurur. |
| SIGTSTP | 20 | Kullanıcı bir hizmeti askıya almak için ++control+z++ tuş kombinasyonuna bastığında gönderilir. |

## Questions

```text
Use the "systemctl" command to list all units of services and submit the unit name with the description "Load AppArmor profiles managed internally by snapd" as the answer.
```

??? tip "Steps"

    ```bash
    systemctl | grep "Load AppArmor profiles managed internally by snapd"
    ```
