---
glightbox: true
icon: material/circle-small
---

# Permission Management

Linux sistemlerindeki tüm izin sistemi sekizli sayı sistemine dayanmaktadır ve temel olarak bir dosyaya veya dizine atanabilecek üç farklı izin türü vardır:

1. Read
2. Write
3. Execute (traverse for directories)

| File type | Owner | Group | Others | Number of hard links | User | Group | File size | Date | File name |
|---|---|---|---|---|---|---|---|---|---|
| `-` | `rwx` | `rw-` | `r--` | `1` | `root` | `root` | `1641` | `May  4 23:41` | `test.sh` |

!!! info "Directory Hard Link"

    Klasörler için hard link oluşturulamaz. Herhangi bir klasör için belirtilen hard link sayısı, ilgili klasörün altında bulunan klasörlerin (gizli olanlar dahil) sayısını ifade eder.

## Change Permissions

İzinleri değiştirmek için `chmod` komutu kullanılabilir. Burada `u` user, `g` group, `o` others ve `a` all users için kullanılır. İzin eklemek için `+` işareti ve izin kaldırmak için `-` işareti kullanılabilir. Örneğin:

```bash
chmod a+r script.py
ls -l script.py
```

```text title="Output"
-rwxr-xr-x   1 serhat serhat 0 May  4 22:12 script.py
```

Bir başka yöntem ise sayısal ifadeleri kullanmaktır. Örneğin:

```bash
chmod 754 script.py
```

Buradaki 754 ifadesi aşağıda gösterildiği şekilde elde edilmiştir:

| 7 | 5 | 4 |
|---|---|---|
| `rwx` | `r-x` | `r--` |
| `421` | `401` | `400` |
| `111` | `101` | `100` |

## Change Owner

Sahiplik değiştirmek için `chown` komutu kullanılabilir. Komutu kullanırken `:` işaretinin solundaki kısım `user` için, sağındaki kısım ise `group` için kullanılır. Örneğin:

```bash
chown root:root script.py
ls -l script.py
```

```text title="Output"
-rwxr-xr--   1 root root 0 May  4 22:12 script.py
```

## SUID & SGID

SUID (Set owner User ID) ve SGID (Set owner Group ID) biti herhangi bir programın, herhangi bir kullanıcı tarafından, o programın sahibinin yetkilerinde çalıştırılmasını sağlar. Bu sayede erişim yetkimizin bulunmadığı bir dosya üzerinde değişiklik yapabiliriz. Örneğin sıradan bir kullanıcı `passwd` komutunu kullanarak kendi parolasını değiştirdiğinde `root` kullanıcısına ait olan `/etc/shadow` dosyası içerisinde kendine ait parola özetini değiştirmiş olur. Böylelikle kendisine ait olmayan bir dosyada düzenleme yapabilmiştir.

Değer `s` ise SUID/SGID aktif ve çalıştırılabilir izin mevcut anlamına gelir. Değer `S` ise SUID/SGID aktif ve çalıştırılabilir izin mevcut değil anlamına gelir.

```bash
chmod 4755 script.py
ls -l script.py
```

```text title="Output"
-rwsr-xr-x   1 root root 0 May  4 22:12 script.py
```

## Sticky Bit

Bir dizinde Sticky Bit ayarlanması, dizin içindeki dosyaları yalnızca sahibinin veya `root` kullanıcısının değiştirebilmesini sağlar. Değer `t` ise Sticky Bit aktif ve çalıştırılabilir izin mevcut anlamına gelir.

Değer `T` ise Sticky Bit aktif ve çalıştırılabilir izin mevcut değil anlamına gelir.

```bash
chmod 1754 scripts
ls -l
```

```text title="Output"
drwxr-xr-T   1 root root 0 May  4 22:12 scripts
```
