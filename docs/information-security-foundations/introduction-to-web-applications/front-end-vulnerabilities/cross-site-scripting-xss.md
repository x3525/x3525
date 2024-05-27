---
glightbox: true
icon: material/help
---

# Cross-Site Scripting (XSS)

XSS pratikte HTML enjeksiyonuna çok benzer. Ancak XSS, istemci tarafında daha gelişmiş saldırılar gerçekleştirmek için JavaScript kodunun enjeksiyonunu içerir.

## Questions

```text
Try to use XSS to get the cookie value in the above page
```

??? tip "Steps"

    Tarayıcıda [http://94.237.59.185:53741](http://94.237.59.185:53741) adresine git.

    Burada `Click to enter your name` butonuna tıkla.

    Aşağıdaki HTML kodunu kullanıcı girdisi olarak ver:

    ```html
    #"><img src=/ onerror=alert(document.cookie)>
    ```

    Girdiyi onayla. Ardından cevap sayfada görüntülenecektir.
