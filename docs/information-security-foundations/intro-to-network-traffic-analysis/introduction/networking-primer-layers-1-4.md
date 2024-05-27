---
glightbox: true
icon: material/circle-small
---

# Networking Primer - Layers 1-4

## OSI / TCP-IP Models

### PDU Packet Breakdown

PDU incelenirken kapsülleme sürecini aklımızda bulundurmakta fayda vardır. Veriler protokol yığınında aşağı doğru ilerledikçe, her katman, önceki katmanın verilerini yeni bir baloncuk içinde toplar. Bu baloncuk, o katmana ait gerekli bilgileri PDU başlığına ekler.

![](../assets/images/pdu-wireshark.png)

Yukarıdaki resim, PDU yapısını Wireshark paket dökümüyle yan yana göstermektedir. PDU sırası ters olarak verilmiştir.

## TCP / UDP, Transport Mechanisms

| TCP | UDP |
|---|---|
| Bağlantı yönelimli. | Bağlantısız. Gönder ve unut. |
| Bağlantının kurulduğundan emin olmak için 3 yönlü el sıkışma. | Hedefin dinleyip dinlemediği bilinmez. |
| Akış tabanlı görüşme. | Paket paket veri gönderimi. |
| Verileri açıklamak için SEQ ve ACK numaraları. | Veriler açıklanmaz. |
| Yerleşik fonksiyonlar nedeniyle yavaş. | Hızlı. Emniyetsiz. |
