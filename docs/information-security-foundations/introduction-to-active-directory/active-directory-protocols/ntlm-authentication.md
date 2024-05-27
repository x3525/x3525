---
glightbox: true
icon: material/circle-small
---

# NTLM Authentication

NTLMv1 ve NTLMv2, LM veya NT hash kullanan kimlik doğrulama protokolleridir.

## LM

LM (LAN Manager) hash, Windows işletim sistemi tarafından kullanılan en eski parola depolama mekanizmasıdır. Önemli güvenlik zayıflıkları nedeniyle modern cihazlarda artık kullanılmamaktadır.

## NTHash (NTLM)

NTLM hash, modern Windows sistemlerinde kullanılır. Bir tür [challenge-response](https://csrc.nist.gov/glossary/term/challenge_response_protocol) (meydan okuma ve karşılık verme) kimlik doğrulama protokolüdür ve kimlik doğrulamak için üç mesaj kullanır:

1. `NEGOTIATE_MESSAGE`
2. `CHALLENGE_MESSAGE`
3. `AUTHENTICATE_MESSAGE`

NTLM hash LM hash ile karşılaştırıldığında daha güçlüdür.
