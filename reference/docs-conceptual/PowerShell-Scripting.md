---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: PowerShell-parancsprogramok
ms.openlocfilehash: c6ba3abc2544834e2cbec16a524f79399a1d2599
ms.sourcegitcommit: 77f62a55cac8c13d69d51eef5fade18f71d66955
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/17/2018
ms.locfileid: "39094051"
---
# <a name="powershell"></a><span data-ttu-id="a6ae3-103">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a6ae3-103">PowerShell</span></span>

<span data-ttu-id="a6ae3-104">A .NET-keretrendszer épülő PowerShell egy feladatalapú parancssori rendszerhéj és programozási nyelv; kifejezetten a rendszergazdák és kiemelt felhasználók felügyeletének részeként (Linux, macOS, Unix és Windows) több operációs rendszer és az operációs rendszereket futtató alkalmazásokhoz kapcsolódó folyamatok gyors automatizálása tervezték.</span><span class="sxs-lookup"><span data-stu-id="a6ae3-104">Built on the .NET Framework, PowerShell is a task-based command-line shell and scripting language; it is designed specifically for system administrators and power-users, to rapidly automate the administration of multiple operating systems (Linux, macOS, Unix, and Windows) and the processes related to the applications that run on those operating systems.</span></span>

## <a name="powershell-is-open-source"></a><span data-ttu-id="a6ae3-105">PowerShell az nyílt forráskódú</span><span class="sxs-lookup"><span data-stu-id="a6ae3-105">PowerShell is open source</span></span>

<span data-ttu-id="a6ae3-106">PowerShell alap forráskód már elérhető a Githubon, és nyissa meg a közösségi közreműködést.</span><span class="sxs-lookup"><span data-stu-id="a6ae3-106">PowerShell base source code is now available in GitHub and open to community contributions.</span></span>
<span data-ttu-id="a6ae3-107">Lásd: [PowerShell forráskód a Githubon](https://github.com/powershell/powershell).</span><span class="sxs-lookup"><span data-stu-id="a6ae3-107">See [PowerShell source on GitHub](https://github.com/powershell/powershell).</span></span>

<span data-ttu-id="a6ae3-108">A bits szükséges kezdhet [a PowerShell első](https://github.com/PowerShell/PowerShell#get-powershell).</span><span class="sxs-lookup"><span data-stu-id="a6ae3-108">You can start with the bits you need at [Get PowerShell](https://github.com/PowerShell/PowerShell#get-powershell).</span></span>
<span data-ttu-id="a6ae3-109">Vagy esetleg a gyors bemutatót [első lépések](https://github.com/PowerShell/PowerShell/blob/master/docs/learning-powershell)</span><span class="sxs-lookup"><span data-stu-id="a6ae3-109">Or, perhaps, with a quick tour at [Getting Started](https://github.com/PowerShell/PowerShell/blob/master/docs/learning-powershell)</span></span>

## <a name="powershell-design-goals"></a><span data-ttu-id="a6ae3-110">PowerShell elérheti a céljait</span><span class="sxs-lookup"><span data-stu-id="a6ae3-110">PowerShell design goals</span></span>
<span data-ttu-id="a6ae3-111">PowerShell régóta fennálló problémák, és új funkciók hozzáadásával a parancssori és parancsfájl-kezelési környezet javítására szolgál.</span><span class="sxs-lookup"><span data-stu-id="a6ae3-111">PowerShell is designed to improve the command-line and scripting environment by eliminating long-standing problems and adding new features.</span></span>

### <a name="discoverability"></a><span data-ttu-id="a6ae3-112">Felderíthetőség</span><span class="sxs-lookup"><span data-stu-id="a6ae3-112">Discoverability</span></span>
<span data-ttu-id="a6ae3-113">PowerShell megkönnyíti a felderítését annak szolgáltatásait.</span><span class="sxs-lookup"><span data-stu-id="a6ae3-113">PowerShell makes it easy to discover its features.</span></span> <span data-ttu-id="a6ae3-114">Ha például megtekintése és módosítása a Windows-szolgáltatások parancsmagjainak listáját találja, írja be:</span><span class="sxs-lookup"><span data-stu-id="a6ae3-114">For example, to find a list of cmdlets that view and change Windows services, type:</span></span>

```powershell
Get-Command *-Service
```

<span data-ttu-id="a6ae3-115">Felfedezése, mely parancsmag feladatot el egy feladatot, miután további információ a parancsmag használatával a `Get-Help` parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="a6ae3-115">After discovering which cmdlet accomplishes a task, you can learn more about the cmdlet by using the `Get-Help` cmdlet.</span></span>
<span data-ttu-id="a6ae3-116">Például kapcsolatos súgó megjelenítése a `Get-Service` parancsmagot, írja be:</span><span class="sxs-lookup"><span data-stu-id="a6ae3-116">For example, to display help about the `Get-Service` cmdlet, type:</span></span>

```powershell
Get-Help Get-Service
```
<span data-ttu-id="a6ae3-117">A legtöbb parancsmagok gridre bocsáthatja ki az objektumok, amelyek kezelhetők, és megjelenítendő szöveget, majd meg.</span><span class="sxs-lookup"><span data-stu-id="a6ae3-117">Most cmdlets emit objects which can be manipulated and then rendered into text for display.</span></span>
<span data-ttu-id="a6ae3-118">Teljes mértékben megérteni, hogy a parancsmag kimenete, kanálu kimenete a `Get-Member` parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="a6ae3-118">To fully understand the output of that cmdlet, pipe its output to the `Get-Member` cmdlet.</span></span>
<span data-ttu-id="a6ae3-119">Például a következő parancsot az objektum kimenete tagjainak információit jeleníti meg a `Get-Service` parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="a6ae3-119">For example, the following command displays information about the members of the object output by the `Get-Service` cmdlet.</span></span>

```powershell
Get-Service | Get-Member
```

### <a name="consistency"></a><span data-ttu-id="a6ae3-120">Consistency</span><span class="sxs-lookup"><span data-stu-id="a6ae3-120">Consistency</span></span>
<span data-ttu-id="a6ae3-121">Rendszerek kezelése egy összetett feladat lehet, és eszközöket, amelyek egy egységes felületen segítségével szabályozhatja a járó összetettséget.</span><span class="sxs-lookup"><span data-stu-id="a6ae3-121">Managing systems can be a complex endeavor and tools that have a consistent interface help to control the inherent complexity.</span></span>
<span data-ttu-id="a6ae3-122">Sajnos azonban nem parancssori eszközöket, és nem alkalmas parancsfájlok futtatására COM-objektumok az előzőekben a konzisztencia.</span><span class="sxs-lookup"><span data-stu-id="a6ae3-122">Unfortunately, neither command-line tools nor scriptable COM objects have been known for their consistency.</span></span>

<span data-ttu-id="a6ae3-123">A PowerShell konzisztencia az egyik elsődleges eszközei.</span><span class="sxs-lookup"><span data-stu-id="a6ae3-123">The consistency of PowerShell is one of its primary assets.</span></span>
<span data-ttu-id="a6ae3-124">Például, ha megismerheti, hogyan használható a `Sort-Object` parancsmag használhatja arra, hogy bármely parancsmag kimenete rendezéséhez.</span><span class="sxs-lookup"><span data-stu-id="a6ae3-124">For example, if you learn how to use the `Sort-Object` cmdlet, you can use that knowledge to sort the output of any cmdlet.</span></span>
<span data-ttu-id="a6ae3-125">További információt a különböző rendezési rutinok minden parancsmag nem rendelkezik.</span><span class="sxs-lookup"><span data-stu-id="a6ae3-125">You do not have to learn the different sorting routines of each cmdlet.</span></span>

<span data-ttu-id="a6ae3-126">A parancsmag a fejlesztők emellett nem rendelkezik a parancsmagok rendezési szolgáltatások tervezéséhez.</span><span class="sxs-lookup"><span data-stu-id="a6ae3-126">In addition, cmdlet developers do not have to design sorting features for their cmdlets.</span></span>
<span data-ttu-id="a6ae3-127">PowerShell biztosít egy keretrendszer, amely olyan alapvető szolgáltatásokat nyújt, és újrainicializálására kényszeríti a kapcsolatos a felület számos szempontból konzisztens.</span><span class="sxs-lookup"><span data-stu-id="a6ae3-127">PowerShell gives them a framework that provides the basic features and forces them to be consistent about many aspects of the interface.</span></span>
<span data-ttu-id="a6ae3-128">A keretrendszer kiküszöböli néhány, a lehetőségek, amelyek általában a fejlesztők marad, de cserébe lehetővé teszi a hatékony és könnyen használható parancsmagok fejlesztését jóval egyszerűbb.</span><span class="sxs-lookup"><span data-stu-id="a6ae3-128">The framework eliminates some of the choices that are typically left to the developer, but, in return, it makes the development of robust and easy-to-use cmdlets much simpler.</span></span>

### <a name="interactive-and-scripting-environments"></a><span data-ttu-id="a6ae3-129">Interaktív és parancsfájl-kezelési környezet</span><span class="sxs-lookup"><span data-stu-id="a6ae3-129">Interactive and Scripting Environments</span></span>
<span data-ttu-id="a6ae3-130">PowerShell az egy kombinált interaktív és parancsfájl-kezelési környezet, amely hozzáférést biztosít a parancssori eszközökkel és COM-objektumok, és lehetővé teszi, hogy a teljesítmény, a .NET Framework Class Library (FCL) használja.</span><span class="sxs-lookup"><span data-stu-id="a6ae3-130">PowerShell is a combined interactive and scripting environment that gives you access to command-line tools and COM objects, and also enables you to use the power of the .NET Framework Class Library (FCL).</span></span>

<span data-ttu-id="a6ae3-131">Ebben a környezetben javítja esetén a Windows parancssor használatával, amely több parancssori eszközökkel interaktív környezetet biztosít.</span><span class="sxs-lookup"><span data-stu-id="a6ae3-131">This environment improves upon the Windows Command Prompt, which provides an interactive environment with multiple command-line tools.</span></span>
<span data-ttu-id="a6ae3-132">Azt is javítja Windows Script Host (WSH) parancsfájlokat, amelyek lehetővé teszik több parancssori eszközeivel és COM-automatizálási objektumok, de nem ad meg egy interaktív környezetet.</span><span class="sxs-lookup"><span data-stu-id="a6ae3-132">It also improves upon Windows Script Host (WSH) scripts, which let you use multiple command-line tools and COM automation objects, but do not provide an interactive environment.</span></span>

<span data-ttu-id="a6ae3-133">Minden ezek a szolgáltatások kombinálásával PowerShell terjeszti ki a lehetőséget, az interaktív felhasználó és a parancsfájl-író, és megkönnyíti a rendszerfelügyelet könnyebben kezelhető.</span><span class="sxs-lookup"><span data-stu-id="a6ae3-133">By combining access to all of these features, PowerShell extends the ability of the interactive user and the script writer, and makes system administration more manageable.</span></span>

### <a name="object-orientation"></a><span data-ttu-id="a6ae3-134">Objektum tájolása</span><span class="sxs-lookup"><span data-stu-id="a6ae3-134">Object Orientation</span></span>
<span data-ttu-id="a6ae3-135">Bár a PowerShell dolgozhat parancsok beírásával a szöveg, PowerShell objektumokat, nem szöveg alapján történik.</span><span class="sxs-lookup"><span data-stu-id="a6ae3-135">Although you interact with PowerShell by typing commands in text, PowerShell is based on objects, not text.</span></span>
<span data-ttu-id="a6ae3-136">A parancs kimenete egy olyan objektum.</span><span class="sxs-lookup"><span data-stu-id="a6ae3-136">The output of a command is an object.</span></span>
<span data-ttu-id="a6ae3-137">A kimeneti objektum bemenetként küldhet egy másik parancsba.</span><span class="sxs-lookup"><span data-stu-id="a6ae3-137">You can send the output object to another command as its input.</span></span>
<span data-ttu-id="a6ae3-138">Ennek eredményeképpen PowerShell felületet biztosít a jól ismert egy új és hatékony parancssori paradigmát bevezetése mellett egyéb parancskörnyezet ismerő személyek számára.</span><span class="sxs-lookup"><span data-stu-id="a6ae3-138">As a result, PowerShell provides a familiar interface to people experienced with other shells, while introducing a new and powerful command-line paradigm.</span></span>
<span data-ttu-id="a6ae3-139">Ez a kiszolgálóvirtualizálás koncepcióján azáltal, hogy engedélyezi parancsokat küldhet az objektumokat, nem pedig szöveg közötti adatküldés.</span><span class="sxs-lookup"><span data-stu-id="a6ae3-139">It extends the concept of sending data between commands by enabling you to send objects, rather than text.</span></span>

### <a name="easy-transition-to-scripting"></a><span data-ttu-id="a6ae3-140">A parancsfájl-kezelési egyszerű Váltás</span><span class="sxs-lookup"><span data-stu-id="a6ae3-140">Easy Transition to Scripting</span></span>
<span data-ttu-id="a6ae3-141">Írja be az átállás egyszerűen parancsokat interaktív módon való létrehozásának és futtatásának parancsfájlok PowerShell teszi.</span><span class="sxs-lookup"><span data-stu-id="a6ae3-141">PowerShell makes it easy to transition from typing commands interactively to creating and running scripts.</span></span>
<span data-ttu-id="a6ae3-142">Fedezze fel, amelyek egy feladatot hajtanak végre a parancsokat a PowerShell-parancssort, írja be az parancsokat.</span><span class="sxs-lookup"><span data-stu-id="a6ae3-142">You can type commands at the PowerShell command prompt to discover the commands that perform a task.</span></span>
<span data-ttu-id="a6ae3-143">Ezután mentheti azokat a parancsokat egy szöveges vagy egy korábbi előtt egy fájl, amely egy parancsfájlt, hogy másolja őket.</span><span class="sxs-lookup"><span data-stu-id="a6ae3-143">Then, you can save those commands in a transcript or a history before copying them to a file for use as a script.</span></span>
