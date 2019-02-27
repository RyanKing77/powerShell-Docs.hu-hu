---
title: ValidateSet típusattribútum-deklaráció |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- attributes, ValidateSet
- ValidateSet attribute, described
- ValidateSet attribute
ms.assetid: 4a6f97ab-45b2-4f3d-84d4-30acf8e074d0
caps.latest.revision: 12
ms.openlocfilehash: b036f39cd01ffe4b4ce7db9627cb6da0d5327190
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56850455"
---
# <a name="validateset-attribute-declaration"></a>ValidateSet attribútumdeklarációja

A ValidateSetAttribute attribútum egy parancsmag paraméterargumentum a lehetséges értékek egy halmazát határozza meg. Ez az attribútum is használható Windows PowerShell-függvényekkel.

Ha ez az attribútum meg van adva, a Windows PowerShell-modul határozza meg, hogy a parancsmag-paraméterben megadott argumentum megegyezik-e a megadott elem beállítása egy eleme. A parancsmag csak akkor, ha a paraméterargumentum megegyezik a készletben lévő elem futtatja. Ha nem talál egyezést, egy hiba lépett fel a Windows PowerShell-modul által.

## <a name="syntax"></a>Szintaxis

```csharp
[ValidateSetAttribute(params string[] validValues)]
[ValidateSetAttribute(params string[] validValues, Named Parameters)]
```

#### <a name="parameters"></a>Paraméterek

`ValidValues` ([System.String](/dotnet/api/System.String)) szükséges. Megadja az elem érvényes paraméterértékeket. A következő minta bemutatja, hogyan elem egy vagy több olyan elemet adja meg.

```csharp
[ValidateSetAttribute("Steve")]
[ValidateSetAttribute("Steve","Mary")]
```

`IgnoreCase` ([System.Boolean](/dotnet/api/System.Boolean)) nevű paraméter nem kötelező. Az alapértelmezett érték `true` azt jelzi, hogy eset rendszer figyelmen kívül hagyja. Érték `false` lehetővé teszi a parancsmag kis-és nagybetűket.

## <a name="remarks"></a>Megjegyzés

- Ez az attribútum csak egyszer használható paraméterenként.

- Ha a paraméter értéke egy tömb, a tömb összes elemét meg kell egyeznie az attribútum a beállított eleme.

- A ValidateSetAttribute attribútum határozza meg a [System.Management.Automation.Validatesetattribute](/dotnet/api/System.Management.Automation.ValidateSetAttribute) osztály.

## <a name="see-also"></a>Lásd még:

[System.Management.Automation.Validatesetattribute](/dotnet/api/System.Management.Automation.ValidateSetAttribute)

[Egy Windows PowerShell-parancsmag írása](./writing-a-windows-powershell-cmdlet.md)
