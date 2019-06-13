---
ms.date: 08/27/2018
keywords: PowerShell, a parancsmag
title: Objektumok tárolása változókban
ms.openlocfilehash: 2d20d84e48d3f68cab5c1ffa05d689b46415ebc8
ms.sourcegitcommit: a6f13c16a535acea279c0ddeca72f1f0d8a8ce4c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2019
ms.locfileid: "67030367"
---
# <a name="using-variables-to-store-objects"></a><span data-ttu-id="15e0b-103">Objektumok tárolása változókban</span><span class="sxs-lookup"><span data-stu-id="15e0b-103">Using variables to store objects</span></span>

<span data-ttu-id="15e0b-104">PowerShell-objektumok működik.</span><span class="sxs-lookup"><span data-stu-id="15e0b-104">PowerShell works with objects.</span></span> <span data-ttu-id="15e0b-105">PowerShell változók néven elnevezett objektumok létrehozását teszi lehetővé.</span><span class="sxs-lookup"><span data-stu-id="15e0b-105">PowerShell lets you create named objects known as variables.</span></span>
<span data-ttu-id="15e0b-106">Változónevek aláhúzásjel és bármely alfanumerikus karaktereket tartalmazhat.</span><span class="sxs-lookup"><span data-stu-id="15e0b-106">Variable names can include the underscore character and any alphanumeric characters.</span></span> <span data-ttu-id="15e0b-107">A PowerShell használatakor egy változó mindig használatával van megadva a \$ karakter követ a változó nevét.</span><span class="sxs-lookup"><span data-stu-id="15e0b-107">When used in PowerShell, a variable is always specified using the \$ character followed by variable name.</span></span>

## <a name="creating-a-variable"></a><span data-ttu-id="15e0b-108">Egy változó létrehozása</span><span class="sxs-lookup"><span data-stu-id="15e0b-108">Creating a variable</span></span>

<span data-ttu-id="15e0b-109">Írja be egy érvényes változónevet hozhat létre egy változót:</span><span class="sxs-lookup"><span data-stu-id="15e0b-109">You can create a variable by typing a valid variable name:</span></span>

```
PS> $loc
PS>
```

<span data-ttu-id="15e0b-110">Ebben a példában nincs eredményt adja vissza, mert `$loc` nincs értéke.</span><span class="sxs-lookup"><span data-stu-id="15e0b-110">This example returns no result because `$loc` doesn't have a value.</span></span> <span data-ttu-id="15e0b-111">Hozzon létre egy változót, és rendelje hozzá ugyanazt a lépésben egy értéket.</span><span class="sxs-lookup"><span data-stu-id="15e0b-111">You can create a variable and assign it a value in the same step.</span></span> <span data-ttu-id="15e0b-112">PowerShell csak a változót hoz létre, ha még nem létezik.</span><span class="sxs-lookup"><span data-stu-id="15e0b-112">PowerShell only creates the variable if it doesn't exist.</span></span>
<span data-ttu-id="15e0b-113">Ellenkező esetben a megadott értéket rendel a meglévő változókat.</span><span class="sxs-lookup"><span data-stu-id="15e0b-113">Otherwise, it assigns the specified value to the existing variable.</span></span> <span data-ttu-id="15e0b-114">Az alábbi példában az aktuális helyen tárolja a változó `$loc`:</span><span class="sxs-lookup"><span data-stu-id="15e0b-114">The following example stores the current location in the variable `$loc`:</span></span>

```powershell
$loc = Get-Location
```

<span data-ttu-id="15e0b-115">PowerShell semmilyen kimenet jeleníti meg, ha ezt a parancsot.</span><span class="sxs-lookup"><span data-stu-id="15e0b-115">PowerShell displays no output when you type this command.</span></span> <span data-ttu-id="15e0b-116">PowerShell Get-Location kimenete küld `$loc`.</span><span class="sxs-lookup"><span data-stu-id="15e0b-116">PowerShell sends the output of 'Get-Location' to `$loc`.</span></span> <span data-ttu-id="15e0b-117">A PowerShell nem hozzárendelt vagy átirányított adatokat küldeni a képernyő.</span><span class="sxs-lookup"><span data-stu-id="15e0b-117">In PowerShell, data that isn't assigned or redirected is sent to the screen.</span></span> <span data-ttu-id="15e0b-118">Írja be `$loc` az aktuális tartózkodási helyét jeleníti meg:</span><span class="sxs-lookup"><span data-stu-id="15e0b-118">Typing `$loc` shows your current location:</span></span>

```
PS> $loc

Path
----
C:\temp
```

<span data-ttu-id="15e0b-119">Használhat `Get-Member` a változók tartalma információit jeleníti meg.</span><span class="sxs-lookup"><span data-stu-id="15e0b-119">You can use `Get-Member` to display information about the contents of variables.</span></span> <span data-ttu-id="15e0b-120">`Get-Member` azt mutatja be, hogy `$loc` van egy **PathInfo** objektum, csakúgy, mint a kimenetét `Get-Location`:</span><span class="sxs-lookup"><span data-stu-id="15e0b-120">`Get-Member` shows you that `$loc` is a **PathInfo** object, just like the output from `Get-Location`:</span></span>

```powershell
PS> $loc | Get-Member -MemberType Property

   TypeName: System.Management.Automation.PathInfo

Name         MemberType Definition
----         ---------- ----------
Drive        Property   System.Management.Automation.PSDriveInfo Drive {get;}
Path         Property   System.String Path {get;}
Provider     Property   System.Management.Automation.ProviderInfo Provider {...
ProviderPath Property   System.String ProviderPath {get;}
```

## <a name="manipulating-variables"></a><span data-ttu-id="15e0b-121">Változók módosítása</span><span class="sxs-lookup"><span data-stu-id="15e0b-121">Manipulating variables</span></span>

<span data-ttu-id="15e0b-122">PowerShell segítségével kezelheti a változók különböző parancsokat biztosít.</span><span class="sxs-lookup"><span data-stu-id="15e0b-122">PowerShell provides several commands to manipulate variables.</span></span> <span data-ttu-id="15e0b-123">Egy olvasható formában felsorolását beírásával tekintheti meg:</span><span class="sxs-lookup"><span data-stu-id="15e0b-123">You can see a complete listing in a readable form by typing:</span></span>

```powershell
Get-Command -Noun Variable | Format-Table -Property Name,Definition -AutoSize -Wrap
```

<span data-ttu-id="15e0b-124">PowerShell számos, a rendszer által meghatározott változókat is létrehoz.</span><span class="sxs-lookup"><span data-stu-id="15e0b-124">PowerShell also creates several system-defined variables.</span></span> <span data-ttu-id="15e0b-125">Használhatja a `Remove-Variable` változók, amely PowerShell nem szabályozza, távolítsa el a jelenlegi munkamenet-parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="15e0b-125">You can use the `Remove-Variable` cmdlet to remove variables, which are not controlled by PowerShell, from the current session.</span></span> <span data-ttu-id="15e0b-126">Írja be a következő parancsot, törölje az összes változót:</span><span class="sxs-lookup"><span data-stu-id="15e0b-126">Type the following command to clear all variables:</span></span>

```powershell
Remove-Variable -Name * -Force -ErrorAction SilentlyContinue
```

<span data-ttu-id="15e0b-127">Az előző parancs futtatása után a `Get-Variable` parancsmag megjeleníti a PowerShell rendszerváltozók.</span><span class="sxs-lookup"><span data-stu-id="15e0b-127">After running the previous command, the `Get-Variable` cmdlet shows the PowerShell system variables.</span></span>

<span data-ttu-id="15e0b-128">PowerShell létrehoz egy változó meghajtó is.</span><span class="sxs-lookup"><span data-stu-id="15e0b-128">PowerShell also creates a variable drive.</span></span> <span data-ttu-id="15e0b-129">Az alábbi példa használatával megjelenítheti az összes PowerShell változók a változó meghajtót használja:</span><span class="sxs-lookup"><span data-stu-id="15e0b-129">Use the following example to display all PowerShell variables using the variable drive:</span></span>

```powershell
Get-ChildItem variable:
```

## <a name="using-cmdexe-variables"></a><span data-ttu-id="15e0b-130">A cmd.exe változók használata</span><span class="sxs-lookup"><span data-stu-id="15e0b-130">Using cmd.exe variables</span></span>

<span data-ttu-id="15e0b-131">PowerShell bármely Windows-folyamat számára elérhető azonos környezeti változókat is használhat, beleértve a **cmd.exe**.</span><span class="sxs-lookup"><span data-stu-id="15e0b-131">PowerShell can use the same environment variables available to any Windows process, including **cmd.exe**.</span></span> <span data-ttu-id="15e0b-132">Ezek a változók nevű meghajtó keresztül közzétett `env:`.</span><span class="sxs-lookup"><span data-stu-id="15e0b-132">These variables are exposed through a drive named `env:`.</span></span> <span data-ttu-id="15e0b-133">Ezek a változók a következő parancs beírásával tekintheti meg:</span><span class="sxs-lookup"><span data-stu-id="15e0b-133">You can view these variables by typing the following command:</span></span>

```powershell
Get-ChildItem env:
```

<span data-ttu-id="15e0b-134">A standard `*-Variable` parancsmagok nem tudja kezelni a környezeti változókat.</span><span class="sxs-lookup"><span data-stu-id="15e0b-134">The standard `*-Variable` cmdlets aren't designed to work with environment variables.</span></span> <span data-ttu-id="15e0b-135">A környezeti változók használatával elért a `env:` meghajtó előtag.</span><span class="sxs-lookup"><span data-stu-id="15e0b-135">Environment variables are accessed using the `env:` drive prefix.</span></span> <span data-ttu-id="15e0b-136">Például a **% SystemRoot %** változóját **cmd.exe** az operációs rendszer legfelső szintű könyvtár nevét tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="15e0b-136">For example, the **%SystemRoot%** variable in **cmd.exe** contains the operating system's root directory name.</span></span> <span data-ttu-id="15e0b-137">A PowerShellben használja `$env:SystemRoot` elérni ugyanazt az értéket.</span><span class="sxs-lookup"><span data-stu-id="15e0b-137">In PowerShell, you use `$env:SystemRoot` to access the same value.</span></span>

```
PS> $env:SystemRoot
C:\WINDOWS
```

<span data-ttu-id="15e0b-138">Is létrehozhat, és a Powershellen belülről a környezeti változók módosításához.</span><span class="sxs-lookup"><span data-stu-id="15e0b-138">You can also create and modify environment variables from within PowerShell.</span></span> <span data-ttu-id="15e0b-139">Környezeti változók a PowerShellben hajtsa végre a környezeti változókat az operációs rendszer máshol használja ugyanazokat a szabályokat.</span><span class="sxs-lookup"><span data-stu-id="15e0b-139">Environment variables in PowerShell follow the same rules for environment variables used elsewhere in the operating system.</span></span> <span data-ttu-id="15e0b-140">A következő példában létrehozunk egy új környezeti változót:</span><span class="sxs-lookup"><span data-stu-id="15e0b-140">The following example creates a new environment variable:</span></span>

```powershell
$env:LIB_PATH='/usr/local/lib'
```

<span data-ttu-id="15e0b-141">Bár nem kötelező, szokás a környezeti változók neve csupa nagybetűssé használatához.</span><span class="sxs-lookup"><span data-stu-id="15e0b-141">Though not required, it's common for environment variable names to use all uppercase letters.</span></span>
