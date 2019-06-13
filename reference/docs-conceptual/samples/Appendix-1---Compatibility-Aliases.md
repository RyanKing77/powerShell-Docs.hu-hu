---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: '1. függelék: Kompatibilitási aliasok'
ms.openlocfilehash: 553b9f01d6b5e3f4e04f1a75c25979b54dc205da
ms.sourcegitcommit: a6f13c16a535acea279c0ddeca72f1f0d8a8ce4c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2019
ms.locfileid: "67030329"
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
|**type**|**cat**|**Get-Content**|**globális katalógus**|
|**cd**|**cd**|**Set-Location**|**sl**|
|**md**|**mkdir**|**New-Item**|**ni**|
|**pushd**|**pushd**|**Leküldéses-helye**|**pushd**|
|**popd**|**popd**|**Pop-Location**|**popd**|
