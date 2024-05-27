---
glightbox: true
icon: material/help
---

# Subnetting

IPv4 adreslerinden oluşan bir adres aralığının daha küçük birkaç adres aralığına bölünmesine alt ağ oluşturma adı verilir.

Örnek olarak aşağıdaki IPv4 adresini ve alt ağ maskesini ele alalım:

| IPv4 Address | Subnet Mask | CIDR |
|---|---|---|
| 192.168.12.160 | 255.255.255.192 | 192.168.12.160/26 |

## Network Part

| 1st Octet | 2nd Octet | 3rd Octet | 4th Octet | Decimal |
|---|---|---|---|---|
| `{==11000000==}` | `{==10101000==}` | `{==00001100==}` | `{==10==}100000` | 192.168.12.160{==/26==} |
| `{==11111111==}` | `{==11111111==}` | `{==11111111==}` | `{==11==}000000` | {==255.255.255.192==} |
| /8 | /16 | /24 | /32 ||

## Host Part

| 1st Octet | 2nd Octet | 3rd Octet | 4th Octet | Decimal |
|---|---|---|---|---|
| `11000000` | `10101000` | `00001100` | `10{==100000==}` | 192.168.12.160/26 |
| `11111111` | `11111111` | `11111111` | `11{==000000==}` | 255.255.255.192 |
| /8 | /16 | /24 | /32 ||

## Separation Of Network & Host Parts

Alt ağ maskesi, host kısmı ve network kısmı arasındaki ayrımın nerede gerçekleşeceğini belirler:

| 1st Octet | 2nd Octet | 3rd Octet | 4th Octet | Decimal |
|---|---|---|---|---|
| `11000000` | `10101000` | `00001100` | `10{== ==}100000` | 192.168.12.160/26 |
| `{==11111111==}` | `{==11111111==}` | `{==11111111==}` | `{==11 ==}000000` | 255.255.255.192 |
| /8 | /16 | /24 | /32 ||

## Network Address

IPv4 adresinin host kısmındaki tüm bitleri 0 (sıfır) olarak ayarlarsak ilgili alt ağın network adresini elde ederiz:

| 1st Octet | 2nd Octet | 3rd Octet | 4th Octet | Decimal |
|---|---|---|---|---|
| `11000000` | `10101000` | `00001100` | `10{== 000000==}` | {==192.168.12.128==}/26 |
| `{==11111111==}` | `{==11111111==}` | `{==11111111==}` | `{==11 ==}000000` | 255.255.255.192 |
| /8 | /16 | /24 | /32 ||

## Broadcast Address

IPv4 adresinin host kısmındaki tüm bitleri 1 olarak ayarlarsak yayın adresini elde ederiz:

| 1st Octet | 2nd Octet | 3rd Octet | 4th Octet | Decimal |
|---|---|---|---|---|
| `11000000` | `10101000` | `00001100` | `10{== 111111==}` | {==192.168.12.191==}/26 |
| `{==11111111==}` | `{==11111111==}` | `{==11111111==}` | `{==11 ==}000000` | 255.255.255.192 |
| /8 | /16 | /24 | /32 ||

Böylece ilk ve son IP adresleri aşağıdaki gibi olmuş olur:

| First Host | Last Host |
|---|---|
| 192.168.12.129 | 192.168.12.190 |

## Subnetting Into Smaller Networks

Aynı örnek üzerinden gidelim. Elimizdeki alt ağı 4 ek alt ağa bölmemiz gerektiğini varsayalım. 4 sayısını elde etmek için 2^2 üstel ifadesini kullanırız. Bu ifadede üst olan 2 sayısı, subnet mask kısmına eklenecek 1 miktarını ifade eder:

| 1st Octet | 2nd Octet | 3rd Octet | 4th Octet | Decimal |
|---|---|---|---|---|
| `11000000` | `10101000` | `00001100` | `1000{== ==}0000` | 192.168.12.128{==/28==} |
| `{==11111111==}` | `{==11111111==}` | `{==11111111==}` | `{==1111 ==}0000` | {==255.255.255.240==} |
| /8 | /16 | /24 | /32 ||

Bize en başta verilen ağda kullanılabilir 64 IP adresi bulunduğundan, ağı 4 alt ağa böldüğümüzde her ağa 16 IP adresi düşer. Bu sayıyı ilk alt ağdan son alt ağa kadar ekleyerek gidersek, her alt ağa ait istenen bilgileri elde etmiş oluruz:

| Subnet No. | Network Address | First Host | Last Address | Broadcast Address |
|---|---|---|---|---|
| 1 | {==192.168.12.128==} | 192.168.12.129 | 192.168.12.142 | {==192.168.12.143==} |
| 2 | {==192.168.12.144==} | 192.168.12.145 | 192.168.12.158 | {==192.168.12.159==} |
| 3 | {==192.168.12.160==} | 192.168.12.161 | 192.168.12.174 | {==192.168.12.175==} |
| 4 | {==192.168.12.176==} | 192.168.12.177 | 192.168.12.190 | {==192.168.12.191==} |

## Questions

```text
Submit the decimal representation of the subnet mask from the following CIDR: 10.200.20.0/27
```

??? tip "Steps"

    /27 --> 11111111.11111111.11111111.11100000

    11111111.11111111.11111111.11100000 --> {==255.255.255.224==}

```text
Submit the broadcast address of the following CIDR: 10.200.20.0/27
```

??? tip "Steps"

    /27 --> 11111111.11111111.11111111.111|00000

    10.200.20.0 --> 00001010.11001000.00010100.000|00000

    00001010.11001000.00010100.000|11111 --> {==10.200.20.31==}

```text
Split the network 10.200.20.0/27 into 4 subnets and submit the network address of the 3rd subnet as the answer.
```

??? tip "Steps"

    10.200.20.0 <--> 10.200.20.31 = 32

    32 / 4 = 8

    10.200.20.0, 10.200.20.8, {==10.200.20.16==}, 10.200.20.24

```text
Split the network 10.200.20.0/27 into 4 subnets and submit the broadcast address of the 2nd subnet as the answer.
```

??? tip "Steps"

    10.200.20.0 <--> 10.200.20.31 = 32

    32 / 4 = 8

    10.200.20.31, 10.200.20.23, {==10.200.20.15==}, 10.200.20.7
