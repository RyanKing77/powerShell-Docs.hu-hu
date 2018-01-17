---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "Közvetlenül a DSC-erőforrás metódusok meghívása"
ms.openlocfilehash: 3e83984fbf31dfcfec76fa15cdd9b83d92501aa0
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 01/17/2018
---
# <a name="calling-dsc-resource-methods-directly"></a>Közvetlenül a DSC-erőforrás metódusok meghívása

>Vonatkozik: A Windows PowerShell 5.0

Használhatja a [Invoke-DscResource](https://technet.microsoft.com/en-us/library/mt517869.aspx) parancsmagot hívja közvetlenül a funkciók vagy DSC erőforrás módszerek (a **Get-TargetResource**, **Set-TargetResource**, és  **Test-TargetResource** funkciók MOF-alapú erőforrás, vagy a **beolvasása**, **beállítása**, és **teszt** osztály-alapú erőforrás módszerek). Ez használható DSC erőforrások használni kívánt harmadik felek által vagy hasznos eszközként erőforrások fejlesztése során. 

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

