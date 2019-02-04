---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: Aktuális hely kezelése
ms.assetid: a9f9e7a7-3ea8-47d3-bbb4-6e437f6d4a4a
ms.openlocfilehash: d1ebc9507a45841e6d4d8219e45c002990e1328c
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55686508"
---
# <a name="managing-current-location"></a>Aktuális hely kezelése

A Fájlkezelőben mappa rendszerek navigáláskor általában rendelkeznek egy adott működő helyen -, az aktuális mappa megnyitása. Az aktuális mappa elemeinek rájuk kattintva könnyen kezelhetők. Tartozó parancssori felületek, például a Cmd.exe Ha egy adott fájl ugyanabban a mappában, elérheti adjon meg egy viszonylag rövid, nem pedig mintha meg kellene adnia a fájl teljes elérési útja. Az aktuális könyvtár neve a munkakönyvtárat.

Windows PowerShell használja a főnév **hely** lehet hivatkozni a munkakönyvtárban és valósítja meg a családba tartozó parancsmagok vizsgálja meg, és a hely kezeléséhez.

### <a name="getting-your-current-location-get-location"></a>Bevezetés az aktuális tartózkodási helyét (Get-hely)

Annak megállapításához, az aktuális könyvtár hely elérési útja, adja meg a **Get-Location** parancsot:

```
PS> Get-Location
Path
----
C:\Documents and Settings\PowerUser
```

> [!NOTE]
> A Get-Location parancsmag hasonlít a **pwd** parancs a bash. A hely beállítása parancsmag hasonlít a **cd** Cmd.exe parancsot.

### <a name="setting-your-current-location-set-location"></a>Az aktuális tartózkodási helyét (hely beállítása) beállítást

A **Get-Location** parancs szolgál a **hely beállítása** parancsot. A **hely beállítása** parancs lehetővé teszi, hogy adja meg az aktuális könyvtár helyet.

```powershell
Set-Location -Path C:\Windows
```

Miután megadta a parancs, megfigyelheti, hogy nem jelenik meg a parancs hatásáról közvetlen visszajelzést. A legtöbb Windows PowerShell-parancsokat, amelyek egy műveletet állít elő alig vagy egyáltalán nem kimenetet, mert a kimenet nem mindig lehet hasznos. Ellenőrizze, hogy sikeres directory módosítás történt a megadásakor a **hely beállítása** parancshoz, például a **- PassThru** paraméter megadásakor a **Set-Location**parancsot:

```
PS> Set-Location -Path C:\Windows -PassThru

Path
----
C:\WINDOWS
```

A **- PassThru** paraméter az eredmény információt ad vissza, amelyben nem nincs alapértelmezett kimenet esetekben használható a Windows PowerShell számos Set-parancsokkal.

Megadhat elérési utak viszonyított jelenlegi tartózkodási ugyanúgy szerint, akkor a legtöbb UNIX- és Windows parancs ismertetése. A relatív elérési utakat, a standard szintű jelölésrendszerben időszak (**.**) az aktuális mappában, és a egy doubled időszak jelöli (**...** ) szülőkönyvtára az aktuális tartózkodási helyét jelöli.

Például, ha a **C:\\Windows** mappa, pont (**.**) jelöli **C:\\Windows** és időszakok duplán (**...** ) képviselő **C:**. Módosíthatja az aktuális helyről a C: meghajtó gyökerébe beírásával:

```
PS> Set-Location -Path .. -PassThru

Path
----
C:\
```

Ugyanezen technika működik, amelyek nem akkor a fájl rendszert tartalmazó meghajtókon, például a Windows PowerShell-meghajtók **HKLM:**. A HKLM is beállíthatja az helyet\\szoftverkulcs írja be a beállításjegyzékben:

```
PS> Set-Location -Path HKLM:\SOFTWARE -PassThru

Path
----
HKLM:\SOFTWARE
```

Módosíthatja a könyvtár helye a a Windows PowerShell HKLM gyökere szülőkönyvtárhoz: meghajtó relatív elérési út használatával:

```
PS> Set-Location -Path .. -PassThru

Path
----
HKLM:\
```

Írja be a Set-helyet, vagy a Set-helye (cd, chdir, sl) használja a beépített Windows PowerShell-aliasok valamelyikét. Például:

```powershell
cd -Path C:\Windows
```

```powershell
chdir -Path .. -PassThru
```

```powershell
sl -Path HKLM:\SOFTWARE -PassThru
```

### <a name="saving-and-recalling-recent-locations-push-location-and-pop-location"></a>Mentés és a legutóbbi helyek (a leküldéses-hely és a csatlakozási pont – hely) visszahívása

Helyek módosításakor hasznos, ahol rendelkezik-e nyomon, és térjen vissza az előző helyre lehessen. A **leküldéses helymeghatározás** a Windows PowerShell parancsmag létrehoz egy rendezett előzmények (a "verem"), ahol rendelkezik-e, és Ön visszaléphet az elérési utak előzményeit a kiegészítő használatával elérési utak  **Csatlakozási pont – hely** parancsmagot.

Ha például Windows PowerShell általában az a felhasználó kezdőkönyvtárának indítja el.

```
PS> Get-Location

Path
----
C:\Documents and Settings\PowerUser
```

> [!NOTE]
> A word *stack* számos programozási beállításai, többek között a .NET-keretrendszer egy különleges jelentése van. Fizikai stack elemek, például a legutóbbi helyezi a veremben elem az első elem, amely a verem ki kérheti le. Felvesz egy elemet egy verem colloquially nevezik "leküldése" a cikk a veremben. Beolvasás a verem ki egy elemet colloquially nevezik "popping" a cikk a verem ki.

Küldje le az aktuális helyét a veremben, és helyezze át a helyi beállításokat mappába, írja be:

```powershell
Push-Location -Path "Local Settings"
```

Ezután küldje le a helyi beállításokat helyét a veremben, és írja be a Temp mappa áthelyezése:

```powershell
Push-Location -Path Temp
```

Könyvtárak módosította beírásával ellenőrizheti a **Get-Location** parancsot:

```
PS> Get-Location

Path
----
C:\Documents and Settings\PowerUser\Local Settings\Temp
```

Meg lehet majd pop az utoljára felkeresett címtárba megadásával a **jelenléti pont – hely** parancsot, és ellenőrizze a módosítást, írja be a **Get-hely** parancsot:

```
PS> Pop-Location
PS> Get-Location

Path
----
C:\Documents and Settings\me\Local Settings
```

Az igény szerint a **hely beállítása** parancsmaggal, megadhatja a **- PassThru** paraméter megadásakor a **jelenléti pont – hely** parancsmaggal a megadott könyvtár:

```
PS> Pop-Location -PassThru

Path
----
C:\Documents and Settings\PowerUser
```

A hely parancsmagok hálózati elérési úttal is használhatja. Ha egy kiszolgáló FS01 nevű nyilvános-megosztásban, módosíthatja írja be a hely

```powershell
Set-Location \\FS01\Public
```

vagy a

```powershell
Push-Location \\FS01\Public
```

Használhatja a **leküldéses helymeghatározás** és **hely beállítása** módosítsa a helyet bármely elérhető meghajtó-parancsokat. Például ha D meghajtóbetűjellel CD-ről adatokat tartalmazó helyi CD-ROM-meghajtóval rendelkezik, módosíthatja a helyet a CD-meghajtó megadásával a **hely beállítása D:** parancsot.

Ha a meghajtó üres, a következő hibaüzenet jelenik meg:

```
PS> Set-Location D:
Set-Location : Cannot find path 'D:\' because it does not exist.
```

Ha olyan parancssori felületet használ, akkor sem kényelmes fájlkezelő használata a rendelkezésre álló fizikai meghajtók vizsgálatához. Ezenkívül fájlkezelő lenne jeleníti meg az összes, a Windows PowerShell-meghajtók. Windows PowerShell parancsokat biztosít kezelésére szolgáló Windows PowerShell-meghajtók és az előadás a Tovább gombra.
