---
title: Helyettesítő karakterek támogatása parancsmag-paraméterekben
ms.custom: ''
ms.date: 08/26/2019
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.openlocfilehash: 19644c5bc186a5554d6b134a67fc7c4d7aa7b64c
ms.sourcegitcommit: a02ccbeaa17c0e513d6c4a21b877c88ac7725458
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/28/2019
ms.locfileid: "70104448"
---
# <a name="supporting-wildcard-characters-in-cmdlet-parameters"></a>Helyettesítő karakterek támogatása parancsmag-paraméterekben

Gyakran olyan parancsmagot kell megterveznie, amely egy erőforrás-csoporton fut ahelyett, hogy egyetlen erőforrásra lenne szüksége. Előfordulhat például, hogy egy parancsmagnak meg kell keresnie egy azonos nevű vagy kiterjesztésű adattár összes fájlját. Meg kell adnia a helyettesítő karakterek támogatását, ha olyan parancsmagot tervez, amely egy erőforrás-csoporton fog futni.

> [!NOTE]
> A helyettesítő karakterek használata más néven *globbing*.

## <a name="windows-powershell-cmdlets-that-use-wildcards"></a>Helyettesítő karaktereket használó Windows PowerShell-parancsmagok

 Számos Windows PowerShell-parancsmag támogatja a helyettesítő karaktereket a paraméter értékeinél. Például szinte minden olyan parancsmag, amely a vagy `Name` `Path` a paraméterrel rendelkezik, helyettesítő karaktereket is támogat ezekhez a paraméterekhez. (Habár a `Path` paraméterrel rendelkező legtöbb parancsmag olyan paraméterrel is `LiteralPath` rendelkezik, amely nem támogatja a helyettesítő karaktereket.) A következő parancs bemutatja, hogyan használható helyettesítő karakter az aktuális munkamenetben lévő összes olyan parancsmag visszaküldéséhez, amelynek a neve tartalmazza a Get műveletet.

 `Get-Command get-*`

## <a name="supported-wildcard-characters"></a>Támogatott helyettesítő karakterek

A Windows PowerShell a következő helyettesítő karaktereket támogatja.

| Helyettesítő |                             Leírás                             |  Példa   |     Egyezik      | Nem egyezik |
| -------- | ------------------------------------------------------------------- | ---------- | ---------------- | -------------- |
| *        | Nulla vagy több karakternek felel meg, a megadott pozíciótól kezdve | `a*`       | A, AG, Apple     |                |
| ?        | Minden karakternek megfelel a megadott pozícióban                     | `?n`       | Egy, a, be       | futott            |
| [ ]      | Számos karakterből áll                                       | `[a-l]ook` | könyv, Cook, Look | Zug, elvitt     |
| [ ]      | Megfelel a megadott karaktereknek                                    | `[bn]ook`  | könyv, Zug       | Cook, Look     |

A helyettesítő karaktereket támogató parancsmagok tervezésekor engedélyezze a helyettesítő karakterek kombinációját. A következő parancs például a `Get-ChildItem` parancsmag használatával kéri le a c:\Techdocs mappában található összes. txt fájlt, amely az "a" betűvel kezdődik az "l" értékkel.

`Get-ChildItem c:\techdocs\[a-l]\*.txt`

Az előző parancs a tartomány helyettesítő karakterét `[a-l]` használja annak megadásához, hogy a fájl nevének az "a" karakterrel kell kezdődnie, és a `*` helyettesítő karaktert használja helyőrzőként a fájlnév első betűje és a a **. txt** kiterjesztés.

Az alábbi példa egy tartományhoz tartozó helyettesítő karaktert használ, amely kizárja a "d" betűt, de az "a" és az "f" közötti összes többi betűt is tartalmazza.

`Get-ChildItem c:\techdocs\[a-cef]\*.txt`

## <a name="handling-literal-characters-in-wildcard-patterns"></a>Literális karakterek használata helyettesítő karakteres mintákban

Ha a megadott helyettesítő karakter olyan literál karaktereket tartalmaz, amelyek nem értelmezendő helyettesítő karakterként, használja a kezdő karaktert (`` ` ``) Escape-karakterként. Ha literál karaktereket ad meg a PowerShell API-val, egyetlen kezdő használjon. Ha literál karaktereket ad meg a PowerShell parancssorába, használjon két aposztrófokkal.

Az alábbi minta például két zárójelet tartalmaz, amelyeket szó szerint kell elvégeznie.

A PowerShell API használatakor használja a következőket:

- "John Smith \`[*"] "

A PowerShell-parancssorból való használat esetén:

- "John Smith \` \`[*\`"] "

Ez a minta a következőnek felel meg: "John Smith [marketing]" vagy "John Smith [Development]". Például:

```
PS> "John Smith [Marketing]" -like "John Smith ``[*``]"
True

PS> "John Smith [Development]" -like "John Smith ``[*``]"
True
```

## <a name="cmdlet-output-and-wildcard-characters"></a>Parancsmag kimenete és helyettesítő karakterei

Ha a parancsmag paraméterei helyettesítő karaktereket is támogatnak, a művelet általában egy tömb kimenetét állítja elő.
Alkalmanként a tömb kimenetét nem érdemes támogatni, mivel a felhasználó csak egyetlen elem használatát teszi lehetővé. A `Set-Location` parancsmag például nem támogatja a tömb kimenetét, mert a felhasználó csak egyetlen helyet állít be. Ebben az esetben a parancsmag továbbra is támogatja a helyettesítő karaktereket, de egyetlen helyre kényszeríti a feloldást.

## <a name="see-also"></a>Lásd még:

[Windows PowerShell-parancsmag írása](./writing-a-windows-powershell-cmdlet.md)

[WildcardPattern osztály](/dotnet/api/system.management.automation.wildcardpattern)
