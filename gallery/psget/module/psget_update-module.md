---
ms.date: 06/12/2017
contributor: manikb
ms.topic: reference
keywords: gyűjtemény, a powershell, a parancsmag, a psget
title: Update-Module
ms.openlocfilehash: 89b0111eda4421606843f108dca90519b2c9379e
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="update-module"></a>Update-Module

Letölti és telepíti a megadott modulokban legújabb verzióját, az online katalógusból a helyi számítógépre.

## <a name="description"></a>Leírás

A frissítés-modul a parancsmag telepíti egy Windows PowerShell-modul telepítése-modul a helyi számítógépen való futtatásával az online katalógusból telepített egy újabb verziója.

Alapértelmezés szerint a megadott modul érhető el az online gyűjtemény legújabb verziója telepítve van, kivéve ha megadja a szükséges verziót. Egy meglévő, telepített modul frissítéséhez a neve a modul; Frissítés-modul keres $env: a frissíteni kívánt modul PSModulePath.

A Name paraméter nélkül futtatja a frissítési-modul frissíti az összes modult a helyi számítógépen is lehet frissíteni.

### <a name="notes"></a>Megjegyzések

- Ez a parancsmag a Windows PowerShell 3.0-s vagy újabb kiadásaiban a Windows PowerShell, a Windows 7 vagy Windows 2008 R2 és újabb Windows-verziókat futtatja.
- Install-modullal nem telepítette a modult, amely a Name paramétert adja meg, ha hiba történik. Frissítés-modul által a telepítés-modulját az online katalógusból telepített modulok csak futtathatja.
- Ha frissítés-modul megpróbálja frissítési bináris fájljainak használt, a frissítés-modul, amely azonosítja a probléma folyamatokat, és értesíti a felhasználót, hogy a folyamat leállítása után próbálkozzon újra a frissítés-modul hibára tér vissza.
- PowerShell 5.0-s vagy újabb verziók amikor a frissítés-modul frissíti egy modult, hozzáadja a legújabb (vagy adott) verzióját a modul úgy, hogy a régebbi és az újabb verziója most-párhuzamos ugyanabban a könyvtárban. Tegyük fel például, és a kimeneti példát, ezek a parancsok megjelenítéséhez hasznos lenne.


## <a name="cmdlet-syntax"></a>A parancsmag szintaxisa
```powershell
Get-Command -Name Update-Module -Module PowerShellGet -Syntax
```

## <a name="cmdlet-online-help-reference"></a>A parancsmag online Súgó-hivatkozás

[Update-Module](http://go.microsoft.com/fwlink/?LinkID=398576)


## <a name="example-commands"></a>Példa parancsok

```powershell
PS C:\windows\system32> Update-Module -Name ContosoServer -RequiredVersion 1.5
PS C:\windows\system32> Get-Module -ListAvailable -Name ContosoServer | Format-List Name,Version,ModuleBase
Name : ContosoServer
Version : 2.0
ModuleBase : C:\Program Files\WindowsPowerShell\Modules\ContosoServer\2.0
Name : ContosoServer
Version : 1.5
ModuleBase : C:\Program Files\WindowsPowerShell\Modules\ContosoServer\1.5
Name : ContosoServer
Version : 1.0
ModuleBase : C:\Program Files\WindowsPowerShell\Modules\ContosoServer\1.0
PS C:\windows\system32> Get-InstalledModule
Version Name Repository Description
------- ---- ---------- -----------
1.0 ContosoServer MSPSGallery ContosoServer module
1.5 ContosoServer MSPSGallery ContosoServer module
2.0 ContosoServer MSPSGallery ContosoServer module
PS C:\windows\system32> Update-Module -Name ContosoServer
PS C:\windows\system32> Get-Module -ListAvailable -Name ContosoServer | Format-List Name,Version,ModuleBase
Name : ContosoServer
Version : 2.8.1
ModuleBase : C:\Program Files\WindowsPowerShell\Modules\ContosoServer\2.8.1
Name : ContosoServer
Version : 2.0
ModuleBase : C:\Program Files\WindowsPowerShell\Modules\ContosoServer\2.0
Name : ContosoServer
Version : 1.5
ModuleBase : C:\Program Files\WindowsPowerShell\Modules\ContosoServer\1.5
Name : ContosoServer
Version : 1.0
ModuleBase : C:\Program Files\WindowsPowerShell\Modules\ContosoServer\1.0
PS C:\windows\system32> Get-InstalledModule
Version Name Repository Description
------- ---- ---------- -----------
1.0 ContosoServer MSPSGallery ContosoServer module
1.5 ContosoServer MSPSGallery ContosoServer module
2.0 ContosoServer MSPSGallery ContosoServer module
2.8.1 ContosoServer MSPSGallery ContosoServer module
```

### <a name="update-the-module-with-a-prerelease-version-requires--allowprerelease-flag"></a>A modul előzetes verziójával frissíti, - AllowPrerelease jelző igényel
```powershell
PS C:\windows\system32> Get-InstalledModule
Version Name Repository Description
------- ---- ---------- -----------
1.0 ContosoServer MSPSGallery ContosoServer module
1.5 ContosoServer MSPSGallery ContosoServer module
2.0 ContosoServer MSPSGallery ContosoServer module
2.8.1 ContosoServer MSPSGallery ContosoServer module

PS C:\windows\system32> Find-Module ContosoServer -AllowPrerelease

Version        Name                                Repository           Description
-------        ----                                ----------           -----------
3.0.0-alpha    ConstosoServer                      MSPSGallery          The PowerShell Contoso Server deployment tools...

PS C:\windows\system32> Update-Module -Name ContosoServer -AllowPrerelease
PS C:\windows\system32> Get-InstalledModule
Version Name Repository Description
------- ---- ---------- -----------
1.0 ContosoServer MSPSGallery ContosoServer module
1.5 ContosoServer MSPSGallery ContosoServer module
2.0 ContosoServer MSPSGallery ContosoServer module
2.8.1 ContosoServer MSPSGallery ContosoServer module
3.0.0-alpha ContosoServer MSPSGallery ContosoServer module

```


### <a name="update-the-testdepwithnestedrequiredmodules1-module-with-dependencies"></a>Frissítse a TestDepWithNestedRequiredModules1 modul függőségek.
```powershell
Find-Module -Name TestDepWithNestedRequiredModules1 -Repository LocalRepo -AllVersions

Version    Name                                Repository  Description
-------    ----                                ----------  -----------
1.0        TestDepWithNestedRequiredModules1   LocalRepo   TestDepWithNestedRequiredModules1 module
2.0        TestDepWithNestedRequiredModules1   LocalRepo   TestDepWithNestedRequiredModules1 module

Update-Module -Name TestDepWithNestedRequiredModules1 -RequiredVersion 2.0
Get-InstalledModule

Version    Name                                Repository  Description
-------    ----                                ----------  -----------
1.0        NestedRequiredModule1               LocalRepo   NestedRequiredModule1 module
2.5        NestedRequiredModule2               LocalRepo   NestedRequiredModule2 module
2.0        NestedRequiredModule3               LocalRepo   NestedRequiredModule3 module
2.5        NestedRequiredModule3               LocalRepo   NestedRequiredModule3 module
1.0        RequiredModule1                     LocalRepo   RequiredModule1 module
2.5        RequiredModule2                     LocalRepo   RequiredModule2 module
2.0        RequiredModule3                     LocalRepo   RequiredModule3 module
2.5        RequiredModule3                     LocalRepo   RequiredModule3 module
1.0        TestDepWithNestedRequiredModules1   LocalRepo   TestDepWithNestedRequiredModules1 module
2.0        TestDepWithNestedRequiredModules1   LocalRepo   TestDepWithNestedRequiredModules1 module



```