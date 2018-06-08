---
ms.date: 06/05/2017
keywords: PowerShell parancsmag
title: Távoli parancsok futtatása
ms.assetid: d6938b56-7dc8-44ba-b4d4-cd7b169fd74d
ms.openlocfilehash: d21d1def1e25895f65b3578bf2892d56f14cc150
ms.sourcegitcommit: 01d6985ed190a222e9da1da41596f524f607a5bc
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/07/2018
ms.locfileid: "34482879"
---
# <a name="running-remote-commands"></a><span data-ttu-id="9974e-103">Távoli parancsok futtatása</span><span class="sxs-lookup"><span data-stu-id="9974e-103">Running Remote Commands</span></span>

<span data-ttu-id="9974e-104">A parancsokat egy vagy több száz számítógép egyetlen Windows PowerShell-parancsot.</span><span class="sxs-lookup"><span data-stu-id="9974e-104">You can run commands on one or hundreds of computers with a single Windows PowerShell command.</span></span> <span data-ttu-id="9974e-105">A Windows PowerShell támogatja a távoli számítási különböző technológiákkal, például WMI, RPC és WS-Management használatával.</span><span class="sxs-lookup"><span data-stu-id="9974e-105">Windows PowerShell supports remote computing by using various technologies, including WMI, RPC, and WS-Management.</span></span>

## <a name="remoting-in-powershell-core"></a><span data-ttu-id="9974e-106">A PowerShell Core távelérése</span><span class="sxs-lookup"><span data-stu-id="9974e-106">Remoting in PowerShell Core</span></span>

<span data-ttu-id="9974e-107">PowerShell mag, a Windows, a macOS és a Linux, PowerShell újabb kiadása támogatja a WMI, WS-Management és az SSH távelérése.</span><span class="sxs-lookup"><span data-stu-id="9974e-107">PowerShell Core, the newer edition of PowerShell on Windows, macOS, and Linux, supports WMI, WS-Management, and SSH remoting.</span></span>
<span data-ttu-id="9974e-108">(RPC már nem támogatott.)</span><span class="sxs-lookup"><span data-stu-id="9974e-108">(RPC is no longer supported.)</span></span>

<span data-ttu-id="9974e-109">Ez beállításával kapcsolatos további információkért lásd:</span><span class="sxs-lookup"><span data-stu-id="9974e-109">For more information on setting this up, see:</span></span>

* <span data-ttu-id="9974e-110">[SSH PowerShell Core a távoli eljáráshívás][ssh-remoting]</span><span class="sxs-lookup"><span data-stu-id="9974e-110">[SSH Remoting in PowerShell Core][ssh-remoting]</span></span>
* <span data-ttu-id="9974e-111">[A PowerShell Core WSMan távelérése][wsman-remoting]</span><span class="sxs-lookup"><span data-stu-id="9974e-111">[WSMan Remoting in PowerShell Core][wsman-remoting]</span></span>

## <a name="remoting-without-configuration"></a><span data-ttu-id="9974e-112">Távelérési konfiguráció nélkül</span><span class="sxs-lookup"><span data-stu-id="9974e-112">Remoting Without Configuration</span></span>

<span data-ttu-id="9974e-113">Számos Windows PowerShell-parancsmagok a ComputerName paraméterre, amely lehetővé teszi az adatok gyűjtéséhez és módosíthatja a beállításokat egy vagy több távoli számítógépeken van.</span><span class="sxs-lookup"><span data-stu-id="9974e-113">Many Windows PowerShell cmdlets have the ComputerName parameter that enables you to collect data and change settings on one or more remote computers.</span></span> <span data-ttu-id="9974e-114">Számos különböző kommunikációs technológiák és számos munkahelyi használata az összes Windows operációs rendszeren, amely a Windows PowerShell támogatja a Speciális konfiguráció nélkül.</span><span class="sxs-lookup"><span data-stu-id="9974e-114">They use a variety of communication technologies and many work on all Windows operating systems that Windows PowerShell supports without any special configuration.</span></span>

<span data-ttu-id="9974e-115">Ezek a parancsmagok a következők:</span><span class="sxs-lookup"><span data-stu-id="9974e-115">These cmdlets include:</span></span>

* [<span data-ttu-id="9974e-116">Indítsa újra a számítógépet</span><span class="sxs-lookup"><span data-stu-id="9974e-116">Restart-Computer</span></span>](https://go.microsoft.com/fwlink/?LinkId=821625)
* [<span data-ttu-id="9974e-117">Test-Connection</span><span class="sxs-lookup"><span data-stu-id="9974e-117">Test-Connection</span></span>](https://go.microsoft.com/fwlink/?LinkId=821646)
* [<span data-ttu-id="9974e-118">Az eseménynaplóban törlése</span><span class="sxs-lookup"><span data-stu-id="9974e-118">Clear-EventLog</span></span>](https://go.microsoft.com/fwlink/?LinkId=821568)
* [<span data-ttu-id="9974e-119">Get-EventLog</span><span class="sxs-lookup"><span data-stu-id="9974e-119">Get-EventLog</span></span>](https://go.microsoft.com/fwlink/?LinkId=821585)
* [<span data-ttu-id="9974e-120">Get-HotFix</span><span class="sxs-lookup"><span data-stu-id="9974e-120">Get-HotFix</span></span>](https://go.microsoft.com/fwlink/?LinkId=821586)
* [<span data-ttu-id="9974e-121">Get-Process</span><span class="sxs-lookup"><span data-stu-id="9974e-121">Get-Process</span></span>](https://go.microsoft.com/fwlink/?linkid=821590)
* [<span data-ttu-id="9974e-122">Get-Service</span><span class="sxs-lookup"><span data-stu-id="9974e-122">Get-Service</span></span>](https://go.microsoft.com/fwlink/?LinkId=821593)
* [<span data-ttu-id="9974e-123">Set-Service</span><span class="sxs-lookup"><span data-stu-id="9974e-123">Set-Service</span></span>](https://go.microsoft.com/fwlink/?LinkId=821633)
* [<span data-ttu-id="9974e-124">Get-WinEvent</span><span class="sxs-lookup"><span data-stu-id="9974e-124">Get-WinEvent</span></span>](https://go.microsoft.com/fwlink/?linkid=821529)
* [<span data-ttu-id="9974e-125">Get-WmiObject</span><span class="sxs-lookup"><span data-stu-id="9974e-125">Get-WmiObject</span></span>](https://go.microsoft.com/fwlink/?LinkId=821595)

<span data-ttu-id="9974e-126">Speciális konfiguráció nélkül távelérése támogató parancsmagok általában a ComputerName paraméterrel, és a munkamenet-paraméter nem rendelkezik.</span><span class="sxs-lookup"><span data-stu-id="9974e-126">Typically, cmdlets that support remoting without special configuration have the ComputerName parameter and do not have the Session parameter.</span></span> <span data-ttu-id="9974e-127">Ezeket a parancsmagokat a munkamenetben, írja be:</span><span class="sxs-lookup"><span data-stu-id="9974e-127">To find these cmdlets in your session, type:</span></span>

```powershell
Get-Command | where { $_.parameters.keys -contains "ComputerName" -and $_.parameters.keys -notcontains "Session"}
```

## <a name="windows-powershell-remoting"></a><span data-ttu-id="9974e-128">A Windows PowerShell-távelérés</span><span class="sxs-lookup"><span data-stu-id="9974e-128">Windows PowerShell Remoting</span></span>

<span data-ttu-id="9974e-129">A Windows PowerShell-távelérést, a WS-Management protokollt használja, amely lehetővé teszi, hogy egy vagy több távoli számítógépeken bármely Windows PowerShell-parancs futtatása.</span><span class="sxs-lookup"><span data-stu-id="9974e-129">Windows PowerShell remoting, which uses the WS-Management protocol, lets you run any Windows PowerShell command on one or many remote computers.</span></span> <span data-ttu-id="9974e-130">Lehetővé teszi az állandó kapcsolatot létrehozni, 1:1 interaktív munkamenetek indításához és parancsfájlok futtatása több számítógépen.</span><span class="sxs-lookup"><span data-stu-id="9974e-130">It lets you establish persistent connections, start 1:1 interactive sessions, and run scripts on multiple computers.</span></span>

<span data-ttu-id="9974e-131">A Windows PowerShell távoli eljáráshívás használatához a távoli számítógép távoli kezelési be kell állítani.</span><span class="sxs-lookup"><span data-stu-id="9974e-131">To use Windows PowerShell remoting, the remote computer must be configured for remote management.</span></span> <span data-ttu-id="9974e-132">További információt, beleértve az utasításokat, lásd: [távoli követelmények](https://technet.microsoft.com/library/dd315349.aspx).</span><span class="sxs-lookup"><span data-stu-id="9974e-132">For more information, including instructions, see [About Remote Requirements](https://technet.microsoft.com/library/dd315349.aspx).</span></span>

<span data-ttu-id="9974e-133">Miután konfigurálta a Windows PowerShell-távelérést, sok távelérési stratégia a következő elérhető.</span><span class="sxs-lookup"><span data-stu-id="9974e-133">After you have configured Windows PowerShell remoting, many remoting strategies are available to you.</span></span> <span data-ttu-id="9974e-134">Ez a dokumentum tovább részében csak néhány őket a sorolja fel.</span><span class="sxs-lookup"><span data-stu-id="9974e-134">The remainder of this document lists just a few of them.</span></span> <span data-ttu-id="9974e-135">További információkért lásd: [kapcsolatos távoli](https://technet.microsoft.com/library/dd347744.aspx) és [távoli GYIK](https://technet.microsoft.com/library/dd347744.aspx).</span><span class="sxs-lookup"><span data-stu-id="9974e-135">For more information, see [About Remote](https://technet.microsoft.com/library/dd347744.aspx) and [About Remote FAQ](https://technet.microsoft.com/library/dd347744.aspx).</span></span>

### <a name="start-an-interactive-session"></a><span data-ttu-id="9974e-136">Egy interaktív munkamenet indítása</span><span class="sxs-lookup"><span data-stu-id="9974e-136">Start an Interactive Session</span></span>

<span data-ttu-id="9974e-137">Egy távoli számítógéppel egy interaktív munkamenet indításához használja a [Enter-PSSession](https://go.microsoft.com/fwlink/?LinkId=821477) parancsmag.</span><span class="sxs-lookup"><span data-stu-id="9974e-137">To start an interactive session with a single remote computer, use the [Enter-PSSession](https://go.microsoft.com/fwlink/?LinkId=821477) cmdlet.</span></span>
<span data-ttu-id="9974e-138">Például a kiszolgalo01 távoli számítógéppel egy interaktív munkamenet elindításához írja be:</span><span class="sxs-lookup"><span data-stu-id="9974e-138">For example, to start an interactive session with the Server01 remote computer, type:</span></span>

```powershell
Enter-PSSession Server01
```

<span data-ttu-id="9974e-139">A parancssor módosításai jeleníti meg, amely csatlakozik a számítógép nevét.</span><span class="sxs-lookup"><span data-stu-id="9974e-139">The command prompt changes to display the name of the computer to which you are connected.</span></span> <span data-ttu-id="9974e-140">Ettől a távoli számítógépen futó parancsok, amely parancssorába írja be, és az eredmények jelennek meg a helyi számítógépen.</span><span class="sxs-lookup"><span data-stu-id="9974e-140">From then on, any commands that you type at the prompt run on the remote computer and the results are displayed on the local computer.</span></span>

<span data-ttu-id="9974e-141">Az interaktív munkamenet befejezéséhez írja be:</span><span class="sxs-lookup"><span data-stu-id="9974e-141">To end the interactive session, type:</span></span>

```powershell
Exit-PSSession
```

<span data-ttu-id="9974e-142">A Enter-PSSession és kilépési-PSSession parancsmag kapcsolatos további információkért lásd: [Enter-PSSession](https://go.microsoft.com/fwlink/?LinkId=821477) és [kilépési-PSSession](https://go.microsoft.com/fwlink/?LinkID=821478).</span><span class="sxs-lookup"><span data-stu-id="9974e-142">For more information about the Enter-PSSession and Exit-PSSession cmdlets, see [Enter-PSSession](https://go.microsoft.com/fwlink/?LinkId=821477) and [Exit-PSSession](https://go.microsoft.com/fwlink/?LinkID=821478).</span></span>

### <a name="run-a-remote-command"></a><span data-ttu-id="9974e-143">Távoli parancs futtatása</span><span class="sxs-lookup"><span data-stu-id="9974e-143">Run a Remote Command</span></span>

<span data-ttu-id="9974e-144">Egy vagy több távoli számítógépeken bármely parancs futtatásához használja a [Invoke-Command](https://go.microsoft.com/fwlink/?LinkId=821493) parancsmag.</span><span class="sxs-lookup"><span data-stu-id="9974e-144">To run any command on one or many remote computers, use the [Invoke-Command](https://go.microsoft.com/fwlink/?LinkId=821493) cmdlet.</span></span>
<span data-ttu-id="9974e-145">Ahhoz például, hogy futtassa egy [Get-UICulture](https://go.microsoft.com/fwlink/?LinkId=821806) parancsot a kiszolgalo01 és Server02 távoli számítógépeken, típus:</span><span class="sxs-lookup"><span data-stu-id="9974e-145">For example, to run a [Get-UICulture](https://go.microsoft.com/fwlink/?LinkId=821806) command on the Server01 and Server02 remote computers, type:</span></span>

```powershell
Invoke-Command -ComputerName Server01, Server02 -ScriptBlock {Get-UICulture}
```

<span data-ttu-id="9974e-146">A kimenetet visszaadja a számítógépre.</span><span class="sxs-lookup"><span data-stu-id="9974e-146">The output is returned to your computer.</span></span>

```output
LCID    Name     DisplayName               PSComputerName
----    ----     -----------               --------------
1033    en-US    English (United States)   server01.corp.fabrikam.com
1033    en-US    English (United States)   server02.corp.fabrikam.com
```

<span data-ttu-id="9974e-147">Az Invoke-Command parancsmaggal kapcsolatos további információkért lásd: [Invoke-Command](https://go.microsoft.com/fwlink/?LinkId=821493).</span><span class="sxs-lookup"><span data-stu-id="9974e-147">For more information about the Invoke-Command cmdlet, see [Invoke-Command](https://go.microsoft.com/fwlink/?LinkId=821493).</span></span>

### <a name="run-a-script"></a><span data-ttu-id="9974e-148">Parancsfájl futtatása</span><span class="sxs-lookup"><span data-stu-id="9974e-148">Run a Script</span></span>

<span data-ttu-id="9974e-149">Parancsprogram futtatása egy vagy több távoli számítógépet, használja az Invoke-Command parancsmaggal FilePath paraméterében.</span><span class="sxs-lookup"><span data-stu-id="9974e-149">To run a script on one or many remote computers, use the FilePath parameter of the Invoke-Command cmdlet.</span></span> <span data-ttu-id="9974e-150">A parancsfájl vagy a helyi számítógép által elérhető kell lennie.</span><span class="sxs-lookup"><span data-stu-id="9974e-150">The script must be on or accessible to your local computer.</span></span> <span data-ttu-id="9974e-151">Az eredmény akkor minősül, a helyi számítógépen.</span><span class="sxs-lookup"><span data-stu-id="9974e-151">The results are returned to your local computer.</span></span>

<span data-ttu-id="9974e-152">Például a következő parancsot a DiskCollect.ps1 parancsfájlt futtatja a kiszolgalo01 és Server02 távoli számítógépeken.</span><span class="sxs-lookup"><span data-stu-id="9974e-152">For example, the following command runs the DiskCollect.ps1 script on the Server01 and Server02 remote computers.</span></span>

```powershell
Invoke-Command -ComputerName Server01, Server02 -FilePath c:\Scripts\DiskCollect.ps1
```

<span data-ttu-id="9974e-153">Az Invoke-Command parancsmaggal kapcsolatos további információkért lásd: [Invoke-Command](https://go.microsoft.com/fwlink/?LinkId=821493).</span><span class="sxs-lookup"><span data-stu-id="9974e-153">For more information about the Invoke-Command cmdlet, see [Invoke-Command](https://go.microsoft.com/fwlink/?LinkId=821493).</span></span>

### <a name="establish-a-persistent-connection"></a><span data-ttu-id="9974e-154">Állandó kapcsolatot létesíteni</span><span class="sxs-lookup"><span data-stu-id="9974e-154">Establish a Persistent Connection</span></span>

<span data-ttu-id="9974e-155">Kapcsolódó parancsokat, amelyek közös adatok futtatásához hozzon létre egy munkamenetet a távoli számítógépen, és az Invoke-Command parancsmaggal futtassa a parancsokat az Ön által létrehozott munkamenetben.</span><span class="sxs-lookup"><span data-stu-id="9974e-155">To run a series of related commands that share data, create a session on the remote computer and then use the Invoke-Command cmdlet to run commands in the session that you create.</span></span> <span data-ttu-id="9974e-156">Távoli munkamenet létrehozása a New-PSSession parancsmag használható.</span><span class="sxs-lookup"><span data-stu-id="9974e-156">To create a remote session, use the New-PSSession cmdlet.</span></span>

<span data-ttu-id="9974e-157">Például a következő parancs létrehoz egy távoli munkamenet a kiszolgalo01 számítógépre és egy másik távoli munkamenet Server02 számítógépen.</span><span class="sxs-lookup"><span data-stu-id="9974e-157">For example, the following command creates a remote session on the Server01 computer and another remote session on the Server02 computer.</span></span> <span data-ttu-id="9974e-158">A munkamenet-objektumok a $s változóban menti.</span><span class="sxs-lookup"><span data-stu-id="9974e-158">It saves the session objects in the $s variable.</span></span>

```powershell
$s = New-PSSession -ComputerName Server01, Server02
```

<span data-ttu-id="9974e-159">Most, hogy a munkamenet jött létre, bennük valamelyik parancsának is futtathatja.</span><span class="sxs-lookup"><span data-stu-id="9974e-159">Now that the sessions are established, you can run any command in them.</span></span> <span data-ttu-id="9974e-160">És a munkameneteket állandó, mert egy parancs az adatgyűjtés, és a következő parancsot használhatja.</span><span class="sxs-lookup"><span data-stu-id="9974e-160">And because the sessions are persistent, you can collect data in one command and use it in a subsequent command.</span></span>

<span data-ttu-id="9974e-161">Például a következő parancsot a Get-gyorsjavítás parancsot futtatja, a $s változóban munkamenetekben, és az eredményeket a $h változóban menti.</span><span class="sxs-lookup"><span data-stu-id="9974e-161">For example, the following command runs a Get-HotFix command in the sessions in the $s variable and it saves the results in the $h variable.</span></span> <span data-ttu-id="9974e-162">A $h változó minden $s munkamenetekben létrejött, de nem létezik a helyi munkamenetben.</span><span class="sxs-lookup"><span data-stu-id="9974e-162">The $h variable is created in each of the sessions in $s, but it does not exist in the local session.</span></span>

```powershell
Invoke-Command -Session $s {$h = Get-HotFix}
```

<span data-ttu-id="9974e-163">Most már használhatja az adatokat a következő parancsok, például a következő $h változót.</span><span class="sxs-lookup"><span data-stu-id="9974e-163">Now you can use the data in the $h variable in subsequent commands, such as the following one.</span></span> <span data-ttu-id="9974e-164">Az eredmények jelennek meg a helyi számítógépen.</span><span class="sxs-lookup"><span data-stu-id="9974e-164">The results are displayed on the local computer.</span></span>

```powershell
Invoke-Command -Session $s {$h | where {$_.InstalledBy -ne "NTAUTHORITY\SYSTEM"}}
```

### <a name="advanced-remoting"></a><span data-ttu-id="9974e-165">Speciális távelérés</span><span class="sxs-lookup"><span data-stu-id="9974e-165">Advanced Remoting</span></span>

<span data-ttu-id="9974e-166">A Windows PowerShell távoli felügyeleti csak itt kezdődik.</span><span class="sxs-lookup"><span data-stu-id="9974e-166">Windows PowerShell remote management just begins here.</span></span> <span data-ttu-id="9974e-167">A telepített Windows PowerShell parancsmagok segítségével létrehozása és konfigurálása mindkét távoli munkamenetek a helyi és távoli véget ér, a testre szabott és korlátozott-munkameneteket hozzon létre engedélyezése a felhasználók parancsok importálása egy távoli munkamenetet, amely futtatja ténylegesen implicit módon adja meg a távoli munkamenet azt a távoli munkamenetet, és még sok más biztonságát.</span><span class="sxs-lookup"><span data-stu-id="9974e-167">By using the cmdlets installed with Windows PowerShell, you can establish and configure remote sessions both from the local and remote ends, create customized and restricted sessions, allow users to import commands from a remote session that actually run implicitly on the remote session, configure the security of a remote session, and much more.</span></span>

<span data-ttu-id="9974e-168">Lehetővé teszi a távoli konfiguráció, a Windows PowerShell a WSMan-szolgáltató foglal magában.</span><span class="sxs-lookup"><span data-stu-id="9974e-168">To facilitate remote configuration, Windows PowerShell includes a WSMan provider.</span></span> <span data-ttu-id="9974e-169">A WSMAN: a meghajtó a szolgáltató által létrehozott lehetővé teszi haladjon végig a konfigurációs beállításokat a helyi számítógépen és a távoli számítógépek hierarchiáját.</span><span class="sxs-lookup"><span data-stu-id="9974e-169">The WSMAN: drive that the provider creates lets you navigate through a hierarchy of configuration settings on the local computer and remote computers.</span></span>
<span data-ttu-id="9974e-170">A WSMan-szolgáltató kapcsolatos további információkért lásd: [WSMan szolgáltató](https://technet.microsoft.com/library/dd819476.aspx) és [WS-Management parancsmagok](https://technet.microsoft.com/library/dd819481.aspx), vagy a Windows PowerShell-konzolban, írja be a "Get-Help wsman".</span><span class="sxs-lookup"><span data-stu-id="9974e-170">For more information about the WSMan provider, see  [WSMan Provider](https://technet.microsoft.com/library/dd819476.aspx) and [About WS-Management Cmdlets](https://technet.microsoft.com/library/dd819481.aspx), or in the Windows PowerShell console, type "Get-Help wsman".</span></span>

<span data-ttu-id="9974e-171">További információ:</span><span class="sxs-lookup"><span data-stu-id="9974e-171">For more information, see:</span></span>

- [<span data-ttu-id="9974e-172">Kapcsolatos távoli – gyakori kérdések</span><span class="sxs-lookup"><span data-stu-id="9974e-172">About Remote FAQ</span></span>](https://technet.microsoft.com/library/dd315359.aspx)
- [<span data-ttu-id="9974e-173">Register-PSSessionConfiguration</span><span class="sxs-lookup"><span data-stu-id="9974e-173">Register-PSSessionConfiguration</span></span>](https://go.microsoft.com/fwlink/?LinkId=821508)
- [<span data-ttu-id="9974e-174">Import-PSSession</span><span class="sxs-lookup"><span data-stu-id="9974e-174">Import-PSSession</span></span>](https://go.microsoft.com/fwlink/?LinkId=821821)

<span data-ttu-id="9974e-175">Távoli eljáráshívás hibákkal kapcsolatban lásd: [about_Remote_Troubleshooting](https://technet.microsoft.com/library/dd347642.aspx).</span><span class="sxs-lookup"><span data-stu-id="9974e-175">For help with remoting errors, see [about_Remote_Troubleshooting](https://technet.microsoft.com/library/dd347642.aspx).</span></span>

## <a name="see-also"></a><span data-ttu-id="9974e-176">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="9974e-176">See Also</span></span>

- [<span data-ttu-id="9974e-177">about_Remote</span><span class="sxs-lookup"><span data-stu-id="9974e-177">about_Remote</span></span>](https://technet.microsoft.com/library/9b4a5c87-9162-4adf-bdfe-fbc80b9b8970)
- [<span data-ttu-id="9974e-178">about_Remote_FAQ</span><span class="sxs-lookup"><span data-stu-id="9974e-178">about_Remote_FAQ</span></span>](https://technet.microsoft.com/library/e23702fd-9415-4a98-9975-390a4d3adc42)
- [<span data-ttu-id="9974e-179">about_Remote_Requirements</span><span class="sxs-lookup"><span data-stu-id="9974e-179">about_Remote_Requirements</span></span>](https://technet.microsoft.com/library/da213949-134c-4741-b307-81f4492ba1bd)
- [<span data-ttu-id="9974e-180">about_Remote_Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="9974e-180">about_Remote_Troubleshooting</span></span>](https://technet.microsoft.com/library/2f890148-8578-49ed-85ea-79a489dd6317)
- [<span data-ttu-id="9974e-181">about_PSSessions</span><span class="sxs-lookup"><span data-stu-id="9974e-181">about_PSSessions</span></span>](https://technet.microsoft.com/library/7a9b4e0e-fa1b-47b0-92f6-6e2995d70acb)
- [<span data-ttu-id="9974e-182">about_WS-Management_Cmdlets</span><span class="sxs-lookup"><span data-stu-id="9974e-182">about_WS-Management_Cmdlets</span></span>](https://technet.microsoft.com/library/6ed3370a-ea10-45a5-9493-696aeace27ed)
- [<span data-ttu-id="9974e-183">Invoke-Command parancsot</span><span class="sxs-lookup"><span data-stu-id="9974e-183">Invoke-Command</span></span>](https://go.microsoft.com/fwlink/?LinkId=821493)
- [<span data-ttu-id="9974e-184">Import-PSSession</span><span class="sxs-lookup"><span data-stu-id="9974e-184">Import-PSSession</span></span>](https://go.microsoft.com/fwlink/?LinkId=821821)
- [<span data-ttu-id="9974e-185">New-PSSession</span><span class="sxs-lookup"><span data-stu-id="9974e-185">New-PSSession</span></span>](https://go.microsoft.com/fwlink/?LinkId=821498)
- [<span data-ttu-id="9974e-186">Register-PSSessionConfiguration</span><span class="sxs-lookup"><span data-stu-id="9974e-186">Register-PSSessionConfiguration</span></span>](https://go.microsoft.com/fwlink/?LinkId=821508)
- [<span data-ttu-id="9974e-187">A WSMan-szolgáltató</span><span class="sxs-lookup"><span data-stu-id="9974e-187">WSMan Provider</span></span>](https://technet.microsoft.com/library/66fe1241-e08f-49ca-832f-a84c33ca8735)

[wsman-remoting]: WSMan-Remoting-in-PowerShell-Core.md
[ssh-remoting]: SSH-Remoting-in-PowerShell-Core.md