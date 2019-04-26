---
title: ValidateCount típusattribútum-deklaráció |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- attributes, ValidateCount
- ValidateCount attribute, described
- ValidateCount attribute
ms.assetid: 516af1ef-2c2e-408d-84bc-865f5bccf761
caps.latest.revision: 11
ms.openlocfilehash: ffc45f6b80a2b7ed22f27d083d042b1de7f353f6
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62067178"
---
# <a name="validatecount-attribute-declaration"></a>ValidateCount attribútumdeklarációja

A ValidateCount attribútum határozza meg a minimális és maximális számú argumentum az engedélyezett egy parancsmag-paraméterben.

## <a name="syntax"></a>Szintaxis

```csharp
[ValidateCount(int minLength, int maxlength)]
```

#### <a name="parameters"></a>Paraméterek

`MinLength` ([System.Int32][]) szükséges. Adja meg a minimális számú argumentumot.

`MaxLength`([System.Int32][]) szükséges. Megadja a maximális számú argumentumot.

## <a name="remarks"></a>Megjegyzés

- Ezt az attribútumot deklarálni kapcsolatos további információkért lásd: [Az argumentumok száma ellenőrzése][].

- Ez az attribútum nem hív, ha a megfelelő parancsmag paraméter rendelkezhet tetszőleges számú argumentum.

- A Windows PowerShell-modul a következő feltételek hibát jelez:

    - A `MinLength` és `MaxLength` attribútum paraméterek nejsou typu [System.Int32][].

    - Értékét a `MaxLength` attribútum paraméter értéke kisebb, mint az értékét a `MinLength` paraméter attribútum.

- A ValidateCount attribútum határozza meg a [System.Management.Automation.ValidateCountAttribute][] osztály.

## <a name="see-also"></a>Lásd még:

[System.Management.Automation.ValidateCountAttribute][]

[Az argumentumok száma ellenőrzése][]

[Egy Windows PowerShell-parancsmag írása][]

[Az argumentumok száma ellenőrzése]: how-to-validate-an-argument-count.md
[Egy Windows PowerShell-parancsmag írása]: writing-a-windows-powershell-cmdlet.md

[System.Int32]: /dotnet/api/System.Int32
[System.Management.Automation.ValidateCountAttribute]: /dotnet/api/System.Management.Automation.ValidateCountAttribute
