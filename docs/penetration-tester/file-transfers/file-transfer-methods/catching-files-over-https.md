---
glightbox: true
icon: material/circle-small
---

# Catching Files over HTTPS

## HTTPS

Web transferi dosya aktarmanın en yaygın yoludur, çünkü HTTP ve HTTPS, güvenlik duvarları aracılığıyla izin verilen en yaygın protokollerdir.

Bir web sunucusu kurmak için Python [uploadserver](https://github.com/Densaugeo/uploadserver) modülü kullanılabileceği gibi Apache veya Nginx de kullanılabilir. Bu bölümde dosya yükleme işlemleri için güvenli bir web sunucusu oluşturulması ele alınacaktır.

## Nginx - Enabling PUT

Apache sunucusuna iyi bir alternatif olarak Nginx sunucusu gösterilebilir. Çünkü, yapılandırma adımları daha az karmaşıktır ve modül sistemi güvenlik sorunlarına yol açmaz.

İlk olarak yüklenen dosyaları yönetebilmek için bir dizin oluşturalım:

```bash
sudo mkdir -p /var/www/uploads/SecretUploadDirectory
```

Bu dizinin ve altındaki dosyaların sahipliğini `www-data` olarak değiştirelim:

```bash
sudo chown -R www-data:www-data /var/www/uploads/SecretUploadDirectory
```

Nginx yapılandırma dosyasını (`/etc/nginx/sites-available/upload.conf`) oluşturalım:

```text title="upload.conf" linenums="1"
server {
    listen 9001;

    location /SecretUploadDirectory/ {
        root    /var/www/uploads;
        dav_methods PUT;
    }
}
```

Sitemizi `sites-enabled` dizinine sembolik link olarak verelim:

```bash
sudo ln -s /etc/nginx/sites-available/upload.conf /etc/nginx/sites-enabled/
```

Nginx servisini başlatalım:

```bash
sudo systemctl restart nginx.service
```

Herhangi bir hata mesajı alırsak log dosyasını (`/var/log/nginx/error.log`) kontrol edebiliriz:

```bash
tail -2 /var/log/nginx/error.log
```

```text title="Output"
2020/11/17 16:11:56 [emerg] 5679#5679: bind() to 0.0.0.0:`80` failed (98: A`ddress already in use`)
2020/11/17 16:11:56 [emerg] 5679#5679: still could not bind()
```

80 numaralı portu kontrol etmek için aşağıdaki komut kullanılabilir:

```bash
ss -lnpt | grep 80
```

```text title="Output"
LISTEN 0      100          0.0.0.0:80        0.0.0.0:*    users:(("python",pid=`2811`,fd=3),("python",pid=2070,fd=3),("python",pid=1968,fd=3),("python",pid=1856,fd=3))
```

PID numarasına göre kontrol etmek için aşağıdaki komut kullanılabilir:

```bash
ps -ef | grep 2811
```

```text title="Output"
user65      2811    1856  0 16:05 ?        00:00:04 `python -m websockify 80 localhost:5901 -D`
root        6720    2226  0 16:14 pts/0    00:00:00 grep --color=auto 2811
```

80 numaralı portu dinleyen bir modül olduğunu görüyoruz. Bunu düzeltmek için 80 numaralı porta bağlanan varsayılan Nginx yapılandırmasını kaldırabiliriz:

```bash
sudo rm /etc/nginx/sites-enabled/default
```

Artık PUT isteği göndermek için cURL kullanarak yüklemeyi test edebiliriz. Aşağıdaki örnekte `/etc/passwd` dosyası sunucuya `users.txt` adı ile yüklenmiştir:

```bash
curl -T /etc/passwd http://localhost:9001/SecretUploadDirectory/users.txt
```

Son olarak [http://localhost/SecretUploadDirectory](http://localhost/SecretUploadDirectory) adresine giderek, dizin listesinin etkin olmadığından emin olmak için bir test yapabiliriz. Apache sunucusunda index dosyası olmayan bir dizine (`index.html`) rastlanıldığında varsayılan olarak tüm dosyalar listelenir. Bu, gizlilik açısından oldukça kötü bir durumdur. Nginx sunucunda ise bu tarz özellikler varsayılan olarak etkin değildir.
