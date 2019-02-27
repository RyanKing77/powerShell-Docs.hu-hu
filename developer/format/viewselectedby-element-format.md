---
title: ViewSelectedBy elem (formátum) |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: acdeef4d-3554-4f39-a7e6-a684e3848fd7
caps.latest.revision: 19
ms.openlocfilehash: efc1c5d1338889ecd0be7150b7733842ce78979e
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56851841"
---
# <a name="viewselectedby-element-format"></a><span data-ttu-id="14637-102">ViewSelectedBy elem (Formátum)</span><span class="sxs-lookup"><span data-stu-id="14637-102">ViewSelectedBy Element (Format)</span></span>

<span data-ttu-id="14637-103">A .NET-objektumokat a nézet által megjelenített határozza meg.</span><span class="sxs-lookup"><span data-stu-id="14637-103">Defines the .NET objects that are displayed by the view.</span></span> <span data-ttu-id="14637-104">Minden egyes nézet adjon meg legalább egy .NET-objektumokat.</span><span class="sxs-lookup"><span data-stu-id="14637-104">Each view must specify at least one .NET object.</span></span>

<span data-ttu-id="14637-105">ViewDefinitions elem (formátum) nézetben (formátum) elem ViewSelectedBy elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="14637-105">ViewDefinitions Element (Format) View Element (Format) ViewSelectedBy Element (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="14637-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="14637-106">Syntax</span></span>

```xml
<ViewSelectedBy>
  <TypeName>Nameof.NetType</TypeName>
  <SelectionSetName>SelectionSet</SelectionSetName>
</ViewSelectedBy>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="14637-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="14637-107">Attributes and Elements</span></span>

<span data-ttu-id="14637-108">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és szülőelemét a `ViewSelectedBy` elemet.</span><span class="sxs-lookup"><span data-stu-id="14637-108">The following sections describe the attributes, child elements, and parent element of the `ViewSelectedBy` element.</span></span> <span data-ttu-id="14637-109">Ezt az elemet kell tartalmaznia kell legalább egy `TypeName` vagy `SelectionSetName` gyermekelemet.</span><span class="sxs-lookup"><span data-stu-id="14637-109">This element must contain at least one `TypeName` or `SelectionSetName` child element.</span></span> <span data-ttu-id="14637-110">Nem adható meg gyermekelemek száma korlátozott, sem a sorrend fontos.</span><span class="sxs-lookup"><span data-stu-id="14637-110">There is no limit to the number of child elements that can be specified nor is their order significant.</span></span>

### <a name="attributes"></a><span data-ttu-id="14637-111">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="14637-111">Attributes</span></span>

<span data-ttu-id="14637-112">Nincs.</span><span class="sxs-lookup"><span data-stu-id="14637-112">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="14637-113">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="14637-113">Child Elements</span></span>

|<span data-ttu-id="14637-114">Elem</span><span class="sxs-lookup"><span data-stu-id="14637-114">Element</span></span>|<span data-ttu-id="14637-115">Leírás</span><span class="sxs-lookup"><span data-stu-id="14637-115">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="14637-116">TypeName eleme ViewSelectedBy (formátum)</span><span class="sxs-lookup"><span data-stu-id="14637-116">TypeName Element for ViewSelectedBy (Format)</span></span>](./typename-element-for-viewselectedby-format.md)|<span data-ttu-id="14637-117">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="14637-117">Optional element.</span></span><br /><br /> <span data-ttu-id="14637-118">Megadja a nézet által megjelenített .NET-objektumokat.</span><span class="sxs-lookup"><span data-stu-id="14637-118">Specifies a .NET object that is displayed by the view.</span></span>|
|[<span data-ttu-id="14637-119">SelectionSetName eleme ViewSelectedBy (formátum)</span><span class="sxs-lookup"><span data-stu-id="14637-119">SelectionSetName Element for ViewSelectedBy (Format)</span></span>](./selectionsetname-element-for-viewselectedby-format.md)|<span data-ttu-id="14637-120">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="14637-120">Optional element.</span></span><br /><br /> <span data-ttu-id="14637-121">.NET-objektumokat a nézet által megjelenített egy halmazát határozza meg.</span><span class="sxs-lookup"><span data-stu-id="14637-121">Specifies a set of .NET objects that are displayed by the view.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="14637-122">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="14637-122">Parent Elements</span></span>

|<span data-ttu-id="14637-123">Elem</span><span class="sxs-lookup"><span data-stu-id="14637-123">Element</span></span>|<span data-ttu-id="14637-124">Leírás</span><span class="sxs-lookup"><span data-stu-id="14637-124">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="14637-125">Nézet elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="14637-125">View Element (Format)</span></span>](./view-element-format.md)|<span data-ttu-id="14637-126">Legalább egy .NET-objektumokat megjelenítő nézet határozza meg.</span><span class="sxs-lookup"><span data-stu-id="14637-126">Defines a view that displays one or more .NET objects.</span></span>|

## <a name="remarks"></a><span data-ttu-id="14637-127">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="14637-127">Remarks</span></span>

<span data-ttu-id="14637-128">Ez az elem használatának módja a következőben különböző nézeteket kapcsolatos további információkért lásd: [táblázat nézet összetevők](./creating-a-table-view.md), [lista nézet összetevők](./creating-a-list-view.md), [széles nézet összetevők](./creating-a-wide-view.md), és [Egyéni vezérlő összetevők](./creating-custom-controls.md).</span><span class="sxs-lookup"><span data-stu-id="14637-128">For more information about how this element is used in different views, see [Table View Components](./creating-a-table-view.md), [List View Components](./creating-a-list-view.md), [Wide View Components](./creating-a-wide-view.md), and [Custom Control Components](./creating-custom-controls.md).</span></span>

<span data-ttu-id="14637-129">A `SelectionSetName` elem szolgál, ha a formázási fájl határozza meg, amely több nézetek által megjelenített objektumok közül.</span><span class="sxs-lookup"><span data-stu-id="14637-129">The `SelectionSetName` element is used when the formatting file defines a set of objects that are displayed by multiple views.</span></span> <span data-ttu-id="14637-130">Kijelölt csoportok definiált és hivatkozott hogyan kapcsolatos további információkért lásd: [meghatározása beállítja az objektumok](./defining-selection-sets.md).</span><span class="sxs-lookup"><span data-stu-id="14637-130">For more information about how selection sets are defined and referenced, see [Defining Sets of Objects](./defining-selection-sets.md).</span></span>

## <a name="example"></a><span data-ttu-id="14637-131">Példa</span><span class="sxs-lookup"><span data-stu-id="14637-131">Example</span></span>

<span data-ttu-id="14637-132">Az alábbi példa bemutatja, hogyan adja meg a [System.Serviceprocess.Servicecontroller](/dotnet/api/System.ServiceProcess.ServiceController) objektum az adott nézet.</span><span class="sxs-lookup"><span data-stu-id="14637-132">The following example shows how to specify the [System.Serviceprocess.Servicecontroller](/dotnet/api/System.ServiceProcess.ServiceController) object for a list view.</span></span> <span data-ttu-id="14637-133">Tábla, széles és egyéni nézetekben használható ugyanazzal a sémával.</span><span class="sxs-lookup"><span data-stu-id="14637-133">The same schema is used for table, wide, and custom views.</span></span>

```xml
<View>
  <Name>System.ServiceProcess.ServiceController</Name>
  <ViewSelectedBy>
    <TypeName>System.ServiceProcess.ServiceController</TypeName>
  </ViewSelectedBy>
  <ListControl>...</ListControl>
</View>
```

## <a name="see-also"></a><span data-ttu-id="14637-134">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="14637-134">See Also</span></span>

[<span data-ttu-id="14637-135">Lista nézet létrehozása</span><span class="sxs-lookup"><span data-stu-id="14637-135">Creating a List View</span></span>](./creating-a-list-view.md)

[<span data-ttu-id="14637-136">Tábla nézet létrehozása</span><span class="sxs-lookup"><span data-stu-id="14637-136">Creating a Table View</span></span>](./creating-a-table-view.md)

[<span data-ttu-id="14637-137">Egy széles nézet létrehozása</span><span class="sxs-lookup"><span data-stu-id="14637-137">Creating a Wide View</span></span>](./creating-a-wide-view.md)

[<span data-ttu-id="14637-138">Egyéni vezérlők létrehozását</span><span class="sxs-lookup"><span data-stu-id="14637-138">Creating Custom Controls</span></span>](./creating-custom-controls.md)

[<span data-ttu-id="14637-139">Kijelölt csoportok meghatározása</span><span class="sxs-lookup"><span data-stu-id="14637-139">Defining Selection Sets</span></span>](./defining-selection-sets.md)

[<span data-ttu-id="14637-140">SelectionSetName eleme ViewSelectedBy (formátum)</span><span class="sxs-lookup"><span data-stu-id="14637-140">SelectionSetName Element for ViewSelectedBy (Format)</span></span>](./selectionsetname-element-for-viewselectedby-format.md)

[<span data-ttu-id="14637-141">TypeName elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="14637-141">TypeName Element (Format)</span></span>](./typename-element-for-viewselectedby-format.md)

[<span data-ttu-id="14637-142">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="14637-142">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
