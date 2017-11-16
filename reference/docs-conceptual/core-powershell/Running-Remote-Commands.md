---
ms.date: 2017-06-05
keywords: PowerShell parancsmag
title: "Távoli parancsok futtatása"
ms.assetid: d6938b56-7dc8-44ba-b4d4-cd7b169fd74d
ms.openlocfilehash: 5cf9690b8fe4549a99186f172cb6f0de156a4dea
ms.sourcegitcommit: c5251755c4442487f99ff74fadf7e37bbf039089
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/18/2017
---
# <a name="running-remote-commands"></a><span data-ttu-id="d203d-103">Távoli parancsok futtatása</span><span class="sxs-lookup"><span data-stu-id="d203d-103">Running Remote Commands</span></span>
<span data-ttu-id="d203d-104">A parancsokat egy vagy több száz számítógép egyetlen Windows PowerShell-parancsot.</span><span class="sxs-lookup"><span data-stu-id="d203d-104">You can run commands on one or hundreds of computers with a single Windows PowerShell command.</span></span> <span data-ttu-id="d203d-105">A Windows PowerShell támogatja a távoli számítási különböző technológiákkal, például WMI, RPC és WS-Management használatával.</span><span class="sxs-lookup"><span data-stu-id="d203d-105">Windows PowerShell supports remote computing by using various technologies, including WMI, RPC, and WS-Management.</span></span>

## <a name="remoting-without-configuration"></a><span data-ttu-id="d203d-106">Távelérési konfiguráció nélkül</span><span class="sxs-lookup"><span data-stu-id="d203d-106">Remoting Without Configuration</span></span>
<span data-ttu-id="d203d-107">Számos Windows PowerShell-parancsmagok a ComputerName paraméterre, amely lehetővé teszi az adatok gyűjtéséhez és módosíthatja a beállításokat egy vagy több távoli számítógépeken van.</span><span class="sxs-lookup"><span data-stu-id="d203d-107">Many Windows PowerShell cmdlets have the ComputerName parameter that enables you to collect data and change settings on one or more remote computers.</span></span> <span data-ttu-id="d203d-108">Számos különböző kommunikációs technológiák és számos munkahelyi használata az összes Windows operációs rendszeren, amely a Windows PowerShell támogatja a Speciális konfiguráció nélkül.</span><span class="sxs-lookup"><span data-stu-id="d203d-108">They use a variety of communication technologies and many work on all Windows operating systems that Windows PowerShell supports without any special configuration.</span></span>

<span data-ttu-id="d203d-109">Ezek a parancsmagok a következők:</span><span class="sxs-lookup"><span data-stu-id="d203d-109">These cmdlets include:</span></span>
* [<span data-ttu-id="d203d-110">Indítsa újra a számítógépet</span><span class="sxs-lookup"><span data-stu-id="d203d-110">Restart-Computer</span></span>](https://go.microsoft.com/fwlink/?LinkId=821625)
* [<span data-ttu-id="d203d-111">Kapcsolat tesztelése</span><span class="sxs-lookup"><span data-stu-id="d203d-111">Test-Connection</span></span>](https://go.microsoft.com/fwlink/?LinkId=821646)
* [<span data-ttu-id="d203d-112">Az eseménynaplóban törlése</span><span class="sxs-lookup"><span data-stu-id="d203d-112">Clear-EventLog</span></span>](https://go.microsoft.com/fwlink/?LinkId=821568)
* [<span data-ttu-id="d203d-113">Get-Eseménynapló</span><span class="sxs-lookup"><span data-stu-id="d203d-113">Get-EventLog</span></span>](https://go.microsoft.com/fwlink/?LinkId=821585)
* [<span data-ttu-id="d203d-114">Get-gyorsjavítás</span><span class="sxs-lookup"><span data-stu-id="d203d-114">Get-HotFix</span></span>](https://go.microsoft.com/fwlink/?LinkId=821586)
  - [<span data-ttu-id="d203d-115">Get-Process</span><span class="sxs-lookup"><span data-stu-id="d203d-115">Get-Process</span></span>](https://go.microsoft.com/fwlink/?linkid=821590)
* [<span data-ttu-id="d203d-116">Get-szolgáltatás</span><span class="sxs-lookup"><span data-stu-id="d203d-116">Get-Service</span></span>](https://go.microsoft.com/fwlink/?LinkId=821593)
* [<span data-ttu-id="d203d-117">Szolgáltatás beállítása</span><span class="sxs-lookup"><span data-stu-id="d203d-117">Set-Service</span></span>](https://go.microsoft.com/fwlink/?LinkId=821633)
* [<span data-ttu-id="d203d-118">Get-WinEvent parancsmaggal</span><span class="sxs-lookup"><span data-stu-id="d203d-118">Get-WinEvent</span></span>](https://go.microsoft.com/fwlink/?linkid=821529)
* [<span data-ttu-id="d203d-119">Get-WmiObject</span><span class="sxs-lookup"><span data-stu-id="d203d-119">Get-WmiObject</span></span>](https://go.microsoft.com/fwlink/?LinkId=821595)

<span data-ttu-id="d203d-120">Speciális konfiguráció nélkül távelérése támogató parancsmagok általában a ComputerName paraméterrel, és a munkamenet-paraméter nem rendelkezik.</span><span class="sxs-lookup"><span data-stu-id="d203d-120">Typically, cmdlets that support remoting without special configuration have the ComputerName parameter and do not have the Session parameter.</span></span> <span data-ttu-id="d203d-121">Ezeket a parancsmagokat a munkamenetben, írja be:</span><span class="sxs-lookup"><span data-stu-id="d203d-121">To find these cmdlets in your session, type:</span></span>

```
Get-Command | where { $_.parameters.keys -contains "ComputerName" -and $_.parameters.keys -notcontains "Session"}
```

## <a name="windows-powershell-remoting"></a><span data-ttu-id="d203d-122">A Windows PowerShell-távelérés</span><span class="sxs-lookup"><span data-stu-id="d203d-122">Windows PowerShell Remoting</span></span>
<span data-ttu-id="d203d-123">A Windows PowerShell-távelérést, a WS-Management protokollt használja, amely lehetővé teszi, hogy egy vagy több távoli számítógépeken bármely Windows PowerShell-parancs futtatása.</span><span class="sxs-lookup"><span data-stu-id="d203d-123">Windows PowerShell remoting, which uses the WS-Management protocol, lets you run any Windows PowerShell command on one or many remote computers.</span></span> <span data-ttu-id="d203d-124">Lehetővé teszi az állandó kapcsolatot létrehozni, 1:1 interaktív munkamenetek indításához és parancsfájlok futtatása több számítógépen.</span><span class="sxs-lookup"><span data-stu-id="d203d-124">It lets you establish persistent connections, start 1:1 interactive sessions, and run scripts on multiple computers.</span></span>

<span data-ttu-id="d203d-125">A Windows PowerShell távoli eljáráshívás használatához a távoli számítógép távoli kezelési be kell állítani.</span><span class="sxs-lookup"><span data-stu-id="d203d-125">To use Windows PowerShell remoting, the remote computer must be configured for remote management.</span></span> <span data-ttu-id="d203d-126">További információt, beleértve az utasításokat, lásd: [távoli követelmények](https://technet.microsoft.com/en-us/library/dd315349.aspx).</span><span class="sxs-lookup"><span data-stu-id="d203d-126">For more information, including instructions, see [About Remote Requirements](https://technet.microsoft.com/en-us/library/dd315349.aspx).</span></span>

<span data-ttu-id="d203d-127">Miután konfigurálta a Windows PowerShell-távelérést, sok távelérési stratégia a következő elérhető.</span><span class="sxs-lookup"><span data-stu-id="d203d-127">After you have configured Windows PowerShell remoting, many remoting strategies are available to you.</span></span> <span data-ttu-id="d203d-128">Ez a dokumentum tovább részében csak néhány őket a sorolja fel.</span><span class="sxs-lookup"><span data-stu-id="d203d-128">The remainder of this document lists just a few of them.</span></span> <span data-ttu-id="d203d-129">További információkért lásd: [kapcsolatos távoli](https://technet.microsoft.com/en-us/library/dd347744.aspx) és [távoli GYIK](https://technet.microsoft.com/en-us/library/dd347744.aspx).</span><span class="sxs-lookup"><span data-stu-id="d203d-129">For more information, see [About Remote](https://technet.microsoft.com/en-us/library/dd347744.aspx) and [About Remote FAQ](https://technet.microsoft.com/en-us/library/dd347744.aspx).</span></span>

### <a name="start-an-interactive-session"></a><span data-ttu-id="d203d-130">Egy interaktív munkamenet indítása</span><span class="sxs-lookup"><span data-stu-id="d203d-130">Start an Interactive Session</span></span>
<span data-ttu-id="d203d-131">Egy távoli számítógéppel egy interaktív munkamenet indításához használja a [Enter-PSSession](https://go.microsoft.com/fwlink/?LinkId=821477) parancsmag.</span><span class="sxs-lookup"><span data-stu-id="d203d-131">To start an interactive session with a single remote computer, use the [Enter-PSSession](https://go.microsoft.com/fwlink/?LinkId=821477) cmdlet.</span></span>
<span data-ttu-id="d203d-132">Például a kiszolgalo01 távoli számítógéppel egy interaktív munkamenet elindításához írja be:</span><span class="sxs-lookup"><span data-stu-id="d203d-132">For example, to start an interactive session with the Server01 remote computer, type:</span></span>

```
Enter-PSSession Server01
```

<span data-ttu-id="d203d-133">A parancssor módosításai jeleníti meg, amely csatlakozik a számítógép nevét.</span><span class="sxs-lookup"><span data-stu-id="d203d-133">The command prompt changes to display the name of the computer to which you are connected.</span></span> <span data-ttu-id="d203d-134">Ettől a távoli számítógépen futó parancsok, amely parancssorába írja be, és az eredmények jelennek meg a helyi számítógépen.</span><span class="sxs-lookup"><span data-stu-id="d203d-134">From then on, any commands that you type at the prompt run on the remote computer and the results are displayed on the local computer.</span></span>

<span data-ttu-id="d203d-135">Az interaktív munkamenet befejezéséhez írja be:</span><span class="sxs-lookup"><span data-stu-id="d203d-135">To end the interactive session, type:</span></span>

```
Exit-PSSession
```

<span data-ttu-id="d203d-136">A Enter-PSSession és kilépési-PSSession parancsmag kapcsolatos további információkért lásd: [Enter-PSSession](https://go.microsoft.com/fwlink/?LinkId=821477) és [kilépési-PSSession](https://go.microsoft.com/fwlink/?LinkID=821478).</span><span class="sxs-lookup"><span data-stu-id="d203d-136">For more information about the Enter-PSSession and Exit-PSSession cmdlets, see [Enter-PSSession](https://go.microsoft.com/fwlink/?LinkId=821477) and [Exit-PSSession](https://go.microsoft.com/fwlink/?LinkID=821478).</span></span>

### <a name="run-a-remote-command"></a><span data-ttu-id="d203d-137">Távoli parancs futtatása</span><span class="sxs-lookup"><span data-stu-id="d203d-137">Run a Remote Command</span></span>
<span data-ttu-id="d203d-138">Egy vagy több távoli számítógépeken bármely parancs futtatásához használja a [Invoke-Command](https://go.microsoft.com/fwlink/?LinkId=821493) parancsmag.</span><span class="sxs-lookup"><span data-stu-id="d203d-138">To run any command on one or many remote computers, use the [Invoke-Command](https://go.microsoft.com/fwlink/?LinkId=821493) cmdlet.</span></span>
<span data-ttu-id="d203d-139">Ahhoz például, hogy futtassa egy [Get-UICulture](https://go.microsoft.com/fwlink/?LinkId=821806) parancsot a kiszolgalo01 és Server02 távoli számítógépeken, típus:</span><span class="sxs-lookup"><span data-stu-id="d203d-139">For example, to run a [Get-UICulture](https://go.microsoft.com/fwlink/?LinkId=821806) command on the Server01 and Server02 remote computers, type:</span></span>

```
Invoke-Command -ComputerName Server01, Server02 -ScriptBlock {Get-UICulture}
```

<span data-ttu-id="d203d-140">A kimenetet visszaadja a számítógépre.</span><span class="sxs-lookup"><span data-stu-id="d203d-140">The output is returned to your computer.</span></span>

```
LCID    Name     DisplayName               PSComputerName
----    ----     -----------               --------------
1033    en-US    English (United States)   server01.corp.fabrikam.com
1033    en-US    English (United States)   server02.corp.fabrikam.com
```
<span data-ttu-id="d203d-141">Az Invoke-Command parancsmaggal kapcsolatos további információkért lásd: [Invoke-Command](https://go.microsoft.com/fwlink/?LinkId=821493).</span><span class="sxs-lookup"><span data-stu-id="d203d-141">For more information about the Invoke-Command cmdlet, see [Invoke-Command](https://go.microsoft.com/fwlink/?LinkId=821493).</span></span>

### <a name="run-a-script"></a><span data-ttu-id="d203d-142">Parancsfájl futtatása</span><span class="sxs-lookup"><span data-stu-id="d203d-142">Run a Script</span></span>
<span data-ttu-id="d203d-143">Parancsprogram futtatása egy vagy több távoli számítógépet, használja az Invoke-Command parancsmaggal FilePath paraméterében.</span><span class="sxs-lookup"><span data-stu-id="d203d-143">To run a script on one or many remote computers, use the FilePath parameter of the Invoke-Command cmdlet.</span></span> <span data-ttu-id="d203d-144">A parancsfájl vagy a helyi számítógép által elérhető kell lennie.</span><span class="sxs-lookup"><span data-stu-id="d203d-144">The script must be on or accessible to your local computer.</span></span> <span data-ttu-id="d203d-145">Az eredmény akkor minősül, a helyi számítógépen.</span><span class="sxs-lookup"><span data-stu-id="d203d-145">The results are returned to your local computer.</span></span>

<span data-ttu-id="d203d-146">Például a következő parancsot a DiskCollect.ps1 parancsfájlt futtatja a kiszolgalo01 és Server02 távoli számítógépeken.</span><span class="sxs-lookup"><span data-stu-id="d203d-146">For example, the following command runs the DiskCollect.ps1 script on the Server01 and Server02 remote computers.</span></span>

```
Invoke-Command -ComputerName Server01, Server02 -FilePath c:\Scripts\DiskCollect.ps1
```

<span data-ttu-id="d203d-147">Az Invoke-Command parancsmaggal kapcsolatos további információkért lásd: [Invoke-Command](https://go.microsoft.com/fwlink/?LinkId=821493).</span><span class="sxs-lookup"><span data-stu-id="d203d-147">For more information about the Invoke-Command cmdlet, see [Invoke-Command](https://go.microsoft.com/fwlink/?LinkId=821493).</span></span>

### <a name="establish-a-persistent-connection"></a><span data-ttu-id="d203d-148">Állandó kapcsolatot létesíteni</span><span class="sxs-lookup"><span data-stu-id="d203d-148">Establish a Persistent Connection</span></span>
<span data-ttu-id="d203d-149">Kapcsolódó parancsokat, amelyek közös adatok futtatásához hozzon létre egy munkamenetet a távoli számítógépen, és az Invoke-Command parancsmaggal futtassa a parancsokat az Ön által létrehozott munkamenetben.</span><span class="sxs-lookup"><span data-stu-id="d203d-149">To run a series of related commands that share data, create a session on the remote computer and then use the Invoke-Command cmdlet to run commands in the session that you create.</span></span> <span data-ttu-id="d203d-150">Távoli munkamenet létrehozása a New-PSSession parancsmag használható.</span><span class="sxs-lookup"><span data-stu-id="d203d-150">To create a remote session, use the New-PSSession cmdlet.</span></span>

<span data-ttu-id="d203d-151">Például a következő parancs létrehoz egy távoli munkamenet a kiszolgalo01 számítógépre és egy másik távoli munkamenet Server02 számítógépen.</span><span class="sxs-lookup"><span data-stu-id="d203d-151">For example, the following command creates a remote session on the Server01 computer and another remote session on the Server02 computer.</span></span> <span data-ttu-id="d203d-152">A munkamenet-objektumok a $s változóban menti.</span><span class="sxs-lookup"><span data-stu-id="d203d-152">It saves the session objects in the $s variable.</span></span>

```
$s = New-PSSession -ComputerName Server01, Server02
```

<span data-ttu-id="d203d-153">Most, hogy a munkamenet jött létre, bennük valamelyik parancsának is futtathatja.</span><span class="sxs-lookup"><span data-stu-id="d203d-153">Now that the sessions are established, you can run any command in them.</span></span> <span data-ttu-id="d203d-154">És a munkameneteket állandó, mert egy parancs az adatgyűjtés, és a következő parancsot használhatja.</span><span class="sxs-lookup"><span data-stu-id="d203d-154">And because the sessions are persistent, you can collect data in one command and use it in a subsequent command.</span></span>

<span data-ttu-id="d203d-155">Például a következő parancsot a Get-gyorsjavítás parancsot futtatja, a $s változóban munkamenetekben, és az eredményeket a $h változóban menti.</span><span class="sxs-lookup"><span data-stu-id="d203d-155">For example, the following command runs a Get-HotFix command in the sessions in the $s variable and it saves the results in the $h variable.</span></span> <span data-ttu-id="d203d-156">A $h változó minden $s munkamenetekben létrejött, de nem létezik a helyi munkamenetben.</span><span class="sxs-lookup"><span data-stu-id="d203d-156">The $h variable is created in each of the sessions in $s, but it does not exist in the local session.</span></span>

```
Invoke-Command -Session $s {$h = Get-HotFix}
```

<span data-ttu-id="d203d-157">Most már használhatja az adatokat a következő parancsok, például a következő $h változót.</span><span class="sxs-lookup"><span data-stu-id="d203d-157">Now you can use the data in the $h variable in subsequent commands, such as the following one.</span></span> <span data-ttu-id="d203d-158">Az eredmények jelennek meg a helyi számítógépen.</span><span class="sxs-lookup"><span data-stu-id="d203d-158">The results are displayed on the local computer.</span></span>

```
Invoke-Command -Session $s {$h | where {$_.InstalledBy -ne "NTAUTHORITY\SYSTEM"}}
```

### <a name="advanced-remoting"></a><span data-ttu-id="d203d-159">Speciális távelérés</span><span class="sxs-lookup"><span data-stu-id="d203d-159">Advanced Remoting</span></span>
<span data-ttu-id="d203d-160">A Windows PowerShell távoli felügyeleti csak itt kezdődik.</span><span class="sxs-lookup"><span data-stu-id="d203d-160">Windows PowerShell remote management just begins here.</span></span> <span data-ttu-id="d203d-161">A telepített Windows PowerShell parancsmagok segítségével létrehozása és konfigurálása mindkét távoli munkamenetek a helyi és távoli véget ér, a testre szabott és korlátozott-munkameneteket hozzon létre engedélyezése a felhasználók parancsok importálása egy távoli munkamenetet, amely futtatja ténylegesen implicit módon adja meg a távoli munkamenet azt a távoli munkamenetet, és még sok más biztonságát.</span><span class="sxs-lookup"><span data-stu-id="d203d-161">By using the cmdlets installed with Windows PowerShell, you can establish and configure remote sessions both from the local and remote ends, create customized and restricted sessions, allow users to import commands from a remote session that actually run implicitly on the remote session, configure the security of a remote session, and much more.</span></span>

<span data-ttu-id="d203d-162">Lehetővé teszi a távoli konfiguráció, a Windows PowerShell a WSMan-szolgáltató foglal magában.</span><span class="sxs-lookup"><span data-stu-id="d203d-162">To facilitate remote configuration, Windows PowerShell includes a WSMan provider.</span></span> <span data-ttu-id="d203d-163">A WSMAN: a meghajtó a szolgáltató által létrehozott lehetővé teszi haladjon végig a konfigurációs beállításokat a helyi számítógépen és a távoli számítógépek hierarchiáját.</span><span class="sxs-lookup"><span data-stu-id="d203d-163">The WSMAN: drive that the provider creates lets you navigate through a hierarchy of configuration settings on the local computer and remote computers.</span></span>
<span data-ttu-id="d203d-164">A WSMan-szolgáltató kapcsolatos további információkért lásd: [WSMan szolgáltató](https://technet.microsoft.com/en-us/library/dd819476.aspx) és [WS-Management parancsmagok](https://technet.microsoft.com/en-us/library/dd819481.aspx), vagy a Windows PowerShell-konzolban, írja be a "Get-Help wsman".</span><span class="sxs-lookup"><span data-stu-id="d203d-164">For more information about the WSMan provider, see  [WSMan Provider](https://technet.microsoft.com/en-us/library/dd819476.aspx) and [About WS-Management Cmdlets](https://technet.microsoft.com/en-us/library/dd819481.aspx), or in the Windows PowerShell console, type "Get-Help wsman".</span></span>

<span data-ttu-id="d203d-165">További információ:</span><span class="sxs-lookup"><span data-stu-id="d203d-165">For more information, see:</span></span>
- [<span data-ttu-id="d203d-166">Kapcsolatos távoli – gyakori kérdések</span><span class="sxs-lookup"><span data-stu-id="d203d-166">About Remote FAQ</span></span>](https://technet.microsoft.com/en-us/library/dd315359.aspx)
- [<span data-ttu-id="d203d-167">Register-PSSessionConfiguration</span><span class="sxs-lookup"><span data-stu-id="d203d-167">Register-PSSessionConfiguration</span></span>](https://go.microsoft.com/fwlink/?LinkId=821508)
- [<span data-ttu-id="d203d-168">Import-PSSession</span><span class="sxs-lookup"><span data-stu-id="d203d-168">Import-PSSession</span></span>](https://go.microsoft.com/fwlink/?LinkId=821821)

<span data-ttu-id="d203d-169">Távoli eljáráshívás hibákkal kapcsolatban lásd: [about_Remote_Troubleshooting](https://technet.microsoft.com/en-us/library/dd347642.aspx).</span><span class="sxs-lookup"><span data-stu-id="d203d-169">For help with remoting errors, see [about_Remote_Troubleshooting](https://technet.microsoft.com/en-us/library/dd347642.aspx).</span></span>

## <a name="see-also"></a><span data-ttu-id="d203d-170">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="d203d-170">See Also</span></span>
- [<span data-ttu-id="d203d-171">about_Remote</span><span class="sxs-lookup"><span data-stu-id="d203d-171">about_Remote</span></span>](https://technet.microsoft.com/en-us/library/9b4a5c87-9162-4adf-bdfe-fbc80b9b8970)
- [<span data-ttu-id="d203d-172">about_Remote_FAQ</span><span class="sxs-lookup"><span data-stu-id="d203d-172">about_Remote_FAQ</span></span>](https://technet.microsoft.com/en-us/library/e23702fd-9415-4a98-9975-390a4d3adc42)
- [<span data-ttu-id="d203d-173">about_Remote_Requirements</span><span class="sxs-lookup"><span data-stu-id="d203d-173">about_Remote_Requirements</span></span>](https://technet.microsoft.com/en-us/library/da213949-134c-4741-b307-81f4492ba1bd)
- [<span data-ttu-id="d203d-174">about_Remote_Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="d203d-174">about_Remote_Troubleshooting</span></span>](https://technet.microsoft.com/en-us/library/2f890148-8578-49ed-85ea-79a489dd6317)
- [<span data-ttu-id="d203d-175">about_PSSessions</span><span class="sxs-lookup"><span data-stu-id="d203d-175">about_PSSessions</span></span>](https://technet.microsoft.com/en-us/library/7a9b4e0e-fa1b-47b0-92f6-6e2995d70acb)
- [<span data-ttu-id="d203d-176">about_WS-Management_Cmdlets</span><span class="sxs-lookup"><span data-stu-id="d203d-176">about_WS-Management_Cmdlets</span></span>](https://technet.microsoft.com/en-us/library/6ed3370a-ea10-45a5-9493-696aeace27ed)
- [<span data-ttu-id="d203d-177">Invoke-Command parancsot</span><span class="sxs-lookup"><span data-stu-id="d203d-177">Invoke-Command</span></span>](https://go.microsoft.com/fwlink/?LinkId=821493)
- [<span data-ttu-id="d203d-178">Import-PSSession</span><span class="sxs-lookup"><span data-stu-id="d203d-178">Import-PSSession</span></span>](https://go.microsoft.com/fwlink/?LinkId=821821)
- [<span data-ttu-id="d203d-179">Új-PSSession</span><span class="sxs-lookup"><span data-stu-id="d203d-179">New-PSSession</span></span>](https://go.microsoft.com/fwlink/?LinkId=821498)
- [<span data-ttu-id="d203d-180">Register-PSSessionConfiguration</span><span class="sxs-lookup"><span data-stu-id="d203d-180">Register-PSSessionConfiguration</span></span>](https://go.microsoft.com/fwlink/?LinkId=821508)
- [<span data-ttu-id="d203d-181">A WSMan-szolgáltató</span><span class="sxs-lookup"><span data-stu-id="d203d-181">WSMan Provider</span></span>](https://technet.microsoft.com/en-us/library/66fe1241-e08f-49ca-832f-a84c33ca8735)
