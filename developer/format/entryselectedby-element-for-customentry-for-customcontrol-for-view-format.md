---
title: A nézet (formátum) CustomControl CustomEntry EntrySelectedBy eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 7828b45b-eabf-4432-b127-131b4ef0c800
caps.latest.revision: 8
ms.openlocfilehash: e7176f9f6ef67116ea7c07a46797fb0ba84f915d
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62066277"
---
# <a name="entryselectedby-element-for-customentry-for-customcontrol-for-view-format"></a><span data-ttu-id="cd9e6-102">A Nézet CustomControl eleméhez tartozó CustomEntry EntrySelectedBy eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="cd9e6-102">EntrySelectedBy Element for CustomEntry for CustomControl for View (Format)</span></span>

<span data-ttu-id="cd9e6-103">A .NET-típusokat, amelyek egyéni tételhez vagy a feltétellel, hogy léteznie kell használni a bejegyzés határozza meg.</span><span class="sxs-lookup"><span data-stu-id="cd9e6-103">Defines the .NET types that use this custom entry or the condition that must exist for this entry to be used.</span></span>

<span data-ttu-id="cd9e6-104">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézet elem (formátum) CustomControl elem (formátum) CustomEntries eleme CustomControl számára a nézet (formátum) EntrySelectedBy CustomEntries megtekintése (formátum) CustomEntry elemhez Elem a CustomEntry nézet (formátum)</span><span class="sxs-lookup"><span data-stu-id="cd9e6-104">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) CustomControl Element (Format) CustomEntries Element for CustomControl for View (Format) CustomEntry Element for CustomEntries for View (Format) EntrySelectedBy Element for CustomEntry for View (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="cd9e6-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="cd9e6-105">Syntax</span></span>

```xml
<EntrySelectedBy>
  <TypeName>Nameof.NetType</TypeName>
  <SelectionSetName>NameofSelectionSet</SelectionSetName>
  <SelectionCondition>...</SelectionCondition>
</EntrySelectedBy>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="cd9e6-106">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="cd9e6-106">Attributes and Elements</span></span>

<span data-ttu-id="cd9e6-107">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `EntrySelectedBy` elemet.</span><span class="sxs-lookup"><span data-stu-id="cd9e6-107">The following sections describe attributes, child elements, and the parent element of the `EntrySelectedBy` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="cd9e6-108">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="cd9e6-108">Attributes</span></span>

<span data-ttu-id="cd9e6-109">Nincs.</span><span class="sxs-lookup"><span data-stu-id="cd9e6-109">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="cd9e6-110">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="cd9e6-110">Child Elements</span></span>

|<span data-ttu-id="cd9e6-111">Elem</span><span class="sxs-lookup"><span data-stu-id="cd9e6-111">Element</span></span>|<span data-ttu-id="cd9e6-112">Leírás</span><span class="sxs-lookup"><span data-stu-id="cd9e6-112">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="cd9e6-113">A CustomEntry (formátum) EntrySelectedBy SelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="cd9e6-113">SelectionCondition Element for EntrySelectedBy for CustomEntry (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-customcontrol-format.md)|<span data-ttu-id="cd9e6-114">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="cd9e6-114">Optional element.</span></span><br /><br /> <span data-ttu-id="cd9e6-115">Határozza meg azt a feltételt, amelyet a definíció használandó léteznie kell.</span><span class="sxs-lookup"><span data-stu-id="cd9e6-115">Defines the condition that must exist for this definition to be used.</span></span>|
|[<span data-ttu-id="cd9e6-116">A CustomEntry (formátum) EntrySelectedBy SelectionSetName elem.</span><span class="sxs-lookup"><span data-stu-id="cd9e6-116">SelectionSetName Element for EntrySelectedBy for CustomEntry (Format)</span></span>](./selectionsetname-element-for-entryselectedby-for-customcontrol-for-view-format.md)|<span data-ttu-id="cd9e6-117">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="cd9e6-117">Optional element.</span></span><br /><br /> <span data-ttu-id="cd9e6-118">Ez a definíció, a vezérlő nézet használó .NET-típusok egy halmazát határozza meg.</span><span class="sxs-lookup"><span data-stu-id="cd9e6-118">Specifies a set of .NET types that use this definition of the control view.</span></span>|
|[<span data-ttu-id="cd9e6-119">EntrySelectedBy CustomEntry (formátum) a TypeName elem.</span><span class="sxs-lookup"><span data-stu-id="cd9e6-119">TypeName Element for EntrySelectedBy for CustomEntry (Format)</span></span>](./typename-element-for-selectioncondition-for-customcontrol-for-view-format.md)|<span data-ttu-id="cd9e6-120">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="cd9e6-120">Optional element.</span></span><br /><br /> <span data-ttu-id="cd9e6-121">Ez a definíció, a vezérlő nézet használó .NET típust határozzon meg.</span><span class="sxs-lookup"><span data-stu-id="cd9e6-121">Specifies a .NET type that uses this definition of the control view.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="cd9e6-122">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="cd9e6-122">Parent Elements</span></span>

|<span data-ttu-id="cd9e6-123">Elem</span><span class="sxs-lookup"><span data-stu-id="cd9e6-123">Element</span></span>|<span data-ttu-id="cd9e6-124">Leírás</span><span class="sxs-lookup"><span data-stu-id="cd9e6-124">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="cd9e6-125">A nézet (formátum) CustomEntries CustomEntry elem</span><span class="sxs-lookup"><span data-stu-id="cd9e6-125">CustomEntry Element for CustomEntries for View (Format)</span></span>](./customentry-element-for-customentries-for-customcontrol-for-view-format.md)|<span data-ttu-id="cd9e6-126">A .NET-objektumokká által használt funkciók határozza meg.</span><span class="sxs-lookup"><span data-stu-id="cd9e6-126">Defines the controls used by specific .NET objects.</span></span>|

## <a name="remarks"></a><span data-ttu-id="cd9e6-127">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="cd9e6-127">Remarks</span></span>

<span data-ttu-id="cd9e6-128">Meg kell adnia legalább egy típus, kijelölés set vagy bejegyzés kiválasztási feltételnek.</span><span class="sxs-lookup"><span data-stu-id="cd9e6-128">You must specify at least one type, selection set, or selection condition for an entry.</span></span> <span data-ttu-id="cd9e6-129">Nincs nem használható gyermekelemek számának maximális korlátot.</span><span class="sxs-lookup"><span data-stu-id="cd9e6-129">There is no maximum limit to the number of child elements that you can use.</span></span>

<span data-ttu-id="cd9e6-130">Kiválasztási feltételek segítségével határozhatók meg egy feltételt, amely léteznie kell használni a bejegyzést, például ha egy objektum rendelkezik-e egy adott tulajdonságra vagy ha egy adott tulajdonság értéke, vagy a parancsfájl kiértékelése `true`.</span><span class="sxs-lookup"><span data-stu-id="cd9e6-130">Selection conditions are used to define a condition that must exist for the entry to be used, such as when an object has a specific property or when a specific property value or script evaluates to `true`.</span></span> <span data-ttu-id="cd9e6-131">További információ a kiválasztási feltételek: [definiáló vonatkozó feltételeket, amikor egy nézet bejegyzés vagy az elem](./defining-conditions-for-displaying-data.md).</span><span class="sxs-lookup"><span data-stu-id="cd9e6-131">For more information about selection conditions, see [Defining Conditions for when a View Entry or Item is Used](./defining-conditions-for-displaying-data.md).</span></span>

<span data-ttu-id="cd9e6-132">Egyéni vezérlő nézet az összetevőivel kapcsolatos további információkért lásd: [egyéni vezérlő nézetében](./creating-custom-controls.md).</span><span class="sxs-lookup"><span data-stu-id="cd9e6-132">For more information about the components of a custom control view, see [Custom Control View](./creating-custom-controls.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="cd9e6-133">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="cd9e6-133">See Also</span></span>

[<span data-ttu-id="cd9e6-134">A CustomEntry (formátum) EntrySelectedBy SelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="cd9e6-134">SelectionCondition Element for EntrySelectedBy for CustomEntry (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-customcontrol-format.md)

[<span data-ttu-id="cd9e6-135">A CustomEntry (formátum) EntrySelectedBy SelectionSetName elem.</span><span class="sxs-lookup"><span data-stu-id="cd9e6-135">SelectionSetName Element for EntrySelectedBy for CustomEntry (Format)</span></span>](./selectionsetname-element-for-entryselectedby-for-customcontrol-for-view-format.md)

[<span data-ttu-id="cd9e6-136">EntrySelectedBy CustomEntry (formátum) a TypeName elem.</span><span class="sxs-lookup"><span data-stu-id="cd9e6-136">TypeName Element for EntrySelectedBy for CustomEntry (Format)</span></span>](./typename-element-for-selectioncondition-for-customcontrol-for-view-format.md)

[<span data-ttu-id="cd9e6-137">A nézet (formátum) CustomEntries CustomEntry elem</span><span class="sxs-lookup"><span data-stu-id="cd9e6-137">CustomEntry Element for CustomEntries for View (Format)</span></span>](./customentry-element-for-customentries-for-customcontrol-for-view-format.md)

[<span data-ttu-id="cd9e6-138">Egyéni vezérlő nézetében.</span><span class="sxs-lookup"><span data-stu-id="cd9e6-138">Custom Control View</span></span>](./creating-custom-controls.md)

[<span data-ttu-id="cd9e6-139">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="cd9e6-139">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
