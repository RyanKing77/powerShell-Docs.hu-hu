---
ms.date: 07/10/2019
keywords: jea, PowerShell, biztonság
title: Elég felügyelet – áttekintés
ms.openlocfilehash: 4b74e5be9558810748a8844a325c8213e1b3ebc9
ms.sourcegitcommit: e894ed833cef57967cdaf002f8c883f66864e836
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/25/2019
ms.locfileid: "70017859"
---
# <a name="just-enough-administration"></a>Just Enough Administration

A elég adminisztráció (JEA) egy olyan biztonsági technológia, amely lehetővé teszi a delegált felügyeletet bármilyen, a PowerShell által felügyelt szolgáltatáshoz. A JEA a következőket teheti:

- **Csökkentse a rendszergazdák számát** a virtuális fiókok vagy csoportosan felügyelt szolgáltatásfiókok használatával, hogy a jogosultsági szintű műveleteket a normál felhasználók nevében végezze el.
- **Korlátozza a felhasználók** által elvégezhető parancsmagok, függvények és külső parancsok megadását.
- **Jobban megismerheti, hogy a felhasználók mit tesznek** olyan átiratokkal és naplókkal, amelyek pontosan megmutatják, hogy egy felhasználó milyen parancsokat futtatott a munkamenet során.

**Miért fontos a JEA?**

A kiszolgálók felügyeletéhez használt magas jogosultsági szintű fiókok komoly biztonsági kockázatot jelentenek. Ha egy támadó megsért egy ilyen fiókot, a szervezeten belül [oldalirányú támadásokat](https://aka.ms/pth) indíthat. Az egyes feltört fiókok még több fiókot és erőforrást biztosítanak a támadók számára, és egy lépéssel közelebb kerülnek a vállalati titkok ellopásához, a szolgáltatásmegtagadási támadások elindításához és egyebekhez.

A rendszergazdai jogosultságok nem mindig könnyen eltávolíthatók. Vegye figyelembe azt a gyakori forgatókönyvet, amelyben a DNS-szerepkör ugyanarra a gépre van telepítve, mint a Active Directory-tartomány vezérlő. A DNS-rendszergazdáknak helyi rendszergazdai jogosultságokkal kell rendelkezniük a DNS-kiszolgálóval kapcsolatos problémák megoldásához. Ehhez azonban a magas jogosultsági szintű **tartományi rendszergazdák** biztonsági csoport tagjait kell megtennie. Ez a megközelítés hatékonyan biztosítja a DNS-rendszergazdák számára a teljes tartomány feletti irányítást, valamint az adott gépen lévő összes erőforrás elérését.

A JEA a **legalacsonyabb jogosultsági**szint elve alapján kezeli ezt a problémát. A JEA használatával olyan felügyeleti végpontot konfigurálhat a DNS-rendszergazdák számára, amely csak a feladataik elvégzéséhez szükséges PowerShell-parancsokhoz biztosít hozzáférést. Ez azt jelenti, hogy megadhatja a megfelelő hozzáférést a megmérgezett DNS-gyorsítótár kijavításához vagy a DNS-kiszolgáló újraindításához anélkül, hogy véletlenül jogosultságot adna Active Directory vagy a fájlrendszer tallózására, vagy potenciálisan veszélyes parancsfájlok futtatására. Még jobb, ha a JEA-munkamenet ideiglenes privilegizált virtuális fiókok használatára van konfigurálva, a DNS-rendszergazdák **nem rendszergazdai** hitelesítő adatokkal csatlakozhatnak a kiszolgálóhoz, és továbbra is futtathatnak olyan parancsokat, amelyek általában rendszergazdai jogosultságokat igényelnek. A JEA lehetővé teszi a felhasználók eltávolítását a széles körű jogosultságú helyi/tartományi rendszergazdai szerepkörökből, és körültekintően szabályozhatja, hogy mit tehetnek az egyes gépeken.

## <a name="next-steps"></a>További lépések

Ha többet szeretne megtudni a JEA használatára vonatkozó követelményekről, tekintse meg az [Előfeltételek](prerequisites.md) című cikket.

## <a name="samples-and-dsc-resource"></a>Minták és DSC-erőforrás

A JEA-konfigurációk és a JEA DSC-erőforrás a [JEA GitHub](https://github.com/PowerShell/JEA)-tárházban található.
