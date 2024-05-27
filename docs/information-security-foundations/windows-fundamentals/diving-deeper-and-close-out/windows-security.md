---
glightbox: true
icon: material/help
---

# Windows Security

## Security Identifier (SID)

Sistemdeki güvenlik ilkelerinin her birinin benzersiz bir güvenlik tanımlayıcısı (SID) vardır. Sistem otomatik olarak SID oluşturur. Sistemde iki özdeş kullanıcı olsa bile Windows bu iki kullanıcıyı ve haklarını SID bilgisine göre ayırt edebilir. SID bilgileri güvenlik veri tabanında saklanan farklı uzunluklara sahip dize değerleridir.

```batch
whoami /user
```

```text title="Output"
USER INFORMATION
----------------

User Name SID
========= =============================================
ws01\bob  S-1-5-21-674899381-4069889467-2080702030-1002
```

| Number | Meaning | Description |
|---|---|---|
| S | SID | Dizeyi SID olarak tanımlar. |
| 1 | Revision Level | Bu değer 1 ise bu tarihe kadar hiç değişmedi anlamına gelir. |
| 5 | Identifier Authority | SID oluşturan yetkiliyi (bilgisayar veya ağ) tanımlayan 48 bitlik bir dizedir. |
| 21 | Subauthority 1 | SID tarafından tanımlanan kullanıcının ilişkisini veya grubunu, onu oluşturan yetkiliyle tanımlayan değişken bir sayıdır. Yetkilinin, kullanıcının hesabını hangi sırayla oluşturduğunu bize bildirir. |
| 674899381-4069889467-2080702030 | Subauthority 2 | Numarayı hangi bilgisayarın (veya etki alanının) oluşturduğunu bize bildirir. |
| 1002 | Subauthority 3 | Bir hesabı diğerinden ayıran RID değeridir. Kullanıcının normal bir kullanıcı mı, misafir mi, yönetici mi, yoksa başka bir grubun parçası mı olduğunu bize söyler. |

## User Account Control (UAC)

UAC, kötü amaçlı yazılımların bilgisayara veya içeriğine zarar verebilecek işlemleri çalıştırmasını veya değiştirmesini engelleyen bir Windows güvenlik özelliğidir. İstenmeyen yazılımların yöneticinin bilgisi dışında yüklenmesini veya sistem çapında değişiklik yapılmasını önlemek için tasarlanmıştır.

## Questions

```text
Find the SID of the bob.smith user.
```

??? tip "Steps"

    ```powershell
    wmic useraccount get name,sid | Select-String "bob"
    ```
