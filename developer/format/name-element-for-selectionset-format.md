---
title: Elem name (formátum) SelectionSet |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 914917f7-0efc-4d1f-88bd-de714bedd98f
caps.latest.revision: 15
ms.openlocfilehash: 29dbdbd335511e4ca2706a625541554825838f23
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62065155"
---
# <a name="name-element-for-selectionset-format"></a><span data-ttu-id="3b01e-102">A SelectionSet Név eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="3b01e-102">Name Element for SelectionSet (Format)</span></span>

<span data-ttu-id="3b01e-103">Megadja a mutató hivatkozás a kijelölés-készlet nevét.</span><span class="sxs-lookup"><span data-stu-id="3b01e-103">Specifies the name used to reference the selection set.</span></span>

<span data-ttu-id="3b01e-104">Konfigurációs elem (formátum) SelectionSets elem (formátum) SelectionSet elem (formátum) nevet eleme SelectionSet (formátum)</span><span class="sxs-lookup"><span data-stu-id="3b01e-104">Configuration Element (Format) SelectionSets Element (Format) SelectionSet Element (Format) Name Element of SelectionSet (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="3b01e-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="3b01e-105">Syntax</span></span>

```xml
<Name>Name of selection set</Name>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="3b01e-106">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="3b01e-106">Attributes and Elements</span></span>

<span data-ttu-id="3b01e-107">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és szülőelemét a `Name` elemet.</span><span class="sxs-lookup"><span data-stu-id="3b01e-107">The following sections describe the attributes, child elements, and parent element of the `Name` Element.</span></span>

### <a name="attributes"></a><span data-ttu-id="3b01e-108">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="3b01e-108">Attributes</span></span>

<span data-ttu-id="3b01e-109">Nincs.</span><span class="sxs-lookup"><span data-stu-id="3b01e-109">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="3b01e-110">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="3b01e-110">Child Elements</span></span>

<span data-ttu-id="3b01e-111">Nincs.</span><span class="sxs-lookup"><span data-stu-id="3b01e-111">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="3b01e-112">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="3b01e-112">Parent Elements</span></span>

|<span data-ttu-id="3b01e-113">Elem</span><span class="sxs-lookup"><span data-stu-id="3b01e-113">Element</span></span>|<span data-ttu-id="3b01e-114">Leírás</span><span class="sxs-lookup"><span data-stu-id="3b01e-114">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="3b01e-115">SelectionSet elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="3b01e-115">SelectionSet Element (Format)</span></span>](./selectionset-element-format.md)|<span data-ttu-id="3b01e-116">Meghatároz egy egységes .NET-objektumokat a készlet neve szerint lehet hivatkozni.</span><span class="sxs-lookup"><span data-stu-id="3b01e-116">Defines a single set of .NET objects that can be referenced by the name of the set.</span></span>|

## <a name="text-value"></a><span data-ttu-id="3b01e-117">A szöveges érték</span><span class="sxs-lookup"><span data-stu-id="3b01e-117">Text Value</span></span>

<span data-ttu-id="3b01e-118">Adja meg a nevét, a kijelölés set hivatkozni.</span><span class="sxs-lookup"><span data-stu-id="3b01e-118">Specify the name to reference the selection set.</span></span> <span data-ttu-id="3b01e-119">Nincsenek nem korlátozza a feltárhatja, hogy mely karakterek használhatók.</span><span class="sxs-lookup"><span data-stu-id="3b01e-119">There are no restrictions as to what characters can be used.</span></span>

## <a name="remarks"></a><span data-ttu-id="3b01e-120">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="3b01e-120">Remarks</span></span>

<span data-ttu-id="3b01e-121">Az itt megadott név használatban van a `SelectionSetName` elemet.</span><span class="sxs-lookup"><span data-stu-id="3b01e-121">The name specified here is used in the `SelectionSetName` element.</span></span> <span data-ttu-id="3b01e-122">A nézet definíciója szerint a nézet által használható kijelölés set (nézetek rendelkezhet több definíciókat), vagy egy kiválasztási feltétel megadásakor.</span><span class="sxs-lookup"><span data-stu-id="3b01e-122">The selection set that can be used by a view, by a definition of a view (views can have multiple definitions), or when specifying a selection condition.</span></span> <span data-ttu-id="3b01e-123">Kijelölt csoportok kapcsolatos további információkért lásd: [meghatározása beállítja az objektumok](./defining-selection-sets.md).</span><span class="sxs-lookup"><span data-stu-id="3b01e-123">For more information about selection sets, see [Defining Sets of Objects](./defining-selection-sets.md).</span></span>

## <a name="example"></a><span data-ttu-id="3b01e-124">Példa</span><span class="sxs-lookup"><span data-stu-id="3b01e-124">Example</span></span>

<span data-ttu-id="3b01e-125">Ez a példa bemutatja egy `SelectionSet` elem, amely négy .NET típusa határozza meg.</span><span class="sxs-lookup"><span data-stu-id="3b01e-125">This example shows a `SelectionSet` element that defines four .NET types.</span></span> <span data-ttu-id="3b01e-126">A kijelölt csoport név "FileSystemTypes".</span><span class="sxs-lookup"><span data-stu-id="3b01e-126">The name of the selection set is "FileSystemTypes".</span></span>

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

## <a name="see-also"></a><span data-ttu-id="3b01e-127">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="3b01e-127">See Also</span></span>

[<span data-ttu-id="3b01e-128">Kijelölt csoportok meghatározása</span><span class="sxs-lookup"><span data-stu-id="3b01e-128">Defining Selection Sets</span></span>](./defining-selection-sets.md)

[<span data-ttu-id="3b01e-129">SelectionSet elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="3b01e-129">SelectionSet Element (Format)</span></span>](./selectionset-element-format.md)

[<span data-ttu-id="3b01e-130">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="3b01e-130">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
