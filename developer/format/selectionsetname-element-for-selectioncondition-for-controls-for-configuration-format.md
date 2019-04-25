---
title: SelectionSetName elemet a vezérlők (formátum) konfiguráció SelectionCondition |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 7dcaeadb-4e79-47a0-96e2-8952af26abbe
caps.latest.revision: 7
ms.openlocfilehash: 5db35a8094ea2bb966c8d6a96802c72f64c05c17
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62064022"
---
# <a name="selectionsetname-element-for-selectioncondition-for-controls-for-configuration-format"></a><span data-ttu-id="7a060-102">A Konfiguráció Vezérlők eleméhez tartozó SelectionCondition SelectionSetName eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="7a060-102">SelectionSetName Element for SelectionCondition for Controls for Configuration (Format)</span></span>

<span data-ttu-id="7a060-103">Megadja azt a feltételt .NET típusú.</span><span class="sxs-lookup"><span data-stu-id="7a060-103">Specifies the set of .NET types that trigger the condition.</span></span> <span data-ttu-id="7a060-104">Az ebben a készletben típusok találhatók, ha a feltétel nem teljesül, és az objektum megjelenik a vezérlőelem használatával.</span><span class="sxs-lookup"><span data-stu-id="7a060-104">When any of the types in this set are present, the condition is met, and the object is displayed by using this control.</span></span> <span data-ttu-id="7a060-105">Ez az elem szolgál egy közös vezérlőelem a formázási fájlban az összes nézetek által használható meghatározásakor.</span><span class="sxs-lookup"><span data-stu-id="7a060-105">This element is used when defining a common control that can be used by all the views in the formatting file.</span></span>

<span data-ttu-id="7a060-106">Konfigurációs elem (formátum) vezérlők elem Configuration (formátum) vezérlőelem elem vezérlők Configuration (formátum) CustomEntries elemhez tartozó CustomControl vezérlők, a vezérlő konfigurációja (formátum) CustomControl elemhez Konfiguráció (formátum) CustomEntry elemet a vezérlők, a Configuration (formátum) EntrySelectedBy elem CustomEntry vezérlők, a vezérlők, a EntrySelectedBy Configuration (formátum) SelectionCondition elemhez tartozó CustomControl Konfiguráció (formátum) SelectionSetName eleme SelectionCondition vezérlők konfiguráció (formátum)</span><span class="sxs-lookup"><span data-stu-id="7a060-106">Configuration Element (Format) Controls Element of Configuration (Format) Control Element for Controls for Configuration (Format) CustomControl Element for Control for Configuration (Format) CustomEntries Element for CustomControl for Controls for Configuration (Format) CustomEntry Element for CustomControl for Controls for Configuration (Format) EntrySelectedBy Element for CustomEntry for Controls for Configuration (Format) SelectionCondition Element for EntrySelectedBy for Controls for Configuration (Format) SelectionSetName Element for SelectionCondition for Controls for Configuration (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="7a060-107">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="7a060-107">Syntax</span></span>

```xml
<SelectionSetName>NameofSelectionSet</SelectionSetName>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="7a060-108">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="7a060-108">Attributes and Elements</span></span>

<span data-ttu-id="7a060-109">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `SelectionSetName` elemet.</span><span class="sxs-lookup"><span data-stu-id="7a060-109">The following sections describe attributes, child elements, and the parent element of the `SelectionSetName` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="7a060-110">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="7a060-110">Attributes</span></span>

<span data-ttu-id="7a060-111">Nincs.</span><span class="sxs-lookup"><span data-stu-id="7a060-111">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="7a060-112">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="7a060-112">Child Elements</span></span>

<span data-ttu-id="7a060-113">Nincs.</span><span class="sxs-lookup"><span data-stu-id="7a060-113">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="7a060-114">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="7a060-114">Parent Elements</span></span>

|<span data-ttu-id="7a060-115">Elem</span><span class="sxs-lookup"><span data-stu-id="7a060-115">Element</span></span>|<span data-ttu-id="7a060-116">Leírás</span><span class="sxs-lookup"><span data-stu-id="7a060-116">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="7a060-117">Konfiguráció (formátum) vezérlők EntrySelectedBy SelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="7a060-117">SelectionCondition Element for EntrySelectedBy for Controls for Configuration (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-controls-for-configuration-format.md)|<span data-ttu-id="7a060-118">Határozza meg egy feltételt, amely a vezérlőelem definíciójában használt léteznie kell.</span><span class="sxs-lookup"><span data-stu-id="7a060-118">Defines a condition that must exist for the control definition to be used.</span></span>|

## <a name="text-value"></a><span data-ttu-id="7a060-119">A szöveges érték</span><span class="sxs-lookup"><span data-stu-id="7a060-119">Text Value</span></span>

<span data-ttu-id="7a060-120">Adja meg a kijelölt csoport nevét.</span><span class="sxs-lookup"><span data-stu-id="7a060-120">Specify the name of the selection set.</span></span>

## <a name="remarks"></a><span data-ttu-id="7a060-121">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="7a060-121">Remarks</span></span>

<span data-ttu-id="7a060-122">Kijelölés sets csoportjai közös nézeten, amely meghatározza a formázási fájl által használható .NET-objektumokat.</span><span class="sxs-lookup"><span data-stu-id="7a060-122">Selection sets are common groups of .NET objects that can be used by any view that the formatting file defines.</span></span> <span data-ttu-id="7a060-123">Létrehozásával és a kijelölt csoportok hivatkozó kapcsolatos további információkért lásd: [meghatározása beállítja az objektumok](./defining-selection-sets.md).</span><span class="sxs-lookup"><span data-stu-id="7a060-123">For more information about creating and referencing selection sets, see [Defining Sets of Objects](./defining-selection-sets.md).</span></span>

<span data-ttu-id="7a060-124">A kiválasztási feltétel egy kijelölés set vagy a .NET-típus is megadhat, de nem adható meg egyszerre.</span><span class="sxs-lookup"><span data-stu-id="7a060-124">The selection condition can specify a selection set or .NET type, but cannot specify both.</span></span> <span data-ttu-id="7a060-125">Kiválasztási feltételek használatával kapcsolatos további információkért lásd: [feltételek meghatározása az adatok megjelenítése](./defining-conditions-for-displaying-data.md).</span><span class="sxs-lookup"><span data-stu-id="7a060-125">For more information about how to use selection conditions, see [Defining Conditions for Displaying Data](./defining-conditions-for-displaying-data.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="7a060-126">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="7a060-126">See Also</span></span>

[<span data-ttu-id="7a060-127">Konfiguráció (formátum) vezérlők EntrySelectedBy SelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="7a060-127">SelectionCondition Element for EntrySelectedBy for Controls for Configuration (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-controls-for-configuration-format.md)

[<span data-ttu-id="7a060-128">Mikor jelenik meg adat feltételeinek meghatározása</span><span class="sxs-lookup"><span data-stu-id="7a060-128">Defining Conditions for When Data Is Displayed</span></span>](./defining-conditions-for-displaying-data.md)

[<span data-ttu-id="7a060-129">Kijelölt csoportok meghatározása</span><span class="sxs-lookup"><span data-stu-id="7a060-129">Defining Selection Sets</span></span>](./defining-selection-sets.md)

[<span data-ttu-id="7a060-130">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="7a060-130">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
