---
glightbox: true
icon: material/help
---

# File System

5 tür Windows dosya sistemi vardır:

1. FAT12
2. FAT16
3. FAT32
4. NTFS
5. exFAT

FAT32, USB ve SD kartlar gibi birçok depolama aygıtı türünde yaygın olarak kullanılır. 32, FAT32 sisteminin depolama aygıtlarındaki veri kümelerini tanımlamak için 32 bit veri kullandığını ifade eder.

* [ ] Desteklediği maksimum dosya boyutu 4 GB ile sınırlıdır.
* [ ] Yerleşik veri koruma veya dosya sıkıştırma özelliği yoktur.
* [ ] Dosya şifreleme için üçüncü taraf araçlar kullanılmalıdır.
* [x] Bilgisayarlarda, dijital kameralarda, oyun konsollarında, akıllı telefonlarda ve tabletlerde kullanılabilir.
* [x] Windows 95 ve sonrası tüm Windows işletim sistemlerinde çalışır ve macOS ve Linux tarafından da desteklenir.

NTFS, Windows NT 3.1 ve sonrası için varsayılan Windows dosya sistemidir. NTFS, FAT32 eksikliklerini gidermenin yanı sıra meta veriler için daha iyi desteğe ve performansa sahiptir.

* [x] Çok büyük boyutlu bölümleri destekler.
* [x] NTFS güvenilirdir ve sistem arızası veya güç kaybı durumunda dosya sisteminin tutarlılığını geri yükleyebilir.
* [x] Hem dosyalar hem de klasörler üzerinde ayrıntılı izinler ayarlanmasına izin vererek güvenlik sağlar.
* [ ] TV ve dijital kameralar gibi daha eski medya aygıtları NTFS depolama aygıtlarını desteklemez.
* [ ] Çoğu mobil cihaz yerel olarak NTFS desteklemez.

## Permissions

| Permission Type | Description |
|---|---|
| Full Control | Dosyaların/klasörlerin okunmasına, yazılmasına, değiştirilmesine ve silinmesine izin verir. |
| Modify | Dosyaların/klasörlerin okunmasına, yazılmasına ve silinmesine izin verir. |
| List Folder Contents | Dosyaları çalıştırmanın yanı sıra klasörleri ve alt klasörleri görüntülemeye ve listelemeye izin verir. Yalnızca klasörler bu izni devralır. |
| Read and Execute | Dosyaların ve alt klasörlerin görüntülenmesine ve listelenmesine ve dosyaların yürütülmesine olanak tanır. Dosyalar ve klasörler bu izni devralır. |
| Write | Klasörlere ve alt klasörlere dosya eklemeye ve bir dosyaya veri yazmaya olanak sağlar. |
| Read | Klasörlerin ve alt klasörlerin görüntülenmesine ve listelenmesine ve bir dosyanın içeriğinin görüntülenmesine olanak tanır. |
| Traverse Folder | Diğer dosyalara veya klasörlere ulaşmak için klasörler arasında geçiş yapma olanağına izin verir veya vermez. Örneğin bir kullanıcının dizin içeriğini listeleme izni olmayabilir ancak dizinde bulunan bir dosyaya erişebilir. |

Dosyalar ve klasörler yönetim kolaylığı için üst klasörlerin NTFS izinlerini devralır. Bu sayede yöneticiler her dosya ve klasör için izinleri tek tek ayarlamak durumunda kalmaz. İzinlerin tek tek ayarlanması gereken durumlarda yönetici, gerekli dosya ve klasörler için izin devralmayı devre dışı bırakabilir.

## Integrity Control Access Control List (icacls)

Bir dizindeki NTFS izinlerini `icacls` aracını kullanarak listeleyebiliriz:

```batch
icacls C:\Windows
```

```text title="Output"
c:\windows NT SERVICE\TrustedInstaller:(F)
           NT SERVICE\TrustedInstaller:(CI)(IO)(F)
           NT AUTHORITY\SYSTEM:(M)
           NT AUTHORITY\SYSTEM:(OI)(CI)(IO)(F)
           BUILTIN\Administrators:(M)
           BUILTIN\Administrators:(OI)(CI)(IO)(F)
           BUILTIN\Users:(RX)
           BUILTIN\Users:(OI)(CI)(IO)(GR,GE)
           CREATOR OWNER:(OI)(CI)(IO)(F)
           APPLICATION PACKAGE AUTHORITY\ALL APPLICATION PACKAGES:(RX)
           APPLICATION PACKAGE AUTHORITY\ALL APPLICATION PACKAGES:(OI)(CI)(IO)(GR,GE)
           APPLICATION PACKAGE AUTHORITY\ALL RESTRICTED APPLICATION PACKAGES:(RX)
           APPLICATION PACKAGE AUTHORITY\ALL RESTRICTED APPLICATION PACKAGES:(OI)(CI)(IO)(GR,GE)

Successfully processed 1 files; Failed processing 0 files
```

Kaynak erişim düzeyi kullanıcı adından sonra listelenir. Olası miras ayarları şunlardır:

| Inheritance Setting | Meaning |
|---|---|
| `(CI)` | container inherit |
| `(OI)` | object inherit |
| `(IO)` | inherit only |
| `(NP)` | do not propagate inherit |
| `(I)` | permission inherited from parent container |

Temel erişim izinleri ise aşağıdaki gibidir:

| Permissions | Meaning |
|---|---|
| `F` | full access |
| `D` | delete access |
| `N` | no access |
| `M` | modify access |
| `RX` | read and execute access |
| `R` | read-only access |
| `W` | write-only access |

Örneğin yukarıdaki çıktıda `NT AUTHORITY\SYSTEM` hesabı şu niteliklere sahiptir: container inherit, inherit only, full access.

Aşağıda verilen komut ile `joe` kullanıcısına `C:\Users` üzerinde tam kontrol verebiliriz. Ancak object inherit ve container inherit ayarlarının komuta dahil edilmediği göz önüne alındığında, `joe` kullanıcısı yalnızca `C:\Users` üzerinde haklara sahip olacaktır:

```batch
icacls C:\Users /grant joe:f
```

Aşağıdaki komut ile kullanıcıya tanınan hakları iptal edebiliriz:

```batch
icacls C:\Users /remove joe
```

## Questions

```text
What system user has full control over the c:\users directory?
```

??? tip "Steps"

    ```batch
    icacls C:\Users
    ```
