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
# <a name="cmdlet-attributes"></a><span data-ttu-id="b2ece-102">Parancsmag-attribútumok</span><span class="sxs-lookup"><span data-stu-id="b2ece-102">Cmdlet Attributes</span></span>

<span data-ttu-id="b2ece-103">Windows PowerShell határozza meg, hogy számos attribútum, amellyel közös funkciók hozzáadása a parancsmagokat a funkció a saját kód implementálása nélkül.</span><span class="sxs-lookup"><span data-stu-id="b2ece-103">Windows PowerShell defines several attributes that you can use to add common functionality to your cmdlets without implementing that functionality within your own code.</span></span> <span data-ttu-id="b2ece-104">Ez magában foglalja a parancsmag attribútum, amely azonosítja az OutputType attribútummal, amely meghatározza a .NET-keretrendszer típusok, a parancsmag a paraméter-attribútumhoz, amely azonosítja a nyilvános tulajdonságok, a parancsmag által visszaadott parancsmag osztályok, a Microsoft .NET-keretrendszer osztály paraméterek és további.</span><span class="sxs-lookup"><span data-stu-id="b2ece-104">This includes the Cmdlet attribute that identifies a Microsoft .NET Framework class as a cmdlet class, the OutputType attribute that specifies the .NET Framework types returned by the cmdlet, the Parameter attribute that identifies public properties as cmdlet parameters, and more.</span></span>

## <a name="in-this-section"></a><span data-ttu-id="b2ece-105">A szakasz tartalma</span><span class="sxs-lookup"><span data-stu-id="b2ece-105">In This Section</span></span>

<span data-ttu-id="b2ece-106">[A parancsmag Code attribútumok](./attributes-in-cmdlet-code.md) attribútumok használata a kódban a parancsmag előnyeit ismerteti.</span><span class="sxs-lookup"><span data-stu-id="b2ece-106">[Attributes in Cmdlet Code](./attributes-in-cmdlet-code.md) Describes the benefit of using attributes in cmdlet code.</span></span>

<span data-ttu-id="b2ece-107">[Attribútum típusa](./attribute-types.md) is megadhat egy parancsmag osztály különböző attribútumokat ismerteti.</span><span class="sxs-lookup"><span data-stu-id="b2ece-107">[Attribute Types](./attribute-types.md) Describes the different attributes that can decorate a cmdlet class.</span></span>

<span data-ttu-id="b2ece-108">[Alias típusattribútum-deklaráció](./alias-attribute-declaration.md) parancsmag a paraméter nevének aliasok definiálását mutatja.</span><span class="sxs-lookup"><span data-stu-id="b2ece-108">[Alias Attribute Declaration](./alias-attribute-declaration.md) Describes how to define aliases for a cmdlet parameter name.</span></span>

<span data-ttu-id="b2ece-109">[A parancsmag típusattribútum-deklaráció](./cmdlet-attribute-declaration.md) ismerteti, hogyan lehet a parancsmag egy .NET-keretrendszer osztályt kell definiálni.</span><span class="sxs-lookup"><span data-stu-id="b2ece-109">[Cmdlet Attribute Declaration](./cmdlet-attribute-declaration.md) Describes how to define a .NET Framework class as a cmdlet.</span></span>

<span data-ttu-id="b2ece-110">[Hitelesítőadat-típusattribútum-deklaráció](./credential-attribute-declaration.md) karakterláncot tartalmazó bemeneti való konvertálása támogatása hozzáadása egy [System.Management.Automation.PSCredential](/dotnet/api/System.Management.Automation.PSCredential) objektum.</span><span class="sxs-lookup"><span data-stu-id="b2ece-110">[Credential Attribute Declaration](./credential-attribute-declaration.md) Describes how to add support for converting string input into a [System.Management.Automation.PSCredential](/dotnet/api/System.Management.Automation.PSCredential) object.</span></span>

<span data-ttu-id="b2ece-111">[Deklarace OutputType attribútummal](./outputtype-attribute-declaration.md) ismerteti, hogyan lehet a .NET-keretrendszer típusok, a parancsmag által visszaadott adja meg.</span><span class="sxs-lookup"><span data-stu-id="b2ece-111">[OutputType attribute Declaration](./outputtype-attribute-declaration.md) Describes how to specify the .NET Framework types returned by the cmdlet.</span></span>

<span data-ttu-id="b2ece-112">[Deklarace parametru attribútum](./parameter-attribute-declaration.md) ismerteti, hogyan lehet egy parancsmag paramétereinek megadása.</span><span class="sxs-lookup"><span data-stu-id="b2ece-112">[Parameter Attribute Declaration](./parameter-attribute-declaration.md) Describes how to define the parameters of a cmdlet.</span></span>

<span data-ttu-id="b2ece-113">[ValidateCount típusattribútum-deklaráció](./validatecount-attribute-declaration.md) azt ismerteti, hogyan adhat meg, hány argumentumok egy paraméter engedélyezett.</span><span class="sxs-lookup"><span data-stu-id="b2ece-113">[ValidateCount Attribute Declaration](./validatecount-attribute-declaration.md) Describes how to define how many arguments are allowed for a parameter.</span></span>

<span data-ttu-id="b2ece-114">[ValidateLength típusattribútum-deklaráció](./validatelength-attribute-declaration.md) ismerteti, hogyan lehet a hossza (karakter) egy paraméter argumentum megadása.</span><span class="sxs-lookup"><span data-stu-id="b2ece-114">[ValidateLength Attribute Declaration](./validatelength-attribute-declaration.md) Describes how to define the length (in characters) of a parameter argument.</span></span>

<span data-ttu-id="b2ece-115">[ValidatePattern típusattribútum-deklaráció](./validatepattern-attribute-declaration.md) egy paraméter argumentumként a érvényes minták definiálását mutatja.</span><span class="sxs-lookup"><span data-stu-id="b2ece-115">[ValidatePattern Attribute Declaration](./validatepattern-attribute-declaration.md) Describes how to define the valid patterns for a parameter argument.</span></span>

<span data-ttu-id="b2ece-116">[ValidateRange típusattribútum-deklaráció](./validaterange-attribute-declaration.md) ismerteti, hogyan lehet egy paraméterargumentum érvényes tartományának megadása.</span><span class="sxs-lookup"><span data-stu-id="b2ece-116">[ValidateRange Attribute Declaration](./validaterange-attribute-declaration.md) Describes how to define the valid range for a parameter argument.</span></span>

<span data-ttu-id="b2ece-117">[ValidateSet típusattribútum-deklaráció](./validateset-attribute-declaration.md) egy paraméter paraméter lehetséges értékei definiálását mutatja.</span><span class="sxs-lookup"><span data-stu-id="b2ece-117">[ValidateSet Attribute Declaration](./validateset-attribute-declaration.md) Describes how to define the possible values for a parameter argument.</span></span>

## <a name="reference"></a><span data-ttu-id="b2ece-118">Referencia</span><span class="sxs-lookup"><span data-stu-id="b2ece-118">Reference</span></span>

[<span data-ttu-id="b2ece-119">Egy Windows PowerShell-parancsmag írása</span><span class="sxs-lookup"><span data-stu-id="b2ece-119">Writing a Windows PowerShell Cmdlet</span></span>](./writing-a-windows-powershell-cmdlet.md)
