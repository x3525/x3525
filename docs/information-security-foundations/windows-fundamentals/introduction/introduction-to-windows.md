---
glightbox: true
icon: material/help
---

# Introduction to Windows

## Windows Versions

Aşağıda Windows 10 ve öncesine ait [Windows versiyon bilgileri](https://learn.microsoft.com/en-us/windows/win32/sysinfo/operating-system-version) verilmiştir:

* 4.0 (Windows NT 4)
* 5.0 (Windows 2000)
* 5.1 (Windows XP)
* 5.2 (Windows Server 2003, 2003 R2)
* 6.0 (Windows Vista, Server 2008)
* 6.1 (Windows 7, Server 2008 R2)
* 6.2 (Windows 8, Server 2012)
* 6.3 (Windows 8.1, Server 2012 R2)
* 10.0 (Windows 10, Server 2016, Server 2019)

İşletim sistemi hakkında bilgi almak için `Get-WmiObject` Cmdlet ile `win32_OperatingSystem` sınıfını kullanabiliriz. Bu Cmdlet mevcut WMI sınıfları hakkında bilgi almak için kullanılabilir:

```powershell
Get-WmiObject -Class win32_OperatingSystem | select Version,BuildNumber
```

```text title="Output"
Version    BuildNumber
-------    -----------
10.0.19041 19041
```

Bu Cmdlet ile kullanılan diğer bazı sınıflar şunlardır:

* `win32_Service`
* `win32_Bios`
* `win32_Process`

## Accessing Windows

### Remote Desktop Protocol (RDP)

RDP uzaktan erişiminin etkinleştirildiği hedef bilgisayar sunucu olarak kabul edilir. RDP varsayılan olarak 3389 numaralı port üzerinden dinleme yapar.

### Using xfreerdp

Linux tabanlı bir saldırı sisteminden Windows sistemine RDP kullanarak uzaktan erişmek için `xfreerdp` adlı aracı kullanabiliriz. Kullanım kolaylığı ve verimliliği nedeniyle tercih edilen bir araçtır:

```bash
xfreerdp /dynamic-resolution /v:<target-ip> /u:<username> /p:<password>
```

## Questions

```text
What is the Build Number of the target workstation?
```

??? tip "Steps"

    Windows hedefine bağlan:

    ```bash
    xfreerdp /dynamic-resolution /v:10.129.203.55 /u:htb-student /p:'Academy_WinFun!'
    ```

    Windows içerisinde aşağıdaki komutu çalıştır:

    ```powershell
    Get-WmiObject -Class win32_OperatingSystem | Select-Object BuildNumber
    ```

```text
Which Windows NT version is installed on the workstation? (i.e. Windows X - case sensitive)
```

??? tip "Steps"

    ```powershell
    Get-ComputerInfo | Select-Object OSName
    ```
