---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 46a278b83edb9d8e3d75b0874603710d416be3b5
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62085750"
---
# <a name="import-dscresource-keyword-supports--moduleversion-parameter"></a>Az import-DscResource kulcsszó támogatja a - ModuleVersion paramétert

Új paraméter hozzáadtuk a `Import-DscResource` dinamikus kulcsszó szerzői DSC-konfigurációk esetén érhető el. Konfigurációs szerzők megadhatja pontosan melyik verziója betölteni a DSC-erőforrásait. Új kulcsszó szintaxisa:

```powershell
Import-DscResource [-Name <ResourceName(s)>] [-ModuleName <ModuleName(s)>] [-ModuleVersion <ModuleVersion>]
```

* **Név**: Egy vagy több erőforrás importálása nevei.
* **ModuleName**: A modul nevét vagy ModuleSpecification objektumok importálása egy vagy több modulja.
* **ModuleVersion**: Modul importálása verzióját. Ha használta, modulename: csak egy modult kell meghatároznia név alapján.

A Windows PowerShell ISE-ben az megjelenik az IntelliSense használatával:

![](../images/Import-DscResource-Modversion.jpg)

**Megjegyzés:**: a `–ModuleVersion` paraméter csak akkor használható együtt a `–ModuleName` paraméter. Az erőforrás-nevek használatával csak nem használható a `–Name` paraméter.

Korábban az adja meg a modul verzióját, DSC-erőforrások betöltése során csak úgy lett pl. specification modul objektum segítségével: `–ModuleName @{ModuleName="UserConfigProvider";ModuleVersion="3.0"}`
