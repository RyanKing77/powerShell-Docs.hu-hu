---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "A DSC WaitForSome erőforrás"
ms.openlocfilehash: 8b0ad0dbd31816cc673c7f77945927987e90e08b
ms.sourcegitcommit: 99227f62dcf827354770eb2c3e95c5cf6a3118b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/15/2018
---
# <a name="dsc-waitforsome-resource"></a>A DSC WaitForSome erőforrás

> Vonatkozik: A Windows PowerShell 5.0-s és újabb verziók

A **WaitForAny** kívánt állapot konfigurációs szolgáltatása (DSC) erőforrás használhatja egy csomópont blokkja egy [DSC-konfiguráció](configurations.md) függőségek konfigurációk létrehozáskor határozza meg.

Ehhez az erőforráshoz sikeres lesz, ha az erőforrás által megadott a **ResourceName** tulajdonság szerepel a kívánt állapot, a csomópontok minimális száma (által megadott **NodeCount**) határozzák meg a **csomópontnév**  tulajdonság. 


## <a name="syntax"></a>Szintaxis

```
WaitForSome [String] #ResourceName
{
    NodeCount = [UInt32]
    NodeName = [string[]]
    ResourceName = [string]
    [DependsOn = [string[]]]
    [PsDscRunAsCredential = [PSCredential]]
    [RetryCount = [UInt32]]
    [RetryIntervalSec = [UInt64]]
    [ThrottleLimit = [UInt32]]
}
```

## <a name="properties"></a>Tulajdonságok

|  Tulajdonság  |  Leírás   | 
|---|---| 
| NodeCount| Ehhez az erőforráshoz sikeres megfelelő állapotban kell lennie csomópontok minimális száma.|
| Csomópontnév| Az erőforrás függ a célcsomópontokat.| 
| resourceName| Az erőforrásnév függ. Ha egy másik konfigurációs ehhez az erőforráshoz tartozik, a neve, ahogyan formázása "[__ResourceType__]__ResourceName__:: [__ConfigurationName__]:: [ __ConfigurationName__] "| 
| RetryIntervalSec| Másodpercig az újrapróbálkozás előtt száma. Minimális érték 1.| 
| a retryCount| A próbálkozások maximális számát.| 
| ThrottleLimit| Az egyidejű csatlakozást a gépek számát. Alapértelmezés szerint új-cimsession alapértelmezett.| 
| dependsOn | Azt jelzi, hogy egy másik erőforrás konfigurációjának kell futtatni, mielőtt ehhez az erőforráshoz van konfigurálva. Például, ha az erőforrás-konfiguráció azonosítója blokk futtatni kívánt parancsfájl első az __ResourceName__ és annak típusa __ResourceType__, az e tulajdonság használatával szintaxisa a következő `DependsOn = "[ResourceType]ResourceName"`.|
| PsDscRunAsCredential | Lásd: [DSC hitelesítő adatokkal rendelkező felhasználó](https://docs.microsoft.com/powershell/dsc/runasuser) |


## <a name="example"></a>Példa

Példa bemutatja, hogyan az erőforrás, lásd: [cross-csomópont függőségeinek megadása](crossNodeDependencies.md)

