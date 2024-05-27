---
glightbox: true
icon: material/help
---

# Interacting with the Windows Operating System

## CMD

Bir araç ile ilgili yardım almak için `help` komutunu kullanabiliriz ya da araca ait `/?` seçeneğini kullanabiliriz. Örneğin:

```batch
help schtasks
```

## PowerShell

### Aliases

Geçerli oturumdaki tüm alias bilgilerini görüntüle:

```powershell
Get-Alias
```

Belirli bir komut için alias bilgisini görüntüle:

```powershell
Get-Alias -Name "cd"
```

Yeni bir alias oluştur:

```powershell
Set-Alias -Name "my" -Value Get-ChildItem
```

Cmdlet `Get-Alias` için çevrim içi yardım sayfasını aç:

```powershell
Get-Help Get-Alias -Online
```

Yardım dosyalarını yerele indir ve yükle:

```powershell
Update-Help
```

Cmdlet `Get-Alias` için yerel yardımı görüntüle:

```powershell
Get-Help Get-Alias
```

### Execution Policy

Çoğu komut dosyasının varsayılan olarak yürütülebilir izni yoktur. Bunun nedeni, kötü amaçlı komut dosyalarının yürütülmesini engelleyen ve yürütme politikası adı verilen bir güvenlik özelliğidir. Olası politikalar şunlardır:

| Policy | Description |
|---|---|
| AllSigned | Tüm komut dosyaları çalıştırılabilir ancak güvenilir bir yayıncının komut dosyalarını ve yapılandırma dosyalarını imzalaması gerekir. Buna hem uzak hem de yerel komut dosyaları dahildir. Henüz güvenilir veya güvenilmez olarak listelenmeyen yayıncılar tarafından imzalanmış komut dosyalarını çalıştırmadan önce bir uyarı alırız. |
| Bypass | Hiçbir komut dosyası veya yapılandırma dosyası engellenmez ve kullanıcı hiçbir uyarı veya istem almaz. |
| Default | Varsayılan yürütme politikasını ayarlar. Windows masaüstü makineleri için varsayılan politika `Restricted` politikasıdır. Windows sunucuları için varsayılan politika `RemoteSigned` politikasıdır. |
| RemoteSigned | Komut dosyaları çalıştırılabilir ancak internet üzerinden indirilen komut dosyalarında dijital imza gerekir. Yerel olarak yazılan komut dosyaları için dijital imzalara gerek yoktur. |
| Restricted | Bireysel komutlara izin verir ancak komut dosyalarının çalıştırılmasına izin vermez. Yapılandırma dosyaları (.ps1xml), modül script dosyaları (.psm1) ve PowerShell profilleri (.ps1) de dahil tüm script dosyası türleri engellenir. |
| Undefined | Geçerli kapsam için herhangi bir yürütme politikası belirlenmediği anlamına gelir. Tüm kapsamlar için yürütme politikası bu şekilde ayarlandıysa `Restricted` politikası varsayılan yürütme politikası olarak kullanılacaktır. |
| Unrestricted | Windows olmayan bilgisayarlar için varsayılan yürütme politikasıdır ve değiştirilemez. Bu politika imzasız komut dosyalarının çalıştırılmasına izin verir ancak yerel Intranet bölgesinden olmayan komut dosyalarını çalıştırmadan önce kullanıcıyı uyarır. |

## Questions

```text
What is the alias set for the ipconfig.exe command?
```

??? tip "Steps"

    ```powershell
    Get-Alias | ? { $_.Definition -match "ipconfig" }
    ```

```text
Find the Execution Policy set for the LocalMachine scope.
```

??? tip "Steps"

    ```powershell
    Get-ExecutionPolicy -List | Select-String "LocalMachine"
    ```
