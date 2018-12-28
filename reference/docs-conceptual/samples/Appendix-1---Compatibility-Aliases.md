---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: '1. függelék: Kompatibilitási aliasok'
ms.assetid: 96ad921e-1a57-463e-8e60-424faf8b6ef8
ms.openlocfilehash: 113bbee1af185f98777df5767022d54accb69447
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404599"
---
# <a name="appendix-1---compatibility-aliases"></a>Függelék: 1 – kompatibilitási aliasok

Windows PowerShell több átmeneti aliasok, amelyek lehetővé teszik a jól ismert parancsnevek használata a Windows PowerShellben a UNIX és a Cmd felhasználók rendelkezik. A leggyakoribb aliasok és a Windows PowerShell-parancsot az alias és a standard szintű Windows PowerShell alias, ha van ilyen mögött az alábbi táblázatban láthatók.

A Windows PowerShell-parancsot, amely bármelyik aliasszal mutat a Windows Powershellen belülről a Get-Alias parancsmag használatával is megtalálhatja. Írja be például **get-alias cls**.

```
CommandType     Name                            Definition
-----------     ----                            ----------
Alias           cls                             Clear-Host
```

|CMD parancsot|UNIX-parancs|PS Parancsot|PS Alias|
|---------------|----------------|--------------|------------|
|**a dir parancs**|**ls**|**Get-ChildItem**|**CGI**|
|**CLS**|**Világos**|**CLEAR-gazdagépen** (funkce)|**CLS**|
|**del, törlés, rmdir**|**erőforrás-kezelő**|**Remove-elem**|**a fenntartott példányok**|
|**Másolás**|**CP**|**Elem másolása**|**konfigurációelem**|
|**Áthelyezés**|**mV**|**Elem áthelyezése**|**Mi**|
|**Nevezze át**|**mV**|**Rename-elem**|**rni**|
|**Típusa**|**cat**|**Get-tartalom**|**globális katalógus**|
|**CD-ről**|**CD-ről**|**Hely beállítása**|**SL**|
|**MD**|**mkdir**|**Új elem**|**Ni**|
|**pushd**|**pushd**|**Leküldéses-helye**|**pushd**|
|**popd**|**popd**|**POP-helye**|**popd**|