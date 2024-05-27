---
glightbox: true
---

# Tmux Basics

## What Is It?

[Tmux](https://github.com/tmux/tmux/wiki) bir terminal çoklayıcı (multiplexer) yazılımıdır. Bir terminaldeki çeşitli programlar arasında geçiş yapmayı kolaylaştırır.

Tmux 3 katmandan oluşur:

1. Sessions (Oturumlar)
2. Windows (Pencereler/Sekmeler)
3. Panes (Bölmeler)

## 1. Sessions

Oturumlar çalışma ortamlarının ayrılması açısından faydalıdır.

!!! info "Command Mode"
    Tmux içerisinde komut moduna girmek için ++control+b++ ve ardından ++colon++ tuşuna basılmalıdır.

Aşağıdaki tabloda tmux oturumları için bir cheat sheet verilmiştir ([kaynak](https://tmuxcheatsheet.com/)):

| Command | Description |
|---|---|
| `:tmux` | Yeni bir oturum başlat. |
| `:tmux new -s s_name` | Adı `s_name` olan yeni bir oturum başlat. |
| ++control+b++ ++d++ | Mevcut oturumdan ayrıl (işlemler arka planda çalışır). |
| `:tmux a` | Son oturuma bağlan. |
| `:tmux a -t s_name` | Adı `s_name` olan oturuma bağlan. |
| `:tmux kill-session -t s_name` | Adı `s_name` olan oturumu sonlandır. |
| `:tmux ls` | Tüm oturumları göster. |

## 2. Windows

Tmux arayüzü sekmelerden oluşur ancak bu sekmelere pencereler denir. Mevcut pencere isminin yanında asterisk (`*`) işareti bulunur.

!!! info "Command Mode"
    Tmux içerisinde komut moduna girmek için ++control+b++ ve ardından ++colon++ tuşuna basılmalıdır.

Aşağıdaki tabloda tmux pencereleri için bir cheat sheet verilmiştir ([kaynak](https://tmuxcheatsheet.com/)):

| Command | Description |
|---|---|
| ++control+b++ ++c++ | Yeni bir pencere oluştur. |
| ++control+b++ ++comma++ | Mevcut pencereyi yeniden adlandır. |
| ++control+b++ ++n++ | Sonraki pencereye geçiş yap. |
| ++control+b++ ++1++ | Numarası verilen pencereye geçiş yap. |
| ++control+b++ ++x++ | Mevcut pencereyi kapat. |
| ++control+b++ ++w++ | Pencereleri GUI desteği ile listele. |

## 3. Panes

Bölmeler kullanılarak herhangi bir tmux penceresi bölmelere ayrılabilir.

!!! info "Command Mode"
    Tmux içerisinde komut moduna girmek için ++control+b++ ve ardından ++colon++ tuşuna basılmalıdır.

Aşağıdaki tabloda tmux bölmeleri için bir cheat sheet verilmiştir ([kaynak](https://tmuxcheatsheet.com/)):

| Command | Description |
|---|---|
| ++control+b++ ++double-quote++ | Geçerli bölmeyi yatay bir çizgi ile böl (dikey düzen). |
| ++control+b++ ++x++ | Geçerli bölmeyi kapat. |
| ++control+b++ ++up++ | Yukarı bölmeye geç (art arda HIZLI basılabilir). |
| ++control+b++ ++down++ | Aşağı bölmeye geç (art arda HIZLI basılabilir). |
| ++control+b++ ++left++ | Sol bölmeye geç (art arda HIZLI basılabilir). |
| ++control+b++ ++right++ | Sağ bölmeye geç (art arda HIZLI basılabilir). |
| ++control+b++ ++control+up++ | Geçerli bölme yüksekliğini yukarı doğru yeniden boyutlandır. |
| ++control+b++ ++control+down++ | Geçerli bölme yüksekliğini aşağı doğru yeniden boyutlandır. |
| ++control+b++ ++control+left++ | Geçerli bölme genişliğini sola doğru yeniden boyutlandır. |
| ++control+b++ ++control+right++ | Geçerli bölme genişliğini sağa doğru yeniden boyutlandır. |

## Copy Mode

Tmux ile fareye gerek duymadan sadece klavye ile kopyalama işlemleri yapılabilir.

!!! info "Command Mode"
    Tmux içerisinde komut moduna girmek için ++control+b++ ve ardından ++colon++ tuşuna basılmalıdır.

Kopyalama modunu kullanabilmek için tmux yapılandırma dosyasında aşağıdaki satır mevcut olmalıdır:

```text title=".tmux.conf" linenums="1"
setw -g mode-keys vi
```

Aşağıdaki tabloda tmux kopyalama modu için bir cheat sheet verilmiştir ([kaynak](https://tmuxcheatsheet.com/)):

| Command | Description |
|---|---|
| ++control+b++ ++open-bracket++ | Kopyalama moduna gir. |
| ++space++ | Metin seçimini başlat. |
| ++enter++ | Seçilen metni kopyala (buffer içine kaydet). |
| ++control+b++ ++close-bracket++ | Önceden kopyalanan metni yapıştır. |
| ++q++ | Kopyalama modundan çık. |
