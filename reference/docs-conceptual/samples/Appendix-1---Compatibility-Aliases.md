---
ms.date: 09/09/2019
keywords: PowerShell, parancsmag
title: '1\. függelék: Kompatibilitási aliasok'
ms.openlocfilehash: 2351fdf23711fe1417f7e3fc3cca5b642d5a59fc
ms.sourcegitcommit: 00083f07b13c73b86936e7d7307397df27c63c04
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/10/2019
ms.locfileid: "70848160"
---
# <a name="appendix-1---compatibility-aliases"></a><span data-ttu-id="75d36-103">1\. függelék – kompatibilitási aliasok</span><span class="sxs-lookup"><span data-stu-id="75d36-103">Appendix 1 - Compatibility Aliases</span></span>

<span data-ttu-id="75d36-104">A PowerShell több aliast is tartalmaz, amelyek lehetővé teszik a **UNIX** és a **cmd. exe** felhasználók számára ismerős parancsok használatát.</span><span class="sxs-lookup"><span data-stu-id="75d36-104">PowerShell has several aliases that allow **UNIX** and **cmd.exe** users to use familiar commands.</span></span>
<span data-ttu-id="75d36-105">A parancsok és a hozzájuk kapcsolódó PowerShell-parancsmagok és PowerShell-aliasok az alábbi táblázatban láthatók:</span><span class="sxs-lookup"><span data-stu-id="75d36-105">The commands and their related PowerShell cmdlet and PowerShell alias are shown in the following table:</span></span>

|<span data-ttu-id="75d36-106">cmd. exe parancs</span><span class="sxs-lookup"><span data-stu-id="75d36-106">cmd.exe command</span></span>|<span data-ttu-id="75d36-107">UNIX-parancs</span><span class="sxs-lookup"><span data-stu-id="75d36-107">UNIX command</span></span>|<span data-ttu-id="75d36-108">PowerShell-parancsmag</span><span class="sxs-lookup"><span data-stu-id="75d36-108">PowerShell cmdlet</span></span>|<span data-ttu-id="75d36-109">PowerShell-alias</span><span class="sxs-lookup"><span data-stu-id="75d36-109">PowerShell alias</span></span>|
|---------------|----------------|--------------|------------|
|<span data-ttu-id="75d36-110">**CLS**</span><span class="sxs-lookup"><span data-stu-id="75d36-110">**cls**</span></span>|<span data-ttu-id="75d36-111">**egyértelmű**</span><span class="sxs-lookup"><span data-stu-id="75d36-111">**clear**</span></span>|<span data-ttu-id="75d36-112">`Clear-Host`függvény</span><span class="sxs-lookup"><span data-stu-id="75d36-112">`Clear-Host` (function)</span></span>|`cls`|
|<span data-ttu-id="75d36-113">**másolja**</span><span class="sxs-lookup"><span data-stu-id="75d36-113">**copy**</span></span>|<span data-ttu-id="75d36-114">**CP**</span><span class="sxs-lookup"><span data-stu-id="75d36-114">**cp**</span></span>|`Copy-Item`|`cpi`|
|<span data-ttu-id="75d36-115">**dir**</span><span class="sxs-lookup"><span data-stu-id="75d36-115">**dir**</span></span>|<span data-ttu-id="75d36-116">**ls**</span><span class="sxs-lookup"><span data-stu-id="75d36-116">**ls**</span></span>|`Get-ChildItem`|`gci`|
|<span data-ttu-id="75d36-117">**type**</span><span class="sxs-lookup"><span data-stu-id="75d36-117">**type**</span></span>|<span data-ttu-id="75d36-118">**cat**</span><span class="sxs-lookup"><span data-stu-id="75d36-118">**cat**</span></span>|`Get-Content`|`gc`|
|<span data-ttu-id="75d36-119">**áthelyezése**</span><span class="sxs-lookup"><span data-stu-id="75d36-119">**move**</span></span>|<span data-ttu-id="75d36-120">**MV**</span><span class="sxs-lookup"><span data-stu-id="75d36-120">**mv**</span></span>|`Move-Item`|`mi`|
|<span data-ttu-id="75d36-121">**MD**</span><span class="sxs-lookup"><span data-stu-id="75d36-121">**md**</span></span>|<span data-ttu-id="75d36-122">**mkdir**</span><span class="sxs-lookup"><span data-stu-id="75d36-122">**mkdir**</span></span>|`New-Item`|`ni`|
|<span data-ttu-id="75d36-123">**pushd**</span><span class="sxs-lookup"><span data-stu-id="75d36-123">**pushd**</span></span>|<span data-ttu-id="75d36-124">**pushd**</span><span class="sxs-lookup"><span data-stu-id="75d36-124">**pushd**</span></span>|`Push-Location`|`pushd`|
|<span data-ttu-id="75d36-125">**popd**</span><span class="sxs-lookup"><span data-stu-id="75d36-125">**popd**</span></span>|<span data-ttu-id="75d36-126">**popd**</span><span class="sxs-lookup"><span data-stu-id="75d36-126">**popd**</span></span>|`Pop-Location`|`popd`|
|<span data-ttu-id="75d36-127">**del**, **Törlés**, **Rd**, **rmdir**</span><span class="sxs-lookup"><span data-stu-id="75d36-127">**del**, **erase**, **rd**, **rmdir**</span></span>|<span data-ttu-id="75d36-128">**RM**</span><span class="sxs-lookup"><span data-stu-id="75d36-128">**rm**</span></span>|`Remove-Item`|`ri`|
|<span data-ttu-id="75d36-129">**Ren**</span><span class="sxs-lookup"><span data-stu-id="75d36-129">**ren**</span></span>|<span data-ttu-id="75d36-130">**MV**</span><span class="sxs-lookup"><span data-stu-id="75d36-130">**mv**</span></span>|`Rename-Item`|`rni`|
|<span data-ttu-id="75d36-131">**CD**, **chdir**</span><span class="sxs-lookup"><span data-stu-id="75d36-131">**cd**, **chdir**</span></span>|<span data-ttu-id="75d36-132">**CD**</span><span class="sxs-lookup"><span data-stu-id="75d36-132">**cd**</span></span>|`Set-Location`|`sl`|

<span data-ttu-id="75d36-133">A PowerShell-aliasok megkereséséhez használja a [Get-alias](/powershell/module/Microsoft.PowerShell.Utility/Get-Alias) parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="75d36-133">To find the PowerShell aliases, use the [Get-Alias](/powershell/module/Microsoft.PowerShell.Utility/Get-Alias) cmdlet.</span></span> <span data-ttu-id="75d36-134">Egy parancsmag aliasnevének megjelenítéséhez használja a **definition** paramétert, és adja meg a parancsmag nevét.</span><span class="sxs-lookup"><span data-stu-id="75d36-134">To display a cmdlet's aliases, use the **Definition** parameter and specify the cmdlet name.</span></span>
<span data-ttu-id="75d36-135">Vagy az alias parancsmag nevének megkereséséhez használja a **Name** paramétert, és adja meg az aliast.</span><span class="sxs-lookup"><span data-stu-id="75d36-135">Or, to find an alias's cmdlet name, use the **Name** parameter and specify the alias.</span></span>

```powershell
Get-Alias -Definition Get-ChildItem
```

```Output
CommandType     Name
-----------     ----
Alias           dir -> Get-ChildItem
Alias           gci -> Get-ChildItem
Alias           ls -> Get-ChildItem
```

```powershell
Get-Alias -Name gci
```

```Output
CommandType     Name
-----------     ----
Alias           gci -> Get-ChildItem
```
