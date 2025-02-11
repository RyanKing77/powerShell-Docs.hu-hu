---
title: A parancsmag attribútumok |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- attributes [PowerShell SDK]
- attributes [PowerShell SDK], described
ms.assetid: d3f4f652-d929-4c27-9358-9baa390a094c
caps.latest.revision: 14
ms.openlocfilehash: 326cd408e86402974569fc76d5e473be5a56f0b6
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62068606"
---
# <a name="cmdlet-attributes"></a>Parancsmag-attribútumok

Windows PowerShell határozza meg, hogy számos attribútum, amellyel közös funkciók hozzáadása a parancsmagokat a funkció a saját kód implementálása nélkül. Ez magában foglalja a parancsmag attribútum, amely azonosítja az OutputType attribútummal, amely meghatározza a .NET-keretrendszer típusok, a parancsmag a paraméter-attribútumhoz, amely azonosítja a nyilvános tulajdonságok, a parancsmag által visszaadott parancsmag osztályok, a Microsoft .NET-keretrendszer osztály paraméterek és további.

## <a name="in-this-section"></a>A szakasz tartalma

[A parancsmag Code attribútumok](./attributes-in-cmdlet-code.md) attribútumok használata a kódban a parancsmag előnyeit ismerteti.

[Attribútum típusa](./attribute-types.md) is megadhat egy parancsmag osztály különböző attribútumokat ismerteti.

[Alias típusattribútum-deklaráció](./alias-attribute-declaration.md) parancsmag a paraméter nevének aliasok definiálását mutatja.

[A parancsmag típusattribútum-deklaráció](./cmdlet-attribute-declaration.md) ismerteti, hogyan lehet a parancsmag egy .NET-keretrendszer osztályt kell definiálni.

[Hitelesítőadat-típusattribútum-deklaráció](./credential-attribute-declaration.md) karakterláncot tartalmazó bemeneti való konvertálása támogatása hozzáadása egy [System.Management.Automation.PSCredential](/dotnet/api/System.Management.Automation.PSCredential) objektum.

[Deklarace OutputType attribútummal](./outputtype-attribute-declaration.md) ismerteti, hogyan lehet a .NET-keretrendszer típusok, a parancsmag által visszaadott adja meg.

[Deklarace parametru attribútum](./parameter-attribute-declaration.md) ismerteti, hogyan lehet egy parancsmag paramétereinek megadása.

[ValidateCount típusattribútum-deklaráció](./validatecount-attribute-declaration.md) azt ismerteti, hogyan adhat meg, hány argumentumok egy paraméter engedélyezett.

[ValidateLength típusattribútum-deklaráció](./validatelength-attribute-declaration.md) ismerteti, hogyan lehet a hossza (karakter) egy paraméter argumentum megadása.

[ValidatePattern típusattribútum-deklaráció](./validatepattern-attribute-declaration.md) egy paraméter argumentumként a érvényes minták definiálását mutatja.

[ValidateRange típusattribútum-deklaráció](./validaterange-attribute-declaration.md) ismerteti, hogyan lehet egy paraméterargumentum érvényes tartományának megadása.

[ValidateSet típusattribútum-deklaráció](./validateset-attribute-declaration.md) egy paraméter paraméter lehetséges értékei definiálását mutatja.

## <a name="reference"></a>Referencia

[Egy Windows PowerShell-parancsmag írása](./writing-a-windows-powershell-cmdlet.md)
