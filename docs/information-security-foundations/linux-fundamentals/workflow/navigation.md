---
glightbox: true
icon: material/help
---

# Navigation

| Command | Description |
|---|---|
| `ls` | Dizin içeriğini listeler. |
| `ls -a` | Dizin içeriğini gizli dosyalarla birlikte listeler. |
| `ls -l` | Dizin içeriğini daha fazla bilgi gösterecek şekilde listeler. |
| `cd` | Dizinler arasında gezinmeyi sağlar. |
| `cd ~` | Mevcut kullanıcının ev dizinine geçiş yapar. |
| `cd -` | Son bulunulan dizine geri döner. |
| `cd ..` | Bir üst dizine geçiş yapar. |
| `clear` | Shell ekranını temizler. |
| `clear -x` | Shell ekranını kısmen temizler. |

## Questions

```text
What is the name of the hidden "history" file in the htb-user's home directory?
```

??? tip "Steps"

    ```bash
    cd ~
    ls -a
    ```

```text
What is the index number of the "sudoers" file in the "/etc" directory?
```

??? tip "Steps"

    ```bash
    ls -i /etc/sudoers
    ```
