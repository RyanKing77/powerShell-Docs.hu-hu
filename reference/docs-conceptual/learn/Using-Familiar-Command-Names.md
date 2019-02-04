---
ms.date: 08/27/2018
keywords: PowerShell, a parancsmag
title: Jól ismert parancsnevek használata
ms.assetid: 021e2424-c64e-4fa5-aa98-aa6405758d5d
ms.openlocfilehash: 3d2c681623086e061e237f08603d65150d2b1947
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55688923"
---
# <a name="using-familiar-command-names"></a>Jól ismert parancsnevek használata

PowerShell alternatív névvel parancsok hivatkozik aliasokat támogatja. Aliasképző segítségével a felhasználók élményét a gyakori, a már ismert parancsnevek használata hasonló műveletek a PowerShellben más ismertetése.

Aliasképző hozzárendeli egy másik parancs egy új nevet. Például, a PowerShell, egy belső függvény nevű `Clear-Host` , amely törli a kimeneti ablakban. Beírhatja, vagy a `cls` vagy `clear` alias parancsot a parancssorba. PowerShell ezek az aliasok értelmezi, és futtatja a `Clear-Host` függvény.

Ez a funkció segít a felhasználóknak további PowerShell. Első, a legtöbb **cmd.exe** és a Unix-felhasználók vannak egy nagy repertoire, amely a felhasználók már tudja név alapján. A PowerShell-megfelelőik nem azonos eredményeket hozhat. Azonban az eredmény Bezárás nem elegendő, amelyeket a felhasználók a PowerShell-parancs neve ismerete nélkül működnek. "Finger memória" as gazdasági válság után egy másik fő forrásai akkor, ha egy új parancs-rendszerhéj tanulási. Ha már használt **cmd.exe** éve reflexively írja be a `cls` paranccsal törölje a képernyőn. Az alias nélkül `Clear-Host`, hibaüzenetet kap, és nem tudja, mi a teendő a kimenet törlése.

Az alábbi lista tartalmazza a közös néhány **cmd.exe** és a Unix-parancsok a PowerShellben is használhatja:

|||||
|-|-|-|-|
|cat|a dir parancs|csatlakoztatási|rm|
|cd|echo|Áthelyezés|rmdir|
|chdir|Tartalmának végleges törlése|popd|alvó állapot|
|Világos|H|PS|Rendezés|
|CLS|Előzmények|pushd|TEE|
|Másolás|Kill|pwd|típus|
|del|LP|r|írási|
|a diff|ls|ren||

A `Get-Alias` parancsmag megjeleníti a valódi neve alias társított natív PowerShell-parancsot.

```powershell
PS> Get-Alias cls
```

```Output
CommandType     Name                               Version    Source
-----------     ----                               -------    ------
Alias           cls -> Clear-Host
```

## <a name="interpreting-standard-aliases"></a>Standard aliasok értelmezése

Az aliasokat, hogy a korábban ismertetett egyéb parancsrendszerhéjakban neve kompatibilitást lettek tervezve.
A legtöbb aliasok beépített PowerShell áttekinthetőség lettek kialakítva. Rövidebb nevek használata egyszerűbb, írja be, de a rendszer nehezen olvasható, ha nem tudja, hogy mire hivatkoznak.

PowerShell-aliasok megpróbálhatja az érthetőség és az áttekinthetőség között. PowerShell közös főneveket és műveletek aliasok szabványos készletét használja.

Példa rövidítések:

| Főnév vagy művelet | Rövidítése |
|--------------|--------------|
| Lekérés          | g            |
| Beállítás          | s            |
| Elem         | i            |
| Hely     | l            |
| Parancs      | cm           |
| Alias        | Al           |

Ezek az aliasok akkor érthető, ha ismeri a hónapok rövid nevét.

| Parancsmag neve    | Alias |
|----------------|-------|
| `Get-Item `    | gi    |
| `Set-Item`     | SI    |
| `Get-Location` | GL    |
| `Set-Location` | SL    |
| `Get-Command`  | gcm –   |
| `Get-Alias`    | gal   |

Ha ismeri, a PowerShell aliasképző, könnyebbé vált a kitalálja, hogy a **sal** alias hivatkozik `Set-Alias`.

## <a name="creating-new-aliases"></a>Új aliasok létrehozása

A saját alias használatával is létrehozhat a `Set-Alias` parancsmagot. Például a következő utasításokat a korábban tárgyalt szabványos parancsmag-aliasok hozzon létre:

```powershell
Set-Alias -Name gi -Value Get-Item
Set-Alias -Name si -Value Set-Item
Set-Alias -Name gl -Value Get-Location
Set-Alias -Name sl -Value Set-Location
Set-Alias -Name gcm -Value Get-Command
```

Belsőleg PowerShell indítása során hasonló parancsokat használja, de ezek az aliasok nem módosítható.
Ha megpróbálja hajtsa végre az alábbi parancsok egyikét, hibaüzenet elmagyarázza, hogy az alias nem lehet módosítani. Például:

```
PS> Set-Alias -Name gi -Value Get-Item
Set-Alias : Alias is not writeable because alias gi is read-only or constant and cannot be written to.
At line:1 char:10
+ Set-Alias  <<<< -Name gi -Value Get-Item
```
