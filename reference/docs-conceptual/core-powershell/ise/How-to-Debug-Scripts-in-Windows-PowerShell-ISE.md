---
ms.date: 06/05/2017
keywords: PowerShell parancsmag
title: Parancsfájlokban való hibakeresés a PowerShell ISE-ben
ms.openlocfilehash: b7af2de83a3f796a2057514e36ad8b74367e8ce2
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="how-to-debug-scripts-in-windows-powershell-ise"></a><span data-ttu-id="c4902-103">Parancsfájlokban való hibakeresés a PowerShell ISE-ben</span><span class="sxs-lookup"><span data-stu-id="c4902-103">How to Debug Scripts in Windows PowerShell ISE</span></span>

<span data-ttu-id="c4902-104">Ez a cikk ismerteti a helyi számítógép parancsfájlok hibakeresése a Windows PowerShell integrált parancsfájlkezelési környezet (ISE) visual hibakeresési szolgáltatások segítségével.</span><span class="sxs-lookup"><span data-stu-id="c4902-104">This article describes how to debug scripts on a local computer by using the Windows PowerShell Integrated Scripting Environment (ISE) visual debugging features.</span></span>

## <a name="how-to-manage-breakpoints"></a><span data-ttu-id="c4902-105">Töréspontokat kezelése</span><span class="sxs-lookup"><span data-stu-id="c4902-105">How to manage breakpoints</span></span>

<span data-ttu-id="c4902-106">Töréspont a kijelölt helyszínen egy parancsfájlban, hol szeretné művelet szüneteltetéséhez, hogy a változók és a környezet, amelyben a parancsprogram fut. az aktuális állapotának ellenőrzéséhez.</span><span class="sxs-lookup"><span data-stu-id="c4902-106">A breakpoint is a designated spot in a script where you would like operation to pause so that you can examine the current state of the variables and the environment in which your script is running.</span></span> <span data-ttu-id="c4902-107">Miután a parancsfájl által töréspont fel van függesztve, a parancsok a konzol ablaktáblában, a parancsfájl állapotának vizsgálata is futtathatja.</span><span class="sxs-lookup"><span data-stu-id="c4902-107">Once your script is paused by a breakpoint, you can run commands in the Console Pane to examine the state of your script.</span></span>  <span data-ttu-id="c4902-108">A kimeneti változók, vagy más parancsok futtatásához.</span><span class="sxs-lookup"><span data-stu-id="c4902-108">You can output variables or run other commands.</span></span> <span data-ttu-id="c4902-109">A jelenleg futó parancsfájl keretében számára látható változó értékét is módosíthatja.</span><span class="sxs-lookup"><span data-stu-id="c4902-109">You can even modify the value of any variables that are visible to the context of the currently running script.</span></span> <span data-ttu-id="c4902-110">Ellenőrzését szeretné látni, követően újból engedélyezheti a parancsfájl működésére.</span><span class="sxs-lookup"><span data-stu-id="c4902-110">After you have examined what you want to see, you can resume operation of the script.</span></span>

<span data-ttu-id="c4902-111">A Windows PowerShell hibakeresési környezetben töréspontok három típusú állíthatja be:</span><span class="sxs-lookup"><span data-stu-id="c4902-111">You can set three types of breakpoints in the Windows PowerShell debugging environment:</span></span>

1. <span data-ttu-id="c4902-112">**. Sor töréspont**.</span><span class="sxs-lookup"><span data-stu-id="c4902-112">**Line breakpoint**.</span></span> <span data-ttu-id="c4902-113">A parancsfájl szünetelteti, amikor a kijelölt sor elérése során a parancsfájl működésére</span><span class="sxs-lookup"><span data-stu-id="c4902-113">The script pauses when the designated line is reached during the operation of the script</span></span>

2. <span data-ttu-id="c4902-114">**Változó töréspont.**</span><span class="sxs-lookup"><span data-stu-id="c4902-114">**Variable breakpoint.**</span></span> <span data-ttu-id="c4902-115">A parancsfájl felfüggesztése, amikor megváltozik a kijelölt változó értékét.</span><span class="sxs-lookup"><span data-stu-id="c4902-115">The script pauses whenever the designated variable's value changes.</span></span>

3. <span data-ttu-id="c4902-116">**Parancs töréspont.**</span><span class="sxs-lookup"><span data-stu-id="c4902-116">**Command breakpoint.**</span></span> <span data-ttu-id="c4902-117">A parancsfájl felfüggesztése, amikor a kijelölt parancs arra készül, hogy a parancsfájl működésére során futtatni.</span><span class="sxs-lookup"><span data-stu-id="c4902-117">The script pauses whenever the designated command is about to be run during the operation of the script.</span></span> <span data-ttu-id="c4902-118">További szűréséhez a töréspont csak a kívánt művelet paraméterek része lehet.</span><span class="sxs-lookup"><span data-stu-id="c4902-118">It can include parameters to further filter the breakpoint to only the operation you want.</span></span> <span data-ttu-id="c4902-119">A parancsot is egy olyan létrehozott függvényt.</span><span class="sxs-lookup"><span data-stu-id="c4902-119">The command can also be a function you created.</span></span>

<span data-ttu-id="c4902-120">Ezek a Windows PowerShell ISE hibakeresési környezetben csak a sor töréspontokat állíthat be a vagy a billentyűparancsok használatával.</span><span class="sxs-lookup"><span data-stu-id="c4902-120">Of these, in the Windows PowerShell ISE debugging environment, only line breakpoints can be set by using the menu or the keyboard shortcuts.</span></span> <span data-ttu-id="c4902-121">A más kétféle töréspontokat állíthat, de be lettek állítva a konzol ablaktáblában használatával a [Set-PSBreakpoint](https://technet.microsoft.com/library/88d2d9ad-17dc-44ae-99aa-f841125b9dc8) parancsmag.</span><span class="sxs-lookup"><span data-stu-id="c4902-121">The other two types of breakpoints can be set, but they are set from the Console Pane by using the [Set-PSBreakpoint](https://technet.microsoft.com/library/88d2d9ad-17dc-44ae-99aa-f841125b9dc8) cmdlet.</span></span> <span data-ttu-id="c4902-122">Ez a szakasz ismerteti, hogyan lehet a Windows PowerShell ISE hibakeresési feladatok végrehajtása a menük használatával, ahol az rendelkezésre áll, és parancsok szélesebb körének végezni a konzol ablaktáblában parancsfájlok használatával.</span><span class="sxs-lookup"><span data-stu-id="c4902-122">This section describes how you can perform debugging tasks in Windows PowerShell ISE by using the menus where available, and perform a wider range of commands from the Console Pane by using scripting.</span></span>

### <a name="to-set-a-breakpoint"></a><span data-ttu-id="c4902-123">Töréspontokat állíthasson</span><span class="sxs-lookup"><span data-stu-id="c4902-123">To set a breakpoint</span></span>

<span data-ttu-id="c4902-124">Csak akkor mentését követően egy parancsfájlban állítható be töréspont.</span><span class="sxs-lookup"><span data-stu-id="c4902-124">A breakpoint can be set in a script only after it has been saved.</span></span> <span data-ttu-id="c4902-125">Kattintson a jobb gombbal az adott sor beállítására, és kattintson a kívánt sor **töréspont**.</span><span class="sxs-lookup"><span data-stu-id="c4902-125">Right-click the line where you want to set a line breakpoint, and then click **Toggle Breakpoint**.</span></span> <span data-ttu-id="c4902-126">Vagy kattintson a sor sor beállítására, ahová nyomja le az ENTER **F9** vagy a a **Debug** menüben kattintson a **töréspont**.</span><span class="sxs-lookup"><span data-stu-id="c4902-126">Or, click the line where you want to set a line breakpoint, and press **F9** or, on the **Debug** menu, click **Toggle Breakpoint**.</span></span>

<span data-ttu-id="c4902-127">A következő parancsfájl példája hogyan között állítható be változó töréspont konzolpanelen használatával a [Set-PSBreakpoint](https://technet.microsoft.com/library/6afd5d2c-a285-4796-8607-3cbf49471420) parancsmag.</span><span class="sxs-lookup"><span data-stu-id="c4902-127">The following script is an example of how you can set a variable breakpoint from the Console Pane by using the [Set-PSBreakpoint](https://technet.microsoft.com/library/6afd5d2c-a285-4796-8607-3cbf49471420) cmdlet.</span></span>

```powershell
# This command sets a breakpoint on the Server variable in the Sample.ps1 script.
Set-PSBreakpoint -Script sample.ps1 -Variable Server
```

### <a name="list-all-breakpoints"></a><span data-ttu-id="c4902-128">Töréspontokat felsorolása</span><span class="sxs-lookup"><span data-stu-id="c4902-128">List all breakpoints</span></span>

<span data-ttu-id="c4902-129">Töréspontokat megjeleníti az aktuális Windows PowerShell-munkamenetben.</span><span class="sxs-lookup"><span data-stu-id="c4902-129">Displays all breakpoints in the current Windows PowerShell session.</span></span>

<span data-ttu-id="c4902-130">Az a **Debug** menüben kattintson a **lista töréspontok**.</span><span class="sxs-lookup"><span data-stu-id="c4902-130">On the **Debug** menu, click **List Breakpoints**.</span></span> <span data-ttu-id="c4902-131">A következő parancsfájl példája hogyan listázhatja a konzol ablaktáblában töréspontokat használatával a [Get-PSBreakpoint](https://technet.microsoft.com/library/0bf48936-00ab-411c-b5e0-9b10a812a3c6) parancsmag.</span><span class="sxs-lookup"><span data-stu-id="c4902-131">The following script is an example of how you can list all breakpoints from the Console Pane by using the [Get-PSBreakpoint](https://technet.microsoft.com/library/0bf48936-00ab-411c-b5e0-9b10a812a3c6) cmdlet.</span></span>

```powershell
# This command lists all breakpoints in the current session.
Get-PSBreakpoint
```

### <a name="remove-a-breakpoint"></a><span data-ttu-id="c4902-132">Távolítsa el a töréspont</span><span class="sxs-lookup"><span data-stu-id="c4902-132">Remove a breakpoint</span></span>

<span data-ttu-id="c4902-133">Töréspont eltávolítása törli őket.</span><span class="sxs-lookup"><span data-stu-id="c4902-133">Removing a breakpoint deletes it.</span></span>

<span data-ttu-id="c4902-134">Ha úgy gondolja, hogy később újra felhasználhatja, érdemes lehet érdemes [tiltsa le a töréspont](#disable-a-breakpoint) , helyette.</span><span class="sxs-lookup"><span data-stu-id="c4902-134">If you think you might want to use it again later, consider [Disable a Breakpoint](#disable-a-breakpoint) it instead.</span></span>
<span data-ttu-id="c4902-135">Kattintson a jobb gombbal a sort, ahol töréspont, és kattintson a kívánt **töréspont**.</span><span class="sxs-lookup"><span data-stu-id="c4902-135">Right-click the line where you want to remove a breakpoint, and then click **Toggle Breakpoint**.</span></span>
<span data-ttu-id="c4902-136">Vagy kattintson a sor, ha szeretné eltávolítani a töréspont, és a a **Debug** menüben kattintson a **töréspont**.</span><span class="sxs-lookup"><span data-stu-id="c4902-136">Or, click the line where you want to remove a breakpoint, and on the **Debug** menu, click **Toggle Breakpoint**.</span></span>
<span data-ttu-id="c4902-137">Az alábbi parancsfájl a megadott Azonosítójú töréspont eltávolítása a konzol ablaktáblában használatával példája a [Remove-PSBreakpoint](https://technet.microsoft.com/library/4c877a80-0ea0-4790-9281-88c08ef0ddd6) parancsmag.</span><span class="sxs-lookup"><span data-stu-id="c4902-137">The following script is an example of how to remove a breakpoint with a specified ID from the Console Pane by using the [Remove-PSBreakpoint](https://technet.microsoft.com/library/4c877a80-0ea0-4790-9281-88c08ef0ddd6) cmdlet.</span></span>

```powershell
# This command deletes the breakpoint with breakpoint ID 2.
Remove-PSBreakpoint -Id 2
```

### <a name="remove-all-breakpoints"></a><span data-ttu-id="c4902-138">Törölje a töréspontokat</span><span class="sxs-lookup"><span data-stu-id="c4902-138">Remove All Breakpoints</span></span>

<span data-ttu-id="c4902-139">Eltávolítja az aktuális munkamenetben definiált töréspontokat a **Debug** menüben kattintson **eltávolítása töréspontokat**.</span><span class="sxs-lookup"><span data-stu-id="c4902-139">To remove all breakpoints defined in the current session, on the **Debug** menu, click **Remove All Breakpoints**.</span></span>

<span data-ttu-id="c4902-140">A következő parancsfájl töréspontokat eltávolítása a konzol ablaktáblában használatával példája a [Remove-PSBreakpoint](https://technet.microsoft.com/library/4c877a80-0ea0-4790-9281-88c08ef0ddd6) parancsmag.</span><span class="sxs-lookup"><span data-stu-id="c4902-140">The following script is an example of how to remove all breakpoints from the Console Pane by using the [Remove-PSBreakpoint](https://technet.microsoft.com/library/4c877a80-0ea0-4790-9281-88c08ef0ddd6) cmdlet.</span></span>

```powershell
# This command deletes all of the breakpoints in the current session.
Get-PSBreakpoint | Remove-PSBreakpoint
```

### <a name="disable-a-breakpoint"></a><span data-ttu-id="c4902-141">Tiltsa le a töréspont</span><span class="sxs-lookup"><span data-stu-id="c4902-141">Disable a Breakpoint</span></span>

<span data-ttu-id="c4902-142">Töréspont letiltásával nem távolítja el azt. az kikapcsolja, amíg az nincs engedélyezve.</span><span class="sxs-lookup"><span data-stu-id="c4902-142">Disabling a breakpoint does not remove it; it turns it off until it is enabled.</span></span>  <span data-ttu-id="c4902-143">Egy adott sor töréspont letiltásához kattintson a jobb gombbal a sort, ahol tiltsa le a töréspont, és kattintson a kívánt **tiltsa le a töréspont**.</span><span class="sxs-lookup"><span data-stu-id="c4902-143">To disable a specific line breakpoint, right-click the line where you want to disable a breakpoint, and then click **Disable Breakpoint**.</span></span> <span data-ttu-id="c4902-144">Vagy kattintson a sor, ha le szeretné tiltani a töréspont nyomja le az ENTER **F9** vagy a a **Debug** menüben kattintson **tiltsa le a töréspont**.</span><span class="sxs-lookup"><span data-stu-id="c4902-144">Or, click the line where you want to disable a breakpoint, and press **F9** or, on the **Debug** menu, click **Disable Breakpoint**.</span></span> <span data-ttu-id="c4902-145">A következő parancsfájl példája hogyan eltávolíthatja a megadott Azonosítójú töréspont konzolpanelen használatával a [Disable-PSBreakpoint](https://technet.microsoft.com/library/d4974e9b-0aaa-4e20-b87f-f599a413e4e8) parancsmag.</span><span class="sxs-lookup"><span data-stu-id="c4902-145">The following script is an example of how you can remove a breakpoint with a specified ID from the Console Pane by using the [Disable-PSBreakpoint](https://technet.microsoft.com/library/d4974e9b-0aaa-4e20-b87f-f599a413e4e8) cmdlet.</span></span>

```powershell
# This command disables the breakpoint with breakpoint ID 0.
Disable-PSBreakpoint -Id 0
```

### <a name="disable-all-breakpoints"></a><span data-ttu-id="c4902-146">Töréspontokat letiltása</span><span class="sxs-lookup"><span data-stu-id="c4902-146">Disable All Breakpoints</span></span>

<span data-ttu-id="c4902-147">Töréspont letiltásával nem távolítja el azt. az kikapcsolja, amíg az nincs engedélyezve.</span><span class="sxs-lookup"><span data-stu-id="c4902-147">Disabling a breakpoint does not remove it; it turns it off until it is enabled.</span></span>  <span data-ttu-id="c4902-148">Le kívánja tiltani töréspontokat a jelenlegi munkamenet a **Debug** menüben kattintson a **tiltsa le a töréspontokat**.</span><span class="sxs-lookup"><span data-stu-id="c4902-148">To disable all breakpoints in the current session, on the **Debug** menu, click **Disable all Breakpoints**.</span></span> <span data-ttu-id="c4902-149">A következő parancsfájl példája letiltásáról töréspontokat a konzol ablaktáblában használatával a [Disable-PSBreakpoint](https://technet.microsoft.com/library/d4974e9b-0aaa-4e20-b87f-f599a413e4e8) parancsmag.</span><span class="sxs-lookup"><span data-stu-id="c4902-149">The following script is an example of how you can disable all breakpoints from the Console Pane by using the [Disable-PSBreakpoint](https://technet.microsoft.com/library/d4974e9b-0aaa-4e20-b87f-f599a413e4e8) cmdlet.</span></span>

```powershell
# This command disables all breakpoints in the current session.
# You can abbreviate this command as: "gbp | dbp".
Get-PSBreakpoint | Disable-PSBreakpoint
```

### <a name="enable-a-breakpoint"></a><span data-ttu-id="c4902-150">Töréspont engedélyezése</span><span class="sxs-lookup"><span data-stu-id="c4902-150">Enable a Breakpoint</span></span>

<span data-ttu-id="c4902-151">Ahhoz, hogy az adott töréspont, kattintson a jobb gombbal a sort, ahol Töréspont engedélyezése, és kattintson a kívánt **engedélyezése töréspont**.</span><span class="sxs-lookup"><span data-stu-id="c4902-151">To enable a specific breakpoint, right-click the line where you want to enable a breakpoint, and then click **Enable Breakpoint**.</span></span> <span data-ttu-id="c4902-152">Vagy kattintson a sorra, ahová Töréspont engedélyezése, és nyomja le az **F9** vagy a a **Debug** menüben kattintson a **engedélyezése töréspont**.</span><span class="sxs-lookup"><span data-stu-id="c4902-152">Or, click the line where you want to enable a breakpoint, and then press **F9** or, on the **Debug** menu, click **Enable Breakpoint**.</span></span> <span data-ttu-id="c4902-153">A következő parancsfájl egy példát, hogyan engedélyezheti a konzol ablaktáblában adott töréspontok használatával a [Enable-PSBreakpoint](https://technet.microsoft.com/library/739e1091-3b3f-405f-a428-bec7543e5df0) parancsmag.</span><span class="sxs-lookup"><span data-stu-id="c4902-153">The following script is an example of how you can enable specific breakpoints from the Console Pane by using the [Enable-PSBreakpoint](https://technet.microsoft.com/library/739e1091-3b3f-405f-a428-bec7543e5df0) cmdlet.</span></span>

```powershell
# This command enables breakpoints with breakpoint IDs 0, 1, and 5.
Enable-PSBreakpoint -Id 0, 1, 5
```

### <a name="enable-all-breakpoints"></a><span data-ttu-id="c4902-154">Töréspontokat engedélyezése</span><span class="sxs-lookup"><span data-stu-id="c4902-154">Enable All Breakpoints</span></span>

<span data-ttu-id="c4902-155">Ahhoz, hogy az aktuális munkamenetben definiált töréspontokat a **Debug** menüben kattintson a **töréspontokat engedélyezése**.</span><span class="sxs-lookup"><span data-stu-id="c4902-155">To enable all breakpoints defined in the current session, on the **Debug** menu, click **Enable all Breakpoints**.</span></span> <span data-ttu-id="c4902-156">A következő parancsfájl egy példát, hogyan engedélyezheti a konzol ablaktáblában töréspontokat használatával a [Enable-PSBreakpoint](https://technet.microsoft.com/library/739e1091-3b3f-405f-a428-bec7543e5df0) parancsmag.</span><span class="sxs-lookup"><span data-stu-id="c4902-156">The following script is an example of how you can enable all breakpoints from the Console Pane by using the [Enable-PSBreakpoint](https://technet.microsoft.com/library/739e1091-3b3f-405f-a428-bec7543e5df0) cmdlet.</span></span>

```powershell
# This command enables all breakpoints in the current session.
# You can abbreviate the command by using their aliases: "gbp | ebp".
Get-PSBreakpoint | Enable-PSBreakpoint
```

## <a name="how-to-manage-a-debugging-session"></a><span data-ttu-id="c4902-157">A hibakeresési munkamenetben kezelése</span><span class="sxs-lookup"><span data-stu-id="c4902-157">How to manage a debugging session</span></span>

<span data-ttu-id="c4902-158">Mielőtt elkezdené a hibakeresést, meg kell adni egy vagy több töréspontok.</span><span class="sxs-lookup"><span data-stu-id="c4902-158">Before you start debugging, you must set one or more breakpoints.</span></span> <span data-ttu-id="c4902-159">Nem állítható be töréspont, kivéve, ha a parancsfájl debug kívánt menti.</span><span class="sxs-lookup"><span data-stu-id="c4902-159">You cannot set a breakpoint unless the script that you want to debug is saved.</span></span> <span data-ttu-id="c4902-160">Bemutatja, hogyan állítható be töréspont az utasításokat, lásd: [töréspontok kezelése](#how-to-manage-breakpoints) vagy [Set-PSBreakpoint](https://docs.microsoft.com/powershell/module/microsoft.powershell.utility/set-psbreakpoint).</span><span class="sxs-lookup"><span data-stu-id="c4902-160">For directions on of how to set a breakpoint, see [How to manage breakpoints](#how-to-manage-breakpoints) or [Set-PSBreakpoint](https://docs.microsoft.com/powershell/module/microsoft.powershell.utility/set-psbreakpoint).</span></span> <span data-ttu-id="c4902-161">Hibakeresés indítása után nem szerkeszthetők egy parancsfájl, amíg le nem állítják hibakeresés.</span><span class="sxs-lookup"><span data-stu-id="c4902-161">After you start debugging, you cannot edit a script until you stop debugging.</span></span> <span data-ttu-id="c4902-162">Egy parancsfájl, amely rendelkezik egy vagy több töréspontok beállítása előtt fut, automatikusan menti.</span><span class="sxs-lookup"><span data-stu-id="c4902-162">A script that has one or more breakpoints set is automatically saved before it is run.</span></span>

### <a name="to-start-debugging"></a><span data-ttu-id="c4902-163">A hibakeresés</span><span class="sxs-lookup"><span data-stu-id="c4902-163">To start debugging</span></span>

<span data-ttu-id="c4902-164">Nyomja le az **F5** vagy az eszköztáron kattintson a **-parancsfájl futtatása** ikonra, vagy a a **Debug** menüben kattintson **Futtatás/Folytatás**.</span><span class="sxs-lookup"><span data-stu-id="c4902-164">Press **F5** or, on the toolbar, click the **Run Script** icon, or on the **Debug** menu click **Run/Continue**.</span></span> <span data-ttu-id="c4902-165">A parancsprogram lefut, amíg az első töréspont ütközik.</span><span class="sxs-lookup"><span data-stu-id="c4902-165">The script runs until it encounters the first breakpoint.</span></span> <span data-ttu-id="c4902-166">Megszakítja a műveletet, és kiemeli a sor, amikor szünetel.</span><span class="sxs-lookup"><span data-stu-id="c4902-166">It pauses operation there and highlights the line on which it paused.</span></span>

### <a name="to-continue-debugging"></a><span data-ttu-id="c4902-167">A folytatáshoz a hibakeresés</span><span class="sxs-lookup"><span data-stu-id="c4902-167">To continue debugging</span></span>

<span data-ttu-id="c4902-168">Nyomja le az **F5** vagy az eszköztáron kattintson a **-parancsfájl futtatása** ikonra, vagy a a **Debug** menüben kattintson a **Futtatás/Folytatás** vagy, írja be a konzol ablaktáblájában **C** , és nyomja le az **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="c4902-168">Press **F5** or, on the toolbar, click the **Run Script** icon, or on the **Debug** menu, click **Run/Continue** or, in the Console Pane, type **C** and then press **ENTER**.</span></span> <span data-ttu-id="c4902-169">Ez azt eredményezi, hogy a parancsfájl a következő töréspont vagy a parancsfájl végén futtatását, ha nincsenek további töréspontok hibát.</span><span class="sxs-lookup"><span data-stu-id="c4902-169">This causes the script to continue running to the next breakpoint or to the end of the script if no further breakpoints are encountered.</span></span>

### <a name="to-view-the-call-stack"></a><span data-ttu-id="c4902-170">A hívási verem megtekintése</span><span class="sxs-lookup"><span data-stu-id="c4902-170">To view the call stack</span></span>

<span data-ttu-id="c4902-171">A hívási verem megjeleníti az aktuális hely a parancsfájl futtatása.</span><span class="sxs-lookup"><span data-stu-id="c4902-171">The call stack displays the current run location in the script.</span></span> <span data-ttu-id="c4902-172">Ha a parancsfájl egy másik függvény által hívott függvény fut, majd, amely képviseli jelennek meg a kimenet további sorokat.</span><span class="sxs-lookup"><span data-stu-id="c4902-172">If the script is running in a function that was called by a different function, then that is represented in the display by additional rows in the output.</span></span> <span data-ttu-id="c4902-173">A legalsó sor jeleníti meg az eredeti parancsfájlt és a sor, amelyben a következő függvényt hívták.</span><span class="sxs-lookup"><span data-stu-id="c4902-173">The bottom-most row displays the original script and the line in it in which a function was called.</span></span> <span data-ttu-id="c4902-174">A Tovább gombra. a függvény és a sort, amelyben egy másik művelet lehet, hogy rendelkezik hívása történt a sor megmutatja.</span><span class="sxs-lookup"><span data-stu-id="c4902-174">The next line up shows that function and the line in it in which another function might have been called.</span></span>  <span data-ttu-id="c4902-175">A legfelső sor tartalmazza az aktuális környezetben, amelyen a töréspont van állítva az aktuális sor.</span><span class="sxs-lookup"><span data-stu-id="c4902-175">The top-most row shows the current context of the current line on which the breakpoint is set.</span></span>

<span data-ttu-id="c4902-176">Szünetel, amíg a jelenlegi hívásverem megtekintéséhez nyomja le az ENTER **CTRL + SHIFT + D** vagy a a **Debug** menüben kattintson a **megjelenítési hívási veremnek megfelelő** vagy, írja be a konzol ablaktáblájában **K**  , és nyomja le az **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="c4902-176">While paused, to see the current call stack, press **CTRL+SHIFT+D** or, on the **Debug** menu, click **Display Call Stack** or, in the Console Pane, type **K** and then press **ENTER**.</span></span>

### <a name="to-stop-debugging"></a><span data-ttu-id="c4902-177">A hibakereső leállítása</span><span class="sxs-lookup"><span data-stu-id="c4902-177">To stop debugging</span></span>

<span data-ttu-id="c4902-178">Nyomja le az ENTER **SHIFT-F5** vagy a a **Debug** menüben kattintson a **hibakereső leállítása**, vagy írja be a konzol ablaktáblájában **Q** , és nyomja le az  **Adja meg**.</span><span class="sxs-lookup"><span data-stu-id="c4902-178">Press **SHIFT-F5** or, on the **Debug** menu, click **Stop Debugger**, or, in the Console Pane, type **Q** and then press **ENTER**.</span></span>

## <a name="how-to-step-over-step-into-and-step-out-while-debugging"></a><span data-ttu-id="c4902-179">Ugorja át, lépjen be és hibakeresés során lépés</span><span class="sxs-lookup"><span data-stu-id="c4902-179">How to step over, step into, and step out while debugging</span></span>

<span data-ttu-id="c4902-180">Lépjen az a folyamat egy utasítás fut egyszerre.</span><span class="sxs-lookup"><span data-stu-id="c4902-180">Stepping is the process of running one statement at a time.</span></span> <span data-ttu-id="c4902-181">Állítsa le a kód sor, és vizsgálja meg a változók és a rendszer állapotát.</span><span class="sxs-lookup"><span data-stu-id="c4902-181">You can stop on a line of code, and examine the values of variables and the state of the system.</span></span> <span data-ttu-id="c4902-182">A következő táblázat ismerteti a gyakori hibakeresési feladatokat, mint a léptetési keresztül, lépjen be, és lépjen.</span><span class="sxs-lookup"><span data-stu-id="c4902-182">The following table describes common debugging tasks such as stepping over, stepping into, and stepping out.</span></span>

| <span data-ttu-id="c4902-183">Hibakeresési feladat</span><span class="sxs-lookup"><span data-stu-id="c4902-183">Debugging Task</span></span> | <span data-ttu-id="c4902-184">Leírás</span><span class="sxs-lookup"><span data-stu-id="c4902-184">Description</span></span> | <span data-ttu-id="c4902-185">A PowerShell ISE elvégzésére</span><span class="sxs-lookup"><span data-stu-id="c4902-185">How to accomplish it in PowerShell ISE</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c4902-186">**Lépjen be**</span><span class="sxs-lookup"><span data-stu-id="c4902-186">**Step Into**</span></span> | <span data-ttu-id="c4902-187">Az aktuális utasítás végrehajtása, és majd leállítja a következő utasításnál.</span><span class="sxs-lookup"><span data-stu-id="c4902-187">Executes the current statement and then stops at the next statement.</span></span> <span data-ttu-id="c4902-188">Ha az aktuális utasítás függvény vagy parancsfájl hívás, majd az adott függvény vagy parancsfájl hibakereső a lépéseket, ellenkező esetben leállítja a következő utasításnál.</span><span class="sxs-lookup"><span data-stu-id="c4902-188">If the current statement is a function or script call, then the debugger steps into that function or script, otherwise it stops at the next statement.</span></span> | <span data-ttu-id="c4902-189">Nyomja le az ENTER **F11** vagy a a **Debug** menüben kattintson a **lépésenként**, vagy írja be a konzol ablaktáblájában **S** nyomja le az ENTER **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="c4902-189">Press **F11** or, on the **Debug** menu, click **Step Into**, or in the Console Pane, type **S** and press **ENTER**.</span></span> |
| <span data-ttu-id="c4902-190">**Átlépés**</span><span class="sxs-lookup"><span data-stu-id="c4902-190">**Step Over**</span></span> | <span data-ttu-id="c4902-191">Az aktuális utasítás végrehajtása, és majd leállítja a következő utasításnál.</span><span class="sxs-lookup"><span data-stu-id="c4902-191">Executes the current statement and then stops at the next statement.</span></span> <span data-ttu-id="c4902-192">Ha az aktuális utasítás függvény vagy parancsfájl hívást, majd a hibakereső a teljes függvény vagy parancsfájl hajt végre, és leállítja a függvény hívása után a következő utasításnál.</span><span class="sxs-lookup"><span data-stu-id="c4902-192">If the current statement is a function or script call, then the debugger executes the whole function or script, and it stops at the next statement after the function call.</span></span> | <span data-ttu-id="c4902-193">Nyomja le az ENTER **F10** vagy a a **Debug** menüben kattintson a **Átlépés**, vagy írja be a konzol ablaktáblájában **V** nyomja le az ENTER **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="c4902-193">Press **F10** or, on the **Debug** menu, click **Step Over**, or in the Console Pane, type **V** and press **ENTER**.</span></span> |
| <span data-ttu-id="c4902-194">**Kilépés**</span><span class="sxs-lookup"><span data-stu-id="c4902-194">**Step Out**</span></span> | <span data-ttu-id="c4902-195">A current függvény kívül, és egy szinttel, ha a függvény van beágyazva lépéseket.</span><span class="sxs-lookup"><span data-stu-id="c4902-195">Steps out of the current function and up one level if the function is nested.</span></span> <span data-ttu-id="c4902-196">Ha törzsébe, a parancsfájl végrehajtása végén, vagy a következő töréspont.</span><span class="sxs-lookup"><span data-stu-id="c4902-196">If in the main body, the script is executed to the end, or to the next breakpoint.</span></span> <span data-ttu-id="c4902-197">A rendszer kihagyta utasítás végrehajtása, de nem lépcsőzetes keresztül.</span><span class="sxs-lookup"><span data-stu-id="c4902-197">The skipped statements are executed, but not stepped through.</span></span> | <span data-ttu-id="c4902-198">Nyomja le az ENTER **SHIFT + F11**, vagy a a **Debug** menüben kattintson a **lépés kimenő**, vagy írja be a konzol ablaktáblájában **O** nyomja le az ENTER **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="c4902-198">Press **SHIFT+F11**, or on the **Debug** menu, click **Step Out**, or in the Console Pane, type **O** and press **ENTER**.</span></span> |
| <span data-ttu-id="c4902-199">**Továbbra is**</span><span class="sxs-lookup"><span data-stu-id="c4902-199">**Continue**</span></span> | <span data-ttu-id="c4902-200">Végén, vagy a következő töréspont végrehajtása folytatódik.</span><span class="sxs-lookup"><span data-stu-id="c4902-200">Continues execution to the end, or to the next breakpoint.</span></span> <span data-ttu-id="c4902-201">A kihagyott funkciók és indítások hajtotta végre, de nem lépcsőzetes keresztül.</span><span class="sxs-lookup"><span data-stu-id="c4902-201">The skipped functions and invocations are executed, but not stepped through.</span></span> | <span data-ttu-id="c4902-202">Nyomja le az ENTER **F5** vagy a a **Debug** menüben kattintson a **Futtatás/Folytatás**, vagy írja be a konzol ablaktáblájában **C** nyomja le az ENTER **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="c4902-202">Press **F5** or, on the **Debug** menu, click **Run/Continue**, or in the Console Pane, type **C** and press **ENTER**.</span></span> |

## <a name="how-to-display-the-values-of-variables-while-debugging"></a><span data-ttu-id="c4902-203">Hibakeresés során változók értékeinek megjelenítése</span><span class="sxs-lookup"><span data-stu-id="c4902-203">How to display the values of variables while debugging</span></span>

<span data-ttu-id="c4902-204">A változók aktuális értékeit megjelenítheti a parancsfájl lépéseit a kódot.</span><span class="sxs-lookup"><span data-stu-id="c4902-204">You can display the current values of variables in the script as you step through the code.</span></span>

### <a name="to-display-the-values-of-standard-variables"></a><span data-ttu-id="c4902-205">Standard változók értékeinek megjelenítéséhez</span><span class="sxs-lookup"><span data-stu-id="c4902-205">To display the values of standard variables</span></span>

<span data-ttu-id="c4902-206">Az alábbi módszerek valamelyikével:</span><span class="sxs-lookup"><span data-stu-id="c4902-206">Use one of the following methods:</span></span>

- <span data-ttu-id="c4902-207">A parancsfájl ablaktáblán mutasson a változó értéke eszközleírásként megjelenítéséhez.</span><span class="sxs-lookup"><span data-stu-id="c4902-207">In the Script Pane, hover over the variable to display its value as a tool tip.</span></span>

- <span data-ttu-id="c4902-208">A konzol ablaktáblában írja be a változó nevét, és nyomja le az **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="c4902-208">In the Console Pane, type the variable name and press **ENTER**.</span></span>

<span data-ttu-id="c4902-209">Minden ablaktáblái ISE mindig ugyanabban a hatókörben van.</span><span class="sxs-lookup"><span data-stu-id="c4902-209">All panes in ISE are always in the same scope.</span></span> <span data-ttu-id="c4902-210">Ezért egy parancsfájl hibakeresést, amíg a konzolpanelen beírt parancsot futtathatja parancsfájl hatókörében.</span><span class="sxs-lookup"><span data-stu-id="c4902-210">Therefore, while you are debugging a script, the commands that you type in the Console Pane run in script scope.</span></span> <span data-ttu-id="c4902-211">Ez lehetővé teszi, hogy a konzol ablaktáblában található változók értékeit, és csak a parancsfájl definiált függvényeket.</span><span class="sxs-lookup"><span data-stu-id="c4902-211">This allows you to use the Console Pane to find the values of variables and call functions that are defined only in the script.</span></span>

### <a name="to-display-the-values-of-automatic-variables"></a><span data-ttu-id="c4902-212">Az automatikus változók értékek megjelenítése</span><span class="sxs-lookup"><span data-stu-id="c4902-212">To display the values of automatic variables</span></span>

<span data-ttu-id="c4902-213">A fenti módszer segítségével szinte minden változók levő értéket jeleníti meg, amíg parancsfájl hibakeresés alatt.</span><span class="sxs-lookup"><span data-stu-id="c4902-213">You can use the preceding method to display the value of almost all variables while you are debugging a script.</span></span> <span data-ttu-id="c4902-214">Ezek a módszerek azonban nem működnek a következő automatikus változók.</span><span class="sxs-lookup"><span data-stu-id="c4902-214">However, these methods do not work for the following automatic variables.</span></span>

- <span data-ttu-id="c4902-215">$_</span><span class="sxs-lookup"><span data-stu-id="c4902-215">$_</span></span>

- <span data-ttu-id="c4902-216">$Input</span><span class="sxs-lookup"><span data-stu-id="c4902-216">$Input</span></span>

- <span data-ttu-id="c4902-217">$MyInvocation</span><span class="sxs-lookup"><span data-stu-id="c4902-217">$MyInvocation</span></span>

- <span data-ttu-id="c4902-218">$PSBoundParameters</span><span class="sxs-lookup"><span data-stu-id="c4902-218">$PSBoundParameters</span></span>

- <span data-ttu-id="c4902-219">$Args</span><span class="sxs-lookup"><span data-stu-id="c4902-219">$Args</span></span>

<span data-ttu-id="c4902-220">Kísérli meg ezek a változók bármelyikének levő értéket jeleníti meg, ha a változó értékét elérhetővé az egy belső folyamat a hibakeresőben, nem értékét használja a változót a parancsfájl.</span><span class="sxs-lookup"><span data-stu-id="c4902-220">If you try to display the value of any of these variables, you get the value of that variable for in an internal pipeline the debugger uses, not the value of the variable in the script.</span></span> <span data-ttu-id="c4902-221">Megkerüléséhez Ez néhány változók ($_ $Input, $MyInvocation, $PSBoundParameters és $Args) a következő módszerrel:</span><span class="sxs-lookup"><span data-stu-id="c4902-221">You can work around this for a few variables ($_, $Input, $MyInvocation, $PSBoundParameters, and $Args) by using the following method:</span></span>

1. <span data-ttu-id="c4902-222">A parancsfájl az automatikus változó értékének hozzárendelése egy új változót.</span><span class="sxs-lookup"><span data-stu-id="c4902-222">In the script, assign the value of the automatic variable to a new variable.</span></span>

2. <span data-ttu-id="c4902-223">Megjeleníti az új változó értékét, vagy a parancssori panelbe az új változó fölé, vagy írja be az új változó a konzol ablaktáblában.</span><span class="sxs-lookup"><span data-stu-id="c4902-223">Display the value of the new variable, either by hovering over the new variable in the Script Pane, or by typing the new variable in the Console Pane.</span></span>

<span data-ttu-id="c4902-224">Például $MyInvocation változó értékének megjelennek a parancsfájlt, az érték hozzárendelése egy új változót, például a $scriptname, és majd vigye vagy vagy típusú értéket $scriptname változó.</span><span class="sxs-lookup"><span data-stu-id="c4902-224">For example, to display the value of the $MyInvocation variable, in the script, assign the value to a new variable, such as $scriptname, and then hover over or type the $scriptname variable to display its value.</span></span>

```powershell
# In C:\ps-test\MyScript.ps1
$scriptname = $MyInvocation.MyCommand.Path
```

```output
# In the Console Pane:
PS> .\MyScript.ps1
PS> $scriptname
C:\ps-test\MyScript.ps1
```

## <a name="see-also"></a><span data-ttu-id="c4902-225">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="c4902-225">See Also</span></span>

- [<span data-ttu-id="c4902-226">A Windows PowerShell ISE felfedezése</span><span class="sxs-lookup"><span data-stu-id="c4902-226">Exploring the Windows PowerShell ISE</span></span>](../../getting-started/fundamental/exploring-the-windows-powershell-ise.md)