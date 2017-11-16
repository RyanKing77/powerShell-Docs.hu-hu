---
ms.date: 2017-06-05
keywords: PowerShell parancsmag
title: "A Windows PowerShell ISE objektummodell Scripting célja"
ms.assetid: d176a131-ab0c-43ee-80c1-f824ab8e4a05
ms.openlocfilehash: 3256d8bff3885d266f0db6f52932e40c4beaf8b1
ms.sourcegitcommit: d6ab9ab5909ed59cce4ce30e29457e0e75c7ac12
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/08/2017
---
# <a name="purpose-of-the-windows-powershell-ise-scripting-object-model"></a><span data-ttu-id="b790d-103">A Windows PowerShell ISE objektummodell Scripting célja</span><span class="sxs-lookup"><span data-stu-id="b790d-103">Purpose of the Windows PowerShell ISE Scripting Object Model</span></span>
  <span data-ttu-id="b790d-104">Objektum társítva az űrlap és a funkció a Windows PowerShell integrált parancsfájlkezelési környezet (ISE).</span><span class="sxs-lookup"><span data-stu-id="b790d-104">Objects are associated with the form and function of Windows PowerShell Integrated Scripting Environment (ISE).</span></span> <span data-ttu-id="b790d-105">Az objektumhivatkozás modell ismerteti a tag tulajdonságai és metódusai, ezek az objektumok visszaállítását.</span><span class="sxs-lookup"><span data-stu-id="b790d-105">The object model reference provides details about the member properties and methods that these objects expose.</span></span> <span data-ttu-id="b790d-106">Példák bemutatják, hogyan használható parancsfájlok közvetlenül elérje ezeket a metódusokat és tulajdonságok állnak rendelkezésre.</span><span class="sxs-lookup"><span data-stu-id="b790d-106">Examples are provided to show how you can use scripts to directly access these methods and properties.</span></span> <span data-ttu-id="b790d-107">A parancsfájl-kezelési objektummodell megkönnyíti a feladatok a következő tartományban kell lennie.</span><span class="sxs-lookup"><span data-stu-id="b790d-107">The scripting object model makes the following range of tasks easier.</span></span>

## <a name="customizing-the-appearance-of-windows-powershell-ise"></a><span data-ttu-id="b790d-108">A Windows PowerShell ISE megjelenésének testreszabása</span><span class="sxs-lookup"><span data-stu-id="b790d-108">Customizing the appearance of Windows PowerShell ISE</span></span>
 <span data-ttu-id="b790d-109">Csak akkor használhatja az objektum az alkalmazásbeállítások és a beállítások módosításához.</span><span class="sxs-lookup"><span data-stu-id="b790d-109">You can use the object model to modify the application settings and options.</span></span> <span data-ttu-id="b790d-110">Például módosíthatja azokat az alábbiak szerint:</span><span class="sxs-lookup"><span data-stu-id="b790d-110">For example, you can modify them as follows:</span></span>

- <span data-ttu-id="b790d-111">Módosíthatja a hibák, figyelmeztetések, részletes kimenetének színét, és a hibakeresési kimenete.</span><span class="sxs-lookup"><span data-stu-id="b790d-111">You can change the color of errors, warnings, verbose outputs, and debug outputs.</span></span>

- <span data-ttu-id="b790d-112">Get, vagy a parancssori ablaktáblában, a kimeneti ablaktábla és a parancssori panelbe a háttérszíneket.</span><span class="sxs-lookup"><span data-stu-id="b790d-112">You can get or set the background colors for the Command pane, the Output pane, and the Script pane.</span></span>

- <span data-ttu-id="b790d-113">Beállíthatja, hogy a kimeneti ablaktábla előtérszínét.</span><span class="sxs-lookup"><span data-stu-id="b790d-113">You can set the foreground color for the Output pane.</span></span>

- <span data-ttu-id="b790d-114">A Windows PowerShell ISE betűtípusok és betűméret adhatja meg.</span><span class="sxs-lookup"><span data-stu-id="b790d-114">You can set the font name and font size for Windows PowerShell ISE.</span></span>

- <span data-ttu-id="b790d-115">Beállíthatja a figyelmeztetések.</span><span class="sxs-lookup"><span data-stu-id="b790d-115">You can configure warnings.</span></span> <span data-ttu-id="b790d-116">Ez a beállítás, amelyeket a fájl megnyitásakor, több PowerShell lap, vagy ha a fájl a parancsfájl futtatása előtt a fájl mentését figyelmeztetések tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="b790d-116">This setting includes warnings that are issued when a file is opened in multiple PowerShell tabs or when a script in the file is run before the file has been saved.</span></span>

- <span data-ttu-id="b790d-117">Egy nézet, ha a parancsfájl és a kimeneti ablaktábla nem egymás melletti és nézet között válthat a parancssori panelbe esetén fölött a Tesztkimenet ablaktáblán.</span><span class="sxs-lookup"><span data-stu-id="b790d-117">You can switch between a view where the Script pane and the Output pane are side-by-side and a view where the Script pane is on top of the Output pane.</span></span> <span data-ttu-id="b790d-118">A parancs ablaktábla rögzítheti az alsó vagy felső részén a Tesztkimenet ablaktáblán.</span><span class="sxs-lookup"><span data-stu-id="b790d-118">You can dock the Command pane to the bottom or the top of the Output pane.</span></span>

## <a name="enhancing-the-functionality-of-windows-powershell-ise"></a><span data-ttu-id="b790d-119">A Windows PowerShell ISE működésére növelése</span><span class="sxs-lookup"><span data-stu-id="b790d-119">Enhancing the functionality of Windows PowerShell ISE</span></span>
 <span data-ttu-id="b790d-120">Csak akkor használhatja a objektum javítása érdekében a Windows PowerShell ISE működésére.</span><span class="sxs-lookup"><span data-stu-id="b790d-120">You can use the object model to enhance the functionality of Windows PowerShell ISE.</span></span> <span data-ttu-id="b790d-121">Például a következőket teheti:</span><span class="sxs-lookup"><span data-stu-id="b790d-121">For example, you can:</span></span>

- <span data-ttu-id="b790d-122">Adja hozzá, és a Windows PowerShell ISE maga-példányt módosító.</span><span class="sxs-lookup"><span data-stu-id="b790d-122">Add and modify the instance of Windows PowerShell ISE itself.</span></span> <span data-ttu-id="b790d-123">Például a menük módosításához, hozzáadhat új menüpontok és az új menüelemek leképezése parancsfájlok.</span><span class="sxs-lookup"><span data-stu-id="b790d-123">For example, to change the menus, you can add new menu items and map the new menu items to scripts.</span></span>

- <span data-ttu-id="b790d-124">Hozzon létre olyan parancsfájlok, amelyek a Windows PowerShell ISE menüparancsai és gombok segítségével elvégezhető feladatok elvégezhetők.</span><span class="sxs-lookup"><span data-stu-id="b790d-124">Create scripts that perform some of the tasks that you can perform by using the menu commands and buttons in Windows PowerShell ISE.</span></span> <span data-ttu-id="b790d-125">Például hozzáadhat, távolítsa el, vagy válasszon egy PowerShell lapon.</span><span class="sxs-lookup"><span data-stu-id="b790d-125">For example, you can add, remove, or select a PowerShell tab.</span></span>

- <span data-ttu-id="b790d-126">Parancsok és gombok segítségével végrehajtható feladatok komplemens számnak.</span><span class="sxs-lookup"><span data-stu-id="b790d-126">Complement tasks that can be performed by using menu commands and buttons.</span></span> <span data-ttu-id="b790d-127">Átnevezheti például a PowerShell-lapon.</span><span class="sxs-lookup"><span data-stu-id="b790d-127">For example, you can rename a PowerShell tab.</span></span>

- <span data-ttu-id="b790d-128">Szöveg pufferek a parancs ablaktáblán, a kimeneti ablaktábla és a parancssori panelbe fájl társított kezelheti.</span><span class="sxs-lookup"><span data-stu-id="b790d-128">Manipulate text buffers for the Command pane, the Output pane, and the Script pane that are associated with a file.</span></span> <span data-ttu-id="b790d-129">Például a következőket teheti:</span><span class="sxs-lookup"><span data-stu-id="b790d-129">For example, you can:</span></span>

    -   <span data-ttu-id="b790d-130">Futtasson, vagy a teljes szöveg.</span><span class="sxs-lookup"><span data-stu-id="b790d-130">Get or set all text.</span></span>

    -   <span data-ttu-id="b790d-131">GET, vagy adjon meg egy kijelölt szöveg.</span><span class="sxs-lookup"><span data-stu-id="b790d-131">Get or set a text selection.</span></span>

    -   <span data-ttu-id="b790d-132">Futtassa a parancsfájlt, vagy futtassa a parancsfájlt kijelölt része.</span><span class="sxs-lookup"><span data-stu-id="b790d-132">Run a script or run a selected portion of a script.</span></span>

    -   <span data-ttu-id="b790d-133">Egy sor görgessen nézetbe.</span><span class="sxs-lookup"><span data-stu-id="b790d-133">Scroll a line into view.</span></span>

    -   <span data-ttu-id="b790d-134">Helyezze be a szöveget egy kalap pozíciójában.</span><span class="sxs-lookup"><span data-stu-id="b790d-134">Insert text at a caret position.</span></span>

    -   <span data-ttu-id="b790d-135">Jelöljön ki egy szöveget.</span><span class="sxs-lookup"><span data-stu-id="b790d-135">Select a block of text.</span></span>

    -   <span data-ttu-id="b790d-136">Első sor utolsó száma.</span><span class="sxs-lookup"><span data-stu-id="b790d-136">Get the last line number.</span></span>

- <span data-ttu-id="b790d-137">Végre fájlműveleteket.</span><span class="sxs-lookup"><span data-stu-id="b790d-137">Perform file operations.</span></span> <span data-ttu-id="b790d-138">Például a következőket teheti:</span><span class="sxs-lookup"><span data-stu-id="b790d-138">For example, you can:</span></span>

    -   <span data-ttu-id="b790d-139">Nyisson meg egy fájlt, mentse a fájlt, vagy mentse a fájlt egy másik nevet.</span><span class="sxs-lookup"><span data-stu-id="b790d-139">Open a file, save a file, or save a file by using a different name.</span></span>

    -   <span data-ttu-id="b790d-140">Határozza meg, hogy a fájl legutóbbi mentése megváltozott-e.</span><span class="sxs-lookup"><span data-stu-id="b790d-140">Determine whether a file has been changed after it was last saved.</span></span>

    -   <span data-ttu-id="b790d-141">Beolvasni a fájlnevet.</span><span class="sxs-lookup"><span data-stu-id="b790d-141">Get the file name.</span></span>

    -   <span data-ttu-id="b790d-142">Válasszon ki egy fájlt.</span><span class="sxs-lookup"><span data-stu-id="b790d-142">Select a file.</span></span>

## <a name="automating-tasks"></a><span data-ttu-id="b790d-143">Feladatok automatizálása</span><span class="sxs-lookup"><span data-stu-id="b790d-143">Automating tasks</span></span>
 <span data-ttu-id="b790d-144">A parancsfájl-kezelési hálózatiobjektum-modellt hozhat létre a billentyűparancsok, gyakori műveletekhez.</span><span class="sxs-lookup"><span data-stu-id="b790d-144">You can use the scripting object model to create keyboard shortcuts for frequent operations.</span></span>

## <a name="see-also"></a><span data-ttu-id="b790d-145">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="b790d-145">See Also</span></span>
- [<span data-ttu-id="b790d-146">A ISE objektum modell hierarchia</span><span class="sxs-lookup"><span data-stu-id="b790d-146">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md) 
- [<span data-ttu-id="b790d-147">A Windows PowerShell ISE objektumhivatkozás modell</span><span class="sxs-lookup"><span data-stu-id="b790d-147">Windows PowerShell ISE Object Model Reference</span></span>](Windows-PowerShell-ISE-Object-Model-Reference.md) 
- [<span data-ttu-id="b790d-148">A Windows PowerShell ISE Scripting Hálózatiobjektum-modellje</span><span class="sxs-lookup"><span data-stu-id="b790d-148">The Windows PowerShell ISE Scripting Object Model</span></span>](The-Windows-PowerShell-ISE-Scripting-Object-Model.md)

  
