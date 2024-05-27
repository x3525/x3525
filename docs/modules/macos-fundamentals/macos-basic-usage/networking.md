---
glightbox: true
icon: material/circle-small
---

# Networking

## Managing Networking Settings Via The CLI

### Finding Info

```bash
ifconfig
```

### Setting a Manual IP with ifconfig

```bash
ifconfig en0 inet 192.168.1.1 netmask 255.255.255.0
```

### lsof

```bash
lsof -n -i4TCP -P
```

### Networksetup

```bash
networksetup -getinfo Wi-Fi
```

## Tips & Tricks

### NetworkQuality

```bash
networkQuality -I en0
```

### Find Wi-Fi Password

```bash
security find-generic-password -wa Office-2.4G
```
