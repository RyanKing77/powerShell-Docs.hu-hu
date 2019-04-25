---
title: Hogyan lehet egy HelpInfo XML-fájl neve |} A Microsoft Docs
ms.custom: ''
ms.date: 09/12/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 64e85b53-5aeb-4d6c-903c-af4ab62f11c1
caps.latest.revision: 7
ms.openlocfilehash: 462cd7bd486a5924bb2bc43e0ac8d1558e30e657
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62082396"
---
# <a name="how-to-name-a-helpinfo-xml-file"></a>HelpInfo XML-fájl elnevezése

Ez a témakör ismerteti a szükséges nevének formátuma a frissíthető súgó információkat fájlok, gyakran nevezik HelpInfo XML-fájlok számára.

## <a name="how-to-name-a-helpinfo-xml-file"></a>HelpInfo XML-fájl elnevezése

Egy HelpInfo XML-fájl nevét a következő formátummal kell rendelkeznie.

`<ModuleName>_<ModuleGUID>_HelpInfo.xml`

A név az elemek a következők.

Modulnév értéke az a **neve** tulajdonságát a **ModuleInfo** objektum, amely a [Get-Module](/powershell/module/Microsoft.PowerShell.Core/Get-Module) parancsmag adja vissza.

ModuleGUID az értéket, a **GUID** kulcsfontosságú a moduljegyzékben.

Például ha a modul neve "TestModule" és a modul GUID 9cabb9ad-f2ac-4914-a46b-bfc1bebf07f9, a modul HelpInfo XML-fájljának nevét a következő lesz:

`TestModule_9cabb9ad-f2ac-4914-a46b-bfc1bebf07f9_HelpInfo.xml`