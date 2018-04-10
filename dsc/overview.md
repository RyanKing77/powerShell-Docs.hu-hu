---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: A Windows PowerShell célállapot-konfiguráló áttekintése
ms.openlocfilehash: 3f357ea11a388a05b73539a63e52e639ee906f68
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="windows-powershell-desired-state-configuration-overview"></a>A Windows PowerShell célállapot-konfiguráló áttekintése

> Vonatkozik: A Windows PowerShell 4.0-s verzióját, a Windows PowerShell 5.0

A DSC-ből egy olyan felügyeleti platformot, amely lehetővé teszi az informatikai kezelését PowerShell és a fejlesztői infrastruktúra és kód-konfigurációt.

- Az üzleti előnyei a DSC áttekintését lásd: [kívánt állapot konfigurációs áttekintése döntéshozók](decisionMaker.md).
- A mérnöki előnyei a DSC áttekintését lásd: [kívánt állapot konfigurációs áttekintése mérnökök](DscForEngineers.md).
- A DSC gyorsan használatának megkezdéséhez tekintse meg [DSC gyors üzembe helyezési](quickStart.md).

## <a name="key-concepts"></a>Alapfogalmak

A DSC-ből a egy konfigurációs, telepítési és felügyeleti rendszerek használt deklaratív platformja. Azt a három elsődleges összetevőből áll:

- [Konfigurációk](configurations.md) deklaratív PowerShell parancsfájlok, amely határozza meg, és erőforrások példányainak konfigurálásához.
    A konfiguráció, DSC (és az erőforrásokat, a konfiguráció által meghívott) lesz, egyszerűen "tenni,", győződjön meg arról, hogy létezik-e a rendszer a konfiguráció leírva állapotban.
    A DSC-konfigurációk megtalálhatók az idempotent: a helyi Configuration Manager (LCM) továbbra is győződjön meg arról, hogy gépek konfigurálva vannak-e bármilyen állapot, a konfiguráció a deklarál.
- [Erőforrások](resources.md) DSC "legyen," részét képezik. A put és a cél konfiguráció ne a megadott állapot kódot tartalmaznak.
    Erőforrások PowerShell-modulok találhatók, és csak írható modell valamilyen általános egy fájl vagy a Windows-folyamat vagy egy IIS-kiszolgálón vagy egy Azure-beli virtuális gép legpontosabb.
- A [helyi Configuration Manager (LCM)](metaConfig.md) a motor, amely DSC elősegíti a konfigurációk és erőforrások közötti kapcsolat.
    A LCM rendszeresen lekérdezi a rendszer az erőforrások által megvalósított folyamata segítségével győződjön meg arról, hogy megőrződjön-e a konfiguráció által meghatározott állapotot.
    Állapotát a rendszer esetén a LCM teszi a kód hívásainak erőforrások ahhoz "," konfigurációjának megfelelően.

## <a name="see-also"></a>Lásd még:

- [A DSC-konfigurációk](configurations.md)
- [A DSC-erőforrások](resources.md)
- [A helyi Configuration Manager konfigurálása](metaConfig.md)