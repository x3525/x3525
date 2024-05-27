---
glightbox: true
icon: material/help
---

# User Management

| Command | Description |
|---|---|
| `sudo` | Verilen komutu farklı bir kullanıcı olarak yürütür. |
| `su` | Belirtilen kullanıcı kimliğine geçer. |
| `useradd` | Yeni bir kullanıcı oluşturur. |
| `userdel` | Bir kullanıcı hesabını ve ilgili dosyaları siler. |
| `usermod` | Bir kullanıcı hesabını değiştirir. |
| `addgroup` | Sisteme bir grup ekler. |
| `delgroup` | Bir grubu sistemden kaldırır. |
| `passwd` | Kullanıcı parolasını değiştirir. |

## Questions

```text
Which option needs to be set to create a home directory for a new user using "useradd" command?
```

??? tip "Steps"

    ```bash
    man useradd | grep home
    ```

```text
Which option needs to be set to lock a user account using the "usermod" command? (long version of the option)
```

??? tip "Steps"

    ```bash
    man usermod | grep lock
    ```

```text
Which option needs to be set to execute a command as a different user using the "su" command? (long version of the option)
```

??? tip "Steps"

    ```bash
    man su | grep command
    ```
