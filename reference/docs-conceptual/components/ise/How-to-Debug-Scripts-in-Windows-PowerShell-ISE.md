---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: Parancsfájlokban való hibakeresés a PowerShell ISE-ben
ms.openlocfilehash: b7af2de83a3f796a2057514e36ad8b74367e8ce2
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55684576"
---
# <a name="how-to-debug-scripts-in-windows-powershell-ise"></a><span data-ttu-id="fe83a-103">Parancsfájlokban való hibakeresés a PowerShell ISE-ben</span><span class="sxs-lookup"><span data-stu-id="fe83a-103">How to Debug Scripts in Windows PowerShell ISE</span></span>

<span data-ttu-id="fe83a-104">Ez a cikk bemutatja, hogyan parancsfájlokban való hibakeresés a helyi számítógépen a Windows PowerShell integrált parancsfájl-kezelési környezet (ISE) vizuális hibakeresési funkciók használatával.</span><span class="sxs-lookup"><span data-stu-id="fe83a-104">This article describes how to debug scripts on a local computer by using the Windows PowerShell Integrated Scripting Environment (ISE) visual debugging features.</span></span>

## <a name="how-to-manage-breakpoints"></a><span data-ttu-id="fe83a-105">Töréspontok kezelése</span><span class="sxs-lookup"><span data-stu-id="fe83a-105">How to manage breakpoints</span></span>

<span data-ttu-id="fe83a-106">Egy töréspontot a kijelölt helyszínen egy parancsfájlban, hova szeretné felfüggeszteni, így megvizsgálhatja a változókat és a környezet, amelyben a parancsprogram fut. az aktuális állapotát a művelet.</span><span class="sxs-lookup"><span data-stu-id="fe83a-106">A breakpoint is a designated spot in a script where you would like operation to pause so that you can examine the current state of the variables and the environment in which your script is running.</span></span> <span data-ttu-id="fe83a-107">Miután a parancsfájl által egy töréspontot szüneteltetve van, futtathat parancsokat vizsgálata a szkript állapotát a konzol ablaktáblában.</span><span class="sxs-lookup"><span data-stu-id="fe83a-107">Once your script is paused by a breakpoint, you can run commands in the Console Pane to examine the state of your script.</span></span>  <span data-ttu-id="fe83a-108">Kimeneti változókat, vagy más parancsok futtatásához.</span><span class="sxs-lookup"><span data-stu-id="fe83a-108">You can output variables or run other commands.</span></span> <span data-ttu-id="fe83a-109">Az aktuálisan futó szkript kontextusában számára látható minden változó értékét akkor is módosíthatja.</span><span class="sxs-lookup"><span data-stu-id="fe83a-109">You can even modify the value of any variables that are visible to the context of the currently running script.</span></span> <span data-ttu-id="fe83a-110">Milyen meg szeretné tekinteni ellenőrzését követően folytathatja a parancsfájl működésére.</span><span class="sxs-lookup"><span data-stu-id="fe83a-110">After you have examined what you want to see, you can resume operation of the script.</span></span>

<span data-ttu-id="fe83a-111">A Windows PowerShell hibakeresési környezetben töréspontok három típusú állíthatja be:</span><span class="sxs-lookup"><span data-stu-id="fe83a-111">You can set three types of breakpoints in the Windows PowerShell debugging environment:</span></span>

1. <span data-ttu-id="fe83a-112">**Töréspont sor**.</span><span class="sxs-lookup"><span data-stu-id="fe83a-112">**Line breakpoint**.</span></span> <span data-ttu-id="fe83a-113">A parancsfájl felfüggeszti a szkript a művelet során a kijelölt sor elérésekor</span><span class="sxs-lookup"><span data-stu-id="fe83a-113">The script pauses when the designated line is reached during the operation of the script</span></span>

2. <span data-ttu-id="fe83a-114">**Változó töréspontot.**</span><span class="sxs-lookup"><span data-stu-id="fe83a-114">**Variable breakpoint.**</span></span> <span data-ttu-id="fe83a-115">A parancsfájl minden alkalommal, amikor megváltozik a kijelölt változó értéke felfüggesztése.</span><span class="sxs-lookup"><span data-stu-id="fe83a-115">The script pauses whenever the designated variable's value changes.</span></span>

3. <span data-ttu-id="fe83a-116">**Parancs töréspontot.**</span><span class="sxs-lookup"><span data-stu-id="fe83a-116">**Command breakpoint.**</span></span> <span data-ttu-id="fe83a-117">A parancsfájl minden alkalommal, amikor a kijelölt parancsot arra készül, hogy a parancsfájl működésére során futtatandó felfüggesztése.</span><span class="sxs-lookup"><span data-stu-id="fe83a-117">The script pauses whenever the designated command is about to be run during the operation of the script.</span></span> <span data-ttu-id="fe83a-118">További szűréséhez, csak a kívánt műveletet a töréspont paramétereket is alkalmas.</span><span class="sxs-lookup"><span data-stu-id="fe83a-118">It can include parameters to further filter the breakpoint to only the operation you want.</span></span> <span data-ttu-id="fe83a-119">A parancsot is létrehozott egy függvényt.</span><span class="sxs-lookup"><span data-stu-id="fe83a-119">The command can also be a function you created.</span></span>

<span data-ttu-id="fe83a-120">Ezeket a Windows PowerShell ISE-hibakeresési környezetben csak a sor töréspontok állítható a menüből vagy a billentyűparancsok segítségével.</span><span class="sxs-lookup"><span data-stu-id="fe83a-120">Of these, in the Windows PowerShell ISE debugging environment, only line breakpoints can be set by using the menu or the keyboard shortcuts.</span></span> <span data-ttu-id="fe83a-121">Akkor állítható be töréspontokat a másik két típusú, de azok-beállításokat a konzol panelen a [Set-PSBreakpoint](https://technet.microsoft.com/library/88d2d9ad-17dc-44ae-99aa-f841125b9dc8) parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="fe83a-121">The other two types of breakpoints can be set, but they are set from the Console Pane by using the [Set-PSBreakpoint](https://technet.microsoft.com/library/88d2d9ad-17dc-44ae-99aa-f841125b9dc8) cmdlet.</span></span> <span data-ttu-id="fe83a-122">Ez a szakasz ismerteti, hogyan hajtsa végre a hibakeresési feladatokat Windows PowerShell ISE-ben menüket használja, ha elérhetők, és hajtsa végre a parancsokat szélesebb körének teszik a konzol panelen parancsfájlok használatával.</span><span class="sxs-lookup"><span data-stu-id="fe83a-122">This section describes how you can perform debugging tasks in Windows PowerShell ISE by using the menus where available, and perform a wider range of commands from the Console Pane by using scripting.</span></span>

### <a name="to-set-a-breakpoint"></a><span data-ttu-id="fe83a-123">Állítson be egy töréspontot a</span><span class="sxs-lookup"><span data-stu-id="fe83a-123">To set a breakpoint</span></span>

<span data-ttu-id="fe83a-124">Töréspont beállítható egy parancsfájlban csak azt követően lett mentve.</span><span class="sxs-lookup"><span data-stu-id="fe83a-124">A breakpoint can be set in a script only after it has been saved.</span></span> <span data-ttu-id="fe83a-125">Kattintson a jobb gombbal a sor, ahol állítson be egy sor töréspontot, és kattintson a kívánt **töréspont**.</span><span class="sxs-lookup"><span data-stu-id="fe83a-125">Right-click the line where you want to set a line breakpoint, and then click **Toggle Breakpoint**.</span></span> <span data-ttu-id="fe83a-126">Vagy kattintson a sorra, ahol szeretné állítani egy sor töréspontot, nyomja le az ENTER **F9** vagy a a **Debug** menüben kattintson a **töréspont**.</span><span class="sxs-lookup"><span data-stu-id="fe83a-126">Or, click the line where you want to set a line breakpoint, and press **F9** or, on the **Debug** menu, click **Toggle Breakpoint**.</span></span>

<span data-ttu-id="fe83a-127">A következő parancsfájl egy példát, hogyan között állítható be változó Töréspont a konzol panel használatával a [Set-PSBreakpoint](https://technet.microsoft.com/library/6afd5d2c-a285-4796-8607-3cbf49471420) parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="fe83a-127">The following script is an example of how you can set a variable breakpoint from the Console Pane by using the [Set-PSBreakpoint](https://technet.microsoft.com/library/6afd5d2c-a285-4796-8607-3cbf49471420) cmdlet.</span></span>

```powershell
# This command sets a breakpoint on the Server variable in the Sample.ps1 script.
Set-PSBreakpoint -Script sample.ps1 -Variable Server
```

### <a name="list-all-breakpoints"></a><span data-ttu-id="fe83a-128">Töréspontokat listázása</span><span class="sxs-lookup"><span data-stu-id="fe83a-128">List all breakpoints</span></span>

<span data-ttu-id="fe83a-129">Töréspontokat megjeleníti az aktuális Windows PowerShell-munkamenetben.</span><span class="sxs-lookup"><span data-stu-id="fe83a-129">Displays all breakpoints in the current Windows PowerShell session.</span></span>

<span data-ttu-id="fe83a-130">Az a **Debug** menüben kattintson a **lista töréspontok**.</span><span class="sxs-lookup"><span data-stu-id="fe83a-130">On the **Debug** menu, click **List Breakpoints**.</span></span> <span data-ttu-id="fe83a-131">A következő parancsfájl egy példát, hogyan listázhatja a konzol panelen töréspontokat használatával a [Get-PSBreakpoint](https://technet.microsoft.com/library/0bf48936-00ab-411c-b5e0-9b10a812a3c6) parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="fe83a-131">The following script is an example of how you can list all breakpoints from the Console Pane by using the [Get-PSBreakpoint](https://technet.microsoft.com/library/0bf48936-00ab-411c-b5e0-9b10a812a3c6) cmdlet.</span></span>

```powershell
# This command lists all breakpoints in the current session.
Get-PSBreakpoint
```

### <a name="remove-a-breakpoint"></a><span data-ttu-id="fe83a-132">Töréspont eltávolítása</span><span class="sxs-lookup"><span data-stu-id="fe83a-132">Remove a breakpoint</span></span>

<span data-ttu-id="fe83a-133">Töréspont eltávolítása törli őket.</span><span class="sxs-lookup"><span data-stu-id="fe83a-133">Removing a breakpoint deletes it.</span></span>

<span data-ttu-id="fe83a-134">Ha úgy véli, hogy később újra felhasználhatja, érdemes lehet érdemes [tiltsa le a töréspont](#disable-a-breakpoint) , helyette.</span><span class="sxs-lookup"><span data-stu-id="fe83a-134">If you think you might want to use it again later, consider [Disable a Breakpoint](#disable-a-breakpoint) it instead.</span></span>
<span data-ttu-id="fe83a-135">Kattintson a jobb gombbal a sor, ahol szeretné eltávolítani egy töréspontot, és kattintson a **töréspont**.</span><span class="sxs-lookup"><span data-stu-id="fe83a-135">Right-click the line where you want to remove a breakpoint, and then click **Toggle Breakpoint**.</span></span>
<span data-ttu-id="fe83a-136">Vagy kattintson a sort, amelyben el kívánja távolítani egy töréspontot, és az a **Debug** menüben kattintson a **töréspont**.</span><span class="sxs-lookup"><span data-stu-id="fe83a-136">Or, click the line where you want to remove a breakpoint, and on the **Debug** menu, click **Toggle Breakpoint**.</span></span>
<span data-ttu-id="fe83a-137">A következő parancsfájl példaként szolgál a megadott Azonosítóval rendelkező töréspont eltávolítása a konzol panel használatával a [Remove-PSBreakpoint](https://technet.microsoft.com/library/4c877a80-0ea0-4790-9281-88c08ef0ddd6) parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="fe83a-137">The following script is an example of how to remove a breakpoint with a specified ID from the Console Pane by using the [Remove-PSBreakpoint](https://technet.microsoft.com/library/4c877a80-0ea0-4790-9281-88c08ef0ddd6) cmdlet.</span></span>

```powershell
# This command deletes the breakpoint with breakpoint ID 2.
Remove-PSBreakpoint -Id 2
```

### <a name="remove-all-breakpoints"></a><span data-ttu-id="fe83a-138">Az összes töréspont eltávolítása</span><span class="sxs-lookup"><span data-stu-id="fe83a-138">Remove All Breakpoints</span></span>

<span data-ttu-id="fe83a-139">Töréspontokat definiálva az aktuális munkamenetben eltávolítása a **Debug** menüben kattintson a **minden töréspont eltávolítása**.</span><span class="sxs-lookup"><span data-stu-id="fe83a-139">To remove all breakpoints defined in the current session, on the **Debug** menu, click **Remove All Breakpoints**.</span></span>

<span data-ttu-id="fe83a-140">Az alábbi parancsfájlt minden töréspont eltávolítása a konzol panel használatával példája a [Remove-PSBreakpoint](https://technet.microsoft.com/library/4c877a80-0ea0-4790-9281-88c08ef0ddd6) parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="fe83a-140">The following script is an example of how to remove all breakpoints from the Console Pane by using the [Remove-PSBreakpoint](https://technet.microsoft.com/library/4c877a80-0ea0-4790-9281-88c08ef0ddd6) cmdlet.</span></span>

```powershell
# This command deletes all of the breakpoints in the current session.
Get-PSBreakpoint | Remove-PSBreakpoint
```

### <a name="disable-a-breakpoint"></a><span data-ttu-id="fe83a-141">Töréspont letiltása</span><span class="sxs-lookup"><span data-stu-id="fe83a-141">Disable a Breakpoint</span></span>

<span data-ttu-id="fe83a-142">Töréspont letiltása nem távolítja el azt. azt kikapcsolja, amíg az nincs engedélyezve.</span><span class="sxs-lookup"><span data-stu-id="fe83a-142">Disabling a breakpoint does not remove it; it turns it off until it is enabled.</span></span>  <span data-ttu-id="fe83a-143">Egy adott sor töréspontot letiltásához kattintson a jobb gombbal a sor, ahol szeretné letiltani egy töréspontot, és kattintson a **letiltása töréspontot**.</span><span class="sxs-lookup"><span data-stu-id="fe83a-143">To disable a specific line breakpoint, right-click the line where you want to disable a breakpoint, and then click **Disable Breakpoint**.</span></span> <span data-ttu-id="fe83a-144">Vagy kattintson a sor, amikor le kívánja tiltani egy töréspontot, nyomja le az ENTER **F9** vagy a a **hibakeresése** menüben kattintson a **letiltása töréspontot**.</span><span class="sxs-lookup"><span data-stu-id="fe83a-144">Or, click the line where you want to disable a breakpoint, and press **F9** or, on the **Debug** menu, click **Disable Breakpoint**.</span></span> <span data-ttu-id="fe83a-145">A következő parancsfájl egy példát, hogyan eltávolíthatja a megadott Azonosítóval rendelkező egy töréspontot a konzol panelen használatával a [Disable-PSBreakpoint](https://technet.microsoft.com/library/d4974e9b-0aaa-4e20-b87f-f599a413e4e8) parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="fe83a-145">The following script is an example of how you can remove a breakpoint with a specified ID from the Console Pane by using the [Disable-PSBreakpoint](https://technet.microsoft.com/library/d4974e9b-0aaa-4e20-b87f-f599a413e4e8) cmdlet.</span></span>

```powershell
# This command disables the breakpoint with breakpoint ID 0.
Disable-PSBreakpoint -Id 0
```

### <a name="disable-all-breakpoints"></a><span data-ttu-id="fe83a-146">Tiltsa le az összes töréspontok keresése</span><span class="sxs-lookup"><span data-stu-id="fe83a-146">Disable All Breakpoints</span></span>

<span data-ttu-id="fe83a-147">Töréspont letiltása nem távolítja el azt. azt kikapcsolja, amíg az nincs engedélyezve.</span><span class="sxs-lookup"><span data-stu-id="fe83a-147">Disabling a breakpoint does not remove it; it turns it off until it is enabled.</span></span>  <span data-ttu-id="fe83a-148">Le kívánja tiltani töréspontokat a jelenlegi munkamenet a **Debug** menüben kattintson a **töréspontokat letiltása**.</span><span class="sxs-lookup"><span data-stu-id="fe83a-148">To disable all breakpoints in the current session, on the **Debug** menu, click **Disable all Breakpoints**.</span></span> <span data-ttu-id="fe83a-149">A következő parancsfájl példaként szolgál a letiltásáról töréspontokat a konzol panelen használatával a [Disable-PSBreakpoint](https://technet.microsoft.com/library/d4974e9b-0aaa-4e20-b87f-f599a413e4e8) parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="fe83a-149">The following script is an example of how you can disable all breakpoints from the Console Pane by using the [Disable-PSBreakpoint](https://technet.microsoft.com/library/d4974e9b-0aaa-4e20-b87f-f599a413e4e8) cmdlet.</span></span>

```powershell
# This command disables all breakpoints in the current session.
# You can abbreviate this command as: "gbp | dbp".
Get-PSBreakpoint | Disable-PSBreakpoint
```

### <a name="enable-a-breakpoint"></a><span data-ttu-id="fe83a-150">Töréspont engedélyezése</span><span class="sxs-lookup"><span data-stu-id="fe83a-150">Enable a Breakpoint</span></span>

<span data-ttu-id="fe83a-151">Ahhoz, hogy egy adott töréspontot, kattintson a jobb gombbal a sor hol szeretne engedélyezni egy töréspontot, és kattintson a **engedélyezése töréspontot**.</span><span class="sxs-lookup"><span data-stu-id="fe83a-151">To enable a specific breakpoint, right-click the line where you want to enable a breakpoint, and then click **Enable Breakpoint**.</span></span> <span data-ttu-id="fe83a-152">Vagy kattintson a sorra, ahol szeretne engedélyezni egy töréspontot, és nyomja le az **F9** vagy a a **Debug** menüben kattintson a **engedélyezése töréspontot**.</span><span class="sxs-lookup"><span data-stu-id="fe83a-152">Or, click the line where you want to enable a breakpoint, and then press **F9** or, on the **Debug** menu, click **Enable Breakpoint**.</span></span> <span data-ttu-id="fe83a-153">A következő parancsfájl egy példát, hogyan engedélyezheti a konzol panelen adott töréspontok használatával a [engedélyezése – PSBreakpoint](https://technet.microsoft.com/library/739e1091-3b3f-405f-a428-bec7543e5df0) parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="fe83a-153">The following script is an example of how you can enable specific breakpoints from the Console Pane by using the [Enable-PSBreakpoint](https://technet.microsoft.com/library/739e1091-3b3f-405f-a428-bec7543e5df0) cmdlet.</span></span>

```powershell
# This command enables breakpoints with breakpoint IDs 0, 1, and 5.
Enable-PSBreakpoint -Id 0, 1, 5
```

### <a name="enable-all-breakpoints"></a><span data-ttu-id="fe83a-154">Az összes töréspontok engedélyezése</span><span class="sxs-lookup"><span data-stu-id="fe83a-154">Enable All Breakpoints</span></span>

<span data-ttu-id="fe83a-155">Ahhoz, hogy definiálva az aktuális munkamenetben töréspontokat a **hibakeresése** menüben kattintson **töréspontokat engedélyezése**.</span><span class="sxs-lookup"><span data-stu-id="fe83a-155">To enable all breakpoints defined in the current session, on the **Debug** menu, click **Enable all Breakpoints**.</span></span> <span data-ttu-id="fe83a-156">A következő parancsfájl egy példát, hogyan engedélyezheti a konzol panelen töréspontokat a rendszer a [engedélyezése – PSBreakpoint](https://technet.microsoft.com/library/739e1091-3b3f-405f-a428-bec7543e5df0) parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="fe83a-156">The following script is an example of how you can enable all breakpoints from the Console Pane by using the [Enable-PSBreakpoint](https://technet.microsoft.com/library/739e1091-3b3f-405f-a428-bec7543e5df0) cmdlet.</span></span>

```powershell
# This command enables all breakpoints in the current session.
# You can abbreviate the command by using their aliases: "gbp | ebp".
Get-PSBreakpoint | Enable-PSBreakpoint
```

## <a name="how-to-manage-a-debugging-session"></a><span data-ttu-id="fe83a-157">A hibakeresési munkamenet kezelése</span><span class="sxs-lookup"><span data-stu-id="fe83a-157">How to manage a debugging session</span></span>

<span data-ttu-id="fe83a-158">Mielőtt elkezdené, hibakeresés, be kell egy vagy több töréspontokat a kiválasztott.</span><span class="sxs-lookup"><span data-stu-id="fe83a-158">Before you start debugging, you must set one or more breakpoints.</span></span> <span data-ttu-id="fe83a-159">Nem lehet állítson be egy töréspontot, kivéve, ha a parancsfájl, amelyen hibakeresést végez, a rendszer menti.</span><span class="sxs-lookup"><span data-stu-id="fe83a-159">You cannot set a breakpoint unless the script that you want to debug is saved.</span></span> <span data-ttu-id="fe83a-160">Bemutatja, hogyan állítson be egy töréspontot a irányban, lásd: [töréspontok kezelése](#how-to-manage-breakpoints) vagy [Set-PSBreakpoint](https://docs.microsoft.com/powershell/module/microsoft.powershell.utility/set-psbreakpoint).</span><span class="sxs-lookup"><span data-stu-id="fe83a-160">For directions on of how to set a breakpoint, see [How to manage breakpoints](#how-to-manage-breakpoints) or [Set-PSBreakpoint](https://docs.microsoft.com/powershell/module/microsoft.powershell.utility/set-psbreakpoint).</span></span> <span data-ttu-id="fe83a-161">Után elindítja a hibakeresés, amíg le nem állítják hibakeresés parancsfájl nem szerkeszthető.</span><span class="sxs-lookup"><span data-stu-id="fe83a-161">After you start debugging, you cannot edit a script until you stop debugging.</span></span> <span data-ttu-id="fe83a-162">Egy parancsfájl, amely rendelkezik egy vagy több töréspontokat a kiválasztott állítsa be a rendszer automatikusan menti azt futtatása előtt.</span><span class="sxs-lookup"><span data-stu-id="fe83a-162">A script that has one or more breakpoints set is automatically saved before it is run.</span></span>

### <a name="to-start-debugging"></a><span data-ttu-id="fe83a-163">A hibakeresés</span><span class="sxs-lookup"><span data-stu-id="fe83a-163">To start debugging</span></span>

<span data-ttu-id="fe83a-164">Nyomja meg **F5** vagy az eszköztáron kattintson a **parancsfájl futtatása** ikonra, vagy a a **Debug** menüben kattintson **Futtatás/Folytatás**.</span><span class="sxs-lookup"><span data-stu-id="fe83a-164">Press **F5** or, on the toolbar, click the **Run Script** icon, or on the **Debug** menu click **Run/Continue**.</span></span> <span data-ttu-id="fe83a-165">A szkript futtatása, amíg az első töréspont tapasztal.</span><span class="sxs-lookup"><span data-stu-id="fe83a-165">The script runs until it encounters the first breakpoint.</span></span> <span data-ttu-id="fe83a-166">Nincs művelet megszakítja, és kiemeli a sort, amelyen szünetel.</span><span class="sxs-lookup"><span data-stu-id="fe83a-166">It pauses operation there and highlights the line on which it paused.</span></span>

### <a name="to-continue-debugging"></a><span data-ttu-id="fe83a-167">A folytatáshoz a hibakeresés</span><span class="sxs-lookup"><span data-stu-id="fe83a-167">To continue debugging</span></span>

<span data-ttu-id="fe83a-168">Nyomja meg **F5** vagy az eszköztáron kattintson a **parancsfájl futtatása** ikonra, vagy a a **Debug** menüben kattintson a **Futtatás/Folytatás** vagy írja be a konzol ablaktáblában **C** , és nyomja le az **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="fe83a-168">Press **F5** or, on the toolbar, click the **Run Script** icon, or on the **Debug** menu, click **Run/Continue** or, in the Console Pane, type **C** and then press **ENTER**.</span></span> <span data-ttu-id="fe83a-169">Ennek hatására a szkript a következő töréspontig vagy a teljes körű parancsfájl futtatását, ha nincsenek további töréspontokat a kiválasztott program hibát.</span><span class="sxs-lookup"><span data-stu-id="fe83a-169">This causes the script to continue running to the next breakpoint or to the end of the script if no further breakpoints are encountered.</span></span>

### <a name="to-view-the-call-stack"></a><span data-ttu-id="fe83a-170">A hívási veremben megtekintése</span><span class="sxs-lookup"><span data-stu-id="fe83a-170">To view the call stack</span></span>

<span data-ttu-id="fe83a-171">A hívási veremben jeleníti meg az aktuális Futtatás helye a szkriptben.</span><span class="sxs-lookup"><span data-stu-id="fe83a-171">The call stack displays the current run location in the script.</span></span> <span data-ttu-id="fe83a-172">Ha a parancsfájl egy másik függvény által hívott függvény fut, majd, amely képviseli jelennek meg a további sorokat a kimenetben.</span><span class="sxs-lookup"><span data-stu-id="fe83a-172">If the script is running in a function that was called by a different function, then that is represented in the display by additional rows in the output.</span></span> <span data-ttu-id="fe83a-173">A legalsó sor jeleníti meg az eredeti parancsfájl és a sort, amelyben egy függvényt hívták.</span><span class="sxs-lookup"><span data-stu-id="fe83a-173">The bottom-most row displays the original script and the line in it in which a function was called.</span></span> <span data-ttu-id="fe83a-174">A következő a sor megmutatja, hogy a függvény és a sort, amelyben egy másik függvény előfordulhat, hogy hívták.</span><span class="sxs-lookup"><span data-stu-id="fe83a-174">The next line up shows that function and the line in it in which another function might have been called.</span></span>  <span data-ttu-id="fe83a-175">A legfelső sor látható, amelyen a töréspont be van állítva az aktuális sor az aktuális környezetben.</span><span class="sxs-lookup"><span data-stu-id="fe83a-175">The top-most row shows the current context of the current line on which the breakpoint is set.</span></span>

<span data-ttu-id="fe83a-176">Fel van függesztve, amíg a jelenlegi hívási vermet, nyomja le a **CTRL + SHIFT + D** vagy a a **Debug** menüben kattintson a **megjelenített hívási veremnek** vagy írja be a konzol ablaktáblában **K**  , és nyomja le az **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="fe83a-176">While paused, to see the current call stack, press **CTRL+SHIFT+D** or, on the **Debug** menu, click **Display Call Stack** or, in the Console Pane, type **K** and then press **ENTER**.</span></span>

### <a name="to-stop-debugging"></a><span data-ttu-id="fe83a-177">A hibakereső leállítása</span><span class="sxs-lookup"><span data-stu-id="fe83a-177">To stop debugging</span></span>

<span data-ttu-id="fe83a-178">Nyomja le az **SHIFT-F5** vagy a a **Debug** menüben kattintson a **hibakereső leállítása**, vagy írja be a konzol ablaktáblában **Q** , és nyomja le az  **Adja meg**.</span><span class="sxs-lookup"><span data-stu-id="fe83a-178">Press **SHIFT-F5** or, on the **Debug** menu, click **Stop Debugger**, or, in the Console Pane, type **Q** and then press **ENTER**.</span></span>

## <a name="how-to-step-over-step-into-and-step-out-while-debugging"></a><span data-ttu-id="fe83a-179">Átlépés, lépjen be és hibakeresése során krokovat s vystoupením</span><span class="sxs-lookup"><span data-stu-id="fe83a-179">How to step over, step into, and step out while debugging</span></span>

<span data-ttu-id="fe83a-180">Lépjen az a folyamat egy utasítás egy időben futnak.</span><span class="sxs-lookup"><span data-stu-id="fe83a-180">Stepping is the process of running one statement at a time.</span></span> <span data-ttu-id="fe83a-181">Állítsa le az egy sor kódot, és vizsgálja meg az értékeket a változók és a rendszer állapotát.</span><span class="sxs-lookup"><span data-stu-id="fe83a-181">You can stop on a line of code, and examine the values of variables and the state of the system.</span></span> <span data-ttu-id="fe83a-182">A következő táblázat ismerteti a gyakori hibakeresési feladatokat, mint a ke krokování keresztül, lépjen be és lépjen.</span><span class="sxs-lookup"><span data-stu-id="fe83a-182">The following table describes common debugging tasks such as stepping over, stepping into, and stepping out.</span></span>

| <span data-ttu-id="fe83a-183">A feladat hibakeresési</span><span class="sxs-lookup"><span data-stu-id="fe83a-183">Debugging Task</span></span> | <span data-ttu-id="fe83a-184">Leírás</span><span class="sxs-lookup"><span data-stu-id="fe83a-184">Description</span></span> | <span data-ttu-id="fe83a-185">Hogyan végezheti el, a PowerShell ISE-ben</span><span class="sxs-lookup"><span data-stu-id="fe83a-185">How to accomplish it in PowerShell ISE</span></span> |
| --- | --- | --- |
| <span data-ttu-id="fe83a-186">**Lépjen be**</span><span class="sxs-lookup"><span data-stu-id="fe83a-186">**Step Into**</span></span> | <span data-ttu-id="fe83a-187">Az aktuális utasítás végrehajtása, és a következő utasítást, majd leáll.</span><span class="sxs-lookup"><span data-stu-id="fe83a-187">Executes the current statement and then stops at the next statement.</span></span> <span data-ttu-id="fe83a-188">Ha az aktuális utasítás egy függvény vagy parancsfájl hívást, majd a hibakeresőt a lépéseket, hogy a függvény vagy parancsfájl, ellenkező esetben leállítja, a következő utasítást.</span><span class="sxs-lookup"><span data-stu-id="fe83a-188">If the current statement is a function or script call, then the debugger steps into that function or script, otherwise it stops at the next statement.</span></span> | <span data-ttu-id="fe83a-189">Nyomja le az **F11** vagy a a **Debug** menüben kattintson a **lépés be**, vagy írja be a konzol ablaktáblában **S** nyomja le az ENTER **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="fe83a-189">Press **F11** or, on the **Debug** menu, click **Step Into**, or in the Console Pane, type **S** and press **ENTER**.</span></span> |
| <span data-ttu-id="fe83a-190">**Átlépés**</span><span class="sxs-lookup"><span data-stu-id="fe83a-190">**Step Over**</span></span> | <span data-ttu-id="fe83a-191">Az aktuális utasítás végrehajtása, és a következő utasítást, majd leáll.</span><span class="sxs-lookup"><span data-stu-id="fe83a-191">Executes the current statement and then stops at the next statement.</span></span> <span data-ttu-id="fe83a-192">Ha az aktuális utasítás függvény vagy parancsfájl-hívást, majd a hibakeresőt a teljes függvény vagy parancsfájl hajt végre, és a következő utasítást a függvény hívása után megáll.</span><span class="sxs-lookup"><span data-stu-id="fe83a-192">If the current statement is a function or script call, then the debugger executes the whole function or script, and it stops at the next statement after the function call.</span></span> | <span data-ttu-id="fe83a-193">Nyomja le az **F10** vagy a a **Debug** menüben kattintson a **Átlépés**, vagy írja be a konzol ablaktáblában **V** nyomja le az ENTER **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="fe83a-193">Press **F10** or, on the **Debug** menu, click **Step Over**, or in the Console Pane, type **V** and press **ENTER**.</span></span> |
| <span data-ttu-id="fe83a-194">**Krokovat s Vystoupením**</span><span class="sxs-lookup"><span data-stu-id="fe83a-194">**Step Out**</span></span> | <span data-ttu-id="fe83a-195">Lépések az aktuális függvény és egy szinttel, ha a függvény van beágyazva.</span><span class="sxs-lookup"><span data-stu-id="fe83a-195">Steps out of the current function and up one level if the function is nested.</span></span> <span data-ttu-id="fe83a-196">Ha a fő törzsében, a parancsfájl végrehajtása a teljes körű, vagy a következő töréspontig.</span><span class="sxs-lookup"><span data-stu-id="fe83a-196">If in the main body, the script is executed to the end, or to the next breakpoint.</span></span> <span data-ttu-id="fe83a-197">A rendszer kihagyta utasításokat végrehajtva, de nem lépcsőzetes keresztül.</span><span class="sxs-lookup"><span data-stu-id="fe83a-197">The skipped statements are executed, but not stepped through.</span></span> | <span data-ttu-id="fe83a-198">Nyomja le az **SHIFT + F11**, vagy a a **Debug** menüben kattintson a **lépés ki**, vagy írja be a konzol ablaktáblában **O** nyomja le az ENTER **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="fe83a-198">Press **SHIFT+F11**, or on the **Debug** menu, click **Step Out**, or in the Console Pane, type **O** and press **ENTER**.</span></span> |
| <span data-ttu-id="fe83a-199">**Továbbra is**</span><span class="sxs-lookup"><span data-stu-id="fe83a-199">**Continue**</span></span> | <span data-ttu-id="fe83a-200">A teljes körű, vagy a következő töréspontig végrehajtása folytatódik.</span><span class="sxs-lookup"><span data-stu-id="fe83a-200">Continues execution to the end, or to the next breakpoint.</span></span> <span data-ttu-id="fe83a-201">A rendszer kihagyta funkciók és indítások végrehajtva, de nem lépcsőzetes keresztül.</span><span class="sxs-lookup"><span data-stu-id="fe83a-201">The skipped functions and invocations are executed, but not stepped through.</span></span> | <span data-ttu-id="fe83a-202">Nyomja le az **F5** vagy a a **Debug** menüben kattintson a **Futtatás/Folytatás**, vagy írja be a konzol ablaktáblában **C** nyomja le az ENTER **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="fe83a-202">Press **F5** or, on the **Debug** menu, click **Run/Continue**, or in the Console Pane, type **C** and press **ENTER**.</span></span> |

## <a name="how-to-display-the-values-of-variables-while-debugging"></a><span data-ttu-id="fe83a-203">Hibakeresés közben változók értékeinek megjelenítése</span><span class="sxs-lookup"><span data-stu-id="fe83a-203">How to display the values of variables while debugging</span></span>

<span data-ttu-id="fe83a-204">A változók aktuális értékeit megjelenítheti a szkriptben, a kód lépéseit.</span><span class="sxs-lookup"><span data-stu-id="fe83a-204">You can display the current values of variables in the script as you step through the code.</span></span>

### <a name="to-display-the-values-of-standard-variables"></a><span data-ttu-id="fe83a-205">Standard változók értékeinek megjelenítése</span><span class="sxs-lookup"><span data-stu-id="fe83a-205">To display the values of standard variables</span></span>

<span data-ttu-id="fe83a-206">Az alábbi módszerek valamelyikével:</span><span class="sxs-lookup"><span data-stu-id="fe83a-206">Use one of the following methods:</span></span>

- <span data-ttu-id="fe83a-207">A parancsfájl panelen a kurzort a változót, egy elemleírás jelenít meg az értékét.</span><span class="sxs-lookup"><span data-stu-id="fe83a-207">In the Script Pane, hover over the variable to display its value as a tool tip.</span></span>

- <span data-ttu-id="fe83a-208">A konzol ablaktáblában írja be a változó nevét, majd nyomja le **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="fe83a-208">In the Console Pane, type the variable name and press **ENTER**.</span></span>

<span data-ttu-id="fe83a-209">A ISE-ben minden ablaktáblák mindig ugyanabban a hatókörben vannak.</span><span class="sxs-lookup"><span data-stu-id="fe83a-209">All panes in ISE are always in the same scope.</span></span> <span data-ttu-id="fe83a-210">Ezért egy parancsfájlt, hibakeresés során, írja be a konzol ablaktáblában parancsok futtatása parancsfájl hatókörében.</span><span class="sxs-lookup"><span data-stu-id="fe83a-210">Therefore, while you are debugging a script, the commands that you type in the Console Pane run in script scope.</span></span> <span data-ttu-id="fe83a-211">Ez lehetővé teszi, hogy a konzol panel használata a változók értékeit, és csak a szkriptben meghatározott függvényeket.</span><span class="sxs-lookup"><span data-stu-id="fe83a-211">This allows you to use the Console Pane to find the values of variables and call functions that are defined only in the script.</span></span>

### <a name="to-display-the-values-of-automatic-variables"></a><span data-ttu-id="fe83a-212">Az automatikus változók értékeinek megjelenítése</span><span class="sxs-lookup"><span data-stu-id="fe83a-212">To display the values of automatic variables</span></span>

<span data-ttu-id="fe83a-213">A fenti módszer segítségével szinte minden változó értékének megjelenítése egy parancsfájl hibakeresés során.</span><span class="sxs-lookup"><span data-stu-id="fe83a-213">You can use the preceding method to display the value of almost all variables while you are debugging a script.</span></span> <span data-ttu-id="fe83a-214">Ezek a módszerek azonban nem működnek a következő automatikus változók.</span><span class="sxs-lookup"><span data-stu-id="fe83a-214">However, these methods do not work for the following automatic variables.</span></span>

- <span data-ttu-id="fe83a-215">$_</span><span class="sxs-lookup"><span data-stu-id="fe83a-215">$_</span></span>

- <span data-ttu-id="fe83a-216">$Input</span><span class="sxs-lookup"><span data-stu-id="fe83a-216">$Input</span></span>

- <span data-ttu-id="fe83a-217">$MyInvocation</span><span class="sxs-lookup"><span data-stu-id="fe83a-217">$MyInvocation</span></span>

- <span data-ttu-id="fe83a-218">$PSBoundParameters</span><span class="sxs-lookup"><span data-stu-id="fe83a-218">$PSBoundParameters</span></span>

- <span data-ttu-id="fe83a-219">$Args</span><span class="sxs-lookup"><span data-stu-id="fe83a-219">$Args</span></span>

<span data-ttu-id="fe83a-220">Meg ezeket a változókat bármelyikének értéket jeleníti meg, ha a változó értékét kap a belső folyamatban a hibakeresőt használ, nem a szkriptben a változó értékét.</span><span class="sxs-lookup"><span data-stu-id="fe83a-220">If you try to display the value of any of these variables, you get the value of that variable for in an internal pipeline the debugger uses, not the value of the variable in the script.</span></span> <span data-ttu-id="fe83a-221">Ön megkerüléséhez Ez néhány változóhoz ($_, $Input, $MyInvocation, $PSBoundParameters és $Args) a következő módszerrel:</span><span class="sxs-lookup"><span data-stu-id="fe83a-221">You can work around this for a few variables ($_, $Input, $MyInvocation, $PSBoundParameters, and $Args) by using the following method:</span></span>

1. <span data-ttu-id="fe83a-222">Új változó az automatikus változó értékét hozzárendelése a szkriptben.</span><span class="sxs-lookup"><span data-stu-id="fe83a-222">In the script, assign the value of the automatic variable to a new variable.</span></span>

2. <span data-ttu-id="fe83a-223">Megjeleníti az új változó értékét, vagy az egérmutatót a parancsfájl panelen az új változó, vagy írja be az új változó a konzol ablaktáblában.</span><span class="sxs-lookup"><span data-stu-id="fe83a-223">Display the value of the new variable, either by hovering over the new variable in the Script Pane, or by typing the new variable in the Console Pane.</span></span>

<span data-ttu-id="fe83a-224">Például szeretné megjeleníteni a $MyInvocation változó értékét a szkriptben, rendelni az értéket az új változó, például a $scriptname, és ezután mutasson vagy $scriptname változó értékéhez megjelenítéséhez írja be.</span><span class="sxs-lookup"><span data-stu-id="fe83a-224">For example, to display the value of the $MyInvocation variable, in the script, assign the value to a new variable, such as $scriptname, and then hover over or type the $scriptname variable to display its value.</span></span>

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

## <a name="see-also"></a><span data-ttu-id="fe83a-225">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="fe83a-225">See Also</span></span>

- [<span data-ttu-id="fe83a-226">A Windows PowerShell ISE felfedezése</span><span class="sxs-lookup"><span data-stu-id="fe83a-226">Exploring the Windows PowerShell ISE</span></span>](../../getting-started/fundamental/exploring-the-windows-powershell-ise.md)