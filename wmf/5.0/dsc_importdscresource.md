---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: ce5afc2f90f78433b64bf5b41946fc7506c43504
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2018
ms.locfileid: "34219650"
---
# <a name="import-dscresource-keyword-supports--moduleversion-parameter"></a>Importálás – DscResource kulcsszó - ModuleVersion paraméter támogatja

Egy új paraméter jelentek meg a `Import-DscResource` érhető el, ha a DSC-konfigurációk szerzői dinamikus kulcsszó. Konfigurációs szerzők mostantól megadhatja, hogy pontosan melyik verziója a DSC-erőforrások betöltése. A kulcsszó új szintaxisa:

```powershell
Import-DscResource [-Name <ResourceName(s)>] [-ModuleName <ModuleName(s)>] [-ModuleVersion <ModuleVersion>]
```

* **Név**: egy vagy több erőforrás importálása nevét.
* **Modulnév**: modulneveket vagy ModuleSpecification objektumok importálása egy vagy több modulja.
* **ModuleVersion**: Soha importálás verzióját. Ha használ, modulename: csak egy modul kell meghatároznia név szerint.

A Windows PowerShell ISE azt mutatja az IntelliSense:

![](../images/Import-DscResource-Modversion.jpg)

**Megjegyzés:**: a `–ModuleVersion` paraméter csak akkor használható együtt a `–ModuleName` paraméter. Az erőforrás nevét, csak a nem használható a `–Name` paraméter.

Ez csak úgy lehet megadni a modul verzióját, ha a DSC-erőforrások betöltése volt a modul specification objektum pl.: `–ModuleName @{ModuleName="UserConfigProvider";ModuleVersion="3.0"}`
