---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: A DSC-erőforrások
ms.openlocfilehash: e393c8fe2e1ba8d68ba9aa1b656d1e5ebfad30e8
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="dsc-resources"></a>A DSC-erőforrások

>Vonatkozik: A Windows PowerShell 4.0-s verzióját, a Windows PowerShell 5.0

A kívánt állapot konfigurációs szolgáltatása (DSC) forrásokban a építőelemeket DSC-konfiguráció. Egy erőforrás konfigurált (séma), valamint a PowerShell parancsfájl olyan függvényeket tartalmaz, hogy "," meghívja a helyi Configuration Manager (LCM) tulajdonságok közzététele.

Egy erőforrás modellezhető valamilyen általános fájlként, vagy egy olyan IIS-kiszolgálói beállítást legpontosabb.  Például erőforrások csoportja, amelyek rendszerezi az összes szükséges fájlt a hordozható, és a metaadatok azonosítására, hogyan a az erőforrásokhoz való használatra készült tartalmazó struktúrára DSC modulra van összevonva.

A következő témakörök ismertetik a DSC-erőforrások:

- [Beépített DSC-erőforrások](builtInResource.md)
- [Egyéni DSC-erőforrások létrehozása](authoringResource.md)
- [Linux beépített DSC-erőforrások](lnxBuiltInResources.md)