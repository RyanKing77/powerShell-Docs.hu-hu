---
title: SelectionSet elem (formátum) |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 848e7acd-d578-4fd1-a575-c0c3b9b5e68a
caps.latest.revision: 17
ms.openlocfilehash: c809aa6c3a40d16cfd2fd99065a846d265ec0f61
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56850420"
---
# <a name="selectionset-element-format"></a><span data-ttu-id="ef1d5-102">SelectionSet elem (Formátum)</span><span class="sxs-lookup"><span data-stu-id="ef1d5-102">SelectionSet Element (Format)</span></span>

<span data-ttu-id="ef1d5-103">Meghatároz egy .NET-objektumokat a készlet neve szerint lehet hivatkozni.</span><span class="sxs-lookup"><span data-stu-id="ef1d5-103">Defines a set of .NET objects that can be referenced by the name of the set.</span></span>

<span data-ttu-id="ef1d5-104">Konfigurációs elem (formátum) SelectionSets elem (formátum) SelectionSet elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="ef1d5-104">Configuration Element (Format) SelectionSets Element (Format) SelectionSet Element (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="ef1d5-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="ef1d5-105">Syntax</span></span>

```xml
<SelectionSet>
  <Name>SelectionSetName</Name>
  <Types>...</Types>
</SelectionSet>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="ef1d5-106">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="ef1d5-106">Attributes and Elements</span></span>

<span data-ttu-id="ef1d5-107">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `SelectionSet` elemet.</span><span class="sxs-lookup"><span data-stu-id="ef1d5-107">The following sections describe the attributes, child elements, and the parent element of the `SelectionSet` element.</span></span> <span data-ttu-id="ef1d5-108">Minden kijelölés set névvel kell rendelkeznie, és meg kell határoznia azt a .NET-objektumokat a készlet.</span><span class="sxs-lookup"><span data-stu-id="ef1d5-108">Each selection set must have a name, and it must specify the .NET objects of the set.</span></span>

### <a name="attributes"></a><span data-ttu-id="ef1d5-109">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="ef1d5-109">Attributes</span></span>

<span data-ttu-id="ef1d5-110">Nincs.</span><span class="sxs-lookup"><span data-stu-id="ef1d5-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="ef1d5-111">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="ef1d5-111">Child Elements</span></span>

|<span data-ttu-id="ef1d5-112">Elem</span><span class="sxs-lookup"><span data-stu-id="ef1d5-112">Element</span></span>|<span data-ttu-id="ef1d5-113">Leírás</span><span class="sxs-lookup"><span data-stu-id="ef1d5-113">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="ef1d5-114">Name elemet a SelectionSet (formátum)</span><span class="sxs-lookup"><span data-stu-id="ef1d5-114">Name Element for SelectionSet (Format)</span></span>](./name-element-for-selectionset-format.md)|<span data-ttu-id="ef1d5-115">Szükséges eleme.</span><span class="sxs-lookup"><span data-stu-id="ef1d5-115">Required element.</span></span><br /><br /> <span data-ttu-id="ef1d5-116">Megadja a mutató hivatkozás a kijelölés-készlet nevét.</span><span class="sxs-lookup"><span data-stu-id="ef1d5-116">Specifies the name used to reference the selection set.</span></span>|
|[<span data-ttu-id="ef1d5-117">Típusok elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="ef1d5-117">Types Element (Format)</span></span>](./types-element-for-selectionset-format.md)|<span data-ttu-id="ef1d5-118">Szükséges eleme.</span><span class="sxs-lookup"><span data-stu-id="ef1d5-118">Required element.</span></span><br /><br /> <span data-ttu-id="ef1d5-119">Meghatározza a .NET-objektumok, amelyek a kijelölés beállítva.</span><span class="sxs-lookup"><span data-stu-id="ef1d5-119">Defines the .NET objects that are in the selection set.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="ef1d5-120">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="ef1d5-120">Parent Elements</span></span>

|<span data-ttu-id="ef1d5-121">Elem</span><span class="sxs-lookup"><span data-stu-id="ef1d5-121">Element</span></span>|<span data-ttu-id="ef1d5-122">Leírás</span><span class="sxs-lookup"><span data-stu-id="ef1d5-122">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="ef1d5-123">SelectionSets elem formátuma</span><span class="sxs-lookup"><span data-stu-id="ef1d5-123">SelectionSets Element Format</span></span>](./selectionsets-element-format.md)|<span data-ttu-id="ef1d5-124">Határozza meg a gyakori eljárások egyikét a formázási fájl összes nézetek által használható .NET-objektumokat.</span><span class="sxs-lookup"><span data-stu-id="ef1d5-124">Defines the common sets of .NET objects that can be used by all views of the formatting file.</span></span>|

## <a name="remarks"></a><span data-ttu-id="ef1d5-125">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="ef1d5-125">Remarks</span></span>

<span data-ttu-id="ef1d5-126">Kijelölt csoportok is használhatja, ha egyetlen nevet, például az öröklődés kapcsolódó objektumok közül a hivatkozni kívánt kapcsolódó objektumok közül.</span><span class="sxs-lookup"><span data-stu-id="ef1d5-126">You can use selection sets when you have a set of related objects that you want to reference by using a single name, such as a set of objects that are related through inheritance.</span></span> <span data-ttu-id="ef1d5-127">A nézetek meghatározásakor a neve helyett az egyes nézetek összes objektumához ajánlati beállítása a kijelölt objektumok készlete is megadhat.</span><span class="sxs-lookup"><span data-stu-id="ef1d5-127">When defining your views, you can specify the set of objects by using the name of the selection set instead of listing all the objects within each view.</span></span>

<span data-ttu-id="ef1d5-128">Közös kijelölt csoportok neve szerint vannak megadva, a nézetek a formázási fájl vagy a definíciók nézetek meghatározásakor.</span><span class="sxs-lookup"><span data-stu-id="ef1d5-128">Common selection sets are specified by their name when defining the views of the formatting file or the definitions of the views.</span></span> <span data-ttu-id="ef1d5-129">Ezekben az esetekben a `SelectionSetName` gyermekeleme a `ViewSelectedBy` és `EntrySelectedBy` elemek szolgáló megadja.</span><span class="sxs-lookup"><span data-stu-id="ef1d5-129">In these cases, the `SelectionSetName` child element of the `ViewSelectedBy` and `EntrySelectedBy` elements specifies the set to be used.</span></span> <span data-ttu-id="ef1d5-130">Kijelölt csoportok kapcsolatos további információkért lásd: [meghatározása beállítja az objektumok](./defining-selection-sets.md).</span><span class="sxs-lookup"><span data-stu-id="ef1d5-130">For more information about selection sets, see [Defining Sets of Objects](./defining-selection-sets.md).</span></span>

## <a name="example"></a><span data-ttu-id="ef1d5-131">Példa</span><span class="sxs-lookup"><span data-stu-id="ef1d5-131">Example</span></span>

<span data-ttu-id="ef1d5-132">A következő példa bemutatja egy `SelectionSet` elem, amely négy .NET típusa határozza meg.</span><span class="sxs-lookup"><span data-stu-id="ef1d5-132">The following example shows a `SelectionSet` element that defines four .NET types.</span></span>

```xml
<SelectionSets>
  <SelectionSet>
    <Name>FileSystemTypes</Name>
    <Types>
     <TypeName>System.IO.DirectoryInfo</TypeName>
     <TypeName>System.IO.FileInfo</TypeName>
     <TypeName>Deserialized.System.IO.DirectoryInfo</TypeName>
     <TypeName>Deserialized.System.IO.FileInfo</TypeName>
    </Types>
  </SelectionSet>
</SelectionSets>
```

## <a name="see-also"></a><span data-ttu-id="ef1d5-133">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="ef1d5-133">See Also</span></span>

[<span data-ttu-id="ef1d5-134">Kijelölt csoportok meghatározása</span><span class="sxs-lookup"><span data-stu-id="ef1d5-134">Defining Selection Sets</span></span>](./defining-selection-sets.md)

[<span data-ttu-id="ef1d5-135">Name elemet a SelectionSet (formátum)</span><span class="sxs-lookup"><span data-stu-id="ef1d5-135">Name Element of SelectionSet (Format)</span></span>](./name-element-for-selectionset-format.md)

[<span data-ttu-id="ef1d5-136">SelectionSets elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="ef1d5-136">SelectionSets Element (Format)</span></span>](./selectionsets-element-format.md)

[<span data-ttu-id="ef1d5-137">Típusok elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="ef1d5-137">Types Element (Format)</span></span>](./types-element-for-selectionset-format.md)

[<span data-ttu-id="ef1d5-138">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="ef1d5-138">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
