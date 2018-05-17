---
ms.date: 06/12/2017
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: A DSC-erőforrások
ms.openlocfilehash: 27e16c39699bb96b2829744b5700f75f59f8802f
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2018
---
# <a name="dsc-resources"></a>A DSC-erőforrások

>Vonatkozik: A Windows PowerShell 4.0-s verzióját, a Windows PowerShell 5.0

A kívánt állapot konfigurációs szolgáltatása (DSC) forrásokban a építőelemeket DSC-konfiguráció. Egy erőforrás konfigurált (séma), valamint a PowerShell parancsfájl olyan függvényeket tartalmaz, hogy "," meghívja a helyi Configuration Manager (LCM) tulajdonságok közzététele.

Egy erőforrás modellezhető valamilyen általános fájlként, vagy egy olyan IIS-kiszolgálói beállítást legpontosabb.  Például erőforrások csoportja, amelyek rendszerezi az összes szükséges fájlt a hordozható, és a metaadatok azonosítására, hogyan a az erőforrásokhoz való használatra készült tartalmazó struktúrára DSC modulra van összevonva.

A következő témakörök ismertetik a DSC-erőforrások:

- [Beépített DSC-erőforrások](builtInResource.md)
- [Egyéni DSC-erőforrások létrehozása](authoringResource.md)
- [Linux beépített DSC-erőforrások](lnxBuiltInResources.md)