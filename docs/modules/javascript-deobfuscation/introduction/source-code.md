---
glightbox: true
icon: material/circle-small
---

# Source Code

Günümüzde çoğu web sitesi işlevlerini yerine getirmek için JavaScript kullanır. Web sitesinin temelini oluşturmak için HTML kullanılır. Web sitesinin tasarımını belirlemek için CSS kullanılır. Web sitesini çalıştırmak için gerekli her türlü işlevi gerçekleştirmek için JavaScript kullanılır. Bu işlemler arka planda gerçekleşir ve biz yalnızca web sitesinin ön ucu ile etkileşime gireriz.

Kaynak kodun tamamı istemci tarafında mevcut olmasına rağmen, çoğu zaman bu kaynak koduna dikkat etmeyiz. Ancak belirli bir sayfanın istemci tarafı işlevlerini anlamak istiyorsak, sayfanın kaynak koduna da bakmamız gerekir. Bu bölümde, kaynak kodunu nasıl ortaya çıkarabileceğimizi ve genel kullanımını nasıl anlayabileceğimizi göreceğiz.

## HTML

Web sitesinin kaynak kodunu görüntülemek için ++control+u++ tuş kombinasyonunu kullanabiliriz.

## CSS

CSS kodu, `<style>` içerisinde dahili olarak tanımlanır veya harici olarak ayrı bir .css dosyasında tanımlanır ve HTML kodu içerisinde referans verilir.

CSS kodu harici olarak tanımlanmışsa, harici .css dosyasına HTML başlığında aşağıdaki gibi `<link>` etiketiyle başvurulur:

```html
<head>
    <link rel="stylesheet" href="style.css">
</head>
```

## JavaScript

JavaScript kodu, `<script>` içerisinde dahili olarak tanımlanır veya harici olarak .js dosyasına tanımlanır ve HTML kodu içerisinde referans verilir:

```html
<script src="secret.js"></script>
```

Komut dosyasını görüntülemek için `secret.js` ismine tıklayabiliriz. Kodun oldukça karmaşık olduğunu görebiliriz:

```javascript
eval(function (p, a, c, k, e, d) { e = function (c) { return c.toString(36) }; if (!''.replace(/^/, String)) { while (c--) { d[c.toString(a)] = k[c] || c.toString(a) } k = [function (e) { return d[e] }]; e = function () { return '\\w+' }; c = 1 }; while (c--) { if (k[c]) { p = p.replace(new RegExp('\\b' + e(c) + '\\b', 'g'), k[c]) } } return p }('g 4(){0 5="6{7!}";0 1=8 a();0 2="/9.c";1.d("e",2,f);1.b(3)}', 17, 17, 'var|xhr|url|null|generateSerial|flag|HTB|1_4m_7h3_53r14l_g3n3r470r|new|serial|XMLHttpRequest|send|php|open|POST|true|function'.split('|'), 0, {}))
```

Bunun sebebi, kodun anlaşılmaz hale getirilmiş olmasıdır (code obfuscation).
