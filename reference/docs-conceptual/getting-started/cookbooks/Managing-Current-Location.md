---
ms.date: 06/05/2017
keywords: PowerShell parancsmag
title: Aktuális hely kezelése
ms.assetid: a9f9e7a7-3ea8-47d3-bbb4-6e437f6d4a4a
ms.openlocfilehash: 8d529bf4a85553b95a9cab2739016859662486f2
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
ms.locfileid: "30952222"
---
# <a name="managing-current-location"></a>Aktuális hely kezelése

A Fájlkezelőben mappa rendszerek navigáláskor általában rendelkeznek egy adott működő hely -, az aktuális mappa megnyitása. Az aktuális mappában elemek kattintással könnyedén kezelhetők. A parancssori felületen például a Cmd.exe amikor egy adott fájl ugyanabban a mappában van-e hozzáférése által viszonylag rövid nevének megadása helyett adja meg a fájl teljes elérési útja kell. Az aktuális könyvtár neve a munkakönyvtárat.

A Windows PowerShell használja a főnév **hely** lehet hivatkozni a munkakönyvtár családba tartozó-parancsmagok segítségével vizsgálja meg és kezelheti a felhasználó tartózkodási helyét, és.

### <a name="getting-your-current-location-get-location"></a>A jelenlegi hely (Get-hely) beolvasása

Határozza meg az elérési útját az aktuális könyvtár helyét, írja be a következőt a **Get-hely** parancs:

```
PS> Get-Location
Path
----
C:\Documents and Settings\PowerUser
```

> [!NOTE]
> A Get-hely parancsmag hasonlít a **pwd** a rendszerhéjakba parancsot. A hely beállítása parancsmag hasonlít a **cd** Cmd.exe parancsot.

### <a name="setting-your-current-location-set-location"></a>A jelenlegi hely (Set-helyének) beállítása

A **Get-hely** parancs használatos a **hely beállítása** parancsot. A **hely beállítása** parancs lehetővé teszi, hogy adja meg az aktuális könyvtár helyet.

```powershell
Set-Location -Path C:\Windows
```

Miután megadta a parancs, megfigyelheti, hogy nem jelenik meg a hatását, hogy a parancs minden közvetlen visszajelzést. Egy műveletet a legtöbb Windows PowerShell-parancsok kevéssé vagy egyáltalán ne kimeneti eredményez, mivel a kimenet nem mindig hasznos. Győződjön meg arról, hogy a sikeres könyvtárváltás történt-e, amikor megadja a a **hely beállítása** paranccsal, tartalmazza a **- PassThru** paraméter megadásakor a **Set-hely**parancs:

```
PS> Set-Location -Path C:\Windows -PassThru

Path
----
C:\WINDOWS
```

A **- PassThru** paraméter használható a Windows PowerShell számos Set parancs tevékenység információt nyújt az eredmény abban az esetben, amelyben nincs alapértelmezett kimenet.

Meg elérési utat is megadhat tartózkodási helyéhez viszonyított azonos módon, akkor volna a UNIX és a Windows legtöbb parancs ismertetése. Standard jelöléssel relatív elérési út esetén időszak (**.**) az aktuális mappát, és egy doubled időszakot jelöli (**...** ) az aktuális hely-jének szülőkönyvtárában jelöli.

Ha például a **C:\\Windows** , az adott időszakban (**.**) jelöli **C:\\Windows** és időszakok duplán (**...** ) képviselő **C:**. Módosíthatja az aktuális helyről a C: meghajtó gyökerébe beírásával:

```
PS> Set-Location -Path .. -PassThru

Path
----
C:\
```

Ugyanaz a technika működik, amelyek nincsenek fájl rendszert tartalmazó meghajtókon, például a Windows PowerShell meghajtókon **HKLM:**. A felhasználó tartózkodási helyét is beállíthatja a HKLM\\szoftverkulcs írja be a beállításjegyzékben:

```
PS> Set-Location -Path HKLM:\SOFTWARE -PassThru

Path
----
HKLM:\SOFTWARE
```

Módosíthatja a könyvtár helyét a szülőkönyvtárat, amely a Windows PowerShell HKLM gyökere: meghajtó relatív elérési úttal:

```
PS> Set-Location -Path .. -PassThru

Path
----
HKLM:\
```

Írja be a hely beállítása, vagy használja a beépített Windows PowerShell-aliasok valamelyikét a Set-helyéhez (cd, chdir, l). Például:

```powershell
cd -Path C:\Windows
```

```powershell
chdir -Path .. -PassThru
```

```powershell
sl -Path HKLM:\SOFTWARE -PassThru
```

### <a name="saving-and-recalling-recent-locations-push-location-and-pop-location"></a>Mentés és a legutóbbi helyek (leküldéses és Pop-) tárolóról

Helyek módosítása, esetén hasznos, ha rendelkezik-e nyomon, és térjen vissza az előző helyre tudja. A **leküldéses-hely** a Windows PowerShell parancsmag hoz létre a könyvtár elérési utakon található rendelkezik-e, vehetjük vissza elérési útjainak előzményeinek a kiegészítő használatával rendezett előzményeit (a "verem")  **POP-hely** parancsmag.

Például a Windows PowerShell általában indítja el a felhasználó saját könyvtárához.

```
PS> Get-Location

Path
----
C:\Documents and Settings\PowerUser
```

> [!NOTE]
> A word *verem* rendelkezik-e speciális jelentéssel számos programozási beállításai, beleértve a .NET-keretrendszer. Fizikai verem elemek, például az utolsó elem a veremben helyezünk elem az első, amely akkor is lehívása a verem. Egy elem felvétele a verem colloquially nevezik "küldését" a cikk a veremben. Húzza ki a verem elem colloquially nevezik "popping" a cikk a verem ki.

Az aktuális helyen, a veremben leküldéses, és helyezze át a helyi beállításokat mappába, írja be:

```powershell
Push-Location -Path "Local Settings"
```

Majd tolható ki a helyi beállításokat helyét a veremben, és írja be az ideiglenes mappa áthelyezése és:

```powershell
Push-Location -Path Temp
```

Könyvtárak módosította beírásával ellenőrizheti a **Get-hely** parancs:

```
PS> Get-Location

Path
----
C:\Documents and Settings\PowerUser\Local Settings\Temp
```

Akkor is majd állítsa vissza a nemrég megtekintett könyvtárba megadásával a **Pop-hely** parancsot, és ellenőrzéséhez írja be a **Get-hely** parancs:

```
PS> Pop-Location
PS> Get-Location

Path
----
C:\Documents and Settings\me\Local Settings
```

Együtt, csak a **hely beállítása** parancsmaggal, megadhatja a **- PassThru** paraméter megadásakor a **Pop-hely** parancsmag használatával jelenítse meg a megadott könyvtár:

```
PS> Pop-Location -PassThru

Path
----
C:\Documents and Settings\PowerUser
```

A hálózati elérési út is használhatja a hely parancsmagokat. Ha egy kiszolgáló egy nyilvános nevű fájlmegosztás FS01 nevű, módosíthatja írja be a felhasználó tartózkodási helyét

```powershell
Set-Location \\FS01\Public
```

vagy a

```powershell
Push-Location \\FS01\Public
```

Használhatja a **leküldéses-hely** és **hely beállítása** parancsok helyének módosításához az összes rendelkezésre álló meghajtóra. Például ha D meghajtóbetűjellel adatok CD-ről tartalmazó helyi CD-ROM-meghajtóval rendelkezik, módosíthatja a hely a CD-meghajtót írja be a **hely beállítása D:** parancsot.

Ha a meghajtó üres, a következő hibaüzenet jelenik meg:

```
PS> Set-Location D:
Set-Location : Cannot find path 'D:\' because it does not exist.
```

Amikor egy parancssori felületet használ, célszerű nem a Fájlkezelőben a rendelkezésre álló fizikai meghajtók ellenőrzéséhez. Emellett a Fájlkezelőben volna jeleníti meg az összes, a Windows PowerShell-meghajtó. Windows PowerShell parancsokat biztosít kezelésére szolgáló Windows PowerShell-meghajtókat, valamint az előadás a Tovább gombra.