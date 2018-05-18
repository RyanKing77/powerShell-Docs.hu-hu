---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 14208e3b5d5c2fef80fa42a87cc00aeee81bd042
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/16/2018
---
# <a name="cryptographic-message-syntax-cms-cmdlets"></a><span data-ttu-id="d6d45-102">Kriptográfiai szintaxisú (CMS) parancsmagok</span><span class="sxs-lookup"><span data-stu-id="d6d45-102">Cryptographic Message Syntax (CMS) cmdlets</span></span>

<span data-ttu-id="d6d45-103">A titkosított üzenetek szintaxisának parancsmagok támogatja a titkosítási és visszafejtési a IETF szabványos formátumot használja az üzenetek titkosítással védi a megfelelően tartalom [RFC5652](https://tools.ietf.org/html/rfc5652).</span><span class="sxs-lookup"><span data-stu-id="d6d45-103">The Cryptographic Message Syntax cmdlets support encryption and decryption of content using the IETF standard format for cryptographically protecting messages as documented by [RFC5652](https://tools.ietf.org/html/rfc5652).</span></span>

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

<span data-ttu-id="d6d45-104">A CMS titkosítási szabvány valósítja meg a nyilvános kulcsú titkosítás, ha a kulcsok tartalom titkosításához használt (a *nyilvános kulcs*) és a tartalom visszafejtésére szolgáló jelszó kulcsok (a *titkos kulcs*) külön.</span><span class="sxs-lookup"><span data-stu-id="d6d45-104">The CMS encryption standard implements public key cryptography, where the keys used to encrypt content (the *public key*) and the keys used to decrypt content (the *private key*) are separate.</span></span>

<span data-ttu-id="d6d45-105">A nyilvános kulcs akkor lehet megosztani, széles körben, és nincs bizalmas adatokat.</span><span class="sxs-lookup"><span data-stu-id="d6d45-105">Your public key can be shared widely, and is not sensitive data.</span></span> <span data-ttu-id="d6d45-106">Ha a tartalom a nyilvános kulcsával van titkosítva, csak a titkos kulcsot is visszafejteni.</span><span class="sxs-lookup"><span data-stu-id="d6d45-106">If any content is encrypted with this public key, only your private key can decrypt it.</span></span> <span data-ttu-id="d6d45-107">További információkért lásd: [nyilvános kulcsú](https://en.wikipedia.org/wiki/Public-key_cryptography).</span><span class="sxs-lookup"><span data-stu-id="d6d45-107">For more information, see [Public-key cryptography](https://en.wikipedia.org/wiki/Public-key_cryptography).</span></span>

<span data-ttu-id="d6d45-108">Titkosítási tanúsítványok a PowerShell ismeretlen, szükség egy egyedi kulcshasználat azonosítója (EKU) segítségével jelölje őket adatok titkosítási tanúsítványok (például az azonosítók "Kód aláírása", 'Titkosított Mail').</span><span class="sxs-lookup"><span data-stu-id="d6d45-108">To be recognized in PowerShell, encryption certificates require a unique key usage identifier (EKU) to identify them as data encryption certificates (like the identifiers for 'Code Signing', 'Encrypted Mail').</span></span>

<span data-ttu-id="d6d45-109">Íme egy példa a jó dokumentum titkosítási tanúsítvány létrehozása:</span><span class="sxs-lookup"><span data-stu-id="d6d45-109">Here is an example of creating a certificate that is good for Document Encryption:</span></span>

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

<span data-ttu-id="d6d45-110">Majd futtassa:</span><span class="sxs-lookup"><span data-stu-id="d6d45-110">Then run:</span></span>
```powershell
certreq -new DocumentEncryption.inf DocumentEncryption.cer
```

<span data-ttu-id="d6d45-111">És mostantól titkosításához és visszafejtéséhez tartalom:</span><span class="sxs-lookup"><span data-stu-id="d6d45-111">And you can now encrypt and decrypt content:</span></span>

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

<span data-ttu-id="d6d45-112">Bármely típusú paramétert **CMSMessageRecipient** azonosítók a következő formátumokban támogatja:</span><span class="sxs-lookup"><span data-stu-id="d6d45-112">Any parameter of type **CMSMessageRecipient** supports identifiers in the following formats:</span></span>
- <span data-ttu-id="d6d45-113">Egy tényleges tanúsítványt (a letöltött tanúsítvány-szolgáltatójáról)</span><span class="sxs-lookup"><span data-stu-id="d6d45-113">An actual certificate (as retrieved from the certificate provider)</span></span>
- <span data-ttu-id="d6d45-114">Elérési útját a tanúsítványát tartalmazó fájl</span><span class="sxs-lookup"><span data-stu-id="d6d45-114">Path to the a file containing the certificate</span></span>
- <span data-ttu-id="d6d45-115">A tanúsítványt tartalmazó könyvtár elérési útja</span><span class="sxs-lookup"><span data-stu-id="d6d45-115">Path to a directory containing the certificate</span></span>
- <span data-ttu-id="d6d45-116">(A tanúsítványtárolóban kereséséhez használt) a tanúsítvány ujjlenyomata</span><span class="sxs-lookup"><span data-stu-id="d6d45-116">Thumbprint of the certificate (used to look in the certificate store)</span></span>
- <span data-ttu-id="d6d45-117">A tanúsítvány (a tanúsítványtárolóban kereséséhez használt)</span><span class="sxs-lookup"><span data-stu-id="d6d45-117">Subject name of the certificate (used to look in the certificate store)</span></span>

<span data-ttu-id="d6d45-118">A tanúsítványszolgáltató dokumentum titkosítási tanúsítványok megtekintéséhez használja a **- DocumentEncryptionCert** dinamikus paramétert:</span><span class="sxs-lookup"><span data-stu-id="d6d45-118">To view document encryption certificates in the certificate provider, you can use the **-DocumentEncryptionCert** dynamic parameter:</span></span>

```powershell
dir -DocumentEncryptionCert
```
