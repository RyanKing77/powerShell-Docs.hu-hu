---
ms.date: 06/12/2017
keywords: jea, a powershell, a biztonsági
title: Éppen elég felügyelettel áttekintése
ms.openlocfilehash: 3dae8b31d4d13ff9033803035c870c02fc7c38ca
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2018
---
# <a name="just-enough-administration"></a>Just Enough Administration

Csak elég adminisztrációs (JEA) olyan biztonsági technológia, amely lehetővé teszi a számára a delegált felügyelet semmit, amelyek a PowerShell használatával kezelhetők.
A jea-ban a következőket teheti:

- **Adjon meg kevesebb a gépeken rendszergazdák** emelés virtuális fiók vagy csoport által felügyelt szolgáltatásfiókok, amelyek rendszeres felhasználók nevében privilegizált műveleteket.
- **Korlátozza a felhasználók mit tehetnek** megadásával, mely parancsmagok, függvények és külső parancsokat futtathatnak.
- **Jobb megértése érdekében a felhasználók tevékenységeit** ki és a naplókat, amelyek bemutatják, pontosan parancsok, amelyek a felhasználó a munkamenet során végrehajtott.

**Miért fontos ez?**

A kiszolgálók felügyeletére használt kiemelt jogosultságokkal rendelkező fiókok súlyos biztonsági kockázatot jelenthet.
Kell egy támadó kedvezőtlenül egyik ezeket a fiókokat, akkor el tudják indítani [támadások oldalirányú](http://aka.ms/pth) a szervezetben.
Minden felhasználói fiókhoz, azok kedvezőtlenül is betekintést biztosít további fiókokat és erőforrásokat, őket még egy lépéssel közelebb kerülnek ellophassák vállalati titkos adatait, a-szolgáltatásmegtagadásos támadás, és több indítása.

Nincs mindig könnyen rendszergazdai jogosultságokkal, vagy távolítsa el.
Vegye figyelembe a gyakori forgatókönyv, ahol telepítve van a DNS-szerepkört az Active Directory-tartományvezérlő ugyanazon a számítógépen.
A DNS-rendszergazdák helyi rendszergazdai jogosultsága a DNS-kiszolgálóval kapcsolatos problémák megoldása, de a művelet végrehajtásához, így kell tenni őket a kiemelt jogosultságokkal rendelkező "Tartományi rendszergazdák" biztonsági csoport szükséges.
Ez a megközelítés hatékonyan biztosít a DNS-rendszergazdák szabályozhatják a teljes tartomány és a hozzáférés meg, hogy a gép összes erőforrás.

JEA segít a probléma segítenek elfogadják a elve *legalacsonyabb jogosultsági szint*.
Az JEA beállíthatja a felügyeleti végpont a DNS-rendszergazdák számára, amely hozzáférést biztosít a munkájához szükséges összes PowerShell-parancsok, de semmi további.
Ez azt jelenti, hogy a hozzáférés egy sor mérgezettként DNS-gyorsítótár javítására, illetve a DNS-kiszolgáló újraindítása nem szándékos jogosultsága ahhoz, hogy az Active Directory adnak, vagy keresse meg a fájlrendszer vagy potenciálisan veszélyes parancsfájlok futtatása.
Még jobb, ha a JEA munkamenet ideiglenes kiemelt jogosultságokkal rendelkező virtuális fiókok használatára van konfigurálva, a DNS-rendszergazdák kapcsolódhatnak a kiszolgálóra történő *nem rendszergazdai* -felhasználó hitelesítő adatait, és bármikor használatához általában szükség van-parancsok futtatásához rendszergazdai jogosultságokkal.
Ez a funkció lehetővé teszi felhasználók eltávolítása széles körben jogosultságú helyi vagy tartományi rendszergazdai szerepköröket, és ehelyett alaposan szabályozhatja azok minden számítógépen el.

## <a name="get-started-with-jea"></a>Ismerkedés a JEA

Megkezdheti JEA ma azon a számítógépen, amelyen a Windows Server 2016 vagy a Windows 10.
JEA egy Windows Management Framework frissítés régebbi operációs rendszereken is futtathatja.
Tudhat meg többet a követelmények, JEA használatára, és megtudhatja, használja, és naplózási JEA-végpont, tekintse meg a következő témaköröket:

- [Előfeltételek](prerequisites.md) -ismerteti, hogyan állítsa be a környezetet, JEA használatára.
- [Szerepkör képességek](role-capabilities.md) -szerepkörök, amelyek megadják, hogy mi a felhasználó számára engedélyezett a JEA-munkamenet az létrehozását ismerteti.
- [Munkamenet-konfigurációk](session-configurations.md) -ismerteti, hogy a felhasználók hozzárendelése szerepkörökhöz, és állítsa be a JEA identitás JEA végpontok konfigurálása
- [Regisztrálja a JEA](register-jea.md) - JEA-végpont létrehozása, és tegye elérhetővé a felhasználók csatlakoznak.
- [JEA használatával](using-jea.md) – ismerje meg a különböző módszereket, JEA.
- [Biztonsági szempontok](security-considerations.md) -tekintse át az ajánlott biztonsági eljárások és JEA konfigurációs beállítások következményeit.
- [Naplózása és jelentése JEA](audit-and-report.md) -megtudhatja, hogyan naplózása és jelentése JEA végpontok.

## <a name="samples-and-dsc-resource"></a>Kódminták és DSC-erőforrás

Minta JEA-konfiguráció és a JEA DSC erőforrás is található a [JEA GitHub-tárházban](https://github.com/PowerShell/JEA).