---
ms.date: 06/12/2017
contributor: manikb
ms.topic: reference
keywords: gyűjtemény, a powershell, a parancsmag, a psget
title: Távolítsa el modul
ms.openlocfilehash: 90f26e64a8a6bc95faf444b1d3ce82a8e3bbefc1
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="uninstall-module"></a>Távolítsa el modul

Eltávolítja a modult, amely PowerShellGet-parancsmagok használatával lett telepítve.

## <a name="description"></a>Leírás

Az Uninstall-modul a parancsmag eltávolítja a megadott modult a helyi számítógépről.
A modul nem távolítható el, ha néhány más modulok függőség van rajta.
Az Uninstall-modul parancsmagokkal azt is ellenőrzi, ha a modul eltávolítása folyamatban használatban, vagy nem. Hibát fog jelezni, ha a modul használatban van.

## <a name="cmdlet-syntax"></a>A parancsmag szintaxisa
```powershell
Get-Command -Name Uninstall-Module -Module PowerShellGet -Syntax
```

## <a name="cmdlet-online-help-reference"></a>A parancsmag online Súgó-hivatkozás

[Távolítsa el modul](http://go.microsoft.com/fwlink/?LinkId=526864)


## <a name="example-commands"></a>Példa parancsok

###  <a name="run-the-uninstall-module-cmdlet-to-uninstall-a-module-that-you-installed-by-using-powershellget"></a>Futtassa az Uninstall-modul parancsmagot egy modul, amely PowerShellGet segítségével telepített eltávolítása.
Ha bármely más modul attól függ, hogy a modul, amely a törölni kívánt, PowerShellGet hibát jelez.
```powershell
Get-InstalledModule -Name RequiredModule1 | Uninstall-Module

PackageManagement\Uninstall-Package : The module 'RequiredModule1' of version '2.5' in module base folder 'C:\Program Files\WindowsPowerShell\Modules\RequiredModule1\2.5' cannot be uninstalled, because one or more other modules 'ModuleWithDependencies2' are dependent on this module. Uninstall the modules that depend on this module before uninstalling module 'RequiredModule1'.
At C:\Program Files\WindowsPowerShell\Modules\PowerShellGet\PSGet.psm1:1303 char:25
+ ... $null = PackageManagement\\Uninstall-Package @PSBoundParameters
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
+ CategoryInfo : InvalidOperation: (Microsoft.Power...ninstallPackage:UninstallPackage) [Uninstall-Package], Exception
+ FullyQualifiedErrorId : UnableToUninstallAsOtherModulesNeedThisModule,Uninstall-Package,Microsoft.PowerShell.PackageManagement.Cmdlets.UninstallPackage
```

### <a name="uninstalling-a-module-when-some-other-modules-have-a-dependency-on-it"></a>A modul eltávolítása, ha néhány más modulok függőség rajta.

```powershell
Uninstall-Module SnippetPx

PackageManagement\Uninstall-Package : The module 'SnippetPx' of version '1.0.5.18' in module base folder 'C:\ProgramFiles\WindowsPowerShell\Modules\SnippetPx\1.0.5.18' cannot be uninstalled, because one or more other modules 'TypePx' are dependent on this module. Uninstall the modules that depend on this module before uninstalling module 'SnippetPx'.
At C:\Program Files\WindowsPowerShell\Modules\PowerShellGet\1.0.0.3\PSModule.psm1:1803 char:21
+ ...        $null = PackageManagement\Uninstall-Package @PSBoundParameters
+                    ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : InvalidOperation: (Microsoft.Power...ninstallPackage:UninstallPackage) [Uninstall-Packag
   e], Exception
    + FullyQualifiedErrorId : UnableToUninstallAsOtherModulesNeedThisModule,Uninstall-Package,Microsoft.PowerShell.Pac
   kageManagement.Cmdlets.UninstallPackage
```

### <a name="you-can-override-this-by-specify--force-option-on-uninstall-module-cmdlet"></a>Ez felülírható által meg az-Uninstall-modul a parancsmag a Force beállítás
**Megjegyzés:** ez nem ajánlott. Egyéb modulok a művelet megszakad.

```powershell
Uninstall-Module SnippetPx -Force
```

### <a name="uninstall-a-module-which-is-already-in-use"></a>Távolítsa el a modult, amely már használatban van

```powershell
Get-InstalledModule TypePx,SnippetPx

Version    Name                                Repository           Description
-------    ----                                ----------           -----------
2.0.1.20   TypePx                              PSGallery            The TypePx module adds properties and methods to...
1.0.5.18   SnippetPx                           PSGallery            The SnippetPx module enhances the snippet experi...
```

### <a name="uninstall-snippetpx-fails-due-to-the-dependent-module"></a>Távolítsa el a függő modul miatt SnippetPx sikertelen

```powershell
Uninstall-Module SnippetPx

PackageManagement\Uninstall-Package : The module 'SnippetPx' of version '1.0.5.18' in module base folder 'C:\Program
Files\WindowsPowerShell\Modules\SnippetPx\1.0.5.18' cannot be uninstalled, because one or more other modules 'TypePx'
are dependent on this module. Uninstall the modules that depend on this module before uninstalling module 'SnippetPx'.
At C:\Program Files\WindowsPowerShell\Modules\PowerShellGet\1.0.0.1\PSModule.psm1:1914 char:21
+ ...        $null = PackageManagement\Uninstall-Package @PSBoundParameters
+                    ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : InvalidOperation: (Microsoft.Power...ninstallPackage:UninstallPackage) [Uninstall-Packag
   e], Exception
    + FullyQualifiedErrorId : UnableToUninstallAsOtherModulesNeedThisModule,Uninstall-Package,Microsoft.PowerShell.Pac
   kageManagement.Cmdlets.UninstallPackage
```

### <a name="uninstall-typepx-then-uninstall-the-snippetpx"></a>Távolítsa el a TypePx, majd távolítsa el a SnippetPx

```powershell
Uninstall-Module TypePx
Uninstall-Module SnippetPx

WARNING: The version '1.0.5.18' of module 'SnippetPx' is currently in use. Retry the operation after closing the
applications.
PackageManagement\Uninstall-Package : Module 'SnippetPx' is in currently in use.
At C:\Program Files\WindowsPowerShell\Modules\PowerShellGet\1.0.0.1\PSModule.psm1:1914 char:21
+ ...        $null = PackageManagement\Uninstall-Package @PSBoundParameters
+                    ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : InvalidOperation: (Microsoft.Power...ninstallPackage:UninstallPackage) [Uninstall-Packag
   e], Exception
    + FullyQualifiedErrorId : ModuleIsInUse,Uninstall-Package,Microsoft.PowerShell.PackageManagement.Cmdlets.Uninstall
   Package
```


### <a name="for-a-module-name-which-is-not-installed-using-powershellget-cmdlets"></a>Az egy modul nevét, amelyen nincs telepítve a PowerShellGet-parancsmagok használatával

```powershell
Uninstall-Module SnipptPx

PackageManagement\Uninstall-Package : No match was found for the specified search criteria and module names 'SnipptPx'.
At C:\Program Files\WindowsPowerShell\Modules\PowerShellGet\1.0.0.1\PSModule.psm1:1914 char:21
+ ...        $null = PackageManagement\Uninstall-Package @PSBoundParameters
+                    ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : ObjectNotFound: (Microsoft.Power...ninstallPackage:UninstallPackage) [Uninstall-Package]
   , Exception
    + FullyQualifiedErrorId : NoMatchFound,Microsoft.PowerShell.PackageManagement.Cmdlets.UninstallPackage
```