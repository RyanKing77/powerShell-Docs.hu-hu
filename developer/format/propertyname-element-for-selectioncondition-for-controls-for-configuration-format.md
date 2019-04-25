---
title: PropertyName elemet a vezérlők (formátum) konfiguráció SelectionCondition |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ec048408-e1c6-41ef-b39b-72f4c2dcf2ac
caps.latest.revision: 6
ms.openlocfilehash: b4b2440fdb7171d09fdc16ac7cc4f25ed1a4bb78
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62064727"
---
# <a name="propertyname-element-for-selectioncondition-for-controls-for-configuration-format"></a><span data-ttu-id="cd822-102">A Konfiguráció Vezérlők eleméhez tartozó SelectionCondition PropertyName eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="cd822-102">PropertyName Element for SelectionCondition for Controls for Configuration (Format)</span></span>

<span data-ttu-id="cd822-103">Megadja a .NET-tulajdonság, amely elindítja a feltételt.</span><span class="sxs-lookup"><span data-stu-id="cd822-103">Specifies the .NET property that triggers the condition.</span></span> <span data-ttu-id="cd822-104">Ha ez a tulajdonság jelen-e, vagy ha való kiértékelése által `true`, a feltétel nem teljesül, és a bejegyzés szolgál.</span><span class="sxs-lookup"><span data-stu-id="cd822-104">When this property is present or when it evaluates to `true`, the condition is met, and the entry is used.</span></span> <span data-ttu-id="cd822-105">Ez az elem szolgál egy közös vezérlőelem a formázási fájlban az összes nézetek által használható meghatározásakor.</span><span class="sxs-lookup"><span data-stu-id="cd822-105">This element is used when defining a common control that can be used by all the views in the formatting file.</span></span>

<span data-ttu-id="cd822-106">Konfigurációs elem (formátum) vezérlők elem Configuration (formátum) vezérlőelem elem vezérlők, a vezérlő konfigurációs (formátum) CustomEntries elemhez tartozó CustomControl Configuration (a Configuration (formátum) CustomControl elem Formátum) CustomEntry elemet a vezérlők, a Configuration (formátum) EntrySelectedBy elem CustomEntry vezérlők, a Configuration (a CustomEntry EntrySelectedBy a Configuration (formátum) SelectionCondition elemhez tartozó CustomControl SelectionCondition EntrySelectedBy ListEntry (formátum) esetében a formátum) PropertyName elem.</span><span class="sxs-lookup"><span data-stu-id="cd822-106">Configuration Element (Format) Controls Element of Configuration (Format) Control Element for Controls for Configuration (Format) CustomControl Element for Control for Configuration (Format) CustomEntries Element for CustomControl for Configuration (Format) CustomEntry Element for CustomControl for Controls for Configuration (Format) EntrySelectedBy Element for CustomEntry for Controls for Configuration (Format) SelectionCondition Element for EntrySelectedBy for CustomEntry for Configuration (Format) PropertyName Element for SelectionCondition for EntrySelectedBy for ListEntry (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="cd822-107">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="cd822-107">Syntax</span></span>

```xml
<PropertyName>.NetTypeProperty</PropertyName>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="cd822-108">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="cd822-108">Attributes and Elements</span></span>

<span data-ttu-id="cd822-109">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `PropertyName` elemet.</span><span class="sxs-lookup"><span data-stu-id="cd822-109">The following sections describe attributes, child elements, and the parent element of the `PropertyName` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="cd822-110">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="cd822-110">Attributes</span></span>

<span data-ttu-id="cd822-111">Nincs.</span><span class="sxs-lookup"><span data-stu-id="cd822-111">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="cd822-112">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="cd822-112">Child Elements</span></span>

<span data-ttu-id="cd822-113">Nincs.</span><span class="sxs-lookup"><span data-stu-id="cd822-113">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="cd822-114">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="cd822-114">Parent Elements</span></span>

|<span data-ttu-id="cd822-115">Elem</span><span class="sxs-lookup"><span data-stu-id="cd822-115">Element</span></span>|<span data-ttu-id="cd822-116">Leírás</span><span class="sxs-lookup"><span data-stu-id="cd822-116">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="cd822-117">Konfiguráció (formátum) vezérlők EntrySelectedBy SelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="cd822-117">SelectionCondition Element for EntrySelectedBy for Controls for Configuration (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-controls-for-configuration-format.md)|<span data-ttu-id="cd822-118">Határozza meg egy feltételt, amely használt gyakori ellenőrzési definíció léteznie kell.</span><span class="sxs-lookup"><span data-stu-id="cd822-118">Defines a condition that must exist for a common control definition to be used.</span></span>|

## <a name="text-value"></a><span data-ttu-id="cd822-119">A szöveges érték</span><span class="sxs-lookup"><span data-stu-id="cd822-119">Text Value</span></span>

<span data-ttu-id="cd822-120">Adja meg a .NET-tulajdonság neve.</span><span class="sxs-lookup"><span data-stu-id="cd822-120">Specify the .NET property name.</span></span>

## <a name="remarks"></a><span data-ttu-id="cd822-121">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="cd822-121">Remarks</span></span>

<span data-ttu-id="cd822-122">A kiválasztási feltétel meg kell adnia legalább egy tulajdonság nevét, vagy egy parancsfájlt, de nem adható meg egyszerre.</span><span class="sxs-lookup"><span data-stu-id="cd822-122">The selection condition must specify a least one property name or a script, but cannot specify both.</span></span> <span data-ttu-id="cd822-123">Hogyan használható a kiválasztási feltételek kapcsolatos további információkért lásd: [feltételek meghatározása az adatok megjelenítése](./defining-conditions-for-displaying-data.md).</span><span class="sxs-lookup"><span data-stu-id="cd822-123">For more information about how selection conditions can be used, see [Defining Conditions for Displaying Data](./defining-conditions-for-displaying-data.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="cd822-124">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="cd822-124">See Also</span></span>

[<span data-ttu-id="cd822-125">Konfiguráció (formátum) vezérlők EntrySelectedBy SelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="cd822-125">SelectionCondition Element for EntrySelectedBy for Controls for Configuration (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-controls-for-configuration-format.md)

[<span data-ttu-id="cd822-126">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="cd822-126">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
