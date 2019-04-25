---
title: SelectionCondition elemet a vezérlők (formátum) konfiguráció EntrySelectedBy |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f23ef405-0f1e-4607-b3f4-4017b7ead106
caps.latest.revision: 7
ms.openlocfilehash: a5098da55d0a63272a121b973cb05e26dc47e3e1
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62075766"
---
# <a name="selectioncondition-element-for-entryselectedby-for-controls-for-configuration-format"></a><span data-ttu-id="f2d53-102">A Konfiguráció Vezérlők eleméhez tartozó EntrySelectedBy SelectionCondition eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="f2d53-102">SelectionCondition Element for EntrySelectedBy for Controls for Configuration (Format)</span></span>

<span data-ttu-id="f2d53-103">Határozza meg egy feltételt, amely használt gyakori ellenőrzési definíció léteznie kell.</span><span class="sxs-lookup"><span data-stu-id="f2d53-103">Defines a condition that must exist for a common control definition to be used.</span></span> <span data-ttu-id="f2d53-104">Ez az elem szolgál egy közös vezérlőelem a formázási fájlban az összes nézetek által használható meghatározásakor.</span><span class="sxs-lookup"><span data-stu-id="f2d53-104">This element is used when defining a common control that can be used by all the views in the formatting file.</span></span>

<span data-ttu-id="f2d53-105">Konfigurációs elem (formátum) vezérlők elem Configuration (formátum) vezérlőelem elem vezérlők Configuration (formátum) CustomEntries elemhez tartozó CustomControl vezérlők, a vezérlő konfigurációja (formátum) CustomControl elemhez Konfiguráció (formátum) CustomEntry elemet a vezérlők, a vezérlők, a Configuration (formátum) SelectionCondition elem esetében a CustomEntry EntrySelectedBy a CustomEntry Configuration (formátum) EntrySelectedBy elemhez CustomControl Konfiguráció (formátum)</span><span class="sxs-lookup"><span data-stu-id="f2d53-105">Configuration Element (Format) Controls Element of Configuration (Format) Control Element for Controls for Configuration (Format) CustomControl Element for Control for Configuration (Format) CustomEntries Element for CustomControl for Controls for Configuration (Format) CustomEntry Element for CustomControl for Controls for Configuration (Format) EntrySelectedBy Element for CustomEntry for Controls for Configuration (Format) SelectionCondition Element for EntrySelectedBy for CustomEntry for Configuration (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="f2d53-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="f2d53-106">Syntax</span></span>

```xml
<SelectionCondition>
  <TypeName>Nameof.NetType</TypeName>
  <SelectionSetName>NameofSelectionSet</SelectionSetName>
  <PropertyName>.NetTypeProperty</PropertyName>
  <ScriptBlock>ScriptToEvaluate</ScriptBlock>
</SelectionCondition>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="f2d53-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="f2d53-107">Attributes and Elements</span></span>

<span data-ttu-id="f2d53-108">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `SelectionCondition` elemet.</span><span class="sxs-lookup"><span data-stu-id="f2d53-108">The following sections describe attributes, child elements, and the parent element of the `SelectionCondition` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="f2d53-109">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="f2d53-109">Attributes</span></span>

<span data-ttu-id="f2d53-110">Nincs.</span><span class="sxs-lookup"><span data-stu-id="f2d53-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="f2d53-111">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="f2d53-111">Child Elements</span></span>

|<span data-ttu-id="f2d53-112">Elem</span><span class="sxs-lookup"><span data-stu-id="f2d53-112">Element</span></span>|<span data-ttu-id="f2d53-113">Leírás</span><span class="sxs-lookup"><span data-stu-id="f2d53-113">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="f2d53-114">Konfiguráció (formátum) vezérlők SelectionCondition PropertyName elem.</span><span class="sxs-lookup"><span data-stu-id="f2d53-114">PropertyName Element for SelectionCondition for Controls for Configuration (Format)</span></span>](./propertyname-element-for-selectioncondition-for-controls-for-configuration-format.md)|<span data-ttu-id="f2d53-115">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="f2d53-115">Optional element.</span></span><br /><br /> <span data-ttu-id="f2d53-116">Megadja a .NET-tulajdonság, amely elindítja a feltétel.</span><span class="sxs-lookup"><span data-stu-id="f2d53-116">Specifies a .NET property that triggers the condition.</span></span>|
|[<span data-ttu-id="f2d53-117">Konfiguráció (formátum) vezérlők SelectionCondition ScriptBlock eleme</span><span class="sxs-lookup"><span data-stu-id="f2d53-117">ScriptBlock Element for SelectionCondition for Controls for Configuration (Format)</span></span>](./scriptblock-element-for-selectioncondition-for-controls-for-configuration-format.md)|<span data-ttu-id="f2d53-118">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="f2d53-118">Optional element.</span></span><br /><br /> <span data-ttu-id="f2d53-119">Megadja a parancsprogramot, amely elindítja a feltétel.</span><span class="sxs-lookup"><span data-stu-id="f2d53-119">Specifies the script that triggers the condition.</span></span>|
|[<span data-ttu-id="f2d53-120">Konfiguráció (formátum) vezérlők SelectionCondition SelectionSetName elem.</span><span class="sxs-lookup"><span data-stu-id="f2d53-120">SelectionSetName Element for SelectionCondition for Controls for Configuration (Format)</span></span>](./selectionsetname-element-for-selectioncondition-for-controls-for-configuration-format.md)|<span data-ttu-id="f2d53-121">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="f2d53-121">Optional element.</span></span><br /><br /> <span data-ttu-id="f2d53-122">Megadja a .NET-típusok, amely elindítja a feltételt.</span><span class="sxs-lookup"><span data-stu-id="f2d53-122">Specifies the set of .NET types that triggers the condition.</span></span>|
|[<span data-ttu-id="f2d53-123">Konfiguráció (formátum) vezérlők SelectionCondition TypeName elem.</span><span class="sxs-lookup"><span data-stu-id="f2d53-123">TypeName Element for SelectionCondition for Controls for Configuration (Format)</span></span>](./typename-element-for-selectioncondition-for-controls-for-configuration-format.md)|<span data-ttu-id="f2d53-124">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="f2d53-124">Optional element.</span></span><br /><br /> <span data-ttu-id="f2d53-125">A .NET típusát, amely elindítja a feltételt határozza meg.</span><span class="sxs-lookup"><span data-stu-id="f2d53-125">Specifies a .NET type that triggers the condition.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="f2d53-126">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="f2d53-126">Parent Elements</span></span>

|<span data-ttu-id="f2d53-127">Elem</span><span class="sxs-lookup"><span data-stu-id="f2d53-127">Element</span></span>|<span data-ttu-id="f2d53-128">Leírás</span><span class="sxs-lookup"><span data-stu-id="f2d53-128">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="f2d53-129">Konfiguráció (formátum) vezérlők CustomEntry EntrySelectedBy elem.</span><span class="sxs-lookup"><span data-stu-id="f2d53-129">EntrySelectedBy Element for CustomEntry for Controls for Configuration (Format)</span></span>](./entryselectedby-element-for-customentry-for-controls-for-configuration-format.md)|<span data-ttu-id="f2d53-130">A .NET-típusokat, amelyek a közös ellenőrzési definícióját a bejegyzés határozza meg.</span><span class="sxs-lookup"><span data-stu-id="f2d53-130">Defines the .NET types that use this entry of the common control definition.</span></span>|

## <a name="remarks"></a><span data-ttu-id="f2d53-131">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="f2d53-131">Remarks</span></span>

<span data-ttu-id="f2d53-132">Kiválasztási feltétel meghatározásakor a következő irányelveket kell követni:</span><span class="sxs-lookup"><span data-stu-id="f2d53-132">The following guidelines must be followed when defining a selection condition:</span></span>

- <span data-ttu-id="f2d53-133">A kiválasztási feltételnek legalább egy tulajdonság nevét, vagy parancsprogram-blokkot kell megadnia, de nem adható meg egyszerre.</span><span class="sxs-lookup"><span data-stu-id="f2d53-133">The selection condition must specify a least one property name or a script block, but cannot specify both.</span></span>

- <span data-ttu-id="f2d53-134">A kiválasztási feltétel adhat meg minden olyan .NET-típusok száma vagy a kiválasztási állítja be, de nem adható meg egyszerre.</span><span class="sxs-lookup"><span data-stu-id="f2d53-134">The selection condition can specify any number of .NET types or selection sets, but cannot specify both.</span></span>

<span data-ttu-id="f2d53-135">Hogyan használható a kiválasztási feltételek kapcsolatos további információkért lásd: [feltételeinek meghatározása mikor jelenik meg adat](./defining-conditions-for-displaying-data.md).</span><span class="sxs-lookup"><span data-stu-id="f2d53-135">For more information about how selection conditions can be used, see [Defining Conditions for when Data is Displayed](./defining-conditions-for-displaying-data.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="f2d53-136">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="f2d53-136">See Also</span></span>

[<span data-ttu-id="f2d53-137">Konfiguráció (formátum) vezérlők SelectionCondition PropertyName elem.</span><span class="sxs-lookup"><span data-stu-id="f2d53-137">PropertyName Element for SelectionCondition for Controls for Configuration (Format)</span></span>](./propertyname-element-for-selectioncondition-for-controls-for-configuration-format.md)

[<span data-ttu-id="f2d53-138">Konfiguráció (formátum) vezérlők SelectionCondition ScriptBlock eleme</span><span class="sxs-lookup"><span data-stu-id="f2d53-138">ScriptBlock Element for SelectionCondition for Controls for Configuration (Format)</span></span>](./scriptblock-element-for-selectioncondition-for-controls-for-configuration-format.md)

[<span data-ttu-id="f2d53-139">Konfiguráció (formátum) vezérlők SelectionCondition SelectionSetName elem.</span><span class="sxs-lookup"><span data-stu-id="f2d53-139">SelectionSetName Element for SelectionCondition for Controls for Configuration (Format)</span></span>](./selectionsetname-element-for-selectioncondition-for-controls-for-configuration-format.md)

[<span data-ttu-id="f2d53-140">Konfiguráció (formátum) vezérlők SelectionCondition TypeName elem.</span><span class="sxs-lookup"><span data-stu-id="f2d53-140">TypeName Element for SelectionCondition for Controls for Configuration (Format)</span></span>](./typename-element-for-selectioncondition-for-controls-for-configuration-format.md)

[<span data-ttu-id="f2d53-141">Konfiguráció (formátum) vezérlők CustomEntry EntrySelectedBy elem.</span><span class="sxs-lookup"><span data-stu-id="f2d53-141">EntrySelectedBy Element for CustomEntry for Controls for Configuration (Format)</span></span>](./entryselectedby-element-for-customentry-for-controls-for-configuration-format.md)

[<span data-ttu-id="f2d53-142">Egy Windows PowerShell formázás és a fájl típusai</span><span class="sxs-lookup"><span data-stu-id="f2d53-142">Writing a Windows PowerShell Formatting and Types File</span></span>](./writing-a-powershell-formatting-file.md)
