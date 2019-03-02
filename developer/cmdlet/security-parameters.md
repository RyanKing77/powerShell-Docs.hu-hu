---
title: Biztonsági paramétereket |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: e199bba3-90d3-41ca-9d78-cb502e58508d
caps.latest.revision: 6
ms.openlocfilehash: c8b3f907a80d1f6125a5ac04236245503db76ed0
ms.sourcegitcommit: ce46e5098786e19d521b4bf948ff62d2b90bc53e
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/02/2019
ms.locfileid: "57251302"
---
# <a name="security-parameters"></a>Biztonsági paraméterek

Az alábbi táblázat a javasolt nevek és a egy művelet, például a tanúsítvány kulcs és a jogosultsági információk megadásához használható paraméterek, a biztonsági információk nyújtásához paraméterek funkciók.

|Paraméter|Funkció|
|---|---|
|**ACL**<br>Adattípus: Sztring|Ezzel a paraméterrel adja meg a hozzáférést vezérlő szintjét védelmének a katalógus és a egy egységes erőforrás-azonosító (URI) megvalósítása.|
|**Tanúsítványfájl**<br>Adattípus: Sztring|Végrehajtja ezt a paramétert, úgy, hogy a felhasználó megadhatja a következők egyikét tartalmazó fájl neve:<br>-A Base64 vagy használjon Distinguished Encoding Rules (DER) kódolású x.509-tanúsítvány<br>-Legalább egy tanúsítvány és kulcs tartalmazó nyilvános kulcs titkosítási szabványok (PKCS) #12-fájl|
|**CertIssuerName**<br>Adattípus: Sztring|Ez a paraméter valósítja meg, hogy a felhasználó megadhatja a tanúsítvány kibocsátójának nevét, vagy úgy, hogy a felhasználó megadhatja a karakterláncrészletet.|
|**CertRequestFile**<br>Adattípus: Sztring|Ez a paraméter egy Base64 vagy DER kódolású PKCS #10 tanúsítványkérelmet tartalmazó fájl nevének megadására megvalósításához.|
|**CertSerialNumber**<br>Adattípus: Sztring|Ezzel a paraméterrel adja meg a hitelesítésszolgáltató által kiállított sorozatszám megvalósításához.|
|**CertStoreLocation**<br>Adattípus: Sztring|Ez a paraméter valósítja meg, hogy a felhasználó megadhatja a helyét, a tanúsítványtárolóban. A hely az általában egy fájl elérési útját.|
|**CertSubjectName**<br>Adattípus: Sztring|Ez a paraméter valósítja meg, hogy a felhasználó megadhatja a tanúsítvány kiállítója, vagy úgy, hogy a felhasználó megadhatja a karakterláncrészletet.|
|**CertUsage**<br>Adattípus: Sztring|Ez a paraméter adja meg a kulcs használata vagy a kibővített kulcshasználat megvalósításához. A kulcs által megjeleníthető egy kicsit maszkolja, egy kicsit objektumazonosító (OID), vagy egy karakterláncot.|
|**Hitelesítő adatok**<br>Adattípus: [System.Management.Automation.Pscredential](/dotnet/api/System.Management.Automation.PSCredential)|Ez a paraméter valósítja meg, hogy a parancsmag automatikusan kérni fogja a felhasználótól a felhasználónevet vagy jelszót. Mindkettő egy kérés jelenik meg, ha egy teljes hitelesítő adat nem közvetlenül tartalmazza.|
|**CSPName**<br>Adattípus: Sztring|Ez a paraméter valósítja meg, hogy a felhasználó megadhatja a tanúsítvány-szolgáltató (CSP) nevét.|
|**CSPType**<br>Adattípus: Integer|Ez a paraméter valósítja meg, hogy a felhasználó megadhatja a kriptográfiai Szolgáltató típusát.|
|**Csoport**<br>Adattípus: Sztring|Ez a paraméter valósítja meg, hogy a felhasználó megadhatja a hozzáféréshez egyszerű gyűjteménye. További információkért tekintse meg a leírását az **egyszerű** paraméter.|
|**KeyAlgorithm**<br>Adattípus: Sztring|Ez a paraméter valósítja meg, hogy a felhasználó megadhatja a kulcs létrehozásának algoritmus használandó. a biztonság.|
|**KeyContainerName**<br>Adattípus: Sztring|Ez a paraméter valósítja meg, hogy a felhasználó megadhatja a kulcstároló nevével.|
|**KeyLength**<br>Adattípus: Integer|Ez a paraméter valósítja meg, hogy a felhasználó úgy adhat meg a kulcs hosszát bitekben.|
|**Művelet**<br>Adattípus: Sztring|Ez a paraméter valósítja meg, hogy a felhasználó megadhatja a védett objektumon végrehajtott műveletet.|
|**Egyszerű szolgáltatásnév**<br>Adattípus: Sztring|Ez a paraméter valósítja meg, hogy a felhasználó megadhatja a hozzáféréshez egy egyedi azonosítható entitást.|
|**Jogosultság**<br>Adattípus: Sztring|Ez a paraméter valósítja meg, hogy a felhasználó megadhatja a jobb oldalon, a parancsmag egy művelettel egy adott entitás van szüksége.|
|**Jogosultságok**<br>Adattípus: Jogosultságok tömbje|Ez a paraméter valósítja meg, hogy a felhasználó megadhatja, hogy a parancsmag kell végrehajtani a műveletet egy adott tétel.|
|**Szerepkör**<br>Adattípus: Sztring|Ez a paraméter valósítja meg, hogy a felhasználó úgy adhat meg az entitás által végrehajtott műveletek készletét.|
|**SaveCred**<br>Adattípus: SwitchParameter|Ez a paraméter valósítja meg, hogy a felhasználó által korábban mentett hitelesítő adatok használandó, ha a paraméter meg van adva.|
|**Hatókör**<br>Adattípus: Sztring|Ez a paraméter valósítja meg, hogy a felhasználó megadhatja a parancsmag védett objektumok csoportja.|
|**SID**<br>Adattípus: Sztring|Ez a paraméter valósítja meg, hogy a felhasználó úgy adhat meg a rendszerbiztonsági tag képviselő egyedi azonosítója.|
|**Megbízható**<br>Adattípus: SwitchParameter|Ez a paraméter valósítja meg, hogy a megbízhatósági szintek támogatottak, ha a paraméter meg van adva.|
|**TrustLevel**<br>Adattípus: Kulcsszó|Ez a paraméter valósítja meg, hogy a felhasználó megadhatja a megbízhatósági szint támogatott. Például lehetséges értékek a következők fulltrust, internetes és intranetes.|

## <a name="see-also"></a>Lásd még:

[Parancsmag-paraméterek](./cmdlet-parameters.md)

[Egy Windows PowerShell-parancsmag írása](./writing-a-windows-powershell-cmdlet.md)

[Windows PowerShell SDK](../windows-powershell-reference.md)
