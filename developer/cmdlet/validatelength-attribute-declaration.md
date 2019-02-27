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
ms.openlocfilehash: 1e8364c78abba5272007019550ffcb2cedaf9fd0
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56848817"
---
# <a name="validatelength-attribute-declaration"></a>ValidateLength attribútumdeklarációja

A ValidateLength attribútum határozza meg, hogy egy parancsmag-paraméterrel argumentumként karakterek minimális és maximális száma. Ez az attribútum is használható Windows PowerShell-függvényekkel.

## <a name="syntax"></a>Szintaxis

```csharp
[ValidateLength(int minLength, int maxlength)]
```

#### <a name="parameters"></a>Paraméterek

`MinLength` ([System.Integer](/dotnet/api/System.Integer)) szükséges. Meghatározza az engedélyezett karakterek minimális számát.

`MaxLength` ([System.Integer](/dotnet/api/System.Integer)) szükséges. Meghatározza az engedélyezett maximális karakterszámot.

## <a name="remarks"></a>Megjegyzés

- Ezt az attribútumot deklarálni kapcsolatos további információkért lásd: [bemenet-ellenőrzési szabályok deklarálja hogyan](http://msdn.microsoft.com/en-us/544c2100-62ba-4be4-b2a2-cc0d4e4fc45b).
- Ezt az attribútumot deklarálni kapcsolatos további információkért lásd: [bemenet-ellenőrzési szabályok deklarálja hogyan](http://msdn.microsoft.com/en-us/544c2100-62ba-4be4-b2a2-cc0d4e4fc45b).

- Ez az attribútum nem használata esetén a megfelelő paraméterargumentum lehet hossza.

- A Windows PowerShell-modul a következő feltételek hibát jelez:

    - Amikor értékét a `MaxLength` attribútum paraméter értéke kisebb, mint az értékét a `MinLength` paraméter attribútum.

    - Ha a `MaxLength` attribútum paraméter 0 értékre van állítva.

    - Ha az argumentuma nem karakterlánc.

- A ValidateLength attribútum határozza meg a [System.Management.Automation.Validatelengthattribute](/dotnet/api/System.Management.Automation.ValidateLengthAttribute) osztály.

## <a name="see-also"></a>Lásd még:

[System.Management.Automation.Validatelengthattribute](/dotnet/api/System.Management.Automation.ValidateLengthAttribute)

[Egy Windows PowerShell-parancsmag írása](./writing-a-windows-powershell-cmdlet.md)
