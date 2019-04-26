---
title: A paraméter bemeneti ellenőrzése |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- parameters, validation rules
- validation, examples
- validation
ms.assetid: 3f15bf20-a068-4a7d-a170-bc43f755d1fe
caps.latest.revision: 14
ms.openlocfilehash: 171e3e974619e197a0bcc9dfc759297005e34568
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62067144"
---
# <a name="validating-parameter-input"></a>Paraméterbevitel érvényesítése

PowerShell parancsmag-paraméterek többféleképpen számára továbbított argumentumok ellenőrizheti.
PowerShell ellenőrizheti a hossza, a tartomány és a minta az argumentum a karaktereket.
Ellenőrizheti, hogy a rendelkezésre álló argumentumok (count) száma.
Ezek a szabályok érvényesítése érvényesítési attribútumokat, amelyek deklarált a nyilvános tulajdonságok parancsmag osztály paraméter attribútummal határozza meg.

A paraméterargumentum ellenőrzéséhez a PowerShell-modul a parancsmag futtatása előtt, győződjön meg arról, hogy a paraméter értékét, az érvényesítési attribútumok által biztosított információkat használja.
Ha a paraméter bemeneti nem érvényes, akkor a felhasználó hibaüzenetet kap.
Minden egyes érvényesítési paraméter határozza meg, hogy egy érvényesítési szabály, amely kikényszeríti a PowerShell.

PowerShell az ellenőrzési szabályok alapján a következő attribútumok érvénybe lépteti.

### <a name="validatecount"></a>ValidateCount

Adja meg a minimális és maximális számú argumentumot, amely egy paraméter tud fogadni.
További információkért lásd: [ValidateCount típusattribútum-deklaráció](./validatecount-attribute-declaration.md).

### <a name="validatelength"></a>ValidateLength

A paraméterargumentum adja meg a minimális és maximális karakterszámot.
További információkért lásd: [ValidateLength típusattribútum-deklaráció](./validatelength-attribute-declaration.md).

### <a name="validatepattern"></a>ValidatePattern

Itt adhatja meg, amely ellenőrzi a paraméterargumentum reguláris kifejezést.
További információkért lásd: [ValidatePattern típusattribútum-deklaráció](./validatepattern-attribute-declaration.md).

### <a name="validaterange"></a>ValidateRange

Adja meg a paraméterargumentum minimális és maximális értékét.
További információkért lásd: [ValidateRange típusattribútum-deklaráció](./validaterange-attribute-declaration.md).

### <a name="validateset"></a>ValidateSet

Adja meg az érvényes értékek a paraméter argumentum.
További információkért lásd: [ValidateSet típusattribútum-deklaráció](./validateset-attribute-declaration.md).

## <a name="see-also"></a>Lásd még:

[A paraméter bemeneti ellenőrzése](./how-to-validate-parameter-input.md)

[Egy Windows PowerShell-parancsmag írása](./writing-a-windows-powershell-cmdlet.md)
