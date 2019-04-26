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
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62068657"
---
# <a name="attribute-types"></a><span data-ttu-id="4c045-102">Attribútumtípusok</span><span class="sxs-lookup"><span data-stu-id="4c045-102">Attribute Types</span></span>

<span data-ttu-id="4c045-103">A parancsmag attribútumok funkciók szerint csoportosíthatók.</span><span class="sxs-lookup"><span data-stu-id="4c045-103">Cmdlet attributes can be grouped by functionality.</span></span>
<span data-ttu-id="4c045-104">Az alábbi szakaszok ismertetik a rendelkezésre álló attribútumok, és írja le milyen a futtatókörnyezet az attribútum meghívásakor.</span><span class="sxs-lookup"><span data-stu-id="4c045-104">The following sections describe the available attributes and describe what the runtime does when the attribute is invoked.</span></span>

## <a name="cmdlet-attributes"></a><span data-ttu-id="4c045-105">Parancsmag-attribútumok</span><span class="sxs-lookup"><span data-stu-id="4c045-105">Cmdlet Attributes</span></span>

### <a name="cmdlet"></a><span data-ttu-id="4c045-106">Parancsmag</span><span class="sxs-lookup"><span data-stu-id="4c045-106">Cmdlet</span></span>

<span data-ttu-id="4c045-107">A .NET-keretrendszer osztály azonosítja, a parancsmag.</span><span class="sxs-lookup"><span data-stu-id="4c045-107">Identifies a .NET Framework class as a cmdlet.</span></span>
<span data-ttu-id="4c045-108">Ez az a szükséges base attribútum.</span><span class="sxs-lookup"><span data-stu-id="4c045-108">This is the required base attribute.</span></span>
<span data-ttu-id="4c045-109">További információkért lásd: [parancsmag típusattribútum-deklaráció](./cmdlet-attribute-declaration.md).</span><span class="sxs-lookup"><span data-stu-id="4c045-109">For more information, see [Cmdlet Attribute Declaration](./cmdlet-attribute-declaration.md).</span></span>

## <a name="parameter-attributes"></a><span data-ttu-id="4c045-110">A paraméter-attribútumok</span><span class="sxs-lookup"><span data-stu-id="4c045-110">Parameter Attributes</span></span>

### <a name="parameter"></a><span data-ttu-id="4c045-111">Paraméter</span><span class="sxs-lookup"><span data-stu-id="4c045-111">Parameter</span></span>

<span data-ttu-id="4c045-112">A parancsmag osztály a nyilvános tulajdonság azonosítja a parancsmag-paraméterként.</span><span class="sxs-lookup"><span data-stu-id="4c045-112">Identifies a public property in the cmdlet class as a cmdlet parameter.</span></span>
<span data-ttu-id="4c045-113">További információkért lásd: [paraméter típusattribútum-deklaráció](./parameter-attribute-declaration.md).</span><span class="sxs-lookup"><span data-stu-id="4c045-113">For more information, see [Parameter Attribute Declaration](./parameter-attribute-declaration.md).</span></span>

### <a name="alias"></a><span data-ttu-id="4c045-114">Alias</span><span class="sxs-lookup"><span data-stu-id="4c045-114">Alias</span></span>

<span data-ttu-id="4c045-115">Adja meg a paraméter egy vagy több aliast.</span><span class="sxs-lookup"><span data-stu-id="4c045-115">Specifies one or more aliases for a parameter.</span></span>
<span data-ttu-id="4c045-116">További információkért lásd: [Alias típusattribútum-deklaráció](./alias-attribute-declaration.md).</span><span class="sxs-lookup"><span data-stu-id="4c045-116">For more information, see [Alias Attribute Declaration](./alias-attribute-declaration.md).</span></span>

## <a name="argument-validation-attributes"></a><span data-ttu-id="4c045-117">Argument érvényesítési attribútumok</span><span class="sxs-lookup"><span data-stu-id="4c045-117">Argument Validation Attributes</span></span>

### <a name="validatecount"></a><span data-ttu-id="4c045-118">ValidateCount</span><span class="sxs-lookup"><span data-stu-id="4c045-118">ValidateCount</span></span>

<span data-ttu-id="4c045-119">Adja meg a minimális és maximális számú argumentumot engedélyezett egy parancsmag-paraméterben.</span><span class="sxs-lookup"><span data-stu-id="4c045-119">Specifies the minimum and maximum number of arguments that are allowed for a cmdlet parameter.</span></span>
<span data-ttu-id="4c045-120">További információkért lásd: [ValidateCount típusattribútum-deklaráció](./validatecount-attribute-declaration.md).</span><span class="sxs-lookup"><span data-stu-id="4c045-120">For more information, see [ValidateCount Attribute Declaration](./validatecount-attribute-declaration.md).</span></span>

### <a name="validatelength"></a><span data-ttu-id="4c045-121">ValidateLength</span><span class="sxs-lookup"><span data-stu-id="4c045-121">ValidateLength</span></span>

<span data-ttu-id="4c045-122">Egy parancsmag paraméterargumentum karakterek minimális és maximális számát adja meg.</span><span class="sxs-lookup"><span data-stu-id="4c045-122">Specifies a minimum and maximum number of characters for a cmdlet parameter argument.</span></span>
<span data-ttu-id="4c045-123">További információkért lásd: [ValidateLength típusattribútum-deklaráció](./validatelength-attribute-declaration.md).</span><span class="sxs-lookup"><span data-stu-id="4c045-123">For more information, see [ValidateLength Attribute Declaration](./validatelength-attribute-declaration.md).</span></span>

### <a name="validatepattern"></a><span data-ttu-id="4c045-124">ValidatePattern</span><span class="sxs-lookup"><span data-stu-id="4c045-124">ValidatePattern</span></span>

<span data-ttu-id="4c045-125">Itt adhatja meg, hogy a parancsmag paraméterargumentum meg kell egyeznie a reguláris kifejezési minta.</span><span class="sxs-lookup"><span data-stu-id="4c045-125">Specifies a regular expression pattern that the cmdlet parameter argument must match.</span></span>
<span data-ttu-id="4c045-126">További információkért lásd: [ValidatePattern típusattribútum-deklaráció](./validatepattern-attribute-declaration.md).</span><span class="sxs-lookup"><span data-stu-id="4c045-126">For more information, see [ValidatePattern Attribute Declaration](./validatepattern-attribute-declaration.md).</span></span>

### <a name="validaterange"></a><span data-ttu-id="4c045-127">ValidateRange</span><span class="sxs-lookup"><span data-stu-id="4c045-127">ValidateRange</span></span>

<span data-ttu-id="4c045-128">Adja meg a minimális és maximális értékeket a parancsmag paraméter argumentumként.</span><span class="sxs-lookup"><span data-stu-id="4c045-128">Specifies the minimum and maximum values for a cmdlet parameter argument.</span></span>
<span data-ttu-id="4c045-129">További információkért lásd: [ValidateRange típusattribútum-deklaráció](./validaterange-attribute-declaration.md).</span><span class="sxs-lookup"><span data-stu-id="4c045-129">For more information, see [ValidateRange Attribute Declaration](./validaterange-attribute-declaration.md).</span></span>

### <a name="validateset"></a><span data-ttu-id="4c045-130">ValidateSet</span><span class="sxs-lookup"><span data-stu-id="4c045-130">ValidateSet</span></span>

<span data-ttu-id="4c045-131">A parancsmag paraméterargumentum az érvényes értékek egy halmazát határozza meg.</span><span class="sxs-lookup"><span data-stu-id="4c045-131">Specifies a set of valid values for the cmdlet parameter argument.</span></span>
<span data-ttu-id="4c045-132">További információkért lásd: [ValidateSet típusattribútum-deklaráció](./validateset-attribute-declaration.md).</span><span class="sxs-lookup"><span data-stu-id="4c045-132">For more information, see [ValidateSet Attribute Declaration](./validateset-attribute-declaration.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="4c045-133">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="4c045-133">See Also</span></span>

[<span data-ttu-id="4c045-134">Windows PowerShell SDK</span><span class="sxs-lookup"><span data-stu-id="4c045-134">Windows PowerShell SDK</span></span>](../windows-powershell-reference.md)
