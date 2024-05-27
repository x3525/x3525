---
glightbox: true
---

# SSH2_MSG_KEX_ECDH_REPLY

SSH bağlantı denemesinde SSH tepki vermiyorsa, ilk önce `-v` parametresi ile bağlantı detaylarını görüntüle:

```bash
ssh user@10.129.236.30 -v
```

```text title="Output" hl_lines="35"
OpenSSH_9.6p1 Debian-3, OpenSSL 3.1.4 24 Oct 2023
debug1: Reading configuration data /etc/ssh/ssh_config
debug1: /etc/ssh/ssh_config line 19: include /etc/ssh/ssh_config.d/*.conf matched no files
debug1: /etc/ssh/ssh_config line 21: Applying options for *
debug1: Connecting to 10.129.236.30 [10.129.236.30] port 22.
debug1: Connection established.
debug1: identity file /home/kali/.ssh/id_rsa type -1
debug1: identity file /home/kali/.ssh/id_rsa-cert type -1
debug1: identity file /home/kali/.ssh/id_ecdsa type -1
debug1: identity file /home/kali/.ssh/id_ecdsa-cert type -1
debug1: identity file /home/kali/.ssh/id_ecdsa_sk type -1
debug1: identity file /home/kali/.ssh/id_ecdsa_sk-cert type -1
debug1: identity file /home/kali/.ssh/id_ed25519 type -1
debug1: identity file /home/kali/.ssh/id_ed25519-cert type -1
debug1: identity file /home/kali/.ssh/id_ed25519_sk type -1
debug1: identity file /home/kali/.ssh/id_ed25519_sk-cert type -1
debug1: identity file /home/kali/.ssh/id_xmss type -1
debug1: identity file /home/kali/.ssh/id_xmss-cert type -1
debug1: identity file /home/kali/.ssh/id_dsa type -1
debug1: identity file /home/kali/.ssh/id_dsa-cert type -1
debug1: Local version string SSH-2.0-OpenSSH_9.6p1 Debian-3
debug1: Remote protocol version 2.0, remote software version OpenSSH_8.2p1 Ubuntu-4ubuntu0.4
debug1: compat_banner: match: OpenSSH_8.2p1 Ubuntu-4ubuntu0.4 pat OpenSSH* compat 0x04000000
debug1: Authenticating to 10.129.236.30:22 as 'user'
debug1: load_hostkeys: fopen /home/kali/.ssh/known_hosts: No such file or directory
debug1: load_hostkeys: fopen /home/kali/.ssh/known_hosts2: No such file or directory
debug1: load_hostkeys: fopen /etc/ssh/ssh_known_hosts: No such file or directory
debug1: load_hostkeys: fopen /etc/ssh/ssh_known_hosts2: No such file or directory
debug1: SSH2_MSG_KEXINIT sent
debug1: SSH2_MSG_KEXINIT received
debug1: kex: algorithm: curve25519-sha256
debug1: kex: host key algorithm: ssh-ed25519
debug1: kex: server->client cipher: chacha20-poly1305@openssh.com MAC: <implicit> compression: none
debug1: kex: client->server cipher: chacha20-poly1305@openssh.com MAC: <implicit> compression: none
debug1: expecting SSH2_MSG_KEX_ECDH_REPLY
```

Çıktının sonunda görülen `SSH2_MSG_KEX_ECDH_REPLY` hatası, [ServerFault](https://serverfault.com/a/670081) sitesinde tartışılmıştır. Hatanın çözümü için, ağ arayüzünün MTU (Maximum Transmission Unit) değeri değiştirilir (genelde 1200 yapılır):

```bash
sudo ip li set mtu 1200 dev tun0
```
