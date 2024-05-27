---
glightbox: true
icon: material/circle-small
---

# Nibbles - Web Footprinting

[WhatWeb](https://www.morningstarsecurity.com/research/whatweb) aracı ile bir web uygulamasında kullanılan teknolojiler hakkında bilgi sahibi olunabilir:

```bash
whatweb http://10.129.42.190/nibbleblog
```

```text title="Output"
http://10.129.42.190/nibbleblog [301 Moved Permanently] Apache[2.4.18], Country[RESERVED][ZZ], HTTPServer[Ubuntu Linux][Apache/2.4.18 (Ubuntu)], IP[10.129.42.190], RedirectLocation[http://10.129.42.190/nibbleblog/], Title[301 Moved Permanently]
http://10.129.42.190/nibbleblog/ [200 OK] Apache[2.4.18], Cookies[PHPSESSID], Country[RESERVED][ZZ], HTML5, HTTPServer[Ubuntu Linux][Apache/2.4.18 (Ubuntu)], IP[10.129.42.190], JQuery, MetaGenerator[Nibbleblog], PoweredBy[Nibbleblog], Script, Title[Nibbles - Yum yum]
```

Bu örnekte HTML5, jQuery, PHP ve Nibbleblog gibi teknolojilerin kullanıldığı görülebilir.
