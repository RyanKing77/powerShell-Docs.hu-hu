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
ms.openlocfilehash: bdf88de0258af75c01739f30a71fb4914cac3a9a
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56849027"
---
# <a name="security-parameters"></a>Biztonsági paraméterek

Az alábbi táblázat a javasolt nevek és a egy művelet, például a tanúsítvány kulcs és a jogosultsági információk megadásához használható paraméterek, a biztonsági információk nyújtásához paraméterek funkciók.

ACL-adattípus: Sztring

Ezzel a paraméterrel adja meg a hozzáférést vezérlő szintjét védelmének a katalógus és a egy egységes erőforrás-azonosító (URI) megvalósítása.

Tanúsítványfájl adattípus: Sztring

Végrehajtja ezt a paramétert, úgy, hogy a felhasználó megadhatja a következők egyikét tartalmazó fájl neve:

- A Base64 vagy használjon Distinguished Encoding Rules (DER) kódolású x.509-tanúsítvány

- Legalább egy tanúsítványt és kulcsot tartalmazó nyilvános kulcs titkosítási szabványok (PKCS) #12-fájl

CertIssuerName adattípus: Sztring

Ez a paraméter valósítja meg, hogy a felhasználó megadhatja a tanúsítvány kibocsátójának nevét, vagy úgy, hogy a felhasználó megadhatja a karakterláncrészletet.

CertRequestFile adattípus: Sztring

Ez a paraméter egy Base64 vagy DER kódolású PKCS #10 tanúsítványkérelmet tartalmazó fájl nevének megadására megvalósításához.

CertSerialNumber adattípus: Sztring

Ezzel a paraméterrel adja meg a hitelesítésszolgáltató által kiállított sorozatszám megvalósításához.

CertStoreLocation Data type: Sztring

Ez a paraméter valósítja meg, hogy a felhasználó megadhatja a helyét, a tanúsítványtárolóban. A hely az általában egy fájl elérési útját.

CertSubjectName adattípus: Sztring

Ez a paraméter valósítja meg, hogy a felhasználó megadhatja a tanúsítvány kiállítója, vagy úgy, hogy a felhasználó megadhatja a karakterláncrészletet.

CertUsage adattípus: Sztring

Ez a paraméter adja meg a kulcs használata vagy a kibővített kulcshasználat megvalósításához. A kulcs által megjeleníthető egy kicsit maszkolja, egy kicsit objektumazonosító (OID), vagy egy karakterláncot.

Írja be a hitelesítő adatok: [System.Management.Automation.Pscredential](/dotnet/api/System.Management.Automation.PSCredential)

Ez a paraméter valósítja meg, hogy a parancsmag automatikusan kérni fogja a felhasználótól a felhasználónevet vagy jelszót. Mindkettő egy kérés jelenik meg, ha egy teljes hitelesítő adat nem közvetlenül tartalmazza.

Csp_név adattípus: Sztring

Ez a paraméter valósítja meg, hogy a felhasználó megadhatja a tanúsítvány-szolgáltató (CSP) nevét.

CSPType adattípus: Integer

Ez a paraméter valósítja meg, hogy a felhasználó megadhatja a kriptográfiai Szolgáltató típusát.

Írja be a csoport adatai: Sztring

Ez a paraméter valósítja meg, hogy a felhasználó megadhatja a hozzáféréshez egyszerű gyűjteménye. További információkért tekintse meg a leírását az `Principal` paraméter.

KeyAlgorithm adattípus: Sztring

Ez a paraméter valósítja meg, hogy a felhasználó megadhatja a kulcs létrehozásának algoritmus használandó. a biztonság.

Kulcstárolónév adattípus: Sztring

Ez a paraméter valósítja meg, hogy a felhasználó megadhatja a kulcstároló nevével.

Kulcshossz adattípus: Integer

Ez a paraméter valósítja meg, hogy a felhasználó úgy adhat meg a kulcs hosszát bitekben.

A művelet adattípus: Sztring

Ez a paraméter valósítja meg, hogy a felhasználó megadhatja a védett objektumon végrehajtott műveletet.

Egyszerű adattípus: Sztring

Ez a paraméter valósítja meg, hogy a felhasználó megadhatja a hozzáféréshez egy egyedi azonosítható entitást.

Írja be a jogosultsági adatokat: Sztring

Ez a paraméter valósítja meg, hogy a felhasználó megadhatja a jobb oldalon, a parancsmag egy művelettel egy adott entitás van szüksége.

Jogosultságok adattípus: Jogosultságok tömbje

Ez a paraméter valósítja meg, hogy a felhasználó megadhatja, hogy a parancsmag kell végrehajtani a műveletet egy adott tétel.

Szerepkör-adattípus: Sztring

Ez a paraméter valósítja meg, hogy a felhasználó úgy adhat meg az entitás által végrehajtott műveletek készletét.

SaveCred adattípus: SwitchParameter

Ez a paraméter valósítja meg, hogy a felhasználó által korábban mentett hitelesítő adatok használandó, ha a paraméter meg van adva.

Hatókör-adattípus: Sztring

Ez a paraméter valósítja meg, hogy a felhasználó megadhatja a parancsmag védett objektumok csoportja.

SID-adattípus: Sztring

Ez a paraméter valósítja meg, hogy a felhasználó úgy adhat meg a rendszerbiztonsági tag képviselő egyedi azonosítója.

A megbízható adattípus: SwitchParameter

Ez a paraméter valósítja meg, hogy a megbízhatósági szintek támogatottak, ha a paraméter meg van adva.

TrustLevel adattípus: Kulcsszó

Ez a paraméter valósítja meg, hogy a felhasználó megadhatja a megbízhatósági szint támogatott. Például lehetséges értékek a következők fulltrust, internetes és intranetes.

## <a name="see-also"></a>Lásd még:

[Parancsmag-paraméterek](./cmdlet-parameters.md)

[Egy Windows PowerShell-parancsmag írása](./writing-a-windows-powershell-cmdlet.md)

[Windows PowerShell SDK](../windows-powershell-reference.md)
