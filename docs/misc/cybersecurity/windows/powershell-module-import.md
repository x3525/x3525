---
glightbox: true
---

# PowerShell Module Import

Aşağıdaki komutlardan herhangi birini kullanarak `profile.ps1` dosyasının konumunu öğren:

* `$profile.AllUsersAllHosts`
* `$profile.AllUsersCurrentHost`
* `$profile.CurrentUserAllHosts`
* `$profile.CurrentUserCurrentHost`

Bulunan `profile.ps1` dosyasının içerisine aşağıdaki satırları ekle:

```powershell title="profile.ps1" linenums="1"
Import-Module "C:\Path\To\Module1"
Import-Module "C:\Path\To\Module2"
```

Bu sayede yeni bir PowerShell işlemi başlatıldığında `profile.ps1` dosyasında belirtilen modüller otomatik olarak import edilecektir.
