---
glightbox: true
icon: material/circle-small
---

# Windows

## Installation Requirements

### Hardware Requirements

* Processor that runs at 1GHz or greater. Dual-core or better is ideal.
* 2G of RAM minimum, 4G or more is ideal.
* 60G of Hard Drive space. This ensures there is room for the OS and some tools. Size can vary based on the number of tools we install on the host.
* Network connectivity, if possible, two network adapters.

### Software Requirements

[Windows geliştirici merkezinde](https://developer.microsoft.com/en-us/windows/downloads/virtual-machines/) önceden yapılandırılmış halde indirmeye hazır sanal makine dosyaları bulunmaktadır. Bu dosyalar aşağıda verilen yapılandırmaları (zamanla değişiklik gösterebilir) içermektedir:

* Windows 11 Enterprise (Evaluation)
* Visual Studio 2022 Community Edition with UWP, .NET Desktop, Azure, and Windows App SDK for C# workloads enabled
* Windows Subsystem for Linux 2 enabled with Ubuntu installed
* Windows Terminal installed
* Developer mode enabled

Sanal makinede `IEUser` isimli bir kullanıcı bulunmaktadır ve kullanıcı parolası `Passw0rd!` olarak ayarlanmıştır. Sanal makinenin deneme süresi 90 gündür, bu yüzden ilk kurulumda VM snapshot almak faydalı olacaktır.

## Chocolatey Package Manager

Chocolatey paket yöneticisini kullanarak Windows makinemiz için bazı faydalı araçları kurabiliriz:

```powershell
choco install python git wsl2 openssh openvpn microsoft-windows-terminal
```

Kurulumların ardından PowerShell ve çevre değişkenlerini güncellemek için `RefreshEnv` komutunu kullanabiliriz:

```powershell
RefreshEnv
```

## Security Configurations and Defender Modifications

Chocolatey veya Git ile sisteme kurulacak olan araçlar Windows Defender tarafından zararlı olarak tespit edilip engellenebilir. Bunu önlemek için Defender ayarlarında bazı klasörleri dışlayabiliriz.
