---
ms.date: 08/14/2018
keywords: PowerShell, a parancsmag
title: Távoli parancsok futtatása
ms.assetid: d6938b56-7dc8-44ba-b4d4-cd7b169fd74d
ms.openlocfilehash: 2001b5509acde6ec4259bb1442944958a67aa66f
ms.sourcegitcommit: 56b9be8503a5a1342c0b85b36f5ba6f57c281b63
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/21/2018
ms.locfileid: "43133857"
---
# <a name="running-remote-commands"></a><span data-ttu-id="2cc8a-103">Távoli parancsok futtatása</span><span class="sxs-lookup"><span data-stu-id="2cc8a-103">Running Remote Commands</span></span>

<span data-ttu-id="2cc8a-104">Egy vagy több száz számítógépről, egyetlen PowerShell-paranccsal, futtathat parancsokat.</span><span class="sxs-lookup"><span data-stu-id="2cc8a-104">You can run commands on one or hundreds of computers with a single PowerShell command.</span></span> <span data-ttu-id="2cc8a-105">Windows PowerShell támogatja a távoli számítógépek különböző technológiákkal, beleértve a WMI távoli Eljáráshívás és WS-Management használatával.</span><span class="sxs-lookup"><span data-stu-id="2cc8a-105">Windows PowerShell supports remote computing by using various technologies, including WMI, RPC, and WS-Management.</span></span>

<span data-ttu-id="2cc8a-106">A PowerShell Core WMI, támogatja a WS-Management és az SSH-távelérésének lehetővé tétele.</span><span class="sxs-lookup"><span data-stu-id="2cc8a-106">PowerShell Core supports WMI, WS-Management, and SSH remoting.</span></span> <span data-ttu-id="2cc8a-107">RPC már nem támogatott.</span><span class="sxs-lookup"><span data-stu-id="2cc8a-107">RPC is no longer supported.</span></span>

<span data-ttu-id="2cc8a-108">A távoli eljáráshívás a PowerShell Core kapcsolatos további információkért tekintse meg a következő cikkeket:</span><span class="sxs-lookup"><span data-stu-id="2cc8a-108">For more information about remoting in PowerShell Core, see the following articles:</span></span>

- <span data-ttu-id="2cc8a-109">[SSH távoli eljáráshívás a PowerShell Core][ssh-remoting]</span><span class="sxs-lookup"><span data-stu-id="2cc8a-109">[SSH Remoting in PowerShell Core][ssh-remoting]</span></span>
- <span data-ttu-id="2cc8a-110">[A PowerShell Core a wsman által használt távoli eljáráshívás][wsman-remoting]</span><span class="sxs-lookup"><span data-stu-id="2cc8a-110">[WSMan Remoting in PowerShell Core][wsman-remoting]</span></span>

## <a name="windows-powershell-remoting-without-configuration"></a><span data-ttu-id="2cc8a-111">Windows PowerShell távoli eljáráshívás konfiguráció nélkül</span><span class="sxs-lookup"><span data-stu-id="2cc8a-111">Windows PowerShell Remoting Without Configuration</span></span>

<span data-ttu-id="2cc8a-112">Számos Windows PowerShell-parancsmagok rendelkeznie a ComputerName paraméter, amely lehetővé teszi az adatok gyűjtéséhez és a egy vagy több távoli számítógépeken lévő beállítások módosításához.</span><span class="sxs-lookup"><span data-stu-id="2cc8a-112">Many Windows PowerShell cmdlets have the ComputerName parameter that enables you to collect data and change settings on one or more remote computers.</span></span> <span data-ttu-id="2cc8a-113">Ezek a parancsmagok különböző kommunikációs protokollokat használ, és az összes Windows operációs rendszeren külön konfigurálás nélkül működik.</span><span class="sxs-lookup"><span data-stu-id="2cc8a-113">These cmdlets use varying communication protocols and work on all Windows operating systems without any special configuration.</span></span>

<span data-ttu-id="2cc8a-114">Ezek a parancsmagok a következők:</span><span class="sxs-lookup"><span data-stu-id="2cc8a-114">These cmdlets include:</span></span>

- [<span data-ttu-id="2cc8a-115">Számítógép újraindítása</span><span class="sxs-lookup"><span data-stu-id="2cc8a-115">Restart-Computer</span></span>](/powershell/module/microsoft.powershell.management/restart-computer)
- [<span data-ttu-id="2cc8a-116">Test-Connection</span><span class="sxs-lookup"><span data-stu-id="2cc8a-116">Test-Connection</span></span>](/powershell/module/microsoft.powershell.management/test-connection)
- [<span data-ttu-id="2cc8a-117">CLEAR-Eseménynapló</span><span class="sxs-lookup"><span data-stu-id="2cc8a-117">Clear-EventLog</span></span>](/powershell/module/microsoft.powershell.management/clear-eventlog)
- [<span data-ttu-id="2cc8a-118">Get-EventLog</span><span class="sxs-lookup"><span data-stu-id="2cc8a-118">Get-EventLog</span></span>](/powershell/module/microsoft.powershell.management/get-eventlog)
- [<span data-ttu-id="2cc8a-119">Get-HotFix</span><span class="sxs-lookup"><span data-stu-id="2cc8a-119">Get-HotFix</span></span>](/powershell/module/microsoft.powershell.management/get-hotfix)
- [<span data-ttu-id="2cc8a-120">Get-Process</span><span class="sxs-lookup"><span data-stu-id="2cc8a-120">Get-Process</span></span>](/powershell/module/microsoft.powershell.management/get-process)
- [<span data-ttu-id="2cc8a-121">Get-Service</span><span class="sxs-lookup"><span data-stu-id="2cc8a-121">Get-Service</span></span>](/powershell/module/microsoft.powershell.management/get-service)
- [<span data-ttu-id="2cc8a-122">Set-Service</span><span class="sxs-lookup"><span data-stu-id="2cc8a-122">Set-Service</span></span>](/powershell/module/microsoft.powershell.management/set-service)
- [<span data-ttu-id="2cc8a-123">Get-WinEvent</span><span class="sxs-lookup"><span data-stu-id="2cc8a-123">Get-WinEvent</span></span>](/powershell/module/microsoft.powershell.diagnostics/get-winevent)
- [<span data-ttu-id="2cc8a-124">Get-WmiObject</span><span class="sxs-lookup"><span data-stu-id="2cc8a-124">Get-WmiObject</span></span>](/powershell/module/microsoft.powershell.management/get-wmiobject)

<span data-ttu-id="2cc8a-125">Általában a távoli eljáráshívás külön konfigurálás nélkül támogató parancsmagok a ComputerName paraméterrel rendelkezik, és a munkamenet-paraméter nem rendelkezik.</span><span class="sxs-lookup"><span data-stu-id="2cc8a-125">Typically, cmdlets that support remoting without special configuration have the ComputerName parameter and don't have the Session parameter.</span></span> <span data-ttu-id="2cc8a-126">Ezeket a parancsmagokat a munkamenetben, írja be:</span><span class="sxs-lookup"><span data-stu-id="2cc8a-126">To find these cmdlets in your session, type:</span></span>

```powershell
Get-Command | where { $_.parameters.keys -contains "ComputerName" -and $_.parameters.keys -notcontains "Session"}
```

## <a name="windows-powershell-remoting"></a><span data-ttu-id="2cc8a-127">Windows PowerShell távoli eljáráshívás</span><span class="sxs-lookup"><span data-stu-id="2cc8a-127">Windows PowerShell Remoting</span></span>

<span data-ttu-id="2cc8a-128">A WS-Management protokoll használatával, a Windows PowerShell távoli eljáráshívás lehetővé teszi egy vagy több távoli számítógépeken bármely Windows PowerShell-parancs futtatása.</span><span class="sxs-lookup"><span data-stu-id="2cc8a-128">Using the WS-Management protocol, Windows PowerShell remoting lets you run any Windows PowerShell command on one or more remote computers.</span></span> <span data-ttu-id="2cc8a-129">Állandó kapcsolatot, interaktív munkamenetek indításához és szkriptek futtatása távoli számítógépeken.</span><span class="sxs-lookup"><span data-stu-id="2cc8a-129">You can establish persistent connections, start interactive sessions, and run scripts on remote computers.</span></span>

<span data-ttu-id="2cc8a-130">Windows PowerShell távoli eljáráshívás használatához konfigurálni kell a távoli számítógép távoli felügyeletére.</span><span class="sxs-lookup"><span data-stu-id="2cc8a-130">To use Windows PowerShell remoting, the remote computer must be configured for remote management.</span></span>
<span data-ttu-id="2cc8a-131">További információt, többek között az utasításokért lásd: [távoli követelmények](/powershell/module/microsoft.powershell.core/about/about_remote_requirements).</span><span class="sxs-lookup"><span data-stu-id="2cc8a-131">For more information, including instructions, see [About Remote Requirements](/powershell/module/microsoft.powershell.core/about/about_remote_requirements).</span></span>

<span data-ttu-id="2cc8a-132">Miután konfigurálta a Windows PowerShell-táveléréssel, sok távoli eljáráshívás stratégiák lesznek elérhetők.</span><span class="sxs-lookup"><span data-stu-id="2cc8a-132">Once you have configured Windows PowerShell remoting, many remoting strategies are available to you.</span></span>
<span data-ttu-id="2cc8a-133">Ez a cikk ezek közül néhány sorolja fel.</span><span class="sxs-lookup"><span data-stu-id="2cc8a-133">This article lists just a few of them.</span></span> <span data-ttu-id="2cc8a-134">További információkért lásd: [kapcsolatos távoli](/powershell/module/microsoft.powershell.core/about/about_remote).</span><span class="sxs-lookup"><span data-stu-id="2cc8a-134">For more information, see [About Remote](/powershell/module/microsoft.powershell.core/about/about_remote).</span></span>

### <a name="start-an-interactive-session"></a><span data-ttu-id="2cc8a-135">Az interaktív munkamenet indítása</span><span class="sxs-lookup"><span data-stu-id="2cc8a-135">Start an Interactive Session</span></span>

<span data-ttu-id="2cc8a-136">Az interaktív munkamenet indításához és a egy távoli számítógépen használja a [Enter-PSSession](/powershell/module/microsoft.powershell.core/enter-pssession) parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="2cc8a-136">To start an interactive session with a single remote computer, use the [Enter-PSSession](/powershell/module/microsoft.powershell.core/enter-pssession) cmdlet.</span></span>
<span data-ttu-id="2cc8a-137">Írja be például a kiszolgalo01 távoli számítógépekkel az interaktív munkamenet indításához:</span><span class="sxs-lookup"><span data-stu-id="2cc8a-137">For example, to start an interactive session with the Server01 remote computer, type:</span></span>

```powershell
Enter-PSSession Server01
```

<span data-ttu-id="2cc8a-138">A parancssor megváltozik a távoli számítógép neve jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="2cc8a-138">The command prompt changes to display the name of the remote computer.</span></span> <span data-ttu-id="2cc8a-139">Minden olyan parancsokat, amelyek a parancssorba írja be a távoli számítógépen futtatja, és az eredmények jelennek meg a helyi számítógépen.</span><span class="sxs-lookup"><span data-stu-id="2cc8a-139">Any commands that you type at the prompt run on the remote computer and the results are displayed on the local computer.</span></span>

<span data-ttu-id="2cc8a-140">Az interaktív munkamenet befejezéséhez írja be:</span><span class="sxs-lookup"><span data-stu-id="2cc8a-140">To end the interactive session, type:</span></span>

```powershell
Exit-PSSession
```

<span data-ttu-id="2cc8a-141">Enter-PSSession és kilépési-PSSession-parancsmagokkal kapcsolatos további információkért lásd:</span><span class="sxs-lookup"><span data-stu-id="2cc8a-141">For more information about the Enter-PSSession and Exit-PSSession cmdlets, see:</span></span>

- [<span data-ttu-id="2cc8a-142">Enter-PSSession</span><span class="sxs-lookup"><span data-stu-id="2cc8a-142">Enter-PSSession</span></span>](/powershell/module/microsoft.powershell.core/enter-pssession)
- [<span data-ttu-id="2cc8a-143">Kilépés-PSSession</span><span class="sxs-lookup"><span data-stu-id="2cc8a-143">Exit-PSSession</span></span>](/powershell/module/microsoft.powershell.core/exit-pssession)

### <a name="run-a-remote-command"></a><span data-ttu-id="2cc8a-144">Távoli parancs futtatása</span><span class="sxs-lookup"><span data-stu-id="2cc8a-144">Run a Remote Command</span></span>

<span data-ttu-id="2cc8a-145">Egy vagy több számítógépet a parancs futtatásához használja a [Invoke-Command](/powershell/module/microsoft.powershell.core/invoke-command) parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="2cc8a-145">To run a command on one or more computers, use the [Invoke-Command](/powershell/module/microsoft.powershell.core/invoke-command) cmdlet.</span></span> <span data-ttu-id="2cc8a-146">Futtassa például egy [Get-UICulture](/powershell/module/microsoft.powershell.utility/get-uiculture) parancsot a kiszolgalo01 és Server02 távoli számítógépeken, írja be:</span><span class="sxs-lookup"><span data-stu-id="2cc8a-146">For example, to run a [Get-UICulture](/powershell/module/microsoft.powershell.utility/get-uiculture) command on the Server01 and Server02 remote computers, type:</span></span>

```powershell
Invoke-Command -ComputerName Server01, Server02 -ScriptBlock {Get-UICulture}
```

<span data-ttu-id="2cc8a-147">A kimenetet visszaadja a számítógépen.</span><span class="sxs-lookup"><span data-stu-id="2cc8a-147">The output is returned to your computer.</span></span>

```output
LCID    Name     DisplayName               PSComputerName
----    ----     -----------               --------------
1033    en-US    English (United States)   server01.corp.fabrikam.com
1033    en-US    English (United States)   server02.corp.fabrikam.com
```

### <a name="run-a-script"></a><span data-ttu-id="2cc8a-148">Parancsfájl futtatása</span><span class="sxs-lookup"><span data-stu-id="2cc8a-148">Run a Script</span></span>

<span data-ttu-id="2cc8a-149">Parancsfájl futtatása egy vagy több távoli számítógépeken használja a fájl elérési útja paramétert, a `Invoke-Command` parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="2cc8a-149">To run a script on one or many remote computers, use the FilePath parameter of the `Invoke-Command` cmdlet.</span></span> <span data-ttu-id="2cc8a-150">A parancsfájl vagy elérhető-e a helyi számítógépen kell lennie.</span><span class="sxs-lookup"><span data-stu-id="2cc8a-150">The script must be on or accessible to your local computer.</span></span> <span data-ttu-id="2cc8a-151">Az eredmény a helyi számítógépen.</span><span class="sxs-lookup"><span data-stu-id="2cc8a-151">The results are returned to your local computer.</span></span>

<span data-ttu-id="2cc8a-152">Ha például a következő parancsot a DiskCollect.ps1 szkriptet futtat a távoli számítógépek kiszolgalo01 és Server02.</span><span class="sxs-lookup"><span data-stu-id="2cc8a-152">For example, the following command runs the DiskCollect.ps1 script on the remote computers, Server01 and Server02.</span></span>

```powershell
Invoke-Command -ComputerName Server01, Server02 -FilePath c:\Scripts\DiskCollect.ps1
```

### <a name="establish-a-persistent-connection"></a><span data-ttu-id="2cc8a-153">Állandó kapcsolatot létesíteni</span><span class="sxs-lookup"><span data-stu-id="2cc8a-153">Establish a Persistent Connection</span></span>

<span data-ttu-id="2cc8a-154">Használja a `New-PSSession` parancsmaggal hozzon létre egy állandó munkamenetet egy távoli számítógépen.</span><span class="sxs-lookup"><span data-stu-id="2cc8a-154">Use the `New-PSSession` cmdlet to create a persistent session on a remote computer.</span></span> <span data-ttu-id="2cc8a-155">A következő példa távoli munkamenetek kiszolgalo01 és Server02 hoz létre.</span><span class="sxs-lookup"><span data-stu-id="2cc8a-155">The following example creates remote sessions on Server01 and Server02.</span></span> <span data-ttu-id="2cc8a-156">A munkamenet-objektumok vannak tárolva a `$s` változó.</span><span class="sxs-lookup"><span data-stu-id="2cc8a-156">The session objects are stored in the `$s` variable.</span></span>

```powershell
$s = New-PSSession -ComputerName Server01, Server02
```

<span data-ttu-id="2cc8a-157">Most, hogy a munkamenet jött létre, bármely parancsot futtathatja bennük.</span><span class="sxs-lookup"><span data-stu-id="2cc8a-157">Now that the sessions are established, you can run any command in them.</span></span> <span data-ttu-id="2cc8a-158">És mivel a munkamenet tartós, egy parancs adatokat gyűjteni, és azokat a egy másik parancs használja.</span><span class="sxs-lookup"><span data-stu-id="2cc8a-158">And because the sessions are persistent, you can collect data from one command and use it in another command.</span></span>

<span data-ttu-id="2cc8a-159">Például a következő parancsot a Get-HotFix parancsot futtatja, a foglalkozások a $s változóban, és az eredmények $h változóba menti.</span><span class="sxs-lookup"><span data-stu-id="2cc8a-159">For example, the following command runs a Get-HotFix command in the sessions in the $s variable and it saves the results in the $h variable.</span></span> <span data-ttu-id="2cc8a-160">A $h változó jön létre az egyes $s munkamenetekben, de a helyi munkamenet nem létezik.</span><span class="sxs-lookup"><span data-stu-id="2cc8a-160">The $h variable is created in each of the sessions in $s, but it doesn't exist in the local session.</span></span>

```powershell
Invoke-Command -Session $s {$h = Get-HotFix}
```

<span data-ttu-id="2cc8a-161">Most már használhatja az adatok a `$h` változó más parancsokkal ugyanabban a munkamenetben.</span><span class="sxs-lookup"><span data-stu-id="2cc8a-161">Now you can use the data in the `$h` variable with other commands in the same session.</span></span> <span data-ttu-id="2cc8a-162">Az eredmények jelennek meg a helyi számítógépen.</span><span class="sxs-lookup"><span data-stu-id="2cc8a-162">The results are displayed on the local computer.</span></span> <span data-ttu-id="2cc8a-163">Például:</span><span class="sxs-lookup"><span data-stu-id="2cc8a-163">For example:</span></span>

```powershell
Invoke-Command -Session $s {$h | where {$_.InstalledBy -ne "NTAUTHORITY\SYSTEM"}}
```

### <a name="advanced-remoting"></a><span data-ttu-id="2cc8a-164">Speciális távelérés</span><span class="sxs-lookup"><span data-stu-id="2cc8a-164">Advanced Remoting</span></span>

<span data-ttu-id="2cc8a-165">Windows PowerShell távoli felügyeleti csak itt kezdődik.</span><span class="sxs-lookup"><span data-stu-id="2cc8a-165">Windows PowerShell remote management just begins here.</span></span> <span data-ttu-id="2cc8a-166">A Windows PowerShell használatával telepített parancsmagokat használatával is létrehozni, valamint mindkét távoli munkamenetek a helyi és távoli véget ér, a hozzon létre személyre szabott és korlátozott munkamenet engedélyezése a felhasználóknak parancsok importálhat egy távoli munkamenetet, amely futtatja ténylegesen implicit módon a távoli munkamenetet a távoli munkamenetet, és még sok más biztonságát konfigurálja.</span><span class="sxs-lookup"><span data-stu-id="2cc8a-166">By using the cmdlets installed with Windows PowerShell, you can establish and configure remote sessions both from the local and remote ends, create customized and restricted sessions, allow users to import commands from a remote session that actually run implicitly on the remote session, configure the security of a remote session, and much more.</span></span>

<span data-ttu-id="2cc8a-167">Windows PowerShell a wsman által használt szolgáltatót tartalmaz.</span><span class="sxs-lookup"><span data-stu-id="2cc8a-167">Windows PowerShell includes a WSMan provider.</span></span> <span data-ttu-id="2cc8a-168">A szolgáltató létrehoz egy `WSMAN:` meghajtó, amely lehetővé teszi a hierarchiájában a konfigurációs beállításokat a helyi számítógépen, és a távoli számítógépek közötti navigáláshoz.</span><span class="sxs-lookup"><span data-stu-id="2cc8a-168">The provider creates a `WSMAN:` drive that lets you navigate through a hierarchy of configuration settings on the local computer and remote computers.</span></span>

<span data-ttu-id="2cc8a-169">A wsman által használt szolgáltató kapcsolatos további információkért lásd: [WSMan szolgáltató](https://technet.microsoft.com/library/dd819476.aspx) és [WS-Management-parancsmagok](/powershell/module/microsoft.powershell.core/about/about_ws-management_cmdlets), vagy írja be a Windows PowerShell-konzol `Get-Help wsman`.</span><span class="sxs-lookup"><span data-stu-id="2cc8a-169">For more information about the WSMan provider, see [WSMan Provider](https://technet.microsoft.com/library/dd819476.aspx) and [About WS-Management Cmdlets](/powershell/module/microsoft.powershell.core/about/about_ws-management_cmdlets), or in the Windows PowerShell console, type `Get-Help wsman`.</span></span>

<span data-ttu-id="2cc8a-170">További információ:</span><span class="sxs-lookup"><span data-stu-id="2cc8a-170">For more information, see:</span></span>

- [<span data-ttu-id="2cc8a-171">Tudnivalók a távoli – gyakori kérdések</span><span class="sxs-lookup"><span data-stu-id="2cc8a-171">About Remote FAQ</span></span>](https://technet.microsoft.com/library/dd315359.aspx)
- [<span data-ttu-id="2cc8a-172">Register-PSSessionConfiguration</span><span class="sxs-lookup"><span data-stu-id="2cc8a-172">Register-PSSessionConfiguration</span></span>](https://go.microsoft.com/fwlink/?LinkId=821508)
- [<span data-ttu-id="2cc8a-173">Import-PSSession</span><span class="sxs-lookup"><span data-stu-id="2cc8a-173">Import-PSSession</span></span>](https://go.microsoft.com/fwlink/?LinkId=821821)

<span data-ttu-id="2cc8a-174">Távoli eljáráshívás hibákkal kapcsolatos útmutatásért lásd: [about_Remote_Troubleshooting](https://technet.microsoft.com/library/dd347642.aspx).</span><span class="sxs-lookup"><span data-stu-id="2cc8a-174">For help with remoting errors, see [about_Remote_Troubleshooting](https://technet.microsoft.com/library/dd347642.aspx).</span></span>

## <a name="see-also"></a><span data-ttu-id="2cc8a-175">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="2cc8a-175">See Also</span></span>

- [<span data-ttu-id="2cc8a-176">about_Remote</span><span class="sxs-lookup"><span data-stu-id="2cc8a-176">about_Remote</span></span>](https://technet.microsoft.com/library/9b4a5c87-9162-4adf-bdfe-fbc80b9b8970)
- [<span data-ttu-id="2cc8a-177">about_Remote_FAQ</span><span class="sxs-lookup"><span data-stu-id="2cc8a-177">about_Remote_FAQ</span></span>](https://technet.microsoft.com/library/e23702fd-9415-4a98-9975-390a4d3adc42)
- [<span data-ttu-id="2cc8a-178">távelérés követelményeivel foglalkozó cikkben</span><span class="sxs-lookup"><span data-stu-id="2cc8a-178">about_Remote_Requirements</span></span>](https://technet.microsoft.com/library/da213949-134c-4741-b307-81f4492ba1bd)
- [<span data-ttu-id="2cc8a-179">about_Remote_Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="2cc8a-179">about_Remote_Troubleshooting</span></span>](https://technet.microsoft.com/library/2f890148-8578-49ed-85ea-79a489dd6317)
- [<span data-ttu-id="2cc8a-180">about_PSSessions</span><span class="sxs-lookup"><span data-stu-id="2cc8a-180">about_PSSessions</span></span>](https://technet.microsoft.com/library/7a9b4e0e-fa1b-47b0-92f6-6e2995d70acb)
- [<span data-ttu-id="2cc8a-181">about_WS-Management_Cmdlets</span><span class="sxs-lookup"><span data-stu-id="2cc8a-181">about_WS-Management_Cmdlets</span></span>](https://technet.microsoft.com/library/6ed3370a-ea10-45a5-9493-696aeace27ed)
- [<span data-ttu-id="2cc8a-182">Invoke-Command</span><span class="sxs-lookup"><span data-stu-id="2cc8a-182">Invoke-Command</span></span>](/powershell/module/microsoft.powershell.core/invoke-command)
- [<span data-ttu-id="2cc8a-183">Import-PSSession</span><span class="sxs-lookup"><span data-stu-id="2cc8a-183">Import-PSSession</span></span>](https://go.microsoft.com/fwlink/?LinkId=821821)
- [<span data-ttu-id="2cc8a-184">New-PSSession</span><span class="sxs-lookup"><span data-stu-id="2cc8a-184">New-PSSession</span></span>](https://go.microsoft.com/fwlink/?LinkId=821498)
- [<span data-ttu-id="2cc8a-185">Register-PSSessionConfiguration</span><span class="sxs-lookup"><span data-stu-id="2cc8a-185">Register-PSSessionConfiguration</span></span>](https://go.microsoft.com/fwlink/?LinkId=821508)
- [<span data-ttu-id="2cc8a-186">A WSMan-szolgáltató</span><span class="sxs-lookup"><span data-stu-id="2cc8a-186">WSMan Provider</span></span>](https://technet.microsoft.com/library/66fe1241-e08f-49ca-832f-a84c33ca8735)

[wsman-remoting]: WSMan-Remoting-in-PowerShell-Core.md
[ssh-remoting]: SSH-Remoting-in-PowerShell-Core.md