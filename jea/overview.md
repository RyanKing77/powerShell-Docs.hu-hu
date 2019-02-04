---
ms.date: 06/12/2017
keywords: a jea, powershell, biztonsági
title: Éppen elég felügyelettel áttekintése
ms.openlocfilehash: c097838fb25a63d42502eebf751c64c537bdd077
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55686081"
---
# <a name="just-enough-administration"></a>Just Enough Administration

Csak Enough Administration (JEA) egy biztonsági technológia lehetővé teszi összes adat delegált felügyeletét, amelyek kezelhetők a PowerShell használatával.
A JEA-segítségével:

- **A rendszergazdák a gépeken számának csökkentése** kibővítéséhez virtuális fiókok és csoportok felügyelt szolgáltatásfiókokat, amelyek a normál felhasználók nevében privilegizált műveletek elvégzéséhez.
- **Korlátozza a felhasználók mit tehetnek** megadásával, mely parancsmagok, a functions és a külső parancsokat futtathatnak.
- **Jobb megértése érdekében a felhasználók mire** az átiratok és a naplókat, amelyek bemutatják, pontosan parancsok, amelyek a felhasználó a munkamenet során végrehajtott.

**Miért fontos ez?**

A kiszolgálók felügyeletéhez használt magas jogosultsági szintű fiókok súlyos biztonsági kockázatot jelenthet.
Kell egy támadó veszélyeztetheti e fiókok, akkor el tudják indítani az [oldalirányú támadások](http://aka.ms/pth) a szervezetben.
Minden fiók, veszélyeztetheti is biztosíthat számukra hozzáférést még további fiókokat és erőforrásokat, őket egy lépéssel közelebb kerülnek lopásának megjelölése vállalati titkos kulcsokat, egy-szolgáltatásmegtagadási támadást, és további indítása.

Akkor sem mindig egyszerű, rendszergazdai jogosultságokkal, vagy eltávolítani.
Fontolja meg a gyakori forgatókönyv, ahol telepítve van a DNS-szerepkört az Active Directory-tartományvezérlő ugyanazon a gépen.
A DNS-rendszergazdák számára szükséges DNS-kiszolgálóval kapcsolatos problémák kijavításához, de annak érdekében, hogy ehhez módosítania kell azokat a magas jogosultsági szintű "Tartományi rendszergazdák" biztonsági csoport tagjai a helyi rendszergazdai jogosultságokkal.
Ezt a módszert hatékonyan DNS-rendszergazdák szabályozni a teljes tartomány- és hozzáférés biztosít ezen a gépen futó összes erőforrást.

JEA segít a probléma megoldása segít elfogadják a elvét *legalacsonyabb jogosultsági*.
A JEA konfigurálhat egy felügyeleti végpont a DNS-rendszergazdák számára, amely hozzáférést biztosít a munkájához szükséges összes PowerShell-parancsokat, de semmi nem további.
Ez azt jelenti, hogy a megfelelő hozzáférés szennyezett DNS-gyorsítótár javítása, vagy indítsa újra a DNS-kiszolgáló nélkül véletlenül is ad nekik az Active Directory rights, vagy tallózással keresse meg a fájlrendszerben, vagy potenciálisan veszélyes szkriptek futtatása.
Még jobb, ha a JEA-munkamenet emelt szintű virtuális ideiglenes fiókok használatára van konfigurálva, a DNS-rendszergazdák kapcsolódhatnak a kiszolgálóra történő *nem rendszergazdai* hitelesítő adatait, és továbbra is képesek általában igénylő parancsok futtatásához rendszergazdai jogosultságokat.
Ez a funkció lehetővé teszi, hogy távolítsa el a felhasználókat széles körben jogosultságú helyi és tartományi rendszergazdai szerepköröket, és ehelyett alaposan ellenőrzését Mik ezek szeretnék megtenni az összes olyan számítógépen.

## <a name="get-started-with-jea"></a>A JEA használatának első lépései

Megkezdheti a használatát még ma a jea-t bármely gépen futó Windows Server 2016 vagy Windows 10-es.
A JEA egy Windows Management Framework frissítéssel régebbi operációs rendszereken is futtathatja.
A jea-t használja, és megtudhatja, hogyan hozhat létre követelményeivel kapcsolatos további használja, és naplózása a JEA-végpont, tekintse meg a következő témaköröket:

- [Előfeltételek](prerequisites.md) -azt ismerteti, hogyan állítsa be a környezetet a JEA használata.
- [Szerepköri funkciók](role-capabilities.md) -ismerteti, hogyan hozhat létre szerepköröket, amelyek meghatározzák, hogy mi a felhasználó számára engedélyezett a JEA-munkamenetben.
- [A munkamenet-konfigurációk](session-configurations.md) -ismerteti, hogy a felhasználók leképezése a szerepkörök és a JEA identitás beállításához a JEA-végpontok konfigurálása
- [A JEA regisztrálása](register-jea.md) – a JEA-végpont létrehozása, és lehetővé teszi a felhasználók számára való csatlakozáshoz.
- [A JEA használata](using-jea.md) – ismerje meg a különböző módszereket használhat a jea-t.
- [Biztonsági szempontok](security-considerations.md) – tekintse át az ajánlott biztonsági eljárások és a JEA-konfigurációs beállítások következményeit.
- [Naplózása és jelentései JEA](audit-and-report.md) – ismerje meg, hogyan naplózása és jelentései a JEA-végpont.

## <a name="samples-and-dsc-resource"></a>Minták és a DSC-erőforrás

Minta JEA konfigurációkat és a JEA DSC-erőforrás megtalálható a [JEA GitHub-adattár](https://github.com/PowerShell/JEA).