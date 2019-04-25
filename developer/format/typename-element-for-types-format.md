---
title: TypeName elem esetében (formátum) |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 0595b99e-b438-4240-b47b-555cf0316f33
caps.latest.revision: 15
ms.openlocfilehash: bd5baa03c2050b2c3bbe1d7697c253d923175d39
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62083790"
---
# <a name="typename-element-for-types-format"></a><span data-ttu-id="25783-102">A Típusok TypeName eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="25783-102">TypeName Element for Types (Format)</span></span>

<span data-ttu-id="25783-103">Megadja a .NET-típus egy objektum, amely a kijelölt csoporthoz tartozik.</span><span class="sxs-lookup"><span data-stu-id="25783-103">Specifies the .NET type of an object that belongs to the selection set.</span></span>

<span data-ttu-id="25783-104">Konfigurációs elem (formátum) SelectionSets elem (formátum) SelectionSet elem (formátum) típusú elem (formátum) TypeName elem típusú (formátum)</span><span class="sxs-lookup"><span data-stu-id="25783-104">Configuration Element (Format) SelectionSets Element (Format) SelectionSet Element (Format) Types Element (Format) TypeName Element of Types (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="25783-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="25783-105">Syntax</span></span>

```xml
<TypeName>Nameof.NetType</Name>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="25783-106">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="25783-106">Attributes and Elements</span></span>

<span data-ttu-id="25783-107">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `TypeName` elemet.</span><span class="sxs-lookup"><span data-stu-id="25783-107">The following sections describe the attributes, child elements, and the parent element of the `TypeName` element.</span></span> <span data-ttu-id="25783-108">Legalább egy `TypeName` elemének szerepelnie kell a kijelölés beállítása.</span><span class="sxs-lookup"><span data-stu-id="25783-108">At least one `TypeName` element must be included in the selection set.</span></span>

### <a name="attributes"></a><span data-ttu-id="25783-109">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="25783-109">Attributes</span></span>

<span data-ttu-id="25783-110">Nincs.</span><span class="sxs-lookup"><span data-stu-id="25783-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="25783-111">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="25783-111">Child Elements</span></span>

<span data-ttu-id="25783-112">Nincs.</span><span class="sxs-lookup"><span data-stu-id="25783-112">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="25783-113">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="25783-113">Parent Elements</span></span>

|<span data-ttu-id="25783-114">Elem</span><span class="sxs-lookup"><span data-stu-id="25783-114">Element</span></span>|<span data-ttu-id="25783-115">Leírás</span><span class="sxs-lookup"><span data-stu-id="25783-115">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="25783-116">Típusok elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="25783-116">Types Element (Format)</span></span>](./types-element-for-selectionset-format.md)|<span data-ttu-id="25783-117">Meghatározza a .NET-objektumok, amelyek a kijelölés beállítva.</span><span class="sxs-lookup"><span data-stu-id="25783-117">Defines the .NET objects that are in the selection set.</span></span>|

## <a name="text-value"></a><span data-ttu-id="25783-118">A szöveges érték</span><span class="sxs-lookup"><span data-stu-id="25783-118">Text Value</span></span>

<span data-ttu-id="25783-119">Adja meg a teljes nevet, a .NET-típus.</span><span class="sxs-lookup"><span data-stu-id="25783-119">Specify the fully qualified name for the .NET type.</span></span>

## <a name="remarks"></a><span data-ttu-id="25783-120">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="25783-120">Remarks</span></span>

<span data-ttu-id="25783-121">Kijelölt csoportok is használhatja, ha egyetlen nevet, például az öröklődés kapcsolódó objektumok közül a hivatkozni kívánt kapcsolódó objektumok közül.</span><span class="sxs-lookup"><span data-stu-id="25783-121">You can use selection sets when you have a set of related objects that you want to reference by using a single name, such as a set of objects that are related through inheritance.</span></span> <span data-ttu-id="25783-122">A nézetek meghatározásakor a neve helyett az egyes nézetek összes objektumához ajánlati beállítása a kijelölt objektumok készlete is megadhat.</span><span class="sxs-lookup"><span data-stu-id="25783-122">When defining your views, you can specify the set of objects by using the name of the selection set instead of listing all the objects within each view.</span></span>

<span data-ttu-id="25783-123">A formázási fájl a nézetek meghatározásakor általános kijelölt csoportok neve szerint vannak megadva.</span><span class="sxs-lookup"><span data-stu-id="25783-123">Common selection sets are specified by their name when defining the views of the formatting file.</span></span> <span data-ttu-id="25783-124">Ezekben az esetekben a `SelectionSetName` gyermekeleme a `ViewSelectedBy` a nézet elem megadja.</span><span class="sxs-lookup"><span data-stu-id="25783-124">In these cases, the `SelectionSetName` child element of the `ViewSelectedBy` element for the view specifies the set.</span></span> <span data-ttu-id="25783-125">Azonban a nézetek különböző bejegyzés is megadhatók azok kijelölés csak adott tételre a nézetet.</span><span class="sxs-lookup"><span data-stu-id="25783-125">However, different entries of a view can also specify a selection set that applies to only that entry of the view.</span></span> <span data-ttu-id="25783-126">Kijelölt csoportok kapcsolatos további információkért lásd: [meghatározása beállítja az objektumok](./defining-selection-sets.md).</span><span class="sxs-lookup"><span data-stu-id="25783-126">For more information about selection sets, see [Defining Sets of Objects](./defining-selection-sets.md).</span></span>

## <a name="example"></a><span data-ttu-id="25783-127">Példa</span><span class="sxs-lookup"><span data-stu-id="25783-127">Example</span></span>

<span data-ttu-id="25783-128">A következő példa bemutatja egy `SelectionSet` elem, amely négy .NET típusa határozza meg.</span><span class="sxs-lookup"><span data-stu-id="25783-128">The following example shows a `SelectionSet` element that defines four .NET types.</span></span>

```
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

## <a name="see-also"></a><span data-ttu-id="25783-129">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="25783-129">See Also</span></span>

[<span data-ttu-id="25783-130">Kijelölt csoportok meghatározása</span><span class="sxs-lookup"><span data-stu-id="25783-130">Defining Selection Sets</span></span>](./defining-selection-sets.md)

[<span data-ttu-id="25783-131">SelectionSet elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="25783-131">SelectionSet Element (Format)</span></span>](./selectionset-element-format.md)

[<span data-ttu-id="25783-132">SelectionSets elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="25783-132">SelectionSets Element (Format)</span></span>](./selectionsets-element-format.md)

[<span data-ttu-id="25783-133">Típusok elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="25783-133">Types Element (Format)</span></span>](./types-element-for-selectionset-format.md)

[<span data-ttu-id="25783-134">Egy Windows PowerShell formázás fájl írása</span><span class="sxs-lookup"><span data-stu-id="25783-134">Writing a Windows PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
