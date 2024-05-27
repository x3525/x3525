---
glightbox: true
---

# Windows Subsystem for Linux

Yardımı görüntüle:

```powershell
wsl --help
```

WSL durumunu görüntüle:

```powershell
wsl --status
```

WSL paketini güncelle:

```powershell
wsl --update
```

Varsayılan WSL versiyonunu WSL 2 olarak ayarla:

```powershell
wsl --set-default-version 2
```

WSL versiyon bilgisini görüntüle:

```powershell
wsl --version
```

Dağıtımları listele:

```powershell
wsl --list
```

Yüklenebilecek dağıtımları listele:

```powershell
wsl --list --online
```

Kali Linux dağıtımını yükle:

```powershell
wsl --install kali-linux
```

Varsayılan dağıtımı Kali Linux olarak ayarla:

```powershell
wsl --set-default kali-linux
```

Kali Linux dağıtımını çalıştır:

```powershell
wsl --distribution kali-linux
```

Tüm dağıtımlara ait tüm disklerin bağlantısını sonlandır:

```powershell
wsl --unmount
```

Kali Linux dağıtımının kaydını kaldır ve kök dosya sistemini sil:

```powershell
wsl --unregister kali-linux
```
