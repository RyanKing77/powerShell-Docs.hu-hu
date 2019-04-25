---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: Újdonságai a PowerShell 50 ISE-ben
ms.assetid: 38648d47-7c27-4b37-a40e-ad29948519c2
ms.openlocfilehash: 2d953bc4553de7720c590304d29750b84a1ef3b2
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62058182"
---
# <a name="what39s-new-in-the-windows-powershell-ise"></a><span data-ttu-id="0caf3-103">Mi&#39;újdonságai a Windows PowerShell ISE-ben</span><span class="sxs-lookup"><span data-stu-id="0caf3-103">What&#39;s New in the Windows PowerShell ISE</span></span>
<span data-ttu-id="0caf3-104">Ez a témakör ismerteti a Windows PowerShell integrált parancsfájlkezelési környezet (ISE) verzióban bevezetett új és frissített funkciókat.</span><span class="sxs-lookup"><span data-stu-id="0caf3-104">This topic explains the new and updated features that have been introduced in versions of Windows PowerShell  Integrated Scripting Environment (ISE).</span></span>

## <a name="feature-description"></a><span data-ttu-id="0caf3-105">A szolgáltatás leírása</span><span class="sxs-lookup"><span data-stu-id="0caf3-105">Feature description</span></span>
<span data-ttu-id="0caf3-106">A Windows PowerShell ISE-ben egy fogadó alkalmazás, amely lehetővé teszi, hogy írási, futtatása és tesztelése a szkriptek és modulok grafikus és intuitív környezetben.</span><span class="sxs-lookup"><span data-stu-id="0caf3-106">The Windows PowerShell ISE is a host application that enables you to write, run, and test scripts and modules in a graphical and intuitive environment.</span></span> <span data-ttu-id="0caf3-107">Például a szintaxis-színezést, a legfontosabb jellemzők lapon befejezését, vizuális hibakeresési, Unicode-megfelelőség és környezetfüggő súgó gazdag parancsfájl-kezelési felületet biztosít.</span><span class="sxs-lookup"><span data-stu-id="0caf3-107">Key features such as syntax-coloring, tab completion, visual debugging, Unicode compliance, and context-sensitive Help provide a rich scripting experience.</span></span>

<span data-ttu-id="0caf3-108">Windows PowerShell ISE-ben áttekintését lásd: [Windows PowerShell integrált parancsfájlkezelési környezet áttekintése](https://technet.microsoft.com/library/3c1892c2-bf84-4cb6-af26-1f453be9e671).</span><span class="sxs-lookup"><span data-stu-id="0caf3-108">For an overview of Windows PowerShell ISE, see [Windows PowerShell Integrated Scripting Environment overview](https://technet.microsoft.com/library/3c1892c2-bf84-4cb6-af26-1f453be9e671).</span></span>

## <a name="new-and-changed-functionality-in-windows-powershell-ise"></a><span data-ttu-id="0caf3-109">Új és módosított funkciók a Windows PowerShell ISE-ben</span><span class="sxs-lookup"><span data-stu-id="0caf3-109">New and changed functionality in Windows PowerShell ISE</span></span>
<span data-ttu-id="0caf3-110">A következő táblázat felsorolja az új és módosított szolgáltatások a Windows PowerShell ISE-ben a Windows PowerShellben, kiadás.</span><span class="sxs-lookup"><span data-stu-id="0caf3-110">The following table lists the new and changed features for this release of Windows PowerShell ISE in Windows PowerShell.</span></span>

|<span data-ttu-id="0caf3-111">Szolgáltatás/funkció</span><span class="sxs-lookup"><span data-stu-id="0caf3-111">Feature/functionality</span></span>|<span data-ttu-id="0caf3-112">Windows PowerShell ISE-ben 4.0</span><span class="sxs-lookup"><span data-stu-id="0caf3-112">Windows PowerShell ISE 4.0</span></span>|<span data-ttu-id="0caf3-113">Windows PowerShell ISE-ben 3.0</span><span class="sxs-lookup"><span data-stu-id="0caf3-113">Windows PowerShell ISE 3.0</span></span>|<span data-ttu-id="0caf3-114">Windows PowerShell ISE-ben 2.0</span><span class="sxs-lookup"><span data-stu-id="0caf3-114">Windows PowerShell ISE 2.0</span></span>|
|--------------------------|-----------------------------------------------|-----------------------------------------------|-----------------------------------------------|
|<span data-ttu-id="0caf3-115">**[IntelliSense](#intellisense)**</span><span class="sxs-lookup"><span data-stu-id="0caf3-115">**[IntelliSense](#intellisense)**</span></span>|<span data-ttu-id="0caf3-116">X</span><span class="sxs-lookup"><span data-stu-id="0caf3-116">X</span></span>|<span data-ttu-id="0caf3-117">X</span><span class="sxs-lookup"><span data-stu-id="0caf3-117">X</span></span>||
|<span data-ttu-id="0caf3-118">**[A kódrészletek](#snippets)**</span><span class="sxs-lookup"><span data-stu-id="0caf3-118">**[Snippets](#snippets)**</span></span>|<span data-ttu-id="0caf3-119">X</span><span class="sxs-lookup"><span data-stu-id="0caf3-119">X</span></span>|<span data-ttu-id="0caf3-120">X</span><span class="sxs-lookup"><span data-stu-id="0caf3-120">X</span></span>||
|<span data-ttu-id="0caf3-121">**[Bővítmény-eszközök](#add-on-tools)**</span><span class="sxs-lookup"><span data-stu-id="0caf3-121">**[Add-on Tools](#add-on-tools)**</span></span>|<span data-ttu-id="0caf3-122">X</span><span class="sxs-lookup"><span data-stu-id="0caf3-122">X</span></span>|<span data-ttu-id="0caf3-123">X</span><span class="sxs-lookup"><span data-stu-id="0caf3-123">X</span></span>||
|<span data-ttu-id="0caf3-124">**[Indítsa újra a Manager és az automatikus mentés](#restart-manager-and-auto-save)**</span><span class="sxs-lookup"><span data-stu-id="0caf3-124">**[Restart Manager and Auto-save](#restart-manager-and-auto-save)**</span></span>|<span data-ttu-id="0caf3-125">X</span><span class="sxs-lookup"><span data-stu-id="0caf3-125">X</span></span>|<span data-ttu-id="0caf3-126">X</span><span class="sxs-lookup"><span data-stu-id="0caf3-126">X</span></span>||
|<span data-ttu-id="0caf3-127">**[Legutóbb használt listája](#most-recently-used-list)**</span><span class="sxs-lookup"><span data-stu-id="0caf3-127">**[Most-recently used list](#most-recently-used-list)**</span></span>|<span data-ttu-id="0caf3-128">X</span><span class="sxs-lookup"><span data-stu-id="0caf3-128">X</span></span>|<span data-ttu-id="0caf3-129">X</span><span class="sxs-lookup"><span data-stu-id="0caf3-129">X</span></span>||
|<span data-ttu-id="0caf3-130">**[Konzol panelen](#console-pane)**</span><span class="sxs-lookup"><span data-stu-id="0caf3-130">**[Console Pane](#console-pane)**</span></span>|<span data-ttu-id="0caf3-131">X</span><span class="sxs-lookup"><span data-stu-id="0caf3-131">X</span></span>|<span data-ttu-id="0caf3-132">X</span><span class="sxs-lookup"><span data-stu-id="0caf3-132">X</span></span>||
|<span data-ttu-id="0caf3-133">**[Parancssori kapcsolók](#command-line-switches)**</span><span class="sxs-lookup"><span data-stu-id="0caf3-133">**[Command-line switches](#command-line-switches)**</span></span>|<span data-ttu-id="0caf3-134">X</span><span class="sxs-lookup"><span data-stu-id="0caf3-134">X</span></span>|<span data-ttu-id="0caf3-135">X</span><span class="sxs-lookup"><span data-stu-id="0caf3-135">X</span></span>||
|<span data-ttu-id="0caf3-136">**[Új szerkesztő szolgáltatások](#new-editor-features)**</span><span class="sxs-lookup"><span data-stu-id="0caf3-136">**[New editor features](#new-editor-features)**</span></span>|<span data-ttu-id="0caf3-137">X</span><span class="sxs-lookup"><span data-stu-id="0caf3-137">X</span></span>|<span data-ttu-id="0caf3-138">X</span><span class="sxs-lookup"><span data-stu-id="0caf3-138">X</span></span>||
|<span data-ttu-id="0caf3-139">**[Új súgó-megjelenítő ablakban](#new-help-viewer-window)**</span><span class="sxs-lookup"><span data-stu-id="0caf3-139">**[New Help viewer window](#new-help-viewer-window)**</span></span>|<span data-ttu-id="0caf3-140">X</span><span class="sxs-lookup"><span data-stu-id="0caf3-140">X</span></span>|<span data-ttu-id="0caf3-141">X</span><span class="sxs-lookup"><span data-stu-id="0caf3-141">X</span></span>||
|<span data-ttu-id="0caf3-142">**[Show-Command parancsmaggal](#show-command-cmdlet)**</span><span class="sxs-lookup"><span data-stu-id="0caf3-142">**[Show-Command cmdlet](#show-command-cmdlet)**</span></span>|<span data-ttu-id="0caf3-143">X</span><span class="sxs-lookup"><span data-stu-id="0caf3-143">X</span></span>|<span data-ttu-id="0caf3-144">X</span><span class="sxs-lookup"><span data-stu-id="0caf3-144">X</span></span>||

### <a name="intellisense"></a><span data-ttu-id="0caf3-145">IntelliSense</span><span class="sxs-lookup"><span data-stu-id="0caf3-145">IntelliSense</span></span>
<span data-ttu-id="0caf3-146">**A ISE-ben 3.0 hozzáadva**</span><span class="sxs-lookup"><span data-stu-id="0caf3-146">**Added in ISE 3.0**</span></span>

<span data-ttu-id="0caf3-147">Az IntelliSense az automatikus kiegészítését támogatás szolgáltatása, amely része a Windows PowerShell ISE-ben.</span><span class="sxs-lookup"><span data-stu-id="0caf3-147">IntelliSense is an automatic-completion assistance feature that is part of Windows PowerShell ISE.</span></span> <span data-ttu-id="0caf3-148">Az IntelliSense potenciálisan egyező parancsmagok, paraméterek, paraméterértékeket, fájlok vagy mappák beírása kattintható menük jeleníti meg.</span><span class="sxs-lookup"><span data-stu-id="0caf3-148">IntelliSense displays clickable menus of potentially matching cmdlets, parameters, parameter values, files, or folders as you type.</span></span>

<span data-ttu-id="0caf3-149">**Milyen hozzáadott értéket nyújt ez a változás?**</span><span class="sxs-lookup"><span data-stu-id="0caf3-149">**What value does this change add?**</span></span>

<span data-ttu-id="0caf3-150">Az IntelliSense igény szerinti hozzáadásával célszerűbb a parancsmagok és a szintaxis észleléséhez, amikor a parancsfájlok létrehozásához használt Windows PowerShell ISE-ben.</span><span class="sxs-lookup"><span data-stu-id="0caf3-150">With the addition of IntelliSense, it is easier to discover cmdlets and syntax when you use Windows PowerShell ISE to create scripts.</span></span> <span data-ttu-id="0caf3-151">További Windows PowerShell új parancsfájlok létrehozásakor használhatja a Windows PowerShell ISE-ben.</span><span class="sxs-lookup"><span data-stu-id="0caf3-151">You can also use Windows PowerShell ISE to learn Windows PowerShell while you create new scripts.</span></span>

<span data-ttu-id="0caf3-152">**Mi működik másképp?**</span><span class="sxs-lookup"><span data-stu-id="0caf3-152">**What works differently?**</span></span>

<span data-ttu-id="0caf3-153">Írja be a parancsmagok a Windows PowerShell ISE 3.0-s vagy újabb verzió, amikor egy görgethető és kattintható menü jeleníti meg, keresse meg és válassza ki a megfelelő parancsokat lehetővé teszi.</span><span class="sxs-lookup"><span data-stu-id="0caf3-153">When you type cmdlets in the Windows PowerShell ISE 3.0 or later, a scrollable and clickable menu displays, allowing you to browse and select the appropriate commands.</span></span>

### <a name="snippets"></a><span data-ttu-id="0caf3-154">A kódrészletek</span><span class="sxs-lookup"><span data-stu-id="0caf3-154">Snippets</span></span>
<span data-ttu-id="0caf3-155">**A ISE-ben 3.0 hozzáadva**</span><span class="sxs-lookup"><span data-stu-id="0caf3-155">**Added in ISE 3.0**</span></span>

<span data-ttu-id="0caf3-156">*A kódrészletek* rövid szakaszok szúrhat be a parancsfájlok a Windows PowerShell ISE-ben létrehozhat Windows PowerShell-szabályzat.</span><span class="sxs-lookup"><span data-stu-id="0caf3-156">*Snippets* are short sections of Windows PowerShell code that you can insert into the scripts you create in Windows PowerShell ISE.</span></span> <span data-ttu-id="0caf3-157">Windows PowerShell ISE-ben tartalmaz egy alapértelmezett részletek.</span><span class="sxs-lookup"><span data-stu-id="0caf3-157">Windows PowerShell ISE comes with a default set of snippets.</span></span> <span data-ttu-id="0caf3-158">A kódrészletek használatával adhat hozzá a **New-kódrészlet** parancsmag használatakor a Windows PowerShell ISE-ben.</span><span class="sxs-lookup"><span data-stu-id="0caf3-158">You can add snippets by using the **New-Snippet** cmdlet while working in Windows PowerShell ISE.</span></span>

<span data-ttu-id="0caf3-159">**Milyen hozzáadott értéket nyújt ez a változás?**</span><span class="sxs-lookup"><span data-stu-id="0caf3-159">**What value does this change add?**</span></span>

<span data-ttu-id="0caf3-160">A kódrészletek, gyorsan összeállíthat és a környezet automatizáló szkriptek létrehozására.</span><span class="sxs-lookup"><span data-stu-id="0caf3-160">By using snippets, you can quickly assemble and create scripts to automate your environment.</span></span>

<span data-ttu-id="0caf3-161">**Mi működik másképp?**</span><span class="sxs-lookup"><span data-stu-id="0caf3-161">**What works differently?**</span></span>

<span data-ttu-id="0caf3-162">Kódrészletek a használata a Windows PowerShell 3.0-s vagy újabb, a **szerkesztése** menüben kattintson a **Start kódrészletek**, vagy nyomja le az **Ctrl-J**.</span><span class="sxs-lookup"><span data-stu-id="0caf3-162">To use snippets in Windows PowerShell 3.0 or later, on the **Edit** menu, click **Start Snippets**, or press **Ctrl-J**.</span></span>

### <a name="add-on-tools"></a><span data-ttu-id="0caf3-163">Bővítmény-eszközök</span><span class="sxs-lookup"><span data-stu-id="0caf3-163">Add-on tools</span></span>
<span data-ttu-id="0caf3-164">**Új funkció a PowerShell 3.0**</span><span class="sxs-lookup"><span data-stu-id="0caf3-164">**Added in PowerShell 3.0**</span></span>

<span data-ttu-id="0caf3-165">Windows PowerShell ISE-ben mostantól támogatja a bővítmény eszközöket, amelyek a Windows megjelenítési Alaprendszeri (WPF) vezérlőelem, amely lehet hozzáadni a hálózatiobjektum-modellt.</span><span class="sxs-lookup"><span data-stu-id="0caf3-165">Windows PowerShell ISE now supports add-on tools, which are Windows Presentation Foundation (WPF) controls that are added by using the object model.</span></span> <span data-ttu-id="0caf3-166">Bővítmény eszközök is megjeleníthetők a konzol egy függőleges vagy vízszintes ablaktáblát.</span><span class="sxs-lookup"><span data-stu-id="0caf3-166">Add-on tools can be displayed as a vertical or horizontal pane in the console.</span></span> <span data-ttu-id="0caf3-167">A többlapos vezérlőként több bővítmény Eszközök panelen jelennek meg.</span><span class="sxs-lookup"><span data-stu-id="0caf3-167">Multiple add-on tools in a pane are displayed as a tabbed control.</span></span> <span data-ttu-id="0caf3-168">Is hozzáadhat, vagy távolítsa el a Microsofton kívüli felek által készített eszközök bővítményt.</span><span class="sxs-lookup"><span data-stu-id="0caf3-168">You can also add or remove add-on tools that are produced by non-Microsoft parties.</span></span> <span data-ttu-id="0caf3-169">Importálhatja, vagy távolítsa el a bővítményt eszközök kapcsolatos további információkért lásd: [Windows PowerShell ISE Operations](https://technet.microsoft.com/library/cc732148.aspx).</span><span class="sxs-lookup"><span data-stu-id="0caf3-169">For more information about how to import or remove add-on tools, see [Windows PowerShell ISE Operations](https://technet.microsoft.com/library/cc732148.aspx).</span></span>

<span data-ttu-id="0caf3-170">**Milyen hozzáadott értéket nyújt ez a változás?**</span><span class="sxs-lookup"><span data-stu-id="0caf3-170">**What value does this change add?**</span></span>

<span data-ttu-id="0caf3-171">A bővítmények lehetővé teszik a kiterjesztéséhez és testre szabásához Windows PowerShell ISE-ben az eszközök, amelyek további funkciókkal bővítik a Windows PowerShell ISE-ben vagy a parancsfájl-kezelési környezet minőségét.</span><span class="sxs-lookup"><span data-stu-id="0caf3-171">Add-ons allow you to extend and customize Windows PowerShell ISE with tools that can enhance your scripting experience or add functionality to Windows PowerShell ISE.</span></span>

<span data-ttu-id="0caf3-172">**Mi működik másképp?**</span><span class="sxs-lookup"><span data-stu-id="0caf3-172">**What works differently?**</span></span>

<span data-ttu-id="0caf3-173">Windows PowerShell ISE-ben, 3.0-s és újabb verziók kapható a **parancsok** bővítményt.</span><span class="sxs-lookup"><span data-stu-id="0caf3-173">Windows PowerShell ISE 3.0 and later come with the **Commands** add-on.</span></span> <span data-ttu-id="0caf3-174">A **parancsok** bővítmény lehetővé teszi, hogy a parancsmagok keresse meg és érheti el a parancsmagok egymás mellett a Súgó a **parancsfájl** és **konzol** ablaktáblái.</span><span class="sxs-lookup"><span data-stu-id="0caf3-174">The **Commands** add-on allows you to browse cmdlets, and access help about the cmdlets side-by-side with the **Script** and **Console** Panes.</span></span>

<span data-ttu-id="0caf3-175">További bővítmények találhatók használatával a **nyílt bővítmény eszközök webhely** parancs a **bővítmények** menü.</span><span class="sxs-lookup"><span data-stu-id="0caf3-175">Additional add-ons can be found by using the **Open Add-on Tools Website** command on the **Add-ons** menu.</span></span>

### <a name="restart-manager-and-auto-save"></a><span data-ttu-id="0caf3-176">Indítsa újra a manager és az automatikus mentés</span><span class="sxs-lookup"><span data-stu-id="0caf3-176">Restart manager and auto-save</span></span>
<span data-ttu-id="0caf3-177">**Új funkció a PowerShell 3.0**</span><span class="sxs-lookup"><span data-stu-id="0caf3-177">**Added in PowerShell 3.0**</span></span>

<span data-ttu-id="0caf3-178">Windows PowerShell ISE-ben mostantól automatikusan menti a megnyitott parancsfájlok két percenként, egy külön helyet.</span><span class="sxs-lookup"><span data-stu-id="0caf3-178">Windows PowerShell ISE now automatically saves your open scripts every two minutes, in a separate location.</span></span>  <span data-ttu-id="0caf3-179">Ha a Windows PowerShell ISE-ben nem működik, vagy ha az operációs rendszer újraindul, Windows PowerShell ISE újraindítása után, működés, visszaadhatja parancsfájlok, amelyek korábban nyissa meg a legutóbbi munkamenet akkor is, ha a parancsfájlok nem lettek mentve.</span><span class="sxs-lookup"><span data-stu-id="0caf3-179">If Windows PowerShell ISE stops working, or if the operating system is restarted, after Windows PowerShell ISE restarts, it recovers scripts that were open in the last session, even if the scripts were not saved.</span></span>

<span data-ttu-id="0caf3-180">Az automatikus mentése időköz módosításához futtassa a következő parancsot a konzolablakban: **$psise. Options.AutoSaveMinuteInterval**.</span><span class="sxs-lookup"><span data-stu-id="0caf3-180">To change the automatic saving interval, run the following command in the Console pane: **$psise.Options.AutoSaveMinuteInterval**.</span></span>

<span data-ttu-id="0caf3-181">**Milyen hozzáadott értéket nyújt ez a változás?**</span><span class="sxs-lookup"><span data-stu-id="0caf3-181">**What value does this change add?**</span></span>

<span data-ttu-id="0caf3-182">Most már dolgozhat, hogy a nyílt parancsprogramok a rendszer automatikusan menti váratlan újraindítása esetén, hogy a Windows PowerShell ISE belül.</span><span class="sxs-lookup"><span data-stu-id="0caf3-182">You can now work within Windows PowerShell ISE knowing that your open scripts are automatically saved in the event of an unexpected restart.</span></span>

<span data-ttu-id="0caf3-183">**Mi működik másképp?**</span><span class="sxs-lookup"><span data-stu-id="0caf3-183">**What works differently?**</span></span>

<span data-ttu-id="0caf3-184">Windows PowerShell ISE 2.0 nem menti a parancsfájlok automatikus újraindítás esetén.</span><span class="sxs-lookup"><span data-stu-id="0caf3-184">Windows PowerShell ISE 2.0 does not save the scripts automatically in the event of a restart.</span></span>

### <a name="most-recently-used-list"></a><span data-ttu-id="0caf3-185">Legutóbb használt listája</span><span class="sxs-lookup"><span data-stu-id="0caf3-185">Most-recently used list</span></span>
<span data-ttu-id="0caf3-186">**Új funkció a PowerShell 3.0**</span><span class="sxs-lookup"><span data-stu-id="0caf3-186">**Added in PowerShell 3.0**</span></span>

<span data-ttu-id="0caf3-187">Windows PowerShell ISE-ben a legutóbb használt listáját a fájlok most már rendelkezik.</span><span class="sxs-lookup"><span data-stu-id="0caf3-187">Windows PowerShell ISE now has a most-recently used list for files.</span></span> <span data-ttu-id="0caf3-188">Amikor megnyit egy fájlt a Windows PowerShell ISE-ben, a fájl bekerül a legutóbb használt listájának a a **fájl** menü.</span><span class="sxs-lookup"><span data-stu-id="0caf3-188">When you open a file in Windows PowerShell ISE, the file is added to the most-recently used list on the **File** menu.</span></span>

<span data-ttu-id="0caf3-189">A legutóbb használt listán fájl alapértelmezett számának módosításához futtassa a következő parancsot a konzolablakban: **$psise. Options.MruCount**.</span><span class="sxs-lookup"><span data-stu-id="0caf3-189">To change the default number of files in the most-recently used list, run the following command in the Console Pane: **$psise.Options.MruCount**.</span></span>

<span data-ttu-id="0caf3-190">**Milyen hozzáadott értéket nyújt ez a változás?**</span><span class="sxs-lookup"><span data-stu-id="0caf3-190">**What value does this change add?**</span></span>

<span data-ttu-id="0caf3-191">A legutóbb használt lista használatával most már könnyedén elérheti a gyakran használt fájlok.</span><span class="sxs-lookup"><span data-stu-id="0caf3-191">You can now use the most-recently used list to easily access your frequently-used files.</span></span>

<span data-ttu-id="0caf3-192">**Mi működik másképp?**</span><span class="sxs-lookup"><span data-stu-id="0caf3-192">**What works differently?**</span></span>

<span data-ttu-id="0caf3-193">Windows PowerShell ISE 2.0 nem rendelkezik a legutóbb használt listáját.</span><span class="sxs-lookup"><span data-stu-id="0caf3-193">Windows PowerShell ISE 2.0 does not have a most-recently used list.</span></span>

### <a name="console-pane"></a><span data-ttu-id="0caf3-194">Konzol panelen</span><span class="sxs-lookup"><span data-stu-id="0caf3-194">Console Pane</span></span>
<span data-ttu-id="0caf3-195">**Új funkció a PowerShell 3.0**</span><span class="sxs-lookup"><span data-stu-id="0caf3-195">**Added in PowerShell 3.0**</span></span>

<span data-ttu-id="0caf3-196">A külön parancsot és a Windows PowerShell ISE-ben az első kiadásban elérhető kimeneti ablaktábla mostantól egy egyetlen konzol ablaktáblában.</span><span class="sxs-lookup"><span data-stu-id="0caf3-196">The separate Command and Output Panes that were available in the first release of Windows PowerShell ISE have been combined into a single Console Pane.</span></span> <span data-ttu-id="0caf3-197">A konzol ablaktáblában a függvény és a egy tipikus Windows PowerShell-konzolt a megjelenése hasonló, de (a legtöbb olyan ebben a témakörben leírtak szerint) a következő fejlesztéseket tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="0caf3-197">The Console Pane is similar in function and appearance to a typical Windows PowerShell console, but it includes the following enhancements (most are described in this topic).</span></span>

- <span data-ttu-id="0caf3-198">Szintaxis színezést bemeneti szöveg (nem kimeneti szöveg), beleértve syntaxe XML</span><span class="sxs-lookup"><span data-stu-id="0caf3-198">Syntax coloring for input text (not output text), including XML syntax</span></span>

- <span data-ttu-id="0caf3-199">IntelliSense</span><span class="sxs-lookup"><span data-stu-id="0caf3-199">IntelliSense</span></span>

- <span data-ttu-id="0caf3-200">Egyező kapcsos zárójel</span><span class="sxs-lookup"><span data-stu-id="0caf3-200">Brace matching</span></span>

- <span data-ttu-id="0caf3-201">Hiba történt annak jelzése</span><span class="sxs-lookup"><span data-stu-id="0caf3-201">Error indication</span></span>

- <span data-ttu-id="0caf3-202">Teljes Unicode-támogatás</span><span class="sxs-lookup"><span data-stu-id="0caf3-202">Full Unicode support</span></span>

- <span data-ttu-id="0caf3-203">**F1** környezetfüggő súgó</span><span class="sxs-lookup"><span data-stu-id="0caf3-203">**F1** context-sensitive help</span></span>

- <span data-ttu-id="0caf3-204">**CTRL + F1** környezetfüggő Show-parancs</span><span class="sxs-lookup"><span data-stu-id="0caf3-204">**Ctrl+F1** context-sensitive Show-Command</span></span>

- <span data-ttu-id="0caf3-205">A parancsfájl komplex és támogatja a jobbról balra</span><span class="sxs-lookup"><span data-stu-id="0caf3-205">Complex script and right-to-left support</span></span>

- <span data-ttu-id="0caf3-206">Betűtípus-támogatás</span><span class="sxs-lookup"><span data-stu-id="0caf3-206">Font support</span></span>

- <span data-ttu-id="0caf3-207">Nagyítás</span><span class="sxs-lookup"><span data-stu-id="0caf3-207">Zoom</span></span>

- <span data-ttu-id="0caf3-208">Vonal-válasszon és a blokk-válasszon módok</span><span class="sxs-lookup"><span data-stu-id="0caf3-208">Line-select and block-select modes</span></span>

- <span data-ttu-id="0caf3-209">A parancssorban, amikor lenyomja a beírt tartalom megőrzése az **mentése** nyílra a konzolon előzményeinek megtekintése</span><span class="sxs-lookup"><span data-stu-id="0caf3-209">Preservation of typed content at the command line when you press the **Up** arrow to view history in the console</span></span>

<span data-ttu-id="0caf3-210">**Milyen hozzáadott értéket nyújt ez a változás?**</span><span class="sxs-lookup"><span data-stu-id="0caf3-210">**What value does this change add?**</span></span>

<span data-ttu-id="0caf3-211">A konzolablakban a módosítások hozzáadása, amely megfelel a konzol felületét a parancsfájl-kezelési élményt nyújt.</span><span class="sxs-lookup"><span data-stu-id="0caf3-211">The addition of these Console Pane changes provides a scripting experience that is more consistent with the console interface.</span></span>

<span data-ttu-id="0caf3-212">**Mi működik másképp?**</span><span class="sxs-lookup"><span data-stu-id="0caf3-212">**What works differently?**</span></span>

<span data-ttu-id="0caf3-213">Windows PowerShell ISE 2.0 rendelkezik, külön parancsot és a kimeneti ablaktábla.</span><span class="sxs-lookup"><span data-stu-id="0caf3-213">Windows PowerShell ISE 2.0 has separate Command and Output Panes.</span></span>

### <a name="command-line-switches"></a><span data-ttu-id="0caf3-214">Parancssori kapcsolók</span><span class="sxs-lookup"><span data-stu-id="0caf3-214">Command-line switches</span></span>
<span data-ttu-id="0caf3-215">**Új funkció a PowerShell 3.0**</span><span class="sxs-lookup"><span data-stu-id="0caf3-215">**Added in PowerShell 3.0**</span></span>

<span data-ttu-id="0caf3-216">Ha a parancssorból indítsa el Windows PowerShell ISE-ben (beírásával **powershell_ise.exe**), a következő új parancssori kapcsolókat is hozzáadhat.</span><span class="sxs-lookup"><span data-stu-id="0caf3-216">If you start Windows PowerShell ISE from the command line (by typing **powershell_ise.exe**), you can add the following new command-line switches.</span></span>

- <span data-ttu-id="0caf3-217">*-NoProfile*: Elindítja a Windows PowerShell ISE-ben futó nélkül **$profile**</span><span class="sxs-lookup"><span data-stu-id="0caf3-217">*-NoProfile*: Starts Windows PowerShell ISE without running **$profile**</span></span>

- <span data-ttu-id="0caf3-218">*-Súgó*: A súgóablak megjelenítése</span><span class="sxs-lookup"><span data-stu-id="0caf3-218">*-Help*: Displays a Help window</span></span>

- <span data-ttu-id="0caf3-219">*-mta*: Többszálú apartman módban indul el a Windows PowerShell ISE-ben.</span><span class="sxs-lookup"><span data-stu-id="0caf3-219">*-mta*: Starts Windows PowerShell ISE in multithreaded apartment mode.</span></span> <span data-ttu-id="0caf3-220">Az alapértelmezett működési mód a Windows PowerShell ISE-ben az egyszálas apartman módban, vagy *- sta*.</span><span class="sxs-lookup"><span data-stu-id="0caf3-220">The default operation mode for Windows PowerShell ISE is single-threaded apartment mode, or *-sta*.</span></span>

<span data-ttu-id="0caf3-221">**Milyen hozzáadott értéket nyújt ez a változás?**</span><span class="sxs-lookup"><span data-stu-id="0caf3-221">**What value does this change add?**</span></span>

<span data-ttu-id="0caf3-222">A parancssori kapcsolók igény szerinti hozzáadásával lehetővé teszi a környezet, amelyben a Windows PowerShell ISE-t futtató szabályozását.</span><span class="sxs-lookup"><span data-stu-id="0caf3-222">The addition of these command-line switches allows you to control the environment in which the Windows PowerShell ISE runs.</span></span>

<span data-ttu-id="0caf3-223">**Mi működik másképp?**</span><span class="sxs-lookup"><span data-stu-id="0caf3-223">**What works differently?**</span></span>

<span data-ttu-id="0caf3-224">Windows PowerShell ISE 2.0 nem ismeri fel a parancssori kapcsolók.</span><span class="sxs-lookup"><span data-stu-id="0caf3-224">Windows PowerShell ISE 2.0 does not recognize these command-line switches.</span></span>

### <a name="new-editor-features"></a><span data-ttu-id="0caf3-225">Új szerkesztő szolgáltatások</span><span class="sxs-lookup"><span data-stu-id="0caf3-225">New editor features</span></span>
<span data-ttu-id="0caf3-226">**Új funkció a PowerShell 3.0**</span><span class="sxs-lookup"><span data-stu-id="0caf3-226">**Added in PowerShell 3.0**</span></span>

<span data-ttu-id="0caf3-227">Más Windows PowerShell ISE-ben szerkesztési funkciók a következők:</span><span class="sxs-lookup"><span data-stu-id="0caf3-227">Other Windows PowerShell ISE editing features include:</span></span>

- <span data-ttu-id="0caf3-228">**XML-szintaxis színezést**Windows PowerShell ISE-ben mostantól színek syntaxe XML ugyanúgy, ahogy azt a Windows PowerShell-szintaxis színek.</span><span class="sxs-lookup"><span data-stu-id="0caf3-228">**XML syntax coloring**Windows PowerShell ISE now colors XML syntax in the same way as it colors Windows PowerShell syntax.</span></span>

- <span data-ttu-id="0caf3-229">**Kapcsos zárójel megfelelő** Windows PowerShell ISE-ben kiterjed kapcsos zárójel megfelelő, és a kiemelés, és az alábbi módon használható: (használata esetén például a **egyezés Ugrás** parancs vagy **Ctrl +]** megkeresi a Záró kapcsos zárójel, ha rendelkezik egy nyitó zárójel jelölve).</span><span class="sxs-lookup"><span data-stu-id="0caf3-229">**Brace matching** Windows PowerShell ISE includes brace matching and highlighting, and can be used in the following ways: (for example, using the **Go to Match** command or **Ctrl + ]** locates the closing brace, if you have an opening brace selected).</span></span>

- <span data-ttu-id="0caf3-230">**Vázlat nézetben** a parancsfájl panelen támogatja, felvázolva, amellyel összecsukás és kód szakaszait Kibontás plusz vagy mínusz kattintson a bal oldali margó bejelentkezik.</span><span class="sxs-lookup"><span data-stu-id="0caf3-230">**Outline view** The Script Pane supports outlining, which allows collapsing or expanding sections of code by clicking plus or minus signs in the left margin.</span></span> <span data-ttu-id="0caf3-231">Zárójelek között is használhatja, vagy a **#region** és **#endregion** címkék elején vagy végén egy összecsukható szakasz megjelölni.</span><span class="sxs-lookup"><span data-stu-id="0caf3-231">You can use braces or the **#region** and **#endregion** tags to mark the beginning or end of a collapsible section.</span></span> <span data-ttu-id="0caf3-232">Kibontása vagy összecsukása minden régióban, nyomja le a **Ctrl + M**.</span><span class="sxs-lookup"><span data-stu-id="0caf3-232">To expand or collapse all regions, press **Ctrl + M**.</span></span>

- <span data-ttu-id="0caf3-233">**Áthúzása szövegszerkesztés**Windows PowerShell ISE-ben mostantól támogatja a áthúzása szöveg szerkesztése.</span><span class="sxs-lookup"><span data-stu-id="0caf3-233">**Drag and drop text editing**Windows PowerShell ISE now supports drag and drop text editing.</span></span> <span data-ttu-id="0caf3-234">Válassza ki bármelyik szövegblokk, és húzza át azt a szerkesztő vagy a konzol a szöveg áthelyezése egy másik helyre.</span><span class="sxs-lookup"><span data-stu-id="0caf3-234">You can select any block of text and drag that text to another location in the editor or the console to move the text.</span></span> <span data-ttu-id="0caf3-235">Ha meg a Ctrl billentyűt lenyomva tartva húzza a kijelölt szöveg az egérgomb felengedésekor a szöveget az új helyre másolódik.</span><span class="sxs-lookup"><span data-stu-id="0caf3-235">If you hold down the Ctrl key while you drag the selected text, when you release the mouse button the text is copied to the new location.</span></span> <span data-ttu-id="0caf3-236">Ebben a Windows PowerShell ISE-ben, valamint a régebbi Windows PowerShell ISE-ben, a Windows PowerShell ISE-ben, fájlokat áthúzása Windows PowerShell ISE-t megnyitja a fájlt.</span><span class="sxs-lookup"><span data-stu-id="0caf3-236">In this version of Windows PowerShell ISE, as well as the previous version of Windows PowerShell ISE, when you drag and drop files onto Windows PowerShell ISE, Windows PowerShell ISE opens the file.</span></span>

- <span data-ttu-id="0caf3-237">**Elemzési hiba megjelenített** piros aláhúzás jelöl, elemzési hibákat.</span><span class="sxs-lookup"><span data-stu-id="0caf3-237">**Parse error display** Parse errors are indicated with red underlines.</span></span> <span data-ttu-id="0caf3-238">Ha az egérmutatót a jelzett hiba, elemleírás jelenik meg a a probléma, amely a kódban található.</span><span class="sxs-lookup"><span data-stu-id="0caf3-238">When you hover over an indicated error, tooltip text displays the problem that was found in the code.</span></span>

- <span data-ttu-id="0caf3-239">**Nagyítás** nagyítás százalékos aránya a konzoltartalmak nagyítás csúszka segítségével (a jobb alsó sarokban a Windows PowerShell ISE-ablakot), vagy a parancs beírásával állítható **$psise.options.Zoom** a konzol ablaktáblában.</span><span class="sxs-lookup"><span data-stu-id="0caf3-239">**Zoom** The zoom percentage of the console's content can be set by using the zoom slider (in the lower right corner of Windows PowerShell ISE window), or by entering the command **$psise.options.Zoom** in the Console Pane.</span></span>

- <span data-ttu-id="0caf3-240">**Rich text másolás és Beillesztés** betűtípusát, méretét, és az eredeti kijelölés színe információkat a Windows PowerShell ISE-ben megtartja a vágólapra másolása.</span><span class="sxs-lookup"><span data-stu-id="0caf3-240">**Rich text copy and paste** Copying to the clipboard in Windows PowerShell ISE preserves the font, size, and color information of the original selection.</span></span>

- <span data-ttu-id="0caf3-241">**Letiltja a kijelölés** szöveg kiválasztásakor az egérrel a parancsfájl panelen az ALT billentyűt lenyomva vagy billentyű lenyomásával kiválaszthatja szövegblokk **Alt + Shift + nyíl**.</span><span class="sxs-lookup"><span data-stu-id="0caf3-241">**Block selection** You can select a block of text by holding down the ALT key while selecting text in the Script Pane with your mouse, or by pressing **Alt+Shift+Arrow**.</span></span>

<span data-ttu-id="0caf3-242">**Milyen hozzáadott értéket nyújt ez a változás?**</span><span class="sxs-lookup"><span data-stu-id="0caf3-242">**What value does this change add?**</span></span>

<span data-ttu-id="0caf3-243">A további szerkesztési funkciók adjon meg egy egységes és a hatékony Kódszerkesztő környezetében.</span><span class="sxs-lookup"><span data-stu-id="0caf3-243">The additional editing features provide a more consistent and powerful editing environment.</span></span>

<span data-ttu-id="0caf3-244">**Mi működik másképp?**</span><span class="sxs-lookup"><span data-stu-id="0caf3-244">**What works differently?**</span></span>

<span data-ttu-id="0caf3-245">Ezek a szerkesztési fejlesztések nem volt megtalálható a Windows PowerShell ISE 2.0.</span><span class="sxs-lookup"><span data-stu-id="0caf3-245">These editing enhancements were not present in Windows PowerShell ISE 2.0.</span></span>

### <a name="new-help-viewer-window"></a><span data-ttu-id="0caf3-246">Új súgó-megjelenítő ablakban</span><span class="sxs-lookup"><span data-stu-id="0caf3-246">New Help viewer window</span></span>
<span data-ttu-id="0caf3-247">**Új funkció a PowerShell 3.0**</span><span class="sxs-lookup"><span data-stu-id="0caf3-247">**Added in PowerShell 3.0**</span></span>

<span data-ttu-id="0caf3-248">Ha lenyomja **F1** a kurzort egy parancsmag vagy van kiemelve a parancsmag részét, ha az új súgómegjelenítő megnyílik a környezetfüggő súgó a kiemelt parancsmaggal kapcsolatban.</span><span class="sxs-lookup"><span data-stu-id="0caf3-248">If you press **F1** when your cursor is in a cmdlet, or you have part of a cmdlet highlighted, the new Help viewer opens context-sensitive Help about the highlighted cmdlet.</span></span> <span data-ttu-id="0caf3-249">Windows PowerShell kapcsolatban súgójának megjelenítéséhez írja be a **operátorok** a konzol ablaktáblában, és nyomja le az **F1**.</span><span class="sxs-lookup"><span data-stu-id="0caf3-249">To display Windows PowerShell About help, type  **operators** in the console pane, and then press **F1**.</span></span>

<span data-ttu-id="0caf3-250">Ez a funkció használatához töltse le a Windows PowerShell súgója témakörök legfrissebb verzióját a Microsoft webhelyén.</span><span class="sxs-lookup"><span data-stu-id="0caf3-250">Before you use this feature, download the most current version of Windows PowerShell Help topics from the Microsoft website.</span></span> <span data-ttu-id="0caf3-251">A legegyszerűbb módja, ha a súgótémakörök letöltése, hogy futtassa a **Update-Help** parancsmag a konzol ablaktáblában, ha rendszergazdaként futtatja a Windows PowerShell ISE-ben.</span><span class="sxs-lookup"><span data-stu-id="0caf3-251">The simplest method for downloading the Help topics is to run the **Update-Help** cmdlet in the Console Pane when running Windows PowerShell ISE as administrator.</span></span>

<span data-ttu-id="0caf3-252">Hol módosíthatja a **F1** kulcs segítséget keres.</span><span class="sxs-lookup"><span data-stu-id="0caf3-252">You can alter where the **F1** key looks for Help.</span></span> <span data-ttu-id="0caf3-253">Az a **eszközök**/**beállítások** menü, az a **általános beállítások** lap **egyéb beállítások**, állítsa be, vagy törölje a jelet a jelölőnégyzet **online tartalom helyett használja a helyi súgó tartalma**.</span><span class="sxs-lookup"><span data-stu-id="0caf3-253">In the **Tools**/**Options** menu, on the **General Settings** tab, under **Other Settings**, you can set or clear the checkbox **Use local help content instead of online content**.</span></span> <span data-ttu-id="0caf3-254">Ha be van jelölve, az ügyfél az a parancsmagot a letöltött súgó modulok mappában található segítséget keres.</span><span class="sxs-lookup"><span data-stu-id="0caf3-254">If checked, then the client looks for the cmdlet Help in the downloaded Help found in the modules folder.</span></span>  <span data-ttu-id="0caf3-255">Ha a jelölőnégyzet nincs bejelölve, majd az ügyfél néz ki mindez a TechNet könyvtárban a parancsmag súgóját.</span><span class="sxs-lookup"><span data-stu-id="0caf3-255">If the checkbox is cleared, then the client looks on the TechNet library for the cmdlet help.</span></span>

<span data-ttu-id="0caf3-256">**Milyen hozzáadott értéket nyújt ez a változás?**</span><span class="sxs-lookup"><span data-stu-id="0caf3-256">**What value does this change add?**</span></span>

<span data-ttu-id="0caf3-257">Az aktuális parancsmag vagy szkript elhagyása nélkül környezetfüggő súgó zökkenőmentes tanulási élményt nyújt.</span><span class="sxs-lookup"><span data-stu-id="0caf3-257">Context-sensitive Help without leaving your current cmdlet or script provides a seamless learning experience.</span></span>

<span data-ttu-id="0caf3-258">**Mi működik másképp?**</span><span class="sxs-lookup"><span data-stu-id="0caf3-258">**What works differently?**</span></span>

<span data-ttu-id="0caf3-259">Korábbi verzióiban a Windows PowerShell ISE-ben az F1 billentyű megnyomásával megnyitni a súgófájlban a helyi számítógépen.</span><span class="sxs-lookup"><span data-stu-id="0caf3-259">Pressing F1 in previous versions of Windows PowerShell ISE opened the help file on the local computer.</span></span> <span data-ttu-id="0caf3-260">A Windows PowerShell ISE 3.0-s és újabb verziók megnyílik egy ablak, amely tartalmazza a kereshető és konfigurálható a parancsmag súgóját.</span><span class="sxs-lookup"><span data-stu-id="0caf3-260">In Windows PowerShell ISE 3.0 and later, a window opens that contains the help for the cmdlet that is searchable and configurable.</span></span> <span data-ttu-id="0caf3-261">Az ügyféltámogatási élmény a Windows PowerShell ISE 3.0 új, és új Windows PowerShell 3.0 a frissíthető súgó.</span><span class="sxs-lookup"><span data-stu-id="0caf3-261">This Help experience is new for Windows PowerShell ISE 3.0, and Updatable Help is new for Windows PowerShell 3.0.</span></span>

### <a name="show-command-cmdlet"></a><span data-ttu-id="0caf3-262">Show-Command parancsmaggal</span><span class="sxs-lookup"><span data-stu-id="0caf3-262">Show-Command cmdlet</span></span>
<span data-ttu-id="0caf3-263">**Új funkció a PowerShell 3.0**</span><span class="sxs-lookup"><span data-stu-id="0caf3-263">**Added in PowerShell 3.0**</span></span>

<span data-ttu-id="0caf3-264">A **Show-parancs** parancsmag lehetővé teszi, hogy compose vagy egy parancsmag vagy függvény futtatása egy grafikus űrlap kitöltésével.</span><span class="sxs-lookup"><span data-stu-id="0caf3-264">The **Show-Command** cmdlet enables you to compose or run a cmdlet or function by filling in a graphical form.</span></span> <span data-ttu-id="0caf3-265">Az űrlap lehetővé teszi, hogy a felhasználók grafikus környezetben a Windows PowerShell-lel dolgozni.</span><span class="sxs-lookup"><span data-stu-id="0caf3-265">The form lets users work with Windows PowerShell in a graphical environment.</span></span> <span data-ttu-id="0caf3-266">**Show-parancs** is lehetővé teszi, hogy komplex, amely a Windows PowerShell-alapú gyors grafikus létrehozásához.</span><span class="sxs-lookup"><span data-stu-id="0caf3-266">**Show-Command** also enables advanced scripters to create a quick Windows PowerShell-based GUI.</span></span>

<span data-ttu-id="0caf3-267">**Milyen hozzáadott értéket nyújt ez a változás?**</span><span class="sxs-lookup"><span data-stu-id="0caf3-267">**What value does this change add?**</span></span>

<span data-ttu-id="0caf3-268">Használatával **Show-parancs** a Windows PowerShell-szkriptek, megadhatja a felhasználók számára, amellyel nem ismeri a grafikus környezetet.</span><span class="sxs-lookup"><span data-stu-id="0caf3-268">By using **Show-Command** in your Windows PowerShell scripts, you can provide your users with the graphical environment with which they are familiar.</span></span> <span data-ttu-id="0caf3-269">**Show-parancs** ismerje meg a Windows PowerShell bevezető felhasználók is segít.</span><span class="sxs-lookup"><span data-stu-id="0caf3-269">**Show-Command** can also help introductory users learn Windows PowerShell.</span></span>

<span data-ttu-id="0caf3-270">**Mi működik másképp?**</span><span class="sxs-lookup"><span data-stu-id="0caf3-270">**What works differently?**</span></span>

<span data-ttu-id="0caf3-271">Show-parancsot az új Windows PowerShell ISE 3.0.</span><span class="sxs-lookup"><span data-stu-id="0caf3-271">Show-Command is new Windows PowerShell ISE 3.0.</span></span>

## <a name="see-also"></a><span data-ttu-id="0caf3-272">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="0caf3-272">See also</span></span>
<span data-ttu-id="0caf3-273">Windows PowerShell ISE-ben a Windows PowerShellben való használatáról további információkért lásd az alábbi hivatkozásokat.</span><span class="sxs-lookup"><span data-stu-id="0caf3-273">For more information about using Windows PowerShell ISE in Windows PowerShell, see the following links.</span></span>

- [<span data-ttu-id="0caf3-274">A Windows PowerShell integrált parancsfájlkezelési környezetet felfedezése</span><span class="sxs-lookup"><span data-stu-id="0caf3-274">Exploring the Windows PowerShell Integrated Scripting Environment</span></span>](../getting-started/fundamental/exploring-the-windows-powershell-ise.md)
- [<span data-ttu-id="0caf3-275">ISE-ben a TechNet-Wikiben</span><span class="sxs-lookup"><span data-stu-id="0caf3-275">ISE on the TechNet Wiki</span></span>](https://social.technet.microsoft.com/wiki/search/searchresults.aspx?q=ISE)
- [<span data-ttu-id="0caf3-276">Script Center</span><span class="sxs-lookup"><span data-stu-id="0caf3-276">Script Center</span></span>](https://technet.microsoft.com/scriptcenter/default)