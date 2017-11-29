---
ms.date: 2017-06-05
keywords: PowerShell parancsmag
title: "Beállításkulcsok használata"
ms.assetid: 91bfaecd-8684-48b4-ad86-065dfe6dc90a
ms.openlocfilehash: e7c16fe5f03330da3ea8f60b141d9e35eed474b9
ms.sourcegitcommit: cd5a1f054cbf9eb95c5242a995f9741e031ddb24
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 11/28/2017
---
# <a name="working-with-registry-keys"></a>Beállításkulcsok használata
Mert beállításkulcsok a Windows PowerShell-meghajtókon elem, azok használata hasonlít a fájlok és mappák. Egy kritikus különbség az, hogy minden eleme egy beállításjegyzék-alapú Windows PowerShell-meghajtón-e a tároló, csakúgy, mint a fájlrendszer meghajtóján az egyik mappájába. Beállításjegyzék-bejegyzések és a hozzájuk tartozó értékek tulajdonságok az elemek nem különálló elemek.

### <a name="listing-all-subkeys-of-a-registry-key"></a>A beállításkulcs összes alkulcsához listázása
Használatával megjelenítheti az összes elemet közvetlenül egy beállításkulcs megadásával belül **Get-ChildItem**. Adja hozzá a választható **kényszerített** rejtett megjelenítése vagy rendszer elemek paraméter. Például a parancs megjeleníti az elemek közvetlenül a Windows PowerShell meghajtót HKCU belül:, amely megfelel a HKEY_CURRENT_USER beállításjegyzék-struktúrát:

```
PS> Get-ChildItem -Path hkcu:\

   Hive: Microsoft.PowerShell.Core\Registry::HKEY_CURRENT_USER

SKC  VC Name                           Property
---  -- ----                           --------
  2   0 AppEvents                      {}
  7  33 Console                        {ColorTable00, ColorTable01, ColorTab...
 25   1 Control Panel                  {Opened}
  0   5 Environment                    {APR_ICONV_PATH, INCLUDE, LIB, TEMP...}
  1   7 Identities                     {Last Username, Last User ...
  4   0 Keyboard Layout                {}
...
```

Ezek a HKEY_CURRENT_USER a a Beállításszerkesztőt (Regedit.exe) látható legfelső szintű kulccsal.

Azt is megadhatja a beállításjegyzékbeli elérési út megadásával a beállításjegyzék-szolgáltatójának neve követ "**::**". A beállításjegyzék-szolgáltatójának teljes neve **Microsoft.PowerShell.Core\\beállításjegyzék**, de ez csak a lerövidíthető **beállításjegyzék**. A következő parancsok felsorolja közvetlenül alatt HKCU tartalma:

```
Get-ChildItem -Path Registry::HKEY_CURRENT_USER
Get-ChildItem -Path Microsoft.PowerShell.Core\Registry::HKEY_CURRENT_USER
Get-ChildItem -Path Registry::HKCU
Get-ChildItem -Path Microsoft.PowerShell.Core\Registry::HKCU
Get-ChildItem HKCU:
```

Ezek a parancsok listában csak a közvetlenül a benne lévő elemek hasonlóan a Cmd.exe tartozó **DIR** parancs vagy **ls** egy UNIX rendszerhéj. A befoglalt elemek megjelenítése, meg kell adnia a **Recurse** paraméter. Minden beállításkulcsok HKCU listájában, használja a következő parancsot (a művelet egy nagyon hosszú időt vehet igénybe.):

```
Get-ChildItem -Path hkcu:\ -Recurse
```

**Get-ChildItem** összetett szűrési képességek segítségével végezheti a **elérési**, **szűrő**, **Include**, és **kizárása** általában alapú csak a name paraméterek, de ezeket a paramétereket. Összetett szűrés használatával-elemek egyéb tulajdonságok alapján hajthat végre a **Where-Object** parancsmag. A következő parancs megkeresi HKCU belül minden kulcs:\\szoftver, amely nem több kulcsot, és pontosan négy értékűek is:

```
Get-ChildItem -Path HKCU:\Software -Recurse | Where-Object -FilterScript {($_.SubKeyCount -le 1) -and ($_.ValueCount -eq 4) }
```

### <a name="copying-keys"></a>Kulcsok másolása
Másolás történik a **elem**. A következő parancsot, másolja át HKLM:\\szoftver\\Microsoft\\Windows\\CurrentVersion és az összes HKCU annak tulajdonságait:\\, "CurrentVersion" nevű új kulcs létrehozása:

```
Copy-Item -Path 'HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion' -Destination hkcu:
```

Ha megvizsgálja az új kulcsot, a Beállításszerkesztő vagy segítségével **Get-ChildItem**, megfigyelheti, hogy nem kell a benne lévő alkulcsok másolatát az új helyen. Ahhoz, hogy a tároló tartalmának másolása, meg kell adnia a **Recurse** paraméter. Ahhoz, hogy az előző Másolás parancs rekurzív, akkor használja a parancsot:

```
Copy-Item -Path 'HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion' -Destination hkcu: -Recurse
```

Már elérhető fájlrendszer hozza eszközök továbbra is használhatja. A beállításjegyzék szerkesztőeszközeivel – beleértve a reg.exe regini.exe és regedit.exe—and COM objektumok, amelyek támogatják a beállításjegyzék szerkesztésével (például WScript.Shell és a WMI StdRegProv osztály) használhatja a Windows PowerShell.

### <a name="creating-keys"></a>Kulcsok létrehozása
Új kulcsok létrehozása a beállításjegyzékben felügyelete egyszerűbb, mint egy fájlrendszer új elem létrehozásához. Minden beállításkulcsok olyan tárolók, mert nem kell megadnia a elemtípus; egyszerűen megadnia explicit elérési utat, például:

```
New-Item -Path hkcu:\software_DeleteMe
```

A szolgáltató alapú elérési segítségével adjon meg egy kulcs:

```
New-Item -Path Registry::HKCU_DeleteMe
```

### <a name="deleting-keys"></a>Kulcsok törlése
Az elemek törlése lényegileg azonos összes szolgáltató. A következő parancsok csendes eltávolítja az elemet:

```
Remove-Item -Path hkcu:\Software_DeleteMe
Remove-Item -Path 'hkcu:\key with spaces in the name'
```

### <a name="removing-all-keys-under-a-specific-key"></a>Egy adott kulcs alatt minden kulcs eltávolítása
Eltávolíthatja a benne lévő elemek használatával **Remove-cikk**, de kérni fogja az eltávolítás megerősítéséhez, ha az elem tartalmaz dolgozott. Például, ha azt a HKCU törlésére tett kísérlet:\\CurrentVersion alkulcs létrehozott, ez látható:

```
Remove-Item -Path hkcu:\CurrentVersion

Confirm
The item at HKCU:\CurrentVersion\AdminDebug has children and the -recurse
parameter was not specified. If you continue, all children will be removed with
 the item. Are you sure you want to continue?
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help
(default is "Y"):
```

Törli a benne lévő elemek értesítése nélkül, adja meg a **-Recurse** paraméter:

```
Remove-Item -Path HKCU:\CurrentVersion -Recurse
```

Ha eltávolítja az összes elemet HKCU belül:\\CurrentVersion, de nem HKCU:\\maga CurrentVersion, helyette használhatja:

```
Remove-Item -Path HKCU:\CurrentVersion\* -Recurse
```

