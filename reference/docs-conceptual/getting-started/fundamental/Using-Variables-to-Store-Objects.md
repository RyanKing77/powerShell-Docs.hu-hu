---
ms.date: 2017-06-05
keywords: PowerShell parancsmag
title: "Tárolási objektumok változók használata"
ms.assetid: b1688d73-c173-491e-9ba6-6d0c1cc852de
ms.openlocfilehash: 9a95d421fa2686608a565987c16fecc41c3c6d20
ms.sourcegitcommit: f069ff0689006fece768f178c10e3e3eeaee09f0
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/13/2017
---
# <a name="using-variables-to-store-objects"></a><span data-ttu-id="b0907-103">Tárolási objektumok változók használata</span><span class="sxs-lookup"><span data-stu-id="b0907-103">Using Variables to Store Objects</span></span>
<span data-ttu-id="b0907-104">PowerShell objektumok működik.</span><span class="sxs-lookup"><span data-stu-id="b0907-104">PowerShell works with objects.</span></span> <span data-ttu-id="b0907-105">PowerShell lehetővé teszi változók, alapvetően az objektumok megőrizni későbbi felhasználásra kimeneti nevű létrehozását.</span><span class="sxs-lookup"><span data-stu-id="b0907-105">PowerShell lets you create variables, essentially named objects, to preserve output for later use.</span></span> <span data-ttu-id="b0907-106">Más változók használata esetén ismertetése ne feledje, hogy PowerShell változók objektumokat, nem szöveges.</span><span class="sxs-lookup"><span data-stu-id="b0907-106">If you are used to working with variables in other shells remember that PowerShell variables are objects, not text.</span></span>

<span data-ttu-id="b0907-107">Változók mindig vannak-e megadva, a kezdeti karakter $, és a alfanumerikus karaktereket vagy a aláhúzásjellel is tartalmazhat, a név.</span><span class="sxs-lookup"><span data-stu-id="b0907-107">Variables are always specified with the initial character $, and can include any alphanumeric characters or the underscore in their names.</span></span>

### <a name="creating-a-variable"></a><span data-ttu-id="b0907-108">Egy változó létrehozása</span><span class="sxs-lookup"><span data-stu-id="b0907-108">Creating a Variable</span></span>
<span data-ttu-id="b0907-109">Írja be egy érvényes változónevet hozhat létre egy változót:</span><span class="sxs-lookup"><span data-stu-id="b0907-109">You can create a variable by typing a valid variable name:</span></span>

```
PS> $loc
PS>
```

<span data-ttu-id="b0907-110">Ez eredményt adja vissza, nem mert **$loc** rendelkezik értékkel.</span><span class="sxs-lookup"><span data-stu-id="b0907-110">This returns no result because **$loc** does not have a value.</span></span> <span data-ttu-id="b0907-111">Hozzon létre egy változót, és rendelje hozzá az azonos lépésben értéket.</span><span class="sxs-lookup"><span data-stu-id="b0907-111">You can create a variable and assign it a value in the same step.</span></span> <span data-ttu-id="b0907-112">PowerShell csak létrehozza a változót, ha nem létezik. Ellenkező esetben a megadott érték rendel a létező változó.</span><span class="sxs-lookup"><span data-stu-id="b0907-112">PowerShell only creates the variable if it does not exist; otherwise, it assigns the specified value to the existing variable.</span></span> <span data-ttu-id="b0907-113">Az aktuális helyen tárolja a változóban **$loc**, típus:</span><span class="sxs-lookup"><span data-stu-id="b0907-113">To store your current location in the variable **$loc**, type:</span></span>

```
$loc = Get-Location
```

<span data-ttu-id="b0907-114">Nem jelenik meg ez a parancs beírásakor, mert a kimeneti $helyi küld kimeneti van</span><span class="sxs-lookup"><span data-stu-id="b0907-114">There is no output displayed when you type this command because the output is sent to $loc.</span></span> <span data-ttu-id="b0907-115">A PowerShellben megjelenített eredménye az, hogy az adatokat, amely nem egyéb irányítva, mindig küldi el a képernyőre egyik mellékhatása.</span><span class="sxs-lookup"><span data-stu-id="b0907-115">In PowerShell, displayed output is a side effect of the fact that data, which is not otherwise directed, always gets sent to the screen.</span></span> <span data-ttu-id="b0907-116">Írja be a $loc megjeleníti az aktuális hely:</span><span class="sxs-lookup"><span data-stu-id="b0907-116">Typing $loc will show your current location:</span></span>

```
PS> $loc

Path
----
C:\temp
```

<span data-ttu-id="b0907-117">Használhat **Get-tag** változók tartalma kapcsolatos információk megjelenítéséhez.</span><span class="sxs-lookup"><span data-stu-id="b0907-117">You can use **Get-Member** to display information about the contents of variables.</span></span> <span data-ttu-id="b0907-118">A Get-tag $loc ismertetett láthatja, hogy a rendszer egy **PathInfo** objektum, csakúgy, mint a kimenet a Get-helyről:</span><span class="sxs-lookup"><span data-stu-id="b0907-118">Piping $loc to Get-Member will show you that it is a **PathInfo** object, just like the output from Get-Location:</span></span>

```
PS> $loc | Get-Member -MemberType Property

   TypeName: System.Management.Automation.PathInfo

Name         MemberType Definition
----         ---------- ----------
Drive        Property   System.Management.Automation.PSDriveInfo Drive {get;}
Path         Property   System.String Path {get;}
Provider     Property   System.Management.Automation.ProviderInfo Provider {...
ProviderPath Property   System.String ProviderPath {get;}
```

### <a name="manipulating-variables"></a><span data-ttu-id="b0907-119">Változók módosítása</span><span class="sxs-lookup"><span data-stu-id="b0907-119">Manipulating Variables</span></span>
<span data-ttu-id="b0907-120">PowerShell biztosít több parancsok, változók módosítására.</span><span class="sxs-lookup"><span data-stu-id="b0907-120">PowerShell provides several commands to manipulate variables.</span></span> <span data-ttu-id="b0907-121">Írja be a teljes listáját a olvasható formában látható:</span><span class="sxs-lookup"><span data-stu-id="b0907-121">You can see a complete listing in a readable form by typing:</span></span>

```
Get-Command -Noun Variable | Format-Table -Property Name,Definition -AutoSize -Wrap
```

<span data-ttu-id="b0907-122">A változók hoz létre az aktuális PowerShell-munkamenetben kívül több rendszer által definiált változókat.</span><span class="sxs-lookup"><span data-stu-id="b0907-122">In addition to the variables you create in your current PowerShell session, there are several system-defined variables.</span></span> <span data-ttu-id="b0907-123">Használhatja a **Remove-változó** parancsmag segítségével törölje a jelet a változókat, amelyek nem szabályozzák PowerShell kijelentkezik.</span><span class="sxs-lookup"><span data-stu-id="b0907-123">You can use the **Remove-Variable** cmdlet to clear out all of the variables which are not controlled by PowerShell.</span></span> <span data-ttu-id="b0907-124">Írja be a következő parancs futtatásával törölje az összes változó:</span><span class="sxs-lookup"><span data-stu-id="b0907-124">Type the following command to clear all variables:</span></span>

```
Remove-Variable -Name * -Force -ErrorAction SilentlyContinue
```

<span data-ttu-id="b0907-125">Ez a művelet létrehoz a megerősítést kérő alább látható.</span><span class="sxs-lookup"><span data-stu-id="b0907-125">This will produce the confirmation prompt you see below.</span></span>

```
Confirm
Are you sure you want to perform this action?
Performing operation "Remove Variable" on Target "Name: Error".
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help
(default is "Y"):A
```

<span data-ttu-id="b0907-126">Ha ezután futtatja a **Get-Variable** parancsmag, látni fogja a fennmaradó PowerShell változókat.</span><span class="sxs-lookup"><span data-stu-id="b0907-126">If you then run the **Get-Variable** cmdlet, you will see the remaining PowerShell variables.</span></span> <span data-ttu-id="b0907-127">Egy változó PowerShell meghajtó is van, mivel emellett megjeleníthetők összes PowerShell változók beírásával:</span><span class="sxs-lookup"><span data-stu-id="b0907-127">Since there is also a variable PowerShell drive, you can also display all PowerShell variables by typing:</span></span>

```
Get-ChildItem variable:
```

### <a name="using-cmdexe-variables"></a><span data-ttu-id="b0907-128">Cmd.exe változók használata</span><span class="sxs-lookup"><span data-stu-id="b0907-128">Using Cmd.exe Variables</span></span>
<span data-ttu-id="b0907-129">PowerShell, de nem Cmd.exe parancs-rendszerhéj környezetben fut, és minden környezetben elérhető azonos változókat is használhat, a Windows.</span><span class="sxs-lookup"><span data-stu-id="b0907-129">Although PowerShell is not Cmd.exe, it runs in a command shell environment and can use the same variables available in any environment in Windows.</span></span> <span data-ttu-id="b0907-130">Ezek a változók egy meghajtón keresztül közzétett **env**:.</span><span class="sxs-lookup"><span data-stu-id="b0907-130">These variables are exposed through a drive named **env**:.</span></span> <span data-ttu-id="b0907-131">Ezek a változók beírásával tekintheti meg:</span><span class="sxs-lookup"><span data-stu-id="b0907-131">You can view these variables by typing:</span></span>

```
Get-ChildItem env:
```

<span data-ttu-id="b0907-132">Bár a szabványos változó parancsmagok vannak nem tudja kezelni a **env:** változók, továbbra is használhatja őket megadásával a **env:** előtag.</span><span class="sxs-lookup"><span data-stu-id="b0907-132">Although the standard variable cmdlets are not designed to work with **env:** variables, you can still use them by specifying the **env:** prefix.</span></span> <span data-ttu-id="b0907-133">Például az operációs rendszer gyökérkönyvtárában megtekintéséhez használhatja a parancs-rendszerhéj **% SystemRoot %** belül PowerShell írja be a változót:</span><span class="sxs-lookup"><span data-stu-id="b0907-133">For example, to see the operating system root directory, you can use the command-shell **%SystemRoot%** variable from within PowerShell by typing:</span></span>

```
PS> $env:SystemRoot
C:\WINDOWS
```

<span data-ttu-id="b0907-134">Hozhat létre, és PowerShell belül a környezeti változók módosításához.</span><span class="sxs-lookup"><span data-stu-id="b0907-134">You can also create and modify environment variables from within PowerShell.</span></span> <span data-ttu-id="b0907-135">Környezeti változók elérhető Windows PowerShell rendszerben található Windows környezeti változók normál szabályok felelnek meg.</span><span class="sxs-lookup"><span data-stu-id="b0907-135">Environment variables accessed from Windows PowerShell conform to the normal rules for environment variables elsewhere in Windows.</span></span>

