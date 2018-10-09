---
ms.date: 08/27/2018
keywords: PowerShell, a parancsmag
title: PowerShell-parancsprogramok
ms.openlocfilehash: 8a152ab338d42f861b7ff38de44d68db14262abb
ms.sourcegitcommit: 6749f67c32e05999e10deb9d45f90f45ac21a599
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/08/2018
ms.locfileid: "48851186"
---
# <a name="powershell"></a><span data-ttu-id="5ee03-103">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5ee03-103">PowerShell</span></span>

<span data-ttu-id="5ee03-104">PowerShell egy feladatalapú parancssori rendszerhéj és programozási nyelv, .NET épülő az.</span><span class="sxs-lookup"><span data-stu-id="5ee03-104">PowerShell is a task-based command-line shell and scripting language built on .NET.</span></span>
<span data-ttu-id="5ee03-105">PowerShell segítségével a rendszergazdák és a teljesítmény – a felhasználók gyorsan automatizálhatja a feladatokat, amelyek kezelése (Linux, macOS és Windows) operációs rendszerekkel és folyamatokkal.</span><span class="sxs-lookup"><span data-stu-id="5ee03-105">PowerShell helps system administrators and power-users can rapidly automate tasks that manage operating systems (Linux, macOS, and Windows) and processes.</span></span>

<span data-ttu-id="5ee03-106">PowerShell-parancsok segítségével kezelhet számítógépeket a parancssorból.</span><span class="sxs-lookup"><span data-stu-id="5ee03-106">PowerShell commands let you manage computers from the command line.</span></span> <span data-ttu-id="5ee03-107">PowerShell-szolgáltatók lehetővé teszik az adattárakban, például a beállításjegyzék eléréséhez, és a tanúsítványtárolót, egyszerűen, férni a fájlrendszerhez.</span><span class="sxs-lookup"><span data-stu-id="5ee03-107">PowerShell providers let you access data stores, such as the registry and certificate store, as easily as you access the file system.</span></span> <span data-ttu-id="5ee03-108">PowerShell tartalmaz egy gazdag kifejezés az elemzési és a egy fejlett programozási nyelv.</span><span class="sxs-lookup"><span data-stu-id="5ee03-108">PowerShell includes a rich expression parser and a fully developed scripting language.</span></span>

## <a name="powershell-is-open-source"></a><span data-ttu-id="5ee03-109">PowerShell az nyílt forráskódú</span><span class="sxs-lookup"><span data-stu-id="5ee03-109">PowerShell is open-source</span></span>

<span data-ttu-id="5ee03-110">PowerShell alap forráskód már elérhető a Githubon, és nyissa meg a közösségi közreműködést.</span><span class="sxs-lookup"><span data-stu-id="5ee03-110">PowerShell base source code is now available in GitHub and open to community contributions.</span></span>
<span data-ttu-id="5ee03-111">Lásd: [PowerShell forráskód a Githubon](https://github.com/powershell/powershell).</span><span class="sxs-lookup"><span data-stu-id="5ee03-111">See [PowerShell source on GitHub](https://github.com/powershell/powershell).</span></span>

<span data-ttu-id="5ee03-112">A bits szükséges kezdhet [a PowerShell első](https://github.com/PowerShell/PowerShell#get-powershell).</span><span class="sxs-lookup"><span data-stu-id="5ee03-112">You can start with the bits you need at [Get PowerShell](https://github.com/PowerShell/PowerShell#get-powershell).</span></span>
<span data-ttu-id="5ee03-113">Vagy esetleg a gyors bemutatót [bevezetés](https://github.com/PowerShell/PowerShell/blob/master/docs/learning-powershell).</span><span class="sxs-lookup"><span data-stu-id="5ee03-113">Or, perhaps, with a quick tour at [Getting Started](https://github.com/PowerShell/PowerShell/blob/master/docs/learning-powershell).</span></span>

## <a name="powershell-design-goals"></a><span data-ttu-id="5ee03-114">PowerShell elérheti a céljait</span><span class="sxs-lookup"><span data-stu-id="5ee03-114">PowerShell design goals</span></span>

<span data-ttu-id="5ee03-115">PowerShell régóta fennálló problémák, és új funkciók hozzáadásával a parancssori és parancsfájl-kezelési környezet javítására szolgál.</span><span class="sxs-lookup"><span data-stu-id="5ee03-115">PowerShell is designed to improve the command-line and scripting environment by eliminating long-standing problems and adding new features.</span></span>

### <a name="discoverability"></a><span data-ttu-id="5ee03-116">Felderíthetőség</span><span class="sxs-lookup"><span data-stu-id="5ee03-116">Discoverability</span></span>

<span data-ttu-id="5ee03-117">PowerShell megkönnyíti a felderítését annak szolgáltatásait.</span><span class="sxs-lookup"><span data-stu-id="5ee03-117">PowerShell makes it easy to discover its features.</span></span> <span data-ttu-id="5ee03-118">Ha például megtekintése és módosítása a Windows-szolgáltatások parancsmagjainak listáját találja, írja be:</span><span class="sxs-lookup"><span data-stu-id="5ee03-118">For example, to find a list of cmdlets that view and change Windows services, type:</span></span>

```powershell
Get-Command *-Service
```

<span data-ttu-id="5ee03-119">Felfedezése, mely parancsmag feladatot el egy feladatot, miután további információ a parancsmag használatával a `Get-Help` parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="5ee03-119">After discovering which cmdlet accomplishes a task, you can learn more about the cmdlet by using the `Get-Help` cmdlet.</span></span> <span data-ttu-id="5ee03-120">Például kapcsolatos súgó megjelenítése a `Get-Service` parancsmagot, írja be:</span><span class="sxs-lookup"><span data-stu-id="5ee03-120">For example, to display help about the `Get-Service` cmdlet, type:</span></span>

```powershell
Get-Help Get-Service
```

<span data-ttu-id="5ee03-121">A legtöbb parancsmagok visszaadott objektumok, amelyek kezelhetők, és ezután jelenik meg a megjelenítendő szöveg.</span><span class="sxs-lookup"><span data-stu-id="5ee03-121">Most cmdlets return objects that can be manipulated and then rendered as text for display.</span></span> <span data-ttu-id="5ee03-122">Teljes mértékben megérteni a parancsmag kimenete, irányítsa a kimenetét a `Get-Member` parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="5ee03-122">To fully understand the output of a cmdlet, pipe the output to the `Get-Member` cmdlet.</span></span> <span data-ttu-id="5ee03-123">Például a következő parancsot az objektum kimenete tagjainak információit jeleníti meg a `Get-Service` parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="5ee03-123">For example, the following command displays information about the members of the object output by the `Get-Service` cmdlet.</span></span>

```powershell
Get-Service | Get-Member
```

### <a name="consistency"></a><span data-ttu-id="5ee03-124">Consistency</span><span class="sxs-lookup"><span data-stu-id="5ee03-124">Consistency</span></span>

<span data-ttu-id="5ee03-125">Rendszerek kezelése összetett feladat lehet.</span><span class="sxs-lookup"><span data-stu-id="5ee03-125">Managing systems can be a complex task.</span></span> <span data-ttu-id="5ee03-126">Egységes felület rendelkező eszközök segítségével szabályozhatja a járó összetettséget.</span><span class="sxs-lookup"><span data-stu-id="5ee03-126">Tools that have a consistent interface help to control the inherent complexity.</span></span> <span data-ttu-id="5ee03-127">Sajnos parancssori eszközök és parancsfájlok futtatására alkalmas COM-objektumok azok konzisztencia nem ismert.</span><span class="sxs-lookup"><span data-stu-id="5ee03-127">Unfortunately, command-line tools and scriptable COM objects aren't known for their consistency.</span></span>

<span data-ttu-id="5ee03-128">A PowerShell konzisztencia az egyik elsődleges eszközei.</span><span class="sxs-lookup"><span data-stu-id="5ee03-128">The consistency of PowerShell is one of its primary assets.</span></span> <span data-ttu-id="5ee03-129">Például, ha megismerheti, hogyan használható a `Sort-Object` parancsmag használhatja arra, hogy bármely parancsmag kimenete rendezéséhez.</span><span class="sxs-lookup"><span data-stu-id="5ee03-129">For example, if you learn how to use the `Sort-Object` cmdlet, you can use that knowledge to sort the output of any cmdlet.</span></span> <span data-ttu-id="5ee03-130">Ismerje meg a különböző rendezési rutinok minden parancsmag nem kell.</span><span class="sxs-lookup"><span data-stu-id="5ee03-130">You don't have to learn the different sorting routines of each cmdlet.</span></span>

<span data-ttu-id="5ee03-131">Tervezési rendezési tulajdonságok azok a parancsmagok ezenkívül parancsmag a fejlesztők nem szükséges.</span><span class="sxs-lookup"><span data-stu-id="5ee03-131">Additionally, cmdlet developers don't have to design sorting features for their cmdlets.</span></span> <span data-ttu-id="5ee03-132">PowerShell az alapvető szolgáltatások egy keretrendszer, amely kényszeríti a konzisztencia biztosít.</span><span class="sxs-lookup"><span data-stu-id="5ee03-132">PowerShell provides a framework with the basic features that forces consistency.</span></span> <span data-ttu-id="5ee03-133">A keretrendszer kiküszöböli az egyes lehetőségek, hogy a fejlesztők van hátra.</span><span class="sxs-lookup"><span data-stu-id="5ee03-133">The framework eliminates some choices that are left to the developer.</span></span> <span data-ttu-id="5ee03-134">De cserébe teszi parancsmagok fejlesztését jóval egyszerűbb.</span><span class="sxs-lookup"><span data-stu-id="5ee03-134">But, in return, it makes the development of cmdlets much simpler.</span></span>

### <a name="interactive-and-scripting-environments"></a><span data-ttu-id="5ee03-135">Interaktív és parancsfájl-kezelési környezet</span><span class="sxs-lookup"><span data-stu-id="5ee03-135">Interactive and scripting environments</span></span>

<span data-ttu-id="5ee03-136">A Windows-parancssor használatával interaktív shell parancssori eszközökkel és az alapszintű parancsfájlok hozzáférést biztosít.</span><span class="sxs-lookup"><span data-stu-id="5ee03-136">The Windows Command Prompt provides an interactive shell with access to command-line tools and basic scripting.</span></span> <span data-ttu-id="5ee03-137">Windows Script Host (WSH) rendelkezik a parancsfájlok futtatására alkalmas parancssori eszközeivel és a COM-automatizálási objektumok, de nem biztosít egy interaktív kezelőfelület.</span><span class="sxs-lookup"><span data-stu-id="5ee03-137">Windows Script Host (WSH) has scriptable command-line tools and COM automation objects, but doesn't provide an interactive shell.</span></span>

<span data-ttu-id="5ee03-138">PowerShell-ben interaktív shell és a egy parancsfájl-kezelési környezet.</span><span class="sxs-lookup"><span data-stu-id="5ee03-138">PowerShell combines an interactive shell and a scripting environment.</span></span> <span data-ttu-id="5ee03-139">PowerShell parancssori eszközökkel, a COM-objektumok és a .NET-osztálytárak hozzáférhet.</span><span class="sxs-lookup"><span data-stu-id="5ee03-139">PowerShell can access command-line tools, COM objects, and .NET class libraries.</span></span> <span data-ttu-id="5ee03-140">Ez a kombinációja bővíti ki az interaktív felhasználó, a parancsfájl-író és a rendszergazdához.</span><span class="sxs-lookup"><span data-stu-id="5ee03-140">This combination of features extends the capabilities of the interactive user, the script writer, and the system administrator.</span></span>

### <a name="object-orientation"></a><span data-ttu-id="5ee03-141">Objektum tájolása</span><span class="sxs-lookup"><span data-stu-id="5ee03-141">Object orientation</span></span>

<span data-ttu-id="5ee03-142">PowerShell az objektum nem szöveg alapján történik.</span><span class="sxs-lookup"><span data-stu-id="5ee03-142">PowerShell is based on object not text.</span></span> <span data-ttu-id="5ee03-143">A parancs kimenete egy olyan objektum.</span><span class="sxs-lookup"><span data-stu-id="5ee03-143">The output of a command is an object.</span></span> <span data-ttu-id="5ee03-144">A kimeneti objektum, a folyamat keresztül küldhet bemenetként egy másik parancsba.</span><span class="sxs-lookup"><span data-stu-id="5ee03-144">You can send the output object, through the pipeline, to another command as its input.</span></span>

<span data-ttu-id="5ee03-145">Ez a folyamat ismerős felületet biztosít a személyek hasznosítani más ismertetése.</span><span class="sxs-lookup"><span data-stu-id="5ee03-145">This pipeline provides a familiar interface for people experienced with other shells.</span></span> <span data-ttu-id="5ee03-146">PowerShell ezen elgondolás szöveg helyett objektumok küldésével.</span><span class="sxs-lookup"><span data-stu-id="5ee03-146">PowerShell extends this concept by sending objects rather than text.</span></span>

### <a name="easy-transition-to-scripting"></a><span data-ttu-id="5ee03-147">A parancsfájl-kezelési egyszerű Váltás</span><span class="sxs-lookup"><span data-stu-id="5ee03-147">Easy transition to scripting</span></span>

<span data-ttu-id="5ee03-148">PowerShell a parancs felderíthetőség teszi azt írja be a Váltás könnyen parancsok, interaktív módon való létrehozásának és futtatásának parancsfájlok.</span><span class="sxs-lookup"><span data-stu-id="5ee03-148">PowerShell's command discoverability makes it easy to transition from typing commands interactively to creating and running scripts.</span></span> <span data-ttu-id="5ee03-149">PowerShell átiratok és előzmények megkönnyítik egy fájlt egy parancsfájl használható parancsok másolása.</span><span class="sxs-lookup"><span data-stu-id="5ee03-149">PowerShell transcripts and history make it easy to copy commands to a file for use as a script.</span></span>
