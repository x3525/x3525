---
glightbox: true
icon: material/circle-small
---

# Containers

Vagrant yükle:

```powershell
choco install -y vagrant
```

Sanal makineleri tutmak için bir klasör oluştur:

```powershell
mkdir "vms"
```

Ubuntu makinesi için bir klasör oluştur:

```powershell
mkdir ".\vms\ubuntu-machine"
```

Vagrantfile dosyasını oluştur:

```powershell
vagrant init ubuntu/focal64
```

Veri paylaşımı (`config.vm.synced_folder`) için bir klasör oluştur:

```powershell
mkdir ".\vms\data"
```

Örnek bir dosya oluştur:

```powershell
Write-Output "hello, world" > ".\vms\data\hello.txt"
```

Vagrantfile dosyasında değişiklik yapıldıysa aşağıdaki komutu çalıştır:

```powershell
vagrant reload
```

Makineyi başlat (ilk sefer için dosyalar indirilir ve yüklenir):

```powershell
vagrant up
```

Makineye SSH ile bağlan:

```powershell
vagrant ssh
```

Makineyi kapat:

```powershell
vagrant halt
```
