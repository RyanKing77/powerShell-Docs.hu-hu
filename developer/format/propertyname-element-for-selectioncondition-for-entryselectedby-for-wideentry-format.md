---
title: SelectionCondition EntrySelectedBy WideEntry (formátum) esetében a PropertyName eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 340abb12-6df1-42f4-bdae-b0509c90952c
caps.latest.revision: 11
ms.openlocfilehash: 196877b97db9ed0592e357486c1318dc1e7efd31
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62064679"
---
# <a name="propertyname-element-for-selectioncondition-for-entryselectedby-for-wideentry-format"></a><span data-ttu-id="e30a5-102">Az WideEntry EntrySelectedBy eleméhez tartozó SelectionCondition PropertyName eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="e30a5-102">PropertyName Element for SelectionCondition for EntrySelectedBy for WideEntry (Format)</span></span>

<span data-ttu-id="e30a5-103">Megadja a .NET-tulajdonság, amely elindítja a feltételt.</span><span class="sxs-lookup"><span data-stu-id="e30a5-103">Specifies the .NET property that triggers the condition.</span></span> <span data-ttu-id="e30a5-104">Ha ez a tulajdonság jelen-e, vagy ha való kiértékelése által `true`, a feltétel nem teljesül, és a definíció szolgál.</span><span class="sxs-lookup"><span data-stu-id="e30a5-104">When this property is present or when it evaluates to `true`, the condition is met, and the definition is used.</span></span>

<span data-ttu-id="e30a5-105">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézet elem (formátum) WideControl elem (formátum) WideEntries elem (formátum) WideEntry elem (formátum) EntrySelectedBy elem WideEntry (formátum) SelectionCondition elem számára A PropertyName elem WideEntry (formátum) a SelectionCondition EntrySelectedBy WideEntry (formátum) esetében a EntrySelectedBy</span><span class="sxs-lookup"><span data-stu-id="e30a5-105">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) WideControl Element (Format) WideEntries Element (Format) WideEntry Element (Format) EntrySelectedBy Element for WideEntry (Format) SelectionCondition Element for EntrySelectedBy for WideEntry (Format) PropertyName Element for SelectionCondition for EntrySelectedBy for WideEntry (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="e30a5-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="e30a5-106">Syntax</span></span>

```xml
<PropertyName>.NetTypeProperty</PropertyName>
```

```csharp

```

## <a name="attributes-and-elements"></a><span data-ttu-id="e30a5-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="e30a5-107">Attributes and Elements</span></span>

<span data-ttu-id="e30a5-108">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `PropertyName` elemet.</span><span class="sxs-lookup"><span data-stu-id="e30a5-108">The following sections describe attributes, child elements, and the parent element of the `PropertyName` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="e30a5-109">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="e30a5-109">Attributes</span></span>

<span data-ttu-id="e30a5-110">Nincs.</span><span class="sxs-lookup"><span data-stu-id="e30a5-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="e30a5-111">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="e30a5-111">Child Elements</span></span>

<span data-ttu-id="e30a5-112">Nincs.</span><span class="sxs-lookup"><span data-stu-id="e30a5-112">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="e30a5-113">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="e30a5-113">Parent Elements</span></span>

|<span data-ttu-id="e30a5-114">Elem</span><span class="sxs-lookup"><span data-stu-id="e30a5-114">Element</span></span>|<span data-ttu-id="e30a5-115">Leírás</span><span class="sxs-lookup"><span data-stu-id="e30a5-115">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="e30a5-116">A WideEntry (formátum) EntrySelectedBy SelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="e30a5-116">SelectionCondition Element for EntrySelectedBy for WideEntry (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-widecontrol-format.md)|<span data-ttu-id="e30a5-117">Határozza meg azt a feltételt, amelyet a definíció használandó léteznie kell.</span><span class="sxs-lookup"><span data-stu-id="e30a5-117">Defines the condition that must exist for this definition to be used.</span></span>|

## <a name="text-value"></a><span data-ttu-id="e30a5-118">A szöveges érték</span><span class="sxs-lookup"><span data-stu-id="e30a5-118">Text Value</span></span>

<span data-ttu-id="e30a5-119">Adja meg a .NET-tulajdonság neve.</span><span class="sxs-lookup"><span data-stu-id="e30a5-119">Specify the .NET property name.</span></span>

## <a name="remarks"></a><span data-ttu-id="e30a5-120">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="e30a5-120">Remarks</span></span>

<span data-ttu-id="e30a5-121">A kiválasztási feltétel meg kell adnia legalább egy tulajdonság neve vagy a parancsfájl kiértékelése, de nem adható meg egyszerre.</span><span class="sxs-lookup"><span data-stu-id="e30a5-121">The selection condition must specify at least one property name or a script to evaluate, but cannot specify both.</span></span> <span data-ttu-id="e30a5-122">Kiválasztási feltételek használatával kapcsolatos további információkért lásd: [feltételeinek meghatározása mikor jelenik meg adat](./defining-conditions-for-displaying-data.md).</span><span class="sxs-lookup"><span data-stu-id="e30a5-122">For more information about how to use selection conditions, see [Defining Conditions for when Data is Displayed](./defining-conditions-for-displaying-data.md).</span></span>

<span data-ttu-id="e30a5-123">Egy széles nézet egyéb összetevőivel kapcsolatos további információkért lásd: [széles nézet](./creating-a-wide-view.md).</span><span class="sxs-lookup"><span data-stu-id="e30a5-123">For more information about other components of a wide view, see [Wide View](./creating-a-wide-view.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="e30a5-124">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="e30a5-124">See Also</span></span>

[<span data-ttu-id="e30a5-125">Egy széles nézet létrehozása</span><span class="sxs-lookup"><span data-stu-id="e30a5-125">Creating a Wide View</span></span>](./creating-a-wide-view.md)

[<span data-ttu-id="e30a5-126">Mikor jelenik meg adat feltételeinek meghatározása</span><span class="sxs-lookup"><span data-stu-id="e30a5-126">Defining Conditions for When Data Is Displayed</span></span>](./defining-conditions-for-displaying-data.md)

[<span data-ttu-id="e30a5-127">SelectionCondition EntrySelectedBy WideEntry (formátum) esetében a scriptblock kulcsszót elem.</span><span class="sxs-lookup"><span data-stu-id="e30a5-127">ScriptBlock Element for SelectionCondition for EntrySelectedBy for WideEntry (Format)</span></span>](./scriptblock-element-for-selectioncondition-for-entryselectedby-for-widecontrol-format.md)

[<span data-ttu-id="e30a5-128">A WideEntry (formátum) EntrySelectedBy SelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="e30a5-128">SelectionCondition Element for EntrySelectedBy for WideEntry (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-widecontrol-format.md)

[<span data-ttu-id="e30a5-129">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="e30a5-129">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
