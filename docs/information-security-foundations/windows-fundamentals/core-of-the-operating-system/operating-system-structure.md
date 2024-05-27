---
glightbox: true
icon: material/help
---

# Operating System Structure

Windows işletim sistemlerinde kök dizin bir sürücü harfi ile (genellikle C:) temsil edilir. Kök dizin (önyükleme bölümü olarak da bilinir) işletim sisteminin kurulu olduğu yerdir. Diğer fiziksel ve sanal sürücülere başka harfler (örneğin E:) atanır. Önyükleme bölümünün dizin yapısı aşağıdaki gibidir:

| Directory | Function |
|---|---|
| Perflogs | Windows performans günlüklerini içerir. |
| Program Files | 64 bit sistemlerde sadece 64 bit programları içerir. |
| Program Files (x86) | 64 bit sistemlerde 16 bit ve 32 bit programları içerir. |
| ProgramData | Bazı programların çalışması için gerekli olan verileri içerir. |
| Users | Sistemdeki her kullanıcı için kullanıcı profillerini içerir. |
| Default | Tüm kullanıcılar için varsayılan kullanıcı profili şablonudur. |
| Public | Tüm kullanıcıların dosya paylaşması için tasarlanmıştır. |
| AppData | Kullanıcı başına uygulama verileri ve ayarlarını içerir. |
| Windows | Windows işletim sistemi için gerekli dosyaları içerir. |
| System, System32, SysWOW64 | Windows için gerekli DLL dosyalarını içerir. |
| WinSxS | Windows Component Store dosyalarını içerir. |

## Questions

```text
Find the non-standard directory in the C drive. Submit the contents of the flag file saved in this directory.
```

??? tip "Steps"

    Dizin içeriğini listele:

    ```powershell
    Get-ChildItem "C:\"
    ```

    Standart olmayan klasöre geçiş yap:

    ```powershell
    Set-Location "C:\Academy\"
    ```

    Flag dosyasının içeriğini görüntüle:

    ```powershell
    Get-Content ".\flag.txt"
    ```
