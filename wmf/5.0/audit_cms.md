---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 14208e3b5d5c2fef80fa42a87cc00aeee81bd042
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/16/2018
---
# <a name="cryptographic-message-syntax-cms-cmdlets"></a>Kriptográfiai szintaxisú (CMS) parancsmagok

A titkosított üzenetek szintaxisának parancsmagok támogatja a titkosítási és visszafejtési a IETF szabványos formátumot használja az üzenetek titkosítással védi a megfelelően tartalom [RFC5652](https://tools.ietf.org/html/rfc5652).

```powershell
Get-CmsMessage [-Content] <string>
Get-CmsMessage [-Path] <string>
Get-CmsMessage [-LiteralPath] <string>
Protect-CmsMessage [-To] <CmsMessageRecipient[]> [-Content] <string> [[-OutFile] <string>]
Protect-CmsMessage [-To] <CmsMessageRecipient[]> [-Path] <string> [[-OutFile] <string>]
Protect-CmsMessage [-To] <CmsMessageRecipient[]> [-LiteralPath] <string> [[-OutFile] <string>]
Unprotect-CmsMessage [-EventLogRecord] <EventLogRecord> [[-To] <CmsMessageRecipient[]>] [-IncludeContext]
Unprotect-CmsMessage [-Content] <string> [[-To] <CmsMessageRecipient[]>] [-IncludeContext]
Unprotect-CmsMessage [-Path] <string> [[-To] <CmsMessageRecipient[]>] [-IncludeContext]
Unprotect-CmsMessage [-LiteralPath] <string> [[-To] <CmsMessageRecipient[]>] [-IncludeContext]
```

A CMS titkosítási szabvány valósítja meg a nyilvános kulcsú titkosítás, ha a kulcsok tartalom titkosításához használt (a *nyilvános kulcs*) és a tartalom visszafejtésére szolgáló jelszó kulcsok (a *titkos kulcs*) külön.

A nyilvános kulcs akkor lehet megosztani, széles körben, és nincs bizalmas adatokat. Ha a tartalom a nyilvános kulcsával van titkosítva, csak a titkos kulcsot is visszafejteni. További információkért lásd: [nyilvános kulcsú](https://en.wikipedia.org/wiki/Public-key_cryptography).

Titkosítási tanúsítványok a PowerShell ismeretlen, szükség egy egyedi kulcshasználat azonosítója (EKU) segítségével jelölje őket adatok titkosítási tanúsítványok (például az azonosítók "Kód aláírása", 'Titkosított Mail').

Íme egy példa a jó dokumentum titkosítási tanúsítvány létrehozása:

```powershell
(Change the text in **Subject** to your name, email, or other identifier), and put in a file (i.e.: DocumentEncryption.inf):
[Version]
Signature = "$Windows NT$"
[Strings]
szOID\_ENHANCED\_KEY\_USAGE = "2.5.29.37"
szOID\_DOCUMENT\_ENCRYPTION = "1.3.6.1.4.1.311.80.1"
[NewRequest]
Subject = "<cn=me@somewhere.com>"
MachineKeySet = false
KeyLength = 2048
KeySpec = AT\_KEYEXCHANGE
HashAlgorithm = Sha1
Exportable = true
RequestType = Cert
KeyUsage = "CERT\_KEY\_ENCIPHERMENT\_KEY\_USAGE | CERT\_DATA\_ENCIPHERMENT\_KEY\_USAGE"
ValidityPeriod = "Years"
ValidityPeriodUnits = "1000"
[Extensions]
%szOID\_ENHANCED\_KEY\_USAGE% = "{text}%szOID\_DOCUMENT\_ENCRYPTION%"
```

Majd futtassa:
```powershell
certreq -new DocumentEncryption.inf DocumentEncryption.cer
```

És mostantól titkosításához és visszafejtéséhez tartalom:

```powershell
$protected = "Hello World" | Protect-CmsMessage -To "\*me@somewhere.com\*[](mailto:*leeholm@microsoft.com*)"
$protected
-----BEGIN CMS-----
MIIBqAYJKoZIhvcNAQcDoIIBmTCCAZUCAQAxggFQMIIBTAIBADA0MCAxHjAcBgNVBAMMFWxlZWhv
bG1AbWljcm9zb2Z0LmNvbQIQQYHsbcXnjIJCtH+OhGmc1DANBgkqhkiG9w0BAQcwAASCAQAnkFHM
proJnFy4geFGfyNmxH3yeoPvwEYzdnsoVqqDPAd8D3wao77z7OhJEXwz9GeFLnxD6djKV/tF4PxR
E27aduKSLbnxfpf/sepZ4fUkuGibnwWFrxGE3B1G26MCenHWjYQiqv+Nq32Gc97qEAERrhLv6S4R
G+2dJEnesW8A+z9QPo+DwYU5FzD0Td0ExrkswVckpLNR6j17Yaags3ltNVmbdEXekhi6Psf2MLMP
TSO79lv2L0KeXFGuPOrdzPAwCkV0vNEqTEBeDnZGrjv/5766bM3GW34FXApod9u+VSFpBnqVOCBA
DVDraA6k+xwBt66cV84OHLkh0kT02SIHMDwGCSqGSIb3DQEHATAdBglghkgBZQMEASoEEJbJaiRl
KMnBoD1dkb/FzSWAEBaL8xkFwCu0e1ZtDj7nSJc=
-----END CMS-----

$protected | Unprotect-CmsMessage
Hello World
```

Bármely típusú paramétert **CMSMessageRecipient** azonosítók a következő formátumokban támogatja:
- Egy tényleges tanúsítványt (a letöltött tanúsítvány-szolgáltatójáról)
- Elérési útját a tanúsítványát tartalmazó fájl
- A tanúsítványt tartalmazó könyvtár elérési útja
- (A tanúsítványtárolóban kereséséhez használt) a tanúsítvány ujjlenyomata
- A tanúsítvány (a tanúsítványtárolóban kereséséhez használt)

A tanúsítványszolgáltató dokumentum titkosítási tanúsítványok megtekintéséhez használja a **- DocumentEncryptionCert** dinamikus paramétert:

```powershell
dir -DocumentEncryptionCert
```
