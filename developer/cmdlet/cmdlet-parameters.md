---
title: Parancsmag-paraméterek |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- optional parameters [PowerShell SDK]
- aliases [PowerShell SDK]
- parameter sets [PowerShell SDK]
- parameters [PowerShell SDK]
- mandatory parameters [PowerShell SDK]
- positional parameters [PowerShell SDK]
- cmdlets [PowerShell SDK], parameters
ms.assetid: 3f1cca5f-5b95-4bce-94a6-a22db1aefd47
caps.latest.revision: 23
ms.openlocfilehash: 914a10907bcf980eed8d7e2f819c382fe6b341ad
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62068402"
---
# <a name="cmdlet-parameters"></a>Parancsmag-paraméterek

Parancsmag-paraméterek adja meg a mechanizmus, amely lehetővé teszi a parancsmag bemeneti fogadására. Paramétereket is fogad bevitelt a közvetlenül a parancssorból, vagy az objektumot a parancsmagnak átadni a folyamatban, az argumentumok (más néven *értékek*), ezeket a paramétereket adhatja meg a bemeneti, amely elfogadja a parancsmagot, a a parancsmag végre kell hajtania a műveletek és az adatok, amelyek a parancsmag visszaadja a folyamat számára.

## <a name="in-this-section"></a>A szakasz tartalma

[Tulajdonságok paraméterekként deklaráló](./declaring-properties-as-parameters.md) látnia kell, mielőtt azt deklarálja, hogy a parancsmag paramétereit alapvető információkat biztosít.

[Parancsmag-paraméterek típusú](./types-of-cmdlet-parameters.md) ismerteti a különböző típusú paramétereket, a parancsmagok eszközhöz adhat.

[Parancsmag paraméter nevének és a funkciók irányelvek](./standard-cmdlet-parameter-names-and-types.md) diszkosz a nevek, adattípus és funkciók a standard szintű paraméterek ajánlott.

[A paraméter-aliasok](./parameter-aliases.md) aliasról, amelyek a paraméterek számára definiálható ismerteti.

[Közös paraméterneveket](./common-parameter-names.md) Ez a témakör ismerteti, amely a Windows PowerShell-parancsmagok hozzáadása a paramétereket.

[A parancsmag paraméterkészletek](./cmdlet-parameter-sets.md) ismerteti, hogyan paraméter csoportok lehetővé teszik, hogy egyetlen parancsmag, amely a különböző helyzetekhez különböző műveleteket hajthat végre írási.

[A dinamikus parancsmag-paraméterek](./cmdlet-dynamic-parameters.md) különleges körülmények között a felhasználó számára elérhető paramétereket ismerteti.

[A helyettesítő karakterek támogató parancsmag-paraméterek](./supporting-wildcard-characters-in-cmdlet-parameters.md) ismerteti, hogyan lehet támogatást nyújt a helyettesítő karakterek egy parancsmag, amely akkor erőforrások csoportjához tervezésekor.

[A paraméter bemeneti ellenőrzése](./validating-parameter-input.md) ismerteti, hogyan a Windows PowerShell parancsmag-paraméterek számára továbbított argumentumok ellenőrzi.

[Adjon meg szűrési paraméterekhez](./input-filter-parameters.md) foglalkozik a `Filter`, `Include`, és `Exclude` szűrése, amely befolyásolja a parancsmag bemeneti objektumok készlete paramétereket.

## <a name="related-sections"></a>Kapcsolódó szakaszok

[A paraméter bemeneti ellenőrzése](./how-to-validate-parameter-input.md)

## <a name="see-also"></a>Lásd még:

[Deklarace parametru attribútum](./parameter-attribute-declaration.md)

[Windows PowerShell-parancsmagok](./cmdlet-overview.md)
