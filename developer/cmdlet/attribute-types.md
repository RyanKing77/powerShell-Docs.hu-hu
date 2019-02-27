---
title: Attribútum típusa |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 9b1026ad-f072-4fca-8052-a2d8eb491c2a
caps.latest.revision: 6
ms.openlocfilehash: 52c75b3ca73706da39029d5b3ead52ff7197a5f1
ms.sourcegitcommit: c581c4c8036edf55147e7bce4b00c860da6c5a8b
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/25/2019
ms.locfileid: "56852275"
---
# <a name="attribute-types"></a>Attribútumtípusok

A parancsmag attribútumok funkciók szerint csoportosíthatók.
Az alábbi szakaszok ismertetik a rendelkezésre álló attribútumok, és írja le milyen a futtatókörnyezet az attribútum meghívásakor.

## <a name="cmdlet-attributes"></a>Parancsmag-attribútumok

### <a name="cmdlet"></a>Parancsmag

A .NET-keretrendszer osztály azonosítja, a parancsmag.
Ez az a szükséges base attribútum.
További információkért lásd: [parancsmag típusattribútum-deklaráció](./cmdlet-attribute-declaration.md).

## <a name="parameter-attributes"></a>A paraméter-attribútumok

### <a name="parameter"></a>Paraméter

A parancsmag osztály a nyilvános tulajdonság azonosítja a parancsmag-paraméterként.
További információkért lásd: [paraméter típusattribútum-deklaráció](./parameter-attribute-declaration.md).

### <a name="alias"></a>Alias

Adja meg a paraméter egy vagy több aliast.
További információkért lásd: [Alias típusattribútum-deklaráció](./alias-attribute-declaration.md).

## <a name="argument-validation-attributes"></a>Argument érvényesítési attribútumok

### <a name="validatecount"></a>ValidateCount

Adja meg a minimális és maximális számú argumentumot engedélyezett egy parancsmag-paraméterben.
További információkért lásd: [ValidateCount típusattribútum-deklaráció](./validatecount-attribute-declaration.md).

### <a name="validatelength"></a>ValidateLength

Egy parancsmag paraméterargumentum karakterek minimális és maximális számát adja meg.
További információkért lásd: [ValidateLength típusattribútum-deklaráció](./validatelength-attribute-declaration.md).

### <a name="validatepattern"></a>ValidatePattern

Itt adhatja meg, hogy a parancsmag paraméterargumentum meg kell egyeznie a reguláris kifejezési minta.
További információkért lásd: [ValidatePattern típusattribútum-deklaráció](./validatepattern-attribute-declaration.md).

### <a name="validaterange"></a>ValidateRange

Adja meg a minimális és maximális értékeket a parancsmag paraméter argumentumként.
További információkért lásd: [ValidateRange típusattribútum-deklaráció](./validaterange-attribute-declaration.md).

### <a name="validateset"></a>ValidateSet

A parancsmag paraméterargumentum az érvényes értékek egy halmazát határozza meg.
További információkért lásd: [ValidateSet típusattribútum-deklaráció](./validateset-attribute-declaration.md).

## <a name="see-also"></a>Lásd még:

[Windows PowerShell SDK](../windows-powershell-reference.md)
