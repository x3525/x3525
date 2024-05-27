---
glightbox: true
icon: material/help
---

# Filter Contents

## Cut

Aşağıdaki komut `cat` ile elde edilen çıktıdaki her bir satırı `:` karakterinden parçalara ayırır ve bu parçalardan 1. sütunu seçer:

```bash
cat /etc/passwd | cut -d":" -f1
```

## Tr

Aşağıdaki komut `cat` ile elde edilen çıktıdaki her bir `:` karakterini boşluk karakteri ile değiştirir:

```bash
cat /etc/passwd | tr ":" " "
```

## Column

Aşağıdaki komut `cat` ile elde edilen çıktıdaki her bir `:` karakterini boşluk karakteri ile değiştirir ve son oluşan görünümü tablo haline çevirir:

```bash
cat /etc/passwd | tr ":" " " | column -t
```

## Sed

Aşağıdaki komut `cat` ile elde edilen çıktıdaki her bir `bin` kelimesini `serhat` kelimesi ile değiştirir:

```bash
cat /etc/passwd | sed 's/bin/serhat/g'
```

| Command | Description |
|---|---|
| `s` | Operasyon türü. Burada `s` yer değiştirme (substitution) anlamına gelir. |
| `bin/serhat` | Bu ifade `bin` kelimesinin `serhat` kelimesi ile değiştirileceği anlamına gelir. |
| `g` | Yer değiştirme işleminin, aynı satırdaki tüm eşleşmeler için yapılacağını belirtir. |

## Questions

```text
How many services are listening on the target system on all interfaces? (Not on localhost and IPv4 only)
```

??? tip "Steps"

    ```bash
    ss -H4 state listening | grep -Ev "127\.*" | wc -l
    ```

```text
Determine what user the ProFTPd server is running under. Submit the username as the answer.
```

??? tip "Steps"

    ```bash
    cat /etc/passwd | grep proftpd
    ```

```text
Use cURL from your Pwnbox (not the target machine) to obtain the source code of the "https://www.inlanefreight.com" website and filter all unique paths of that domain. Submit the number of these paths as the answer.
```

??? tip "Steps"

    ```bash
    curl https://www.inlanefreight.com > source.txt
    cat source.txt | tr " " "\n" | grep -oE "(\"|').*https://www\.inlanefreight\.com.*(\"|')" | tr -d "\"'" | sort -u | wc -l
    ```
