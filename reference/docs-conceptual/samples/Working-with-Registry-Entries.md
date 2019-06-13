---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: Beállításjegyzék-bejegyzések használata
ms.openlocfilehash: c1fd6f57f13240eb2039f2d5756796678800aee0
ms.sourcegitcommit: a6f13c16a535acea279c0ddeca72f1f0d8a8ce4c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2019
ms.locfileid: "67030733"
---
# <a name="working-with-registry-entries"></a>Beállításjegyzék-bejegyzések használata

Mivel a beállításjegyzék-bejegyzések tulajdonságok kulcsokat, és mint ilyen, nem közvetlenül tallózható, ha a velük végzett munkát egy némileg eltérő megközelítést kell.

## <a name="listing-registry-entries"></a>Beállításjegyzék-bejegyzések listája

Nincsenek számos különböző módon megvizsgálhatja a beállításjegyzékbeli bejegyzéseket. A legegyszerűbb módja, hogy a kulcshoz társított tulajdonságnevek kap. Például ahhoz, hogy a beállításkulcs bejegyzések `HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion`, használjon `Get-Item`. Beállításkulcsok rendelkezik egy tulajdonságot "Property" általános nevét, amely az a kulcsot a beállításjegyzék-bejegyzések listája.
A következő parancsot a tulajdonság tulajdonság kiválasztása, és kibontja az elemeket, hogy egy listában jelennek:

```powershell
Get-Item -Path Registry::HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion |
  Select-Object -ExpandProperty Property
```

```Output
DevicePath
MediaPathUnexpanded
ProgramFilesDir
CommonFilesDir
ProductId
```

A beállításjegyzék-bejegyzések olvashatóbb formátumban megtekintéséhez használja `Get-ItemProperty`:

```powershell
Get-ItemProperty -Path Registry::HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion
```

```Output
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

A Windows PowerShell biztonsággal kapcsolatos tulajdonságok a kulcshoz tartozó összes előtaggal van "PS", mint például **PSPath**, **PSParentPath**, **PSChildName**, és **PSProvider** .

Használhatja a `*.*` jelölése címre az aktuális helyét. Használhat `Set-Location` módosítani a **CurrentVersion** registry container első:

```powershell
Set-Location -Path Registry::HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion
```

Másik lehetőségként használhatja a beépített HKLM PSDrive az `Set-Location`:

```powershell
Set-Location -Path hklm:\SOFTWARE\Microsoft\Windows\CurrentVersion
```

Ezután a `*.*` jelöléssel aktuális helyének teljes elérési út megadása nélkül a tulajdonságok listázásához:

```powershell
Get-ItemProperty -Path .
```

```Output
...
DevicePath          : C:\WINDOWS\inf
MediaPathUnexpanded : C:\WINDOWS\Media
ProgramFilesDir     : C:\Program Files
...
```

Elérési út bővítése működik ugyanaz, mint a fájlrendszeren belüli ennek a helynek, így a **ItemProperty** listázásakor `HKLM:\SOFTWARE\Microsoft\Windows\Help` használatával `Get-ItemProperty -Path ..\Help`.

## <a name="getting-a-single-registry-entry"></a>Egyetlen bejegyzés beolvasása

Ha szeretné lekérdezni egy adott bejegyzést egy beállításkulcsot, több lehetséges módszer egyikét használhatja. Ebben a példában találja értékét **DevicePath** a `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion`.

Használatával `Get-ItemProperty`, használja a **elérési** paraméterrel adja meg annak a kulcsnak a nevét, és a **neve** paramétert adja meg a nevét a **DevicePath** bejegyzés.

```powershell
Get-ItemProperty -Path HKLM:\Software\Microsoft\Windows\CurrentVersion -Name DevicePath
```

```Output
PSPath       : Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\Software\
               Microsoft\Windows\CurrentVersion
PSParentPath : Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\Software\
               Microsoft\Windows
PSChildName  : CurrentVersion
PSDrive      : HKLM
PSProvider   : Microsoft.PowerShell.Core\Registry
DevicePath   : C:\WINDOWS\inf
```

Ez a parancs visszaadja a standard szintű Windows PowerShell tulajdonságait, valamint a **DevicePath** tulajdonság.

> [!NOTE]
> Bár a `Get-ItemProperty` rendelkezik **szűrő**, **Belefoglalás**, és **kizárása** paraméterek, nem használható a név tulajdonság szerint szűrheti. Tekintse meg ezeket a paramétereket beállításkulcsokról, amelyek elem elérési utak és nem a beállításjegyzék-bejegyzések. Beállításjegyzék-bejegyzések, amelyek elem tulajdonságai.

Egy másik lehetőség, hogy a Reg.exe parancssori eszközzel. Segítségre van szüksége a reg.exe, írja be a következőt `reg.exe /?` parancsot a parancssorba. A DevicePath bejegyzés megkereséséhez használja reg.exe, ahogyan az alábbi parancsot:

```powershell
reg query HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion /v DevicePath
```

```Output
! REG.EXE VERSION 3.0

HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion
    DevicePath  REG_EXPAND_SZ   %SystemRoot%\inf
```

Is használhatja a **WshHej** COM-objektum is található egyes beállításjegyzék-bejegyzések, bár ez a módszer nem működik nagy mennyiségű bináris adatot, vagy a beállításjegyzék-bejegyzések neve, amely tartalmazhat, mint például "\\"). A tulajdonságnév hozzáfűzése a nézetelem elérési útja a egy \\ elválasztó:

```powershell
(New-Object -ComObject WScript.Shell).RegRead("HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\DevicePath")
```

```Output
%SystemRoot%\inf
```

## <a name="setting-a-single-registry-entry"></a>Egyetlen bejegyzés beállítása

Ha szeretné módosítani egy adott bejegyzést egy beállításkulcsot, több lehetséges módszer egyikét használhatja. Ez a példa módosítja a **elérési** bejegyzés alatt `HKEY_CURRENT_USER\Environment`. A **elérési út** bejegyzés határozza meg, hogy hol található a végrehajtható fájlokat.

1. Az aktuális értéket, a **elérési** bejegyzés használatával `Get-ItemProperty`.
2. Adja hozzá az új értéket, és megadhat, az azt egy `;`.
3. Használat `Set-ItemProperty` a megadott kulcs, bejegyzés neve és értéke módosíthatja a beállításjegyzék-bejegyzést.

```powershell
$value = Get-ItemProperty -Path HKCU:\Environment -Name Path
$newpath = $value.Path += ";C:\src\bin\"
Set-ItemProperty -Path HKCU:\Environment -Name Path -Value $newpath
```

> [!NOTE]
> Bár a `Set-ItemProperty` rendelkezik **szűrő**, **Belefoglalás**, és **kizárása** paraméterek, nem használható a név tulajdonság szerint szűrheti. Tekintse meg ezeket a paramétereket beállításkulcsok – elem elérési utak minősülő – és nem a beállításjegyzék-bejegyzések – amelyeket elem tulajdonságai.

Egy másik lehetőség, hogy a Reg.exe parancssori eszközzel. Segítségre van szüksége a reg.exe, írja be a következőt **reg.exe /?**
a parancssorba.

A következő példát módosítások a **elérési út** bejegyzés az elérési út hozzáadása a fenti példában eltávolításával.
`Get-ItemProperty` továbbra is a jelenlegi érték elemzése a által visszaadott karakterlánc ne kelljen beolvasásához használt `reg query`. A **SubString** és **LastIndexOf** módszerek használhatók a hozzáadott utolsó elérési beolvasni a **elérési út** bejegyzés.

```powershell
$value = Get-ItemProperty -Path HKCU:\Environment -Name Path
$newpath = $value.Path.SubString(0, $value.Path.LastIndexOf(';'))
reg add HKCU\Environment /v Path /d $newpath /f
```

```Output
The operation completed successfully.
```

## <a name="creating-new-registry-entries"></a>Új beállításjegyzék-bejegyzések létrehozása

"PowerShellPath" nevű új bejegyzés hozzáadása a **CurrentVersion** fő, használati `New-ItemProperty` az elérési útját a kulcsot, a bejegyzés neve és a bejegyzés értéke. Ebben a példában azt vesz igénybe a Windows PowerShell-változó értékét `$PSHome`, amely a telepítési könyvtár elérési útját tárolja a Windows PowerShell környezethez.

Adhat hozzá az új bejegyzést a kulcs a következő paranccsal, és a parancs is információval szolgál az új bejegyzést:

```powershell
New-ItemProperty -Path HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion -Name PowerShellPath -PropertyType String -Value $PSHome
```

```Output
PSPath         : Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion
PSParentPath   : Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows
PSChildName    : CurrentVersion
PSDrive        : HKLM
PSProvider     : Microsoft.PowerShell.Core\Registry
PowerShellPath : C:\Program Files\Windows PowerShell\v1.0
```

A **%d{PropertyType/** nevének kell lennie egy **Microsoft.Win32.RegistryValueKind** enumerálási tag a következő táblázatból:

|%D{PropertyType/ érték|Jelentés|
|----------------------|-----------|
|Bináris|Bináris adatok|
|DWord|Egy szám, amely egy érvényes UInt32|
|ExpandString|Egy karakterlánc, amely dinamikusan bontva környezeti változókat is tartalmazhat.|
|MultiString|Egy többsoros karakterlánc|
|Sztring|bármilyen karakterlánc típusú értéket|
|QWord|8 bájtos bináris adatok|

> [!NOTE]
> Adjon meg egy olyan értéktömböt a több helyre egy beállításjegyzékbeli bejegyzést is hozzáadhat a **elérési út** paramétert:

```powershell
New-ItemProperty -Name PowerShellPath -PropertyType String -Value $PSHome `
  -Path HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion, HKCU:\SOFTWARE\Microsoft\Windows\CurrentVersion
```

Egy már meglévő beállításazonosító bejegyzés hozzáadásával is felülírhatja a **kényszerített** paraméter sem `New-ItemProperty` parancsot.

## <a name="renaming-registry-entries"></a>Beállításjegyzék-bejegyzések átnevezése

Átnevezi a **PowerShellPath** bejegyzést a "PSHome," használata `Rename-ItemProperty`:

```powershell
Rename-ItemProperty -Path HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion -Name PowerShellPath -NewName PSHome
```

Átnevezett értéket jeleníti meg, adja hozzá a **PassThru** paramétert a parancshoz.

```powershell
Rename-ItemProperty -Path HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion -Name PowerShellPath -NewName PSHome -passthru
```

## <a name="deleting-registry-entries"></a>Beállításjegyzék-bejegyzések törlése

A PSHome és a PowerShellPath beállításjegyzék-bejegyzések törléséhez használja `Remove-ItemProperty`:

```powershell
Remove-ItemProperty -Path HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion -Name PSHome
Remove-ItemProperty -Path HKCU:\SOFTWARE\Microsoft\Windows\CurrentVersion -Name PowerShellPath
```
