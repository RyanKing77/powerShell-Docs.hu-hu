---
title: ValidatePattern típusattribútum-deklaráció |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- attributes, ValidatePattern
- ValidatePattern attribute, described
- ValidatePattern attribute
ms.assetid: 87b811be-6d93-4e7d-b9d0-c567a19bb0ef
caps.latest.revision: 13
ms.openlocfilehash: 5edcb65a6fbe1cb2fe2d0efe3f763fb84628b049
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56848824"
---
# <a name="validatepattern-attribute-declaration"></a>ValidatePattern attribútumdeklarációja

A ValidatePattern attribútum határozza meg, amely ellenőrzi az argumentuma egy parancsmag-paraméterben Reguláriskifejezés-mintának. Ez az attribútum is használható Windows PowerShell-függvényekkel.

ValidatePattern belül egy parancsmag meghívása, amikor a Windows PowerShell-modul alakítja át a parancsmag-paraméterben argumentuma egy karakterlánc, és összehasonlítja az, hogy a minta az ValidatePattern attribútum által megadott karakterláncot. Csak akkor, ha az argumentum, és a megadott mintának konvertált karakteres formáját egyezik a parancsmagot futtatja. Ha nem egyeznek, a Windows PowerShell-modul által egy hiba lépett fel.

## <a name="syntax"></a>Szintaxis

```csharp
[ValidatePattern(string regexString)]
[ValidatePattern(string regexString, Named Parameters)]
```

#### <a name="parameters"></a>Paraméterek

`RegexString` ([System.String](/dotnet/api/System.String)) szükséges. Itt adhatja meg, amely ellenőrzi a paraméterargumentum reguláris kifejezést.

Beállítások ([System.Text.Regularexpressions.Regexoptions](/dotnet/api/System.Text.RegularExpressions.RegexOptions)) nevű paraméter nem kötelező. Adja meg a bitenkénti kombinációját [System.Text.Regularexpressions.Regexoptions](/dotnet/api/System.Text.RegularExpressions.RegexOptions) reguláris kifejezés beállítások meghatározó jelzők.

## <a name="remarks"></a>Megjegyzés

- Ez az attribútum csak egyszer használható paraméterenként.

- Használhatja a `Option` paraméter az attribútum a minta még jobban meghatározhatja. Például hogy a minta kis-és nagybetűket.

- Ez az attribútum egy gyűjtemény alkalmazza, ha minden elem a gyűjteményben lévő meg kell egyeznie a minta.

- A ValidatePattern attribútum határozza meg a [System.Management.Automation.Validatepatternattribute](/dotnet/api/System.Management.Automation.ValidatePatternAttribute) osztály.

## <a name="see-also"></a>Lásd még:

[System.Management.Automation.Validatepatternattribute](/dotnet/api/System.Management.Automation.ValidatePatternAttribute)

[Egy Windows PowerShell-parancsmag írása](./writing-a-windows-powershell-cmdlet.md)
