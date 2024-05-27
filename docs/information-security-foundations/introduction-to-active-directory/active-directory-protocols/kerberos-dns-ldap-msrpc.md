---
glightbox: true
icon: material/circle-small
---

# Kerberos, DNS, LDAP, MSRPC

## Kerberos

Kerberos, etki alanı hesapları için varsayılan kimlik doğrulama protokolüdür. Kullanıcı, bilgisayarında oturum açtığında karşılıklı kimlik doğrulama yoluyla kimlik doğrulaması yapmak için Kerberos kullanır. Kerberos, kullanıcı parolalarını ağ üzerinden iletmez. Bunun yerine biletlere dayalı, durum bilgisi olmayan bir kimlik doğrulama protokolü kullanır. Bilet düzenleyen bir KDC (Key Distribution Center) bulunur. Kullanıcı, sisteme giriş isteği başlattığında kimlik doğrulaması için kullandıkları istemci, KDC üzerinden bir bilet talep eder ve bu isteği kullanıcının parolasıyla şifreler. KDC kendi parolasını kullanarak talebin şifresini çözebilirse, bir TGT (Ticket Granting Ticket) oluşturur ve bunu kullanıcıya iletir. Kullanıcı, daha sonra ilgili hizmetin NTLM parola hash dizesi ile şifrelenmiş bir TGS (Ticket Granting Service) bileti talep etmek için TGT biletini etki alanı denetleyicisine sunar. Son olarak istemci, uygulama veya hizmete TGS biletini sunarak gerekli hizmete erişim talebinde bulunur ve bu TGS biletinin şifresini, biletin kendi parola hash dizesi ile çözer. Tüm sürecin uygun şekilde tamamlanması durumunda, kullanıcının, talep edilen hizmete veya uygulamaya erişmesine izin verilir.

## DNS

### Forward DNS Lookup

```batch
nslookup INLANEFREIGHT.LOCAL
```

```text title="Output"
Server:  172.16.6.5
Address:  172.16.6.5

Name:    INLANEFREIGHT.LOCAL
Address:  172.16.6.5
```

### Reverse DNS Lookup

```batch
nslookup 172.16.6.5
```

```text title="Output"
Server:  172.16.6.5
Address:  172.16.6.5

Name:    ACADEMY-EA-DC01.INLANEFREIGHT.LOCAL
Address:  172.16.6.5
```

## LDAP

AD ve LDAP ilişkisi, Apache ve HTTP ilişkisine benzetilebilir. Apache, HTTP protokolünü kullanan bir web sunucusudur. AD, LDAP protokolünü kullanan bir dizin sunucusudur.
