---
glightbox: true
---

# Registry

Korumalı kayıt defteri anahtarlarını düzenlemek için aşağıdaki adımlar takip edilerek tam izin kontrolü alınabilir:

1. İşlem yapılacak `Key` üzerinde ++right-button++ --> `Permissions...` seç.
2. Açılan pencerede `Advanced` tıkla.
3. Açılan pencerede `Owner` kısmında `Change` tıkla.
4. Açılan kutuya kullanıcı adını gir ve `Check Names` tıkla. Ardından `OK` bas ve çık.
5. Aynı pencerede `Replace owner on subcontainers and objects` kutucuğunu işaretle.
6. Aynı pencerede `Disable inheritance` bas.
7. Uyarı penceresi çıkarsa `Convert inherited permissions into explicit permissions on this object.` seçeneğini seç.
8. Aynı pencerede `Permissions` sekmesinde `Add` bas.
9. Açılan pencerede `Select a principal` bas. Adım 4 ve sonrasını tekrarla. Ardından `OK` bas ve çık.

| Context |
|---|
| `HKCR\Directory\Background` |

| Environment |
|---|
| `HKCU\Environment` |

| Open With |
|---|
| `HKCR\Applications` |

| Run |
|---|
| `HKCU\Software\Microsoft\Windows\CurrentVersion\Run` |
| `HKCU\Software\Microsoft\Windows\CurrentVersion\RunOnce` |
| `HKLM\Software\Microsoft\Windows\CurrentVersion\Run` |
| `HKLM\Software\Microsoft\Windows\CurrentVersion\RunOnce` |
