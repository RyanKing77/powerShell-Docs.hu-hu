---
title: Megjegyzések hozzáadása egy parancsmag súgó-témakörének |} A Microsoft Docs
ms.custom: ''
ms.date: 09/12/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 2bea35e5-b680-4f86-b928-176890aac99d
caps.latest.revision: 5
ms.openlocfilehash: 4e9ca9a3bbcbc900d079b9275bc47d21de9e2996
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56851197"
---
# <a name="how-to-add-notes-to-a-cmdlet-help-topic"></a>Jegyzetek hozzáadása egy parancsmagokkal kapcsolatos súgótémakörhöz

Ez a szakasz ismerteti a megjegyzések szakasza Windows PowerShell® parancsmag Súgó-témakör hozzáadása. A megjegyzések szakasza azt ismertetik, amelyek nem férnek el egyszerűen a többi strukturált szakaszokra, például egy paraméter részletesebb magyarázatáért részletek szolgál. Ez a tartalom magában foglalhatja a parancsmag működését egy adott szolgáltató, néhány egyedi, de fontos, használja a parancsmag vagy a lehetséges hibaállapotok elkerülésének fűzött megjegyzések.

Tudomásul veszi, hogy is hozzáadhat a megjegyzések szakasza száma nincs korlátozva van. Minden egyes Megjegyzés hozzáadása egy \<maml:alert > címkét rendel a \<maml:alertset > csomópont. Az egyes Megjegyzés tartalmakról halmazába \<maml:para > címkéket. Használat üres \<maml:para > térköze címke.

A következő XML-mutatja egy \<maml:alertset > csomópont két megjegyzések. Figyelje meg, hogy minden egyes Megjegyzés rendelkezik egy nem kötelező \<maml:title > címke (címek segítségével minden olyan csoport \<maml:alert > címkék), és, hogy minden egyes Megjegyzés rendelkezik egy üres sort térköz tartalmát a következő.

```xml
<maml:alertSet>
  <maml:title>title for Note 1</maml:title>
  <maml:alert>
    <maml:para> Note 1</maml:para>
    <maml:para></maml:para>
  </maml:alert>
  <maml:title>title for Note 2</maml:title>
  <maml:alert>
    <maml:para> Note 1</maml:para>
    <maml:para></maml:para>
  </maml:alert>
</maml:alertSet>
```



