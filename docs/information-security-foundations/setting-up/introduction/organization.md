---
glightbox: true
icon: material/circle-small
---

# Organization

Klasör yapısını, sızma testi aşamalarına, işletim sistemlerine veya elde edilen verilere göre organize etmek düzenli çalışmamızı sağlar.

## 1. Discovered Information

Keşfedilen bilgiler hedef şirkete karşı kullanılabilecek bilgilerdir. Bu tür bilgiler OSINT, aktif taramalar ve bilgi kaynaklarının analizi ile elde edilir.

## 2. Processing

Sızma testi sırasında birçok farklı bilgi elde edilir. Bu sonuçlar daha sonra uygulanacak adımlar konusunda fikir verebilir. Bu nedenle, araştırılması gereken her şey not edilmelidir.

## 3. Results

Sızma testi sonrası elde edilen sonuçlar çok önemlidir. Bu sonuçlar dokümantasyon amacıyla da kullanılabilir. Kritik bilgi parçalarını filtrelemek kolay değildir. Bu, tecrübe ile elde edilebilecek bir yetenektir.

## 4. Logging

Log tutmak sızma testinin önemli bir parçasıdır. Test sırasında başka kişiler tarafından bir saldırı gerçekleştirilirse ve bu saldırı sonucunda bir hasar meydana gelirse, bu hasarın bizden kaynaklı olmadığını tutulan log dosyaları ile kanıtlayabiliriz. Bunun için Linux sistemlerinde `date` ve `script` isimli araçları, Windows sistemlerinde ise `Get-Date` ve `Start-Transcript` isimli araçları kullanabiliriz. Bu araçları kullanarak dosya ismi o anki tarih bilgisi olan bir log dosyası oluştururuz. Böylece çalıştırdığımız her komut -biz durdurana kadar- kayıt altına alınmış olur.

### Script

Kaydı başlat:

```bash
script "$(date +"%m-%d-%Y_%H-%M")"-filename.log
```

Kaydı durdur:

```bash
exit
```

### Start-Transcript

Kaydı başlat:

```powershell
Start-Transcript -Path "$(Get-Date -UFormat "%m-%d-%Y_%H-%M")-filename.log"
```

Kaydı durdur:

```powershell
Stop-Transcript
```
