---
ms.date: 2017-06-05
keywords: PowerShell parancsmag
title: A PowerShell 50 a milyen s ISE
ms.assetid: 38648d47-7c27-4b37-a40e-ad29948519c2
ms.openlocfilehash: 89dcc905ce200d06029e148c9675269e6f518fa3
ms.sourcegitcommit: 3720ce4efb6735694cfb53a1b793d949af5d1bc5
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/29/2017
---
# <a name="what39s-new-in-the-windows-powershell-ise"></a><span data-ttu-id="c23be-103">Mi &#39;szükségesek, a Windows PowerShell ISE a újdonságai</span><span class="sxs-lookup"><span data-stu-id="c23be-103">What&#39;s New in the Windows PowerShell ISE</span></span>
<span data-ttu-id="c23be-104">Ez a témakör ismerteti a Windows PowerShell integrált parancsfájlkezelési környezet (ISE) verzióban bevezetett új és frissített szolgáltatásai.</span><span class="sxs-lookup"><span data-stu-id="c23be-104">This topic explains the new and updated features that have been introduced in versions of Windows PowerShell  Integrated Scripting Environment (ISE).</span></span>

## <a name="feature-description"></a><span data-ttu-id="c23be-105">A szolgáltatás leírása</span><span class="sxs-lookup"><span data-stu-id="c23be-105">Feature description</span></span>
<span data-ttu-id="c23be-106">A Windows PowerShell ISE még egy fogadó alkalmazás, amely lehetővé teszi a írási, futtatására, és tesztelje a parancsfájlokat és a modulok grafikus és intuitív környezetben.</span><span class="sxs-lookup"><span data-stu-id="c23be-106">The Windows PowerShell ISE is a host application that enables you to write, run, and test scripts and modules in a graphical and intuitive environment.</span></span> <span data-ttu-id="c23be-107">A legfontosabb jellemzők zintaxisszínek, például lapon befejezését, visual-hibakeresés, Unicode-megfelelőségi és környezetfüggő Súgó hatékony programozási környezetet biztosítson.</span><span class="sxs-lookup"><span data-stu-id="c23be-107">Key features such as syntax-coloring, tab completion, visual debugging, Unicode compliance, and context-sensitive Help provide a rich scripting experience.</span></span>

<span data-ttu-id="c23be-108">A Windows PowerShell ISE áttekintését lásd: [Windows PowerShell integrált parancsfájlkezelési környezet áttekintése](https://technet.microsoft.com/en-us/library/3c1892c2-bf84-4cb6-af26-1f453be9e671).</span><span class="sxs-lookup"><span data-stu-id="c23be-108">For an overview of Windows PowerShell ISE, see [Windows PowerShell Integrated Scripting Environment overview](https://technet.microsoft.com/en-us/library/3c1892c2-bf84-4cb6-af26-1f453be9e671).</span></span>

## <a name="new-and-changed-functionality-in-windows-powershell-ise"></a><span data-ttu-id="c23be-109">A Windows PowerShell ISE új és módosított funkciók</span><span class="sxs-lookup"><span data-stu-id="c23be-109">New and changed functionality in Windows PowerShell ISE</span></span>
<span data-ttu-id="c23be-110">A következő táblázat felsorolja az új és módosított szolgáltatások a jelen kiadása a Windows PowerShell ISE a Windows PowerShellben.</span><span class="sxs-lookup"><span data-stu-id="c23be-110">The following table lists the new and changed features for this release of Windows PowerShell ISE in Windows PowerShell.</span></span>

|<span data-ttu-id="c23be-111">Szolgáltatás/funkció</span><span class="sxs-lookup"><span data-stu-id="c23be-111">Feature/functionality</span></span>|<span data-ttu-id="c23be-112">A Windows PowerShell ISE 4.0</span><span class="sxs-lookup"><span data-stu-id="c23be-112">Windows PowerShell ISE 4.0</span></span>|<span data-ttu-id="c23be-113">A Windows PowerShell ISE 3.0</span><span class="sxs-lookup"><span data-stu-id="c23be-113">Windows PowerShell ISE 3.0</span></span>|<span data-ttu-id="c23be-114">A Windows PowerShell ISE 2.0</span><span class="sxs-lookup"><span data-stu-id="c23be-114">Windows PowerShell ISE 2.0</span></span>|
|--------------------------|-----------------------------------------------|-----------------------------------------------|-----------------------------------------------|
|<span data-ttu-id="c23be-115">**[IntelliSense](#intellisense)**</span><span class="sxs-lookup"><span data-stu-id="c23be-115">**[IntelliSense](#intellisense)**</span></span>|<span data-ttu-id="c23be-116">X</span><span class="sxs-lookup"><span data-stu-id="c23be-116">X</span></span>|<span data-ttu-id="c23be-117">X</span><span class="sxs-lookup"><span data-stu-id="c23be-117">X</span></span>||
|<span data-ttu-id="c23be-118">**[Részletek](#snippets)**</span><span class="sxs-lookup"><span data-stu-id="c23be-118">**[Snippets](#snippets)**</span></span>|<span data-ttu-id="c23be-119">X</span><span class="sxs-lookup"><span data-stu-id="c23be-119">X</span></span>|<span data-ttu-id="c23be-120">X</span><span class="sxs-lookup"><span data-stu-id="c23be-120">X</span></span>||
|<span data-ttu-id="c23be-121">**[Bővítmény eszközök](#add-on-tools)**</span><span class="sxs-lookup"><span data-stu-id="c23be-121">**[Add-on Tools](#add-on-tools)**</span></span>|<span data-ttu-id="c23be-122">X</span><span class="sxs-lookup"><span data-stu-id="c23be-122">X</span></span>|<span data-ttu-id="c23be-123">X</span><span class="sxs-lookup"><span data-stu-id="c23be-123">X</span></span>||
|<span data-ttu-id="c23be-124">**[Indítsa újra a Manager és az automatikus mentés](#restart-manager-and-auto-save)**</span><span class="sxs-lookup"><span data-stu-id="c23be-124">**[Restart Manager and Auto-save](#restart-manager-and-auto-save)**</span></span>|<span data-ttu-id="c23be-125">X</span><span class="sxs-lookup"><span data-stu-id="c23be-125">X</span></span>|<span data-ttu-id="c23be-126">X</span><span class="sxs-lookup"><span data-stu-id="c23be-126">X</span></span>||
|<span data-ttu-id="c23be-127">**[A legtöbb-legutóbbi listája](#most-recently-used-list)**</span><span class="sxs-lookup"><span data-stu-id="c23be-127">**[Most-recently used list](#most-recently-used-list)**</span></span>|<span data-ttu-id="c23be-128">X</span><span class="sxs-lookup"><span data-stu-id="c23be-128">X</span></span>|<span data-ttu-id="c23be-129">X</span><span class="sxs-lookup"><span data-stu-id="c23be-129">X</span></span>||
|<span data-ttu-id="c23be-130">**[Konzol ablaktáblában](#console-pane)**</span><span class="sxs-lookup"><span data-stu-id="c23be-130">**[Console Pane](#console-pane)**</span></span>|<span data-ttu-id="c23be-131">X</span><span class="sxs-lookup"><span data-stu-id="c23be-131">X</span></span>|<span data-ttu-id="c23be-132">X</span><span class="sxs-lookup"><span data-stu-id="c23be-132">X</span></span>||
|<span data-ttu-id="c23be-133">**[Parancssori kapcsolók](#command-line-switches)**</span><span class="sxs-lookup"><span data-stu-id="c23be-133">**[Command-line switches](#command-line-switches)**</span></span>|<span data-ttu-id="c23be-134">X</span><span class="sxs-lookup"><span data-stu-id="c23be-134">X</span></span>|<span data-ttu-id="c23be-135">X</span><span class="sxs-lookup"><span data-stu-id="c23be-135">X</span></span>||
|<span data-ttu-id="c23be-136">**[Új szerkesztő szolgáltatások](#new-editor-features)**</span><span class="sxs-lookup"><span data-stu-id="c23be-136">**[New editor features](#new-editor-features)**</span></span>|<span data-ttu-id="c23be-137">X</span><span class="sxs-lookup"><span data-stu-id="c23be-137">X</span></span>|<span data-ttu-id="c23be-138">X</span><span class="sxs-lookup"><span data-stu-id="c23be-138">X</span></span>||
|<span data-ttu-id="c23be-139">**[Új súgó-megjelenítő ablakban](#new-help-viewer-window)**</span><span class="sxs-lookup"><span data-stu-id="c23be-139">**[New Help viewer window](#new-help-viewer-window)**</span></span>|<span data-ttu-id="c23be-140">X</span><span class="sxs-lookup"><span data-stu-id="c23be-140">X</span></span>|<span data-ttu-id="c23be-141">X</span><span class="sxs-lookup"><span data-stu-id="c23be-141">X</span></span>||
|<span data-ttu-id="c23be-142">**[Megjelenítése-Command parancsmaggal](#show-command-cmdlet)**</span><span class="sxs-lookup"><span data-stu-id="c23be-142">**[Show-Command cmdlet](#show-command-cmdlet)**</span></span>|<span data-ttu-id="c23be-143">X</span><span class="sxs-lookup"><span data-stu-id="c23be-143">X</span></span>|<span data-ttu-id="c23be-144">X</span><span class="sxs-lookup"><span data-stu-id="c23be-144">X</span></span>||

### <a name="intellisense"></a><span data-ttu-id="c23be-145">IntelliSense</span><span class="sxs-lookup"><span data-stu-id="c23be-145">IntelliSense</span></span>
<span data-ttu-id="c23be-146">**A hozzáadott ISE 3.0**</span><span class="sxs-lookup"><span data-stu-id="c23be-146">**Added in ISE 3.0**</span></span>

<span data-ttu-id="c23be-147">IntelliSense az automatikus-végrehajtási segítséget szolgáltatása, amely része a Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="c23be-147">IntelliSense is an automatic-completion assistance feature that is part of Windows PowerShell ISE.</span></span> <span data-ttu-id="c23be-148">IntelliSense megjeleníti a parancsmagok, paraméterek, a paraméterértékek, fájlok vagy mappák potenciálisan megfelelő beíráskor kattintható menük.</span><span class="sxs-lookup"><span data-stu-id="c23be-148">IntelliSense displays clickable menus of potentially matching cmdlets, parameters, parameter values, files, or folders as you type.</span></span>

<span data-ttu-id="c23be-149">**Milyen hozzáadott értéket nyújt ez a változás?**</span><span class="sxs-lookup"><span data-stu-id="c23be-149">**What value does this change add?**</span></span>

<span data-ttu-id="c23be-150">IntelliSense hozzáadásával ezért könnyebben parancsmagok és szintaxis észleléséhez, amikor a Windows PowerShell ISE parancsfájlok létrehozására használhatja.</span><span class="sxs-lookup"><span data-stu-id="c23be-150">With the addition of IntelliSense, it is easier to discover cmdlets and syntax when you use Windows PowerShell ISE to create scripts.</span></span> <span data-ttu-id="c23be-151">A Windows PowerShell ISE segítségével ismerje meg a Windows PowerShell új parancsfájlok létrehozása során.</span><span class="sxs-lookup"><span data-stu-id="c23be-151">You can also use Windows PowerShell ISE to learn Windows PowerShell while you create new scripts.</span></span>

<span data-ttu-id="c23be-152">**Mi működik másképp?**</span><span class="sxs-lookup"><span data-stu-id="c23be-152">**What works differently?**</span></span>

<span data-ttu-id="c23be-153">Amikor beírja parancsmagok a Windows PowerShell ISE 3.0-s vagy újabb, egy görgethető és kattintható menü jeleníti meg, keresse meg és jelölje ki a megfelelő parancsokat.</span><span class="sxs-lookup"><span data-stu-id="c23be-153">When you type cmdlets in the Windows PowerShell ISE 3.0 or later, a scrollable and clickable menu displays, allowing you to browse and select the appropriate commands.</span></span>

### <a name="snippets"></a><span data-ttu-id="c23be-154">Részletek</span><span class="sxs-lookup"><span data-stu-id="c23be-154">Snippets</span></span>
<span data-ttu-id="c23be-155">**A hozzáadott ISE 3.0**</span><span class="sxs-lookup"><span data-stu-id="c23be-155">**Added in ISE 3.0**</span></span>

<span data-ttu-id="c23be-156">*Kódtöredékek* a Windows PowerShell-kódot hoz létre a Windows PowerShell ISE parancsfájlok beilleszthet rövid szakaszok is vannak.</span><span class="sxs-lookup"><span data-stu-id="c23be-156">*Snippets* are short sections of Windows PowerShell code that you can insert into the scripts you create in Windows PowerShell ISE.</span></span> <span data-ttu-id="c23be-157">A Windows PowerShell ISE kódtöredékek alapértelmezett készletét tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="c23be-157">Windows PowerShell ISE comes with a default set of snippets.</span></span> <span data-ttu-id="c23be-158">Kódtöredékek használatával adhat hozzá a **New-részlet** parancsmag a Windows PowerShell ISE végzett munka közben.</span><span class="sxs-lookup"><span data-stu-id="c23be-158">You can add snippets by using the **New-Snippet** cmdlet while working in Windows PowerShell ISE.</span></span>

<span data-ttu-id="c23be-159">**Milyen hozzáadott értéket nyújt ez a változás?**</span><span class="sxs-lookup"><span data-stu-id="c23be-159">**What value does this change add?**</span></span>

<span data-ttu-id="c23be-160">Részletek segítségével gyorsan állítson össze és automatizálását a környezetében parancsfájlokat hozhatnak létre.</span><span class="sxs-lookup"><span data-stu-id="c23be-160">By using snippets, you can quickly assemble and create scripts to automate your environment.</span></span>

<span data-ttu-id="c23be-161">**Mi működik másképp?**</span><span class="sxs-lookup"><span data-stu-id="c23be-161">**What works differently?**</span></span>

<span data-ttu-id="c23be-162">Kódtöredékek használata a Windows PowerShell 3.0-s vagy újabb, a **szerkesztése** menüben kattintson a **Start kódtöredékek**, vagy nyomja le az ENTER **Ctrl-J**.</span><span class="sxs-lookup"><span data-stu-id="c23be-162">To use snippets in Windows PowerShell 3.0 or later, on the **Edit** menu, click **Start Snippets**, or press **Ctrl-J**.</span></span>

### <a name="add-on-tools"></a><span data-ttu-id="c23be-163">Bővítmény eszközök</span><span class="sxs-lookup"><span data-stu-id="c23be-163">Add-on tools</span></span>
<span data-ttu-id="c23be-164">**A PowerShell 3.0 hozzáadva**</span><span class="sxs-lookup"><span data-stu-id="c23be-164">**Added in PowerShell 3.0**</span></span>

<span data-ttu-id="c23be-165">A Windows PowerShell ISE mostantól támogatja a bővítmény eszközök, amelyek Windows megjelenítési alaprendszer (WPF) vezérlők, amelyek felhasználásával a hálózatiobjektum-modellt.</span><span class="sxs-lookup"><span data-stu-id="c23be-165">Windows PowerShell ISE now supports add-on tools, which are Windows Presentation Foundation (WPF) controls that are added by using the object model.</span></span> <span data-ttu-id="c23be-166">Bővítmények megjelenítése a konzol egy függőleges vagy vízszintes ablaktáblát.</span><span class="sxs-lookup"><span data-stu-id="c23be-166">Add-on tools can be displayed as a vertical or horizontal pane in the console.</span></span> <span data-ttu-id="c23be-167">Lapokra vezérlőként több bővítmény eszközök ablaktáblában jelennek meg.</span><span class="sxs-lookup"><span data-stu-id="c23be-167">Multiple add-on tools in a pane are displayed as a tabbed control.</span></span> <span data-ttu-id="c23be-168">Hozzáadhat, vagy távolítsa el a bővítmény eszközök, amelyek a Microsofton kívüli más felek hozzák létre.</span><span class="sxs-lookup"><span data-stu-id="c23be-168">You can also add or remove add-on tools that are produced by non-Microsoft parties.</span></span> <span data-ttu-id="c23be-169">Importálandó, vagy távolítsa el a bővítmény eszközök kapcsolatos további információkért lásd: [Windows PowerShell ISE műveletek](http://technet.microsoft.com/library/cc732148.aspx).</span><span class="sxs-lookup"><span data-stu-id="c23be-169">For more information about how to import or remove add-on tools, see [Windows PowerShell ISE Operations](http://technet.microsoft.com/library/cc732148.aspx).</span></span>

<span data-ttu-id="c23be-170">**Milyen hozzáadott értéket nyújt ez a változás?**</span><span class="sxs-lookup"><span data-stu-id="c23be-170">**What value does this change add?**</span></span>

<span data-ttu-id="c23be-171">A bővítmények lehetővé teszik bővíthető és testreszabható a Windows PowerShell ISE, amelyek a parancsfájl-kezelési élmény javítása érdekében vagy funkciókat adnak hozzá a Windows PowerShell ISE eszközökkel.</span><span class="sxs-lookup"><span data-stu-id="c23be-171">Add-ons allow you to extend and customize Windows PowerShell ISE with tools that can enhance your scripting experience or add functionality to Windows PowerShell ISE.</span></span>

<span data-ttu-id="c23be-172">**Mi működik másképp?**</span><span class="sxs-lookup"><span data-stu-id="c23be-172">**What works differently?**</span></span>

<span data-ttu-id="c23be-173">A Windows PowerShell ISE 3.0-s és újabb verziói rendelkeznek a **parancsok** bővítmény.</span><span class="sxs-lookup"><span data-stu-id="c23be-173">Windows PowerShell ISE 3.0 and later come with the **Commands** add-on.</span></span> <span data-ttu-id="c23be-174">A **parancsok** bővítmény lehetővé teszi a parancsmagok keresse meg és érheti el a parancsmagok-mellé a vonatkozó súgó megjelenítéséhez a **parancsfájl** és **konzol** ablaktábla.</span><span class="sxs-lookup"><span data-stu-id="c23be-174">The **Commands** add-on allows you to browse cmdlets, and access help about the cmdlets side-by-side with the **Script** and **Console** Panes.</span></span>

<span data-ttu-id="c23be-175">További bővítmények található használatával a **bővítmény eszközök webhely megnyitása** parancs a **bővítmények** menü.</span><span class="sxs-lookup"><span data-stu-id="c23be-175">Additional add-ons can be found by using the **Open Add-on Tools Website** command on the **Add-ons** menu.</span></span>

### <a name="restart-manager-and-auto-save"></a><span data-ttu-id="c23be-176">Indítsa újra a manager és az automatikus mentés</span><span class="sxs-lookup"><span data-stu-id="c23be-176">Restart manager and auto-save</span></span>
<span data-ttu-id="c23be-177">**A PowerShell 3.0 hozzáadva**</span><span class="sxs-lookup"><span data-stu-id="c23be-177">**Added in PowerShell 3.0**</span></span>

<span data-ttu-id="c23be-178">Windows PowerShell ISE mostantól automatikusan menti a Megnyitás parancsfájlokba két percenként másik helyen.</span><span class="sxs-lookup"><span data-stu-id="c23be-178">Windows PowerShell ISE now automatically saves your open scripts every two minutes, in a separate location.</span></span>  <span data-ttu-id="c23be-179">Ha a Windows PowerShell ISE nem működik, vagy ha az operációs rendszer újraindítása után a Windows PowerShell ISE újraindul, helyreállítja parancsfájlok, melyeket nyissa meg az utolsó munkamenetnek, még akkor is, ha a parancsfájlok nem sikerült menteni.</span><span class="sxs-lookup"><span data-stu-id="c23be-179">If Windows PowerShell ISE stops working, or if the operating system is restarted, after Windows PowerShell ISE restarts, it recovers scripts that were open in the last session, even if the scripts were not saved.</span></span>

<span data-ttu-id="c23be-180">Az automatikus mentése időköz módosításához futtassa a következő parancsot a konzol ablaktáblában: **$psise. Options.AutoSaveMinuteInterval**.</span><span class="sxs-lookup"><span data-stu-id="c23be-180">To change the automatic saving interval, run the following command in the Console pane: **$psise.Options.AutoSaveMinuteInterval**.</span></span>

<span data-ttu-id="c23be-181">**Milyen hozzáadott értéket nyújt ez a változás?**</span><span class="sxs-lookup"><span data-stu-id="c23be-181">**What value does this change add?**</span></span>

<span data-ttu-id="c23be-182">Most már dolgozhat ismerete, hogy a Megnyitás parancsfájlokba automatikusan menti a rendszer váratlan újraindítása esetén a Windows PowerShell ISE belül.</span><span class="sxs-lookup"><span data-stu-id="c23be-182">You can now work within Windows PowerShell ISE knowing that your open scripts are automatically saved in the event of an unexpected restart.</span></span>

<span data-ttu-id="c23be-183">**Mi működik másképp?**</span><span class="sxs-lookup"><span data-stu-id="c23be-183">**What works differently?**</span></span>

<span data-ttu-id="c23be-184">A Windows PowerShell ISE 2.0 nem menti a parancsfájlok automatikusan esetén a számítógép újraindítását.</span><span class="sxs-lookup"><span data-stu-id="c23be-184">Windows PowerShell ISE 2.0 does not save the scripts automatically in the event of a restart.</span></span>

### <a name="most-recently-used-list"></a><span data-ttu-id="c23be-185">A legtöbb-legutóbbi listája</span><span class="sxs-lookup"><span data-stu-id="c23be-185">Most-recently used list</span></span>
<span data-ttu-id="c23be-186">**A PowerShell 3.0 hozzáadva**</span><span class="sxs-lookup"><span data-stu-id="c23be-186">**Added in PowerShell 3.0**</span></span>

<span data-ttu-id="c23be-187">Windows PowerShell ISE most már rendelkezik a legtöbb legutóbb használt fájlok listáját.</span><span class="sxs-lookup"><span data-stu-id="c23be-187">Windows PowerShell ISE now has a most-recently used list for files.</span></span> <span data-ttu-id="c23be-188">Amikor megnyit egy fájlt a Windows PowerShell ISE, a fájl kerül a legtöbb legutóbb használt lista a a **fájl** menü.</span><span class="sxs-lookup"><span data-stu-id="c23be-188">When you open a file in Windows PowerShell ISE, the file is added to the most-recently used list on the **File** menu.</span></span>

<span data-ttu-id="c23be-189">A legtöbb legutóbb használt fájlok alapértelmezett számának módosításához, futtassa a következő parancsot a konzol ablaktáblában: **$psise. Options.MruCount**.</span><span class="sxs-lookup"><span data-stu-id="c23be-189">To change the default number of files in the most-recently used list, run the following command in the Console Pane: **$psise.Options.MruCount**.</span></span>

<span data-ttu-id="c23be-190">**Milyen hozzáadott értéket nyújt ez a változás?**</span><span class="sxs-lookup"><span data-stu-id="c23be-190">**What value does this change add?**</span></span>

<span data-ttu-id="c23be-191">A legtöbb legutóbb használt lista segítségével mostantól egyszerűen hozzáférhessenek a gyakran használt fájlokat.</span><span class="sxs-lookup"><span data-stu-id="c23be-191">You can now use the most-recently used list to easily access your frequently-used files.</span></span>

<span data-ttu-id="c23be-192">**Mi működik másképp?**</span><span class="sxs-lookup"><span data-stu-id="c23be-192">**What works differently?**</span></span>

<span data-ttu-id="c23be-193">A Windows PowerShell ISE 2.0 nem rendelkezik a legtöbb legutóbb használt listáját.</span><span class="sxs-lookup"><span data-stu-id="c23be-193">Windows PowerShell ISE 2.0 does not have a most-recently used list.</span></span>

### <a name="console-pane"></a><span data-ttu-id="c23be-194">Konzol ablaktáblában</span><span class="sxs-lookup"><span data-stu-id="c23be-194">Console Pane</span></span>
<span data-ttu-id="c23be-195">**A PowerShell 3.0 hozzáadva**</span><span class="sxs-lookup"><span data-stu-id="c23be-195">**Added in PowerShell 3.0**</span></span>

<span data-ttu-id="c23be-196">A külön parancs és a kimeneti ablaktábla elérhető Windows PowerShell ISE első kiadása már megtörtént egyesített konzol egytáblás.</span><span class="sxs-lookup"><span data-stu-id="c23be-196">The separate Command and Output Panes that were available in the first release of Windows PowerShell ISE have been combined into a single Console Pane.</span></span> <span data-ttu-id="c23be-197">A konzol ablaktáblában függvény és egy tipikus Windows PowerShell-konzolba megjelenése hasonló, de (a legtöbb ebben a témakörben ismertetett) a következő fejlesztéseket tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="c23be-197">The Console Pane is similar in function and appearance to a typical Windows PowerShell console, but it includes the following enhancements (most are described in this topic).</span></span>

- <span data-ttu-id="c23be-198">Zintaxisszínek bemeneti szöveg (kimeneti szöveg nem), beleértve az XML-szintaxis</span><span class="sxs-lookup"><span data-stu-id="c23be-198">Syntax coloring for input text (not output text), including XML syntax</span></span>

- <span data-ttu-id="c23be-199">IntelliSense</span><span class="sxs-lookup"><span data-stu-id="c23be-199">IntelliSense</span></span>

- <span data-ttu-id="c23be-200">Megfelelő zárójel</span><span class="sxs-lookup"><span data-stu-id="c23be-200">Brace matching</span></span>

- <span data-ttu-id="c23be-201">Hiba arra utal, hogy</span><span class="sxs-lookup"><span data-stu-id="c23be-201">Error indication</span></span>

- <span data-ttu-id="c23be-202">Teljes Unicode-támogatás</span><span class="sxs-lookup"><span data-stu-id="c23be-202">Full Unicode support</span></span>

- <span data-ttu-id="c23be-203">**F1** környezetfüggő súgó</span><span class="sxs-lookup"><span data-stu-id="c23be-203">**F1** context-sensitive help</span></span>

- <span data-ttu-id="c23be-204">**CTRL + F1** környezetfüggő megjelenítése-parancs</span><span class="sxs-lookup"><span data-stu-id="c23be-204">**Ctrl+F1** context-sensitive Show-Command</span></span>

- <span data-ttu-id="c23be-205">Összetett parancsfájl és jobbról balra támogatás</span><span class="sxs-lookup"><span data-stu-id="c23be-205">Complex script and right-to-left support</span></span>

- <span data-ttu-id="c23be-206">Betűtípus-támogatás</span><span class="sxs-lookup"><span data-stu-id="c23be-206">Font support</span></span>

- <span data-ttu-id="c23be-207">Nagyítás</span><span class="sxs-lookup"><span data-stu-id="c23be-207">Zoom</span></span>

- <span data-ttu-id="c23be-208">Vonal-válassza ki, és a blokk-válassza módok</span><span class="sxs-lookup"><span data-stu-id="c23be-208">Line-select and block-select modes</span></span>

- <span data-ttu-id="c23be-209">A parancssorban megnyomásakor beírt tartalom megőrzése a **mentése** mutató nyílra kattintva a konzol előzményeinek megtekintése</span><span class="sxs-lookup"><span data-stu-id="c23be-209">Preservation of typed content at the command line when you press the **Up** arrow to view history in the console</span></span>

<span data-ttu-id="c23be-210">**Milyen hozzáadott értéket nyújt ez a változás?**</span><span class="sxs-lookup"><span data-stu-id="c23be-210">**What value does this change add?**</span></span>

<span data-ttu-id="c23be-211">A konzol ablaktáblában módosítások hozzáadását, amely több azonos-e a konzol felületét parancsfájl-kezelési élményt nyújt.</span><span class="sxs-lookup"><span data-stu-id="c23be-211">The addition of these Console Pane changes provides a scripting experience that is more consistent with the console interface.</span></span>

<span data-ttu-id="c23be-212">**Mi működik másképp?**</span><span class="sxs-lookup"><span data-stu-id="c23be-212">**What works differently?**</span></span>

<span data-ttu-id="c23be-213">A Windows PowerShell ISE 2.0 rendelkezik, külön parancs és a kimeneti ablaktábla.</span><span class="sxs-lookup"><span data-stu-id="c23be-213">Windows PowerShell ISE 2.0 has separate Command and Output Panes.</span></span>

### <a name="command-line-switches"></a><span data-ttu-id="c23be-214">Parancssori kapcsolók</span><span class="sxs-lookup"><span data-stu-id="c23be-214">Command-line switches</span></span>
<span data-ttu-id="c23be-215">**A PowerShell 3.0 hozzáadva**</span><span class="sxs-lookup"><span data-stu-id="c23be-215">**Added in PowerShell 3.0**</span></span>

<span data-ttu-id="c23be-216">Ha a parancssorból indítsa el a Windows PowerShell ISE (írja be a **powershell_ise.exe**), a következő új parancssori kapcsolókat is hozzáadhat.</span><span class="sxs-lookup"><span data-stu-id="c23be-216">If you start Windows PowerShell ISE from the command line (by typing **powershell_ise.exe**), you can add the following new command-line switches.</span></span>

- <span data-ttu-id="c23be-217">*-NoProfile*: elindul a Windows PowerShell ISE futtatása nélkül **$profile**</span><span class="sxs-lookup"><span data-stu-id="c23be-217">*-NoProfile*: Starts Windows PowerShell ISE without running **$profile**</span></span>

- <span data-ttu-id="c23be-218">*-Súgó*: a súgóablak megjelenítése</span><span class="sxs-lookup"><span data-stu-id="c23be-218">*-Help*: Displays a Help window</span></span>

- <span data-ttu-id="c23be-219">*-mta*: Windows PowerShell ISE többszálas apartman módban indul.</span><span class="sxs-lookup"><span data-stu-id="c23be-219">*-mta*: Starts Windows PowerShell ISE in multithreaded apartment mode.</span></span> <span data-ttu-id="c23be-220">Az alapértelmezett működési mód a Windows PowerShell ISE egyszálas apartman módban, vagy *- sta*.</span><span class="sxs-lookup"><span data-stu-id="c23be-220">The default operation mode for Windows PowerShell ISE is single-threaded apartment mode, or *-sta*.</span></span>

<span data-ttu-id="c23be-221">**Milyen hozzáadott értéket nyújt ez a változás?**</span><span class="sxs-lookup"><span data-stu-id="c23be-221">**What value does this change add?**</span></span>

<span data-ttu-id="c23be-222">A parancssori kapcsolók hozzáadása lehetővé teszi, hogy a környezet, amelyben a Windows PowerShell ISE fut. szabályozzák.</span><span class="sxs-lookup"><span data-stu-id="c23be-222">The addition of these command-line switches allows you to control the environment in which the Windows PowerShell ISE runs.</span></span>

<span data-ttu-id="c23be-223">**Mi működik másképp?**</span><span class="sxs-lookup"><span data-stu-id="c23be-223">**What works differently?**</span></span>

<span data-ttu-id="c23be-224">A Windows PowerShell ISE 2.0 nem ismeri fel a parancssori kapcsolók.</span><span class="sxs-lookup"><span data-stu-id="c23be-224">Windows PowerShell ISE 2.0 does not recognize these command-line switches.</span></span>

### <a name="new-editor-features"></a><span data-ttu-id="c23be-225">Új szerkesztő szolgáltatások</span><span class="sxs-lookup"><span data-stu-id="c23be-225">New editor features</span></span>
<span data-ttu-id="c23be-226">**A PowerShell 3.0 hozzáadva**</span><span class="sxs-lookup"><span data-stu-id="c23be-226">**Added in PowerShell 3.0**</span></span>

<span data-ttu-id="c23be-227">Más Windows PowerShell ISE szerkesztési funkciói a következők:</span><span class="sxs-lookup"><span data-stu-id="c23be-227">Other Windows PowerShell ISE editing features include:</span></span>

- <span data-ttu-id="c23be-228">**XML-zintaxisszínek**Windows PowerShell ISE most színek XML szintaxis ugyanúgy, mint azt a Windows PowerShell-szintaxis színek.</span><span class="sxs-lookup"><span data-stu-id="c23be-228">**XML syntax coloring**Windows PowerShell ISE now colors XML syntax in the same way as it colors Windows PowerShell syntax.</span></span>

- <span data-ttu-id="c23be-229">**Megfelelő zárójel** Windows PowerShell ISE megfelelő zárójel és kiemelve, és a következőképpen használható: (használata esetén például a **egyezés Ugrás** parancs vagy **Ctrl +]** talál a záró zárójel, ha egy kijelölt nyitó zárójel).</span><span class="sxs-lookup"><span data-stu-id="c23be-229">**Brace matching** Windows PowerShell ISE includes brace matching and highlighting, and can be used in the following ways: (for example, using the **Go to Match** command or **Ctrl + ]** locates the closing brace, if you have an opening brace selected).</span></span>

- <span data-ttu-id="c23be-230">**Vázlat nézetben** a parancssori panelbe támogatja, tagolás, amely lehetővé teszi, hogy összecsukás és kód szakasza Kibontás plusz vagy mínusz kattintva jelentkezik be a bal margó.</span><span class="sxs-lookup"><span data-stu-id="c23be-230">**Outline view** The Script Pane supports outlining, which allows collapsing or expanding sections of code by clicking plus or minus signs in the left margin.</span></span> <span data-ttu-id="c23be-231">Használhatja a kapcsos zárójelek vagy a **#region** és **#endregion** címkék elején vagy végén egy összecsukható szakasz megjelölni.</span><span class="sxs-lookup"><span data-stu-id="c23be-231">You can use braces or the **#region** and **#endregion** tags to mark the beginning or end of a collapsible section.</span></span> <span data-ttu-id="c23be-232">Kibontásához vagy összecsukásához minden egyes, nyomja le az **Ctrl + M**.</span><span class="sxs-lookup"><span data-stu-id="c23be-232">To expand or collapse all regions, press **Ctrl + M**.</span></span>

- <span data-ttu-id="c23be-233">**Áthúzása szöveg szerkesztése**Windows PowerShell ISE most támogatja áthúzása szöveg szerkesztése.</span><span class="sxs-lookup"><span data-stu-id="c23be-233">**Drag and drop text editing**Windows PowerShell ISE now supports drag and drop text editing.</span></span> <span data-ttu-id="c23be-234">Jelöljön ki egyetlen szövegrészt, és húzza a szöveget a szerkesztő vagy a konzol a szöveg áthelyezése egy másik helyre.</span><span class="sxs-lookup"><span data-stu-id="c23be-234">You can select any block of text and drag that text to another location in the editor or the console to move the text.</span></span> <span data-ttu-id="c23be-235">Ha lenyomva tartja a Ctrl billentyűt, miközben a kijelölt szöveg az egérgomb felengedésekor a szöveget az új helyre másolódik.</span><span class="sxs-lookup"><span data-stu-id="c23be-235">If you hold down the Ctrl key while you drag the selected text, when you release the mouse button the text is copied to the new location.</span></span> <span data-ttu-id="c23be-236">Ebben a Windows PowerShell ISE, valamint a Windows PowerShell ISE korábbi verzióját, a Windows PowerShell ISE fájlokat áthúzása Windows PowerShell ISE megnyitja a fájlt.</span><span class="sxs-lookup"><span data-stu-id="c23be-236">In this version of Windows PowerShell ISE, as well as the previous version of Windows PowerShell ISE, when you drag and drop files onto Windows PowerShell ISE, Windows PowerShell ISE opens the file.</span></span>

- <span data-ttu-id="c23be-237">**Elemzési hiba megjelenítési** piros aláhúzás jelöl, elemzési hibákat.</span><span class="sxs-lookup"><span data-stu-id="c23be-237">**Parse error display** Parse errors are indicated with red underlines.</span></span> <span data-ttu-id="c23be-238">Ha hibát jelzett, telepített mutat, elemleírás jelenik meg a probléma megoldására a kódban található.</span><span class="sxs-lookup"><span data-stu-id="c23be-238">When you hover over an indicated error, tooltip text displays the problem that was found in the code.</span></span>

- <span data-ttu-id="c23be-239">**Nagyítás** nagyítás százalékos aránya a konzol "™ s tartalom állítható be a nagyítási csúszkát (a jobb alsó sarkában Windows PowerShell ISE ablaka), vagy a parancs **$psise.options.Zoom** a konzol ablaktáblában.</span><span class="sxs-lookup"><span data-stu-id="c23be-239">**Zoom** The zoom percentage of the console'™s content can be set by using the zoom slider (in the lower right corner of Windows PowerShell ISE window), or by entering the command **$psise.options.Zoom** in the Console Pane.</span></span>

- <span data-ttu-id="c23be-240">**Rich text másolás és Beillesztés** a betűtípus mérete és szín adatokat az eredeti kijelölés a Windows PowerShell ISE megtartja a vágólapra másolása.</span><span class="sxs-lookup"><span data-stu-id="c23be-240">**Rich text copy and paste** Copying to the clipboard in Windows PowerShell ISE preserves the font, size, and color information of the original selection.</span></span>

- <span data-ttu-id="c23be-241">**Kijelölés blokkolása** szövegblokk választhatja ki a parancsfájl ablaktáblán az egérrel szöveg kijelölése közben az ALT billentyűt lenyomva tartja, vagy billentyűkombináció lenyomásával **Alt + Shift + mutató nyílra**.</span><span class="sxs-lookup"><span data-stu-id="c23be-241">**Block selection** You can select a block of text by holding down the ALT key while selecting text in the Script Pane with your mouse, or by pressing **Alt+Shift+Arrow**.</span></span>

<span data-ttu-id="c23be-242">**Milyen hozzáadott értéket nyújt ez a változás?**</span><span class="sxs-lookup"><span data-stu-id="c23be-242">**What value does this change add?**</span></span>

<span data-ttu-id="c23be-243">A további szerkesztési funkcióival egy egységes és hatékony szerkesztési környezetben.</span><span class="sxs-lookup"><span data-stu-id="c23be-243">The additional editing features provide a more consistent and powerful editing environment.</span></span>

<span data-ttu-id="c23be-244">**Mi működik másképp?**</span><span class="sxs-lookup"><span data-stu-id="c23be-244">**What works differently?**</span></span>

<span data-ttu-id="c23be-245">Szerkesztési fejlesztéseknek nem volt megtalálható a Windows PowerShell ISE 2.0.</span><span class="sxs-lookup"><span data-stu-id="c23be-245">These editing enhancements were not present in Windows PowerShell ISE 2.0.</span></span>

### <a name="new-help-viewer-window"></a><span data-ttu-id="c23be-246">Új súgó-megjelenítő ablakban</span><span class="sxs-lookup"><span data-stu-id="c23be-246">New Help viewer window</span></span>
<span data-ttu-id="c23be-247">**A PowerShell 3.0 hozzáadva**</span><span class="sxs-lookup"><span data-stu-id="c23be-247">**Added in PowerShell 3.0**</span></span>

<span data-ttu-id="c23be-248">Ha lenyomja az **F1** parancsmag a kurzor áll, vagy van kiemelve parancsmag részét, az új súgómegjelenítő nyílik meg a kijelölt parancsmag vonatkozó környezetfüggő súgó.</span><span class="sxs-lookup"><span data-stu-id="c23be-248">If you press **F1** when your cursor is in a cmdlet, or you have part of a cmdlet highlighted, the new Help viewer opens context-sensitive Help about the highlighted cmdlet.</span></span> <span data-ttu-id="c23be-249">A Windows PowerShell vonatkozó súgó megjelenítéséhez írja be **operátorok** a konzol ablaktáblában, majd nyomja le az **F1**.</span><span class="sxs-lookup"><span data-stu-id="c23be-249">To display Windows PowerShell About help, type  **operators** in the console pane, and then press **F1**.</span></span>

<span data-ttu-id="c23be-250">Ez a funkció használatához Windows PowerShell súgója témakörök legújabb verziója letölthető a Microsoft webhelyén.</span><span class="sxs-lookup"><span data-stu-id="c23be-250">Before you use this feature, download the most current version of Windows PowerShell Help topics from the Microsoft website.</span></span> <span data-ttu-id="c23be-251">A legegyszerűbb módja, ha a súgótémakörök letöltése futtatni a **Update-Help** parancsmag a konzol ablaktáblában, ha fut a Windows PowerShell ISE rendszergazdaként.</span><span class="sxs-lookup"><span data-stu-id="c23be-251">The simplest method for downloading the Help topics is to run the **Update-Help** cmdlet in the Console Pane when running Windows PowerShell ISE as administrator.</span></span>

<span data-ttu-id="c23be-252">Hol megváltoztathatja a **F1** kulcs segítséget keres.</span><span class="sxs-lookup"><span data-stu-id="c23be-252">You can alter where the **F1** key looks for Help.</span></span> <span data-ttu-id="c23be-253">A a **eszközök**/**beállítások** menü, az a **általános beállítások** lap **egyéb beállítások**, állítsa be, vagy törölje a jelölőnégyzet **online tartalom helyett használja a helyi súgó tartalma**.</span><span class="sxs-lookup"><span data-stu-id="c23be-253">In the **Tools**/**Options** menu, on the **General Settings** tab, under **Other Settings**, you can set or clear the checkbox **Use local help content instead of online content**.</span></span> <span data-ttu-id="c23be-254">Ha be van jelölve, majd az ügyfél keresi a parancsmag segítségre van szüksége a letöltött súgó modulok mappában található.</span><span class="sxs-lookup"><span data-stu-id="c23be-254">If checked, then the client looks for the cmdlet Help in the downloaded Help found in the modules folder.</span></span>  <span data-ttu-id="c23be-255">Ha a jelölőnégyzet nincs bejelölve, majd az ügyfél jelenik meg a TechNet könyvtárban a parancsmag súgóját.</span><span class="sxs-lookup"><span data-stu-id="c23be-255">If the checkbox is cleared, then the client looks on the TechNet library for the cmdlet help.</span></span>

<span data-ttu-id="c23be-256">**Milyen hozzáadott értéket nyújt ez a változás?**</span><span class="sxs-lookup"><span data-stu-id="c23be-256">**What value does this change add?**</span></span>

<span data-ttu-id="c23be-257">Környezetfüggő súgó anélkül, hogy az aktuális parancsmag vagy parancsfájl tanulási zökkenőmentes élményt nyújt.</span><span class="sxs-lookup"><span data-stu-id="c23be-257">Context-sensitive Help without leaving your current cmdlet or script provides a seamless learning experience.</span></span>

<span data-ttu-id="c23be-258">**Mi működik másképp?**</span><span class="sxs-lookup"><span data-stu-id="c23be-258">**What works differently?**</span></span>

<span data-ttu-id="c23be-259">A súgófájl a helyi számítógépen a Windows PowerShell ISE korábbi verzióiban az F1 billentyű megnyomásával megnyitva.</span><span class="sxs-lookup"><span data-stu-id="c23be-259">Pressing F1 in previous versions of Windows PowerShell ISE opened the help file on the local computer.</span></span> <span data-ttu-id="c23be-260">A Windows PowerShell ISE 3.0-s és újabb verziók megnyílik egy ablak, amely tartalmazza a parancsmag, amely kereshető és konfigurálható a Súgó gombra.</span><span class="sxs-lookup"><span data-stu-id="c23be-260">In Windows PowerShell ISE 3.0 and later, a window opens that contains the help for the cmdlet that is searchable and configurable.</span></span> <span data-ttu-id="c23be-261">A Súgó élmény új Windows PowerShell ISE 3.0, és új Windows PowerShell 3.0 frissített súgó.</span><span class="sxs-lookup"><span data-stu-id="c23be-261">This Help experience is new for Windows PowerShell ISE 3.0, and Updatable Help is new for Windows PowerShell 3.0.</span></span>

### <a name="show-command-cmdlet"></a><span data-ttu-id="c23be-262">Megjelenítése-Command parancsmaggal</span><span class="sxs-lookup"><span data-stu-id="c23be-262">Show-Command cmdlet</span></span>
<span data-ttu-id="c23be-263">**A PowerShell 3.0 hozzáadva**</span><span class="sxs-lookup"><span data-stu-id="c23be-263">**Added in PowerShell 3.0**</span></span>

<span data-ttu-id="c23be-264">A **megjelenítése-parancs** parancsmag lehetővé teszi állítható össze, vagy futtassa egy parancsmag vagy a függvény egy grafikus űrlap kitöltésével.</span><span class="sxs-lookup"><span data-stu-id="c23be-264">The **Show-Command** cmdlet enables you to compose or run a cmdlet or function by filling in a graphical form.</span></span> <span data-ttu-id="c23be-265">Az űrlap lehetővé teszi, hogy a felhasználók grafikus környezetben a Windows PowerShell-lel dolgozni.</span><span class="sxs-lookup"><span data-stu-id="c23be-265">The form lets users work with Windows PowerShell in a graphical environment.</span></span> <span data-ttu-id="c23be-266">**A parancs megjelenítése** is lehetővé teszi, hogy speciális, amely a gyors Windows PowerShell-alapú grafikus felhasználói felületének létrehozásához.</span><span class="sxs-lookup"><span data-stu-id="c23be-266">**Show-Command** also enables advanced scripters to create a quick Windows PowerShell-based GUI.</span></span>

<span data-ttu-id="c23be-267">**Milyen hozzáadott értéket nyújt ez a változás?**</span><span class="sxs-lookup"><span data-stu-id="c23be-267">**What value does this change add?**</span></span>

<span data-ttu-id="c23be-268">A **megjelenítése-parancs** a Windows PowerShell-parancsfájlok, megadhatja a felhasználók a grafikus környezet, amelyhez nem ismeri.</span><span class="sxs-lookup"><span data-stu-id="c23be-268">By using **Show-Command** in your Windows PowerShell scripts, you can provide your users with the graphical environment with which they are familiar.</span></span> <span data-ttu-id="c23be-269">**A parancs megjelenítése** is hozzájárulhat a bevezető felhasználók ismerje meg a Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c23be-269">**Show-Command** can also help introductory users learn Windows PowerShell.</span></span>

<span data-ttu-id="c23be-270">**Mi működik másképp?**</span><span class="sxs-lookup"><span data-stu-id="c23be-270">**What works differently?**</span></span>

<span data-ttu-id="c23be-271">Show-parancsot az új Windows PowerShell ISE 3.0.</span><span class="sxs-lookup"><span data-stu-id="c23be-271">Show-Command is new Windows PowerShell ISE 3.0.</span></span>

## <a name="see-also"></a><span data-ttu-id="c23be-272">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="c23be-272">See also</span></span>
<span data-ttu-id="c23be-273">A Windows PowerShell ISE a Windows PowerShell használatával kapcsolatos további információkért tekintse meg a következőket.</span><span class="sxs-lookup"><span data-stu-id="c23be-273">For more information about using Windows PowerShell ISE in Windows PowerShell, see the following links.</span></span>

- [<span data-ttu-id="c23be-274">A Windows PowerShell integrált parancsfájlkezelési környezet használata</span><span class="sxs-lookup"><span data-stu-id="c23be-274">Using the Windows PowerShell Integrated Scripting Environment</span></span>](../core-powershell/ise/Using-the-Windows-PowerShell-ISE.md)
- [<span data-ttu-id="c23be-275">A TechNet Wiki ISE</span><span class="sxs-lookup"><span data-stu-id="c23be-275">ISE on the TechNet Wiki</span></span>](http://social.technet.microsoft.com/wiki/search/searchresults.aspx?q=ISE)
- [<span data-ttu-id="c23be-276">Script Center</span><span class="sxs-lookup"><span data-stu-id="c23be-276">Script Center</span></span>](http://technet.microsoft.com/scriptcenter/default)

