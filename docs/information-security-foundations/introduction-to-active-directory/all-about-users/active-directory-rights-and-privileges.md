---
glightbox: true
icon: material/circle-small
---

# Active Directory Rights and Privileges

Haklar, genellikle kullanıcılara veya gruplara atanır ve dosya gibi bir nesneye erişim izinleriyle ilgilenir. Ayrıcalıklar ise, kullanıcıya, bir programı çalıştırma, sistemi kapatma, parolaları sıfırlama vb. gibi eylemleri gerçekleştirme izni verir. Ayrıcalıklar kullanıcılara ayrı ayrı atanır veya yerleşik veya özel grup üyeliği yoluyla onlara verilir. Windows bilgisayarlarında User Rights Assignment adı verilen bir kavram bulunur. Bu kavram haklar olarak anılsa da aslında kullanıcıya verilen ayrıcalık türlerini ifade eder.

## Built-in AD Groups

### Server Operators Group Details

```powershell
Get-ADGroup -Identity "Server Operators" -Properties *
```

### Domain Admins Group Membership

```powershell
Get-ADGroup -Identity "Domain Admins" -Properties * | select DistinguishedName,GroupCategory,GroupScope,Name,Members
```

## Viewing a User's Privileges

```batch
whoami /priv
```
