---
glightbox: true
icon: material/help
---

# Find Files and Directories

## Find

Aşağıda, sistemde arama yapmak için kullanılan araçlardan biri olan `find` aracına ait örnek bir komut verilmiştir:

```bash
find / -type f -name "*.conf" -size +20k -exec ls -al {} \; 2> /dev/null
```

| Command | Description |
|---|---|
| `find` | Dizin hiyerarşisinde dosyaları aramaya yarar. |
| `-type f` | Aranan dosyaların tipi belirtilir. Burada `f` file anlamına gelir. |
| `-name "*.conf"` | Aranan dosyaların adı belirtilir. Burada .conf uzantısına sahip olan dosyalar anlamına gelir. |
| `-size +20k` | Aranan dosyaların boyutu belirtilir. Burada 20 KiB boyutundan daha büyük olan dosyalar anlamına gelir. |
| `-exec ls -al {} \;` | Süslü parantezler, bulunan her bir sonuç için yer tutucu olarak kullanılır. Ters eğik çizgi sonraki karakterin shell tarafından yorumlanmasını önler. Aksi takdirde noktalı virgül komutu sonlandırır ve yeniden yönlendirmeye ulaşılamaz. |
| `2> /dev/null` | Yeniden yönlendirme ile hatalar göz ardı edilir. |

## Locate

Arama yapmak için kullanılan diğer bir araç `locate` isimli araçtır. Bu araç sistemde arama yapmanın daha hızlı bir yolunu sunar ve `find` aracının aksine, mevcut dosya ve klasörlerle ilgili tüm bilgileri içeren yerel bir veri tabanıyla çalışır. Veri tabanını aşağıdaki komutla güncelleyebiliriz:

```bash
sudo updatedb
```

Ardından aşağıdaki şekilde örnek bir arama gerçekleştirebiliriz:

```bash
locate "*.conf"
```

## Questions

```text
What is the name of the config file that has been created after 2020-03-03 and is smaller than 28k but larger than 25k?
```

??? tip "Steps"

    ```bash
    sudo find / -name "*.conf" -type f -newermt 2020-03-03 -size +25k -size -28k
    ```

```text
How many files exist on the system that have the ".bak" extension?
```

??? tip "Steps"

    ```bash
    sudo find / -name "*.bak" -type f 2> /dev/null | wc -l
    ```

```text
Submit the full path of the "xxd" binary.
```

??? tip "Steps"

    ```bash
    sudo find / -name "xxd" -type f 2> /dev/null
    ```
