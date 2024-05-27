---
glightbox: true
icon: material/circle-small
---

# Basic Obfuscation

## Running JavaScript code

[JSConsole](https://jsconsole.com/) sitesine giderek aşağıdaki kodu çalıştıralım:

```javascript
console.log("Hello, World!");
```

```text title="Output"
Hello, World!
```

## Minifying JavaScript code

JavaScript kodunun okunabilirliğini azaltmanın yaygın bir yolu, JavaScript kodunun küçültülmesidir (minifying). Kod küçültmesi özellikle uzun kodlar için daha kullanışlıdır.

[JavaScript Minifier](https://www.toptal.com/developers/javascript-minifier) aracı JavaScript kodunu küçültmek için kullanılabilir:

```javascript
function log() {
    console.log("Hello, World!");
}
```

```javascript title="Output"
function log(){console.log("Hello, World!")}
```

## Packing JavaScript code

Aşağıda verilen JavaScript kodu, [BeautifyTools](https://beautifytools.com/) sitesinde bulunan [Javascript Obfuscator](https://beautifytools.com/javascript-obfuscator.php) aracı ile anlaşılmaz hale getirilmiştir:

```javascript
console.log("Hello, World!");
```

```javascript title="Output"
eval(function(p,a,c,k,e,d){e=function(c){return c};if(!''.replace(/^/,String)){while(c--){d[c]=k[c]||c}k=[function(e){return d[e]}];e=function(){return'\\w+'};c=1};while(c--){if(k[c]){p=p.replace(new RegExp('\\b'+e(c)+'\\b','g'),k[c])}}return p}('0.1("2, 3!");',4,4,'console|log|Hello|World'.split('|'),0,{}))
```

Yukarıda verilen obfuscation tekniği paketleme (packing) olarak bilinir ve genellikle başlangıç fonksiyonunda kullanılan altı bağımsız değişkenden (`function(p,a,c,k,e,d)`) tanınabilir.

Verilen bu yöntemler, kodun okunabilirliğini azaltmak için kullanışlı olsalar da, string ifadeler (`Hello` ve `World`) açık metin olarak gözükmektedir. Bu durum koda ait önemli işlevleri açığa çıkarabilir. Bu nedenle kodumuzu gizlemenin daha iyi yollarını aramak isteyebiliriz.
