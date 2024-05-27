---
glightbox: true
icon: material/circle-small
---

# Plugins

## Using Plugins

Eklentiler doğru dizine kurulduklarında Msfconsole içerisinde kullanılabilirler.

Aşağıdaki komut ile yüklü olan eklentiler görüntülenebilir:

```bash
ls /usr/share/metasploit-framework/plugins
```

```text title="Output"
aggregator.rb      beholder.rb        event_tester.rb  komand.rb     msfd.rb    nexpose.rb   request.rb  session_notifier.rb  sounds.rb  token_adduser.rb  wmap.rb
alias.rb           db_credcollect.rb  ffautoregen.rb   lab.rb        msgrpc.rb  openvas.rb   rssfeed.rb  session_tagger.rb    sqlmap.rb  token_hunter.rb
auto_add_route.rb  db_tracker.rb      ips_filter.rb    libnotify.rb  nessus.rb  pcap_log.rb  sample.rb   socket_logger.rb     thread.rb  wiki.rb
```

## Installing New Plugins

### Downloading MSF Plugins

Aşağıdaki komut ile [darkoperator](https://github.com/darkoperator/Metasploit-Plugins.git) kullanıcısının eklenti reposu indirilmiştir:

```bash
git clone https://github.com/darkoperator/Metasploit-Plugins
```

### Copying Plugin to MSF

Aşağıdaki komut ile `pentest.rb` eklentisi, eklentiler dizinine kopyalanmıştır:

```bash
sudo cp ./Metasploit-Plugins/pentest.rb /usr/share/metasploit-framework/plugins/pentest.rb
```

### MSF - Load Plugin

Aşağıdaki komut ile `pentest.rb` eklentisi, Msfconsole içerisinde kullanılmak üzere yüklenmiştir:

```text
load pentest
```

```text title="Output"
       ___         _          _     ___ _           _
      | _ \___ _ _| |_ ___ __| |_  | _ \ |_  _ __ _(_)_ _
      |  _/ -_) ' \  _/ -_|_-<  _| |  _/ | || / _` | | ' \
      |_| \___|_||_\__\___/__/\__| |_| |_|\_,_\__, |_|_||_|
                                              |___/

Version 1.6
Pentest Plugin loaded.
by Carlos Perez (carlos_perez[at]darkoperator.com)
[*] Successfully loaded plugin: pentest
```
