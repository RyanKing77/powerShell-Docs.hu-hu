---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: A célállapot-konfiguráció áttekintése döntéshozók számára
ms.openlocfilehash: ce554d4bb994d4b1816d9d9c24599e4ef0e1c593
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62079591"
---
# <a name="desired-state-configuration-overview-for-decision-makers"></a>A célállapot-konfiguráció áttekintése döntéshozók számára

Ez a dokumentum ismerteti az üzleti előnyei Windows PowerShell Desired State Configuration (DSC). Már nem műszaki útmutatója.

## <a name="what-is-desired-state-configuration"></a>Mi a Desired State Configuration?

PowerShell Desired State Configuration az nyílt szabványok alapján Windows beépített konfigurációs felügyeleti platform. DSC elég rugalmas, megbízható és konzisztens módon működnek az egyes fázisokban, a központi telepítési életciklus (fejlesztés, teszt, éles üzem előtti, éles környezetben), valamint a horizontális felskálázás során.

DSC-erőforrások köré [konfigurációk](../configurations/configurations.md).
Egy konfigurációs egy könnyen olvasható dokumentum, amely leírja a számítógépeket ("csomópont") adott jellemzőkkel rendelkező környezetben.
Ezek a jellemzők egyszerűen biztosítása egy adott Windows-szolgáltatás engedélyezett vagy a SharePoint központi telepítése összetett lehet.

DSC is rendelkezik figyelési és jelentéskészítési beépített.
A rendszer már nem megfelelő, ha DSC riasztást, és javítsa ki a rendszer a működésre.

## <a name="benefits-of-using-desired-state-configuration"></a>Desired State Configuration használatának előnyei

Konfigurációk könnyen olvasható, tárolja, és frissítve lettek kialakítva.
Konfigurációk deklarálja, hogy az állapot Céleszközök kell lennie, ahelyett, hogy hogyan helyezi őket abban az állapotban lévő utasításokat.
Így sokkal kevésbé költséges, ismerje meg, elfogadja, megvalósításához és keresztül DSC konfigurációs karbantartása.

Konfigurációk létrehozása, az azt jelenti, hogy összetett üzembe helyezési lépések rögzíti a rendszer egy "egyetlen hiteles forrásaként", egyetlen helyen.
Ez lehetővé teszi egy adott készletét gépek ismételt központi telepítései sokkal kevésbé hibalehetőséget magában rejtő.
Így gyorsabb és megbízhatóbb központi telepítések lehetővé teszi a egy gyors válaszidejű, optimalizált összetett üzemelő példányok esetében.

Konfigurációk a következők is megosztható keresztül a [PowerShell-galériából](https://powershellgallery.com) azaz gyakori forgatókönyvek és ajánlott eljárások előfordulhat, hogy már létezik az elvégezni kívánt munka.


## <a name="desired-state-configuration-and-devops"></a>Desired State Configuration és a fejlesztés és üzemeltetés

DSC úgy lett kialakítva [fejlesztési és üzemeltetési](http://blogs.technet.com/b/ashleymcglone/archive/2015/11/20/devops-for-n00bs-ie-windows-people.aspx) szem előtt, a személyeket, folyamatokat és eszközöket, amelyek lehetővé teszik a gyors üzembe helyezési és az iteráció kombinációja összpontosított érték továbbítása a végfelhasználók számára, hogy belső vagy külső.
Adja meg egy környezetben azt jelenti, hogy a fejlesztők is kódolása a rájuk vonatkozó követelményeket a konfigurációban, ellenőrizze, hogy forrásvezérlőben konfigurációját és a művelet csapatok egyetlen konfigurációval rendelkező üzembe helyezhetik a kód nélkül haladhat végig hibalehetőséget magában rejtő manuális folyamatokat.

Konfigurációk a következők is [adatvezérelt](../configurations/configData.md), amely megkönnyíti a ops azonosításához, és módosítsa a környezetek fejlesztői beavatkozás nélkül.

## <a name="desired-state-configuration-on-premises-and-off-premises"></a>Helyszíni és a helyszíni Desired State Configuration
DSC a helyszíni és a helyszíni központi telepítéseinek kezeléséhez használható.
A helyszíni megoldásokhoz, DSC rendelkezik egy [lekéréses kiszolgálón](../pull-server/pullServer.md) gépek kezelésének központosítása és a jelentés az állapotukat, amely használható.
A felhőalapú megoldások DSC akkor használható bárhol is legyenek Windows használható.
Még nincsenek különleges ajánlatok a Desired State Configuration, például a beépített Azure-ból [Azure Automation](https://azure.microsoft.com/en-us/documentation/services/automation/), amely központosítja a DSC-jelentés.

## <a name="dsc-and-compatibility"></a>DSC és kompatibilitása

Bár a Windows Server 2012 R2 DSC jelent meg, azt keresztül a Windows Management Framework (WMF) csomag régebbi verziójú operációs rendszerekhez érhető el.
A WMF kapcsolatos további információk találhatók a [PowerShell kezdőlap](/powershell/).

DSC a Linux kezelésére is használható. További információkért lásd: [Linuxhoz készült DSC – első lépések](../getting-started/lnxGettingStarted.md).
