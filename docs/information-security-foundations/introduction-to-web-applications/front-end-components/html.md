---
glightbox: true
icon: material/circle-small
---

# HTML

## Example

```html title="index.html" linenums="1"
<!DOCTYPE html>
<html>
    <head>
        <title>Page Title</title>
    </head>
    <body>
        <h1>A Heading</h1>
        <p>A Paragraph</p>
    </body>
</html>
```

## URL Encoding

HTML çalışırken öğrenilmesi gereken önemli bir kavram, URL encoding veya [Percent-encoding](https://en.wikipedia.org/wiki/Percent-encoding) kavramıdır. URL için yalnızca ASCII kodlaması kullanılabilir. URL kodlaması, güvenli olmayan ASCII karakterlerini yüzde sembolü ve ardından iki hex rakamla değiştirir.

## Usage

Bir `<head>` elementi genellikle sayfa başlığı gibi doğrudan sayfaya yazdırılmayan elementleri içerirken, tüm ana sayfa elementleri `<body>` altında bulunur. Bir `<style>` elementi sayfanın CSS kodunu içerirken, `<script>` elementi JavaScript kodlarını içerir.

Bu elementlerin her birine DOM adı verilir. W3C (World Wide Web Consortium), DOM kavramını şu şekilde tanımlar:

!!! info "DOM"
    W3C DOM, programların ve komut dosyalarının, bir belgenin içeriğine, yapısına ve stiline dinamik olarak erişmesine ve bunları güncellemesine olanak tanıyan bir platform ve dilden bağımsız bir arayüzdür.

DOM standardı 3 bölüme ayrılmıştır: Core DOM, XML DOM, HTML DOM.
