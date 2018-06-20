---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: da603fda4499129b415477f627842fe10abefe06
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/16/2018
ms.locfileid: "34188496"
---
# <a name="just-enough-administration-jea"></a>Just Enough Administration (JEA)
Csak elég felügyeleti az új szolgáltatása, amely lehetővé teszi, hogy a szerepkör alapú felügyelet PowerShell távoli eljáráshívás keresztül WMF 5.0.  Az kiterjeszti a meglévő korlátozott végpont infrastruktúra azáltal, hogy a nem rendszergazda konkrét parancsok, parancsfájlok és végrehajtható fájlok futtassa rendszergazdaként.  Ez lehetővé teszi a környezetében teljes rendszergazdák számának csökkentése és a biztonság növelése.  JEA működik minden kezelheti a PowerShell segítségével; Ha valaminek a PowerShell használatával kezelheti, JEA is segítséget nyújthat így biztonságosabban.  Csak elég felügyeleti részletes vizsgálja meg, tekintse meg a [útmutató élmény](http://aka.ms/JEA).

Régi korlátozott végpontok, ellentétben a JEA egyben a hatékony és könnyen konfigurálható.  Felhasználói képességei JEA granularly szabályozhatja, mely paraméterkészletei és értékeket is kell adni egy adott parancshoz korlátozása le. A felhasználói műveletek egy egyszeri virtuális fiók, amely a felügyeleti műveletek elvégzéséhez jogosultsággal rendelkezik a környezetében futnak.  A felhasználó által indított a parancsok a biztonsági naplózás kell jelentkeznie.

JEA működik azáltal, hogy kifejezetten konfigurált korlátozott végpontokat hoz létre.  Ezeket a végpontokat néhány fontos jellemzőkkel rendelkezik:

1. Azokat a "Futtatás mint" a védett virtuális fiók, amely a távoli munkamenet időtartama alatt csak a kapcsolódó felhasználókat.  Alapértelmezés szerint ez a virtuális fiók tagja a beépített Rendszergazdák csoportnak, valamint a tartományvezérlőkön a tartományi rendszergazdák (Megjegyzés: ezek az engedélyek is konfigurálható). Csatlakozás egy felhasználó nevében, és más, jogosultsággal rendelkező felhasználóként fut, engedélyezheti a rendszerjogosultsággal nem rendelkező felhasználók nem rendszerek rendszergazdai jogosultságokkal adnak bizonyos felügyeleti feladatok végrehajtásához.
2. A végpont zárolva van.  Ez azt jelenti, hogy a PowerShell futtatása nem nyelvi módban.  Csak a konkrét parancsok, parancsfájlok és végrehajtható fájlok a felhasználó számára láthatók.
3. Csatlakozó más felhasználók számára a különböző képességek egy készletét, csoporttagság alapján vannak feltüntetve.  Más szerepkörök biztosíthat a azonos végpont különböző képességeket.
