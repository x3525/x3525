---
glightbox: true
---

# Vim Basics

## Modes

### NORMAL Mode

Vim, otomatik olarak NORMAL modda açılır. NORMAL mod haricinde bir modda iken tekrar NORMAL moda geçiş yapmak için ++escape++ tuşu ya da ++control+bracket-left++ tuş kombinasyonu kullanılabilir.

!!! info "Vim Motions"

    Vim motions (hareketler), imleci istenilen konuma hareket ettirmek için kullanılan tuşlardır.

| Input | Description |
|---|---|
| ++lower-j++ | Satır boyu aşağı (++down++) ilerle. |
| ++lower-k++ | Satır boyu yukarı (++up++) ilerle. |
| ++lower-h++ | Karakter boyu sola (++left++) ilerle. |
| ++lower-l++ | Karakter boyu sağa (++right++) ilerle. |
| ++lower-w++ | Kelime boyu sağa ilerle. |
| ++lower-b++ | Kelime boyu sola ilerle. |

!!! info "Count + Motion"

    Motion tuşları sayılar ile birlikte kullanılabilir. Örneğin ++3++ ++lower-k++ tuş kombinasyonu ile mevcut satırdan 3 satır yukarıda bulunan satıra hareket edilebilir.

| Input | Description |
|---|---|
| ++lower-d++ ++lower-d++ | Mevcut satırı sil. |
| ++lower-y++ ++lower-y++ | Mevcut satırı kopyala. |
| ++lower-p++ | Kopyalanan içeriği imleç sonrasına yapıştır. |
| ++p++ | Kopyalanan içeriği imleç öncesine yapıştır. |
| ++lower-u++ | Geri al. |
| ++control+lower-r++ | Yinele. |

### COMMAND Mode

NORMAL modda iken ++colon++ tuşuna basılarak COMMAND moda geçiş yapılabilir.

| Input | Description |
|---|---|
| `:w` | Değişiklikleri kaydet. |
| `:q` | Vim uygulamasından çık. |
| `:q!` | Değişiklikleri kaydetmeden çık. |
| `:wq` | Değişiklikleri kaydet ve çık. |
| `:x` | Değişiklikleri kaydet ve çık. |

!!! info "Command + Count + Motion"

    Komutlar, motion tuşları ile birlikte kullanılabilir. Örneğin ++lower-d++ ++2++ ++lower-j++ tuş kombinasyonu ile mevcut satır ve bu satırın altında bulunan 2 satır (toplamda 3 satır) silinebilir.

### INSERT Mode

NORMAL modda iken ++lower-i++ tuşuna basılarak INSERT moda geçiş yapılabilir.

Hem INSERT moda geçiş yapmak hem de imleci mevcut karakterin bir sağına hareket ettirmek için, NORMAL modda iken ++lower-a++ tuşuna basılabilir.

### VISUAL Mode

NORMAL modda iken ++lower-v++ tuşuna basılarak VISUAL moda geçiş yapılabilir.

Bu modda iken, NORMAL modda bahsedilen motion tuşları aynı şekilde kullanılabilir. Ek olarak, yapılan hareketler ile metin seçimi gerçekleştirilir.

| Input | Description |
|---|---|
| ++lower-y++ | Mevcut seçimi kopyala. |
| ++lower-p++ | Kopyalanan seçimi imleç sonrasına yapıştır. |
| ++p++ | Kopyalanan seçimi imleç öncesine yapıştır. |

### VISUAL LINE Mode

NORMAL modda iken ++v++ tuşuna basılarak VISUAL LINE moda geçiş yapılabilir.

Bu modda iken, VISUAL moda benzer şekilde metin seçimi gerçekleştirilir. Farklı olarak, seçim işlemi satır satır işleme alınır.

## Movement

### Horizontal Movement

| Input | Description |
|---|---|
| ++lower-f++ | Ardından verilecek karakteri bulmak için sağa ilerle. |
| ++f++ | Ardından verilecek karakteri bulmak için sola ilerle. |

!!! info "Forward Find"

    ++lower-f++ kullanımına örnek olarak ++lower-f++ ++equal++ verilebilir. Bu sayede ilk ++equal++ karakterine gidilir.

    ++semicolon++ ile bir sonraki ++equal++ karakterine gidilir.

    ++comma++ ile bir önceki ++equal++ karakterine gidilir.

### Vertical Movement

| Input | Description |
|---|---|
| ++lower-g++ ++lower-g++ | Sayfa başına git. |
| ++g++ | Sayfa sonuna git. |
| ++lower-o++ | İmleç sonrasına yeni satır ekle ve INSERT moda geç. |
| ++o++ | İmleç sonrasına öncesine yeni satır ekle ve INSERT moda geç. |
| ++control+lower-b++ | Tam sayfa yukarı kaydır. |
| ++control+lower-f++ | Tam sayfa aşağı kaydır. |

## Search

| Input | Description |
|---|---|
| ++slash++ | İleri yönde aramayı başlat. Aranacak ifadeyi gir ve ++enter++ tuşuna bas. |
| ++question++ | Geri yönde aramayı başlat. Aranacak ifadeyi gir ve ++enter++ tuşuna bas. |
| ++lower-n++ | İleri/geri yönde bir sonraki eşleşmeyi bul. |
| ++n++ | Geri/ileri yönde bir sonraki eşleşmeyi bul. |
