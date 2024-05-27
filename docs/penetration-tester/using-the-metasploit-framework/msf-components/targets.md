---
glightbox: true
icon: material/circle-small
---

# Targets

Herhangi bir exploit modülü seçmeden ana menüde hedefleri görüntülemeye çalışırsak aşağıdaki uyarı ile karşılaşırız:

```text
show targets
```

```text title="Output"
[-] No exploit module selected.
```

Bir modül seçtikten sonra o modüle ait seçenekleri aşağıdaki komut ile görüntüleyebiliriz:

```text
options
```

```text title="Output"
Module options (exploit/windows/browser/ie_execcommand_uaf):

   Name       Current Setting  Required  Description
   ----       ---------------  --------  -----------
   OBFUSCATE  false            no        Enable JavaScript obfuscation
   SRVHOST    0.0.0.0          yes       The local host to listen on. This must be an address on the local machine or 0.0.0.0
   SRVPORT    8080             yes       The local port to listen on.
   SSL        false            no        Negotiate SSL for incoming connections
   SSLCert                     no        Path to a custom SSL certificate (default is randomly generated)
   URIPATH                     no        The URI to use for this exploit (default is random)


Exploit target:

   Id  Name
   --  ----
   0   Automatic
```

Artık hedefleri görüntüleyebiliriz:

```text
show targets
```

```text title="Output"
Exploit targets:

   Id  Name
   --  ----
   0   Automatic
   1   IE 7 on Windows XP SP3
   2   IE 8 on Windows XP SP3
   3   IE 7 on Windows Vista
   4   IE 8 on Windows Vista
   5   IE 8 on Windows 7
   6   IE 9 on Windows 7
```

## MSF - Target Selection

```text
set target 6
```

```text title="Output"
target => 6
```
