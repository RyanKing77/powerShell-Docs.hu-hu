---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "A DSC WaitForAny erőforrás"
ms.openlocfilehash: 43922dbcccb6d06d7d9edfcf16ce4eb107e9d4e6
ms.sourcegitcommit: 99227f62dcf827354770eb2c3e95c5cf6a3118b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/15/2018
---
# <a name="dsc-waitforany-resource"></a>A DSC WaitForAny erőforrás

> Vonatkozik: A Windows PowerShell 5.1-es és újabb verziók

A **WaitForSome** kívánt állapot konfigurációs szolgáltatása (DSC) erőforrás használhatja egy csomópont blokkja egy [DSC-konfiguráció](configurations.md) függőségek konfigurációk létrehozáskor határozza meg.

Ehhez az erőforráshoz sikeres lesz, ha az erőforrás által megadott Ha a **ResourceName** tulajdonság a bármilyen definiált célcsomópontokat megfelelő állapotban van a **csomópontnév** tulajdonság.


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
| resourceName| Az erőforrásnév függ. Ha egy másik konfigurációs ehhez az erőforráshoz tartozik, a neve, ahogyan formázása "[__ResourceType__]__ResourceName__:: [__ConfigurationName__]:: [ __ConfigurationName__] "| 
| Csomópontnév| Az erőforrás függ a célcsomópontokat.| 
| RetryIntervalSec| Másodpercig az újrapróbálkozás előtt száma. Minimális érték 1.| 
| a retryCount| A próbálkozások maximális számát.| 
| ThrottleLimit| Az egyidejű csatlakozást a gépek számát. Alapértelmezés szerint új-cimsession alapértelmezett.| 
| dependsOn | Azt jelzi, hogy egy másik erőforrás konfigurációjának kell futtatni, mielőtt ehhez az erőforráshoz van konfigurálva. Például, ha az erőforrás-konfiguráció azonosítója blokk futtatni kívánt parancsfájl első az __ResourceName__ és annak típusa __ResourceType__, az e tulajdonság használatával szintaxisa a következő `DependsOn = "[ResourceType]ResourceName"`.|


## <a name="example"></a>Példa

Példa bemutatja, hogyan az erőforrás, lásd: [cross-csomópont függőségeinek megadása](crossNodeDependencies.md)

