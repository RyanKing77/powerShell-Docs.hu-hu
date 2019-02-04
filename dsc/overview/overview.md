---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Windows PowerShell Desired State Configuration áttekintése
ms.openlocfilehash: 3e4f0afa17ab60bfa98f1b86b9830462a7c8e1cf
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55686312"
---
# <a name="windows-powershell-desired-state-configuration-overview"></a>Windows PowerShell Desired State Configuration áttekintése

> Érvényes: Windows PowerShell 4.0-s, a Windows PowerShell 5.0

DSC egy felügyeleti platform, amely lehetővé teszi, hogy az informatikai RÉSZLEG felügyelete PowerShell és a fejlesztési infrastruktúra mint kód konfigurációval.

- Az üzleti előnyei DSC áttekintését lásd: [Desired State Configuration áttekintése döntéshozók számára](decisionMaker.md).
- A mérnöki előnyei DSC áttekintését lásd: [Desired State Configuration áttekintése mérnökök számára](DscForEngineers.md).
- DSC használatának gyors megkezdéséhez lásd [DSC gyors üzembe helyezési](../quickstarts/website-quickstart.md).

## <a name="key-concepts"></a>Fő fogalmak

DSC az deklaratív platform konfiguráció, telepítési és felügyeleti rendszerek használható. Három elsődleges összetevőből áll:

- [Konfigurációk](../configurations/configurations.md) deklaratív PowerShell-szkriptek, amelyek meghatározása és konfigurálása erőforráspéldány.
    Futtatása a konfiguráció, DSC (és az erőforrások által a konfiguráció) lesz, egyszerűen csak "Győződjön meg arról, hogy így", annak biztosítása, hogy létezik-e a rendszer által a konfiguráció állapotban.
    DSC-konfigurációk is idempotens: a helyi Configuration Manager (LCM) továbbra is győződjön meg arról, hogy a gépek megtörténik-e a függetlenül a konfigurációs állapot deklarálja.
- [Erőforrások](../resources/resources.md) DSC "Győződjön meg arról, hogy így" részét képezik. A put és a cél egy konfiguráció ne a megadott állapot kódját tartalmazza.
    Erőforrások PowerShell-modulok tartalmazhat, és írható, valamilyen általános egy fájl vagy egy Windows-folyamat vagy egy IIS-kiszolgáló vagy az Azure-ban futó virtuális gépek az adott modell.
- A [helyi Configuration Manager (LCM) Konfigurálása](../managing-nodes/metaConfig.md) a motor, amellyel DSC elősegíti a közötti interakció erőforrásokat és konfigurációkat.
    Az LCM rendszeresen lekérdezi a rendszer az erőforrások által megvalósított vezérlési folyamatában segítségével győződjön meg arról, hogy megőrződjön-e a konfiguráció által meghatározott állapotot.
    Ha a rendszer állapotát, a LCM teszi a kód meghívja "erőforrásaink, így" konfigurációjának megfelelően.

## <a name="see-also"></a>Lásd még:

- [DSC-konfigurációk](../configurations/configurations.md)
- [DSC-erőforrások](../resources/resources.md)
- [A helyi Configuration Manager](../managing-nodes/metaConfig.md)
