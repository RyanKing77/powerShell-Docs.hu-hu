---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: A célállapot-konfiguráció áttekintése döntéshozók számára
ms.openlocfilehash: 8b410420ef30b066a32864a0d08a12a8485eaa4b
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="desired-state-configuration-overview-for-decision-makers"></a>A célállapot-konfiguráció áttekintése döntéshozók számára

Ez a dokumentum ismerteti az üzleti előnyei a PowerShell kívánt állapot konfigurációs szolgáltatása (DSC). Műszaki útmutató nincs.

## <a name="what-is-desired-state-configuration"></a>Mi az célállapot konfiguráló?

Windows PowerShell kívánt állapot konfigurációs szolgáltatása (DSC) olyan nyitott szabványok alapuló Windows beépített konfigurációs felügyeleti platform. A DSC-ből elég rugalmas, megbízható és konzisztens működéséhez az egyes fázisokban, a központi telepítési életciklus (fejlesztési, tesztelési, éles üzem előtti, éles), és a kibővített.

DSC adatközpontok körül "[konfigurációk](https://msdn.microsoft.com/powershell/dsc/configurations)".
A beállítás egy olyan számítógépeket ("csomópont") adott tulajdonságokkal rendelkező környezetben egy könnyen áttekinthető ismertető dokumentum.
Lehet, hogy a következő jellemzőkkel más dolga, mint annak biztosításában, egy adott Windows-szolgáltatás engedélyezve vagy nem lehet összetett, mint a SharePoint központi telepítése.

A DSC-ből is rendelkezik figyelési és jelentéskészítési beépített.
Ha a rendszer már nem megfelelő, DSC hoz létre riasztást, és javítsa ki a rendszer való.

## <a name="benefits-of-using-desired-state-configuration"></a>Célállapot-konfiguráció használatának előnyei

Konfigurációk könnyen olvasható, tárolja, és frissítve lettek kialakítva.
Konfigurációk deklarálja a állapot Céleszközök kell megadni, ahelyett utasításokkal szolgál, amelyre az őket az adott állapotban.
Ennek köszönhetően sokkal kevésbé költséges, elfogadja, valósítja meg, valamint keresztül DSC konfigurációs karbantartása.

Konfigurációk létrehozásához, az azt jelenti, hogy összetett üzembe helyezés lépései a rendszer rögzíti forrásaként"egyetlen igazság" egyetlen helyen megvalósítható.
Így a gépek egy adott csoportjának ismételt központi telepítéséhez sokkal kevesebb hibákhoz vezethet.
Így gyorsabb és megbízhatóbb központi telepítések lehetővé teszi a egy gyors esetenként összetett üzemelő példányok esetében.

Konfigurációk megtalálhatók megosztható keresztül a [PowerShell-galériában](https://powershellgallery.com) gyakori forgatókönyvek és ajánlott eljárások talán már létezik a dolgozott van szüksége.


## <a name="desired-state-configuration-and-devops"></a>Célállapot-konfiguráció és Devopok

[DevOps](http://blogs.technet.com/b/ashleymcglone/archive/2015/11/20/devops-for-n00bs-ie-windows-people.aspx) személyek, a folyamat, valamint az eszközök, amelyek lehetővé teszik a gyors üzembe helyezési és iterációs összpontosított érték továbbítása a végfelhasználók számára, hogy a belső vagy külső kombinációja.
A DSC úgy lett kialakítva, a DevOps szem előtt.
Egy olyan környezetben egyetlen konfigurációval rendelkező megadása azt jelenti, hogy a fejlesztők is kódolja a követelményeknek, a konfiguráció, ellenőrizze, hogy az adatforrás-vezérlő konfigurálása és műveletek csapat könnyedén telepítheti kód nem kell végighaladnia hibákhoz vezethet manuálisan végrehajtott folyamatokat.

Konfigurációk megtalálhatók [adatvezérelt](https://msdn.microsoft.com/powershell/dsc/configdata), így egyszerűbb azonosításához, és módosítsa a fejlesztői beavatkozás nélküli környezetekben ops csoportjai.

## <a name="desired-state-configuration-on--and-off-premises"></a>Célállapot-konfiguráció - és kikapcsolása-helyszíni

A DSC mind a helyszíni, mind a helyszíni központi telepítések felügyeletéhez használható.
A helyszíni megoldásokkal, DSC rendelkezik egy [lekérési kiszolgálójával](https://msdn.microsoft.com/powershell/dsc/pullserver) , amelyek segítségével központosíthatja a gépek felügyeletét és a jelentés az állapotuk.
A felhőalapú megoldások DSC használható legyen a Windows rendszer használható.
Van még a célállapot-konfiguráció, például a épülő Azure adott ajánlatok [Azure Automation](https://azure.microsoft.com/en-us/documentation/services/automation/), amely központosítja DSC jelentése.

## <a name="dsc-and-compatibility"></a>A DSC-ből és kompatibilitása

Bár a DSC-ből Windows Server 2012 R2 rendszerben jelent meg, érhető el a régebbi operációs rendszerekhez a Windows Management Framework (WMF) csomag segítségével.
A WMF további információ található a [PowerShell kezdőlap](https://msdn.microsoft.com/en-us/powershell/).

A DSC Linux kezelésére is használható. További információkért lásd: [Ismerkedés a Linux DSC](https://msdn.microsoft.com/en-us/powershell/dsc/lnxgettingstarted).