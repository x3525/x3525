---
glightbox: true
---

# Hide a User from Login Screen

Regedit uygulamasında aşağıdaki konuma git:

```text
HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\
```

Bu konumda bulunan `Winlogon` anahtarı altında `SpecialAccounts` isminde bir anahtar oluştur ve `SpecialAccounts` anahtarı altında `UserList` isminde bir anahtar oluştur. Ardından `UserList` anahtarı altında `DWORD (32-bit) Value` değeri oluştur. Oluşturulan bu değerin adını, gizlemek istediğin kullanıcı hesabının adıyla olacak şekilde ayarla ve değerini `0` olarak belirle.

Değişikliklerin etkili olabilmesi için yeniden başlatma gerekebilir.
