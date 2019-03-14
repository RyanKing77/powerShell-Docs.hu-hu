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
ms.openlocfilehash: 4e0be34b6f7a56dcf02a4381de4d2a5d08db14df
ms.sourcegitcommit: 5990f04b8042ef2d8e571bec6d5b051e64c9921c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/12/2019
ms.locfileid: "57794440"
---
# <a name="validatecount-attribute-declaration"></a>ValidateCount attribútumdeklarációja

A ValidateCount attribútum határozza meg a minimális és maximális számú argumentum az engedélyezett egy parancsmag-paraméterben.

## <a name="syntax"></a>Szintaxis

```csharp
[ValidateCount(int minLength, int maxlength)]
```

#### <a name="parameters"></a>Paraméterek

`MinLength` ([System.Int32](/dotnet/api/System.Int32)) szükséges. Adja meg a minimális számú argumentumot.

`MaxLength`([System.Int32](/dotnet/api/System.Int32)) szükséges. Megadja a maximális számú argumentumot.

## <a name="remarks"></a>Megjegyzés

- Ezt az attribútumot deklarálni kapcsolatos további információkért lásd: [bemenet-ellenőrzési szabályok deklarálja hogyan](http://msdn.microsoft.com/en-us/544c2100-62ba-4be4-b2a2-cc0d4e4fc45b).

- Ez az attribútum nem hív, ha a megfelelő parancsmag paraméter rendelkezhet tetszőleges számú argumentum.

- A Windows PowerShell-modul a következő feltételek hibát jelez:

    - A `MinLength` és `MaxLength` attribútum paraméterek nejsou typu [System.Int32](/dotnet/api/System.Int32).

    - Értékét a `MaxLength` attribútum paraméter értéke kisebb, mint az értékét a `MinLength` paraméter attribútum.

- A ValidateCount attribútum határozza meg a [System.Management.Automation.Validatecount](/dotnet/api/System.Management.Automation.ValidateCount) osztály.

## <a name="see-also"></a>Lásd még:

[System.Management.Automation.Validatecount](/dotnet/api/System.Management.Automation.ValidateCount)

[Hogyan deklarálja a bemeneti érvényesítési szabályok](http://msdn.microsoft.com/en-us/544c2100-62ba-4be4-b2a2-cc0d4e4fc45b)

[Egy Windows PowerShell-parancsmag írása](./writing-a-windows-powershell-cmdlet.md)
