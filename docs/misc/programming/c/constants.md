---
glightbox: true
---

# Constants

Aşağıdaki kod satırını ele alalım:

```c
#define MAX 9
```

Kaynak kodun her yerinde `MAX` --> `9` değişimi yapılır (preprocessor tarafından).

Aşağıdaki kod satırını ele alalım:

```c
const int max = 9;
```

Buradaki `max` ifadesi sabit değişken olarak ele alınır ve bu değişken için hafızada gerekli yer tahsis edilir (compiler tarafından).
