---
ms.date: 2017-06-05
keywords: PowerShell parancsmag
title: "A Windows PowerShell kezelése meghajtók"
ms.assetid: bd809e38-8de9-437a-a250-f30a667d11b4
ms.openlocfilehash: e2908246bb584291f04b67dc8635caec93d3b72e
ms.sourcegitcommit: d6ab9ab5909ed59cce4ce30e29457e0e75c7ac12
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/08/2017
---
# <a name="managing-windows-powershell-drives"></a><span data-ttu-id="ee15f-103">A Windows PowerShell kezelése meghajtók</span><span class="sxs-lookup"><span data-stu-id="ee15f-103">Managing Windows PowerShell Drives</span></span>
<span data-ttu-id="ee15f-104">A *Windows PowerShell meghajtót* hasonlóan a Windows PowerShellben a fájlrendszer meghajtóján keresztül elérhető adatok tárolási helyen található.</span><span class="sxs-lookup"><span data-stu-id="ee15f-104">A *Windows PowerShell drive* is a data store location that you can access like a file system drive in Windows PowerShell.</span></span> <span data-ttu-id="ee15f-105">A Windows PowerShell-szolgáltatók néhány meghajtó hozza létre, mint például a fájl-meghajtók (beleértve a C: és D:), a beállításjegyzék meghajtók (HKCU: és HKLM:), és a tanúsítvány meghajtó (Cert:), és létrehozhat saját Windows PowerShell-meghajtókat.</span><span class="sxs-lookup"><span data-stu-id="ee15f-105">The Windows PowerShell providers create some drives for you, such as the file system drives (including C: and D:), the registry drives (HKCU: and HKLM:), and the certificate drive (Cert:), and you can create your own Windows PowerShell drives.</span></span> <span data-ttu-id="ee15f-106">Ezek a meghajtók nagyon hasznosak, de csak a Windows PowerShell belül elérhetők.</span><span class="sxs-lookup"><span data-stu-id="ee15f-106">These drives are very useful, but they are available only within Windows PowerShell.</span></span> <span data-ttu-id="ee15f-107">Nem érhetők el azokat a Windows más eszközeit, például a Fájlkezelőben vagy a Cmd.exe.</span><span class="sxs-lookup"><span data-stu-id="ee15f-107">You cannot access them by using other Windows tools, such as File Explorer or Cmd.exe.</span></span>

<span data-ttu-id="ee15f-108">A Windows PowerShell használja a főnév **PSDrive**, a Windows PowerShell paranccsal meghajtók.</span><span class="sxs-lookup"><span data-stu-id="ee15f-108">Windows PowerShell uses the noun, **PSDrive**, for commands that work with Windows PowerShell drives.</span></span> <span data-ttu-id="ee15f-109">Az a Windows PowerShell listáját a Windows PowerShell-munkamenetben meghajtók, használja a **Get-PSDrive** parancsmag.</span><span class="sxs-lookup"><span data-stu-id="ee15f-109">For a list of the Windows PowerShell drives in your Windows PowerShell session, use the **Get-PSDrive** cmdlet.</span></span>

```
PS> Get-PSDrive

Name       Provider      Root                                   CurrentLocation
----       --------      ----                                   ---------------
A          FileSystem    A:\
Alias      Alias
C          FileSystem    C:\                                 ...And Settings\me
cert       Certificate   \
D          FileSystem    D:\
Env        Environment
Function   Function
HKCU       Registry      HKEY_CURRENT_USER
HKLM       Registry      HKEY_LOCAL_MACHINE
Variable   Variable
```

<span data-ttu-id="ee15f-110">Noha a jelennek meg a meghajtó a meghajtók, a rendszer, a listaelem alábbihoz hasonlóan fog megjelenni a kimenetét a **Get-PSDrive** fenti parancsot.</span><span class="sxs-lookup"><span data-stu-id="ee15f-110">Although the drives in the display vary with the drives on your system, the listing will look similar to the output of the **Get-PSDrive** command shown above.</span></span>

<span data-ttu-id="ee15f-111">Fájl rendszermeghajtók megtalálhatók a Windows PowerShell meghajtót.</span><span class="sxs-lookup"><span data-stu-id="ee15f-111">File system drives are a subset of the Windows PowerShell drives.</span></span> <span data-ttu-id="ee15f-112">Azonosíthatja, hogy a fájl rendszermeghajtók által a szolgáltató oszlop fájlrendszer bejegyzése.</span><span class="sxs-lookup"><span data-stu-id="ee15f-112">You can identify the file system drives by the FileSystem entry in the Provider column.</span></span> <span data-ttu-id="ee15f-113">(A Windows PowerShell FileSystem szolgáltató által a Windows PowerShellben a fájl rendszermeghajtók támogatott.)</span><span class="sxs-lookup"><span data-stu-id="ee15f-113">(The file system drives in Windows PowerShell are supported by the Windows PowerShell FileSystem provider.)</span></span>

<span data-ttu-id="ee15f-114">Által használt szintaxis megtekintéséhez a **Get-PSDrive** parancsmag, adjon meg egy **Get-Command** parancsot a **szintaxis** paraméter:</span><span class="sxs-lookup"><span data-stu-id="ee15f-114">To see the syntax of the **Get-PSDrive** cmdlet, type a **Get-Command** command with the **Syntax** parameter:</span></span>

```
PS> Get-Command -Name Get-PSDrive -Syntax
Get-PSDrive [[-Name] <String[]>] [-Scope <String>] [-PSProvider <String[]>] [-V
erbose] [-Debug] [-ErrorAction <ActionPreference>] [-ErrorVariable <String>] [-
OutVariable <String>] [-OutBuffer <Int32>]
```

<span data-ttu-id="ee15f-115">A **PSProvider** paraméter megadható, hogy csak a Windows PowerShell-meghajtók megjeleníti egy adott szolgáltató által támogatott.</span><span class="sxs-lookup"><span data-stu-id="ee15f-115">The **PSProvider** parameter lets you display only the Windows PowerShell drives that are supported by a particular provider.</span></span> <span data-ttu-id="ee15f-116">Csak a Windows PowerShell-meghajtókat, amelyek a Windows PowerShell FileSystem szolgáltató által támogatott megjelenítéséhez írja be például a **Get-PSDrive** parancsot a **PSProvider** paraméter és a  **Fájlrendszer** érték:</span><span class="sxs-lookup"><span data-stu-id="ee15f-116">For example, to display only the Windows PowerShell drives that are supported by the Windows PowerShell FileSystem provider, type a **Get-PSDrive** command with the **PSProvider** parameter and the **FileSystem** value:</span></span>

```
PS> Get-PSDrive -PSProvider FileSystem

Name       Provider      Root                                   CurrentLocation
----       --------      ----                                   ---------------
A          FileSystem    A:\
C          FileSystem    C:\                           ...nd Settings\PowerUser
D          FileSystem    D:\
```

<span data-ttu-id="ee15f-117">A Windows PowerShell-meghajtókat, amelyek megfelelnek a beállításjegyzék-struktúra megtekintéséhez használja a **PSProvider** paraméter csak a Windows PowerShell-meghajtók jelenik meg, hogy a Windows PowerShell beállításjegyzék-szolgáltató által támogatott:</span><span class="sxs-lookup"><span data-stu-id="ee15f-117">To view the Windows PowerShell drives that represent registry hives, use the **PSProvider** parameter to display only the Windows PowerShell drives that are supported by the Windows PowerShell Registry provider:</span></span>

<pre>PS> Get-PSDrive -PSProvider Registry
Name       Provider      Root                                   CurrentLocation
----       --------      ----                                   ---------------
HKCU       Registry      HKEY_CURRENT_USER
HKLM       Registry      HKEY_LOCAL_MACHINE</pre>

<span data-ttu-id="ee15f-118">A Windows PowerShell-meghajtókon is használhatja a szabványos hely parancsmagokat:</span><span class="sxs-lookup"><span data-stu-id="ee15f-118">You can also use the standard Location cmdlets with the Windows PowerShell drives:</span></span>

<pre>PS> Set-Location HKLM:\SOFTWARE
PS> Push-Location .\Microsoft
PS> Get-Location
Path
----
HKLM:\SOFTWARE\Microsoft</pre>

### <a name="adding-new-windows-powershell-drives-new-psdrive"></a><span data-ttu-id="ee15f-119">Hozzáadása az új Windows PowerShell-meghajtók (új PSDrive)</span><span class="sxs-lookup"><span data-stu-id="ee15f-119">Adding New Windows PowerShell Drives (New-PSDrive)</span></span>
<span data-ttu-id="ee15f-120">A Windows PowerShell meghajtót használatával adhat hozzá a **New-PSDrive** parancsot.</span><span class="sxs-lookup"><span data-stu-id="ee15f-120">You can add your own Windows PowerShell drives by using the **New-PSDrive** command.</span></span> <span data-ttu-id="ee15f-121">A szintaxisának lekérése a **New-PSDrive** parancsot, írja be a **Get-Command** parancsot a **szintaxis** paraméter:</span><span class="sxs-lookup"><span data-stu-id="ee15f-121">To get the syntax for the **New-PSDrive** command, enter the **Get-Command** command with the **Syntax** parameter:</span></span>

```
PS> Get-Command -Name New-PSDrive -Syntax
New-PSDrive [-Name] <String> [-PSProvider] <String> [-Root] <String> [-Descript
ion <String>] [-Scope <String>] [-Credential <PSCredential>] [-Verbose] [-Debug
] [-ErrorAction <ActionPreference>] [-ErrorVariable <String>] [-OutVariable <St
ring>] [-OutBuffer <Int32>] [-WhatIf] [-Confirm]
```

<span data-ttu-id="ee15f-122">Hozzon létre egy új Windows PowerShell meghajtót, meg kell adnia három paramétert:</span><span class="sxs-lookup"><span data-stu-id="ee15f-122">To create a new Windows PowerShell drive, you must supply three parameters:</span></span>

- <span data-ttu-id="ee15f-123">(Használhat bármilyen érvényes Windows PowerShell-név) a meghajtó nevét</span><span class="sxs-lookup"><span data-stu-id="ee15f-123">A name for the drive (you can use any valid Windows PowerShell name)</span></span>

- <span data-ttu-id="ee15f-124">A PSProvider (használja a rendszer fájlhelyek "FileSystem" és "Beállításjegyzék" beállításjegyzék-helyek esetében)</span><span class="sxs-lookup"><span data-stu-id="ee15f-124">The PSProvider (use "FileSystem" for file system locations and "Registry" for registry locations)</span></span>

- <span data-ttu-id="ee15f-125">A gyökérszintű, ez azt jelenti, hogy a legfelső szintű az új meghajtó elérési útja</span><span class="sxs-lookup"><span data-stu-id="ee15f-125">The root, that is, the path to the root of the new drive</span></span>

<span data-ttu-id="ee15f-126">Például létrehozhat egy nevű "Office" a Microsoft Office-alkalmazásokat, például a tartalmazó mappa leképezett meghajtót **C:\\Program Files\\Microsoft Office\\OFFICE11**.</span><span class="sxs-lookup"><span data-stu-id="ee15f-126">For example, you can create a drive named "Office" that is mapped to the folder that contains the Microsoft Office applications on your computer, such as **C:\\Program Files\\Microsoft Office\\OFFICE11**.</span></span> <span data-ttu-id="ee15f-127">A meghajtó, írja be a következő parancsot:</span><span class="sxs-lookup"><span data-stu-id="ee15f-127">To create the drive, type the following command:</span></span>

```
PS> New-PSDrive -Name Office -PSProvider FileSystem -Root "C:\Program Files\Micr
osoft Office\OFFICE11"

Name       Provider      Root                                   CurrentLocation
----       --------      ----                                   ---------------
Office     FileSystem    C:\Program Files\Microsoft Offic...
```

> [!NOTE]
> <span data-ttu-id="ee15f-128">Általában az elérési utak csak kis-és nagybetűket.</span><span class="sxs-lookup"><span data-stu-id="ee15f-128">In general, paths are not case-sensitive.</span></span>

<span data-ttu-id="ee15f-129">Az új Windows PowerShell meghajtót az összes Windows PowerShell-meghajtó – egy kettőspontot a név által módon hivatkozik (**:**).</span><span class="sxs-lookup"><span data-stu-id="ee15f-129">You refer to the new Windows PowerShell drive as you do all Windows PowerShell drives -- by its name followed by a colon (**:**).</span></span>

<span data-ttu-id="ee15f-130">A Windows PowerShell meghajtót számos feladatot tehet jóval egyszerűbbé válik.</span><span class="sxs-lookup"><span data-stu-id="ee15f-130">A Windows PowerShell drive can make many tasks much simpler.</span></span> <span data-ttu-id="ee15f-131">Például a Windows beállításjegyzékében legfontosabb kulcsok rendelkeznek rendkívül hosszú elérési utak, nehézkes lehet hozzáférési és nehéz megjegyezni minősítené.</span><span class="sxs-lookup"><span data-stu-id="ee15f-131">For example, some of the most important keys in the Windows registry have extremely long paths, making them cumbersome to access and difficult to remember.</span></span> <span data-ttu-id="ee15f-132">Fontos konfigurációs adatok alatt található **HKEY_LOCAL_MACHINE\\szoftver\\Microsoft\\Windows\\CurrentVersion**.</span><span class="sxs-lookup"><span data-stu-id="ee15f-132">Critical configuration information resides under **HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\Windows\\CurrentVersion**.</span></span> <span data-ttu-id="ee15f-133">- És CurrentVersion beállításkulcs, létrehozhat egy Windows PowerShell meghajtót, feltörték a kulcs írja be:</span><span class="sxs-lookup"><span data-stu-id="ee15f-133">To view and change items in the CurrentVersion registry key, you can create a Windows PowerShell drive that is rooted in that key by typing:</span></span>

<pre>PS> New-PSDrive -Name cvkey -PSProvider Registry -Root HKLM\Software\Microsoft\W
indows\CurrentVersion
Name       Provider      Root                                   CurrentLocation
----       --------      ----                                   ---------------
cvkey      Registry      HKLM\Software\Microsoft\Windows\...</pre>

<span data-ttu-id="ee15f-134">Módosíthatja a helyet, a **cvkey:** meghajtó, mint bármilyen más meghajtóról: "</span><span class="sxs-lookup"><span data-stu-id="ee15f-134">You can then change location to the **cvkey:** drive as you would any other drive:``</span></span>

`PS> cd cvkey:`

<span data-ttu-id="ee15f-135">vagy:</span><span class="sxs-lookup"><span data-stu-id="ee15f-135">or:</span></span>

<pre>PS> Set-Location cvkey: -PassThru
Path
----
cvkey:\</pre>

<span data-ttu-id="ee15f-136">A New-PsDrive parancsmag ad hozzá az új meghajtó csak az aktuális Windows PowerShell-munkamenetben.</span><span class="sxs-lookup"><span data-stu-id="ee15f-136">The New-PsDrive cmdlet adds the new drive only to the current Windows PowerShell session.</span></span> <span data-ttu-id="ee15f-137">Ha bezárja a Windows PowerShell-ablakot, az új meghajtó elveszik.</span><span class="sxs-lookup"><span data-stu-id="ee15f-137">If you close the Windows PowerShell window, the new drive is lost.</span></span> <span data-ttu-id="ee15f-138">Ha a Windows PowerShell-meghajtót, az Export-konzol parancsmag segítségével exportálhatja az aktuális Windows PowerShell-munkamenetet, és használja a PowerShell.exe **PSConsoleFile** paraméter importálnia.</span><span class="sxs-lookup"><span data-stu-id="ee15f-138">To save a Windows PowerShell drive, use the Export-Console cmdlet to export the current Windows PowerShell session, and then use the PowerShell.exe **PSConsoleFile** parameter to import it.</span></span> <span data-ttu-id="ee15f-139">Vagy az új meghajtó hozzáadása a Windows PowerShell-profilhoz.</span><span class="sxs-lookup"><span data-stu-id="ee15f-139">Or, add the new drive to your Windows PowerShell profile.</span></span>

### <a name="deleting-windows-powershell-drives-remove-psdrive"></a><span data-ttu-id="ee15f-140">Törli a Windows PowerShell-meghajtók (Remove-PSDrive)</span><span class="sxs-lookup"><span data-stu-id="ee15f-140">Deleting Windows PowerShell Drives (Remove-PSDrive)</span></span>
<span data-ttu-id="ee15f-141">Ön meghajtókat a Windows PowerShell használatával törölheti a **Remove-PSDrive** parancsmag.</span><span class="sxs-lookup"><span data-stu-id="ee15f-141">You can delete drives from Windows PowerShell by using the **Remove-PSDrive** cmdlet.</span></span> <span data-ttu-id="ee15f-142">A **Remove-PSDrive** parancsmag könnyen használható, egy adott Windows PowerShell meghajtót törölni, csak meg a Windows PowerShell meghajtót nevet.</span><span class="sxs-lookup"><span data-stu-id="ee15f-142">The **Remove-PSDrive** cmdlet is easy to use; to delete a specific Windows PowerShell drive, you just supply the Windows PowerShell drive name.</span></span>

<span data-ttu-id="ee15f-143">Például, ha hozzáadta a **Office:** Windows PowerShell meghajtót, ahogy az a **New-PSDrive** témakör, törölheti a beírásával:</span><span class="sxs-lookup"><span data-stu-id="ee15f-143">For example, if you added the **Office:** Windows PowerShell drive, as shown in the **New-PSDrive** topic, you can delete it by typing:</span></span>

```
PS> Remove-PSDrive -Name Office
```

<span data-ttu-id="ee15f-144">Törli a **cvkey:** Windows PowerShell meghajtót, is látható a **New-PSDrive** témakör, használja a következő parancsot:</span><span class="sxs-lookup"><span data-stu-id="ee15f-144">To delete the **cvkey:** Windows PowerShell drive, also shown in the **New-PSDrive** topic, use the following command:</span></span>

```
PS> Remove-PSDrive -Name cvkey
```

<span data-ttu-id="ee15f-145">A Windows PowerShell meghajtót törölheti, de nem törölhető, amíg a meghajtó.</span><span class="sxs-lookup"><span data-stu-id="ee15f-145">It's easy to delete a Windows PowerShell drive, but you can't delete it while you are in the drive.</span></span> <span data-ttu-id="ee15f-146">Például:</span><span class="sxs-lookup"><span data-stu-id="ee15f-146">For example:</span></span>

```
PS> cd office:
PS Office:\> remove-psdrive -name office
Remove-PSDrive : Cannot remove drive 'Office' because it is in use.
At line:1 char:15
+ remove-psdrive  <<<< -name office
```

### <a name="adding-and-removing-drives-outside-windows-powershell"></a><span data-ttu-id="ee15f-147">-Meghajtók kívül a Windows PowerShell hozzáadása és eltávolítása</span><span class="sxs-lookup"><span data-stu-id="ee15f-147">Adding and Removing Drives Outside Windows PowerShell</span></span>
<span data-ttu-id="ee15f-148">A Windows PowerShell hozzáadásakor vagy eltávolításakor a Windowsban, beleértve a csatlakoztatott hálózati meghajtók, a csatlakoztatott USB-meghajtók és a meghajtók használatával vagy törölt fájl rendszermeghajtók észleli a **használata net** parancs vagy a  **WScript.NetworkMapNetworkDrive** és **RemoveNetworkDrive** módszerek a Windows Script Host (WSH) parancsfájlt.</span><span class="sxs-lookup"><span data-stu-id="ee15f-148">Windows PowerShell detects file system drives that are added or removed in Windows, including network drives that are mapped, USB drives that are attached, and drives that are deleted by using either the **net use** command or the **WScript.NetworkMapNetworkDrive** and **RemoveNetworkDrive** methods from a Windows Script Host (WSH) script.</span></span>

