---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: Windows PowerShell-meghajtók kezelése
ms.assetid: bd809e38-8de9-437a-a250-f30a667d11b4
ms.openlocfilehash: cfc5418e9d2efb1a786817e1b941d75e22291742
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404503"
---
# <a name="managing-windows-powershell-drives"></a><span data-ttu-id="65e2b-103">Windows PowerShell-meghajtók kezelése</span><span class="sxs-lookup"><span data-stu-id="65e2b-103">Managing Windows PowerShell Drives</span></span>

<span data-ttu-id="65e2b-104">A *Windows PowerShell meghajtót* egy tároló hely, például a Windows PowerShellben a fájlrendszer meghajtóján keresztül elérhető.</span><span class="sxs-lookup"><span data-stu-id="65e2b-104">A *Windows PowerShell drive* is a data store location that you can access like a file system drive in Windows PowerShell.</span></span> <span data-ttu-id="65e2b-105">A Windows PowerShell-szolgáltatók néhány meghajtó hozza létre, például a fájlrendszer meghajtók (beleértve a C: és D:), a beállításjegyzék meghajtók (HKCU: és HKLM:), és a tanúsítvány-meghajtó (Cert:), és létrehozhatja a saját Windows PowerShell-meghajtók.</span><span class="sxs-lookup"><span data-stu-id="65e2b-105">The Windows PowerShell providers create some drives for you, such as the file system drives (including C: and D:), the registry drives (HKCU: and HKLM:), and the certificate drive (Cert:), and you can create your own Windows PowerShell drives.</span></span> <span data-ttu-id="65e2b-106">Ezek a meghajtók nagyon hasznos, de csak a Windows PowerShell belül elérhetők legyenek.</span><span class="sxs-lookup"><span data-stu-id="65e2b-106">These drives are very useful, but they are available only within Windows PowerShell.</span></span> <span data-ttu-id="65e2b-107">Nem érhetők el azokat más Windows-eszközök, például a Cmd.exe vagy a fájlkezelő használatával.</span><span class="sxs-lookup"><span data-stu-id="65e2b-107">You cannot access them by using other Windows tools, such as File Explorer or Cmd.exe.</span></span>

<span data-ttu-id="65e2b-108">Windows PowerShell használja a főnév **PSDrive**, parancsok, amelyek a Windows PowerShell-lel dolgozni meghajtók.</span><span class="sxs-lookup"><span data-stu-id="65e2b-108">Windows PowerShell uses the noun, **PSDrive**, for commands that work with Windows PowerShell drives.</span></span> <span data-ttu-id="65e2b-109">A listáját a Windows PowerShell meghajtót a Windows PowerShell-munkamenetben, használja a **Get-PSDrive** parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="65e2b-109">For a list of the Windows PowerShell drives in your Windows PowerShell session, use the **Get-PSDrive** cmdlet.</span></span>

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

<span data-ttu-id="65e2b-110">Bár a meghajtók, a megjelenő információk a rendszer a meghajtók számától függ, a listaelem láthatóhoz fog hasonlítani a kimenetét a **Get-PSDrive** fenti parancsot.</span><span class="sxs-lookup"><span data-stu-id="65e2b-110">Although the drives in the display vary with the drives on your system, the listing will look similar to the output of the **Get-PSDrive** command shown above.</span></span>

<span data-ttu-id="65e2b-111">Fájl rendszermeghajtók megtalálhatók a Windows PowerShell meghajtót.</span><span class="sxs-lookup"><span data-stu-id="65e2b-111">File system drives are a subset of the Windows PowerShell drives.</span></span> <span data-ttu-id="65e2b-112">A fájl rendszermeghajtók a fájlrendszer-bejegyzést a szolgáltató oszlop alapján azonosíthatja.</span><span class="sxs-lookup"><span data-stu-id="65e2b-112">You can identify the file system drives by the FileSystem entry in the Provider column.</span></span> <span data-ttu-id="65e2b-113">(A Windows PowerShellben a fájl rendszermeghajtók támogatottak a Windows PowerShell fájlrendszer-szolgáltatót.)</span><span class="sxs-lookup"><span data-stu-id="65e2b-113">(The file system drives in Windows PowerShell are supported by the Windows PowerShell FileSystem provider.)</span></span>

<span data-ttu-id="65e2b-114">Szintaxisának megtekintéséhez a **Get-PSDrive** parancsmagot, adjon meg egy **Get-Command** parancsot a **szintaxis** paramétert:</span><span class="sxs-lookup"><span data-stu-id="65e2b-114">To see the syntax of the **Get-PSDrive** cmdlet, type a **Get-Command** command with the **Syntax** parameter:</span></span>

```
PS> Get-Command -Name Get-PSDrive -Syntax

Get-PSDrive [[-Name] <String[]>] [-Scope <String>] [-PSProvider <String[]>] [-V
erbose] [-Debug] [-ErrorAction <ActionPreference>] [-ErrorVariable <String>] [-
OutVariable <String>] [-OutBuffer <Int32>]
```

<span data-ttu-id="65e2b-115">A **PSProvider** paraméter lehetővé teszi, hogy csak azok a Windows PowerShell-meghajtók jelenjenek meg az egyes szolgáltatók által támogatott.</span><span class="sxs-lookup"><span data-stu-id="65e2b-115">The **PSProvider** parameter lets you display only the Windows PowerShell drives that are supported by a particular provider.</span></span> <span data-ttu-id="65e2b-116">Ha például csak a Windows PowerShell fájlrendszer szolgáltató által támogatott Windows PowerShell meghajtót megjelenítéséhez írja be egy **Get-PSDrive** parancsot a **PSProvider** paraméter és a  **Fájlrendszer** érték:</span><span class="sxs-lookup"><span data-stu-id="65e2b-116">For example, to display only the Windows PowerShell drives that are supported by the Windows PowerShell FileSystem provider, type a **Get-PSDrive** command with the **PSProvider** parameter and the **FileSystem** value:</span></span>

```
PS> Get-PSDrive -PSProvider FileSystem

Name       Provider      Root                                   CurrentLocation
----       --------      ----                                   ---------------
A          FileSystem    A:\
C          FileSystem    C:\                           ...nd Settings\PowerUser
D          FileSystem    D:\
```

<span data-ttu-id="65e2b-117">A beállításjegyzék-struktúrát képviselő Windows PowerShell-meghajtók megtekintéséhez használja a **PSProvider** paraméter csak a Windows PowerShell-meghajtók jelenik meg, hogy a Windows PowerShell beállításjegyzék-szolgáltatója által támogatott:</span><span class="sxs-lookup"><span data-stu-id="65e2b-117">To view the Windows PowerShell drives that represent registry hives, use the **PSProvider** parameter to display only the Windows PowerShell drives that are supported by the Windows PowerShell Registry provider:</span></span>

```
PS> Get-PSDrive -PSProvider Registry

Name       Provider      Root                                   CurrentLocation
----       --------      ----                                   ---------------
HKCU       Registry      HKEY_CURRENT_USER
HKLM       Registry      HKEY_LOCAL_MACHINE
```

<span data-ttu-id="65e2b-118">A szabványos helyre parancsmagok a Windows PowerShell-meghajtók is használhatja:</span><span class="sxs-lookup"><span data-stu-id="65e2b-118">You can also use the standard Location cmdlets with the Windows PowerShell drives:</span></span>

```
PS> Set-Location HKLM:\SOFTWARE
PS> Push-Location .\Microsoft
PS> Get-Location

Path
----
HKLM:\SOFTWARE\Microsoft
```

### <a name="adding-new-windows-powershell-drives-new-psdrive"></a><span data-ttu-id="65e2b-119">Hozzáadás, új Windows PowerShell-meghajtók (új PSDrive)</span><span class="sxs-lookup"><span data-stu-id="65e2b-119">Adding New Windows PowerShell Drives (New-PSDrive)</span></span>

<span data-ttu-id="65e2b-120">A saját Windows PowerShell-meghajtók használatával adhat hozzá a **New-PSDrive** parancsot.</span><span class="sxs-lookup"><span data-stu-id="65e2b-120">You can add your own Windows PowerShell drives by using the **New-PSDrive** command.</span></span> <span data-ttu-id="65e2b-121">A szintaxisának lekérése a **New-PSDrive** parancshoz, írja be a **Get-Command** parancsot a **szintaxis** paramétert:</span><span class="sxs-lookup"><span data-stu-id="65e2b-121">To get the syntax for the **New-PSDrive** command, enter the **Get-Command** command with the **Syntax** parameter:</span></span>

```
PS> Get-Command -Name New-PSDrive -Syntax

New-PSDrive [-Name] <String> [-PSProvider] <String> [-Root] <String> [-Descript
ion <String>] [-Scope <String>] [-Credential <PSCredential>] [-Verbose] [-Debug
] [-ErrorAction <ActionPreference>] [-ErrorVariable <String>] [-OutVariable <St
ring>] [-OutBuffer <Int32>] [-WhatIf] [-Confirm]
```

<span data-ttu-id="65e2b-122">Hozzon létre egy új Windows PowerShell meghajtót, három paramétert kell megadnia:</span><span class="sxs-lookup"><span data-stu-id="65e2b-122">To create a new Windows PowerShell drive, you must supply three parameters:</span></span>

- <span data-ttu-id="65e2b-123">A meghajtó (bármilyen érvényes Windows PowerShell-nevet is használ) nevét</span><span class="sxs-lookup"><span data-stu-id="65e2b-123">A name for the drive (you can use any valid Windows PowerShell name)</span></span>

- <span data-ttu-id="65e2b-124">A PSProvider (használja a "Fájlrendszer" fájlrendszerbeli helyeken és a "Beállításjegyzék" beállításjegyzék-helyeken a)</span><span class="sxs-lookup"><span data-stu-id="65e2b-124">The PSProvider (use "FileSystem" for file system locations and "Registry" for registry locations)</span></span>

- <span data-ttu-id="65e2b-125">A legfelső szintű, a legfelső szintű, az új meghajtó elérési útja</span><span class="sxs-lookup"><span data-stu-id="65e2b-125">The root, that is, the path to the root of the new drive</span></span>

<span data-ttu-id="65e2b-126">Például létrehozhat egy nevű, "Office", mint például a számítógépre, a Microsoft Office-alkalmazásokat tartalmazó mappát leképezett meghajtót **C:\\Program Files\\a Microsoft Office\\OFFICE11**.</span><span class="sxs-lookup"><span data-stu-id="65e2b-126">For example, you can create a drive named "Office" that is mapped to the folder that contains the Microsoft Office applications on your computer, such as **C:\\Program Files\\Microsoft Office\\OFFICE11**.</span></span> <span data-ttu-id="65e2b-127">Hozza létre a meghajtót, írja be a következő parancsot:</span><span class="sxs-lookup"><span data-stu-id="65e2b-127">To create the drive, type the following command:</span></span>

```
PS> New-PSDrive -Name Office -PSProvider FileSystem -Root "C:\Program Files\Micr
osoft Office\OFFICE11"

Name       Provider      Root                                   CurrentLocation
----       --------      ----                                   ---------------
Office     FileSystem    C:\Program Files\Microsoft Offic...
```

> [!NOTE]
> <span data-ttu-id="65e2b-128">Általánosságban véve az elérési utakat nem kis-és nagybetűket.</span><span class="sxs-lookup"><span data-stu-id="65e2b-128">In general, paths are not case-sensitive.</span></span>

<span data-ttu-id="65e2b-129">Az új Windows PowerShell meghajtót mint Önnek az összes Windows PowerShell-meghajtó – egy kettőspontot a név alapján hivatkozhat (**:**).</span><span class="sxs-lookup"><span data-stu-id="65e2b-129">You refer to the new Windows PowerShell drive as you do all Windows PowerShell drives -- by its name followed by a colon (**:**).</span></span>

<span data-ttu-id="65e2b-130">A Windows PowerShell meghajtót számos feladatot teheti sokkal egyszerűbbek.</span><span class="sxs-lookup"><span data-stu-id="65e2b-130">A Windows PowerShell drive can make many tasks much simpler.</span></span> <span data-ttu-id="65e2b-131">Például néhány, a legfontosabb kulcsokat, a Windows beállításjegyzékben kell rendkívül hosszú elérési utak teszi őket a hozzáférés nehézkes és nehezen ne felejtse el.</span><span class="sxs-lookup"><span data-stu-id="65e2b-131">For example, some of the most important keys in the Windows registry have extremely long paths, making them cumbersome to access and difficult to remember.</span></span> <span data-ttu-id="65e2b-132">Nagyon fontos konfigurációs adatok alatt találhatók **HKEY_LOCAL_MACHINE\\szoftver\\Microsoft\\Windows\\CurrentVersion**.</span><span class="sxs-lookup"><span data-stu-id="65e2b-132">Critical configuration information resides under **HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\Windows\\CurrentVersion**.</span></span> <span data-ttu-id="65e2b-133">Megtekintése és módosítása CurrentVersion beállításkulcs elemek, hozhat létre egy Windows PowerShell meghajtót, amely feltörték ezt a kulcsot a beírásával:</span><span class="sxs-lookup"><span data-stu-id="65e2b-133">To view and change items in the CurrentVersion registry key, you can create a Windows PowerShell drive that is rooted in that key by typing:</span></span>

```
PS> New-PSDrive -Name cvkey -PSProvider Registry -Root HKLM\Software\Microsoft\W
indows\CurrentVersion

Name       Provider      Root                                   CurrentLocation
----       --------      ----                                   ---------------
cvkey      Registry      HKLM\Software\Microsoft\Windows\...
```

<span data-ttu-id="65e2b-134">Ezt követően módosíthatja a helyet a **cvkey:** meghajtó, mint bármilyen más meghajtóról:''</span><span class="sxs-lookup"><span data-stu-id="65e2b-134">You can then change location to the **cvkey:** drive as you would any other drive:\`\`</span></span>

`PS> cd cvkey:`

<span data-ttu-id="65e2b-135">vagy:</span><span class="sxs-lookup"><span data-stu-id="65e2b-135">or:</span></span>

```
PS> Set-Location cvkey: -PassThru

Path
----
cvkey:\
```

<span data-ttu-id="65e2b-136">A New-PsDrive parancsmag hozzáadja az új meghajtó csak az aktuális Windows PowerShell-munkamenetben.</span><span class="sxs-lookup"><span data-stu-id="65e2b-136">The New-PsDrive cmdlet adds the new drive only to the current Windows PowerShell session.</span></span> <span data-ttu-id="65e2b-137">Ha bezárja a Windows PowerShell-ablakot, az új meghajtó elveszik.</span><span class="sxs-lookup"><span data-stu-id="65e2b-137">If you close the Windows PowerShell window, the new drive is lost.</span></span> <span data-ttu-id="65e2b-138">Szeretné menteni egy Windows PowerShell meghajtót, az Export-konzol parancsmaggal exportálhatja a jelenlegi Windows PowerShell-munkamenetet, és használja a PowerShell.exe **PSConsoleFile** paraméter importálásához.</span><span class="sxs-lookup"><span data-stu-id="65e2b-138">To save a Windows PowerShell drive, use the Export-Console cmdlet to export the current Windows PowerShell session, and then use the PowerShell.exe **PSConsoleFile** parameter to import it.</span></span> <span data-ttu-id="65e2b-139">Vagy az új meghajtó felvétele a Windows PowerShell-profilt.</span><span class="sxs-lookup"><span data-stu-id="65e2b-139">Or, add the new drive to your Windows PowerShell profile.</span></span>

### <a name="deleting-windows-powershell-drives-remove-psdrive"></a><span data-ttu-id="65e2b-140">Törlése a Windows PowerShell-meghajtók (Remove-PSDrive)</span><span class="sxs-lookup"><span data-stu-id="65e2b-140">Deleting Windows PowerShell Drives (Remove-PSDrive)</span></span>

<span data-ttu-id="65e2b-141">A Windows powershellből meghajtók segítségével törölheti a **Remove-PSDrive** parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="65e2b-141">You can delete drives from Windows PowerShell by using the **Remove-PSDrive** cmdlet.</span></span> <span data-ttu-id="65e2b-142">A **Remove-PSDrive** parancsmag könnyen használható; Ha törölni szeretné egy adott Windows PowerShell-meghajtón, csak megadni a Windows PowerShell-meghajtó nevét.</span><span class="sxs-lookup"><span data-stu-id="65e2b-142">The **Remove-PSDrive** cmdlet is easy to use; to delete a specific Windows PowerShell drive, you just supply the Windows PowerShell drive name.</span></span>

<span data-ttu-id="65e2b-143">Például, ha hozzáadta a **Office:** Windows PowerShell meghajtót, ahogyan az a **New-PSDrive** témakör, törölheti azt írja be:</span><span class="sxs-lookup"><span data-stu-id="65e2b-143">For example, if you added the **Office:** Windows PowerShell drive, as shown in the **New-PSDrive** topic, you can delete it by typing:</span></span>

```powershell
Remove-PSDrive -Name Office
```

<span data-ttu-id="65e2b-144">Törli a **cvkey:** Windows PowerShell-meghajtó, is látható a **New-PSDrive** témakörben, használja a következő parancsot:</span><span class="sxs-lookup"><span data-stu-id="65e2b-144">To delete the **cvkey:** Windows PowerShell drive, also shown in the **New-PSDrive** topic, use the following command:</span></span>

```powershell
Remove-PSDrive -Name cvkey
```

<span data-ttu-id="65e2b-145">Egyszerűen törölni egy Windows PowerShell meghajtót, de nem törölhető, amíg a meghajtó.</span><span class="sxs-lookup"><span data-stu-id="65e2b-145">It's easy to delete a Windows PowerShell drive, but you can't delete it while you are in the drive.</span></span> <span data-ttu-id="65e2b-146">Például:</span><span class="sxs-lookup"><span data-stu-id="65e2b-146">For example:</span></span>

```
PS> cd office:
PS Office:\> remove-psdrive -name office
Remove-PSDrive : Cannot remove drive 'Office' because it is in use.
At line:1 char:15
+ remove-psdrive  <<<< -name office
```

### <a name="adding-and-removing-drives-outside-windows-powershell"></a><span data-ttu-id="65e2b-147">-Meghajtók kívül a Windows PowerShell hozzáadása és eltávolítása</span><span class="sxs-lookup"><span data-stu-id="65e2b-147">Adding and Removing Drives Outside Windows PowerShell</span></span>

<span data-ttu-id="65e2b-148">Windows PowerShell hozzáadásakor vagy eltávolításakor a Windows, beleértve a csatlakoztatott hálózati meghajtók, a csatlakoztatott USB-meghajtók és a meghajtók, a törölt fájl rendszermeghajtók észleli a **használata net** parancsot vagy a  **WScript.NetworkMapNetworkDrive** és **RemoveNetworkDrive** módszerek a Windows Script Host (WSH) parancsfájlt.</span><span class="sxs-lookup"><span data-stu-id="65e2b-148">Windows PowerShell detects file system drives that are added or removed in Windows, including network drives that are mapped, USB drives that are attached, and drives that are deleted by using either the **net use** command or the **WScript.NetworkMapNetworkDrive** and **RemoveNetworkDrive** methods from a Windows Script Host (WSH) script.</span></span>