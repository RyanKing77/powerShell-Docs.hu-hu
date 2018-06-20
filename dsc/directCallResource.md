---
ms.date: 06/12/2017
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: DSC-erőforrások metódusainak közvetlen hívása
ms.openlocfilehash: 3ec3a3a8da615f45f3fdd28b1c1e46e312507ed5
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/16/2018
ms.locfileid: "34189618"
---
# <a name="calling-dsc-resource-methods-directly"></a>DSC-erőforrások metódusainak közvetlen hívása

>Vonatkozik: A Windows PowerShell 5.0

Használhatja a [Invoke-DscResource](https://technet.microsoft.com/library/mt517869.aspx) parancsmagot hívja közvetlenül a funkciók vagy DSC erőforrás módszerek (a **Get-TargetResource**, **Set-TargetResource**, és  **Test-TargetResource** funkciók MOF-alapú erőforrás, vagy a **beolvasása**, **beállítása**, és **teszt** osztály-alapú erőforrás módszerek).
Ez használható DSC erőforrások használni kívánt harmadik felek által vagy hasznos eszközként erőforrások fejlesztése során.

Ez a parancsmag jellemzően metakonfigurációját tulajdonsággal együtt `refreshMode = 'Disabled'`, függetlenül attól, hogy mi is használható, de **refreshMode** értékre van állítva.

Ha előhívja a **Invoke-DscResource** parancsmaggal, megadhatja mely metódus vagy függvény használatával a **metódus** paraméter. Az erőforrás tulajdonságait úgy, hogy egy kivonattáblát értékeként adja meg a **tulajdonság** paraméter.

A következő példák-k közvetlen hívásakor erőforrás módszerek:

## <a name="ensure-a-file-is-present"></a>Győződjön meg arról, egy fájl jelen

```powershell
$result = Invoke-DscResource -Name File -Method Set -Property @{
                            DestinationPath = "$env:SystemDrive\\DirectAccess.txt";
                            Contents = 'This file is create by Invoke-DscResource'} -Verbose
$result | fl
```

## <a name="test-that-a-file-is-present"></a>Tesztelje, hogy a fájl megtalálható-e

```powershell
$result = Invoke-DscResource -Name File -Method Test -Property @{
                            DestinationPath="$env:SystemDrive\\DirectAccess.txt";
                            Contents='This file is create by Invoke-DscResource'} -Verbose
$result | fl
```

## <a name="get-the-contents-of-file"></a>A fájl tartalmának beolvasása

```powershell
$result = Invoke-DscResource -Name File -Method Get -Property @{
                            DestinationPath="$env:SystemDrive\\DirectAccess.txt";
                            Contents='This file is create by Invoke-DscResource'} -Verbose
$result.ItemValue | fl
```

>**Megjegyzés:** közvetlen összetett erőforrás metódusok meghívása nem támogatott. Ehelyett hívása az alapul szolgáló erőforrások, az összetett erőforrás alkotó módszerek.

## <a name="see-also"></a>Lásd még:
- [Egyéni DSC-erőforrás MOF írása](authoringResourceMOF.md)
- [A PowerShell osztályok egyéni DSC-erőforrás írása](authoringResourceClass.md)
- [ DSC-erőforrások hibakeresése](debugResource.md)