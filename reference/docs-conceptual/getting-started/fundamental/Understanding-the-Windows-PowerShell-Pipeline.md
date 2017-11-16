---
ms.date: 2017-06-05
keywords: PowerShell parancsmag
title: "A Windows PowerShell kimenetátirányítási mechanizmusával ismertetése"
ms.assetid: 6be50926-7943-4ef7-9499-4490d72a63fb
ms.openlocfilehash: 6d152e52d2fcfb9dd592eb9ac40500615f2186cb
ms.sourcegitcommit: 74255f0b5f386a072458af058a15240140acb294
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/03/2017
---
# <a name="understanding-the-windows-powershell-pipeline"></a><span data-ttu-id="9e946-103">A Windows PowerShell kimenetátirányítási mechanizmusával ismertetése</span><span class="sxs-lookup"><span data-stu-id="9e946-103">Understanding the Windows PowerShell Pipeline</span></span>
<span data-ttu-id="9e946-104">Átirányítás gyakorlatilag tetszőleges helyszínről a Windows PowerShell működik.</span><span class="sxs-lookup"><span data-stu-id="9e946-104">Piping works virtually everywhere in Windows PowerShell.</span></span> <span data-ttu-id="9e946-105">Bár a képernyőn látható szöveg, a Windows PowerShell a szöveges parancsok között nem csövön keresztüli.</span><span class="sxs-lookup"><span data-stu-id="9e946-105">Although you see text on the screen, Windows PowerShell does not pipe text between commands.</span></span> <span data-ttu-id="9e946-106">Ehelyett azt kiszolgálókészletéhez objektumok.</span><span class="sxs-lookup"><span data-stu-id="9e946-106">Instead, it pipes objects.</span></span>

<span data-ttu-id="9e946-107">A notation szállítására hasonlít más ismertetése a használt, így első ránézésre nem lehet nyilvánvaló, hogy a Windows PowerShell bevezet egy új.</span><span class="sxs-lookup"><span data-stu-id="9e946-107">The notation used for pipelines is similar to that used in other shells, so at first glance, it may not be apparent that Windows PowerShell introduces something new.</span></span> <span data-ttu-id="9e946-108">Például, ha használja a **kimenő gazdagép** lap-lap megjeleníti a kimeneti csak egy másik parancsba is, a kimeneti keresi a force parancsmagot, például a normál szöveget a képernyőn látható, lapok lebontva:</span><span class="sxs-lookup"><span data-stu-id="9e946-108">For example, if you use the **Out-Host** cmdlet to force a page-by-page display of output from another command, the output looks just like the normal text displayed on the screen, broken up into pages:</span></span>

```
PS> Get-ChildItem -Path C:\WINDOWS\System32 | Out-Host -Paging

    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\WINDOWS\system32

Mode                LastWriteTime     Length Name
----                -------------     ------ ----
-a---        2005-10-22  11:04 PM        315 $winnt$.inf
-a---        2004-08-04   8:00 AM      68608 access.cpl
-a---        2004-08-04   8:00 AM      64512 acctres.dll
-a---        2004-08-04   8:00 AM     183808 accwiz.exe
-a---        2004-08-04   8:00 AM      61952 acelpdec.ax
-a---        2004-08-04   8:00 AM     129536 acledit.dll
-a---        2004-08-04   8:00 AM     114688 aclui.dll
-a---        2004-08-04   8:00 AM     194048 activeds.dll
-a---        2004-08-04   8:00 AM     111104 activeds.tlb
-a---        2004-08-04   8:00 AM       4096 actmovie.exe
-a---        2004-08-04   8:00 AM     101888 actxprxy.dll
-a---        2003-02-21   6:50 PM     143150 admgmt.msc
-a---        2006-01-25   3:35 PM      53760 admparse.dll
<SPACE> next page; <CR> next line; Q quit
...
```

<span data-ttu-id="9e946-109">A Out-Host-lapozást parancs esetén hasznos csővezeték tényező, valahányszor lassan megjeleníteni kívánt hosszadalmas kimenet van.</span><span class="sxs-lookup"><span data-stu-id="9e946-109">The Out-Host -Paging command is a useful pipeline element whenever you have lengthy output that you would like to display slowly.</span></span> <span data-ttu-id="9e946-110">Akkor különösen hasznos, ha a művelet nagyon processzorigényes.</span><span class="sxs-lookup"><span data-stu-id="9e946-110">It is especially useful if the operation is very CPU-intensive.</span></span> <span data-ttu-id="9e946-111">Mivel feldolgozási átkerül a kimenő futtatni a parancsmagot akkor is rendelkezik teljes készen áll a megjelenítése, ha azt megelőző az adatcsatorna parancsmagok halt művelet mindaddig, amíg a kimenet a következő oldalon érhető el.</span><span class="sxs-lookup"><span data-stu-id="9e946-111">Because processing is transferred to the Out-Host cmdlet when it has a complete page ready to display, cmdlets that precede it in the pipeline halt operation until the next page of output is available.</span></span> <span data-ttu-id="9e946-112">Erre úgy tekinthet, a Windows Feladatkezelő figyelése Processzor- és használja a Windows PowerShell használatakor.</span><span class="sxs-lookup"><span data-stu-id="9e946-112">You can see this if you use the Windows Task Manager to monitor CPU and memory use by Windows PowerShell.</span></span>

<span data-ttu-id="9e946-113">A következő parancsot: **Get-ChildItem C:\\Windows-Recurse**.</span><span class="sxs-lookup"><span data-stu-id="9e946-113">Run the following command: **Get-ChildItem C:\\Windows -Recurse**.</span></span> <span data-ttu-id="9e946-114">Hasonlítsa össze a parancs a Processzor- és memóriahasználatról: **Get-ChildItem C:\\Windows-Recurse |} Kimenő gazdagép-lapozást**.</span><span class="sxs-lookup"><span data-stu-id="9e946-114">Compare the CPU and memory usage to this command: **Get-ChildItem C:\\Windows -Recurse | Out-Host -Paging**.</span></span> <span data-ttu-id="9e946-115">Mi a képernyőn látható szöveg, de, mert a szükséges objektumokat képviseli a konzolablakban szövegként.</span><span class="sxs-lookup"><span data-stu-id="9e946-115">What you see on the screen is text, but that is because it is necessary to represent objects as text in a console window.</span></span> <span data-ttu-id="9e946-116">Ez az imént a megjelenítése, hogy mit valóban abba az írást, a Windows PowerShell belül.</span><span class="sxs-lookup"><span data-stu-id="9e946-116">This is just a representation of what is really going on inside Windows PowerShell.</span></span> <span data-ttu-id="9e946-117">Vegye figyelembe például a Get-hely parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="9e946-117">For example, consider the Get-Location cmdlet.</span></span> <span data-ttu-id="9e946-118">Ha **Get-hely** amíg tartózkodási helyéhez a C meghajtó gyökérkönyvtárában, akkor jelenik meg a következő kimeneti:</span><span class="sxs-lookup"><span data-stu-id="9e946-118">If you type **Get-Location** while your current location is the root of the C drive, you would see the following output:</span></span>

```
PS> Get-Location

Path
----
C:\
```

<span data-ttu-id="9e946-119">A Windows PowerShell futószalagos szöveg, ha a parancs kiadása például **Get-hely |} Kimenő gazdagép**, átadása akkor **Get-hely** való **kimenő gazdagép** karakterek képernyőn megjelenésük sorrendjében.</span><span class="sxs-lookup"><span data-stu-id="9e946-119">If Windows PowerShell pipelined text, issuing a command such as **Get-Location | Out-Host**, would pass from **Get-Location** to **Out-Host** a set of characters in the order they are displayed onscreen.</span></span> <span data-ttu-id="9e946-120">Más szóval, amelyeket a rendszer figyelmen kívül hagyja a fejlécadatokat **kimenő gazdagép** először kapja a karakter "**C"**, majd a karakter "**:"**, majd a karakter " **\\'**.</span><span class="sxs-lookup"><span data-stu-id="9e946-120">In other words, if you were to ignore the heading information, **Out-Host** would first receive the character '**C'**, then the character '**:'**, then the character '**\\'**.</span></span> <span data-ttu-id="9e946-121">A **kimenő gazdagép** parancsmag nem tudta megállapítani, mely tehát a karakterek kimenete társítandó a **Get-hely** parancsmag.</span><span class="sxs-lookup"><span data-stu-id="9e946-121">The **Out-Host** cmdlet could not determine what meaning to associate with the characters output by the **Get-Location** cmdlet.</span></span>

<span data-ttu-id="9e946-122">Ahhoz, hogy egy folyamat parancsok szöveg helyett kommunikálnak, a Windows PowerShell-objektumokat használ.</span><span class="sxs-lookup"><span data-stu-id="9e946-122">Instead of using text to let commands in a pipeline communicate, Windows PowerShell uses objects.</span></span> <span data-ttu-id="9e946-123">A felhasználók szempontjából az objektumok kapcsolódó információkat, amelyek segítségével könnyebben egységként adatok kezelésére formába csomagot, majd bontsa ki a kívánt elemeket.</span><span class="sxs-lookup"><span data-stu-id="9e946-123">From the standpoint of a user, objects package related information into a form that makes it easier to manipulate the information as a unit, and extract specific items that you need.</span></span>

<span data-ttu-id="9e946-124">A **Get-hely** parancs nem ad vissza, amely tartalmazza az aktuális útvonalon szöveg.</span><span class="sxs-lookup"><span data-stu-id="9e946-124">The **Get-Location** command does not return text that contains the current path.</span></span> <span data-ttu-id="9e946-125">Nevű ismeretek adja vissza egy **PathInfo** objektum, amely tartalmazza az aktuális útvonalon néhány egyéb információk mellett.</span><span class="sxs-lookup"><span data-stu-id="9e946-125">It returns a package of information called a **PathInfo** object that contains the current path along with some other information.</span></span> <span data-ttu-id="9e946-126">A **kimenő gazdagép** parancsmag ezután elküldi a **PathInfo** a képernyő, és a Windows PowerShell-objektum úgy dönt, hogy mi megjelenítendő adatok és hogyan kell megjelenítenie a formázási szabályok alapján.</span><span class="sxs-lookup"><span data-stu-id="9e946-126">The **Out-Host** cmdlet then sends this **PathInfo** object to the screen, and Windows PowerShell decides what information to display and how to display it based on its formatting rules.</span></span>

<span data-ttu-id="9e946-127">Valójában a fejlécadatokat kimenetét az a **Get-hely** parancsmag csak a folyamat végén a képernyőn megjelenő megjelenített adatok formázási folyamat részeként kerül.</span><span class="sxs-lookup"><span data-stu-id="9e946-127">In fact, the heading information output by the **Get-Location** cmdlet is added only at the end of the process, as part of the process of formatting the data for onscreen display.</span></span> <span data-ttu-id="9e946-128">Megjelenő képernyőn van információk összegzését, és a kimeneti objektum nem a teljes megjelenítése.</span><span class="sxs-lookup"><span data-stu-id="9e946-128">What you see onscreen is a summary of information, and not a complete representation of the output object.</span></span>

<span data-ttu-id="9e946-129">Fényében, hogy előfordulhat, hogy egy parancs, mint mi látható ablakban jelenik meg a konzolon, hogyan lehet Windows PowerShell kimenete további információk lekérése az nem látható elemek?</span><span class="sxs-lookup"><span data-stu-id="9e946-129">Given that there may be more information output from a Windows PowerShell command than what we see displayed in the console window, how can you retrieve the non-visible elements?</span></span> <span data-ttu-id="9e946-130">Miként jelenjenek meg a további adatokat?</span><span class="sxs-lookup"><span data-stu-id="9e946-130">How do you view the extra data?</span></span> <span data-ttu-id="9e946-131">És mi történik, ha azt szeretné, az adatok megtekintéséhez eltér a egy Windows PowerShell formátuma általában?</span><span class="sxs-lookup"><span data-stu-id="9e946-131">And what if you want to view the data in a format different than the one Windows PowerShell normally uses?</span></span>

<span data-ttu-id="9e946-132">A többi Ez a fejezet ismerteti, hogyan felderítené az adott Windows PowerShell objektumok szerkezete meghatározott elemek kijelölése és formázási azokat könnyebben megjelenítési, és ezek az információk küldése az alternatív kimeneti helyekre, mint a fájlok és nyomtatók.</span><span class="sxs-lookup"><span data-stu-id="9e946-132">The rest of this chapter discusses how you can discover the structure of specific Windows PowerShell objects, selecting specific items and formatting them for easier display, and how to send this information to alternative output locations such as files and printers.</span></span>

