---
glightbox: true
---

# Port Numbers

## Table Legend

| Cell | Description |
|---|---|
| {++Yes++} | Açıklanan protokol, bu port için IANA tarafından atanmıştır ve bu protokol için bir standart hale gelmiş, belirtilmiş veya yaygın olarak kullanılmaktadır. |
| {==Assigned==} | Açıklanan protokol, bu port için IANA tarafından atanmıştır ancak bu protokol için bir standart hale gelmemiş, belirtilmemiş veya yaygın olarak kullanılmamaktadır. |
| {--No--} | Açıklanan protokol, bu port için IANA tarafından atanmamıştır ve bu protokol için bir standart hale gelmemiş, belirtilmemiş veya yaygın olarak kullanılmamaktadır. |
| Reserved | Belirtilen port, çakışmaları önlemek amacıyla IANA tarafından ayrılmıştır. Port numarası, talep edilmesi halinde IANA tarafından atanabilir. |

## Well Known Ports

| Port | Service/Protocol/Application | TCP | UDP |
|---|---|---|---|
| 0 | Dynamic port (system allocated) | Reserved | Reserved |
| 20 | FTP data transfer | {++Yes++} | {==Assigned==} |
| 21 | FTP control (command) | {++Yes++} | {==Assigned==} |
| 22 | SSH | {++Yes++} | {==Assigned==} |
| 23 | Telnet protocol | {++Yes++} | {==Assigned==} |
| 25 | SMTP (unencrypted) | {++Yes++} | {==Assigned==} |
| 43 | WHOIS protocol | {++Yes++} | {==Assigned==} |
| 53 | DNS | {++Yes++} | {++Yes++} |
| 80 | HTTP | {++Yes++} | {++Yes++} |
| 88 | Kerberos authentication system | {++Yes++} | {++Yes++} |
| 110 | POP3 (unencrypted) | {++Yes++} | {==Assigned==} |
| 111 | ONC-RPC/SUN-RPC | {++Yes++} | {++Yes++} |
| 135 | Microsoft DCE/RPC Locator service | {++Yes++} | {++Yes++} |
| 137 | NetBIOS Name Service, SMB with UDP | {++Yes++} | {++Yes++} |
| 138 | NetBIOS Datagram Service, SMB with UDP | {==Assigned==} | {++Yes++} |
| 139 | NetBIOS over TCP/IP (SMB on top of NBT) | {++Yes++} | {==Assigned==} |
| 143 | IMAP (unencrypted) | {++Yes++} | {==Assigned==} |
| 161 | SNMP | {==Assigned==} | {++Yes++} |
| 162 | SNMPTRAP | {++Yes++} | {++Yes++} |
| 443 | HTTPS | {++Yes++} | {++Yes++} |
| 445 | SMB directly over TCP/IP | {++Yes++} | {==Assigned==} |
| 465 | SMTP Encrypted | {++Yes++} | {--No--} |
| 587 | SMTP Encrypted/STARTTLS | {++Yes++} | {==Assigned==} |
| 623 | IPMI Remote Management Protocol || {++Yes++} |
| 993 | IMAPS | {++Yes++} | {==Assigned==} |
| 995 | POP3S | {++Yes++} | {++Yes++} |

## Registered Ports

| Port | Service/Protocol/Application | TCP | UDP |
|---|---|---|---|
| 1080 | SOCKS proxy | {++Yes++} | {++Yes++} |
| 1433 | MSSQL Server database management system server | {++Yes++} | {++Yes++} |
| 1434 | MSSQL Server database management system monitor | {++Yes++} | {++Yes++} |
| 2049 | NFS | {++Yes++} | {++Yes++} |
| 3020 | CIFS | {++Yes++} | {++Yes++} |
| 3306 | MySQL database system | {++Yes++} | {==Assigned==} |
| 3389 | RDP (Microsoft Terminal Server) | {++Yes++} | {++Yes++} |
| 5355 | LLMNR (Link-Local Multicast Name Resolution) | {++Yes++} | {++Yes++} |
| 5985 | WinRM-HTTP | {++Yes++} ||
| 5986 | WinRM-HTTPS | {++Yes++} ||
