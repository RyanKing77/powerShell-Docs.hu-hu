---
title: Adjon meg szűrési paraméterekhez |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: e45929d1-bbb4-4dc6-892f-f9eacdb1c84c
caps.latest.revision: 8
ms.openlocfilehash: 553878c34e74129f9876cca25a5393cb0d53445a
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62067688"
---
# <a name="input-filter-parameters"></a>Bemeneti szűrőparaméterek

A parancsmag definiálhat `Filter`, `Include`, és `Exclude` szűrése, amely befolyásolja a parancsmag bemeneti objektumok készlete paraméterek.

A bemeneti objektumok készlete által meghatározott általában egy `InputObject`, `Path`, vagy `Name` paraméter. A parancsmag lehet például egy `Path` paraméter, amely több elérési út elfogadja a helyettesítő karaktereket, és minden egyes bemeneti objektum elérési pontok használatával. Együttes, a `Filter`, `Include`, és `Exclude` további paraméterek minősítéséhez az elérési utakat, a parancsmag minden alkalommal, amikor indítva a működik.

## <a name="include-and-exclude-parameters"></a>Belefoglalása vagy kizárása a paraméterek

A `Include` és `Exclude` paramétereket lévő vagy a készletből bemeneti objektumot a parancsmagnak átadott kizárt objektumok azonosítása. Akkor használja ezeket a paramétereket, ha a szűrőt a standard szintű helyettesítő nyelven lehet kifejezni. (További információ a helyettesítő karakterek: [helyettesítő karaktereket támogató parancsmag-paraméterek](./supporting-wildcard-characters-in-cmdlet-parameters.md).) A `Include` paraméter nevében a belefoglalási szűrőnek megfelelő összes objektumot magában foglalja. A `Exclude` paraméter nem tartalmazza a mappanevek megfelelnek a szűrőnek összes objektumot.

## <a name="filter-parameter"></a>Szűrési paraméterhez

A `Filter` paraméterrel egy szűrőt, amely nem fejezzük ki a standard szintű helyettesítő nyelven. Például az Active Directory Service Interfaces (ADSI) vagy az SQL-szűrők előfordulhat, hogy adható át a parancsmag segítségével a `Filter` paraméter. A parancsmagok a Windows PowerShell által biztosított ezeket a szűrőket, amelyek a parancsmagot egy adattár eléréséhez használja a Windows PowerShell-szolgáltatók által vannak megadva. Egyes szolgáltatók jellemzően a saját szűrő határozza meg.

## <a name="filtering-if-no-set-of-input-objects-is-specified"></a>Ha meg van adva a nincs megadva bemeneti objektumok szűrése

Ha nincs megadva bemeneti objektumok van megadva, ez általában azt jelenti, szemben az összes objektum szűréséhez. További információkért lásd:[Get-Process](/powershell/module/Microsoft.PowerShell.Management/Get-Process).

## <a name="see-also"></a>Lásd még:

[Egy Windows PowerShell-parancsmag írása](./writing-a-windows-powershell-cmdlet.md)