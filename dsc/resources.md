---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "A DSC-erőforrások"
ms.openlocfilehash: 62bf352b929d661e585e145e5aab0f44f13010a1
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
# <a name="dsc-resources"></a>A DSC-erőforrások

>Vonatkozik: A Windows PowerShell 4.0-s verzióját, a Windows PowerShell 5.0

A kívánt állapot konfigurációs szolgáltatása (DSC) forrásokban a építőelemeket DSC-konfiguráció. Egy erőforrás konfigurált (séma), valamint a PowerShell parancsfájl olyan függvényeket tartalmaz, hogy "," meghívja a helyi Configuration Manager (LCM) tulajdonságok közzététele.

Egy erőforrás modellezhető valamilyen általános fájlként, vagy egy olyan IIS-kiszolgálói beállítást legpontosabb.  Például erőforrások csoportja, amelyek rendszerezi az összes szükséges fájlt a hordozható, és a metaadatok azonosítására, hogyan a az erőforrásokhoz való használatra készült tartalmazó struktúrára DSC modulra van összevonva.  

A következő témakörök ismertetik a DSC-erőforrások:

- [Beépített DSC-erőforrások](builtInResource.md)
- [Egyéni DSC-erőforrások létrehozása](authoringResource.md)
- [Linux beépített DSC-erőforrások](lnxBuiltInResources.md)

