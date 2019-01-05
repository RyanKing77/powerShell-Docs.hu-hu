---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC WaitForAny erőforrás
ms.openlocfilehash: 39e90f0df3459b8891ed46e02ae82c45a285e7f5
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048438"
---
# <a name="dsc-waitforany-resource"></a>DSC WaitForAny erőforrás

> Érvényes: Windows PowerShell 5.1-es és újabb verziók

A **WaitForSome** egy csomópont letiltása a Desired State Configuration (DSC) erőforrás használható egy [DSC-konfiguráció](../../../configurations/configurations.md) függőségeinek megadása a konfigurációk a többi csomóponton.

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

Egy példa bemutatja, hogyan használhatja ezt az erőforrást: [csomópontok közötti függőségek megadása](../../../configurations/crossNodeDependencies.md)
