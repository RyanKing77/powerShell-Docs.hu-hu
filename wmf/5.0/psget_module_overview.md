---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 9efc640dfda7e08e59d2c56746facd9658b1f9de
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2018
ms.locfileid: "34222173"
---
# <a name="powershell-module-discovery-install-and-inventory-with-powershellget"></a>PowerShell modul felderítési, telepítése és PowerShellGet készlethez

Ebben a kiadásban a WMF PowerShellGet tartalmazza:
-   Keresés-modul a modul metaadatai szűrheti az a – Tag paraméter
-   Keresés-modul szűrést végezhet a tárház vonatkozó keresést nyelvi paraméterrel - szűrő
-   Keresés-modul is szűrő alapján a modul tartalmának a - paranccsal - DscResource, és - paramétereket tartalmaz
-   Keresés – DscResource lehetővé teszi, hogy a tárolóhelyekkel egyes DSC erőforrásainak felderítése
-   A telepítés és a fájlmegosztások a NuGet közzétételi támogatása

## <a name="example-commands"></a>Példa parancsok
```powershell
\# Find all modules with tags Azure or DSC
Find-Module -Tag Azure, DSC

\# Find modules with a specific DscResource
Find-Module -DscResource xFirewall

\#Find modules with specific commands
Find-Module -Command Get-ScriptAnalyzerRule, Invoke-ScriptAnalyzer

\# Find all modules with Dsc resources
Find-Module -Includes DscResource

\# Find all modules with cmdlets
Find-Module -Includes Cmdlet

\# Find all modules with functions
Find-Module -Includes Function

\# Find all DSC resources
Find-DscResource

\# Find all DSC resources contained within a specific module
Find-DscResource -ModuleName xNetworking

\# Find all DSC resources in modules with DSCResourceKit or DesiredStateConfiguration
Find-DscResource -Tag DesiredStateConfiguration, DSCResourceKit

\# Find modules using -Filter parameter
\# Specified filter value is searched in Name and Description properties
Find-Module -Filter Cookbook -Repository PSGallery
Find-Module -Filter RBAC -Repository PSGallery
```

## <a name="new-features-in-powershellget"></a>Az PowerShellGet új funkciói
-   Egymás melletti verzióinak támogatása a Windows PowerShell 5.0-s vagy újabb
-   A modul függőségi telepítés támogatása
-   Három új parancsmagok
    -   Get-InstalledModule
    -   Távolítsa el modul
    -   Mentés-modul
