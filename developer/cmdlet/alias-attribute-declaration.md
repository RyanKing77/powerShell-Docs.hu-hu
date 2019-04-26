---
title: Alias típusattribútum-deklaráció |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Alias attribute
- attributes, Alias
- Alias attribute, described
ms.assetid: d0df3a46-b1cc-42b9-beb1-e16bce254007
caps.latest.revision: 10
ms.openlocfilehash: 4d20672c5181c994c1b53624f6c42a301db11f26
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62068714"
---
# <a name="alias-attribute-declaration"></a>Aliasok attribútumdeklarációja

Az Alias attribútum lehetővé teszi, hogy a felhasználó számára adjon meg másik nevet egy parancsmag-paraméterben. Aliasok használható billentyűparancsok adja meg a paraméter neve, vagy megfelelő különböző helyzetekhez különböző neveket is biztosítanak.

## <a name="syntax"></a>Szintaxis

```csharp
[Alias(aliasNames)]
```

#### <a name="parameters"></a>Paraméterek

`aliasName` (String[]) Szükséges. Alias vesszővel elválasztott neveket a parancsmag paraméter egy halmazát határozza meg.

## <a name="remarks"></a>Megjegyzés

- Amikor megad egy parancsmag-paraméterben az Alias attribútum használnak a paraméter-attribútumhoz. Ezek az attribútumok deklarálja kapcsolatos további információkért lásd: [deklarálja parancsmag-paraméterek hogyan](./how-to-declare-cmdlet-parameters.md).

- Minden egyes aliasnevet egy parancsmag egyedinek kell lennie. Windows PowerShell nem ellenőrzi az ismétlődő alias nevét.

- Az Alias attribútum mindegyik paraméterhez, a parancsmag az egyszer használatos.

- Az Alias attribútum határozza meg a [System.Management.Automation.Aliasattribute](/dotnet/api/System.Management.Automation.AliasAttribute) osztály.

## <a name="see-also"></a>Lásd még:

[A paraméter-aliasok](./parameter-aliases.md)

[Egy Windows PowerShell-parancsmag írása](./writing-a-windows-powershell-cmdlet.md)
