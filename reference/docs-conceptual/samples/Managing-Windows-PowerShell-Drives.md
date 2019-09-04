---
ms.date: 06/05/2017
keywords: PowerShell, parancsmag
title: Windows PowerShell-meghajtók kezelése
ms.openlocfilehash: 5d1aba459caeaab2542e17e74534da6713b0faa9
ms.sourcegitcommit: 02eed65c526ef19cf952c2129f280bb5615bf0c8
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/03/2019
ms.locfileid: "70215508"
---
# <a name="managing-windows-powershell-drives"></a><span data-ttu-id="1371d-103">Windows PowerShell-meghajtók kezelése</span><span class="sxs-lookup"><span data-stu-id="1371d-103">Managing Windows PowerShell Drives</span></span>

<span data-ttu-id="1371d-104">A *Windows PowerShell meghajtó* egy adattár-hely, amely a Windows PowerShellben található fájlrendszer-meghajtóhoz is hozzáférhet.</span><span class="sxs-lookup"><span data-stu-id="1371d-104">A *Windows PowerShell drive* is a data store location that you can access like a file system drive in Windows PowerShell.</span></span> <span data-ttu-id="1371d-105">A Windows PowerShell-szolgáltatók létrehoznak néhány meghajtót az Ön számára, például a fájlrendszer meghajtóit (beleértve a C: és a D:), a beállításjegyzék-meghajtókat (HKCU: és HKLM:) és a tanúsítvány meghajtóját (CERT:), és létrehozhat saját Windows PowerShell-meghajtókat is.</span><span class="sxs-lookup"><span data-stu-id="1371d-105">The Windows PowerShell providers create some drives for you, such as the file system drives (including C: and D:), the registry drives (HKCU: and HKLM:), and the certificate drive (Cert:), and you can create your own Windows PowerShell drives.</span></span> <span data-ttu-id="1371d-106">Ezek a meghajtók nagyon hasznosak, de csak a Windows PowerShellben érhetők el.</span><span class="sxs-lookup"><span data-stu-id="1371d-106">These drives are very useful, but they are available only within Windows PowerShell.</span></span> <span data-ttu-id="1371d-107">Nem érheti el őket más Windows-eszközök, például a fájlkezelő vagy a cmd. exe használatával.</span><span class="sxs-lookup"><span data-stu-id="1371d-107">You cannot access them by using other Windows tools, such as File Explorer or Cmd.exe.</span></span>

<span data-ttu-id="1371d-108">A Windows PowerShell a **PSDrive**, a Windows PowerShell-meghajtókkal működő parancsok esetében a főnévot használja.</span><span class="sxs-lookup"><span data-stu-id="1371d-108">Windows PowerShell uses the noun, **PSDrive**, for commands that work with Windows PowerShell drives.</span></span> <span data-ttu-id="1371d-109">A Windows PowerShell-munkamenetben található Windows PowerShell-meghajtók listáját a **Get-PSDrive** parancsmaggal teheti meg.</span><span class="sxs-lookup"><span data-stu-id="1371d-109">For a list of the Windows PowerShell drives in your Windows PowerShell session, use the **Get-PSDrive** cmdlet.</span></span>

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

<span data-ttu-id="1371d-110">Bár a kijelzőn lévő meghajtók a rendszeren található meghajtóktól eltérőek, a lista a fent látható **Get-PSDrive** parancs kimenetéhez hasonlóan fog kinézni.</span><span class="sxs-lookup"><span data-stu-id="1371d-110">Although the drives in the display vary with the drives on your system, the listing will look similar to the output of the **Get-PSDrive** command shown above.</span></span>

<span data-ttu-id="1371d-111">A fájlrendszer-meghajtók a Windows PowerShell-meghajtók egy részhalmaza.</span><span class="sxs-lookup"><span data-stu-id="1371d-111">File system drives are a subset of the Windows PowerShell drives.</span></span> <span data-ttu-id="1371d-112">A fájlrendszer meghajtóit a szolgáltató oszlopban található fájlrendszer-bejegyzés alapján azonosíthatja.</span><span class="sxs-lookup"><span data-stu-id="1371d-112">You can identify the file system drives by the FileSystem entry in the Provider column.</span></span> <span data-ttu-id="1371d-113">(A Windows PowerShell fájlrendszer-meghajtóit a Windows PowerShell fájlrendszer-szolgáltatója támogatja.)</span><span class="sxs-lookup"><span data-stu-id="1371d-113">(The file system drives in Windows PowerShell are supported by the Windows PowerShell FileSystem provider.)</span></span>

<span data-ttu-id="1371d-114">A **Get-PSDrive** parancsmag szintaxisának megtekintéséhez írja be a **Get-Command** parancsot a **szintaxis** paraméterrel:</span><span class="sxs-lookup"><span data-stu-id="1371d-114">To see the syntax of the **Get-PSDrive** cmdlet, type a **Get-Command** command with the **Syntax** parameter:</span></span>

```
PS> Get-Command -Name Get-PSDrive -Syntax

Get-PSDrive [[-Name] <String[]>] [-Scope <String>] [-PSProvider <String[]>] [-V
erbose] [-Debug] [-ErrorAction <ActionPreference>] [-ErrorVariable <String>] [-
OutVariable <String>] [-OutBuffer <Int32>]
```

<span data-ttu-id="1371d-115">A **PSProvider** paraméter lehetővé teszi, hogy csak az adott szolgáltató által támogatott Windows PowerShell-meghajtókat jelenítse meg.</span><span class="sxs-lookup"><span data-stu-id="1371d-115">The **PSProvider** parameter lets you display only the Windows PowerShell drives that are supported by a particular provider.</span></span> <span data-ttu-id="1371d-116">Ha például csak a Windows PowerShell fájlrendszer-szolgáltató által támogatott Windows PowerShell-meghajtókat szeretné megjeleníteni, írja be a **Get-PSDrive** parancsot a **PSProvider** paraméterrel és a **fájlrendszer** értékével:</span><span class="sxs-lookup"><span data-stu-id="1371d-116">For example, to display only the Windows PowerShell drives that are supported by the Windows PowerShell FileSystem provider, type a **Get-PSDrive** command with the **PSProvider** parameter and the **FileSystem** value:</span></span>

```
PS> Get-PSDrive -PSProvider FileSystem

Name       Provider      Root                                   CurrentLocation
----       --------      ----                                   ---------------
A          FileSystem    A:\
C          FileSystem    C:\                           ...nd Settings\PowerUser
D          FileSystem    D:\
```

<span data-ttu-id="1371d-117">A beállításjegyzék-struktúrákat képviselő Windows PowerShell-meghajtók megtekintéséhez használja a **PSProvider** paramétert a Windows PowerShell beállításjegyzék-szolgáltató által támogatott Windows PowerShell-meghajtók megjelenítéséhez:</span><span class="sxs-lookup"><span data-stu-id="1371d-117">To view the Windows PowerShell drives that represent registry hives, use the **PSProvider** parameter to display only the Windows PowerShell drives that are supported by the Windows PowerShell Registry provider:</span></span>

```
PS> Get-PSDrive -PSProvider Registry

Name       Provider      Root                                   CurrentLocation
----       --------      ----                                   ---------------
HKCU       Registry      HKEY_CURRENT_USER
HKLM       Registry      HKEY_LOCAL_MACHINE
```

<span data-ttu-id="1371d-118">A standard Location parancsmagokat a Windows PowerShell-meghajtókkal is használhatja:</span><span class="sxs-lookup"><span data-stu-id="1371d-118">You can also use the standard Location cmdlets with the Windows PowerShell drives:</span></span>

```
PS> Set-Location HKLM:\SOFTWARE
PS> Push-Location .\Microsoft
PS> Get-Location

Path
----
HKLM:\SOFTWARE\Microsoft
```

## <a name="adding-new-windows-powershell-drives-new-psdrive"></a><span data-ttu-id="1371d-119">Új Windows PowerShell-meghajtók hozzáadása (New-PSDrive)</span><span class="sxs-lookup"><span data-stu-id="1371d-119">Adding New Windows PowerShell Drives (New-PSDrive)</span></span>

<span data-ttu-id="1371d-120">A **New-PSDrive** parancs használatával saját Windows PowerShell-meghajtókat is hozzáadhat.</span><span class="sxs-lookup"><span data-stu-id="1371d-120">You can add your own Windows PowerShell drives by using the **New-PSDrive** command.</span></span> <span data-ttu-id="1371d-121">A **New-PSDrive** parancs szintaxisának lekéréséhez írja be a **Get-Command** parancsot a **szintaxis** paraméterrel:</span><span class="sxs-lookup"><span data-stu-id="1371d-121">To get the syntax for the **New-PSDrive** command, enter the **Get-Command** command with the **Syntax** parameter:</span></span>

```
PS> Get-Command -Name New-PSDrive -Syntax

New-PSDrive [-Name] <String> [-PSProvider] <String> [-Root] <String> [-Descript
ion <String>] [-Scope <String>] [-Credential <PSCredential>] [-Verbose] [-Debug
] [-ErrorAction <ActionPreference>] [-ErrorVariable <String>] [-OutVariable <St
ring>] [-OutBuffer <Int32>] [-WhatIf] [-Confirm]
```

<span data-ttu-id="1371d-122">Új Windows PowerShell-meghajtó létrehozásához három paramétert kell megadnia:</span><span class="sxs-lookup"><span data-stu-id="1371d-122">To create a new Windows PowerShell drive, you must supply three parameters:</span></span>

- <span data-ttu-id="1371d-123">A meghajtó neve (bármilyen érvényes Windows PowerShell-nevet használhat)</span><span class="sxs-lookup"><span data-stu-id="1371d-123">A name for the drive (you can use any valid Windows PowerShell name)</span></span>

- <span data-ttu-id="1371d-124">A PSProvider (a "fájlrendszer" használata a beállításjegyzék helyein a fájlrendszerbeli és a beállításjegyzékben)</span><span class="sxs-lookup"><span data-stu-id="1371d-124">The PSProvider (use "FileSystem" for file system locations and "Registry" for registry locations)</span></span>

- <span data-ttu-id="1371d-125">A gyökér, azaz az új meghajtó gyökerének elérési útja</span><span class="sxs-lookup"><span data-stu-id="1371d-125">The root, that is, the path to the root of the new drive</span></span>

<span data-ttu-id="1371d-126">Létrehozhat például egy "Office" nevű meghajtót, amely a számítógépen Microsoft Office alkalmazást tartalmazó mappához van rendelve, például **C:\\program\\Files\\Microsoft Office Office11**.</span><span class="sxs-lookup"><span data-stu-id="1371d-126">For example, you can create a drive named "Office" that is mapped to the folder that contains the Microsoft Office applications on your computer, such as **C:\\Program Files\\Microsoft Office\\OFFICE11**.</span></span> <span data-ttu-id="1371d-127">A meghajtó létrehozásához írja be a következő parancsot:</span><span class="sxs-lookup"><span data-stu-id="1371d-127">To create the drive, type the following command:</span></span>

```
PS> New-PSDrive -Name Office -PSProvider FileSystem -Root "C:\Program Files\Microsoft Office\OFFICE11"

Name       Provider      Root                                   CurrentLocation
----       --------      ----                                   ---------------
Office     FileSystem    C:\Program Files\Microsoft Offic...
```

> [!NOTE]
> <span data-ttu-id="1371d-128">Az elérési utak általában nem megkülönböztetik a kis-és nagybetűket.</span><span class="sxs-lookup"><span data-stu-id="1371d-128">In general, paths are not case-sensitive.</span></span>

<span data-ttu-id="1371d-129">Az új Windows PowerShell-meghajtót az összes Windows PowerShell-meghajtón tekintheti meg – a neve után egy kettősponttal ( **:** ).</span><span class="sxs-lookup"><span data-stu-id="1371d-129">You refer to the new Windows PowerShell drive as you do all Windows PowerShell drives -- by its name followed by a colon (**:**).</span></span>

<span data-ttu-id="1371d-130">A Windows PowerShell-meghajtók sokkal egyszerűbben végezhetnek el sok feladatot.</span><span class="sxs-lookup"><span data-stu-id="1371d-130">A Windows PowerShell drive can make many tasks much simpler.</span></span> <span data-ttu-id="1371d-131">A Windows beállításjegyzék legfontosabb kulcsai például rendkívül hosszú elérési utakkal rendelkeznek, így nehézkes a hozzáférés és a nehezen megjegyezhető.</span><span class="sxs-lookup"><span data-stu-id="1371d-131">For example, some of the most important keys in the Windows registry have extremely long paths, making them cumbersome to access and difficult to remember.</span></span> <span data-ttu-id="1371d-132">A kritikus konfigurációs információk a **HKEY_LOCAL_MACHINE\\Software\\\\Microsoft\\Windows CurrentVersion**alatt találhatók.</span><span class="sxs-lookup"><span data-stu-id="1371d-132">Critical configuration information resides under **HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\Windows\\CurrentVersion**.</span></span> <span data-ttu-id="1371d-133">A CurrentVersion beállításkulcs elemeinek megtekintéséhez és módosításához hozzon létre egy olyan Windows PowerShell-meghajtót, amely az adott kulcsban gyökerezik a következő beírásával:</span><span class="sxs-lookup"><span data-stu-id="1371d-133">To view and change items in the CurrentVersion registry key, you can create a Windows PowerShell drive that is rooted in that key by typing:</span></span>

```
PS> New-PSDrive -Name cvkey -PSProvider Registry -Root HKLM\Software\Microsoft\Windows\CurrentVersion

Name       Provider      Root                                   CurrentLocation
----       --------      ----                                   ---------------
cvkey      Registry      HKLM\Software\Microsoft\Windows\...
```

<span data-ttu-id="1371d-134">Ezután megváltoztathatja a helyet a **cvkey:** meghajtóra, mint bármely más meghajtót:</span><span class="sxs-lookup"><span data-stu-id="1371d-134">You can then change location to the **cvkey:** drive as you would any other drive:</span></span>

```
PS> cd cvkey:
```

<span data-ttu-id="1371d-135">vagy:</span><span class="sxs-lookup"><span data-stu-id="1371d-135">or:</span></span>

```
PS> Set-Location cvkey: -PassThru

Path
----
cvkey:\
```

<span data-ttu-id="1371d-136">A New-PsDrive parancsmag csak az aktuális Windows PowerShell-munkamenethez adja hozzá az új meghajtót.</span><span class="sxs-lookup"><span data-stu-id="1371d-136">The New-PsDrive cmdlet adds the new drive only to the current Windows PowerShell session.</span></span> <span data-ttu-id="1371d-137">Ha bezárta a Windows PowerShell ablakát, az új meghajtó elvész.</span><span class="sxs-lookup"><span data-stu-id="1371d-137">If you close the Windows PowerShell window, the new drive is lost.</span></span> <span data-ttu-id="1371d-138">Windows PowerShell-meghajtó mentéséhez használja az export-Console parancsmagot az aktuális Windows PowerShell-munkamenet exportálásához, majd a PowerShell. exe **PSConsoleFile** paraméter használatával importálja.</span><span class="sxs-lookup"><span data-stu-id="1371d-138">To save a Windows PowerShell drive, use the Export-Console cmdlet to export the current Windows PowerShell session, and then use the PowerShell.exe **PSConsoleFile** parameter to import it.</span></span> <span data-ttu-id="1371d-139">Vagy adja hozzá az új meghajtót a Windows PowerShell-profilhoz.</span><span class="sxs-lookup"><span data-stu-id="1371d-139">Or, add the new drive to your Windows PowerShell profile.</span></span>

## <a name="deleting-windows-powershell-drives-remove-psdrive"></a><span data-ttu-id="1371d-140">Windows PowerShell-meghajtók törlése (remove-PSDrive)</span><span class="sxs-lookup"><span data-stu-id="1371d-140">Deleting Windows PowerShell Drives (Remove-PSDrive)</span></span>

<span data-ttu-id="1371d-141">A **Remove-PSDrive** parancsmag használatával törölheti a meghajtókat a Windows powershellből.</span><span class="sxs-lookup"><span data-stu-id="1371d-141">You can delete drives from Windows PowerShell by using the **Remove-PSDrive** cmdlet.</span></span> <span data-ttu-id="1371d-142">A **Remove-PSDrive** parancsmag egyszerűen használható; egy adott Windows PowerShell-meghajtó törléséhez csak adja meg a Windows PowerShell-meghajtó nevét.</span><span class="sxs-lookup"><span data-stu-id="1371d-142">The **Remove-PSDrive** cmdlet is easy to use; to delete a specific Windows PowerShell drive, you just supply the Windows PowerShell drive name.</span></span>

<span data-ttu-id="1371d-143">Ha például hozzáadta az **irodát:** Windows PowerShell-meghajtó, ahogy az a **New-PSDrive** című témakörben is látható, a következő beírásával törölheti:</span><span class="sxs-lookup"><span data-stu-id="1371d-143">For example, if you added the **Office:** Windows PowerShell drive, as shown in the **New-PSDrive** topic, you can delete it by typing:</span></span>

```powershell
Remove-PSDrive -Name Office
```

<span data-ttu-id="1371d-144">A cvkey törlése **:** Windows PowerShell meghajtó, a **New-PSDrive** című témakörben is látható, használja a következő parancsot:</span><span class="sxs-lookup"><span data-stu-id="1371d-144">To delete the **cvkey:** Windows PowerShell drive, also shown in the **New-PSDrive** topic, use the following command:</span></span>

```powershell
Remove-PSDrive -Name cvkey
```

<span data-ttu-id="1371d-145">Egyszerűen törölheti a Windows PowerShell-meghajtót, de nem törölheti a meghajtót.</span><span class="sxs-lookup"><span data-stu-id="1371d-145">It's easy to delete a Windows PowerShell drive, but you can't delete it while you are in the drive.</span></span> <span data-ttu-id="1371d-146">Például:</span><span class="sxs-lookup"><span data-stu-id="1371d-146">For example:</span></span>

```
PS> cd office:
PS Office:\> remove-psdrive -name office
Remove-PSDrive : Cannot remove drive 'Office' because it is in use.
At line:1 char:15
+ remove-psdrive  <<<< -name office
```

## <a name="adding-and-removing-drives-outside-windows-powershell"></a><span data-ttu-id="1371d-147">Meghajtók hozzáadása és eltávolítása a Windows PowerShellen kívül</span><span class="sxs-lookup"><span data-stu-id="1371d-147">Adding and Removing Drives Outside Windows PowerShell</span></span>

<span data-ttu-id="1371d-148">A Windows PowerShell észleli a Windowsban hozzáadott vagy eltávolított fájlrendszer-meghajtókat, beleértve a csatlakoztatott hálózati meghajtókat, a csatlakoztatott USB-meghajtókat, valamint a **net use** paranccsal vagy a **használatával törölt meghajtókat. WScript. NetworkMapNetworkDrive** és **RemoveNetworkDrive** metódusok egy Windows Script Host (WSH) parancsfájlból.</span><span class="sxs-lookup"><span data-stu-id="1371d-148">Windows PowerShell detects file system drives that are added or removed in Windows, including network drives that are mapped, USB drives that are attached, and drives that are deleted by using either the **net use** command or the **WScript.NetworkMapNetworkDrive** and **RemoveNetworkDrive** methods from a Windows Script Host (WSH) script.</span></span>
