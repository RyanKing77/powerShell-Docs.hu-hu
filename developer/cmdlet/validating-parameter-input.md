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
ms.openlocfilehash: f7e5d4fb2f89bd6bc7036fdcff8f38e017d5d0e4
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56848803"
---
# <a name="validating-parameter-input"></a>Paraméterbevitel érvényesítése

Windows PowerShell parancsmag-paraméterek többféleképpen számára továbbított argumentumok ellenőrizheti. Windows PowerShell ellenőrizheti a hossza, a tartomány és a minta az argumentum a karaktereket. Ellenőrizheti, hogy a rendelkezésre álló argumentumok (count) száma. Ezek a szabályok érvényesítése érvényesítési attribútumokat, amelyek deklarált a nyilvános tulajdonságok parancsmag osztály paraméter attribútummal határozza meg.

A paraméterargumentum ellenőrzése, a Windows PowerShell-modul a parancsmag futtatása előtt, győződjön meg arról, hogy a paraméter értékét, az érvényesítési attribútumok által biztosított információkat használja. Ha a paraméter bemeneti nem érvényes, akkor a felhasználó hibaüzenetet kap. Minden egyes érvényesítési paraméter határozza meg, hogy egy érvényesítési szabály, amely kikényszeríti a Windows PowerShell.

Windows PowerShell kikényszeríti az ellenőrzési szabályok alapján a következő attribútumokkal.

ValidateCount paraméter elfogadó argumentumok minimális és maximális számát adja meg. Ennek az attribútumnak kódcsomagjaihoz a szintaxissal kapcsolatos további információkért lásd: [ValidateCount típusattribútum-deklaráció](./validatecount-attribute-declaration.md).

ValidateLength a paraméterargumentum karakterek minimális és maximális száma határozza meg. Ennek az attribútumnak kódcsomagjaihoz a szintaxissal kapcsolatos további információkért lásd: [ValidateLength típusattribútum-deklaráció](./validatelength-attribute-declaration.md).

ValidatePattern adja meg, amely ellenőrzi a paraméterargumentum reguláris kifejezést. Ennek az attribútumnak kódcsomagjaihoz a szintaxissal kapcsolatos további információkért lásd: [ValidatePattern típusattribútum-deklaráció](./validatepattern-attribute-declaration.md).

ValidateRange megadja a paraméterargumentum minimális és maximális értékét. Ennek az attribútumnak kódcsomagjaihoz a szintaxissal kapcsolatos további információkért lásd: [ValidateRange típusattribútum-deklaráció](./validaterange-attribute-declaration.md).

ValidateSet adja meg az érvényes értékek a paraméter argumentum. Ennek az attribútumnak kódcsomagjaihoz a szintaxissal kapcsolatos további információkért lásd: [ValidateSet típusattribútum-deklaráció](./validateset-attribute-declaration.md).

## <a name="see-also"></a>Lásd még:

[A paraméter bemeneti ellenőrzése](./how-to-validate-parameter-input.md)

[Egy Windows PowerShell-parancsmag írása](./writing-a-windows-powershell-cmdlet.md)
