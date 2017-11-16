---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "A DSC WaitForAll erőforrás"
ms.openlocfilehash: dcc23ad4e6905bc277ad39348350d5425fc90ad7
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
# <a name="dsc-waitforall-resource"></a>A DSC WaitForAll erőforrás

> Vonatkozik: A Windows PowerShell 5.0-s és újabb verziók

A **WaitForAll** kívánt állapot konfigurációs szolgáltatása (DSC) erőforrás használhatja egy csomópont blokkja egy [DSC-konfiguráció](configurations.md) függőségek konfigurációk létrehozáskor határozza meg.

Ehhez az erőforráshoz sikeres lesz, ha az erőforrás által megadott Ha a **ResourceName** tulajdonság definiált összes cél csomóponton megfelelő állapotban van a **csomópontnév** tulajdonság.


## <a name="syntax"></a>Szintaxis

```
WaitForAll [string] #ResourceName
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
| resourceName| Az erőforrásnév függ.| 
| Csomópontnév| Az erőforrás függ a célcsomópontokat.| 
| RetryIntervalSec| Másodpercig az újrapróbálkozás előtt száma. Minimális érték 1.| 
| a retryCount| A próbálkozások maximális számát.| 
| ThrottleLimit| Az egyidejű csatlakozást a gépek számát. Alapértelmezés szerint új-cimsession alapértelmezett.| 
| dependsOn | Azt jelzi, hogy egy másik erőforrás konfigurációjának kell futtatni, mielőtt ehhez az erőforráshoz van konfigurálva. Például, ha az erőforrás-konfiguráció azonosítója blokk futtatni kívánt parancsfájl első az __ResourceName__ és annak típusa __ResourceType__, az e tulajdonság használatával szintaxisa a következő `DependsOn = "[ResourceType]ResourceName"`.|


## <a name="example"></a>Példa

Példa bemutatja, hogyan az erőforrás, lásd: [cross-csomópont függőségeinek megadása](crossNodeDependencies.md)

