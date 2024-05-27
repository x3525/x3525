---
glightbox: true
icon: material/help
---

# Task Scheduling

Linux sistemlerinde `systemd` aracı kullanılarak işlemler, belirli bir zaman ya da zaman aralığında çalışacak şekilde ayarlanabilir. Bunun için aşağıdaki adımlar takip edilmelidir:

1. Zamanlayıcı oluştur.
2. Servis oluştur.
3. Zamanlayıcıyı aktifleştir.

## Create a Timer

```bash
sudo touch /etc/systemd/system/mytimer.timer
```

Oluşturulan dosyaya aşağıda verilen değerler girilir:

```text title="mytimer.timer" linenums="1"
[Unit]
Description=My Timer
Requires=mytimer.service

[Timer]
Unit=mytimer.service
OnBootSec=3min
#OnUnitActiveSec=1hour

[Install]
WantedBy=timers.target
```

Burada `Unit` kısmı zamanlayıcıya ait açıklamayı ve gereklilikleri içerir. Ardından gelen `Timer` kısmı zamanlayıcının ne zaman çalışacağı bilgisini içerir. Script dosyasının sistem açılışında bir kez çalışması gerekiyorsa `OnBootSec` seçeneği, düzenli aralıklarla çalışması gerekiyorsa `OnUnitActiveSec` seçeneği kullanılabilir. Son olarak `Install` kısmı zamanlayıcının nereye kurulacağı bilgisini içerir.

## Create a Service

Zamanlayıcı oluşturulduktan sonra servis dosyasını oluşturabiliriz:

```bash
sudo touch /etc/systemd/system/mytimer.service
```

Oluşturulan dosyaya aşağıda verilen değerler girilir:

```text title="mytimer.service" linenums="1"
[Unit]
Description=My Service
Wants=mytimer.timer

[Service]
ExecStart=/full/path/to/my/script.sh

[Install]
WantedBy=multi-user.target
```

Burada `Unit` kısmı servise ait açıklamayı içerir. Ardından gelen `Service` kısmı servis dosyasının tam yol bilgisini içerir. Son olarak `Install` kısmında bulunan `multi-user.target` seçeneği, servisin normal şekilde gerçekleşen bir sistem açılışından sonra başlatılacağını ifade eder.

## Reload Systemd

Yapılan değişikliklerin geçerli olması için daemon yeniden yüklenir:

```bash
sudo systemctl daemon-reload
```

## Start the Timer & Service

Servisi el ile başlat:

```bash
sudo systemctl start mytimer.service
```

Servisi, sistem açılışında otomatik başlayacak şekilde ayarla:

```bash
sudo systemctl enable mytimer.service
```

## Questions

```text
What is the type of the service of the "syslog.service"?
```

??? tip "Steps"

    ```bash
    sudo systemctl show syslog.service | grep Type
    ```
