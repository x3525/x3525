---
glightbox: true
icon: material/circle-small
---

# System Logs

## Kernel logs

Bu günlükler donanım sürücüleri, sistem çağrıları ve kernel olayları da dahil olmak üzere sistemin çekirdeği hakkında bilgiler içerir ve `/var/log/kern.log` dosyasında saklanırlar. Bu günlükler, saldırganların sisteme erişim sağlamak için hedef alabileceği savunmasız veya güncel olmayan sürücülerin varlığını ortaya çıkarabilir. Ayrıca sistem çökmeleri, kaynak sınırlamaları ve hizmet reddine veya diğer güvenlik sorunlarına yol açabilecek diğer olaylara ilişkin bilgiler de sağlayabilirler. Ek olarak kernel günlükleri, sistemde kötü amaçlı yazılımların varlığını gösterebilecek şüpheli sistem çağrılarını veya diğer etkinlikleri tanımlamamıza yardımcı olabilir. Bu günlükler izlenerek şüpheli davranışları tespit edebilir ve sistemin daha fazla zarar görmesini önlemek için uygun önlemler alınabilir.

## System logs

Bu günlükler hizmetin başlatılması ve durdurulması, oturum açma denemeleri ve sistemin yeniden başlatılması gibi sistem düzeyindeki olaylarla ilgili bilgileri içerir ve `/var/log/syslog` dosyasında saklanırlar. Oturum açma denemeleri, hizmet başlatma ve durdurma işlemleri ve sistem düzeyindeki diğer olaylar analiz edilerek sistemdeki olası erişimler veya etkinlikler tespit edilebilir. Bu, kötüye kullanılabilecek güvenlik açıklarını belirlememize ve bu riskleri azaltmak için güvenlik önlemleri önermemize yardımcı olabilir. Ayrıca sistem günlüğü, başarısız hizmet başlatmaları veya sistem yeniden başlatmaları gibi sistemin kullanılabilirliğini veya performansını etkileyebilecek olası sorunları tanımlamak için de kullanılabilir.

## Authentication logs

Bu günlükler, başarılı ve başarısız girişimler de dahil olmak üzere kullanıcı kimlik doğrulama girişimleri hakkında bilgiler içerir ve `/var/log/auth.log` dosyasında saklanırlar. Bu günlükler, sistem günlüklerine benzer oturum açma bilgilerini içerse de özellikle kullanıcı kimlik doğrulama girişimlerine odaklandığından potansiyel güvenlik tehditlerini tanımlamak için daha değerli bir kaynaktır. Bu nedenle sistemin güvenli olduğundan emin olmak için bu günlüklerin incelenmesi önemlidir.

## Auth.log

```text title="Auth.log" linenums="1"
Feb 28 2023 18:15:01 sshd[5678]: Accepted publickey for admin from 10.14.15.2 port 43210 ssh2: RSA SHA256:+KjEzN2cVhIW/5uJpVX9n5OB5zVJ92FtCZxVzzcKjw
Feb 28 2023 18:15:03 sudo:   admin : TTY=pts/1 ; PWD=/home/admin ; USER=root ; COMMAND=/bin/bash
Feb 28 2023 18:15:05 sudo:   admin : TTY=pts/1 ; PWD=/home/admin ; USER=root ; COMMAND=/usr/bin/apt-get install netcat-traditional
Feb 28 2023 18:15:08 sshd[5678]: Disconnected from 10.14.15.2 port 43210 [preauth]
Feb 28 2023 18:15:12 kernel: [  778.941871] firewall: unexpected traffic allowed on port 22
Feb 28 2023 18:15:15 auditd[9876]: Audit daemon started successfully
Feb 28 2023 18:15:18 systemd-logind[1234]: New session 4321 of user admin.
Feb 28 2023 18:15:21 CRON[2345]: pam_unix(cron:session): session opened for user root by (uid=0)
Feb 28 2023 18:15:24 CRON[2345]: pam_unix(cron:session): session closed for user root
```

İlk satırda `admin` kullanıcısı için kimlik doğrulama amacıyla başarılı bir ortak anahtarın kullanıldığını görebiliriz. Kullanıcı `sudo` yardımıyla komut çalıştırmıştır. Bu yüzden kullanıcının `sudoers` grubunda olduğunu söyleyebiliriz. Kernel mesajı 22 numaralı port üzerinde beklenmeyen bir trafiğe izin verildiğini belirtiyor. Bu, olası bir güvenlik ihlaline işaret edebilir. Daha sonrasında `systemd-logind` ile `admin` kullanıcısı için yeni bir oturum oluşturulduğunu ve `root` kullanıcısı için bir `cron` oturumunun açılıp kapatıldığını görüyoruz.

## Application logs

Bu günlükler, sistemde çalışan belirli uygulamaların etkinlikleri hakkında bilgiler içerir. Bu günlükleri inceleyerek olası güvenlik açıklarını veya yanlış yapılandırmaları tespit edebiliriz. Örneğin erişim günlükleri, bir web sunucusuna yapılan istekleri izlemek için kullanılabilir ve denetim günlükleri, sistemde veya belirli dosyalarda yapılan değişiklikleri izlemek için kullanılabilir. Bu günlükler yetkisiz erişim girişimlerini, veri sızıntılarını veya diğer şüpheli etkinlikleri tanımlamak için kullanılabilir.

## Security logs

Bu günlükler, kullanılan güvenlik aracına bağlı olarak çeşitli günlük dosyalarına kaydedilir. Sızma testi uzmanları olarak, bir güvenlik sorununa işaret edebilecek belirli olayları veya faaliyet modellerini aramak için günlük analiz araçlarını ve tekniklerini kullanabiliriz ve bu bilgileri güvenlik açıkları veya potansiyel saldırı vektörleri açısından daha fazla test etmek için kullanabiliriz.
