---
ms.date: 06/05/2017
keywords: PowerShell parancsmag
title: '1. függelék: Kompatibilitási aliasok'
ms.assetid: 96ad921e-1a57-463e-8e60-424faf8b6ef8
ms.openlocfilehash: 113bbee1af185f98777df5767022d54accb69447
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
ms.locfileid: "30954636"
---
# <a name="appendix-1---compatibility-aliases"></a>Függelék: 1 - kompatibilitási aliasok

A Windows PowerShell több átmenet aliasok UNIX- és Cmd a felhasználók használhatnak a megszokott parancs a Windows PowerShell lehetővé tévő rendelkezik. A leggyakoribb aliasok mellett a Windows PowerShell-parancsot az aliast, és a szabványos Windows PowerShell alias, ha van ilyen, az alábbi táblázatban láthatók.

A Windows PowerShell-parancsot bármelyik aliasszal mutat, a Windows PowerShell belül a Get-Alias parancsmaggal található. Írja be például **get-alias cls**.

```
CommandType     Name                            Definition
-----------     ----                            ----------
Alias           cls                             Clear-Host
```

|CMD parancs|UNIX parancs|PS Parancs|PS Alias|
|---------------|----------------|--------------|------------|
|**dir**|**ls**|**Get-ChildItem**|**gci**|
|**cls**|**Törölje a jelet**|**Törölje az állomás** (függvény)|**cls**|
|**del, erase, rmdir**|**rm**|**Remove-Item**|**ri**|
|**Másolás**|**cp**|**Copy-Item**|**ci**|
|**move**|**mv**|**Move-Item**|**mi**|
|**rename**|**mv**|**Rename-Item**|**rni**|
|**Típusa**|**cat**|**Get-Content**|**gc**|
|**cd**|**cd**|**Set-Location**|**sl**|
|**md**|**mkdir**|**New-Item**|**ni**|
|**pushd**|**pushd**|**Push-Location**|**pushd**|
|**popd**|**popd**|**Pop-Location**|**popd**|