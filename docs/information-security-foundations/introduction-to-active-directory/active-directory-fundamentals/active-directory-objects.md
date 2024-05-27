---
glightbox: true
icon: material/circle-small
---

# Active Directory Objects

## AD Objects

Nesne, AD ortamında bulunan yazıcılar, kullanıcılar, etki alanı denetleyicileri gibi herhangi bir kaynak olarak tanımlanabilir.

## Users

Kullanıcılar, yaprak nesneler olarak kabul edilirler. Bu, içlerinde başka hiçbir nesneyi içeremeyecekleri anlamına gelir. Bir kullanıcı nesnesi bir güvenlik sorumlusu olarak kabul edilir ve bir güvenlik tanımlayıcısına (SID) ve bir genel benzersiz tanımlayıcıya (GUID) sahiptir. Kullanıcı nesnelerinin görünen adı, son giriş zamanı, son parola değiştirme tarihi, hesap açıklaması, yöneticisi ve adresi gibi birçok özelliği vardır.

## Contacts

Genellikle harici bir kullanıcıyı temsil etmek için kullanılır ve ad, soyad, telefon numarası vb. gibi bilgi niteliklerini içerir. Bunlar yaprak nesnelerdir ve güvenlik sorumlusu olarak kabul edilmezler, dolayısıyla bu nesnelere SID atanmaz, sadece GUID atanır.

## Computers

Bilgisayar, AD ağına (iş istasyonu veya sunucu) katılan herhangi bir bilgisayardır. Bilgisayarlar yaprak nesnelerdir, çünkü başka nesneler içermezler. Güvenlik sorumlusu olarak kabul edilirler.

## Groups

Bir grup, kullanıcılar, bilgisayarlar ve hatta diğer gruplar da dahil olmak üzere başka nesneleri içerebildiğinden kapsayıcı nesne olarak kabul edilir. Güvenlik sorumlusu olarak kabul edilirler.

## Organizational Units (OUs)

OU, sistem yöneticilerinin yönetim kolaylığı için benzer nesneleri depolamak için kullanabileceği bir kapsayıcıdır. Genellikle bir kullanıcı hesabına tam yönetim hakları vermeden görevlerin idari olarak devredilmesi için kullanılır.

## Domain

Etki alanları, gruplar ve OU gibi kapsayıcı nesneler halinde düzenlenen kullanıcılar ve bilgisayarlar gibi nesneleri içerir. Her alanın kendine ait ayrı bir veri tabanı ve etki alanındaki tüm nesnelere uygulanabilecek politika kümeleri vardır.

## Domain Controllers

Etki alanı denetleyicileri bir AD ağının beynidir. Kimlik doğrulama isteklerini yönetir, ağdaki kullanıcıları doğrular ve etki alanındaki çeşitli kaynaklara kimlerin erişebileceğini kontrol ederler. Tüm erişim istekleri etki alanı denetleyicisi aracılığıyla doğrulanır. Ayrıca güvenlik politikalarını uygular ve etki alanındaki diğer tüm nesnelerle ilgili bilgileri depolar.

## Sites

AD içindeki bir site, yüksek hızlı bağlantılar kullanılarak bağlanan bir veya daha fazla alt ağdaki bir dizi bilgisayardır. Etki alanı denetleyicileri arasında çoğaltmanın verimli bir şekilde çalışmasını sağlamak için kullanılırlar.

## Built-in

AD etki alanında varsayılan grupları tutan bir kapsayıcıdır. Bir AD alanı oluşturulduğunda önceden tanımlanırlar.
