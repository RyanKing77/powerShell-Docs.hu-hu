---
ms.date: 07/10/2019
keywords: a jea, powershell, biztonsági
title: Éppen elég felügyelettel áttekintése
ms.openlocfilehash: 4b74e5be9558810748a8844a325c8213e1b3ebc9
ms.sourcegitcommit: 46bebe692689ebedfe65ff2c828fe666b443198d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/10/2019
ms.locfileid: "67726651"
---
# <a name="just-enough-administration"></a>Just Enough Administration

Csak Enough Administration (JEA) egy biztonsági technológia lehetővé teszi összes adat delegált felügyeletét PowerShell kezeli. A JEA-segítségével:

- **A rendszergazdák a gépeken számának csökkentése** virtuális fiók vagy csoportosan felügyelt szolgáltatásfiókok használatával rendszeres felhasználók nevében privilegizált műveletek elvégzéséhez.
- **Korlátozza a felhasználók mit tehetnek** megadásával, mely parancsmagok, a functions és a külső parancsokat futtathatnak.
- **Jobb megértése érdekében a felhasználók mire** az átiratok és a naplókat, amelyek bemutatják, pontosan parancsok, amelyek a felhasználó a munkamenet során végrehajtott.

**Miért fontos a jea-t?**

A kiszolgálók felügyeletéhez használt magas jogosultsági szintű fiókok súlyos biztonsági kockázatot jelenthet. Kell egy támadó veszélyeztetheti e fiókok, akkor el tudják indítani az [oldalirányú támadások](https://aka.ms/pth) a szervezetben. Minden egyes feltört fiók egy támadó hozzáférést még további fiókokat és erőforrásokat biztosít, és visszaállítja azokat a vállalati titkos kulcsokat, egy-szolgáltatásmegtagadási támadást, és további indítása ellophatják egy lépéssel közelebb kerülnek.

Akkor sem mindig egyszerű, rendszergazdai jogosultságokkal, vagy eltávolítani. Fontolja meg a gyakori forgatókönyv, ahol telepítve van a DNS-szerepkört az Active Directory-tartományvezérlő ugyanazon a gépen. A DNS-rendszergazdák számára helyi rendszergazdai jogosultsága a DNS-kiszolgálóval kapcsolatos problémák kijavításához szükséges. Ehhez meg kell győződnie, azokat a magas jogosultsági szintű tagjai, de **Tartománygazdák** biztonsági csoportot. Ezt a módszert hatékonyan DNS-rendszergazdák szabályozni a teljes tartomány- és hozzáférés biztosít ezen a gépen futó összes erőforrást.

JEA-címek a probléma elve **legalacsonyabb jogosultsági**. A JEA-konfigurálhat felügyeleti végpontot, amely hozzáférést biztosít csak a PowerShell-parancsokat a munkájához szükséges DNS-rendszergazdák számára. Ez azt jelenti, hogy a megfelelő hozzáférés szennyezett DNS-gyorsítótár javítása, vagy indítsa újra a DNS-kiszolgáló nélkül véletlenül is ad nekik az Active Directory rights, vagy tallózással keresse meg a fájlrendszerben, vagy potenciálisan veszélyes szkriptek futtatása. Még jobb, ha a JEA-munkamenet emelt szintű virtuális ideiglenes fiókok használatára van konfigurálva, a DNS-rendszergazdák kapcsolódhatnak a kiszolgálóra történő **nem rendszergazdai** hitelesítő adatokat, és továbbra is futtassa rendszergazdai általában igénylő parancsok jogosultságok. A JEA széles körben emelt szintű helyi és tartományi rendszergazdai szerepkörök távolítsa el a felhasználókat és a gondosan a műveleteket az egyes gépekre irányítását teszi lehetővé.

## <a name="next-steps"></a>További lépések

A JEA használata követelményeivel kapcsolatos további tudnivalókért tekintse meg a [Előfeltételek](prerequisites.md) cikk.

## <a name="samples-and-dsc-resource"></a>Minták és a DSC-erőforrás

Minta JEA konfigurációkat és a JEA DSC-erőforrás megtalálható a [JEA GitHub-adattár](https://github.com/PowerShell/JEA).
