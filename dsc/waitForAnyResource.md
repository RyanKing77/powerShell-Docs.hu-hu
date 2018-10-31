---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC WaitForAny erőforrás
ms.openlocfilehash: 39100f0fc52092c54bbecab55e3ef3dfabb4c70e
ms.sourcegitcommit: e76665315fd928bf85210778f1fea2be15264fea
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/30/2018
ms.locfileid: "50226049"
---
# <a name="dsc-waitforany-resource"></a>DSC WaitForAny erőforrás

> A következőkre vonatkozik: Windows PowerShell 5.1-es és újabb verziók

A **WaitForSome** egy csomópont letiltása a Desired State Configuration (DSC) erőforrás használható egy [DSC-konfiguráció](configurations.md) függőségeinek megadása a konfigurációk a többi csomóponton.

Ez az erőforrás sikeres lesz, abban az esetben, ha az erőforrás által meghatározott a **ResourceName** tulajdonság bármely meghatározott cél-csomópontokon a kívánt állapotban van a **csomópontnév** tulajdonság.


## <a name="syntax"></a>Szintaxis

```
WaitForAny [string] #ResourceName
{
    ResourceName = [string]
    NodeName = [string]
    [ RetryIntervalSec = [Uint64] ]
    [ RetryCount = [Uint32] ]
    [ ThrottleLimit = [Uint32]]
    [ DependsOn = [string[]] ]
}
```

## <a name="properties"></a>Tulajdonságok

|  Tulajdonság  |  Leírás   |
|---|---|
| Erőforrásnév| Az erőforrásnév függenek. Ha az erőforrás tartozik egy másik konfigurációs, formázhatja a nevet a következőként "[__ResourceType__]__ResourceName__:: [__ConfigurationName__]:: [ __ConfigurationName__] "|
| Csomópontnév| Az erőforrás függenek a célcsomópontokat.|
| RetryIntervalSec| Mielőtt újra próbálkozna másodpercek számát. Minimális érték 1.|
| retryCount| Az újrapróbálkozások maximális száma.|
| ThrottleLimit| Egyidejű csatlakozás gépek száma. Alapértelmezés szerint új cimsession alapértelmezett.|
| DependsOn | Azt jelzi, hogy a konfigurációt egy másik erőforrás futtatnia kell, mielőtt az erőforrás konfigurálva van. Például, ha az erőforrás-konfiguráció azonosítója letiltása, a futtatni kívánt parancsfájl először van __ResourceName__ és a típusa __ResourceType__, ez a tulajdonság használata esetén `DependsOn = "[ResourceType]ResourceName"`.|


## <a name="example"></a>Példa

Egy példa bemutatja, hogyan használhatja ezt az erőforrást: [csomópontok közötti függőségek megadása](crossNodeDependencies.md)