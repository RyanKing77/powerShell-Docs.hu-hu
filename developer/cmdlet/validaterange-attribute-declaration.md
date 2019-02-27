---
title: ValidateRange típusattribútum-deklaráció |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- ValidateRange, described
- ValidateRange attribute
- attributes, ValidateRange
ms.assetid: 1f8066e6-e5d3-4f4e-8948-a90af5dace82
caps.latest.revision: 11
ms.openlocfilehash: 155a406b9855c435041fe175ac7d983a4b4eb8b7
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56847536"
---
# <a name="validaterange-attribute-declaration"></a>ValidateRange attribútumdeklarációja

A ValidateRange attribútum határozza meg a minimális és maximális értékek (tartomány) a parancsmag paraméter argumentum. Ez az attribútum is használható Windows PowerShell-függvényekkel.

## <a name="syntax"></a>Szintaxis

```csharp
[ValidateRange(object minRange, object maxRange)]
```

#### <a name="parameters"></a>Paraméterek

`MinRange` ([System.Object](/dotnet/api/system.object)) szükséges. Meghatározza az engedélyezett minimális értéknél.

`MaxRange` ([System.Object](/dotnet/api/system.object)) szükséges. Megadja a maximális engedélyezett érték.

## <a name="remarks"></a>Megjegyzés

- A Windows PowerShell-modul egy konstrukció hibát jelenít amikor értékét a `MinRange` paraméter értéke nagyobb a `MaxRange` paraméter.

- A Windows PowerShell-modul a következő feltételek ellenőrzési hibát jelez:

    - Ha az argumentum értéke kisebb, mint a `MinRange` korlátot vagy nagyobb, mint a `MaxRange` korlátot.

    - Ha az argumentuma nem ugyanolyan típusú, mint a `MinRange` és a `MaxRange` paramétereket.

- A ValidateRange attribútum határozza meg a [System.Management.Automation.Validaterangeattribute](/dotnet/api/System.Management.Automation.ValidateRangeAttribute) osztály.

## <a name="see-also"></a>Lásd még:

[System.Management.Automation.Validaterangeattribute](/dotnet/api/System.Management.Automation.ValidateRangeAttribute)

[Egy Windows PowerShell-parancsmag írása](./writing-a-windows-powershell-cmdlet.md)
