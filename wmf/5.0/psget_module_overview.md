---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: a0b1573611c5d4232082c19ca19b4cca79d0699e
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62057468"
---
# <a name="powershell-module-discovery-install-and-inventory-with-powershellget"></a>PowerShell-modulok felderítése, telepítése és Leltárazása a powershellgettel

A PowerShellGet ebben a kiadásban a WMF tartalmazza:
-   Modul metaadatainak szűrésével find-Module-a - Tag paraméter
-   Tárház-specifikus keresési nyelv szűrésével find-Module-a - Filter paraméter
-   Find-Module is szűrés annak alapján, a modul tartalmának a - paranccsal, - DscResource, és - paramétereket
-   Find-DscResource lehetővé teszi, hogy az egyes DSC-erőforrások tárházakban
-   A telepítés és NuGet fájlmegosztások közzétételét támogatása

## <a name="example-commands"></a>Példaparancsok
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

## <a name="new-features-in-powershellget"></a>A PowerShellGet az új funkciói
-   Egymás melletti verzió támogatása a Windows PowerShell 5.0-s vagy újabb
-   A modul függőséget telepítés támogatása
-   Három új parancsmagok
    -   Get-InstalledModule
    -   Uninstall-Module
    -   Save-Module
