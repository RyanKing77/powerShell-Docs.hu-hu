---
title: A függvények helyezi el a Megjegyzés-alapú súgó |} A Microsoft Docs
ms.custom: ''
ms.date: 09/12/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 5ec7159e-e4e9-4b21-95df-94244432f679
caps.latest.revision: 5
ms.openlocfilehash: a663bd69be7825b1685f64ff8d3068bdd8ca3265
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62083195"
---
# <a name="placing-comment-based-help-in-functions"></a>Megjegyzésalapú súgótémakörök elhelyezése függvényekben

Ez a témakör ismerteti a Megjegyzés-alapú súgó-függvény elhelyezése, hogy a `Get-Help` parancsmag hozzárendeli a megfelelő függvény Megjegyzés-alapú súgó-témakör.

## <a name="where-to-place-comment-based-help-for-a-function"></a>Megjegyzés-alapú súgó-függvény elhelyezése

- A függvény törzsében elején.

- A függvény törzsében végén.

- Mielőtt a `Function` kulcsszót. A funkciót, ha van olyan parancsfájl vagy a modul skriptu nem szerepelhet egynél több üres sor utolsó sora a Megjegyzés-alapú súgó között, és a `Function` kulcsszót. Ellenkező esetben `Get-Help` társítja a Súgó a szkriptet, és nem az a függvény.

## <a name="examples-of-help-placement-in-a-function"></a>Súgó az Elhelyezés a függvény példái

 Az alábbi példák bemutatják az egyes Megjegyzés-alapú súgó-függvény három elhelyezési beállításait.

### <a name="help-at-the-beginning-of-a-function-body"></a>A függvény törzséhez elején Súgó

 Az alábbi példa bemutatja a Megjegyzés-alapú, a függvény törzséhez elején.

```powershell

function MyProcess
{
    <#
       .Description
       The MyProcess function gets the Windows PowerShell process.
    #>

    Get-Process powershell
}

```

### <a name="help-at-the-end-of-a-function-body"></a>A függvény törzséhez végén található Súgó

 Az alábbi példa bemutatja, hogy a függvény törzséhez végén található megjegyzés-alapú.

```powershell

function MyFunction
{
    Get-Process powershell

    <#
       .Description
       The MyProcess function gets the Windows PowerShell process.
    #>
}

```

### <a name="help-before-the-function-keyword"></a>A függvény kulcsszó előtt Súgó

 A következő példákban Megjegyzés-alapú előtt a függvény kulcsszó a sorban.

```powershell

<#
    .Description
    The MyProcess function gets the Windows PowerShell process.
#>
function MyFunction { Get-Process powershell}

```