---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: b8940ded189d822a5a2cd40773ef5146353611cc
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55686207"
---
# <a name="cryptographic-message-syntax-cms-cmdlets"></a>Titkosítási üzenet szintaxis-(CMS-) parancsmagok

A titkosítási üzenet szintaxis parancsmagok támogatják a titkosítási és visszafejtési a IETF szabvány formátum használatával titkosítási szempontból védelme érdekében üzenetet megfelelően tartalom [RFC5652](https://tools.ietf.org/html/rfc5652).

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

A standard szintű tartalomkezelő rendszer titkosítási valósítja meg a nyilvános kulcsú titkosítás, ahol a kulcsok tartalom titkosításához használt (a *nyilvános kulcs*) és a tartalom visszafejtésére szolgáló kulcsok (a *titkos kulcs*) jelennek meg.

A nyilvános kulcs széles körben történő megosztásának, és nem érzékeny adatokat. Ha bármilyen tartalmat a nyilvános kulccsal titkosított, csak a titkos kulcsot is a visszafejtésre. További információkért lásd: [nyilvános kulcsú titkosítással](https://en.wikipedia.org/wiki/Public-key_cryptography).

Titkosítási tanúsítványok ismerhetők meg a PowerShell, szükség van egy egyedi kulcshasználat azonosító (EKU) lenne azonosítani őket (például a "Kód aláírása", 'Titkosított Mail' azonosítók) adatok titkosítási tanúsítványok.

Íme egy példa, amely jó dokumentum titkosítási tanúsítvány létrehozása:

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

És most titkosítása és visszafejtése a tartalmat:

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

Bármilyen típusú paramétert **CMSMessageRecipient** azonosítók támogatja a következő formátumban:
- Egy tényleges tanúsítványt (a lekért tanúsítványt szolgáltatójáról)
- Elérési útját a tanúsítványt tartalmazó fájl
- Egy tanúsítványt tartalmazó könyvtár elérési útja
- (A tanúsítvány-áruházban keresse meg a használt) a tanúsítvány ujjlenyomata
- (A tanúsítvány-áruházban keresse meg a használt) a tanúsítvány tulajdonos neve

A tanúsítványszolgáltató dokumentum titkosítási tanúsítványok megtekintéséhez használja a **- DocumentEncryptionCert** dinamikus paraméterek:

```powershell
dir -DocumentEncryptionCert
```
