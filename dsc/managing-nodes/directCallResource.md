---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC-erőforrások metódusainak közvetlen hívása
ms.openlocfilehash: cf237f638593706e5959e2bcc0d851b0e55baf0e
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55685675"
---
# <a name="calling-dsc-resource-methods-directly"></a>DSC-erőforrások metódusainak közvetlen hívása

>Érvényes: Windows PowerShell 5.0

Használhatja a [Invoke-DscResource](/powershell/module/PSDesiredStateConfiguration/Invoke-DscResource) parancsmag, amellyel közvetlenül hívja az a funkciók vagy DSC-erőforrás módszerek (a **Get-TargetResource**, **Set-TargetResource**, és  **Test-TargetResource** funkciók MOF-alapú erőforrás, vagy a **első**, **beállítása**, és **teszt** módszer egy adott osztály-alapú erőforrás).
Ez használható szeretné használni a DSC-erőforrások harmadik felek, akár egy hasznos eszköz erőforrások fejlesztése során.

Ez a parancsmag jellemzően a metaconfiguration tulajdonsággal együtt `refreshMode = 'Disabled'`, függetlenül attól, hogy mi is használható, de **refreshMode** értékre van állítva.

Hívásakor a **Invoke-DscResource** parancsmaggal, megadhatja mely metódus vagy függvény használatával a **metódus** paraméter. Az erőforrás tulajdonságainak egy kivonattáblát átadásával értékeként adja meg a **tulajdonság** paraméter.

Az alábbi példák-erőforrások metódusainak közvetlen hívása:

## <a name="ensure-a-file-is-present"></a>Győződjön meg, hogy egy fájl jelen

```powershell
$result = Invoke-DscResource -Name File -Method Set -Property @{
                            DestinationPath = "$env:SystemDrive\\DirectAccess.txt";
                            Contents = 'This file is create by Invoke-DscResource'} -Verbose
$result | fl
```

## <a name="test-that-a-file-is-present"></a>Tesztelje, hogy egy fájl jelen

```powershell
$result = Invoke-DscResource -Name File -Method Test -Property @{
                            DestinationPath="$env:SystemDrive\\DirectAccess.txt";
                            Contents='This file is create by Invoke-DscResource'} -Verbose
$result | fl
```

## <a name="get-the-contents-of-file"></a>Fájl tartalmának beolvasása

```powershell
$result = Invoke-DscResource -Name File -Method Get -Property @{
                            DestinationPath="$env:SystemDrive\\DirectAccess.txt";
                            Contents='This file is create by Invoke-DscResource'} -Verbose
$result.ItemValue | fl
```

>**Megjegyzés:** Összetett erőforrások metódusainak közvetlen hívása nem támogatott. Ehelyett hívja meg a mögöttes erőforrások, az összetett erőforrás alkotó módszereket.

## <a name="see-also"></a>Lásd még:
- [MOF-egyéni DSC-erőforrás írása](../resources/authoringResourceMOF.md)
- [A PowerShell-osztályok egyéni DSC-erőforrás írása](../resources/authoringResourceClass.md)
- [ DSC-erőforrások hibakeresése](../troubleshooting/debugResource.md)