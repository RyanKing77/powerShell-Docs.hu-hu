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
# <a name="managing-windows-powershell-drives"></a>Windows PowerShell-meghajtók kezelése

A *Windows PowerShell meghajtó* egy adattár-hely, amely a Windows PowerShellben található fájlrendszer-meghajtóhoz is hozzáférhet. A Windows PowerShell-szolgáltatók létrehoznak néhány meghajtót az Ön számára, például a fájlrendszer meghajtóit (beleértve a C: és a D:), a beállításjegyzék-meghajtókat (HKCU: és HKLM:) és a tanúsítvány meghajtóját (CERT:), és létrehozhat saját Windows PowerShell-meghajtókat is. Ezek a meghajtók nagyon hasznosak, de csak a Windows PowerShellben érhetők el. Nem érheti el őket más Windows-eszközök, például a fájlkezelő vagy a cmd. exe használatával.

A Windows PowerShell a **PSDrive**, a Windows PowerShell-meghajtókkal működő parancsok esetében a főnévot használja. A Windows PowerShell-munkamenetben található Windows PowerShell-meghajtók listáját a **Get-PSDrive** parancsmaggal teheti meg.

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

Bár a kijelzőn lévő meghajtók a rendszeren található meghajtóktól eltérőek, a lista a fent látható **Get-PSDrive** parancs kimenetéhez hasonlóan fog kinézni.

A fájlrendszer-meghajtók a Windows PowerShell-meghajtók egy részhalmaza. A fájlrendszer meghajtóit a szolgáltató oszlopban található fájlrendszer-bejegyzés alapján azonosíthatja. (A Windows PowerShell fájlrendszer-meghajtóit a Windows PowerShell fájlrendszer-szolgáltatója támogatja.)

A **Get-PSDrive** parancsmag szintaxisának megtekintéséhez írja be a **Get-Command** parancsot a **szintaxis** paraméterrel:

```
PS> Get-Command -Name Get-PSDrive -Syntax

Get-PSDrive [[-Name] <String[]>] [-Scope <String>] [-PSProvider <String[]>] [-V
erbose] [-Debug] [-ErrorAction <ActionPreference>] [-ErrorVariable <String>] [-
OutVariable <String>] [-OutBuffer <Int32>]
```

A **PSProvider** paraméter lehetővé teszi, hogy csak az adott szolgáltató által támogatott Windows PowerShell-meghajtókat jelenítse meg. Ha például csak a Windows PowerShell fájlrendszer-szolgáltató által támogatott Windows PowerShell-meghajtókat szeretné megjeleníteni, írja be a **Get-PSDrive** parancsot a **PSProvider** paraméterrel és a **fájlrendszer** értékével:

```
PS> Get-PSDrive -PSProvider FileSystem

Name       Provider      Root                                   CurrentLocation
----       --------      ----                                   ---------------
A          FileSystem    A:\
C          FileSystem    C:\                           ...nd Settings\PowerUser
D          FileSystem    D:\
```

A beállításjegyzék-struktúrákat képviselő Windows PowerShell-meghajtók megtekintéséhez használja a **PSProvider** paramétert a Windows PowerShell beállításjegyzék-szolgáltató által támogatott Windows PowerShell-meghajtók megjelenítéséhez:

```
PS> Get-PSDrive -PSProvider Registry

Name       Provider      Root                                   CurrentLocation
----       --------      ----                                   ---------------
HKCU       Registry      HKEY_CURRENT_USER
HKLM       Registry      HKEY_LOCAL_MACHINE
```

A standard Location parancsmagokat a Windows PowerShell-meghajtókkal is használhatja:

```
PS> Set-Location HKLM:\SOFTWARE
PS> Push-Location .\Microsoft
PS> Get-Location

Path
----
HKLM:\SOFTWARE\Microsoft
```

## <a name="adding-new-windows-powershell-drives-new-psdrive"></a>Új Windows PowerShell-meghajtók hozzáadása (New-PSDrive)

A **New-PSDrive** parancs használatával saját Windows PowerShell-meghajtókat is hozzáadhat. A **New-PSDrive** parancs szintaxisának lekéréséhez írja be a **Get-Command** parancsot a **szintaxis** paraméterrel:

```
PS> Get-Command -Name New-PSDrive -Syntax

New-PSDrive [-Name] <String> [-PSProvider] <String> [-Root] <String> [-Descript
ion <String>] [-Scope <String>] [-Credential <PSCredential>] [-Verbose] [-Debug
] [-ErrorAction <ActionPreference>] [-ErrorVariable <String>] [-OutVariable <St
ring>] [-OutBuffer <Int32>] [-WhatIf] [-Confirm]
```

Új Windows PowerShell-meghajtó létrehozásához három paramétert kell megadnia:

- A meghajtó neve (bármilyen érvényes Windows PowerShell-nevet használhat)

- A PSProvider (a "fájlrendszer" használata a beállításjegyzék helyein a fájlrendszerbeli és a beállításjegyzékben)

- A gyökér, azaz az új meghajtó gyökerének elérési útja

Létrehozhat például egy "Office" nevű meghajtót, amely a számítógépen Microsoft Office alkalmazást tartalmazó mappához van rendelve, például **C:\\program\\Files\\Microsoft Office Office11**. A meghajtó létrehozásához írja be a következő parancsot:

```
PS> New-PSDrive -Name Office -PSProvider FileSystem -Root "C:\Program Files\Microsoft Office\OFFICE11"

Name       Provider      Root                                   CurrentLocation
----       --------      ----                                   ---------------
Office     FileSystem    C:\Program Files\Microsoft Offic...
```

> [!NOTE]
> Az elérési utak általában nem megkülönböztetik a kis-és nagybetűket.

Az új Windows PowerShell-meghajtót az összes Windows PowerShell-meghajtón tekintheti meg – a neve után egy kettősponttal ( **:** ).

A Windows PowerShell-meghajtók sokkal egyszerűbben végezhetnek el sok feladatot. A Windows beállításjegyzék legfontosabb kulcsai például rendkívül hosszú elérési utakkal rendelkeznek, így nehézkes a hozzáférés és a nehezen megjegyezhető. A kritikus konfigurációs információk a **HKEY_LOCAL_MACHINE\\Software\\\\Microsoft\\Windows CurrentVersion**alatt találhatók. A CurrentVersion beállításkulcs elemeinek megtekintéséhez és módosításához hozzon létre egy olyan Windows PowerShell-meghajtót, amely az adott kulcsban gyökerezik a következő beírásával:

```
PS> New-PSDrive -Name cvkey -PSProvider Registry -Root HKLM\Software\Microsoft\Windows\CurrentVersion

Name       Provider      Root                                   CurrentLocation
----       --------      ----                                   ---------------
cvkey      Registry      HKLM\Software\Microsoft\Windows\...
```

Ezután megváltoztathatja a helyet a **cvkey:** meghajtóra, mint bármely más meghajtót:

```
PS> cd cvkey:
```

vagy:

```
PS> Set-Location cvkey: -PassThru

Path
----
cvkey:\
```

A New-PsDrive parancsmag csak az aktuális Windows PowerShell-munkamenethez adja hozzá az új meghajtót. Ha bezárta a Windows PowerShell ablakát, az új meghajtó elvész. Windows PowerShell-meghajtó mentéséhez használja az export-Console parancsmagot az aktuális Windows PowerShell-munkamenet exportálásához, majd a PowerShell. exe **PSConsoleFile** paraméter használatával importálja. Vagy adja hozzá az új meghajtót a Windows PowerShell-profilhoz.

## <a name="deleting-windows-powershell-drives-remove-psdrive"></a>Windows PowerShell-meghajtók törlése (remove-PSDrive)

A **Remove-PSDrive** parancsmag használatával törölheti a meghajtókat a Windows powershellből. A **Remove-PSDrive** parancsmag egyszerűen használható; egy adott Windows PowerShell-meghajtó törléséhez csak adja meg a Windows PowerShell-meghajtó nevét.

Ha például hozzáadta az **irodát:** Windows PowerShell-meghajtó, ahogy az a **New-PSDrive** című témakörben is látható, a következő beírásával törölheti:

```powershell
Remove-PSDrive -Name Office
```

A cvkey törlése **:** Windows PowerShell meghajtó, a **New-PSDrive** című témakörben is látható, használja a következő parancsot:

```powershell
Remove-PSDrive -Name cvkey
```

Egyszerűen törölheti a Windows PowerShell-meghajtót, de nem törölheti a meghajtót. Például:

```
PS> cd office:
PS Office:\> remove-psdrive -name office
Remove-PSDrive : Cannot remove drive 'Office' because it is in use.
At line:1 char:15
+ remove-psdrive  <<<< -name office
```

## <a name="adding-and-removing-drives-outside-windows-powershell"></a>Meghajtók hozzáadása és eltávolítása a Windows PowerShellen kívül

A Windows PowerShell észleli a Windowsban hozzáadott vagy eltávolított fájlrendszer-meghajtókat, beleértve a csatlakoztatott hálózati meghajtókat, a csatlakoztatott USB-meghajtókat, valamint a **net use** paranccsal vagy a **használatával törölt meghajtókat. WScript. NetworkMapNetworkDrive** és **RemoveNetworkDrive** metódusok egy Windows Script Host (WSH) parancsfájlból.
