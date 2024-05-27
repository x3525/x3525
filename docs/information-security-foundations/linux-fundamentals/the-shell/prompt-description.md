---
glightbox: true
icon: material/circle-small
---

# Prompt Description

Terminali açtığımızda shell isteminde gözüken `$` sembolü ayrıcalıksız kullanıcı hesabını temsil eder. Eğer `#` sembolü gözüküyorsa ayrıcalıklı `root` hesabını temsil eder.

Shell isteminin nasıl gözükeceği PS1 (Prompt String 1) değişkeni ile belirlenebilir. Bunun için bazı özel karakterler kullanılmaktadır:

| Special Character | Description |
|---|---|
| `\d` | Tarih (Mon Feb 6) |
| `\D{%Y-%m-%d}` | Tarih (YYYY-MM-DD) |
| `\H` | Tam makine adı |
| `\j` | Shell tarafından yönetilen iş sayısı |
| `\n` | Yeni satır |
| `\r` | Satır başı |
| `\s` | Shell adı |
| `\t` | Güncel saat, 24 saatlik (HH:MM:SS) |
| `\T` | Güncel saat, 12 saatlik (HH:MM:SS) |
| `\@` | Güncel saat |
| `\u` | Mevcut kullanıcı adı |
| `\w` | Geçerli çalışma dizinine ait tam yol |
