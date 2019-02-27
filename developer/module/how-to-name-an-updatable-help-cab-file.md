---
title: Hogyan lehet egy frissíthető súgó CAB-fájl neve |} A Microsoft Docs
ms.custom: ''
ms.date: 09/12/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: de302da0-c17a-4d31-a8ef-14a626738993
caps.latest.revision: 7
ms.openlocfilehash: 23303489372cfe7e036fdea842ae75f7e47503c8
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56850511"
---
# <a name="how-to-name-an-updatable-help-cab-file"></a>Frissíthető CAB-súgófájlok elnevezése

Ez a témakör ismerteti a frissíthető súgó kabinet szükséges név formátuma (. CAB-fájl) fájlok.

## <a name="how-to-name-an-updatable-help-cab-file"></a>Frissíthető CAB-súgófájlok elnevezése

Frissíthető kabinet (. CAB-fájl) fájlt a következő formátumú névvel kell rendelkeznie.

`<ModuleName>_<ModuleGUID>_<UICulture>_HelpContent.cab`

A név az elemek a következők.

Modulnév értéke az a **neve** tulajdonságát a **ModuleInfo** objektum, amely a [Get-Module](/powershell/module/Microsoft.PowerShell.Core/Get-Module) parancsmag adja vissza.
Értékét a **neve** tulajdonságát a **ModuleInfo** objektum, amely a [Get-Module](/powershell/module/Microsoft.PowerShell.Core/Get-Module) parancsmag adja vissza.

ModuleGUID az értéket, a **GUID** kulcsfontosságú a moduljegyzékben.

A CAB-fájl a súgófájlt UICulture a felhasználói felület kulturális környezet. Ezt az értéket meg kell egyeznie az egyik értékét a **UICulture** elemek modul HelpInfo XML-fájlban.

Például ha a modul neve "TestModule", a modul GUID 9cabb9ad-f2ac-4914-a46b-bfc1bebf07f9 és a felhasználói felület kultúrafüggő részletei az "en-US", a CAB-fájl neve:

`TestModule_9cabb9ad-f2ac-4914-a46b-bfc1bebf07f9_en-US_HelpContent.cab`