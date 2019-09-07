---
ms.date: 09/06/2019
keywords: PowerShell, parancsmag
title: A PowerShell 5,0 ISE újdonságai
ms.openlocfilehash: a719baef0da1600f0a5377e1b72c81b67e37eef2
ms.sourcegitcommit: a74ae7ed089301992fed201fbe55d827a622afa0
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/06/2019
ms.locfileid: "70746224"
---
# <a name="whats-new-in-the-windows-powershell-50-ise"></a><span data-ttu-id="db8ff-103">A Windows PowerShell 5,0 ISE újdonságai</span><span class="sxs-lookup"><span data-stu-id="db8ff-103">What's New in the Windows PowerShell 5.0 ISE</span></span>

<span data-ttu-id="db8ff-104">Ez a témakör a Windows PowerShell integrált parancsfájlkezelési környezet (ISE) verzióiban bevezetett új és frissített funkciókat ismerteti.</span><span class="sxs-lookup"><span data-stu-id="db8ff-104">This topic explains the new and updated features that have been introduced in versions of Windows PowerShell Integrated Scripting Environment (ISE).</span></span>

## <a name="feature-description"></a><span data-ttu-id="db8ff-105">A szolgáltatás leírása</span><span class="sxs-lookup"><span data-stu-id="db8ff-105">Feature description</span></span>

<span data-ttu-id="db8ff-106">A Windows PowerShell integrált parancsprogram-kezelési környezet egy olyan gazda-alkalmazás, amely lehetővé teszi parancsfájlok és modulok írását, futtatását és tesztelését grafikus és intuitív környezetben.</span><span class="sxs-lookup"><span data-stu-id="db8ff-106">The Windows PowerShell ISE is a host application that enables you to write, run, and test scripts and modules in a graphical and intuitive environment.</span></span> <span data-ttu-id="db8ff-107">A főbb funkciók, mint például a szintaxis – színezés, a tabulátorok befejezése, a vizualizációs hibakeresés, a Unicode-megfelelőség és a környezetfüggő súgó nyújt széles körű programozási élményt.</span><span class="sxs-lookup"><span data-stu-id="db8ff-107">Key features such as syntax-coloring, tab completion, visual debugging, Unicode compliance, and context-sensitive Help provide a rich scripting experience.</span></span>

<span data-ttu-id="db8ff-108">További információ: [a Windows PowerShell integrált parancsprogram-kezelési környezet bemutatása](../components/ise/Introducing-the-Windows-PowerShell-ISE.md).</span><span class="sxs-lookup"><span data-stu-id="db8ff-108">For more information, see [Introducing the Windows PowerShell ISE](../components/ise/Introducing-the-Windows-PowerShell-ISE.md).</span></span>

<span data-ttu-id="db8ff-109">A következő táblázat a Windows PowerShell integrált parancsprogram-kezelési környezet ezen kiadásának új és megváltozott funkcióit sorolja fel a Windows PowerShellben.</span><span class="sxs-lookup"><span data-stu-id="db8ff-109">The following table lists the new and changed features for this release of Windows PowerShell ISE in Windows PowerShell.</span></span>

## <a name="intellisense"></a><span data-ttu-id="db8ff-110">IntelliSense</span><span class="sxs-lookup"><span data-stu-id="db8ff-110">IntelliSense</span></span>

> <span data-ttu-id="db8ff-111">Az ISE 3,0-ben hozzáadva</span><span class="sxs-lookup"><span data-stu-id="db8ff-111">Added in ISE 3.0</span></span>

<span data-ttu-id="db8ff-112">Az IntelliSense egy automatikus kiegészítési szolgáltatás, amely a Windows PowerShell integrált parancsprogram-kezelési környezet részét képezi.</span><span class="sxs-lookup"><span data-stu-id="db8ff-112">IntelliSense is an automatic-completion assistance feature that is part of Windows PowerShell ISE.</span></span>
<span data-ttu-id="db8ff-113">Az IntelliSense a beíráskor a potenciálisan egyező parancsmagok, paraméterek, paraméterérték, fájlok vagy mappák kattintható menüit jeleníti meg.</span><span class="sxs-lookup"><span data-stu-id="db8ff-113">IntelliSense displays clickable menus of potentially matching cmdlets, parameters, parameter values, files, or folders as you type.</span></span>

<span data-ttu-id="db8ff-114">**Milyen értéket vesz fel ez a változás?**</span><span class="sxs-lookup"><span data-stu-id="db8ff-114">**What value does this change add?**</span></span>

<span data-ttu-id="db8ff-115">Az IntelliSense hozzáadásával könnyebben felderítheti a parancsmagokat és a szintaxist, ha a Windows PowerShell integrált parancsprogram-kezelési környezet használatával parancsfájlokat hoz létre.</span><span class="sxs-lookup"><span data-stu-id="db8ff-115">With the addition of IntelliSense, it's easier to discover cmdlets and syntax when you use Windows PowerShell ISE to create scripts.</span></span> <span data-ttu-id="db8ff-116">Az új parancsfájlok létrehozásakor Windows PowerShell integrált parancsprogram-kezelési környezet is megismerheti a Windows PowerShellt.</span><span class="sxs-lookup"><span data-stu-id="db8ff-116">You can also use Windows PowerShell ISE to learn Windows PowerShell while you create new scripts.</span></span>

<span data-ttu-id="db8ff-117">**Mi működik másképp?**</span><span class="sxs-lookup"><span data-stu-id="db8ff-117">**What works differently?**</span></span>

<span data-ttu-id="db8ff-118">Ha parancsmagokat gépel be a Windows PowerShell integrált parancsprogram-kezelési környezetba, egy görgethető és kattintható menü jelenik meg, amely lehetővé teszi a megfelelő parancsok tallózását és kiválasztását.</span><span class="sxs-lookup"><span data-stu-id="db8ff-118">When you type cmdlets in the Windows PowerShell ISE, a scrollable and clickable menu displays, allowing you to browse and select the appropriate commands.</span></span>

## <a name="snippets"></a><span data-ttu-id="db8ff-119">Kódrészletek</span><span class="sxs-lookup"><span data-stu-id="db8ff-119">Snippets</span></span>

> <span data-ttu-id="db8ff-120">Az ISE 3,0-ben hozzáadva</span><span class="sxs-lookup"><span data-stu-id="db8ff-120">Added in ISE 3.0</span></span>

<span data-ttu-id="db8ff-121">A *kódrészletek* a Windows PowerShell-kód rövid részei, amelyeket beillesztheti a Windows PowerShell integrált parancsprogram-kezelési környezetban létrehozott parancsfájlba.</span><span class="sxs-lookup"><span data-stu-id="db8ff-121">*Snippets* are short sections of Windows PowerShell code that you can insert into the scripts you create in Windows PowerShell ISE.</span></span> <span data-ttu-id="db8ff-122">A Windows PowerShell integrált parancsprogram-kezelési környezet a kódrészletek alapértelmezett készletét tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="db8ff-122">Windows PowerShell ISE comes with a default set of snippets.</span></span> <span data-ttu-id="db8ff-123">Kódrészleteket a `New-Snippet` parancsmag használatával adhat hozzá Windows PowerShell integrált parancsprogram-kezelési környezetban való munka közben.</span><span class="sxs-lookup"><span data-stu-id="db8ff-123">You can add snippets by using the `New-Snippet` cmdlet while working in Windows PowerShell ISE.</span></span>

<span data-ttu-id="db8ff-124">**Milyen értéket vesz fel ez a változás?**</span><span class="sxs-lookup"><span data-stu-id="db8ff-124">**What value does this change add?**</span></span>

<span data-ttu-id="db8ff-125">A kódrészletek használatával gyorsan összeállíthat és létrehozhat parancsfájlokat a környezet automatizálásához.</span><span class="sxs-lookup"><span data-stu-id="db8ff-125">By using snippets, you can quickly assemble and create scripts to automate your environment.</span></span>

<span data-ttu-id="db8ff-126">**Mi működik másképp?**</span><span class="sxs-lookup"><span data-stu-id="db8ff-126">**What works differently?**</span></span>

<span data-ttu-id="db8ff-127">Ha a kódrészleteket a Windows PowerShell 3,0-es vagy újabb verziójában szeretné használni, akkor a **Szerkesztés** menüben kattintson a **kódrészletek indítása**lehetőségre, vagy nyomja le a <kbd>CTRL</kbd>+<kbd>J</kbd>billentyűt.</span><span class="sxs-lookup"><span data-stu-id="db8ff-127">To use snippets in Windows PowerShell 3.0 or later, on the **Edit** menu, click **Start Snippets**, or press <kbd>Ctrl</kbd>+<kbd>J</kbd>.</span></span>

## <a name="add-on-tools"></a><span data-ttu-id="db8ff-128">Kiegészítő eszközök</span><span class="sxs-lookup"><span data-stu-id="db8ff-128">Add-on tools</span></span>

> <span data-ttu-id="db8ff-129">A PowerShell 3,0-ben hozzáadva</span><span class="sxs-lookup"><span data-stu-id="db8ff-129">Added in PowerShell 3.0</span></span>

<span data-ttu-id="db8ff-130">A Windows PowerShell integrált parancsprogram-kezelési környezet mostantól támogatja a kiegészítő eszközöket az objektummodell használatával.</span><span class="sxs-lookup"><span data-stu-id="db8ff-130">Windows PowerShell ISE now supports add-on tools using the object model.</span></span> <span data-ttu-id="db8ff-131">Ezek a bővítmények Windows megjelenítési alaprendszer (WPF) vezérlők, amelyek függőleges vagy vízszintes ablaktáblában jelennek meg a konzolon.</span><span class="sxs-lookup"><span data-stu-id="db8ff-131">These add-ons are Windows Presentation Foundation (WPF) controls that are displayed as a vertical or horizontal pane in the console.</span></span> <span data-ttu-id="db8ff-132">Egy panelen több kiegészítő eszköz jelenik meg Többlapos vezérlőelemként.</span><span class="sxs-lookup"><span data-stu-id="db8ff-132">Multiple add-on tools in a pane are displayed as a tabbed control.</span></span> <span data-ttu-id="db8ff-133">A nem Microsoft felek által készített kiegészítő eszközöket is hozzáadhat vagy eltávolíthat.</span><span class="sxs-lookup"><span data-stu-id="db8ff-133">You can also add or remove add-on tools that are produced by non-Microsoft parties.</span></span> <span data-ttu-id="db8ff-134">További információkért tekintse meg a [Windows PowerShell integrált parancsprogram-kezelési környezet parancsfájl-objektummodell célját](../components/ise/object-model/Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md).</span><span class="sxs-lookup"><span data-stu-id="db8ff-134">For more information, see [The Purpose of the Windows PowerShell ISE Scripting Object Model](../components/ise/object-model/Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md).</span></span>

<span data-ttu-id="db8ff-135">**Milyen értéket vesz fel ez a változás?**</span><span class="sxs-lookup"><span data-stu-id="db8ff-135">**What value does this change add?**</span></span>

<span data-ttu-id="db8ff-136">A bővítmények lehetővé teszik a Windows PowerShell integrált parancsprogram-kezelési környezet bővítését és testreszabását olyan eszközökkel, amelyek funkciókkal bővítik és javítják a parancsfájl-kezelési élményt.</span><span class="sxs-lookup"><span data-stu-id="db8ff-136">Add-ons allow you to extend and customize Windows PowerShell ISE with tools that add functionality and enhance your scripting experience.</span></span>

<span data-ttu-id="db8ff-137">**Mi működik másképp?**</span><span class="sxs-lookup"><span data-stu-id="db8ff-137">**What works differently?**</span></span>

<span data-ttu-id="db8ff-138">A Windows PowerShell integrált parancsprogram-kezelési környezet 3,0-es és újabb verzióiban az Add-on **parancs** szerepel.</span><span class="sxs-lookup"><span data-stu-id="db8ff-138">Windows PowerShell ISE 3.0 and later come with the **Commands** add-on.</span></span> <span data-ttu-id="db8ff-139">A **parancsok** bővítmény lehetővé teszi a parancsmagok tallózását, és a parancsmagokkal kapcsolatos súgó elérését a **parancsfájl** és a **konzol** ablaktáblán.</span><span class="sxs-lookup"><span data-stu-id="db8ff-139">The **Commands** add-on allows you to browse cmdlets, and access help about the cmdlets side-by-side with the **Script** and **Console** Panes.</span></span>

<span data-ttu-id="db8ff-140">További bővítmények a **bővítmények** menüjének a kiegészítő **eszközök webhely megnyitása** parancsával érhetők el.</span><span class="sxs-lookup"><span data-stu-id="db8ff-140">Additional add-ons can be found by using the **Open Add-on Tools Website** command on the **Add-ons** menu.</span></span>

## <a name="restart-manager-and-auto-save"></a><span data-ttu-id="db8ff-141">Újraindítás-kezelő és automatikus mentés</span><span class="sxs-lookup"><span data-stu-id="db8ff-141">Restart manager and auto-save</span></span>

> <span data-ttu-id="db8ff-142">A PowerShell 3,0-ben hozzáadva</span><span class="sxs-lookup"><span data-stu-id="db8ff-142">Added in PowerShell 3.0</span></span>

<span data-ttu-id="db8ff-143">Windows PowerShell integrált parancsprogram-kezelési környezet mostantól két percenként automatikusan menti a megnyitott parancsfájlokat egy külön helyen.</span><span class="sxs-lookup"><span data-stu-id="db8ff-143">Windows PowerShell ISE now automatically saves your open scripts every two minutes, in a separate location.</span></span> <span data-ttu-id="db8ff-144">Ha a Windows PowerShell integrált parancsprogram-kezelési környezet váratlan összeomlás vagy újraindítás után újraindul, akkor a a legutóbbi munkamenetben megnyitott parancsfájlokat is helyreállítja, még akkor is, ha a parancsfájlok nem lettek mentve.</span><span class="sxs-lookup"><span data-stu-id="db8ff-144">When Windows PowerShell ISE restarts after an unexpected crash or reboot, it recovers scripts that were open in the last session, even if the scripts weren't saved.</span></span>

<span data-ttu-id="db8ff-145">Az automatikus mentési időköz módosításához futtassa a következő parancsot a konzol ablaktáblán: `$psise.Options.AutoSaveMinuteInterval`.</span><span class="sxs-lookup"><span data-stu-id="db8ff-145">To change the automatic saving interval, run the following command in the Console pane: `$psise.Options.AutoSaveMinuteInterval`.</span></span>

<span data-ttu-id="db8ff-146">**Milyen értéket vesz fel ez a változás?**</span><span class="sxs-lookup"><span data-stu-id="db8ff-146">**What value does this change add?**</span></span>

<span data-ttu-id="db8ff-147">Mostantól Windows PowerShell integrált parancsprogram-kezelési környezet tudja, hogy a megnyitott parancsfájlok automatikusan mentve lesznek.</span><span class="sxs-lookup"><span data-stu-id="db8ff-147">You can now work within Windows PowerShell ISE knowing that your open scripts are automatically saved.</span></span>

<span data-ttu-id="db8ff-148">**Mi működik másképp?**</span><span class="sxs-lookup"><span data-stu-id="db8ff-148">**What works differently?**</span></span>

<span data-ttu-id="db8ff-149">Windows PowerShell integrált parancsprogram-kezelési környezet 2,0 nem menti automatikusan a parancsfájlokat.</span><span class="sxs-lookup"><span data-stu-id="db8ff-149">Windows PowerShell ISE 2.0 doesn't save the scripts automatically.</span></span>

## <a name="most-recently-used-list"></a><span data-ttu-id="db8ff-150">Legutóbb használt lista</span><span class="sxs-lookup"><span data-stu-id="db8ff-150">Most-recently used list</span></span>

> <span data-ttu-id="db8ff-151">A PowerShell 3,0-ben hozzáadva</span><span class="sxs-lookup"><span data-stu-id="db8ff-151">Added in PowerShell 3.0</span></span>

<span data-ttu-id="db8ff-152">Windows PowerShell integrált parancsprogram-kezelési környezet mostantól a fájlok legutóbb használt listája szerepel.</span><span class="sxs-lookup"><span data-stu-id="db8ff-152">Windows PowerShell ISE now has a most-recently used list for files.</span></span> <span data-ttu-id="db8ff-153">Amikor megnyit egy fájlt a Windows PowerShell integrált parancsprogram-kezelési környezetban, a fájl hozzá lesz adva a **fájl** menü legutóbb használt listájához.</span><span class="sxs-lookup"><span data-stu-id="db8ff-153">When you open a file in Windows PowerShell ISE, the file is added to the most-recently used list on the **File** menu.</span></span>

<span data-ttu-id="db8ff-154">A legutóbb használt listán szereplő fájlok alapértelmezett számának módosításához futtassa a következő parancsot a konzol ablaktáblán: `$psise.Options.MruCount`.</span><span class="sxs-lookup"><span data-stu-id="db8ff-154">To change the default number of files in the most-recently used list, run the following command in the Console Pane: `$psise.Options.MruCount`.</span></span>

<span data-ttu-id="db8ff-155">**Milyen értéket vesz fel ez a változás?**</span><span class="sxs-lookup"><span data-stu-id="db8ff-155">**What value does this change add?**</span></span>

<span data-ttu-id="db8ff-156">Mostantól a leggyakrabban használt lista használatával könnyedén hozzáférhet a gyakran használt fájlokhoz.</span><span class="sxs-lookup"><span data-stu-id="db8ff-156">You can now use the most-recently used list to easily access your frequently used files.</span></span>

<span data-ttu-id="db8ff-157">**Mi működik másképp?**</span><span class="sxs-lookup"><span data-stu-id="db8ff-157">**What works differently?**</span></span>

<span data-ttu-id="db8ff-158">Windows PowerShell integrált parancsprogram-kezelési környezet 2,0 nem rendelkezik legutóbb használt listával.</span><span class="sxs-lookup"><span data-stu-id="db8ff-158">Windows PowerShell ISE 2.0 doesn't have a most-recently used list.</span></span>

## <a name="console-pane"></a><span data-ttu-id="db8ff-159">Konzol ablaktábla</span><span class="sxs-lookup"><span data-stu-id="db8ff-159">Console Pane</span></span>

> <span data-ttu-id="db8ff-160">A PowerShell 3,0-ben hozzáadva</span><span class="sxs-lookup"><span data-stu-id="db8ff-160">Added in PowerShell 3.0</span></span>

<span data-ttu-id="db8ff-161">A Windows PowerShell integrált parancsprogram-kezelési környezet első kiadásában elérhető külön parancs-és kimeneti ablaktábla egyetlen konzol ablaktáblába lett egyesítve.</span><span class="sxs-lookup"><span data-stu-id="db8ff-161">The separate Command and Output Panes that were available in the first release of Windows PowerShell ISE have been combined into a single Console Pane.</span></span> <span data-ttu-id="db8ff-162">A konzol ablaktábla hasonló a függvényhez és a megjelenéshez egy tipikus Windows PowerShell-konzolon, de a következő fejlesztéseket tartalmazza:</span><span class="sxs-lookup"><span data-stu-id="db8ff-162">The Console Pane is similar in function and appearance to a typical Windows PowerShell console, but it includes the following enhancements:</span></span>

- <span data-ttu-id="db8ff-163">A bemeneti szöveg (nem kimeneti szöveg) szintaxisának színezése, beleértve az XML-szintaxist is</span><span class="sxs-lookup"><span data-stu-id="db8ff-163">Syntax coloring for input text (not output text), including XML syntax</span></span>
- <span data-ttu-id="db8ff-164">IntelliSense</span><span class="sxs-lookup"><span data-stu-id="db8ff-164">IntelliSense</span></span>
- <span data-ttu-id="db8ff-165">Zárójel egyeztetése</span><span class="sxs-lookup"><span data-stu-id="db8ff-165">Brace matching</span></span>
- <span data-ttu-id="db8ff-166">Hiba jelzése</span><span class="sxs-lookup"><span data-stu-id="db8ff-166">Error indication</span></span>
- <span data-ttu-id="db8ff-167">Teljes Unicode-támogatás</span><span class="sxs-lookup"><span data-stu-id="db8ff-167">Full Unicode support</span></span>
- <span data-ttu-id="db8ff-168">Az <kbd>F1</kbd> környezetfüggő súgója</span><span class="sxs-lookup"><span data-stu-id="db8ff-168"><kbd>F1</kbd> context-sensitive help</span></span>
- <span data-ttu-id="db8ff-169"><kbd></kbd>CTRL+<kbd>F1</kbd> Context-szenzitív show-parancs</span><span class="sxs-lookup"><span data-stu-id="db8ff-169"><kbd>Ctrl</kbd>+<kbd>F1</kbd> context-sensitive Show-Command</span></span>
- <span data-ttu-id="db8ff-170">Összetett parancsfájl és jobbról balra író támogatás</span><span class="sxs-lookup"><span data-stu-id="db8ff-170">Complex script and right-to-left support</span></span>
- <span data-ttu-id="db8ff-171">Betűkészlet-támogatás</span><span class="sxs-lookup"><span data-stu-id="db8ff-171">Font support</span></span>
- <span data-ttu-id="db8ff-172">Nagyítás</span><span class="sxs-lookup"><span data-stu-id="db8ff-172">Zoom</span></span>
- <span data-ttu-id="db8ff-173">Vonal kiválasztása és letiltása – válasszon üzemmódot</span><span class="sxs-lookup"><span data-stu-id="db8ff-173">Line-select and block-select modes</span></span>
- <span data-ttu-id="db8ff-174">A beírt tartalom megőrzése a parancssorban, amikor megnyomja a <kbd>felfelé mutató nyilat</kbd> a konzolon megjelenő előzmények megtekintéséhez</span><span class="sxs-lookup"><span data-stu-id="db8ff-174">Preservation of typed content at the command line when you press the <kbd>UpArrow</kbd> to view history in the console</span></span>

<span data-ttu-id="db8ff-175">**Milyen értéket vesz fel ez a változás?**</span><span class="sxs-lookup"><span data-stu-id="db8ff-175">**What value does this change add?**</span></span>

<span data-ttu-id="db8ff-176">A konzol ablaktáblájának módosításai mellett a konzol felületének konzisztens programozási élménye is elérhető.</span><span class="sxs-lookup"><span data-stu-id="db8ff-176">The addition of these Console Pane changes provides a scripting experience that is more consistent with the console interface.</span></span>

<span data-ttu-id="db8ff-177">**Mi működik másképp?**</span><span class="sxs-lookup"><span data-stu-id="db8ff-177">**What works differently?**</span></span>

<span data-ttu-id="db8ff-178">A Windows PowerShell integrált parancsprogram-kezelési környezet 2,0 külön parancs-és kimeneti ablaktáblával rendelkezik.</span><span class="sxs-lookup"><span data-stu-id="db8ff-178">Windows PowerShell ISE 2.0 has separate Command and Output Panes.</span></span>

## <a name="command-line-switches"></a><span data-ttu-id="db8ff-179">Parancssori kapcsolók</span><span class="sxs-lookup"><span data-stu-id="db8ff-179">Command-line switches</span></span>

> <span data-ttu-id="db8ff-180">A PowerShell 3,0-ben hozzáadva</span><span class="sxs-lookup"><span data-stu-id="db8ff-180">Added in PowerShell 3.0</span></span>

<span data-ttu-id="db8ff-181">Ha a parancssorból indítja a Windows PowerShell integrált parancsprogram-kezelési környezett (a **powershell_ise. exe**beírásával), a következő új parancssori kapcsolók adhatók hozzá.</span><span class="sxs-lookup"><span data-stu-id="db8ff-181">If you start Windows PowerShell ISE from the command line (by typing **powershell_ise.exe**), you can add the following new command-line switches.</span></span>

- <span data-ttu-id="db8ff-182">`-NoProfile`: Windows PowerShell integrált parancsprogram-kezelési környezet futtatása nélkül elindul`$profile`</span><span class="sxs-lookup"><span data-stu-id="db8ff-182">`-NoProfile`: Starts Windows PowerShell ISE without running `$profile`</span></span>
- <span data-ttu-id="db8ff-183">`-Help`: Súgóablak megjelenítése</span><span class="sxs-lookup"><span data-stu-id="db8ff-183">`-Help`: Displays a Help window</span></span>
- <span data-ttu-id="db8ff-184">`-mta`: A Windows PowerShell integrált parancsprogram-kezelési környezet elindítása többszálú lakás módban.</span><span class="sxs-lookup"><span data-stu-id="db8ff-184">`-mta`: Starts Windows PowerShell ISE in multithreaded apartment mode.</span></span> <span data-ttu-id="db8ff-185">Windows PowerShell integrált parancsprogram-kezelési környezet alapértelmezett működési módja az egyszálas apartman mód vagy `-sta`a.</span><span class="sxs-lookup"><span data-stu-id="db8ff-185">The default operation mode for Windows PowerShell ISE is single-threaded apartment mode, or `-sta`.</span></span>

<span data-ttu-id="db8ff-186">**Milyen értéket vesz fel ez a változás?**</span><span class="sxs-lookup"><span data-stu-id="db8ff-186">**What value does this change add?**</span></span>

<span data-ttu-id="db8ff-187">Ezen parancssori kapcsolók hozzáadásával szabályozhatja azt a környezetet, amelyben a Windows PowerShell integrált parancsprogram-kezelési környezet fut.</span><span class="sxs-lookup"><span data-stu-id="db8ff-187">The addition of these command-line switches allows you to control the environment in which the Windows PowerShell ISE runs.</span></span>

<span data-ttu-id="db8ff-188">**Mi működik másképp?**</span><span class="sxs-lookup"><span data-stu-id="db8ff-188">**What works differently?**</span></span>

<span data-ttu-id="db8ff-189">Windows PowerShell integrált parancsprogram-kezelési környezet 2,0 nem ismeri fel ezeket a parancssori kapcsolókat.</span><span class="sxs-lookup"><span data-stu-id="db8ff-189">Windows PowerShell ISE 2.0 doesn't recognize these command-line switches.</span></span>

## <a name="new-editor-features"></a><span data-ttu-id="db8ff-190">Új szerkesztői funkciók</span><span class="sxs-lookup"><span data-stu-id="db8ff-190">New editor features</span></span>

> <span data-ttu-id="db8ff-191">A PowerShell 3,0-ben hozzáadva</span><span class="sxs-lookup"><span data-stu-id="db8ff-191">Added in PowerShell 3.0</span></span>

<span data-ttu-id="db8ff-192">Más Windows PowerShell integrált parancsprogram-kezelési környezet szerkesztési funkciói a következők:</span><span class="sxs-lookup"><span data-stu-id="db8ff-192">Other Windows PowerShell ISE editing features include:</span></span>

- <span data-ttu-id="db8ff-193">Az **XML-szintaxis színezése** – Windows PowerShell integrált parancsprogram-kezelési környezet a színek XML-szintaxisa ugyanúgy, mint a Windows PowerShell-szintaxis.</span><span class="sxs-lookup"><span data-stu-id="db8ff-193">**XML syntax coloring** - Windows PowerShell ISE now colors XML syntax in the same way as it colors Windows PowerShell syntax.</span></span>
- <span data-ttu-id="db8ff-194">A **kapcsos zárójelek** – Windows PowerShell integrált parancsprogram-kezelési környezet kapcsos zárójeleket és kiemeléseket tartalmaz, és a következő módokon használhatók: (például az **Ugrás egyezési** paranccsal vagy a <kbd>CTRL billentyűvel</kbd>+<kbd>)</kbd> a záró kapcsos zárójelek megkeresése, ha nyitó zárójel van kiválasztva).</span><span class="sxs-lookup"><span data-stu-id="db8ff-194">**Brace matching** - Windows PowerShell ISE includes brace matching and highlighting, and can be used in the following ways: (for example, using the **Go to Match** command or <kbd>Ctrl</kbd>+<kbd>]</kbd> locates the closing brace, if you have an opening brace selected).</span></span>
- <span data-ttu-id="db8ff-195">**Vázlat nézet** A parancsfájl panel támogatja a kibontást, amely lehetővé teszi a kódok összecsukását vagy kibővítését a bal oldali margón a plusz vagy a mínusz jelre kattintva.</span><span class="sxs-lookup"><span data-stu-id="db8ff-195">**Outline view** The Script Pane supports outlining, which allows collapsing or expanding sections of code by clicking plus or minus signs in the left margin.</span></span> <span data-ttu-id="db8ff-196">Használhat kapcsos zárójeleket, illetve a `#region` és `#endregion` címkéket is egy összecsukható szakasz elejének vagy végének megjelöléséhez.</span><span class="sxs-lookup"><span data-stu-id="db8ff-196">You can use braces or the `#region` and `#endregion` tags to mark the beginning or end of a collapsible section.</span></span> <span data-ttu-id="db8ff-197">Az összes régió kibontásához vagy összecsukásához nyomja le a <kbd>CTRL</kbd>+<kbd>M</kbd>billentyűkombinációt.</span><span class="sxs-lookup"><span data-stu-id="db8ff-197">To expand or collapse all regions, press <kbd>Ctrl</kbd>+<kbd>M</kbd>.</span></span>
- <span data-ttu-id="db8ff-198">**A szöveg szerkesztésének húzása – a** Windows PowerShell integrált parancsprogram-kezelési környezet mostantól támogatja a szövegszerkesztés húzását.</span><span class="sxs-lookup"><span data-stu-id="db8ff-198">**Drag and drop text editing** - Windows PowerShell ISE now supports drag and drop text editing.</span></span> <span data-ttu-id="db8ff-199">Bármelyik szövegrészt kiválaszthatja, és a szövegszerkesztőben vagy a konzolon áthelyezheti a szöveget egy másik helyre.</span><span class="sxs-lookup"><span data-stu-id="db8ff-199">You can select any block of text and drag that text to another location in the editor or the console to move the text.</span></span> <span data-ttu-id="db8ff-200">Ha lenyomva tartja a <kbd>CTRL</kbd> billentyűt a kijelölt szöveg húzása közben, az egérgomb felengedésekor a rendszer az új helyre másolja a szöveget.</span><span class="sxs-lookup"><span data-stu-id="db8ff-200">If you hold down the <kbd>Ctrl</kbd> key while you drag the selected text, when you release the mouse button the text is copied to the new location.</span></span> <span data-ttu-id="db8ff-201">Windows PowerShell integrált parancsprogram-kezelési környezet jelen verziójában a fájlok Windows PowerShell integrált parancsprogram-kezelési környezetre húzásakor Windows PowerShell integrált parancsprogram-kezelési környezet megnyitja a fájlt.</span><span class="sxs-lookup"><span data-stu-id="db8ff-201">In this version of Windows PowerShell ISE, when you drag and drop files onto Windows PowerShell ISE, Windows PowerShell ISE opens the file.</span></span>
- <span data-ttu-id="db8ff-202">**Elemzési hiba megjelenítése** – az elemzési hibák piros aláhúzással vannak jelezve.</span><span class="sxs-lookup"><span data-stu-id="db8ff-202">**Parse error display** - Parse errors are indicated with red underlines.</span></span> <span data-ttu-id="db8ff-203">Ha egy jelzett hiba fölé viszi a mutatót, az elemleírás szövege megjeleníti a kódban talált problémát.</span><span class="sxs-lookup"><span data-stu-id="db8ff-203">When you hover over an indicated error, tooltip text displays the problem that was found in the code.</span></span>
- <span data-ttu-id="db8ff-204">**Nagyítás** – a konzol tartalmának nagyítási aránya a nagyítás csúszkával állítható be (a Windows PowerShell integrált parancsprogram-kezelési környezet ablak jobb alsó sarkában), vagy a konzol ablaktáblán a parancs `$psise.options.Zoom` megadásával.</span><span class="sxs-lookup"><span data-stu-id="db8ff-204">**Zoom** - The zoom percentage of the console's content can be set by using the zoom slider (in the lower right corner of Windows PowerShell ISE window), or by entering the command `$psise.options.Zoom` in the Console Pane.</span></span>
- <span data-ttu-id="db8ff-205">**Rich Text másolás és beillesztés** – a vágólapra másolása Windows PowerShell integrált parancsprogram-kezelési környezet megőrzi az eredeti kijelölés betűtípusát, méretét és színét.</span><span class="sxs-lookup"><span data-stu-id="db8ff-205">**Rich text copy and paste** - Copying to the clipboard in Windows PowerShell ISE preserves the font, size, and color information of the original selection.</span></span>
- <span data-ttu-id="db8ff-206">**Kijelölés tiltása** – kijelölhet egy szövegrészt úgy, hogy lenyomja az <kbd>ALT</kbd> billentyűt, miközben kiválasztja a szöveget a szkript ablaktáblán az egérrel, vagy az <kbd>ALT</kbd>+<kbd>SHIFT</kbd>+<kbd>billentyű lenyomásával.</kbd></span><span class="sxs-lookup"><span data-stu-id="db8ff-206">**Block selection** - You can select a block of text by holding down the <kbd>ALT</kbd> key while selecting text in the Script Pane with your mouse, or by pressing <kbd>Alt</kbd>+<kbd>Shift</kbd>+<kbd>Arrow</kbd>.</span></span>

<span data-ttu-id="db8ff-207">**Milyen értéket vesz fel ez a változás?**</span><span class="sxs-lookup"><span data-stu-id="db8ff-207">**What value does this change add?**</span></span>

<span data-ttu-id="db8ff-208">A további szerkesztési funkciók konzisztens és hatékony szerkesztési környezetet biztosítanak.</span><span class="sxs-lookup"><span data-stu-id="db8ff-208">The additional editing features provide a more consistent and powerful editing environment.</span></span>

<span data-ttu-id="db8ff-209">**Mi működik másképp?**</span><span class="sxs-lookup"><span data-stu-id="db8ff-209">**What works differently?**</span></span>

<span data-ttu-id="db8ff-210">Ezek a szerkesztési fejlesztések nem voltak jelen a Windows PowerShell integrált parancsprogram-kezelési környezet 2,0-ben.</span><span class="sxs-lookup"><span data-stu-id="db8ff-210">These editing enhancements weren't present in Windows PowerShell ISE 2.0.</span></span>

## <a name="new-help-viewer-window"></a><span data-ttu-id="db8ff-211">Új Súgó megjelenítői ablak</span><span class="sxs-lookup"><span data-stu-id="db8ff-211">New Help viewer window</span></span>

> <span data-ttu-id="db8ff-212">A PowerShell 3,0-ben hozzáadva</span><span class="sxs-lookup"><span data-stu-id="db8ff-212">Added in PowerShell 3.0</span></span>

<span data-ttu-id="db8ff-213">Ha lenyomja az <kbd>F1</kbd> billentyűt, amikor a kurzor egy parancsmagban van, vagy ha egy kijelölt parancsmag része, az új Súgó megjelenítő környezetfüggő súgót nyit meg a Kiemelt parancsmaggal kapcsolatban.</span><span class="sxs-lookup"><span data-stu-id="db8ff-213">If you press <kbd>F1</kbd> when your cursor is in a cmdlet, or you have part of a cmdlet highlighted, the new Help viewer opens context-sensitive Help about the highlighted cmdlet.</span></span> <span data-ttu-id="db8ff-214">A **Súgó Windows** PowerShell megjelenítéséhez írja be `operators` a konzolt a konzol ablaktáblán, majd nyomja le az <kbd>F1</kbd>billentyűt.</span><span class="sxs-lookup"><span data-stu-id="db8ff-214">To display Windows PowerShell **About** help, type `operators` in the console pane, and then press <kbd>F1</kbd>.</span></span>

<span data-ttu-id="db8ff-215">A szolgáltatás használata előtt töltse le a Windows PowerShell súgójának legújabb verzióját a Microsoft webhelyén.</span><span class="sxs-lookup"><span data-stu-id="db8ff-215">Before you use this feature, download the most current version of Windows PowerShell Help topics from the Microsoft website.</span></span> <span data-ttu-id="db8ff-216">A súgótémakörök letöltésének legegyszerűbb módja, ha a Windows PowerShell integrált parancsprogram-kezelési környezet rendszergazdaként `Update-Help` való futtatásakor a konzol ablaktábláján futtatja a parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="db8ff-216">The simplest method for downloading the Help topics is to run the `Update-Help` cmdlet in the Console Pane when running Windows PowerShell ISE as administrator.</span></span>

<span data-ttu-id="db8ff-217">Megváltoztathatja az <kbd>F1</kbd> -es kulcs súgóját.</span><span class="sxs-lookup"><span data-stu-id="db8ff-217">You can alter where the <kbd>F1</kbd> key looks for Help.</span></span> <span data-ttu-id="db8ff-218">Az **eszközök**/**beállításai** menü **általános beállítások** lapján a **többi beállítás**alatt beállíthatja vagy törölheti a jelölőnégyzetet a **helyi súgótartalom használata online tartalom helyett**.</span><span class="sxs-lookup"><span data-stu-id="db8ff-218">In the **Tools**/**Options** menu, on the **General Settings** tab, under **Other Settings**, you can set or clear the checkbox **Use local help content instead of online content**.</span></span> <span data-ttu-id="db8ff-219">Ha be van jelölve, a-ügyfél a modul mappában található letöltött súgóban megkeresi a parancsmag súgóját.</span><span class="sxs-lookup"><span data-stu-id="db8ff-219">When checked, the client looks for the cmdlet Help in the downloaded Help found in the modules folder.</span></span> <span data-ttu-id="db8ff-220">Ha a jelölőnégyzet nincs bejelölve, az ügyfél az online súgót keresi.</span><span class="sxs-lookup"><span data-stu-id="db8ff-220">If the checkbox is cleared, the client looks for help online.</span></span>

<span data-ttu-id="db8ff-221">**Milyen értéket vesz fel ez a változás?**</span><span class="sxs-lookup"><span data-stu-id="db8ff-221">**What value does this change add?**</span></span>

<span data-ttu-id="db8ff-222">Környezetfüggő súgó a jelenlegi parancsmag vagy parancsfájl elhagyása nélkül integrált tanulási élményt biztosít.</span><span class="sxs-lookup"><span data-stu-id="db8ff-222">Context-sensitive Help without leaving your current cmdlet or script provides an integrated learning experience.</span></span>

<span data-ttu-id="db8ff-223">**Mi működik másképp?**</span><span class="sxs-lookup"><span data-stu-id="db8ff-223">**What works differently?**</span></span>

<span data-ttu-id="db8ff-224">Windows PowerShell integrált parancsprogram-kezelési környezet korábbi verzióiban az <kbd>F1</kbd> billentyű lenyomásával megnyitotta a súgófájl a helyi számítógépen.</span><span class="sxs-lookup"><span data-stu-id="db8ff-224">Pressing <kbd>F1</kbd> in previous versions of Windows PowerShell ISE opened the help file on the local computer.</span></span> <span data-ttu-id="db8ff-225">A Windows PowerShell integrált parancsprogram-kezelési környezet 3,0-es és újabb verzióiban megnyílik egy ablak, amely tartalmazza a kereshető és konfigurálható parancsmag súgóját.</span><span class="sxs-lookup"><span data-stu-id="db8ff-225">In Windows PowerShell ISE 3.0 and later, a window opens that contains the help for the cmdlet that is searchable and configurable.</span></span> <span data-ttu-id="db8ff-226">Ez a Windows PowerShell 3,0 újdonsága a Windows PowerShell integrált parancsprogram-kezelési környezet 3,0 és a frissíthető Súgó.</span><span class="sxs-lookup"><span data-stu-id="db8ff-226">This Help experience is new for Windows PowerShell ISE 3.0, and Updatable Help is new for Windows PowerShell 3.0.</span></span>

## <a name="show-command-cmdlet"></a><span data-ttu-id="db8ff-227">Parancssori parancsmag megjelenítése</span><span class="sxs-lookup"><span data-stu-id="db8ff-227">Show-Command cmdlet</span></span>

> <span data-ttu-id="db8ff-228">A PowerShell 3,0-ben hozzáadva</span><span class="sxs-lookup"><span data-stu-id="db8ff-228">Added in PowerShell 3.0</span></span>

<span data-ttu-id="db8ff-229">A `Show-Command` parancsmag lehetővé teszi a parancsmagok vagy függvények összeállítását és futtatását grafikus űrlapok kitöltésével.</span><span class="sxs-lookup"><span data-stu-id="db8ff-229">The `Show-Command` cmdlet enables you to compose or run a cmdlet or function by filling in a graphical form.</span></span> <span data-ttu-id="db8ff-230">Az űrlap lehetővé teszi, hogy a felhasználók grafikus környezetben működjenek a Windows PowerShell használatával.</span><span class="sxs-lookup"><span data-stu-id="db8ff-230">The form lets users work with Windows PowerShell in a graphical environment.</span></span>
<span data-ttu-id="db8ff-231">`Show-Command`a speciális parancsfájlokat is lehetővé tesz a gyors Windows PowerShell-alapú grafikus felhasználói felület létrehozásához.</span><span class="sxs-lookup"><span data-stu-id="db8ff-231">`Show-Command` also enables advanced scripters to create a quick Windows PowerShell-based GUI.</span></span>

<span data-ttu-id="db8ff-232">**Milyen értéket vesz fel ez a változás?**</span><span class="sxs-lookup"><span data-stu-id="db8ff-232">**What value does this change add?**</span></span>

<span data-ttu-id="db8ff-233">A használatával `Show-Command` a Windows PowerShell-parancsfájlok segítségével megadhatja a felhasználók számára, hogy milyen grafikus környezettel rendelkeznek.</span><span class="sxs-lookup"><span data-stu-id="db8ff-233">By using `Show-Command` in your Windows PowerShell scripts, you can provide your users with the graphical environment with which they're familiar.</span></span> <span data-ttu-id="db8ff-234">`Show-Command`a a bevezető felhasználók számára is segítséget nyújt a Windows PowerShell megismerésében.</span><span class="sxs-lookup"><span data-stu-id="db8ff-234">`Show-Command` can also help introductory users learn Windows PowerShell.</span></span>

<span data-ttu-id="db8ff-235">**Mi működik másképp?**</span><span class="sxs-lookup"><span data-stu-id="db8ff-235">**What works differently?**</span></span>

<span data-ttu-id="db8ff-236">`Show-Command`új Windows PowerShell integrált parancsprogram-kezelési környezet 3,0.</span><span class="sxs-lookup"><span data-stu-id="db8ff-236">`Show-Command` is new Windows PowerShell ISE 3.0.</span></span>

## <a name="see-also"></a><span data-ttu-id="db8ff-237">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="db8ff-237">See also</span></span>

<span data-ttu-id="db8ff-238">További információ a Windows PowerShell integrált parancsprogram-kezelési környezet használatáról: [a Windows PowerShell integrált parancsfájlkezelési környezetének feltárása](../getting-started/fundamental/exploring-the-windows-powershell-ise.md).</span><span class="sxs-lookup"><span data-stu-id="db8ff-238">For more information about using Windows PowerShell ISE, see [Exploring the Windows PowerShell Integrated Scripting Environment](../getting-started/fundamental/exploring-the-windows-powershell-ise.md).</span></span>
