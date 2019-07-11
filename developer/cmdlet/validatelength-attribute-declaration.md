---
title: ValidateLength típusattribútum-deklaráció |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- ValidateLength attribute, described
- attributes, ValidateLength
- ValidateLength attribute
ms.assetid: 82fe3a35-a94b-4bc1-ad9e-dfc5f1e788b3
caps.latest.revision: 13
ms.openlocfilehash: a25fa2410fcc6803563573596af1bc99052c3ffa
ms.sourcegitcommit: 46bebe692689ebedfe65ff2c828fe666b443198d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/10/2019
ms.locfileid: "67735110"
---
# <a name="validatelength-attribute-declaration"></a>ValidateLength attribútumdeklarációja

A ValidateLength attribútum határozza meg, hogy egy parancsmag-paraméterrel argumentumként karakterek minimális és maximális száma. Ez az attribútum is használható Windows PowerShell-függvényekkel.

## <a name="syntax"></a>Szintaxis

```csharp
[ValidateLength(int minLength, int maxlength)]
```

#### <a name="parameters"></a>Paraméterek

`MinLength` ([System.Int32](/dotnet/api/System.Int32)) szükséges. Meghatározza az engedélyezett karakterek minimális számát.

`MaxLength` ([System.Int32](/dotnet/api/System.Int32)) szükséges. Meghatározza az engedélyezett maximális karakterszámot.

## <a name="remarks"></a>Megjegyzés

- Ezt az attribútumot deklarálni kapcsolatos további információkért lásd: [bemenet-ellenőrzési szabályok deklarálja hogyan](./how-to-validate-parameter-input.md).

- Ez az attribútum nem használata esetén a megfelelő paraméterargumentum lehet hossza.

- A Windows PowerShell-modul a következő feltételek hibát jelez:

    - Amikor értékét a `MaxLength` attribútum paraméter értéke kisebb, mint az értékét a `MinLength` paraméter attribútum.

    - Ha a `MaxLength` attribútum paraméter 0 értékre van állítva.

    - Ha az argumentuma nem karakterlánc.

- A ValidateLength attribútum határozza meg a [System.Management.Automation.Validatelengthattribute](/dotnet/api/System.Management.Automation.ValidateLengthAttribute) osztály.

## <a name="see-also"></a>Lásd még:

[System.Management.Automation.Validatelengthattribute](/dotnet/api/System.Management.Automation.ValidateLengthAttribute)

[Egy Windows PowerShell-parancsmag írása](./writing-a-windows-powershell-cmdlet.md)
