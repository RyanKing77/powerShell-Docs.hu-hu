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
# <a name="managing-windows-powershell-drives"></a>A Windows PowerShell kezelése meghajtók
A *Windows PowerShell meghajtót* hasonlóan a Windows PowerShellben a fájlrendszer meghajtóján keresztül elérhető adatok tárolási helyen található. A Windows PowerShell-szolgáltatók néhány meghajtó hozza létre, mint például a fájl-meghajtók (beleértve a C: és D:), a beállításjegyzék meghajtók (HKCU: és HKLM:), és a tanúsítvány meghajtó (Cert:), és létrehozhat saját Windows PowerShell-meghajtókat. Ezek a meghajtók nagyon hasznosak, de csak a Windows PowerShell belül elérhetők. Nem érhetők el azokat a Windows más eszközeit, például a Fájlkezelőben vagy a Cmd.exe.

A Windows PowerShell használja a főnév **PSDrive**, a Windows PowerShell paranccsal meghajtók. Az a Windows PowerShell listáját a Windows PowerShell-munkamenetben meghajtók, használja a **Get-PSDrive** parancsmag.

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

Noha a jelennek meg a meghajtó a meghajtók, a rendszer, a listaelem alábbihoz hasonlóan fog megjelenni a kimenetét a **Get-PSDrive** fenti parancsot.

Fájl rendszermeghajtók megtalálhatók a Windows PowerShell meghajtót. Azonosíthatja, hogy a fájl rendszermeghajtók által a szolgáltató oszlop fájlrendszer bejegyzése. (A Windows PowerShell FileSystem szolgáltató által a Windows PowerShellben a fájl rendszermeghajtók támogatott.)

Által használt szintaxis megtekintéséhez a **Get-PSDrive** parancsmag, adjon meg egy **Get-Command** parancsot a **szintaxis** paraméter:

```
PS> Get-Command -Name Get-PSDrive -Syntax
Get-PSDrive [[-Name] <String[]>] [-Scope <String>] [-PSProvider <String[]>] [-V
erbose] [-Debug] [-ErrorAction <ActionPreference>] [-ErrorVariable <String>] [-
OutVariable <String>] [-OutBuffer <Int32>]
```

A **PSProvider** paraméter megadható, hogy csak a Windows PowerShell-meghajtók megjeleníti egy adott szolgáltató által támogatott. Csak a Windows PowerShell-meghajtókat, amelyek a Windows PowerShell FileSystem szolgáltató által támogatott megjelenítéséhez írja be például a **Get-PSDrive** parancsot a **PSProvider** paraméter és a  **Fájlrendszer** érték:

```
PS> Get-PSDrive -PSProvider FileSystem

Name       Provider      Root                                   CurrentLocation
----       --------      ----                                   ---------------
A          FileSystem    A:\
C          FileSystem    C:\                           ...nd Settings\PowerUser
D          FileSystem    D:\
```

A Windows PowerShell-meghajtókat, amelyek megfelelnek a beállításjegyzék-struktúra megtekintéséhez használja a **PSProvider** paraméter csak a Windows PowerShell-meghajtók jelenik meg, hogy a Windows PowerShell beállításjegyzék-szolgáltató által támogatott:

<pre>PS> Get-PSDrive -PSProvider Registry
Name       Provider      Root                                   CurrentLocation
----       --------      ----                                   ---------------
HKCU       Registry      HKEY_CURRENT_USER
HKLM       Registry      HKEY_LOCAL_MACHINE</pre>

A Windows PowerShell-meghajtókon is használhatja a szabványos hely parancsmagokat:

<pre>PS> Set-Location HKLM:\SOFTWARE
PS> Push-Location .\Microsoft
PS> Get-Location
Path
----
HKLM:\SOFTWARE\Microsoft</pre>

### <a name="adding-new-windows-powershell-drives-new-psdrive"></a>Hozzáadása az új Windows PowerShell-meghajtók (új PSDrive)
A Windows PowerShell meghajtót használatával adhat hozzá a **New-PSDrive** parancsot. A szintaxisának lekérése a **New-PSDrive** parancsot, írja be a **Get-Command** parancsot a **szintaxis** paraméter:

```
PS> Get-Command -Name New-PSDrive -Syntax
New-PSDrive [-Name] <String> [-PSProvider] <String> [-Root] <String> [-Descript
ion <String>] [-Scope <String>] [-Credential <PSCredential>] [-Verbose] [-Debug
] [-ErrorAction <ActionPreference>] [-ErrorVariable <String>] [-OutVariable <St
ring>] [-OutBuffer <Int32>] [-WhatIf] [-Confirm]
```

Hozzon létre egy új Windows PowerShell meghajtót, meg kell adnia három paramétert:

- (Használhat bármilyen érvényes Windows PowerShell-név) a meghajtó nevét

- A PSProvider (használja a rendszer fájlhelyek "FileSystem" és "Beállításjegyzék" beállításjegyzék-helyek esetében)

- A gyökérszintű, ez azt jelenti, hogy a legfelső szintű az új meghajtó elérési útja

Például létrehozhat egy nevű "Office" a Microsoft Office-alkalmazásokat, például a tartalmazó mappa leképezett meghajtót **C:\\Program Files\\Microsoft Office\\OFFICE11**. A meghajtó, írja be a következő parancsot:

```
PS> New-PSDrive -Name Office -PSProvider FileSystem -Root "C:\Program Files\Micr
osoft Office\OFFICE11"

Name       Provider      Root                                   CurrentLocation
----       --------      ----                                   ---------------
Office     FileSystem    C:\Program Files\Microsoft Offic...
```

> [!NOTE]
> Általában az elérési utak csak kis-és nagybetűket.

Az új Windows PowerShell meghajtót az összes Windows PowerShell-meghajtó – egy kettőspontot a név által módon hivatkozik (**:**).

A Windows PowerShell meghajtót számos feladatot tehet jóval egyszerűbbé válik. Például a Windows beállításjegyzékében legfontosabb kulcsok rendelkeznek rendkívül hosszú elérési utak, nehézkes lehet hozzáférési és nehéz megjegyezni minősítené. Fontos konfigurációs adatok alatt található **HKEY_LOCAL_MACHINE\\szoftver\\Microsoft\\Windows\\CurrentVersion**. - És CurrentVersion beállításkulcs, létrehozhat egy Windows PowerShell meghajtót, feltörték a kulcs írja be:

<pre>PS> New-PSDrive -Name cvkey -PSProvider Registry -Root HKLM\Software\Microsoft\W
indows\CurrentVersion
Name       Provider      Root                                   CurrentLocation
----       --------      ----                                   ---------------
cvkey      Registry      HKLM\Software\Microsoft\Windows\...</pre>

Módosíthatja a helyet, a **cvkey:** meghajtó, mint bármilyen más meghajtóról: "

`PS> cd cvkey:`

vagy:

<pre>PS> Set-Location cvkey: -PassThru
Path
----
cvkey:\</pre>

A New-PsDrive parancsmag ad hozzá az új meghajtó csak az aktuális Windows PowerShell-munkamenetben. Ha bezárja a Windows PowerShell-ablakot, az új meghajtó elveszik. Ha a Windows PowerShell-meghajtót, az Export-konzol parancsmag segítségével exportálhatja az aktuális Windows PowerShell-munkamenetet, és használja a PowerShell.exe **PSConsoleFile** paraméter importálnia. Vagy az új meghajtó hozzáadása a Windows PowerShell-profilhoz.

### <a name="deleting-windows-powershell-drives-remove-psdrive"></a>Törli a Windows PowerShell-meghajtók (Remove-PSDrive)
Ön meghajtókat a Windows PowerShell használatával törölheti a **Remove-PSDrive** parancsmag. A **Remove-PSDrive** parancsmag könnyen használható, egy adott Windows PowerShell meghajtót törölni, csak meg a Windows PowerShell meghajtót nevet.

Például, ha hozzáadta a **Office:** Windows PowerShell meghajtót, ahogy az a **New-PSDrive** témakör, törölheti a beírásával:

```
PS> Remove-PSDrive -Name Office
```

Törli a **cvkey:** Windows PowerShell meghajtót, is látható a **New-PSDrive** témakör, használja a következő parancsot:

```
PS> Remove-PSDrive -Name cvkey
```

A Windows PowerShell meghajtót törölheti, de nem törölhető, amíg a meghajtó. Például:

```
PS> cd office:
PS Office:\> remove-psdrive -name office
Remove-PSDrive : Cannot remove drive 'Office' because it is in use.
At line:1 char:15
+ remove-psdrive  <<<< -name office
```

### <a name="adding-and-removing-drives-outside-windows-powershell"></a>-Meghajtók kívül a Windows PowerShell hozzáadása és eltávolítása
A Windows PowerShell hozzáadásakor vagy eltávolításakor a Windowsban, beleértve a csatlakoztatott hálózati meghajtók, a csatlakoztatott USB-meghajtók és a meghajtók használatával vagy törölt fájl rendszermeghajtók észleli a **használata net** parancs vagy a  **WScript.NetworkMapNetworkDrive** és **RemoveNetworkDrive** módszerek a Windows Script Host (WSH) parancsfájlt.

