---
title: Súgó fájlok elnevezési |} A Microsoft Docs
ms.custom: ''
ms.date: 09/12/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: bf54eac7-88c6-4108-a5f6-2f0906d1662b
caps.latest.revision: 5
ms.openlocfilehash: 06281a1260dbdc120867fce89e6d5c8dd0754b87
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56847277"
---
# <a name="naming-help-files"></a>Elnevezési súgófájlok

Ez a témakör azt ismerteti, hogyan egy XML-alapú súgófájl neve úgy, hogy a [Get-Help](/powershell/module/Microsoft.PowerShell.Core/Get-Help) parancsmag is megtalálhatják azt. A vonatkozó követelményeknek eltérőek az egyes parancsot.
Ez a témakör azt ismerteti, hogyan egy XML-alapú súgófájl neve úgy, hogy a [Get-Help](/powershell/module/Microsoft.PowerShell.Core/Get-Help) parancsmag is megtalálhatják azt. A vonatkozó követelményeknek eltérőek az egyes parancsot.

## <a name="cmdlet-help-files"></a>A parancsmag Súgó-fájlok

A súgófájlban talál egy C# parancsmag névvel kell rendelkeznie a szerelvény, amelyben a parancsmag definiálva van. Használja a következő fájl nevének formátuma:

```
<AssemblyName>.dll-help.xml
```

A szerelvény neve formátumra szükség, akkor is, ha a szerelvény egy beágyazott modul.

Ha például a [Get-WinEvent; PSITPro5_Diagnostic; ](/powershell/module/Microsoft.PowerShell.Diagnostics/Get-WinEvent) parancsmag Microsoft.PowerShell.Diagnostics.dll szerelvény van definiálva. A `Get-Help` parancsmag keres egy Súgó-témakör a `Get-WinEvent` parancsmag csak az modulkönyvtárat Microsoft.PowerShell.Diagnostics.dll-help.xml fájlban.
Ha például a [Get-WinEvent; PSITPro5_Diagnostic; ](/powershell/module/Microsoft.PowerShell.Diagnostics/Get-WinEvent) parancsmag Microsoft.PowerShell.Diagnostics.dll szerelvény van definiálva. A `Get-Help` parancsmag keres egy Súgó-témakör a `Get-WinEvent` parancsmag csak az modulkönyvtárat Microsoft.PowerShell.Diagnostics.dll-help.xml fájlban.

## <a name="provider-help-files"></a>Szolgáltató súgófájlok

A szerelvény, amelyben a szolgáltató van definiálva a súgófájlban talál egy Windows PowerShell-szolgáltatóban névvel kell rendelkeznie. Használja a következő fájl nevének formátuma:

```
<AssemblyName>.dll-help.xml
```

A szerelvény neve formátumra szükség, akkor is, ha a szerelvény egy beágyazott modul.

Ha például a tanúsítványszolgáltató Microsoft.PowerShell.Security.dll szerelvény van meghatározva. A `Get-Help` parancsmag a tanúsítvány-szolgáltató csak az modulkönyvtárat Microsoft.PowerShell.Security.dll-help.xml fájlban keres egy Súgó-témakört.

## <a name="function-help-files"></a>Függvény súgófájlok

Függvények használatával dokumentálni kell [Megjegyzés-alapú súgó](/powershell/module/microsoft.powershell.core/about/about_comment_based_help) vagy dokumentált súgó XML-fájlban. Ha a funkció leírása itt található egy XML-fájlt, a következő függvénynek rendelkeznie kell egy `.ExternalHelp` kulcsszó, amely összekapcsolja az XML-fájlt a funkciót megjegyzéseket. Ellenkező esetben a `Get-Help` parancsmag nem találja a súgófájlt.
Függvények használatával dokumentálni kell [Megjegyzés-alapú súgó](/powershell/module/microsoft.powershell.core/about/about_comment_based_help) vagy dokumentált súgó XML-fájlban. Ha a funkció leírása itt található egy XML-fájlt, a következő függvénynek rendelkeznie kell egy `.ExternalHelp` kulcsszó, amely összekapcsolja az XML-fájlt a funkciót megjegyzéseket. Ellenkező esetben a `Get-Help` parancsmag nem találja a súgófájlt.

Nem vonatkoznak technikai követelmények nevéhez egy függvény súgófájl. Azonban ajánlott eljárás, hogy nevezze el a súgófájlban a parancsfájl-modul, amely a függvény definiálva van. Például a következő függvényt a MyModule.psm1 fájlban van definiálva.

```csharp
#.ExternalHelp MyModule.psm1-help.xml
function Test-Function { ... }
```

## <a name="cim-command-help-files"></a>A CIM-parancs súgófájlok

A súgófájl a CIM-parancshoz névvel kell rendelkeznie a CDXML-fájlt, amelyben a CIM-parancs van definiálva. Használja a következő fájl nevének formátuma:

```
<FileName>.cdxml-help.xml
```

A CIM-parancsok beágyazott modulként modulokban szereplő CDXML fájlban vannak definiálva. A CIM-parancs a munkamenet függvényében való importálásakor, a Windows PowerShell ad hozzá egy `.ExternalHelp` Megjegyzés kulcsszó használatával a függvény definícióját, amely összekapcsolja a függvény egy XML-súgó-fájlba, amelyben a CIM-parancs van definiálva CDXML-fájl neve.

## <a name="script-workflow-help-files"></a>Parancsfájl-munkafolyamat súgófájlok

XML-alapú súgófájlokat, amelyek szerepelnek a modulok a parancsfájl-munkafolyamatok is dokumentálni. Nem vonatkoznak technikai követelmények a neve, a súgófájlt. Azonban ajánlott eljárás, hogy nevezze el a súgófájlban a parancsfájl modul, amely a parancsfájl-munkafolyamathoz definiálva van. Például:

```
<ScriptModule>.psm1-help.xml
```

Ellentétben más parancsfájlalapú parancsok parancsfájl-munkafolyamatokban nem szükséges egy `.ExternalHelp` kulcsszó használatával társíthatja azokat a súgófájlban megjegyzéseket. Ehelyett Windows PowerShell a felhasználói felület kulturális környezet-specifikus alkönyvtárát modul XML-alapú súgó fájlokat keres, és megkeresi az összes fájlt a parancsfájl-munkafolyamathoz tartozó súgó. `.ExternalHelp` Megjegyzés kulcsszót a rendszer figyelmen kívül hagyja.

Mivel a `.ExternalHelp` Megjegyzés kulcsszót a rendszer figyelmen kívül hagyja, a `Get-Help` parancsmag talál segítséget a parancsfájl-munkafolyamatokban csak akkor, ha a modulok szerepelnek.