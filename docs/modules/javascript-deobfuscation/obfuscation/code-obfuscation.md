---
glightbox: true
icon: material/circle-small
---

# Code Obfuscation

## What is obfuscation

Obfuscation (anlaşılmaz hale getirme), bir komut dosyasının insanlar tarafından okunmasını zorlaştırmak için kullanılan bir tekniktir. Bu işlem, genellikle bir gizleme aracı kullanılarak otomatik olarak gerçekleştirilir. Ancak bu durum kodun daha yavaş çalışmasına sebep olabilir.

Kod gizleme araçları verilen kodu, kod içinde kullanılan tüm sözcük ve simgelerin yer aldığı bir sözlüğe dönüştürür. Ardından yürütme sırasında sözlükteki her sözcük ve simgeye atıfta bulunarak orijinal kodu yeniden oluşturmaya çalışır.

Python, PHP ve JavaScript gibi dillerde yazılan kodlar derlenmeden yürütülür. Python ve PHP genellikle sunucu tarafında bulunur ve bu nedenle son kullanıcılardan gizlenir. Ancak JavaScript, genellikle istemci tarafında (örneğin tarayıcılarda) kullanılır ve bu sebeple kod kullanıcıya açık metin olarak gönderilir. Bu nedenle obfuscation işlemi JavaScript diliyle yazılan kodlarda sıklıkla kullanılır.

## Use Cases

* Geliştiricinin izni olmadan kodun yeniden kullanılmasını veya kopyalanmasını önlemek.
* Tersine mühendislik işlemini zorlaştırmak.
* Kötü niyetli kodu IDS ve IPS sistemlerinden korumak.
