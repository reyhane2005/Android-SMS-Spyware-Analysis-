 

```markdown
# Elgfus – Android SMS Spyware Analysis

**Malware Family:** Provisional IRATA-style / Realrat  
**Package:** `com.elgfus.app`  
**SHA-256:** `dba10d0b3d89f977a84fa21033d65a3a989c89dc30da5be197b47e4f8f7cbbb6`  
**Lure:** AI Gallery (گالری هوش مصنوعی)

## Overview

Elgfus is a malicious Android application that functions as an SMS, contacts, and photo stealer with remote operator control and financial reconnaissance capabilities targeting Iranian users.

It was developed using **B4A (Basic4Android)** and leverages Firebase Cloud Messaging (FCM) for command delivery.

## Sample Information

| Field                    | Value |
|--------------------------|-------|
| SHA-256                  | `dba10d0b3d89f977a84fa21033d65a3a989c89dc30da5be197b47e4f8f7cbbb6` |
| MD5                      | `c45d843f107394fb943285c4c7c6b323` |
| SHA-1                    | `e6bfc489b8a34c346e6a73b0ee4b0fea1f23ed14` |
| Package Name             | `com.elgfus.app` |
| Version                  | 1.3.0 (versionCode 240) |
| Size                     | 5,202,920 bytes |
| Min / Target SDK         | 21 / 35 |
| Certificate              | Android Debug |

## Permissions

```
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
```

## C2 Infrastructure

- **Domain:** `arvvvanepoohhh.site`
- **Registration / SMS:** `https://arvvvanepoohhh.site/FPkXgpj6pA/Received.php`
- **File Upload:** `https://arvvvanepoohhh.site/FPkXgpj6pA/file.php`
- **Gallery Upload:** `https://arvvvanepoohhh.site/upload_gallery.php`
- **Firebase Topic:** `FPkXgpj6pA`

## Key Capabilities

- Live & historical SMS interception
- Contact collection and insertion
- DCIM photo theft (resized + ZIP)
- Iranian bank balance and card extraction
- USSD call forwarding (`*21*`)
- Launcher icon disguise (Google / Chrome)
- Offline SMS forwarding
- Remote command execution via FCM

## Targeted Banks

```
com.bki.mobilebanking.android
com.isc.bminew
ir.bmi.bam.nativeweb
com.refahbank.dpi.android
ir.tejaratbank.tata.mobile.android.tejarat
...
```

## Targeted Crypto Exchanges & Wallets

```
market.nobitex
co.okex.app
io.bitpin.app
ir.wallex.app
com.wallet.crypto.trustapp
app.phantom
exodusmovement.exodus
com.ton_keeper
...
```

## Notable Commands

| Command              | Description                        |
|----------------------|------------------------------------|
| `balance`            | Extract bank balances              |
| `get_gallery_v2`     | Steal and upload photos            |
| `divert`             | Activate call forwarding           |
| `all_contacts`       | Steal contact list                 |
| `TEL_HIDE_SUM`       | Disguise as Google                 |
| `offline_mode_on`    | Enable SMS forwarding              |

## YARA Rule

```yara
rule Android_Elgfus_SMS_Spyware {
    meta:
        description = "Elgfus Android SMS Spyware"
        author = "Your Name"
        hash = "dba10d0b3d89f977a84fa21033d65a3a989c89dc30da5be197b47e4f8f7cbbb6"
    strings:
        $pkg = "Lcom/elgfus/app/" ascii
        $s1 = "TEL_HIDE_SUM" ascii
        $s2 = "get_gallery_v2" ascii
        $s3 = "offline_key.txt" ascii
        $s4 = "arvvvanepoohhh" ascii
    condition:
        uint32(0) == 0x0A786564 and $pkg and 3 of them
}
```

## MITRE ATT&CK

- T1636.004 – SMS Messages
- T1636.003 – Contact List
- T1582 – SMS Control
- T1541 – Foreground Persistence
- T1628.001 – Hide Artifacts
- T1616 – Call Control

## IOCs

**Hashes**
- SHA-256: `dba10d0b3d89f977a84fa21033d65a3a989c89dc30da5be197b47e4f8f7cbbb6`

**Network**
- `arvvvanepoohhh.site`

---

**Full technical details, dynamic analysis notes, and additional detection content are available in this repository.**
```

---
