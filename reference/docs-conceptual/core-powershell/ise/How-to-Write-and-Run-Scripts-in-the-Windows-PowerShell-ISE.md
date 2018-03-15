---
ms.date: 2017-06-05
keywords: PowerShell parancsmag
title: "Parancsfájlok írása és futtatása a Windows PowerShell ISE-ben"
ms.assetid: 62f916d9-b3a1-484a-bdfb-41f57112c22b
ms.openlocfilehash: 77d8ae81cb03f03b3b5d044e6503bbb23cb5b771
ms.sourcegitcommit: 99227f62dcf827354770eb2c3e95c5cf6a3118b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/15/2018
---
# <a name="how-to-write-and-run-scripts-in-the-windows-powershell-ise"></a><span data-ttu-id="95b71-103">Parancsfájlok írása és futtatása a Windows PowerShell ISE-ben</span><span class="sxs-lookup"><span data-stu-id="95b71-103">How to Write and Run Scripts in the Windows PowerShell ISE</span></span>
<span data-ttu-id="95b71-104">Ez a témakör ismerteti létrehozása, szerkesztése, futtatása és mentése a parancsfájlok a parancssori panelbe.</span><span class="sxs-lookup"><span data-stu-id="95b71-104">This topic describes how to create, edit, run, and save scripts in the Script Pane.</span></span>

## <a name="how-to-create-and-run-scripts"></a><span data-ttu-id="95b71-105">Hozzon létre, és parancsfájlok futtatása</span><span class="sxs-lookup"><span data-stu-id="95b71-105">How to create and run scripts</span></span>
<span data-ttu-id="95b71-106">Nyissa meg, és szerkesztheti a parancssori panelbe Windows PowerShell-fájlokat.</span><span class="sxs-lookup"><span data-stu-id="95b71-106">You can open and edit Windows PowerShell files in the Script Pane.</span></span> <span data-ttu-id="95b71-107">A Windows PowerShell érdeklő adott fájltípusokhoz olyan parancsfájlokat (.ps1), parancsfájlok (.psd1) és parancsfájlok modul (.psm1).</span><span class="sxs-lookup"><span data-stu-id="95b71-107">Specific file types of interest in Windows PowerShell are script files (.ps1), script data files (.psd1), and script module files (.psm1).</span></span> <span data-ttu-id="95b71-108">Ilyen típusú a parancssori panelbe szerkesztőben színes szintaxist.</span><span class="sxs-lookup"><span data-stu-id="95b71-108">These file types are syntax colored in the Script Pane editor.</span></span> <span data-ttu-id="95b71-109">Más közös fájltípus esetében előfordulhat, hogy nyissa meg a parancssori panelbe konfigurációs fájlok (.ps1xml), XML, és szövegfájlok.</span><span class="sxs-lookup"><span data-stu-id="95b71-109">Other common file types you may open in the Script Pane are configuration files (.ps1xml), XML files, and text files.</span></span>

> [!NOTE]
> <span data-ttu-id="95b71-110">A Windows PowerShell végrehajtási házirend határozza meg, hogy parancsfájlok futtatásához, és a Windows PowerShell-profilok és konfigurációs fájlok.</span><span class="sxs-lookup"><span data-stu-id="95b71-110">The Windows PowerShell execution policy determines whether you can run scripts and load Windows PowerShell profiles and configuration files.</span></span> <span data-ttu-id="95b71-111">Az alapértelmezett végrehajtási házirendjét, korlátozott, megakadályozza, hogy az összes parancsfájl futtatását, és megakadályozza, hogy a profil betöltését.</span><span class="sxs-lookup"><span data-stu-id="95b71-111">The default execution policy, Restricted, prevents all scripts from running, and prevents loading profiles.</span></span> <span data-ttu-id="95b71-112">Profilok betölteni, és használható engedélyezi a végrehajtási házirend módosításához lásd [Set-ExecutionPolicy [PSITPro5_Security]](https://technet.microsoft.com/library/5690a0e1-495b-4e63-8280-65ead7bf01ab) és [about_Signing [v4]](https://technet.microsoft.com/library/fcbdd3b9-0b9f-4734-b5c7-e0dcc304fa1d).</span><span class="sxs-lookup"><span data-stu-id="95b71-112">To change the execution policy to allow profiles to load and be used, see [Set-ExecutionPolicy[PSITPro5_Security]](https://technet.microsoft.com/library/5690a0e1-495b-4e63-8280-65ead7bf01ab) and [about_Signing [v4]](https://technet.microsoft.com/library/fcbdd3b9-0b9f-4734-b5c7-e0dcc304fa1d).</span></span>

### <a name="to-create-a-new-script-file"></a><span data-ttu-id="95b71-113">Az új parancsfájl létrehozása</span><span class="sxs-lookup"><span data-stu-id="95b71-113">To create a new script file</span></span>
<span data-ttu-id="95b71-114">Kattintson az eszköztár **új** , vagy a **fájl** menüben kattintson **új**.</span><span class="sxs-lookup"><span data-stu-id="95b71-114">On the toolbar, click **New** , or on the **File** menu, click **New**.</span></span> <span data-ttu-id="95b71-115">A létrehozott fájl az aktuális PowerShell lapon új fájl lapon jelenik meg. Ne feledje, hogy a PowerShell fülek láthatók csak ha egynél több.</span><span class="sxs-lookup"><span data-stu-id="95b71-115">The created file appears in a new file tab under the current PowerShell tab. Remember that the PowerShell tabs are only visible when there are more than one.</span></span> <span data-ttu-id="95b71-116">Alapértelmezés szerint a fájl típusa parancsfájl (.ps1) létrejött, de egy olyan új nevét és kiterjesztését is menthető.</span><span class="sxs-lookup"><span data-stu-id="95b71-116">By default a file of type script (.ps1) is created, but it can be saved with a new name and extension.</span></span> <span data-ttu-id="95b71-117">Több parancsfájlok ugyanazon a PowerShell lapon hozhatók létre.</span><span class="sxs-lookup"><span data-stu-id="95b71-117">Multiple script files can be created in the same PowerShell tab.</span></span>

### <a name="to-open-an-existing-script"></a><span data-ttu-id="95b71-118">Egy meglévő parancsfájl megnyitása</span><span class="sxs-lookup"><span data-stu-id="95b71-118">To open an existing script</span></span>
<span data-ttu-id="95b71-119">Kattintson az eszköztár **nyitott**, vagy a a **fájl** menüben kattintson **nyissa meg**.</span><span class="sxs-lookup"><span data-stu-id="95b71-119">On the toolbar, click **Open**, or on the **File** menu, click **Open**.</span></span> <span data-ttu-id="95b71-120">Az a **nyissa meg a** párbeszédpanelen jelölje ki a megnyitni kívánt fájlt.</span><span class="sxs-lookup"><span data-stu-id="95b71-120">In the **Open** dialog box, select the file you want to open.</span></span> <span data-ttu-id="95b71-121">A megnyitott fájlt egy új lapon jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="95b71-121">The opened file appears in a new tab.</span></span>

### <a name="to-close-a-script-tab"></a><span data-ttu-id="95b71-122">A parancsfájl lap bezárásához</span><span class="sxs-lookup"><span data-stu-id="95b71-122">To close a script tab</span></span>
<span data-ttu-id="95b71-123">A parancsfájl bezárja a parancsfájl lapon, majd tegye a következők egyikét:</span><span class="sxs-lookup"><span data-stu-id="95b71-123">Click the script tab of the script you want to close, then do one of the following:</span></span>

1. <span data-ttu-id="95b71-124">Kattintson a **Bezárás** (X) ikonra, a parancsfájl fülre.</span><span class="sxs-lookup"><span data-stu-id="95b71-124">Click the **Close** icon (X) on the script tab.</span></span>

2. <span data-ttu-id="95b71-125">Az a **fájl** menüben kattintson a **Bezárás**.</span><span class="sxs-lookup"><span data-stu-id="95b71-125">On the **File** menu, click **Close**.</span></span>

<span data-ttu-id="95b71-126">Ha a fájl utolsó mentése óta módosították, mentse vagy vesse el, hogy kéri.</span><span class="sxs-lookup"><span data-stu-id="95b71-126">If the file has been altered since it was last saved, you are prompted to save or discard it.</span></span>

### <a name="to-display-the-file-path"></a><span data-ttu-id="95b71-127">A fájl elérési útjának megjelenítése</span><span class="sxs-lookup"><span data-stu-id="95b71-127">To display the file path</span></span>
<span data-ttu-id="95b71-128">A Fájl fülre mutasson a fájl nevét.</span><span class="sxs-lookup"><span data-stu-id="95b71-128">On the file tab, point to the file name.</span></span> <span data-ttu-id="95b71-129">A parancsfájlban a teljes elérési útja megjelenik egy elemleírás.</span><span class="sxs-lookup"><span data-stu-id="95b71-129">The fully qualified path to the script file appears in a tooltip.</span></span>

### <a name="to-run-a-script"></a><span data-ttu-id="95b71-130">Parancsfájl futtatása</span><span class="sxs-lookup"><span data-stu-id="95b71-130">To run a script</span></span>
<span data-ttu-id="95b71-131">Kattintson az eszköztár **-parancsfájl futtatása**, vagy a a **fájl** menüben kattintson a **futtatása**.</span><span class="sxs-lookup"><span data-stu-id="95b71-131">On the toolbar, click **Run Script**, or on the **File** menu, click **Run**.</span></span>

### <a name="to-run-a-portion-of-a-script"></a><span data-ttu-id="95b71-132">Egy része egy parancsfájl futtatásához</span><span class="sxs-lookup"><span data-stu-id="95b71-132">To run a portion of a script</span></span>

1. <span data-ttu-id="95b71-133">A parancsfájl ablaktáblában jelölje ki a parancsfájl egy részét.</span><span class="sxs-lookup"><span data-stu-id="95b71-133">In the Script Pane, select a portion of a script.</span></span>

2. <span data-ttu-id="95b71-134">A a **fájl** menüben kattintson a **kijelölés futtatása**, vagy kattintson az eszköztár **kijelölés futtatása**.</span><span class="sxs-lookup"><span data-stu-id="95b71-134">On the **File** menu, click **Run Selection**, or on the toolbar, click **Run Selection**.</span></span>

### <a name="to-stop-a-running-script"></a><span data-ttu-id="95b71-135">Leállítja a futó parancsfájlt</span><span class="sxs-lookup"><span data-stu-id="95b71-135">To stop a running script</span></span>
<span data-ttu-id="95b71-136">Kattintson az eszköztár **művelet leállítása**, nyomja le a CTRL + BREAK, vagy a a **fájl** menüben kattintson a **művelet leállítása**.</span><span class="sxs-lookup"><span data-stu-id="95b71-136">On the toolbar, click **Stop Operation**, press CTRL+BREAK, or on the **File** menu, click **Stop Operation**.</span></span> <span data-ttu-id="95b71-137">Nyomja le **CTRL + C** is működik, kivéve, ha néhány szöveg van kijelölve, ebben az esetben **CTRL + C** a másolási funkcióhoz a kijelölt szöveg van leképezve.</span><span class="sxs-lookup"><span data-stu-id="95b71-137">Pressing **CTRL+C** also works unless some text is currently selected, in which case **CTRL+C** maps to the copy function for the selected text.</span></span>

## <a name="how-to-write-and-edit-text-in-the-script-pane"></a><span data-ttu-id="95b71-138">Írása, és a parancssori panelbe szöveg szerkesztése</span><span class="sxs-lookup"><span data-stu-id="95b71-138">How to write and edit text in the Script Pane</span></span>
<span data-ttu-id="95b71-139">Az alábbi lépések segítségével panelbe szöveg szerkesztése.</span><span class="sxs-lookup"><span data-stu-id="95b71-139">Use the following steps to edit text in the Script Pane.</span></span> <span data-ttu-id="95b71-140">Akkor is másolja, Kivágás, beillesztés, szöveg keresése és cseréje.</span><span class="sxs-lookup"><span data-stu-id="95b71-140">You can copy, cut, paste, find, and replace text.</span></span> <span data-ttu-id="95b71-141">Is visszavonja, és az utolsó végrehajtott művelet.</span><span class="sxs-lookup"><span data-stu-id="95b71-141">You can also undo and redo the last action you just performed.</span></span> <span data-ttu-id="95b71-142">Ezekhez a billentyűparancsok ugyanazok, mint az összes Windows-alkalmazások.</span><span class="sxs-lookup"><span data-stu-id="95b71-142">The keyboard shortcuts for performing these actions are the same as those used for all Windows applications.</span></span>

### <a name="to-enter-text-in-the-script-pane"></a><span data-ttu-id="95b71-143">Szöveg bevitele a parancssori panelbe</span><span class="sxs-lookup"><span data-stu-id="95b71-143">To enter text in the Script Pane</span></span>

1. <span data-ttu-id="95b71-144">Húzza az egérmutatót a parancssori panelbe bárhova kattinthat a parancssori panelbe, vagy úgy **nyissa meg a parancssori panelbe** a a **nézet** menü.</span><span class="sxs-lookup"><span data-stu-id="95b71-144">Move the cursor to the Script Pane by clicking anywhere in the Script Pane, or by clicking **Go to Script Pane** in the **View** menu.</span></span>

2. <span data-ttu-id="95b71-145">Hozzon létre egy parancsfájlt.</span><span class="sxs-lookup"><span data-stu-id="95b71-145">Create a script.</span></span> <span data-ttu-id="95b71-146">Zintaxisszínek és kiegészítést legyen ez egy gazdagabb élmény a Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="95b71-146">Syntax coloring and tab completion make this a richer experience in Windows PowerShell ISE.</span></span>

3. <span data-ttu-id="95b71-147">Lásd: [kiegészítést használja a parancsfájl és a konzol ablaktáblában hogyan](How-to-Use-Tab-Completion-in-the-Script-Pane-and-Console-Pane.md) segítő írja be a lapon kiegészítési funkció használatáról részleteket.</span><span class="sxs-lookup"><span data-stu-id="95b71-147">See [How to Use Tab Completion in the Script Pane and Console Pane](How-to-Use-Tab-Completion-in-the-Script-Pane-and-Console-Pane.md) for details about using the tab completion feature to help in typing.</span></span>

### <a name="to-find-text-in-the-script-pane"></a><span data-ttu-id="95b71-148">A parancssori panelbe szöveg keresése</span><span class="sxs-lookup"><span data-stu-id="95b71-148">To find text in the Script Pane</span></span>

1. <span data-ttu-id="95b71-149">Szöveg bárhol megkereséséhez nyomja le az **CTRL + F** vagy a a **szerkesztése** menüben kattintson a **parancsfájl található**.</span><span class="sxs-lookup"><span data-stu-id="95b71-149">To find text anywhere, press **CTRL+F** or, on the **Edit** menu, click **Find in Script**.</span></span>

2. <span data-ttu-id="95b71-150">A kurzor utáni szöveg megkereséséhez nyomja le az **F3** vagy a a **szerkesztése** menüben kattintson a **következő parancsfájlban**.</span><span class="sxs-lookup"><span data-stu-id="95b71-150">To find text after the cursor, press **F3** or, on the **Edit** menu, click **Find Next in Script**.</span></span>

3. <span data-ttu-id="95b71-151">A kurzor előtti szöveg megkereséséhez nyomja le az **SHIFT + F3** vagy a a **szerkesztése** menüben kattintson a **előző parancsfájlban**.</span><span class="sxs-lookup"><span data-stu-id="95b71-151">To find text before the cursor, press **SHIFT+F3** or, on the **Edit** menu, click **Find Previous in Script**.</span></span>

### <a name="to-find-and-replace-text-in-the-script-pane"></a><span data-ttu-id="95b71-152">A parancssori panelbe szöveg keresése és cseréje</span><span class="sxs-lookup"><span data-stu-id="95b71-152">To find and replace text in the Script Pane</span></span>
<span data-ttu-id="95b71-153">Nyomja le az **CTRL + H** vagy a a **szerkesztése** menüben kattintson a **cserélje le a parancsfájl**.</span><span class="sxs-lookup"><span data-stu-id="95b71-153">Press **CRTL+H** or, on the **Edit** menu, click **Replace in Script**.</span></span> <span data-ttu-id="95b71-154">Adja meg mind a keresett szöveget, és a szöveg, amellyel cserélje le azt, és nyomja le az **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="95b71-154">Enter both the text you want to find and the text with which you want to replace it, and then press **ENTER**.</span></span>

### <a name="to-go-to-a-particular-line-of-text-in-the-script-pane"></a><span data-ttu-id="95b71-155">Ugrás a parancsfájl ablaktáblán egy adott szövegsor</span><span class="sxs-lookup"><span data-stu-id="95b71-155">To go to a particular line of text in the Script Pane</span></span>

1. <span data-ttu-id="95b71-156">A parancsfájl ablaktáblán nyomja le az **CTRL + G** vagy a a **szerkesztése** menüben kattintson **sor Ugrás**.</span><span class="sxs-lookup"><span data-stu-id="95b71-156">In the Script Pane, press **CTRL+G** or, on the **Edit** menu, click **Go to Line**.</span></span>

2. <span data-ttu-id="95b71-157">Adja meg a sor számát.</span><span class="sxs-lookup"><span data-stu-id="95b71-157">Enter a line number.</span></span>

### <a name="to-copy-text-in-the-script-pane"></a><span data-ttu-id="95b71-158">A parancssori panelbe szöveg másolása</span><span class="sxs-lookup"><span data-stu-id="95b71-158">To copy text in the Script Pane</span></span>

1. <span data-ttu-id="95b71-159">A parancsfájl ablaktáblában jelölje ki a másolni kívánt szöveg.</span><span class="sxs-lookup"><span data-stu-id="95b71-159">In the Script Pane, select the text that you want to copy.</span></span>

2. <span data-ttu-id="95b71-160">Nyomja le az **CTRL + C** vagy az eszköztáron kattintson a **másolási** ikonra, vagy a a **szerkesztése** menüben kattintson a **másolása**.</span><span class="sxs-lookup"><span data-stu-id="95b71-160">Press **CTRL+C** or, on the toolbar, click the **Copy** icon, or on the **Edit** menu, click **Copy**.</span></span>

### <a name="to-cut-text-in-the-script-pane"></a><span data-ttu-id="95b71-161">A parancssori panelbe szöveg kivágni</span><span class="sxs-lookup"><span data-stu-id="95b71-161">To cut text in the Script Pane</span></span>

1. <span data-ttu-id="95b71-162">A parancsfájl ablaktáblában jelölje ki a szöveget, amelyet szeretne kivágása.</span><span class="sxs-lookup"><span data-stu-id="95b71-162">In the Script Pane, select the text that you want to cut.</span></span>

2. <span data-ttu-id="95b71-163">Nyomja le az **CTRL + X** vagy az eszköztáron kattintson a **Kivágás** ikonra, vagy a a **szerkesztése** menüben kattintson a **Kivágás**.</span><span class="sxs-lookup"><span data-stu-id="95b71-163">Press **CTRL+X** or, on the toolbar, click the **Cut** icon, or on the **Edit** menu, click **Cut**.</span></span>

### <a name="to-paste-text-into-the-script-pane"></a><span data-ttu-id="95b71-164">Szöveg beillesztése a parancsfájl ablaktábla</span><span class="sxs-lookup"><span data-stu-id="95b71-164">To paste text into the Script Pane</span></span>
<span data-ttu-id="95b71-165">Nyomja le az **CTRL + V** vagy az eszköztáron kattintson a **Beillesztés** ikonra, vagy a a **szerkesztése** menüben kattintson a **Beillesztés**.</span><span class="sxs-lookup"><span data-stu-id="95b71-165">Press **CTRL+V** or, on the toolbar, click the **Paste** icon, or on the **Edit** menu, click **Paste**.</span></span>

### <a name="to-undo-an-action-in-the-script-pane"></a><span data-ttu-id="95b71-166">A parancssori panelbe művelet visszavonása</span><span class="sxs-lookup"><span data-stu-id="95b71-166">To undo an action in the Script Pane</span></span>
<span data-ttu-id="95b71-167">Nyomja le az **CTRL + Z** vagy az eszköztáron kattintson a **visszavonása** ikonra, vagy a a **szerkesztése** menüben kattintson a **visszavonása**.</span><span class="sxs-lookup"><span data-stu-id="95b71-167">Press **CTRL+Z** or, on the toolbar, click the **Undo** icon, or on the **Edit** menu, click **Undo**.</span></span>

### <a name="to-redo-an-action-in-the-script-pane"></a><span data-ttu-id="95b71-168">A parancssori panelbe művelet visszavonása</span><span class="sxs-lookup"><span data-stu-id="95b71-168">To redo an action in the Script Pane</span></span>
<span data-ttu-id="95b71-169">Nyomja le az **CTRL + Y** vagy az eszköztáron kattintson a **végezze el újra** ikonra, vagy a a **szerkesztése** menüben kattintson a **végezze el újra**.</span><span class="sxs-lookup"><span data-stu-id="95b71-169">Press **CTRL+Y** or, on the toolbar, click the **Redo** icon, or on the **Edit** menu, click **Redo**.</span></span>

## <a name="how-to-save-a-script"></a><span data-ttu-id="95b71-170">A parancsfájl mentése</span><span class="sxs-lookup"><span data-stu-id="95b71-170">How to save a script</span></span>
<span data-ttu-id="95b71-171">A következő lépésekkel mentéséhez és a parancsfájl neve.</span><span class="sxs-lookup"><span data-stu-id="95b71-171">Use the following steps to save and name a script.</span></span> <span data-ttu-id="95b71-172">Egy csillag megjelölni egy fájlt, amely nem lett mentve óta módosították, hogy a parancsfájl neve mellett jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="95b71-172">An asterisk appears next to the script name to mark a file that has not been saved since it was altered.</span></span> <span data-ttu-id="95b71-173">A csillag eltűnik, ha a fájl mentése.</span><span class="sxs-lookup"><span data-stu-id="95b71-173">The asterisk disappears when the file is saved.</span></span>

### <a name="to-save-a-script"></a><span data-ttu-id="95b71-174">A parancsfájl mentése</span><span class="sxs-lookup"><span data-stu-id="95b71-174">To save a script</span></span>
<span data-ttu-id="95b71-175">Nyomja le az **CTRL + S** vagy az eszköztáron kattintson a **mentése** ikonra, vagy a a **fájl** menüben kattintson a **mentése**.</span><span class="sxs-lookup"><span data-stu-id="95b71-175">Press **CTRL+S** or, on the toolbar, click the **Save** icon, or on the **File** menu, click **Save**.</span></span>

### <a name="to-save-and-name-a-script"></a><span data-ttu-id="95b71-176">A mentéshez és a parancsfájl neve</span><span class="sxs-lookup"><span data-stu-id="95b71-176">To save and name a script</span></span>

1. <span data-ttu-id="95b71-177">Az a **fájl** menüben kattintson a **Mentés másként**.</span><span class="sxs-lookup"><span data-stu-id="95b71-177">On the **File** menu, click **Save As**.</span></span> <span data-ttu-id="95b71-178">A **Mentés másként** párbeszédpanel jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="95b71-178">The **Save As** dialog box will appear.</span></span>

2. <span data-ttu-id="95b71-179">Az a **Fájlnév** mezőbe írja be a fájl nevét.</span><span class="sxs-lookup"><span data-stu-id="95b71-179">In the **File name** box, enter a name for the file.</span></span>

3. <span data-ttu-id="95b71-180">Az a **Fájltípus** jelölje ki a fájl típusa.</span><span class="sxs-lookup"><span data-stu-id="95b71-180">In the **Save as type** box, select a file type.</span></span> <span data-ttu-id="95b71-181">Például a **Fájltípus** mezőben jelölje ki "œPowerShell parancsfájlok (\* .ps1)".</span><span class="sxs-lookup"><span data-stu-id="95b71-181">For example, in the **Save as type** box, select 'œPowerShell Scripts (\* .ps1)'.</span></span>

4. <span data-ttu-id="95b71-182">Kattintson a **Save** (Mentés) gombra.</span><span class="sxs-lookup"><span data-stu-id="95b71-182">Click **Save**.</span></span>

### <a name="to-save-a-script-in-ascii-encoding"></a><span data-ttu-id="95b71-183">A parancsfájl mentése ASCII kódolással</span><span class="sxs-lookup"><span data-stu-id="95b71-183">To save a script in ASCII encoding</span></span>
<span data-ttu-id="95b71-184">Alapértelmezés szerint a Windows PowerShell ISE új parancsfájlokat (.ps1), parancsfájlok (.psd1) és parancsfájlok modul (.psm1) (BigEndianUnicode kódolás) Unicode-ként alapértelmezés szerint menti. Â mentse a parancsfájlt egy másik kódolással, például az ASCII (ANSI), használja a **mentése** vagy **SaveAs** metódusai a [$psISE.CurrentFile](https://technet.microsoft.com/en-us/library/bc3300e4-9c17-4f00-a621-c8867126e3b3#CurrentFile) objektum.</span><span class="sxs-lookup"><span data-stu-id="95b71-184">By default, Windows PowerShell ISE saves new script files (.ps1), script data files (.psd1), and script module files (.psm1) as Unicode (BigEndianUnicode) by default.Â To save a script in another encoding, such as ASCII (ANSI), use the **Save** or **SaveAs** methods on the [$psISE.CurrentFile](https://technet.microsoft.com/en-us/library/bc3300e4-9c17-4f00-a621-c8867126e3b3#CurrentFile) object.</span></span>

<span data-ttu-id="95b71-185">A következő parancsot egy új parancsfájlt parancsfájl.ps1 ASCII kódolással menti.</span><span class="sxs-lookup"><span data-stu-id="95b71-185">The following command saves a new script as MyScript.ps1 with ASCII encoding.</span></span>

```
$psise.CurrentFile.SaveAs("MyScript.ps1", [System.Text.Encoding]::ASCII)
```

<span data-ttu-id="95b71-186">A következő parancs lecseréli a jelenlegi parancsfájlt ugyanazzal a névvel, de ASCII kódolással.</span><span class="sxs-lookup"><span data-stu-id="95b71-186">The following command replaces the current script file with a file with the same name, but with ASCII encoding.</span></span>

```
$psise.CurrentFile.Save([System.Text.Encoding]::ASCII)
```

<span data-ttu-id="95b71-187">A következő paranccsal lekérdezi az aktuális fájl kódolási.</span><span class="sxs-lookup"><span data-stu-id="95b71-187">The following command gets the encoding of the current file.</span></span>

```
$psise.CurrentFile.encoding
```

<span data-ttu-id="95b71-188">A Windows PowerShell ISE támogatja a következő kódolási beállítások: ASCII, BigEndianUnicode kódolás, Unicode, UTF32, UTF7, UTF8 és alapértelmezett.</span><span class="sxs-lookup"><span data-stu-id="95b71-188">Windows PowerShell ISE supports the following encoding options: ASCII, BigEndianUnicode, Unicode, UTF32, UTF7, UTF8 and Default.</span></span> <span data-ttu-id="95b71-189">A rendszer az alapértelmezett beállítás értékének függ.</span><span class="sxs-lookup"><span data-stu-id="95b71-189">The value of the Default option varies with the system.</span></span>

<span data-ttu-id="95b71-190">A Windows PowerShell ISE nem változtatja meg más szerkesztők által létrehozott parancsfájlok kódolás Windows PowerShell ISE még ha használja a Mentés vagy a Mentés másként parancsokat.</span><span class="sxs-lookup"><span data-stu-id="95b71-190">Windows PowerShell ISE does not change the encoding of scripts that were created by in other editors, even when you use the Save or Save As commands in Windows PowerShell ISE.</span></span>

## <a name="see-also"></a><span data-ttu-id="95b71-191">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="95b71-191">See Also</span></span>
- [<span data-ttu-id="95b71-192">A Windows PowerShell ISE felfedezése</span><span class="sxs-lookup"><span data-stu-id="95b71-192">Exploring the Windows PowerShell ISE</span></span>](../../getting-started/fundamental/exploring-the-windows-powershell-ise.md)
