---
ms.date: 08/14/2018
keywords: PowerShell, a parancsmag
title: Parancsfájlok írása és futtatása a Windows PowerShell ISE-ben
ms.openlocfilehash: 4a08d7d206d103dcb398964d7ce75bea1e76559a
ms.sourcegitcommit: a6f13c16a535acea279c0ddeca72f1f0d8a8ce4c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2019
ms.locfileid: "67028972"
---
# <a name="how-to-write-and-run-scripts-in-the-windows-powershell-ise"></a><span data-ttu-id="6ec6f-103">Parancsfájlok írása és futtatása a Windows PowerShell ISE-ben</span><span class="sxs-lookup"><span data-stu-id="6ec6f-103">How to Write and Run Scripts in the Windows PowerShell ISE</span></span>

<span data-ttu-id="6ec6f-104">Ez a cikk ismerteti, hogyan létrehozása, szerkesztése, futtatása és mentése a parancsfájlokat a parancsfájl panelen.</span><span class="sxs-lookup"><span data-stu-id="6ec6f-104">This article describes how to create, edit, run, and save scripts in the Script Pane.</span></span>

## <a name="how-to-create-and-run-scripts"></a><span data-ttu-id="6ec6f-105">Hogyan hozhat létre és szkriptek futtatása</span><span class="sxs-lookup"><span data-stu-id="6ec6f-105">How to create and run scripts</span></span>

<span data-ttu-id="6ec6f-106">Megnyithatja és szerkesztheti a Windows PowerShell-fájlokat a parancsfájl panelen.</span><span class="sxs-lookup"><span data-stu-id="6ec6f-106">You can open and edit Windows PowerShell files in the Script Pane.</span></span> <span data-ttu-id="6ec6f-107">Adott fájltípusokat a lényeges a Windows PowerShell parancsfájlok (.ps1), parancsfájlok (.psd1) és parancsfájlok modul (.psm1).</span><span class="sxs-lookup"><span data-stu-id="6ec6f-107">Specific file types of interest in Windows PowerShell are script files (.ps1), script data files (.psd1), and script module files (.psm1).</span></span> <span data-ttu-id="6ec6f-108">Az ilyen a parancsfájl panelen szerkesztőben színes szintaxist.</span><span class="sxs-lookup"><span data-stu-id="6ec6f-108">These file types are syntax colored in the Script Pane editor.</span></span> <span data-ttu-id="6ec6f-109">Más közös fájltípusok megnyitásakor előfordulhat, hogy a parancsfájl panelen olyan konfigurációs fájlok (.ps1xml), XML-fájlok és szöveges fájlok.</span><span class="sxs-lookup"><span data-stu-id="6ec6f-109">Other common file types you may open in the Script Pane are configuration files (.ps1xml), XML files, and text files.</span></span>

> [!NOTE]
> <span data-ttu-id="6ec6f-110">A Windows PowerShell végrehajtási házirend határozza meg, hogy parancsfájlok futtatásához, és Windows PowerShell-profilok és konfigurációs fájlok betöltése.</span><span class="sxs-lookup"><span data-stu-id="6ec6f-110">The Windows PowerShell execution policy determines whether you can run scripts and load Windows PowerShell profiles and configuration files.</span></span> <span data-ttu-id="6ec6f-111">Az alapértelmezett végrehajtási házirend korlátozott, megakadályozza, hogy az összes parancsfájl futtatását, és megakadályozza, hogy a profilok betöltése.</span><span class="sxs-lookup"><span data-stu-id="6ec6f-111">The default execution policy, Restricted, prevents all scripts from running, and prevents loading profiles.</span></span> <span data-ttu-id="6ec6f-112">Ha módosítani szeretné a végrehajtási házirendet, hogy a profilok betölteni és használni, lásd: [Set-ExecutionPolicy](/powershell/module/microsoft.powershell.security/set-executionpolicy) és [about_Signing](/powershell/module/microsoft.powershell.core/about/about_signing).</span><span class="sxs-lookup"><span data-stu-id="6ec6f-112">To change the execution policy to allow profiles to load and be used, see [Set-ExecutionPolicy](/powershell/module/microsoft.powershell.security/set-executionpolicy) and [about_Signing](/powershell/module/microsoft.powershell.core/about/about_signing).</span></span>

### <a name="to-create-a-new-script-file"></a><span data-ttu-id="6ec6f-113">Az új parancsfájl létrehozása</span><span class="sxs-lookup"><span data-stu-id="6ec6f-113">To create a new script file</span></span>

<span data-ttu-id="6ec6f-114">Kattintson az eszköztár **új**, vagy a a **fájl** menüben kattintson a **új**.</span><span class="sxs-lookup"><span data-stu-id="6ec6f-114">On the toolbar, click **New**, or on the **File** menu, click **New**.</span></span> <span data-ttu-id="6ec6f-115">A létrehozott fájlt a jelenlegi PowerShell-lap egy új fájl lapján jelenik meg. Ne feledje, hogy a PowerShell-lapok láthatók csak ha egynél több.</span><span class="sxs-lookup"><span data-stu-id="6ec6f-115">The created file appears in a new file tab under the current PowerShell tab. Remember that the PowerShell tabs are only visible when there are more than one.</span></span> <span data-ttu-id="6ec6f-116">Alapértelmezés szerint létrejön egy fájl, a típus parancsprogramnak (.ps1), de egy új nevet és a kiterjesztéssel menthetők.</span><span class="sxs-lookup"><span data-stu-id="6ec6f-116">By default a file of type script (.ps1) is created, but it can be saved with a new name and extension.</span></span> <span data-ttu-id="6ec6f-117">Több parancsfájl-fájl is létrehozható PowerShell ugyanazon a lapon.</span><span class="sxs-lookup"><span data-stu-id="6ec6f-117">Multiple script files can be created in the same PowerShell tab.</span></span>

### <a name="to-open-an-existing-script"></a><span data-ttu-id="6ec6f-118">Meglévő parancsfájl megnyitása</span><span class="sxs-lookup"><span data-stu-id="6ec6f-118">To open an existing script</span></span>

<span data-ttu-id="6ec6f-119">Kattintson az eszköztár **nyissa meg**, vagy a a **fájl** menüben kattintson a **nyílt**.</span><span class="sxs-lookup"><span data-stu-id="6ec6f-119">On the toolbar, click **Open**, or on the **File** menu, click **Open**.</span></span> <span data-ttu-id="6ec6f-120">Az a **nyissa meg a** párbeszédpanelen jelölje ki a megnyitni kívánt fájlt.</span><span class="sxs-lookup"><span data-stu-id="6ec6f-120">In the **Open** dialog box, select the file you want to open.</span></span> <span data-ttu-id="6ec6f-121">A megnyitott fájlt egy új lapon jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="6ec6f-121">The opened file appears in a new tab.</span></span>

### <a name="to-close-a-script-tab"></a><span data-ttu-id="6ec6f-122">A parancsfájl lap bezárása</span><span class="sxs-lookup"><span data-stu-id="6ec6f-122">To close a script tab</span></span>

<span data-ttu-id="6ec6f-123">Kattintson a **bezárásához** (X) ikonra a fájl lap szeretné zárja be, vagy válassza ki a **fájl** menüben, majd kattintson **bezárásához**.</span><span class="sxs-lookup"><span data-stu-id="6ec6f-123">Click the **Close** icon (X) of the file tab you want to close or select the **File** menu and click **Close**.</span></span>

<span data-ttu-id="6ec6f-124">Ha a fájl utolsó mentése óta módosítva lett, mentse vagy vesse el, hogy kéri.</span><span class="sxs-lookup"><span data-stu-id="6ec6f-124">If the file has been altered since it was last saved, you're prompted to save or discard it.</span></span>

### <a name="to-display-the-file-path"></a><span data-ttu-id="6ec6f-125">A fájl elérési útja megjelenítése</span><span class="sxs-lookup"><span data-stu-id="6ec6f-125">To display the file path</span></span>

<span data-ttu-id="6ec6f-126">A fájl lapon mutasson a fájl nevét.</span><span class="sxs-lookup"><span data-stu-id="6ec6f-126">On the file tab, point to the file name.</span></span> <span data-ttu-id="6ec6f-127">A teljes elérési útját a parancsfájl egy elemleírás jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="6ec6f-127">The fully qualified path to the script file appears in a tooltip.</span></span>

### <a name="to-run-a-script"></a><span data-ttu-id="6ec6f-128">Parancsfájl futtatása</span><span class="sxs-lookup"><span data-stu-id="6ec6f-128">To run a script</span></span>

<span data-ttu-id="6ec6f-129">Kattintson az eszköztár **parancsfájl futtatása**, vagy a a **fájl** menüben kattintson a **futtatása**.</span><span class="sxs-lookup"><span data-stu-id="6ec6f-129">On the toolbar, click **Run Script**, or on the **File** menu, click **Run**.</span></span>

### <a name="to-run-a-portion-of-a-script"></a><span data-ttu-id="6ec6f-130">Egy része egy parancsfájl futtatása</span><span class="sxs-lookup"><span data-stu-id="6ec6f-130">To run a portion of a script</span></span>

1. <span data-ttu-id="6ec6f-131">A parancsfájl panelen válassza ki a parancsfájl egy részét.</span><span class="sxs-lookup"><span data-stu-id="6ec6f-131">In the Script Pane, select a portion of a script.</span></span>
2. <span data-ttu-id="6ec6f-132">Az a **fájl** menüben kattintson a **kijelölés futtatása**, vagy kattintson az eszköztár **kijelölés futtatása**.</span><span class="sxs-lookup"><span data-stu-id="6ec6f-132">On the **File** menu, click **Run Selection**, or on the toolbar, click **Run Selection**.</span></span>

### <a name="to-stop-a-running-script"></a><span data-ttu-id="6ec6f-133">Leállítja a parancsprogram futtatásához</span><span class="sxs-lookup"><span data-stu-id="6ec6f-133">To stop a running script</span></span>

<span data-ttu-id="6ec6f-134">Többféleképpen is lehet leállítani a parancsfájl futtatását.</span><span class="sxs-lookup"><span data-stu-id="6ec6f-134">There are several ways to stop a running script.</span></span>

- <span data-ttu-id="6ec6f-135">Kattintson a **leállítása műveletet** eszköztár</span><span class="sxs-lookup"><span data-stu-id="6ec6f-135">Click **Stop Operation** on the toolbar</span></span>
- <span data-ttu-id="6ec6f-136">Nyomja le a CTRL + BREAK</span><span class="sxs-lookup"><span data-stu-id="6ec6f-136">Press CTRL+BREAK</span></span>
- <span data-ttu-id="6ec6f-137">Válassza ki a **fájl** menüben, majd kattintson **leállítása műveletet**.</span><span class="sxs-lookup"><span data-stu-id="6ec6f-137">Select the **File** menu and click **Stop Operation**.</span></span>

<span data-ttu-id="6ec6f-138">Billentyű **CTRL + C** is működik, hacsak a szöveg van kijelölve, ebben az esetben **CTRL + C** leképezi a másolási funkcióhoz a kijelölt szöveg.</span><span class="sxs-lookup"><span data-stu-id="6ec6f-138">Pressing **CTRL+C** also works unless some text is currently selected, in which case **CTRL+C** maps to the copy function for the selected text.</span></span>

## <a name="how-to-write-and-edit-text-in-the-script-pane"></a><span data-ttu-id="6ec6f-139">Írása, és a parancsfájl panelen szöveg szerkesztése</span><span class="sxs-lookup"><span data-stu-id="6ec6f-139">How to write and edit text in the Script Pane</span></span>

<span data-ttu-id="6ec6f-140">Akkor is másolás, Kivágás, illessze be, szöveg keresése és cseréje a parancsfájl panelen.</span><span class="sxs-lookup"><span data-stu-id="6ec6f-140">You can copy, cut, paste, find, and replace text in the Script Pane.</span></span> <span data-ttu-id="6ec6f-141">Visszavonás is, és az iménti az utolsó művelet megismétlése.</span><span class="sxs-lookup"><span data-stu-id="6ec6f-141">You can also undo and redo the last action you just performed.</span></span> <span data-ttu-id="6ec6f-142">Ezek a műveletek billentyűparancsai a azonos parancsikonjait, az összes Windows-alkalmazásokhoz használható.</span><span class="sxs-lookup"><span data-stu-id="6ec6f-142">The keyboard shortcuts for these actions are the same shortcuts used for all Windows applications.</span></span>

### <a name="to-enter-text-in-the-script-pane"></a><span data-ttu-id="6ec6f-143">Szöveg bevitele a parancsfájl panelen</span><span class="sxs-lookup"><span data-stu-id="6ec6f-143">To enter text in the Script Pane</span></span>

1. <span data-ttu-id="6ec6f-144">A kurzor elmozdítása a parancsfájl panelen, a parancsfájl panelen egy tetszőleges pontjára kattint, vagy kattintson **Ugrás a parancsfájl panelen** a a **nézet** menü.</span><span class="sxs-lookup"><span data-stu-id="6ec6f-144">Move the cursor to the Script Pane by clicking anywhere in the Script Pane, or by clicking **Go to Script Pane** in the **View** menu.</span></span>
2. <span data-ttu-id="6ec6f-145">Hozzon létre egy parancsfájlt.</span><span class="sxs-lookup"><span data-stu-id="6ec6f-145">Create a script.</span></span> <span data-ttu-id="6ec6f-146">Szintaxis színezés és kiegészítés adjon meg egy gazdagabb szerkesztési funkciót a Windows PowerShell ISE-ben.</span><span class="sxs-lookup"><span data-stu-id="6ec6f-146">Syntax coloring and tab completion provide a richer editing experience in Windows PowerShell ISE.</span></span>
3. <span data-ttu-id="6ec6f-147">Lásd: [kiegészítés használata a parancsfájl panelen és a konzol ablaktáblában hogyan](How-to-Use-Tab-Completion-in-the-Script-Pane-and-Console-Pane.md) segítheti a írja be a lapon kiegészítési funkció használatával.</span><span class="sxs-lookup"><span data-stu-id="6ec6f-147">See [How to Use Tab Completion in the Script Pane and Console Pane](How-to-Use-Tab-Completion-in-the-Script-Pane-and-Console-Pane.md) for details about using the tab completion feature to help in typing.</span></span>

### <a name="to-find-text-in-the-script-pane"></a><span data-ttu-id="6ec6f-148">A parancsfájl panelen belüli szövegek megkeresése</span><span class="sxs-lookup"><span data-stu-id="6ec6f-148">To find text in the Script Pane</span></span>

1. <span data-ttu-id="6ec6f-149">Szöveg bárhol megkereséséhez nyomja le az ENTER **CTRL + F** vagy a a **szerkesztése** menüben kattintson a **parancsfájl található**.</span><span class="sxs-lookup"><span data-stu-id="6ec6f-149">To find text anywhere, press **CTRL+F** or, on the **Edit** menu, click **Find in Script**.</span></span>
2. <span data-ttu-id="6ec6f-150">Szöveg keresése a kurzor utáni, nyomja le a **F3** vagy a a **szerkesztése** menüben kattintson a **következő parancsfájlban**.</span><span class="sxs-lookup"><span data-stu-id="6ec6f-150">To find text after the cursor, press **F3** or, on the **Edit** menu, click **Find Next in Script**.</span></span>
3. <span data-ttu-id="6ec6f-151">A kurzor előtti szöveg megkereséséhez nyomja le az ENTER **SHIFT + F3** vagy a a **szerkesztése** menüben kattintson a **előző szkriptben**.</span><span class="sxs-lookup"><span data-stu-id="6ec6f-151">To find text before the cursor, press **SHIFT+F3** or, on the **Edit** menu, click **Find Previous in Script**.</span></span>

### <a name="to-find-and-replace-text-in-the-script-pane"></a><span data-ttu-id="6ec6f-152">A parancssori panelbe szöveg keresése és cseréje</span><span class="sxs-lookup"><span data-stu-id="6ec6f-152">To find and replace text in the Script Pane</span></span>

<span data-ttu-id="6ec6f-153">Nyomja meg **CTRL + H** vagy a a **szerkesztése** menüben kattintson a **cserélje le a parancsfájl**.</span><span class="sxs-lookup"><span data-stu-id="6ec6f-153">Press **CTRL+H** or, on the **Edit** menu, click **Replace in Script**.</span></span> <span data-ttu-id="6ec6f-154">Adja meg a szöveg keresése és a cseréhez használandó szöveg nyomja le az **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="6ec6f-154">Enter the text you want to find and the replacement text, then press **ENTER**.</span></span>

### <a name="to-go-to-a-particular-line-of-text-in-the-script-pane"></a><span data-ttu-id="6ec6f-155">Ugrás a parancsfájl panelen egy adott szövegsor</span><span class="sxs-lookup"><span data-stu-id="6ec6f-155">To go to a particular line of text in the Script Pane</span></span>

1. <span data-ttu-id="6ec6f-156">Nyomja le a parancsfájl panelen **CTRL + G** vagy a a **szerkesztése** menüben kattintson a **lépjen sorra**.</span><span class="sxs-lookup"><span data-stu-id="6ec6f-156">In the Script Pane, press **CTRL+G** or, on the **Edit** menu, click **Go to Line**.</span></span>

2. <span data-ttu-id="6ec6f-157">Adjon meg egy sor száma.</span><span class="sxs-lookup"><span data-stu-id="6ec6f-157">Enter a line number.</span></span>

### <a name="to-copy-text-in-the-script-pane"></a><span data-ttu-id="6ec6f-158">A parancsfájl panelen szöveg másolása</span><span class="sxs-lookup"><span data-stu-id="6ec6f-158">To copy text in the Script Pane</span></span>

1. <span data-ttu-id="6ec6f-159">A parancsfájl panelen válassza ki a másolni kívánt szöveg.</span><span class="sxs-lookup"><span data-stu-id="6ec6f-159">In the Script Pane, select the text that you want to copy.</span></span>

2. <span data-ttu-id="6ec6f-160">Nyomja meg **CTRL + C** vagy az eszköztáron kattintson a **másolási** ikonra, vagy a a **szerkesztése** menüben kattintson a **másolási**.</span><span class="sxs-lookup"><span data-stu-id="6ec6f-160">Press **CTRL+C** or, on the toolbar, click the **Copy** icon, or on the **Edit** menu, click **Copy**.</span></span>

### <a name="to-cut-text-in-the-script-pane"></a><span data-ttu-id="6ec6f-161">A parancsfájl panelen szöveg kivágása</span><span class="sxs-lookup"><span data-stu-id="6ec6f-161">To cut text in the Script Pane</span></span>

1. <span data-ttu-id="6ec6f-162">A parancsfájl panelen válassza ki a Kivágás kívánt szöveg.</span><span class="sxs-lookup"><span data-stu-id="6ec6f-162">In the Script Pane, select the text that you want to cut.</span></span>
2. <span data-ttu-id="6ec6f-163">Nyomja meg **CTRL + X** vagy az eszköztáron kattintson a **Kivágás** ikonra, vagy a a **szerkesztése** menüben kattintson a **Kivágás**.</span><span class="sxs-lookup"><span data-stu-id="6ec6f-163">Press **CTRL+X** or, on the toolbar, click the **Cut** icon, or on the **Edit** menu, click **Cut**.</span></span>

### <a name="to-paste-text-into-the-script-pane"></a><span data-ttu-id="6ec6f-164">Szöveg beillesztése a parancsfájl panelen</span><span class="sxs-lookup"><span data-stu-id="6ec6f-164">To paste text into the Script Pane</span></span>

<span data-ttu-id="6ec6f-165">Nyomja meg **CTRL + V** vagy az eszköztáron kattintson a **beillesztési** ikonra, vagy a a **szerkesztése** menüben kattintson a **beillesztési**.</span><span class="sxs-lookup"><span data-stu-id="6ec6f-165">Press **CTRL+V** or, on the toolbar, click the **Paste** icon, or on the **Edit** menu, click **Paste**.</span></span>

### <a name="to-undo-an-action-in-the-script-pane"></a><span data-ttu-id="6ec6f-166">A parancsfájl panelen művelet visszavonása</span><span class="sxs-lookup"><span data-stu-id="6ec6f-166">To undo an action in the Script Pane</span></span>

<span data-ttu-id="6ec6f-167">Nyomja meg **CTRL + Z** vagy az eszköztáron kattintson a **visszavonása** ikonra, vagy a a **szerkesztése** menüben kattintson a **visszavonása**.</span><span class="sxs-lookup"><span data-stu-id="6ec6f-167">Press **CTRL+Z** or, on the toolbar, click the **Undo** icon, or on the **Edit** menu, click **Undo**.</span></span>

### <a name="to-redo-an-action-in-the-script-pane"></a><span data-ttu-id="6ec6f-168">A parancsfájl panelen művelet visszavonása</span><span class="sxs-lookup"><span data-stu-id="6ec6f-168">To redo an action in the Script Pane</span></span>

<span data-ttu-id="6ec6f-169">Nyomja meg **CTRL + Y** vagy az eszköztáron kattintson a **újra elvégzi** ikonra, vagy a a **szerkesztése** menüben kattintson a **ismétlése**.</span><span class="sxs-lookup"><span data-stu-id="6ec6f-169">Press **CTRL+Y** or, on the toolbar, click the **Redo** icon, or on the **Edit** menu, click **Redo**.</span></span>

## <a name="how-to-save-a-script"></a><span data-ttu-id="6ec6f-170">A parancsfájl mentése</span><span class="sxs-lookup"><span data-stu-id="6ec6f-170">How to save a script</span></span>

<span data-ttu-id="6ec6f-171">Egy csillag megjelölni egy fájlt, amely még nem mentette, mert megváltozott a szkript neve mellett jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="6ec6f-171">An asterisk appears next to the script name to mark a file that hasn't been saved since it was changed.</span></span> <span data-ttu-id="6ec6f-172">A csillag eltűnik a fájl mentésekor.</span><span class="sxs-lookup"><span data-stu-id="6ec6f-172">The asterisk disappears when the file is saved.</span></span>

### <a name="to-save-a-script"></a><span data-ttu-id="6ec6f-173">A parancsfájl mentése</span><span class="sxs-lookup"><span data-stu-id="6ec6f-173">To save a script</span></span>

<span data-ttu-id="6ec6f-174">Nyomja meg **CTRL + S** vagy az eszköztáron kattintson a **mentése** ikonra, vagy a a **fájl** menüben kattintson a **mentése**.</span><span class="sxs-lookup"><span data-stu-id="6ec6f-174">Press **CTRL+S** or, on the toolbar, click the **Save** icon, or on the **File** menu, click **Save**.</span></span>

### <a name="to-save-and-name-a-script"></a><span data-ttu-id="6ec6f-175">Mentéséhez és a egy parancsfájl neve</span><span class="sxs-lookup"><span data-stu-id="6ec6f-175">To save and name a script</span></span>

1. <span data-ttu-id="6ec6f-176">Az a **fájl** menüben kattintson a **Mentés másként**.</span><span class="sxs-lookup"><span data-stu-id="6ec6f-176">On the **File** menu, click **Save As**.</span></span> <span data-ttu-id="6ec6f-177">A **Mentés másként** párbeszédpanel fog megjelenni.</span><span class="sxs-lookup"><span data-stu-id="6ec6f-177">The **Save As** dialog box will appear.</span></span>
2. <span data-ttu-id="6ec6f-178">Az a **Fájlnév** mezőbe írja be a fájl nevét.</span><span class="sxs-lookup"><span data-stu-id="6ec6f-178">In the **File name** box, enter a name for the file.</span></span>
3. <span data-ttu-id="6ec6f-179">Az a **Fájltípus** jelölje ki a fájl típusa.</span><span class="sxs-lookup"><span data-stu-id="6ec6f-179">In the **Save as type** box, select a file type.</span></span> <span data-ttu-id="6ec6f-180">Például a **Fájltípus** jelölje ki "PowerShell-parancsfájlok (\*.ps1)".</span><span class="sxs-lookup"><span data-stu-id="6ec6f-180">For example, in the **Save as type** box, select 'PowerShell Scripts (\*.ps1)'.</span></span>
4. <span data-ttu-id="6ec6f-181">Kattintson a **Save** (Mentés) gombra.</span><span class="sxs-lookup"><span data-stu-id="6ec6f-181">Click **Save**.</span></span>

### <a name="to-save-a-script-in-ascii-encoding"></a><span data-ttu-id="6ec6f-182">A parancsfájl mentéséhez ASCII-kódolás</span><span class="sxs-lookup"><span data-stu-id="6ec6f-182">To save a script in ASCII encoding</span></span>

<span data-ttu-id="6ec6f-183">Alapértelmezés szerint Windows PowerShell ISE-ben új parancsfájlok (.ps1), parancsfájlok (.psd1) és parancsfájlok modul (.psm1), Unicode a (BigEndianUnicode kódolás) alapértelmezés szerint menti. Â mentse a parancsfájlt egy másik kódolással, például az ASCII (ANSI), használja a **mentése** vagy **Mentés másként** metódusokat a [$psISE.CurrentFile](object-model/the-ise-object-model-hierarchy.md) objektum.</span><span class="sxs-lookup"><span data-stu-id="6ec6f-183">By default, Windows PowerShell ISE saves new script files (.ps1), script data files (.psd1), and script module files (.psm1) as Unicode (BigEndianUnicode) by default.Â To save a script in another encoding, such as ASCII (ANSI), use the **Save** or **SaveAs** methods on the [$psISE.CurrentFile](object-model/the-ise-object-model-hierarchy.md) object.</span></span>

<span data-ttu-id="6ec6f-184">A következő parancsot egy új parancsfájl parancsfájl.ps1 ASCII kódolással menti.</span><span class="sxs-lookup"><span data-stu-id="6ec6f-184">The following command saves a new script as MyScript.ps1 with ASCII encoding.</span></span>

```powershell
$psISE.CurrentFile.SaveAs("MyScript.ps1", [System.Text.Encoding]::ASCII)
```

<span data-ttu-id="6ec6f-185">A következő parancs ugyanazzal a névvel, de a kódolással ASCII fájl lecseréli a jelenlegi parancsfájlt.</span><span class="sxs-lookup"><span data-stu-id="6ec6f-185">The following command replaces the current script file with a file with the same name, but with ASCII encoding.</span></span>

```powershell
$psISE.CurrentFile.Save([System.Text.Encoding]::ASCII)
```

<span data-ttu-id="6ec6f-186">Az alábbi parancs lekéri az aktuális fájl kódolási.</span><span class="sxs-lookup"><span data-stu-id="6ec6f-186">The following command gets the encoding of the current file.</span></span>

```powershell
$psISE.CurrentFile.encoding
```

<span data-ttu-id="6ec6f-187">Windows PowerShell ISE-ben a következő kódolási beállításokat támogatja: ASCII, Toto, Unicode, UTF32, UTF7, UTF8 és alapértelmezett.</span><span class="sxs-lookup"><span data-stu-id="6ec6f-187">Windows PowerShell ISE supports the following encoding options: ASCII, BigEndianUnicode, Unicode, UTF32, UTF7, UTF8, and Default.</span></span> <span data-ttu-id="6ec6f-188">Az alapértelmezett beállítás értékét a rendszer függ.</span><span class="sxs-lookup"><span data-stu-id="6ec6f-188">The value of the Default option varies with the system.</span></span>

<span data-ttu-id="6ec6f-189">Windows PowerShell ISE parancsfájl-fájlok kódolást, ha a Mentés vagy a Mentés másként nem változik parancsokat.</span><span class="sxs-lookup"><span data-stu-id="6ec6f-189">Windows PowerShell ISE doesn't change the encoding of script files when you use the Save or Save As commands.</span></span>

## <a name="see-also"></a><span data-ttu-id="6ec6f-190">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="6ec6f-190">See Also</span></span>

- [<span data-ttu-id="6ec6f-191">A Windows PowerShell ISE felfedezése</span><span class="sxs-lookup"><span data-stu-id="6ec6f-191">Exploring the Windows PowerShell ISE</span></span>](../../getting-started/fundamental/exploring-the-windows-powershell-ise.md)
