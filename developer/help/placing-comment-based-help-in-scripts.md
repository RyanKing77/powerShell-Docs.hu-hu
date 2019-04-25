---
title: Helyezi el a Megjegyzés-alapú súgó parancsfájlok |} A Microsoft Docs
ms.custom: ''
ms.date: 09/12/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 49f8267c-d887-4d7d-b9b7-80dc624b1261
caps.latest.revision: 4
ms.openlocfilehash: d199c53a748ac57bb2a5f998b5056e39d3e80c0d
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62083229"
---
# <a name="placing-comment-based-help-in-scripts"></a>Megjegyzésalapú súgótémakörök elhelyezése szkriptekben

Ez a témakör ismerteti a Megjegyzés-alapú súgó parancsfájl helyét, hogy a `Get-Help` parancsmag társítja a Megjegyzés-alapú súgó-témakör szkriptekkel és nem lehet, a parancsfájl funkciók.

## <a name="where-to-place-comment-based-help-for-a-script"></a>Megjegyzés-alapú súgó parancsfájl helye

- A parancsfájl elején. Parancsfájl segítséget is megelőzi a szkriptben csak megjegyzésekkel és az üres sorok.

- A parancsfájl végén.

  Ha a parancsfájl törzsének (után a Súgó) első elemében függvény határozza meg, legalább két üres sorok Súgó-szkript és a függvény deklarációjában között lehet. Ellenkező esetben a Súgó értelmezi, hogy a Súgó a függvény esetében a szkript nem súgója.

## <a name="examples-of-help-placement-in-a-script"></a>Súgó az Elhelyezés a parancsfájl példái

 Az alábbi példák bemutatják az elhelyezési lehetőségek Megjegyzés-alapú segítségét az parancsprogramok.

### <a name="help-at-the-beginning-of-a-script"></a>A parancsfájl elején Súgó

 Az alábbi példa bemutatja a Megjegyzés-alapú, a parancsfájl elején.

```
<#
.Description
This script performs a series of network connection tests.
#>

param [string]$ComputerName
...
```

### <a name="help-at-the-end-of-a-script"></a>A szkript végén található Súgó

 Az alábbi példa bemutatja, hogy a parancsfájl végén található megjegyzés-alapú.

```powershell
...
function Ping { Test-Connection -ComputerName $ComputerName }

<#
.Description
This script performs a series of network connection tests.
#>

```