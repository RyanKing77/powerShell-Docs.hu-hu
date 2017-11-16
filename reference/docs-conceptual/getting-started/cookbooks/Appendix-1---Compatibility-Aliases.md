---
ms.date: 2017-06-05
keywords: PowerShell parancsmag
title: "1. függelékében kompatibilitási aliasok"
ms.assetid: 96ad921e-1a57-463e-8e60-424faf8b6ef8
ms.openlocfilehash: d789139ef80d4208b56e0b2930f04f824a00537d
ms.sourcegitcommit: 74255f0b5f386a072458af058a15240140acb294
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/03/2017
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
|**dir**|**ls**|**Get-ChildItem**|**CGI**|
|**CLS**|**Törölje a jelet**|**Törölje az állomás** (függvény)|**CLS**|
|**del, törlés, rmdir**|**erőforrás-kezelő**|**Elem eltávolítása**|**RI**|
|**Másolás**|**a CP**|**Elem másolása**|**konfigurációelem**|
|**Helyezze át**|**mV**|**Elem áthelyezése**|**Mi**|
|**Nevezze át**|**mV**|**Elemátnevezés**|**rni**|
|**típusa**|**cat**|**Get-tartalom**|**a globális katalógus**|
|**CD-ről**|**CD-ről**|**Hely beállítása**|**SA**|
|**MD**|**mkdir**|**Új elem**|**Ni**|
|**pushd**|**pushd**|**Leküldéses-helye**|**pushd**|
|**popd**|**popd**|**POP-helye**|**popd**|

