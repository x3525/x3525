---
glightbox: true
---

# Variables

* [ ] Değişken ismi, tanımlı bir anahtar kelime olamaz.
* [x] Değişken ismi, tanımlı bir anahtar kelime içerebilir.
* [ ] Değişken ismi, rakam ile başlayamaz.
* [x] Değişken ismi, rakam içerebilir.
* [ ] Değişken ismi, alt tire (`_`) dışında bir özel karakter içeremez.
* [x] Değişken ismi, alt tire (`_`) içerebilir.

!!! warning "Maximum Length"

    Değişken ismi sınırsız uzunlukta olabilir. Ancak bir değişkeni, diğer değişkenlerden ayırt etmek için sadece ilk 31 karakterine bakılır (ANSI C).

## Variable Declaration

```c
int x;
```

## Variable Initialization

```c
int x;
x = 9;
```

## Variable Declaration and Initialization

```c
int x = 9;
```

## Variable Declaration - Multiple

```c
int x, y, z;
```
