---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: Windows PowerShell-meghajtók kezelése
ms.assetid: bd809e38-8de9-437a-a250-f30a667d11b4
ms.openlocfilehash: 9ac5136fb28b450ea6397cab2f36082c50f22e1f
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62057825"
---
# <a name="managing-windows-powershell-drives"></a>Windows PowerShell-meghajtók kezelése

A *Windows PowerShell meghajtót* egy tároló hely, például a Windows PowerShellben a fájlrendszer meghajtóján keresztül elérhető. A Windows PowerShell-szolgáltatók néhány meghajtó hozza létre, például a fájlrendszer meghajtók (beleértve a C: és D:), a beállításjegyzék meghajtók (HKCU: és HKLM:), és a tanúsítvány-meghajtó (Cert:), és létrehozhatja a saját Windows PowerShell-meghajtók. Ezek a meghajtók nagyon hasznos, de csak a Windows PowerShell belül elérhetők legyenek. Nem érhetők el azokat más Windows-eszközök, például a Cmd.exe vagy a fájlkezelő használatával.

Windows PowerShell használja a főnév **PSDrive**, parancsok, amelyek a Windows PowerShell-lel dolgozni meghajtók. A listáját a Windows PowerShell meghajtót a Windows PowerShell-munkamenetben, használja a **Get-PSDrive** parancsmagot.

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

Bár a meghajtók, a megjelenő információk a rendszer a meghajtók számától függ, a listaelem láthatóhoz fog hasonlítani a kimenetét a **Get-PSDrive** fenti parancsot.

Fájl rendszermeghajtók megtalálhatók a Windows PowerShell meghajtót. A fájl rendszermeghajtók a fájlrendszer-bejegyzést a szolgáltató oszlop alapján azonosíthatja. (A Windows PowerShellben a fájl rendszermeghajtók támogatottak a Windows PowerShell fájlrendszer-szolgáltatót.)

Szintaxisának megtekintéséhez a **Get-PSDrive** parancsmagot, adjon meg egy **Get-Command** parancsot a **szintaxis** paramétert:

```
PS> Get-Command -Name Get-PSDrive -Syntax

Get-PSDrive [[-Name] <String[]>] [-Scope <String>] [-PSProvider <String[]>] [-V
erbose] [-Debug] [-ErrorAction <ActionPreference>] [-ErrorVariable <String>] [-
OutVariable <String>] [-OutBuffer <Int32>]
```

A **PSProvider** paraméter lehetővé teszi, hogy csak azok a Windows PowerShell-meghajtók jelenjenek meg az egyes szolgáltatók által támogatott. Ha például csak a Windows PowerShell fájlrendszer szolgáltató által támogatott Windows PowerShell meghajtót megjelenítéséhez írja be egy **Get-PSDrive** parancsot a **PSProvider** paraméter és a  **Fájlrendszer** érték:

```
PS> Get-PSDrive -PSProvider FileSystem

Name       Provider      Root                                   CurrentLocation
----       --------      ----                                   ---------------
A          FileSystem    A:\
C          FileSystem    C:\                           ...nd Settings\PowerUser
D          FileSystem    D:\
```

A beállításjegyzék-struktúrát képviselő Windows PowerShell-meghajtók megtekintéséhez használja a **PSProvider** paraméter csak a Windows PowerShell-meghajtók jelenik meg, hogy a Windows PowerShell beállításjegyzék-szolgáltatója által támogatott:

```
PS> Get-PSDrive -PSProvider Registry

Name       Provider      Root                                   CurrentLocation
----       --------      ----                                   ---------------
HKCU       Registry      HKEY_CURRENT_USER
HKLM       Registry      HKEY_LOCAL_MACHINE
```

A szabványos helyre parancsmagok a Windows PowerShell-meghajtók is használhatja:

```
PS> Set-Location HKLM:\SOFTWARE
PS> Push-Location .\Microsoft
PS> Get-Location

Path
----
HKLM:\SOFTWARE\Microsoft
```

## <a name="adding-new-windows-powershell-drives-new-psdrive"></a>Hozzáadás, új Windows PowerShell-meghajtók (új PSDrive)

A saját Windows PowerShell-meghajtók használatával adhat hozzá a **New-PSDrive** parancsot. A szintaxisának lekérése a **New-PSDrive** parancshoz, írja be a **Get-Command** parancsot a **szintaxis** paramétert:

```
PS> Get-Command -Name New-PSDrive -Syntax

New-PSDrive [-Name] <String> [-PSProvider] <String> [-Root] <String> [-Descript
ion <String>] [-Scope <String>] [-Credential <PSCredential>] [-Verbose] [-Debug
] [-ErrorAction <ActionPreference>] [-ErrorVariable <String>] [-OutVariable <St
ring>] [-OutBuffer <Int32>] [-WhatIf] [-Confirm]
```

Hozzon létre egy új Windows PowerShell meghajtót, három paramétert kell megadnia:

- A meghajtó (bármilyen érvényes Windows PowerShell-nevet is használ) nevét

- A PSProvider (használja a "Fájlrendszer" fájlrendszerbeli helyeken és a "Beállításjegyzék" beállításjegyzék-helyeken a)

- A legfelső szintű, a legfelső szintű, az új meghajtó elérési útja

Például létrehozhat egy nevű, "Office", mint például a számítógépre, a Microsoft Office-alkalmazásokat tartalmazó mappát leképezett meghajtót **C:\\Program Files\\a Microsoft Office\\OFFICE11**. Hozza létre a meghajtót, írja be a következő parancsot:

```
PS> New-PSDrive -Name Office -PSProvider FileSystem -Root "C:\Program Files\Micr
osoft Office\OFFICE11"

Name       Provider      Root                                   CurrentLocation
----       --------      ----                                   ---------------
Office     FileSystem    C:\Program Files\Microsoft Offic...
```

> [!NOTE]
> Általánosságban véve az elérési utakat nem kis-és nagybetűket.

Az új Windows PowerShell meghajtót mint Önnek az összes Windows PowerShell-meghajtó – egy kettőspontot a név alapján hivatkozhat (**:**).

A Windows PowerShell meghajtót számos feladatot teheti sokkal egyszerűbbek. Például néhány, a legfontosabb kulcsokat, a Windows beállításjegyzékben kell rendkívül hosszú elérési utak teszi őket a hozzáférés nehézkes és nehezen ne felejtse el. Nagyon fontos konfigurációs adatok alatt találhatók **HKEY_LOCAL_MACHINE\\szoftver\\Microsoft\\Windows\\CurrentVersion**. Megtekintése és módosítása CurrentVersion beállításkulcs elemek, hozhat létre egy Windows PowerShell meghajtót, amely feltörték ezt a kulcsot a beírásával:

```
PS> New-PSDrive -Name cvkey -PSProvider Registry -Root HKLM\Software\Microsoft\W
indows\CurrentVersion

Name       Provider      Root                                   CurrentLocation
----       --------      ----                                   ---------------
cvkey      Registry      HKLM\Software\Microsoft\Windows\...
```

Ezt követően módosíthatja a helyet a **cvkey:** meghajtó, mint bármilyen más meghajtóról:''

`PS> cd cvkey:`

vagy:

```
PS> Set-Location cvkey: -PassThru

Path
----
cvkey:\
```

A New-PsDrive parancsmag hozzáadja az új meghajtó csak az aktuális Windows PowerShell-munkamenetben. Ha bezárja a Windows PowerShell-ablakot, az új meghajtó elveszik. Szeretné menteni egy Windows PowerShell meghajtót, az Export-konzol parancsmaggal exportálhatja a jelenlegi Windows PowerShell-munkamenetet, és használja a PowerShell.exe **PSConsoleFile** paraméter importálásához. Vagy az új meghajtó felvétele a Windows PowerShell-profilt.

## <a name="deleting-windows-powershell-drives-remove-psdrive"></a>Törlése a Windows PowerShell-meghajtók (Remove-PSDrive)

A Windows powershellből meghajtók segítségével törölheti a **Remove-PSDrive** parancsmagot. A **Remove-PSDrive** parancsmag könnyen használható; Ha törölni szeretné egy adott Windows PowerShell-meghajtón, csak megadni a Windows PowerShell-meghajtó nevét.

Például, ha hozzáadta a **Office:** Windows PowerShell meghajtót, ahogyan az a **New-PSDrive** témakör, törölheti azt írja be:

```powershell
Remove-PSDrive -Name Office
```

Törli a **cvkey:** Windows PowerShell-meghajtó, is látható a **New-PSDrive** témakörben, használja a következő parancsot:

```powershell
Remove-PSDrive -Name cvkey
```

Egyszerűen törölni egy Windows PowerShell meghajtót, de nem törölhető, amíg a meghajtó. Például:

```
PS> cd office:
PS Office:\> remove-psdrive -name office
Remove-PSDrive : Cannot remove drive 'Office' because it is in use.
At line:1 char:15
+ remove-psdrive  <<<< -name office
```

## <a name="adding-and-removing-drives-outside-windows-powershell"></a>-Meghajtók kívül a Windows PowerShell hozzáadása és eltávolítása

Windows PowerShell hozzáadásakor vagy eltávolításakor a Windows, beleértve a csatlakoztatott hálózati meghajtók, a csatlakoztatott USB-meghajtók és a meghajtók, a törölt fájl rendszermeghajtók észleli a **használata net** parancsot vagy a  **WScript.NetworkMapNetworkDrive** és **RemoveNetworkDrive** módszerek a Windows Script Host (WSH) parancsfájlt.