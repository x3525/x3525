---
glightbox: true
icon: material/circle-small
---

# Active Directory Terminology

## Object

Nesne, AD ortamında bulunan OU (Organizational Unit), yazıcı, kullanıcı, domain denetleyici vb. gibi herhangi bir kaynak olarak tanımlanabilir.

## Attributes

AD içinde bulunan her nesne belirli bir nesnenin özelliklerini tanımlamak için kullanılan ilişkili bir dizi [öznitelik](https://learn.microsoft.com/en-us/windows/win32/adschema/attributes-all) bilgisine sahiptir. Bir bilgisayar nesnesi bilgisayar adı ve DNS adı gibi nitelikleri içerir. Tüm özniteliklerin LDAP (Lightweight Directory Access Protocol) sorguları gerçekleştirilirken kullanılabilecek ilişkili bir LDAP adı vardır.

## Schema

AD şeması herhangi bir kurumsal ortamın taslağıdır. AD veri tabanında ne tür nesnelerin bulunabileceğini ve bunlarla ilişkili nitelikleri tanımlar. AD nesnelerine karşılık gelen tanımları listeler ve her nesneyle ilgili bilgileri tutar. Örneğin AD içindeki kullanıcılar kullanıcı sınıfına, bilgisayar nesneleri ise bilgisayar sınıfına aittir. Bir sınıftan bir nesne oluşturulduğunda buna örnekleme adı verilir ve belirli bir sınıftan oluşturulan bir nesneye, o sınıfın örneği denir.

## Domain

Etki alanı, bilgisayarlar, kullanıcılar vb. gibi nesnelerin mantıksal bir grubudur. Etki alanları birbirinden tamamen bağımsız olarak çalışabilir veya güven ilişkileri aracılığıyla birbirine bağlanabilir.

## Forest

Orman, AD etki alanlarının bir koleksiyonudur. En üstteki kapsayıcıdır ve etki alanları, kullanıcılar, gruplar, bilgisayarlar vb. gibi tüm AD nesnelerini içerir. Orman, bir veya daha fazla etki alanı içerebilir. Her orman bağımsız olarak çalışır ancak diğer ormanlarla çeşitli güven ilişkileri olabilir.

## Tree

Ağaç, tek bir kök etki alanında başlayan AD etki alanlarının bir koleksiyonudur. Bir ağaçtaki her etki alanı diğer etki alanlarıyla bir sınırı paylaşır. Bir alan adı bir ağaçtaki başka bir alanın altına eklendiğinde ebeveyn-çocuk güven ilişkisi oluşur. Bir ağaçtaki tüm etki alanları, ağaca ait nesnelerle ilgili tüm bilgileri içeren standart bir Global Catalog paylaşır.

## Container

Konteyner nesneleri diğer nesneleri tutar ve dizin alt ağaç hiyerarşisinde tanımlanmış bir yere sahiptir.

## Leaf

Yaprak nesneler başka nesneler içermez ve alt ağaç hiyerarşisinin sonunda bulunur.

## Global Unique Identifier (GUID)

GUID, bir etki alanı kullanıcısı veya grubu oluşturulduğunda atanan benzersiz 128 bitlik bir değerdir. AD tarafından oluşturulan her nesneye bir GUID atanır. GUID, `ObjectGUID` niteliğinde depolanır ve bu özellik hiçbir zaman değişmez. Bir AD nesnesini (kullanıcı, grup, bilgisayar, etki alanı, etki alanı denetleyicisi vb.) sorgularken PowerShell kullanarak nesne GUID değerini sorgulayabiliriz. GUID, AD tarafından nesneleri tanımlamak için kullanılır. AD içinde GUID değerine göre arama yapmak aranılan nesneyi bulmanın en doğru ve güvenilir yoludur. AD numaralandırması yaparken `ObjectGUID` değerini belirtmek, hakkında bilgi aradığımız nesneye ait en doğru sonuçları almamızı sağlayacaktır.

## Security principals

Güvenlik sorumluları kullanıcılar, bilgisayar hesapları ve hatta bir kullanıcı veya bilgisayar hesabı bağlamında çalışan iş parçacıkları/işlemler de dahil olmak üzere işletim sisteminin kimliğini doğrulayabildiği her şeydir. AD güvenlik ilkeleri etki alanı içindeki diğer kaynaklara erişimi yönetebilen etki alanı nesneleridir.

## Security Identifier (SID)

Bir güvenlik tanımlayıcısı veya SID, bir güvenlik sorumlusu veya güvenlik grubu için benzersiz bir tanımlayıcı olarak kullanılır. Her hesap, grup veya işlemin, AD ortamında etki alanı denetleyicisi tarafından verilen ve güvenli bir veri tabanında saklanan kendine özgü bir SID değeri vardır. Bir SID yalnızca bir kez kullanılabilir. Güvenlik ilkesi silinse dahi o ortamda bir daha asla başka bir kullanıcı veya grubu tanımlamak amacıyla kullanılamaz. Ayrıca genel kullanıcıları ve grupları tanımlamak için kullanılan [iyi bilinen SID](https://learn.microsoft.com/en-us/windows-server/identity/ad-ds/manage/understand-security-identifiers#well-known-sids) değerleri vardır. Bunlar tüm işletim sistemlerinde aynıdır. Bunun bir örneği Everyone grubudur.

## Distinguished Name (DN)

Ayırt edici ad, AD içindeki bir nesnenin tam yolunu açıklar.

## Relative Distinguished Name (RDN)

Göreceli ayırt edici ad, nesneyi, adlandırma hiyerarşisindeki geçerli düzeydeki diğer nesnelerden benzersiz olarak tanımlayan ayırt edici adın tek bir bileşenidir. AD, aynı üst kapsayıcı altında aynı ada sahip iki nesneye izin vermez.

## sAMAccountName

Kullanıcının oturum açma adıdır. Benzersiz bir değer olmalıdır ve 20 veya daha az karakterden oluşmalıdır.

## userPrincipalName

Bu özellik AD içindeki kullanıcıları tanımlamanın başka bir yoludur. Bir prefix (kullanıcı hesabı adı) ve bir suffix (domain adı) birleşiminden oluşur.

## FSMO Roles

Beş adet FSMO (Flexible Single Master Operation) rolü vardır:

| Role | Description |
|---|---|
| Schema Master | AD içindeki bir nesneye uygulanabilecek tüm öznitelikleri tanımlayan AD şemasının okuma/yazma kopyasını yönetir. |
| Domain Naming Master | Etki alanı adlarını yönetir ve aynı ormanda aynı adı taşıyan iki etki alanının oluşturulmamasını sağlar. |
| Relative ID Master | Birden fazla nesnenin aynı SID değerine sahip olmamasını sağlamaya yardımcı olur. |
| Primary Domain Controller Emulator | Bu role sahip bilgisayar etki alanındaki yetkili DC olacaktır ve kimlik doğrulama isteklerine, parola değişikliklerine yanıt verecek ve grup ilkesi nesnelerini yönetecektir. |
| Infrastructure Master | Etki alanları arasında GUID, SID ve DN çevrimi yapar. Tek bir ormanda birden çok etki alanına sahip kuruluşlarda kullanılır. |

## Global Catalog

Genel katalog, tüm nesnelerin kopyalarını bir AD ormanında depolayan bir etki alanı denetleyicisidir. Genel katalog, geçerli etki alanındaki tüm nesnelerin tam kopyasını ve ormandaki diğer etki alanlarına ait nesnelerin kısmi bir kopyasını saklar. Standart etki alanı denetleyicileri, ormandaki farklı etki alanlarına ait olmayan ancak kendi etki alanına ait olan nesnelerin tam bir kopyasını tutar. Genel katalog hem kullanıcıların hem de uygulamaların, ormandaki bir etki alanındaki herhangi bir nesne hakkında bilgi bulmasına olanak tanır.

## Read-Only Domain Controller

RODC, salt okunur bir AD veri tabanına sahiptir. RODC içinde hiçbir AD hesabı parolası önbelleğe alınmaz (RODC bilgisayar hesabı ve RODC KRBTGT parolaları dışında). RODC ayrıca salt okunur bir DNS sunucusu içerir. Yönetici rolü ayrımına izin verir ve ortamdaki çoğaltma trafiğini azaltır.

## Replication

AD nesneleri güncellendiğinde AD içinde çoğaltma gerçekleşir. Bir DC (Domain Controller) eklendiğinde aralarındaki çoğaltmayı yönetmek için bağlantı nesneleri oluşturulur.

## Service Principal Name (SPN)

SPN, bir hizmet örneğini benzersiz şekilde tanımlar. Kerberos kimlik doğrulaması tarafından bir hizmetin örneğini, bir oturum açma hesabıyla ilişkilendirmek için kullanılırlar. Böylece istemci uygulamasının hesap adını bilmesine gerek kalmadan, bir hesabın kimliğini doğrulamak için hizmetten talepte bulunmasına olanak sağlanır.

## Group Policy Object (GPO)

GPO, ilke ayarlarının sanal koleksiyonudur. Her GPO benzersiz bir GUID değeri içerir. Bir GPO yerel dosya sistemi ayarlarını veya AD ayarlarını içerebilir. GPO ayarları hem kullanıcı hem de bilgisayar nesnelerine uygulanabilir. Domain içindeki tüm kullanıcılara ve bilgisayarlara uygulanabilir veya kuruluş birimi düzeyinde daha ayrıntılı bir şekilde tanımlanabilirler.

## Access Control List (ACL)

ACL, bir nesneye uygulanan erişim kontrol varlıklarının (ACE) sıralı koleksiyonudur.

## Access Control Entities (ACEs)

Bir ACL içindeki her ACE bir emanetçi (kullanıcı hesabı, grup hesabı veya oturum açma oturumu) tanımlar ve söz konusu emanetçi için izin verilen, reddedilen veya denetlenen erişim haklarını listeler.

## Discretionary Access Control List (DACL)

DACL, bir nesneye hangi güvenlik ilkelerine erişim izni verildiğini veya reddedildiğini tanımlar. ACE listesini içerir. Bir işlem güvenliği sağlanabilir bir nesneye erişmeye çalıştığında sistem, erişim izni verilip verilmeyeceğini belirlemek için nesnenin DACL bilgisindeki ACE değerini kontrol eder.

## System Access Control List (SACL)

Yöneticilerin güvenli nesnelere yapılan erişim girişimlerini günlüğe kaydetmesine olanak tanır.

## Fully Qualified Domain Name (FQDN)

FQDN, belirli bir bilgisayarın tam adıdır. Bir nesnenin DNS ağaç hiyerarşisindeki konumunu belirtmek için kullanılır. FQDN, IP adresini bilmeden bir AD içindeki bilgisayarları bulmak için kullanılabilir.

## Tombstone

Mezar taşı, AD içinde silinmiş nesneleri tutan bir konteyner nesnesidir. Bir nesne AD içinden silindiğinde Tombstone Lifetime olarak bilinen belirli bir süre boyunca kalmaya devam eder.

## AD Recycle Bin

AD geri dönüşüm kutusu, silinen AD nesnelerinin kurtarılmasını kolaylaştırmak için ilk olarak Windows Server 2008 R2 sürümünde tanıtılmıştır. Bu durum sistem yöneticilerinin nesneleri geri yüklemesini kolaylaştırmıştır. AD geri dönüşüm kutusu etkinleştirildiğinde silinen nesneler bir süre boyunca korunur ve gerektiğinde geri yüklenebilir. AD geri dönüşüm kutusunu kullanmanın en büyük avantajı, silinmiş bir nesnenin özniteliklerinin çoğunun korunmasıdır. Bu sayede silinmiş bir nesnenin önceki durumuna tamamen geri yüklenmesi mümkün olur.

## SYSVOL

SYSVOL klasörü veya paylaşımı, sistem ilkeleri, grup ilkesi ayarları, oturum açma/oturum kapatma komut dosyaları gibi etki alanındaki genel dosyaların kopyalarını saklar ve genellikle AD ortamında çeşitli görevleri gerçekleştirmek için yürütülen diğer komut dosyası türlerini içerir.

## AdminSDHolder

Korunan grupların üyelerine uygulanan güvenlik tanımlayıcısını tutan bir konteyner görevi görür.

## dsHeuristics

Orman çapında birden çok yapılandırma ayarını tanımlamak için kullanılan bir dize değeridir.

## adminCount

Bu niteliğin değeri 0 (sıfır) olarak ayarlanmışsa kullanıcı korunmaz. Saldırganlar genellikle bu değerin 1 olarak ayarlanmış olduğu hesapları ararlar. Bunlar genellikle ayrıcalıklı hesaplardır ve alan adının tamamının tehlikeye atılmasına yol açabilirler.

## Active Directory Users and Computers (ADUC)

ADUC, AD içindeki kullanıcıları, grupları, bilgisayarları ve kişileri yönetmek için yaygın olarak kullanılan bir GUI konsoludur. ADUC içinde yapılan değişiklikler PowerShell üzerinden de yapılabilir.

## ADSI Edit

AD içindeki nesneleri yönetmek için kullanılan bir GUI aracıdır. Bir nesnede mevcut olan herhangi bir özelliği ayarlamak veya silmek, nesneleri eklemek, kaldırmak ve taşımak için de kullanılabilir. Buradaki değişiklikler AD üzerinde büyük sorunlara neden olabileceğinden dikkatli kullanılmalıdır.

## sIDHistory

Bir nesneye daha önceden atanmış tüm SID değerlerini tutar. Güvenli olmayan bir şekilde ayarlanırsa saldırganlar tarafından kötüye kullanılabilir.

## NTDS.DIT

NTDS.dit dosyası AD kalbi olarak düşünülebilir. Kullanıcı ve grup nesneleri, grup üyeliği hakkındaki bilgiler ve parola hash dizeleri gibi AD verilerini depolayan bir veri tabanıdır.
