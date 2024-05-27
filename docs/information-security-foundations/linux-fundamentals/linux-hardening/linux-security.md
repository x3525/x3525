---
glightbox: true
icon: material/circle-small
---

# Linux Security

## TCP Wrappers

TCP wrappers yalnızca hizmet erişim kontrolü sağlar. Port işlemleri yapılamaz. Bu yüzden güvenlik duvarı yazılımlarının yerini alamazlar.

## /etc/hosts.allow

Hangi servislerin ve bilgisayarların sisteme erişmesine izin verildiğini belirten dosyadır:

```text title="/etc/hosts.allow" linenums="1"
# Yerel ağda SSH erişimine izin ver
sshd : 10.129.14.0/24

# Sadece belirtilen bilgisayar için FTP erişimine izin ver
ftpd : 10.129.14.10

# Belirtilen domain için Telnet erişimine izin ver
telnetd : .inlanefreight.local
```

## /etc/hosts.deny

Hangi servislerin ve bilgisayarların sisteme erişmesine izin verilmediğini belirten dosyadır:

```text title="/etc/hosts.deny" linenums="1"
# Belirtilen bilgisayar için SSH erişimine izin verme
sshd : 10.129.22.22

# 10.129.22.0 ile 10.129.22.255 aralığında FTP erişimine izin verme
ftpd : 10.129.22.0/24

# Belirtilen domain için servis erişimine izin verme
ALL : .inlanefreight.com
```
