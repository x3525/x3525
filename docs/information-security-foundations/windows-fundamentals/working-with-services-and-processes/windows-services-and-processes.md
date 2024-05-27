---
glightbox: true
icon: material/help
---

# Windows Services & Processes

## Windows Services

```powershell
Get-Service | Where-Object { $PSItem.Status -eq "Running" } | Select-Object -First 2 | Format-List
```

Yukarıda verilen PowerShell komutunu kullanarak çalışmakta olan ilk 2 servisi ayrıntılı bir şekilde listeledik. Bu komutun kısa versiyonu aşağıdaki gibidir:

```powershell
Get-Service | ? { $_.Status -eq "Running" } | select -First 2 | fl
```

Bazı kritik Windows servisleri sistem yeniden başlatılmadan durdurulamaz ya da yeniden başlatılamaz. Bunlardan bazıları şunlardır:

| Service | Description |
|---|---|
| smss.exe | Sistemdeki oturumların yönetilmesinden sorumludur. |
| csrss.exe | Windows alt sisteminin kullanıcı mod kısmıdır. |
| wininit.exe | Bir program yüklendikten ve bilgisayar yeniden başlatıldıktan sonra yapılacak tüm değişiklikleri listeleyen .ini dosyasını başlatır. |
| logonui.exe | Kullanıcının bilgisayarda oturum açmasını kolaylaştırmak için kullanılır. |
| lsass.exe | Bir bilgisayarda veya sunucuda kullanıcı oturum açma işlemlerinin geçerliliğini doğrular. Winlogon hizmeti için kullanıcıların kimlik doğrulamasından sorumlu süreci oluşturur. |
| services.exe | Hizmetlerin başlatılması ve durdurulması operasyonunu yönetir. |
| winlogon.exe | Oturum açıldığında kullanıcı profilinin yüklenmesinden ve ekran koruyucu çalışırken bilgisayarın kilitlenmesinden sorumludur. |
| System | Windows kernel çalıştıran bir arka plan sistem işlemidir. |
| svchost.exe | Otomatik güncelleştirmeler, Windows güvenlik duvarı ve tak ve çalıştır gibi dinamik bağlantı kitaplıklarından (DLL dosyaları) çalışan sistem hizmetlerini yönetir. |

## Local Security Authority Subsystem Service (LSASS)

LSASS, Windows sistemlerinde güvenlik politikasının uygulanmasından sorumlu olan süreçtir. Bir kullanıcı sistemde oturum açmayı denediğinde, kullanıcının oturum açma girişimi doğrulanır ve kullanıcının izin düzeylerine göre erişim belirteçleri oluşturulur. Bu servis kullanıcı hesabı parola değişikliklerinden de sorumludur. LSASS işlemi ile bellekte saklanan açık metin ya da hash kimlik bilgilerini elde etmek için çeşitli araçlar mevcuttur.

## Questions

```text
Identify one of the non-standard update services running on the host. Submit the full name of the service executable (not the DisplayName) as your answer.
```

??? tip "Steps"

    ```powershell
    Get-Service | ? { $_.Status -eq "Running" } | ? { $_.DisplayName -match "update" } | Select-Object -Property Name
    ```
