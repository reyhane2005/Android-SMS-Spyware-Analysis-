# Elgfus – Comprehensive Android SMS Spyware Analysis

**Malware Family:** Provisional IRATA-style / Realrat cluster (MEDIUM confidence)  
**Package Name:** `com.elgfus.app`  
**SHA-256:** `dba10d0b3d89f977a84fa21033d65a3a989c89dc30da5be197b47e4f8f7cbbb6`  
**Lure:** AI Gallery (گالری هوش مصنوعی)  
**Author:** reyhane2005  
**Analysis Date:** October 2026

---

## 1. Executive Summary

Elgfus is a malicious Android application that functions as an **SMS / Contacts / Photo spyware** with remote operator control and strong financial reconnaissance capabilities targeting Iranian users.

It was developed using **B4A (Basic4Android)** and uses **Firebase Cloud Messaging (FCM)** for command delivery combined with HTTPS exfiltration.

**Confirmed capabilities include:**
- Live and historical SMS interception (including OTPs)
- Contact theft and insertion
- DCIM photo harvesting (resized + ZIP compressed)
- Iranian bank balance, account number and card number extraction
- USSD call forwarding (`*21*`)
- Launcher icon disguise as Google or Chrome
- Offline SMS forwarding to attacker-controlled numbers
- Remote command execution via FCM

No Accessibility Service, banking overlays, root exploit, ransomware, live camera/microphone recording, or full-device screen control was identified.

---

## 2. Sample Information

| Field                    | Value |
|--------------------------|-------|
| **SHA-256**              | `dba10d0b3d89f977a84fa21033d65a3a989c89dc30da5be197b47e4f8f7cbbb6` |
| **MD5**                  | `c45d843f107394fb943285c4c7c6b323` |
| **SHA-1**                | `e6bfc489b8a34c346e6a73b0ee4b0fea1f23ed14` |
| **Package Name**         | `com.elgfus.app` |
| **App Label**            | AI Gallery (گالری هوش مصنوعی) |
| **Version**              | 1.3.0 (versionCode 240) |
| **Size**                 | 5,202,920 bytes (≈ 4.96 MiB) |
| **Min / Target SDK**     | 21 / 35 |
| **Signing Certificate**  | Android Debug (`CN=Android Debug, O=Android, C=US`) |
| **Certificate SHA-256**  | `1e08a903aef9c3a721510b64ec764d01d3d094eb954161b62544ea8f187b5953` |
| **Native Libraries**     | None |

---

## 3. Complete Permission List

### High-Risk / Dangerous Permissions
android.permission.READ_SMS
android.permission.RECEIVE_SMS
android.permission.SEND_SMS
android.permission.READ_CONTACTS
android.permission.WRITE_CONTACTS
android.permission.READ_PHONE_STATE
android.permission.CALL_PHONE
android.permission.READ_EXTERNAL_STORAGE
android.permission.WRITE_EXTERNAL_STORAGE
android.permission.READ_MEDIA_IMAGES
android.permission.QUERY_ALL_PACKAGES
android.permission.FOREGROUND_SERVICE
android.permission.FOREGROUND_SERVICE_SPECIAL_USE
android.permission.WAKE_LOCK
android.permission.RECEIVE_BOOT_COMPLETED
android.permission.INTERNET
android.permission.ACCESS_NETWORK_STATE
android.permission.POST_NOTIFICATIONS
android.permission.VIBRATE
android.permission.USE_BIOMETRIC
android.permission.USE_FINGERPRINT

---

## 4. C2 Infrastructure

| Type              | Value                                              | Purpose                          |
|-------------------|----------------------------------------------------|----------------------------------|
| Domain            | `arvvvanepoohhh.site`                              | Primary C2                       |
| Registration/SMS  | `https://arvvvanepoohhh.site/FPkXgpj6pA/Received.php` | Device registration + SMS exfil |
| File Upload       | `https://arvvvanepoohhh.site/FPkXgpj6pA/file.php`   | Contacts, SMS, screenshots       |
| Gallery Upload    | `https://arvvvanepoohhh.site/upload_gallery.php`    | Chunked photo ZIP                |
| Firebase Project  | `fir-f9c5f`                                        | Command delivery                 |
| Firebase Topic    | `FPkXgpj6pA`                                       | Operator commands                |

Operator can override the C2 host at runtime via Base64-encoded `domain.txt`.

---

## 5. Targeted Iranian Banks (Hardcoded)
com.bki.mobilebanking.android
com.isc.bminew
ir.bmi.bam.nativeweb
com.refahbank.dpi.android
com.isc.bsinew
ir.tejaratbank.tata.mobile.android.tejarat
com.pmb.mobile
com.dotin.wepod
---

## 6. Targeted Cryptocurrency Exchanges & Wallets
market.nobitex
co.okex.app
com.iranicard.app
io.bitpin.app
land.tether.tetherland
com.arzypto.my
com.arzinja.app
com.exnovin
com.bitex.pooleno
com.tabdeal
co.app.xpay
ir.wallex.app
com.ompfinex.app
ir.myter.bit24
com.bitbarg.app
com.excoino.excoino
com.exir.mobile
ir.bitmax.twa
com.tickpaymobileapp.user
com.coininno.android
kifpool.me.v2
com.nipoto.app
com.kcex
com.planet.toobit
com.coinex.trade.play
net.arzplus.twa
com.ramzinex.ramzinex
com.arzjoo
com.hamtapay.exchange
com.raastin.light
com.arzpaya.arzpaya
com.wallet.crypto.trustapp
org.toshi
app.phantom
exodusmovement.exodus
com.debank.rabbymobile
io.safepal.wallet
com.ton_keeper

---

## 7. Remote Commands (Complete List)

### Financial Commands
- `balance` / `getallbalance` / `getallbalanc_two`
- `searchCard`
- `all_bank_sms`
- `hamrahbank` / `hamrahbankall`
- `exchange` / `exchangeall`

### Data Collection
- `all_contacts`
- `all_sms` / `all_sms_recived` / `all_sms_sent` / `last_sms`
- `get_gallery` / `get_gallery_v2`
- `get_screenshot`
- `applist`
- `userphone` / `userphoneall`
- `searchSMS` / `lastsearchSMS` / `allSearch`

### Remote Control & Evasion
- `divert` → USSD `*21*number#`
- `ussdreq`
- `hidden` / `visible` / `hide_all` / `hidden_delayed`
- `changetogoogle` / `changetogoogleall`
- `TEL_HIDE_SUM` / `CHEROME_HIDE_SUM` / `VISIBLE_HIDE_SUM`
- `silent` / `silent_all` / `Vibrate` / `Normal`
- `offline_mode_on` / `offline_mode_off`
- `ratdomain`
- `updateofflinekey` / `updateofflinekeyforuser`
- `send_sms` / `send_sms_all` / `smcontact` / `smcontactall`
- `add_contact`
- `online_device` / `status` / `checker` / `refresh_token`

---

## 8. Persistence Mechanisms

- Foreground service `sysc` with `FOREGROUND_SERVICE_SPECIAL_USE`
- Partial WakeLock + KeepAlive
- Dynamic registration of `BOOT_COMPLETED` and package-replaced receivers
- Task removal recovery
- Launcher component disabling / aliasing as Google or Chrome

---

## 9. Anti-Analysis / Evasion

- Strong anti-emulator checks (exits on goldfish/ranchu/qemu, specific carriers, x86 ABI)
- Manipulated ZIP compression metadata
- Malformed manifest attributes
- Base64 encoding of C2 host
- Icon hiding and disguise

---
---

## 10. YARA Rule

```yara
rule Android_Elgfus_SMS_Spyware {
    meta:
        description = "Elgfus / IRATA-style Android SMS Spyware"
        author = "reyhane2005"
        date = "2026-10"
        hash = "dba10d0b3d89f977a84fa21033d65a3a989c89dc30da5be197b47e4f8f7cbbb6"
    strings:
        $pkg = "Lcom/elgfus/app/" ascii
        $s1 = "TEL_HIDE_SUM" ascii
        $s2 = "get_gallery_v2" ascii
        $s3 = "updateofflinekeyforuser" ascii
        $s4 = "offline_key.txt" ascii
        $s5 = "arvvvanepoohhh" ascii
        $s6 = "hamrahbank" ascii
    condition:
        uint32(0) == 0x0A786564 and $pkg and 4 of ($s*)
}

11. MITRE ATT&CK Mobile Mapping
Technique ID
Name
Confidence
T1636.004
SMS Messages
Confirmed
T1636.003
Contact List
Confirmed
T1582
SMS Control
Confirmed
T1418
Software Discovery
High
T1426
System Information Discovery
Confirmed
T1541
Foreground Persistence
Confirmed
T1628.001
Hide Artifacts
Confirmed
T1437.001
Web Protocols
Confirmed
T1646
Exfiltration Over C2 Channel
Confirmed
T1616
Call Control
Confirmed
T1533
Data from Local System
High
12. Indicators of Compromise (IOCs)
Hashes
SHA-256: dba10d0b3d89f977a84fa21033d65a3a989c89dc30da5be197b47e4f8f7cbbb6
MD5: c45d843f107394fb943285c4c7c6b323
SHA-1: e6bfc489b8a34c346e6a73b0ee4b0fea1f23ed14
Network
Domain: arvvvanepoohhh.site
Paths:
/FPkXgpj6pA/Received.php
/FPkXgpj6pA/file.php
/upload_gallery.php
Package
com.elgfus.app
13. Conclusion
Elgfus is a practical and effective Iranian-focused SMS spyware. While it lacks advanced Accessibility overlays, its combination of OTP theft, bank balance extraction, photo collection, call forwarding, and remote control makes it a significant threat to mobile banking users.
The primary infection vector appears to be social-engineering sideloading under the “AI Gallery” lure.
Disclaimer: This analysis is for educational and defensive research purposes only.
