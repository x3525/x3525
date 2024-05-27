---
glightbox: true
icon: material/help
---

# HTML Injection

Çoğu durumda kullanıcı girdisinin doğrulanması ve sanitize edilmesi arka uç tarafında gerçekleştirilir. Ancak bazı kullanıcı girdileri, bazı durumlarda hiçbir zaman arka uç tarafına ulaşamaz ve tamamen ön uç tarafında işlenir. Bu nedenle hem ön uç hem de arka uç tarafında kullanıcı girdisinin doğrulanması ve sanitize edilmesi kritik öneme sahiptir.

```html title="index.html" linenums="1"
<!DOCTYPE html>
<html>

<body>
    <button onclick="inputFunction()">Click to enter your name</button>
    <p id="output"></p>

    <script>
        function inputFunction() {
            var input = prompt("Please enter your name", "");

            if (input != null) {
                document.getElementById("output").innerHTML = "Your name is " + input;
            }
        }
    </script>
</body>

</html>
```

Yukarıdaki web sayfası, verilen butona tıkladığımızda bizden ismimizi girmemizi istiyor ve girdiğimiz isme göre bir mesaj görüntülüyor. Kullanıcı girdisi kontrol edilmediğinden girdi kısmına herhangi bir HTML kod parçası yerleştirilebilir. Örneğin aşağıdaki kod parçası kullanıcı girdisi olarak verildiğinde sayfanın arka planı değişecektir:

```html
<style> body { background-image: url('https://academy.hackthebox.com/images/logo.svg'); } </style>
```

Bu örnekte her şey ön uç tarafında gerçekleştiğinden, web sayfasını yenilemek, sayfayı orijinal haline döndürecektir.

## Questions

```text
What text would be displayed on the page if we use the following payload as our input: <a href="http://www.hackthebox.com">Click Me</a>
```

??? tip "Steps"

    Tarayıcıda [http://94.237.59.185:53741](http://94.237.59.185:53741) adresine git.

    Burada `Click to enter your name` butonuna tıkla.

    Soruda verilen HTML kodunu kullanıcı girdisi olarak ver.

    Girdiyi onayla. Ardından cevap sayfada görüntülenecektir.
