---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: WMF, powershell, beállítás
ms.openlocfilehash: a3b176101bebf7081febd8629bddcfa0ae1e7540
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
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