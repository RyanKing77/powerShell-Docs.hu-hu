---
ms.date: 06/05/2017
keywords: PowerShell parancsmag
title: Beállításjegyzék-bejegyzések használata
ms.assetid: fd254570-27ac-4cc9-81d4-011afd29b7dc
ms.openlocfilehash: bffdf80931fc4dc570b584623487077dc5d449dc
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
ms.locfileid: "30952375"
---
# <a name="working-with-registry-entries"></a>Beállításjegyzék-bejegyzések használata

Mivel a beállításjegyzék-bejegyzések kulcsok tulajdonságainak, és mint ilyen, nem közvetlenül tallózható, igazolnia kell némileg eltérő megközelítést hajtson végre hozzájuk.

### <a name="listing-registry-entries"></a>Beállításjegyzék-bejegyzések listázása

Vizsgálja meg a beállításjegyzék-bejegyzések számos különböző módja van. A legegyszerűbb módja a beolvasni a tulajdonság nevét, a kulcshoz tartozó. Ahhoz, hogy a beállításkulcs bejegyzések például **HKEY_LOCAL_MACHINE\\szoftver\\Microsoft\\Windows\\CurrentVersion**, használjon **Get-elem** . Beállításkulcsok rendelkezik tulajdonsággal általános nevű, "Property" Ez a kulcs a beállításjegyzék-bejegyzések listáját. A következő parancsot a tulajdonság-tulajdonság kiválasztása, és kibontja az elemeket, hogy egy listán jelennek:

```
PS> Get-Item -Path Registry::HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion | Select-Object -ExpandProperty Property
DevicePath
MediaPathUnexpanded
ProgramFilesDir
CommonFilesDir
ProductId
```

Segítségével olvashatóbb formátumban tekintheti a beállításjegyzék-bejegyzések **Get-ItemProperty**:

```
PS> Get-ItemProperty -Path Registry::HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion

PSPath              : Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\SO
                      FTWARE\Microsoft\Windows\CurrentVersion
PSParentPath        : Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\SO
                      FTWARE\Microsoft\Windows
PSChildName         : CurrentVersion
PSDrive             : HKLM
PSProvider          : Microsoft.PowerShell.Core\Registry
DevicePath          : C:\WINDOWS\inf
MediaPathUnexpanded : C:\WINDOWS\Media
ProgramFilesDir     : C:\Program Files
CommonFilesDir      : C:\Program Files\Common Files
ProductId           : 76487-338-1167776-22465
WallPaperDir        : C:\WINDOWS\Web\Wallpaper
MediaPath           : C:\WINDOWS\Media
ProgramFilesPath    : C:\Program Files
PF_AccessoriesName  : Accessories
(default)           :
```

A kulcs a Windows PowerShell-kapcsolódó tulajdonságok vannak összes előzi meg a "PS", például a **PSPath**, **PSParentPath**, **PSChildName**, és **PSProvider** .

Használhatja a "**.**" jelölése a jelenlegi helyre hivatkozik. Használhat **hely beállítása** átállítása a **CurrentVersion** beállításjegyzék tároló első:

```powershell
Set-Location -Path Registry::HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion
```

Másik lehetőségként használhatja a beépített HKLM PSDrive rendelkező **hely beállítása**:

```powershell
Set-Location -Path hklm:\SOFTWARE\Microsoft\Windows\CurrentVersion
```

Ezután használhatja a "**.**" jelöléssel a jelenlegi helyhez egy teljes elérési út megadása nélkül a tulajdonságok listázásához:

```
PS> Get-ItemProperty -Path .
...
DevicePath          : C:\WINDOWS\inf
MediaPathUnexpanded : C:\WINDOWS\Media
ProgramFilesDir     : C:\Program Files
...
```

Elérési út bővítése ugyanúgy működik, mint a fájlrendszeren belül a következő helyről érheti a **ItemProperty** listázásakor **HKLM:\\szoftver\\Microsoft\\Windows \\Súgó** használatával **Get-ItemProperty-elérési út... \\Súgó**.

### <a name="getting-a-single-registry-entry"></a>Egyetlen bejegyzés beolvasása

Ha szeretné beolvasni egy meghatározott bejegyzés egy beállításkulcsot, több lehetséges módszer egyikét használhatja. Ebben a példában a értékének megkeresése **DevicePath** a **HKEY_LOCAL_MACHINE\\szoftver\\Microsoft\\Windows\\CurrentVersion**.

Használatával **Get-ItemProperty**, használja a **elérési** paraméterrel adhatja meg a kulcs nevét és a **neve** paraméterrel adhatja meg a nevét a **DevicePath** bejegyzés.

```
PS> Get-ItemProperty -Path HKLM:\Software\Microsoft\Windows\CurrentVersion -Name DevicePath

PSPath       : Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\Software\
               Microsoft\Windows\CurrentVersion
PSParentPath : Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\Software\
               Microsoft\Windows
PSChildName  : CurrentVersion
PSDrive      : HKLM
PSProvider   : Microsoft.PowerShell.Core\Registry
DevicePath   : C:\WINDOWS\inf
```

Ez a parancs visszaadja a szabványos Windows PowerShell tulajdonságait, valamint a **DevicePath** tulajdonság.

> [!NOTE]
> Bár **Get-ItemProperty** rendelkezik **szűrő**, **Include**, és **kizárása** paraméterek, a szűréshez tulajdonság neve nem használhatók. Ezek a paraméterek tekintse meg a beállításkulcsok – amelyeket elem elérési utak – és nem a beállításjegyzék-bejegyzések – amelyeket elem tulajdonságai.

Egy másik lehetőség, hogy a Reg.exe parancssori eszközt használja. Súgó a reg.exe, írja be a **reg.exe /?** parancsot a parancssorba. A DevicePath bejegyzés megkereséséhez használja reg.exe, ahogy az az alábbi parancsot:

```
PS> reg query HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion /v DevicePath

! REG.EXE VERSION 3.0

HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion
    DevicePath  REG_EXPAND_SZ   %SystemRoot%\inf
```

Használhatja a **WshHej COM** objektum is található egyes beállításjegyzék-bejegyzések, bár ez a módszer nem működik a nagy bináris adatok vagy a beállításjegyzék-bejegyzések neve, amely olyan karaktereket, mint például "\\"). Az elem elérési útját a tulajdonságnév hozzáfűzése egy \\ elválasztó:

```
PS> (New-Object -ComObject WScript.Shell).RegRead("HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\DevicePath")
%SystemRoot%\inf
```

### <a name="creating-new-registry-entries"></a>Új beállításjegyzék-bejegyzések létrehozása

"PowerShellPath" nevű új bejegyzés hozzáadása a **CurrentVersion** kulcshasználat, **New-ItemProperty** az elérési útját a kulcsot, a bejegyzés neve és a bejegyzés. Ehhez a példához most elindítjuk a Windows PowerShell-változó értékének **$PSHome**, amely a telepítési könyvtár elérési útjának tárolja a Windows PowerShell környezethez.

Az új bejegyzést adhat a kulcsot a következő paranccsal, és a parancs is az új bejegyzést információt ad vissza:

```
PS> New-ItemProperty -Path HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion -Name PowerShellPath -PropertyType String -Value $PSHome

PSPath         : Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\SOFTWAR
                 E\Microsoft\Windows\CurrentVersion
PSParentPath   : Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\SOFTWAR
                 E\Microsoft\Windows
PSChildName    : CurrentVersion
PSDrive        : HKLM
PSProvider     : Microsoft.PowerShell.Core\Registry
PowerShellPath : C:\Program Files\Windows PowerShell\v1.0
```

A **PropertyType típusa** nevének kell lennie egy **Microsoft.Win32.RegistryValueKind** enumerálási tag a következő táblázatból:

|PropertyType típusa érték|Jelentés|
|----------------------|-----------|
|Bináris|Bináris adatok|
|DWord|Egy szám, amely egy érvényes UInt32|
|ExpandString|Karakterlánc, amely dinamikusan bontva környezeti változókat is tartalmazhat.|
|Attribútummal rendelkező multistring karakterláncok|Egy többsoros karakterlánc|
|Karakterlánc|Bármilyen karakterlánc típusú értéket|
|QWord|8 bájtos bináris adatok|

> [!NOTE]
> Egy tömböt a megadásával több helyre egy beállításjegyzékbeli bejegyzést is hozzáadhat a **elérési** paraméter:

```powershell
New-ItemProperty -Path HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion, HKCU:\SOFTWARE\Microsoft\Windows\CurrentVersion -Name PowerShellPath -PropertyType String -Value $PSHome
```

Egy már meglévő beállításazonosítót bejegyzés hozzáadásával is felülírhatja a **kényszerített** bármelyik paraméter **New-ItemProperty** parancsot.

### <a name="renaming-registry-entries"></a>Beállításjegyzék-bejegyzések átnevezése

Átnevezi a **PowerShellPath** "PSHome," használata bejegyzést **Rename-ItemProperty**:

```powershell
Rename-ItemProperty -Path HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion -Name PowerShellPath -NewName PSHome
```

Az átnevezett értéket jeleníti meg, vegye fel a **PassThru** paramétert a parancshoz.

```powershell
Rename-ItemProperty -Path HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion -Name PowerShellPath -NewName PSHome -passthru
```

### <a name="deleting-registry-entries"></a>Beállításjegyzék-bejegyzések törlése

A PSHome és a PowerShellPath beállításjegyzék-bejegyzések törléséhez használja **Remove-ItemProperty**:

```powershell
Remove-ItemProperty -Path HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion -Name PSHome
Remove-ItemProperty -Path HKCU:\SOFTWARE\Microsoft\Windows\CurrentVersion -Name PowerShellPath
```