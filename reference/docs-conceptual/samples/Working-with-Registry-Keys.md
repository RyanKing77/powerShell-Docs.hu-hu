---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: Beállításkulcsok használata
ms.assetid: 91bfaecd-8684-48b4-ad86-065dfe6dc90a
ms.openlocfilehash: e7b497ec2fccf9ba3934439a9c1e9be3cf70a705
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62058862"
---
# <a name="working-with-registry-keys"></a>Beállításkulcsok használata

Mivel beállításkulcsok a Windows PowerShell-meghajtókon lévő elemek, a használatukat a nagyon hasonló fájlok és mappák használata. Egy fontos különbséggel, hogy minden eleme egy beállításjegyzék-alapú Windows PowerShell-meghajtón egy tárolóban, csakúgy, mint a fájlrendszer meghajtóján az egyik mappájába. Azonban a beállításjegyzék-bejegyzések és a hozzájuk tartozó értékek azok az elemek nem különálló elemek tulajdonságai.

## <a name="listing-all-subkeys-of-a-registry-key"></a>Egy beállításkulcs alkulcsait összes listázása

Közvetlenül egy beállításkulcs található minden elem megjelenítése használatával **Get-ChildItem**. Adja hozzá a választható **kényszerített** rejtettek megjelenítése vagy rendszer elemek paramétert. Ha például a parancs megjeleníti a közvetlenül a Windows PowerShell meghajtót HKCU található elem:, amely megfelel a HKEY_CURRENT_USER beállításjegyzék-struktúrát:

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

Ezek a HKEY_CURRENT_USER a a Beállításszerkesztőt (Regedit.exe) alatt látható a legfelső szintű kulcsokat.

Azt is beállíthatja a beállításjegyzékbeli elérési út megadásával a beállításjegyzék-szolgáltatójának neve, majd "**::**". A beállításjegyzék-szolgáltató teljes neve **Microsoft.PowerShell.Core\\beállításjegyzék**, de ez csupán lerövidíthető **beállításjegyzék**. A következő parancsokhoz felsorolja a tartalmat közvetlenül a HKCU alatt:

```powershell
Get-ChildItem -Path Registry::HKEY_CURRENT_USER
Get-ChildItem -Path Microsoft.PowerShell.Core\Registry::HKEY_CURRENT_USER
Get-ChildItem -Path Registry::HKCU
Get-ChildItem -Path Microsoft.PowerShell.Core\Registry::HKCU
Get-ChildItem HKCU:
```

Ezek a parancsok listája csak a közvetlenül benne lévő elemek, hasonlóan a Cmd.exe használatával **DIR** parancs vagy **ls** egy UNIX-rendszerhéjban. A befoglalt elemek megjelenítése, meg kell adnia a **Recurse** paraméter. Minden beállításkulcsok HKCU listájában, használja az alábbi parancsot (Ez a művelet egy rendkívül hosszú időbe telhet.):

```powershell
Get-ChildItem -Path hkcu:\ -Recurse
```

**Get-ChildItem** összetett szűrési képességek segítségével elvégezheti a **elérési**, **szűrő**, **Belefoglalás**, és **kizárása**általában alapú csak a name paraméter, de ezeket a paramétereket. Összetett szűrését az egyéb elemek tulajdonságai alapján is végezhet a **Where-Object** parancsmagot. A következő parancs megkeresi a HKCU belül az összes kulcs:\\szoftver, amely legfeljebb egy kulcsot, és pontosan négy értéket is rendelkeznek:

```powershell
Get-ChildItem -Path HKCU:\Software -Recurse | Where-Object -FilterScript {($_.SubKeyCount -le 1) -and ($_.ValueCount -eq 4) }
```

## <a name="copying-keys"></a>Kulcsok másolása

Másolás végzett **Copy-Item**. A következő parancsot, másolja át HKLM:\\szoftver\\Microsoft\\Windows\\CurrentVersion és az összes hozzá tartozó tulajdonságok HKCU:\\, "CurrentVersion" nevű új kulcs létrehozása:

```powershell
Copy-Item -Path 'HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion' -Destination hkcu:
```

Ha megvizsgálja az új kulcs a Beállításszerkesztő vagy a **Get-ChildItem**, megfigyelheti, hogy nem kell a tartalmazott alkulcsok másolatát az új helyen. Annak érdekében, hogy a tároló tartalmának másolása, meg kell adnia a **Recurse** paraméter. Ahhoz, hogy az előző másolási parancs rekurzív, használja ezt a parancsot:

```powershell
Copy-Item -Path 'HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion' -Destination hkcu: -Recurse
```

Már elérhető fájlrendszer másolatok végrehajtásához más eszközök továbbra is használhatja. Minden olyan beállításjegyzék szerkesztőeszközeihez – beleértve a beállításjegyzék szerkesztése (például WScript.Shell és a WMI StdRegProv osztály) támogató reg.exe regini.exe és regedit.exe—and COM-objektumok is használható a Windows PowerShell.

## <a name="creating-keys"></a>Kulcsok létrehozása

Új kulcsok létrehozása a beállításjegyzékben egyszerűbb, mint a fájlrendszer egy új elem létrehozása. Mivel az összes beállításkulcsok tárolók, nem kell megadnia a elemtípus; egyszerűen adhat meg explicit elérési utat, mint például:

```powershell
New-Item -Path hkcu:\software_DeleteMe
```

Olyan szolgáltató alapú elérési út használatával adja meg a kulcs:

```powershell
New-Item -Path Registry::HKCU_DeleteMe
```

## <a name="deleting-keys"></a>Kulcsok törlése

Elemek törlése lényegében ugyanúgy történik minden szolgáltató számára. Elemek csendes eltávolítja a következő parancsokat:

```powershell
Remove-Item -Path hkcu:\Software_DeleteMe
Remove-Item -Path 'hkcu:\key with spaces in the name'
```

## <a name="removing-all-keys-under-a-specific-key"></a>Egy adott kulcs alapján minden kulcs eltávolítása

Eltávolíthatja a benne lévő elemek használatával **Remove-cikk**, de meg kell adnia az eltávolítás megerősítéséhez, ha az elem tartalmaz bármi más. Ha például azt próbál meg törölni a HKCU:\\CurrentVersion alkulcs hoztunk létre, ez látható:

```
Remove-Item -Path hkcu:\CurrentVersion

Confirm
The item at HKCU:\CurrentVersion\AdminDebug has children and the -recurse
parameter was not specified. If you continue, all children will be removed with
 the item. Are you sure you want to continue?
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help
(default is "Y"):
```

Rákérdezés nélkül törli a benne lévő elemek, adja meg a **-Recurse** paramétert:

```powershell
Remove-Item -Path HKCU:\CurrentVersion -Recurse
```

Ha szeretne HKCU található minden elem eltávolítása:\\CurrentVersion, de nem HKCU:\\maga CurrentVersion, Ehelyett használhatja:

```powershell
Remove-Item -Path HKCU:\CurrentVersion\* -Recurse
```