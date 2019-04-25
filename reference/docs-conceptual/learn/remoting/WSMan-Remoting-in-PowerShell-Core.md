---
title: WS-Management (WSMan) távoli eljáráshívás a PowerShell Core-ban
description: Távoli eljáráshívás a PowerShell Core-t a wsman által használt
ms.date: 08/06/2018
ms.openlocfilehash: e5f00128bc8ebc1b432cc77a5896a9e09d684109
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62058879"
---
# <a name="ws-management-wsman-remoting-in-powershell-core"></a><span data-ttu-id="91d81-103">WS-Management (WSMan) távoli eljáráshívás a PowerShell Core-ban</span><span class="sxs-lookup"><span data-stu-id="91d81-103">WS-Management (WSMan) Remoting in PowerShell Core</span></span>

## <a name="instructions-to-create-a-remoting-endpoint"></a><span data-ttu-id="91d81-104">A távoli eljáráshívás végpont létrehozására vonatkozó utasításokat</span><span class="sxs-lookup"><span data-stu-id="91d81-104">Instructions to Create a Remoting Endpoint</span></span>

<span data-ttu-id="91d81-105">A Windows PowerShell Core csomag tartalmaz egy beépülő modul WinRM (`pwrshplugin.dll`) és a egy telepítési szkript (`Install-PowerShellRemoting.ps1`) a `$PSHome`.</span><span class="sxs-lookup"><span data-stu-id="91d81-105">The PowerShell Core package for Windows includes a WinRM plug-in (`pwrshplugin.dll`) and an installation script (`Install-PowerShellRemoting.ps1`) in `$PSHome`.</span></span>
<span data-ttu-id="91d81-106">Ezek a fájlok PowerShell bejövő távoli PowerShell-kapcsolatok fogadására, ha meg van adva a végpont engedélyezése.</span><span class="sxs-lookup"><span data-stu-id="91d81-106">These files enable PowerShell to accept incoming PowerShell remote connections when its endpoint is specified.</span></span>

### <a name="motivation"></a><span data-ttu-id="91d81-107">Motiváció</span><span class="sxs-lookup"><span data-stu-id="91d81-107">Motivation</span></span>

<span data-ttu-id="91d81-108">Telepíteni kell a PowerShell távoli számítógépekről, amelyek a PowerShell-munkameneteket hozhat létre `New-PSSession` és `Enter-PSSession`.</span><span class="sxs-lookup"><span data-stu-id="91d81-108">An installation of PowerShell can establish PowerShell sessions to remote computers using `New-PSSession` and `Enter-PSSession`.</span></span>
<span data-ttu-id="91d81-109">A felhasználó engedélyezi a bejövő távoli PowerShell-kapcsolatok fogadására, egy WinRM távoli eljáráshívás végpontot kell létrehoznia.</span><span class="sxs-lookup"><span data-stu-id="91d81-109">To enable it to accept incoming PowerShell remote connections, the user must create a WinRM remoting endpoint.</span></span>
<span data-ttu-id="91d81-110">Ez az egy explicit vehetnek részt a forgatókönyvben, a felhasználó futtatja a telepítés-PowerShellRemoting.ps1 a WinRM-végpont létrehozása.</span><span class="sxs-lookup"><span data-stu-id="91d81-110">This is an explicit opt-in scenario where the user runs Install-PowerShellRemoting.ps1 to create the WinRM endpoint.</span></span>
<span data-ttu-id="91d81-111">A telepítési parancsfájl egy rövid távú megoldást, a további funkciók még nem `Enable-PSRemoting` ugyanaz a művelet végrehajtásához.</span><span class="sxs-lookup"><span data-stu-id="91d81-111">The installation script is a short-term solution until we add additional functionality to `Enable-PSRemoting` to perform the same action.</span></span>
<span data-ttu-id="91d81-112">További részletekért tekintse meg a probléma [#1193](https://github.com/PowerShell/PowerShell/issues/1193).</span><span class="sxs-lookup"><span data-stu-id="91d81-112">For more details, please see issue [#1193](https://github.com/PowerShell/PowerShell/issues/1193).</span></span>

### <a name="script-actions"></a><span data-ttu-id="91d81-113">A Parancsfájlműveletek</span><span class="sxs-lookup"><span data-stu-id="91d81-113">Script Actions</span></span>

<span data-ttu-id="91d81-114">A parancsfájl</span><span class="sxs-lookup"><span data-stu-id="91d81-114">The script</span></span>

1. <span data-ttu-id="91d81-115">Létrehoz egy könyvtárat a beépülő modulhoz belül `$env:windir\System32\PowerShell`</span><span class="sxs-lookup"><span data-stu-id="91d81-115">Creates a directory for the plug-in within `$env:windir\System32\PowerShell`</span></span>
1. <span data-ttu-id="91d81-116">Másolja át a pwrshplugin.dll adott helyhez</span><span class="sxs-lookup"><span data-stu-id="91d81-116">Copies pwrshplugin.dll to that location</span></span>
1. <span data-ttu-id="91d81-117">Egy konfigurációs fájlt hoz létre</span><span class="sxs-lookup"><span data-stu-id="91d81-117">Generates a configuration file</span></span>
1. <span data-ttu-id="91d81-118">Regisztrál, hogy beépülő modul a Rendszerfelügyeleti webszolgáltatások</span><span class="sxs-lookup"><span data-stu-id="91d81-118">Registers that plug-in with WinRM</span></span>

### <a name="registration"></a><span data-ttu-id="91d81-119">Regisztráció</span><span class="sxs-lookup"><span data-stu-id="91d81-119">Registration</span></span>

<span data-ttu-id="91d81-120">A szkript egy rendszergazdai PowerShell-munkamenetet, és két módban fut belül kell végrehajtani.</span><span class="sxs-lookup"><span data-stu-id="91d81-120">The script must be executed within an Administrator-level PowerShell session and runs in two modes.</span></span>

#### <a name="executed-by-the-instance-of-powershell-that-it-will-register"></a><span data-ttu-id="91d81-121">PowerShell parancsmag, amely, regisztrálja az példány által végrehajtott</span><span class="sxs-lookup"><span data-stu-id="91d81-121">Executed by the instance of PowerShell that it will register</span></span>

```powershell
Install-PowerShellRemoting.ps1
```

#### <a name="executed-by-another-instance-of-powershell-on-behalf-of-the-instance-that-it-will-register"></a><span data-ttu-id="91d81-122">Egy másik példánya PowerShell nevében, regisztrálja az adott példány által végrehajtott</span><span class="sxs-lookup"><span data-stu-id="91d81-122">Executed by another instance of PowerShell on behalf of the instance that it will register</span></span>

```powershell
<path to powershell>\Install-PowerShellRemoting.ps1 -PowerShellHome "<absolute path to the instance's $PSHOME>"
```

<span data-ttu-id="91d81-123">Példa:</span><span class="sxs-lookup"><span data-stu-id="91d81-123">For Example:</span></span>

```powershell
Set-Location -Path 'C:\Program Files\PowerShell\6.0.0\'
.\Install-PowerShellRemoting.ps1 -PowerShellHome "C:\Program Files\PowerShell\6.0.0\"
```

<span data-ttu-id="91d81-124">**MEGJEGYZÉS:** A távoli eljáráshívás regisztrációs parancsfájl újraindul a Rendszerfelügyeleti webszolgáltatások, így az összes meglévő PSRP munkamenet befejeződik, azonnal a szkript futtatása után.</span><span class="sxs-lookup"><span data-stu-id="91d81-124">**NOTE:** The remoting registration script will restart WinRM, so all existing PSRP sessions will terminate immediately after the script is run.</span></span> <span data-ttu-id="91d81-125">Ha egy távoli munkamenet közben fut, ez a kapcsolat le fog állni.</span><span class="sxs-lookup"><span data-stu-id="91d81-125">If run during a remote session, this will terminate the connection.</span></span>

## <a name="how-to-connect-to-the-new-endpoint"></a><span data-ttu-id="91d81-126">Hogyan lehet csatlakozni az új végpont</span><span class="sxs-lookup"><span data-stu-id="91d81-126">How to Connect to the New Endpoint</span></span>

<span data-ttu-id="91d81-127">Hozzon létre egy PowerShell-munkamenetet az új PowerShell-végpont megadásával `-ConfigurationName "some endpoint name"`.</span><span class="sxs-lookup"><span data-stu-id="91d81-127">Create a PowerShell session to the new PowerShell endpoint by specifying `-ConfigurationName "some endpoint name"`.</span></span> <span data-ttu-id="91d81-128">Ha csatlakozni szeretne a PowerShell-példány a fenti példában, vagy használja:</span><span class="sxs-lookup"><span data-stu-id="91d81-128">To connect to the PowerShell instance from the example above, use either:</span></span>

```powershell
New-PSSession ... -ConfigurationName "powershell.6.0.0"
Enter-PSSession ... -ConfigurationName "powershell.6.0.0"
```

<span data-ttu-id="91d81-129">Vegye figyelembe, hogy `New-PSSession` és `Enter-PSSession` meghívásához, amely nem ad meg `-ConfigurationName` az alapértelmezett PowerShell végpont által megcélzott `microsoft.powershell`.</span><span class="sxs-lookup"><span data-stu-id="91d81-129">Note that `New-PSSession` and `Enter-PSSession` invocations that do not specify `-ConfigurationName` will target the default PowerShell endpoint, `microsoft.powershell`.</span></span>