---
ms.date: 2017-06-12
contributor: manikb
ms.topic: reference
keywords: "gyűjtemény, a powershell, a parancsmag, a psget"
title: "Frissítés-modul"
ms.openlocfilehash: 66535cd5b1f44e108c2bc47fa343c77c86bb21dc
ms.sourcegitcommit: 58371abe9db4b9a0e4e1eb82d39a9f9e187355f9
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/05/2017
---
# <a name="update-module"></a><span data-ttu-id="0268a-103">Frissítés-modul</span><span class="sxs-lookup"><span data-stu-id="0268a-103">Update-Module</span></span>

<span data-ttu-id="0268a-104">Letölti és telepíti a megadott modulokban legújabb verzióját, az online katalógusból a helyi számítógépre.</span><span class="sxs-lookup"><span data-stu-id="0268a-104">Downloads and installs the newest version of specified modules from an online gallery to the local computer.</span></span>

## <a name="description"></a><span data-ttu-id="0268a-105">Leírás</span><span class="sxs-lookup"><span data-stu-id="0268a-105">Description</span></span>

<span data-ttu-id="0268a-106">A frissítés-modul a parancsmag telepíti egy Windows PowerShell-modul telepítése-modul a helyi számítógépen való futtatásával az online katalógusból telepített egy újabb verziója.</span><span class="sxs-lookup"><span data-stu-id="0268a-106">The Update-Module cmdlet installs a newer version of a Windows PowerShell module that was installed from the online gallery by running Install-Module on the local computer.</span></span>

<span data-ttu-id="0268a-107">Alapértelmezés szerint a megadott modul érhető el az online gyűjtemény legújabb verziója telepítve van, kivéve ha megadja a szükséges verziót.</span><span class="sxs-lookup"><span data-stu-id="0268a-107">By default, the newest version of the specified module available in online gallery is installed, unless you specify a required version.</span></span> <span data-ttu-id="0268a-108">Egy meglévő, telepített modul frissítéséhez a neve a modul; Frissítés-modul keres $env: a frissíteni kívánt modul PSModulePath.</span><span class="sxs-lookup"><span data-stu-id="0268a-108">You can update an existing, installed module by specifying the name of the module; Update-Module searches $env:PSModulePath for the module that you want to update.</span></span>

<span data-ttu-id="0268a-109">A Name paraméter nélkül futtatja a frissítési-modul frissíti az összes modult a helyi számítógépen is lehet frissíteni.</span><span class="sxs-lookup"><span data-stu-id="0268a-109">Running Update-Module without the Name parameter updates all modules that can be updated on the local computer.</span></span>

### <a name="notes"></a><span data-ttu-id="0268a-110">Megjegyzések</span><span class="sxs-lookup"><span data-stu-id="0268a-110">Notes</span></span>

- <span data-ttu-id="0268a-111">Ez a parancsmag a Windows PowerShell 3.0-s vagy újabb kiadásaiban a Windows PowerShell, a Windows 7 vagy Windows 2008 R2 és újabb Windows-verziókat futtatja.</span><span class="sxs-lookup"><span data-stu-id="0268a-111">This cmdlet runs on Windows PowerShell 3.0 or later releases of Windows PowerShell, on Windows 7 or Windows 2008 R2 and later releases of Windows.</span></span>
- <span data-ttu-id="0268a-112">Install-modullal nem telepítette a modult, amely a Name paramétert adja meg, ha hiba történik.</span><span class="sxs-lookup"><span data-stu-id="0268a-112">If the module that you specify with the Name parameter was not installed by using Install-Module, an error occurs.</span></span> <span data-ttu-id="0268a-113">Frissítés-modul által a telepítés-modulját az online katalógusból telepített modulok csak futtathatja.</span><span class="sxs-lookup"><span data-stu-id="0268a-113">You can only run Update-Module on modules that you installed from the online gallery by running Install-Module.</span></span>
- <span data-ttu-id="0268a-114">Ha frissítés-modul megpróbálja frissítési bináris fájljainak használt, a frissítés-modul, amely azonosítja a probléma folyamatokat, és értesíti a felhasználót, hogy a folyamat leállítása után próbálkozzon újra a frissítés-modul hibára tér vissza.</span><span class="sxs-lookup"><span data-stu-id="0268a-114">If Update-Module attempts to update binaries that are in use, Update-Module returns an error that identifies the problem processes, and informs the user to retry Update-Module after stopping the processes.</span></span>
- <span data-ttu-id="0268a-115">PowerShell 5.0-s vagy újabb verziók amikor a frissítés-modul frissíti egy modult, hozzáadja a legújabb (vagy adott) verzióját a modul úgy, hogy a régebbi és az újabb verziója most-párhuzamos ugyanabban a könyvtárban.</span><span class="sxs-lookup"><span data-stu-id="0268a-115">On PowerShell 5.0 or newer versions, when Update-Module updates a module, it adds the latest (or specified) version of the module, so the older and newer versions are now side-by-side in the same directory.</span></span> <span data-ttu-id="0268a-116">Tegyük fel például, és a kimeneti példát, ezek a parancsok megjelenítéséhez hasznos lenne.</span><span class="sxs-lookup"><span data-stu-id="0268a-116">It would be useful to say so and to show an example of the output from these commands.</span></span>


## <a name="cmdlet-syntax"></a><span data-ttu-id="0268a-117">A parancsmag szintaxisa</span><span class="sxs-lookup"><span data-stu-id="0268a-117">Cmdlet syntax</span></span>
```powershell
Get-Command -Name Update-Module -Module PowerShellGet -Syntax
```

## <a name="cmdlet-online-help-reference"></a><span data-ttu-id="0268a-118">A parancsmag online Súgó-hivatkozás</span><span class="sxs-lookup"><span data-stu-id="0268a-118">Cmdlet online help reference</span></span>

[<span data-ttu-id="0268a-119">Frissítés-modul</span><span class="sxs-lookup"><span data-stu-id="0268a-119">Update-Module</span></span>](http://go.microsoft.com/fwlink/?LinkID=398576)


## <a name="example-commands"></a><span data-ttu-id="0268a-120">Példa parancsok</span><span class="sxs-lookup"><span data-stu-id="0268a-120">Example commands</span></span>

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

### <a name="update-the-module-with-a-prerelease-version-requires--allowprerelease-flag"></a><span data-ttu-id="0268a-121">A modul előzetes verziójával frissíti, - AllowPrerelease jelző igényel</span><span class="sxs-lookup"><span data-stu-id="0268a-121">Update the module with a prerelease version, requires -AllowPrerelease flag</span></span>
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


### <a name="update-the-testdepwithnestedrequiredmodules1-module-with-dependencies"></a><span data-ttu-id="0268a-122">Frissítse a TestDepWithNestedRequiredModules1 modul függőségek.</span><span class="sxs-lookup"><span data-stu-id="0268a-122">Update the TestDepWithNestedRequiredModules1 module with dependencies.</span></span>
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

