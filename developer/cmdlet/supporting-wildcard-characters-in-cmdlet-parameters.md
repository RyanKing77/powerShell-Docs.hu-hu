---
title: A helyettesítő karakterek támogató parancsmag-paraméterek |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- wildcards [PowerShell Programmer's Guide]
- parameters [PowerShell Programmer's Guide], wildcards
ms.assetid: 9b26e1e9-9350-4a5a-aad5-ddcece658d93
caps.latest.revision: 12
ms.openlocfilehash: 6c762d3889bc4b649252390625525db4735f4c1d
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62067399"
---
# <a name="supporting-wildcard-characters-in-cmdlet-parameters"></a>Helyettesítő karakterek támogatása parancsmag-paraméterekben

Gyakran előfordul akkor tervezhet a parancsmag futtatásához az erőforrások csoportjához, nem pedig egy egyetlen erőforrás ellen. Például a parancsmag található összes fájl egy azonos nevű vagy kiterjesztéssel rendelkező adattárban előfordulhat, hogy kell. Egy parancsmag, amely akkor erőforrások csoportjához kialakításakor kell biztosítanak támogatást a helyettesítő karakterek.

> [!NOTE]
> A helyettesítő karakterek használatával van más néven *helyettesítés*.

## <a name="windows-powershell-cmdlets-that-use-wildcards"></a>A helyettesítő karakterek használata, a Windows PowerShell-parancsmagok

 Számos Windows PowerShell-parancsmagok a helyettesítő karakterek támogatása a paraméterértékeket. Ha például szinte minden parancsmag, amely rendelkezik egy `Name` vagy `Path` paraméter támogatja a helyettesítő karakterek ezeket a paramétereket. (Bár a legtöbb parancsmag, amely rendelkezik egy `Path` paraméter is rendelkezik egy `LiteralPath` paraméter, amely nem támogatja a helyettesítő karakterek.) A következő parancs bemutatja, hogyan helyettesítő karaktert adja vissza az összes parancsmagot a jelenlegi munkamenet, amelynek a neve tartalmazza a Get-verb szolgál.

 **PS > get-command get -\***

## <a name="supported-wildcard-characters"></a>Támogatott helyettesítő karakterek

Windows PowerShell támogatja a következő helyettesítő karaktereket.

|Helyettesítő karakter|Leírás|Példa|Egyezik|Nem egyezik|
|------------------------|-----------------|-------------|-------------|--------------------|
|*|A megadott pozíciótól kezdődően nulla vagy több karakterre illeszkedik|a*|A, ag, Apple||
|?|A megadott pozíciónál található egyezés anycharacter|?n|Egy, a, a|futott|
|[ ]|Egy karaktertartományt megfelel|[a-l]ook|könyv, cook, tekintse meg|tartott|
|[ ]|A megadott karakterre illeszkedik|[bc]ook|könyv, cook|nézd|

A helyettesítő karakterek támogató parancsmagok tervezésekor lehetővé teszi a helyettesítő karakterek kombinációját. Használja az alábbi parancs például a `Get-ChildItem` parancsmag a .txt fájlok, amelyek a c:\Techdocs mappában, és, betűkkel kezdődik "a" és "l."

**Get-childitem c:\techdocs\\[a-l]\*.txt**

Az előző parancs használja a tartomány helyettesítő **[a-l]** megadásához, hogy a fájl nevét kell karakterekkel kezdődnek "a" és "l." A parancsot, majd használja a * helyettesítő karaktert bármely karakter között a fájl nevének első betűje és a .txt kiterjesztése helyettesíti.

Az alábbi példában egy tartomány helyettesítő karakterrel, amely nem tartalmazza a "d" betű, de a "a" és "f." az összes többi betűt tartalmaz

**Get-childitem c:\techdocs\\[a-cef]\*.txt**

## <a name="handling-literal-characters-in-wildcard-patterns"></a>Helyettesítő karakterek mintái literális karakter kezelése

Ha a helyettesítő karakterrel megadott szövegkonstans karaktereket tartalmaz, használja a használni kívánt szintaxiskiemelést karaktert (') escape-karakter. Ha programozott módon adja meg a literális karakter, használja egy egyetlen használni kívánt szintaxiskiemelést. A parancssorban literális karakter megadása esetén két backticks használja. A következő mintát tartalmazza például két zárójelben, amely szerint kell értelmezni.

"John Smith \`[*"] "(megadott programozott módon)

"John Smith \` \`[*\`"] "(a parancssorban megadott)

Ez a minta illeszkedik "John Smith [Marketing]" vagy "John Smith [fejlesztési]".

## <a name="cmdlet-output-and-wildcard-characters"></a>A parancsmag kimenete és a helyettesítő karakterek

Parancsmag-paraméterek támogatja a helyettesítő karaktereket, amikor egy parancsmag-műveletet, az általában egy tömb kimeneti állít elő. Néha előfordul logikus nem támogatja a kimeneti, mert a felhasználó egyszerre csak egy elemet lehet, hogy használ egy tömb. Ha például a `Set-Location` parancsmag támogatja a tömb kimeneti, mert a felhasználó csak egyetlen helyen állítja. Ebben a példában a parancsmag továbbra is támogatja a helyettesítő karaktereket, de feloldási kényszerül, egyetlen helyen.

## <a name="see-also"></a>Lásd még:

[Egy Windows PowerShell-parancsmag írása](./writing-a-windows-powershell-cmdlet.md)

[WildcardPattern osztályban](/dotnet/api/system.management.automation.wildcardpattern)
