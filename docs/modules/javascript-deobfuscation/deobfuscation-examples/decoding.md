---
glightbox: true
icon: material/circle-small
---

# Decoding

## Base64

### Base64 Encode

```bash
echo https://www.hackthebox.eu/ | base64
```

```text title="Output"
aHR0cHM6Ly93d3cuaGFja3RoZWJveC5ldS8K
```

### Base64 Decode

```bash
echo aHR0cHM6Ly93d3cuaGFja3RoZWJveC5ldS8K | base64 -d
```

```text title="Output"
https://www.hackthebox.eu/
```

## Hex

### Hex Encode

```bash
echo https://www.hackthebox.eu/ | xxd -p
```

```text title="Output"
68747470733a2f2f7777772e6861636b746865626f782e65752f0a
```

### Hex Decode

```bash
echo 68747470733a2f2f7777772e6861636b746865626f782e65752f0a | xxd -p -r
```

```text title="Output"
https://www.hackthebox.eu/
```

## Caesar/Rot13

### Rot13 Encode

```bash
echo https://www.hackthebox.eu/ | tr 'A-Za-z' 'N-ZA-Mn-za-m'
```

```text title="Output"
uggcf://jjj.unpxgurobk.rh/
```

### Rot13 Decode

```bash
echo uggcf://jjj.unpxgurobk.rh/ | tr 'A-Za-z' 'N-ZA-Mn-za-m'
```

```text title="Output"
https://www.hackthebox.eu/
```

## Other Types of Encoding

[Cipher Identifier](https://www.boxentriq.com/code-breaking/cipher-identifier) gibi araçlar, kodlama türünü otomatik olarak belirlememize yardımcı olabilir.
