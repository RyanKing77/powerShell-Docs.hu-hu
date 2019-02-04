---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: '1. függelék: Kompatibilitási aliasok'
ms.assetid: 96ad921e-1a57-463e-8e60-424faf8b6ef8
ms.openlocfilehash: 113bbee1af185f98777df5767022d54accb69447
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55684688"
---
# <a name="appendix-1---compatibility-aliases"></a>Függelék: 1 – kompatibilitási aliasok

Windows PowerShell több átmeneti aliasok, amelyek lehetővé teszik a jól ismert parancsnevek használata a Windows PowerShellben a UNIX és a Cmd felhasználók rendelkezik. A leggyakoribb aliasok és a Windows PowerShell-parancsot az alias és a standard szintű Windows PowerShell alias, ha van ilyen mögött az alábbi táblázatban láthatók.

A Windows PowerShell-parancsot, amely bármelyik aliasszal mutat a Windows Powershellen belülről a Get-Alias parancsmag használatával is megtalálhatja. Írja be például **get-alias cls**.

```
CommandType     Name                            Definition
-----------     ----                            ----------
Alias           cls                             Clear-Host
```

|CMD Command|UNIX-parancs|PS Command|PS Alias|
|---------------|----------------|--------------|------------|
|**dir**|**ls**|**Get-ChildItem**|**gci**|
|**cls**|**clear**|**CLEAR-gazdagépen** (funkce)|**cls**|
|**del, erase, rmdir**|**rm**|**Remove-Item**|**ri**|
|**Másolás**|**cp**|**Copy-Item**|**ci**|
|**move**|**mv**|**Elem áthelyezése**|**mi**|
|**Nevezze át**|**mv**|**Rename-Item**|**rni**|
|**Típusa**|**cat**|**Get-Content**|**globális katalógus**|
|**cd**|**cd**|**Set-Location**|**sl**|
|**md**|**mkdir**|**New-Item**|**ni**|
|**pushd**|**pushd**|**Leküldéses-helye**|**pushd**|
|**popd**|**popd**|**Pop-Location**|**popd**|