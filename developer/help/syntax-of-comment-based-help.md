---
title: Megjegyzés-alapú súgó szintaxisát |} A Microsoft Docs
ms.custom: ''
ms.date: 09/12/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: e8adc997-1a71-48e9-9383-513ef13da7cf
caps.latest.revision: 4
ms.openlocfilehash: 584e5923008e8369a83c699478844f0e0c295adc
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56846493"
---
# <a name="syntax-of-comment-based-help"></a>Megjegyzésalapú súgótémakörök szintaxisa

Ez a szakasz ismerteti a Megjegyzés-alapú súgó szintaxisát.

## <a name="syntax-diagram"></a>Szintaxisdiagramja

 A Megjegyzés-alapú súgó szintaxisa a következő:

```
# .< help keyword>
# <help content>

-or -

<#
.< help keyword>
< help content>
#>
```

## <a name="syntax-description"></a>Szintaxis leírása

 Megjegyzés-alapú súgó írt megjegyzések sorozataként. Megjegyzések minden egyes sora elé is írja be a Megjegyzés szimbólumát (#), vagy használhatja a "\<#" és "#>" hozhat létre egy megjegyzésblokkot szimbólumok. A Megjegyzés blokkon belül a sorok megjegyzésként értelmezi.

 Megjegyzés-alapú súgó minden szakasza határozza meg egy kulcsszót, és minden kulcsszó előzi meg egy pontot (.). A kulcsszavak bármilyen sorrendben is megjelenhetnek. A kulcsszó nevében a rendszer nem kis-és nagybetűket.

 A megjegyzésblokkot tartalmaznia kell legalább egy Súgó kulcsszót. Néhány kulcsszóra, mint PÉLDÁUL az azonos megjegyzésblokkot sokszor szerepelhetnek. Minden kulcsszó súgója kulcsszó után a sor kezdődik, és több sort is kiterjedhetnek.

 Az összes megjegyzés-alapú súgótémakör sorok összefüggőeknek kell lenniük. A Megjegyzés-alapú súgó-témakör egy megjegyzés, amely nem része a Súgó-témakör követi, ha legalább egy üres sor utolsó sora nem súgó Megjegyzés és a Megjegyzés-alapú súgó kezdete közötti lehet.

 Például a következő megjegyzés-alapú témakör tartalmazza a. Leírás kulcsszó és a hozzá tartozó értéket, amely egy függvény vagy parancsfájl leírása.

```powershell
<#
    .Description
    The Get-Function function displays the name and syntax of all functions in the session.
#>
```