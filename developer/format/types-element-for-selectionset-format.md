---
title: Elem SelectionSet (formátum)-típusokat |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 4606fec0-ff31-4d36-af68-227405335ec3
caps.latest.revision: 15
ms.openlocfilehash: 0427367efa2c8a7e352d718706d1341a0c8e3621
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56851274"
---
# <a name="types-element-for-selectionset-format"></a><span data-ttu-id="f301a-102">A SelectionSet Típusok eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="f301a-102">Types Element for SelectionSet (Format)</span></span>

<span data-ttu-id="f301a-103">Meghatározza a .NET-objektumok, amelyek a kijelölés beállítva.</span><span class="sxs-lookup"><span data-stu-id="f301a-103">Defines the .NET objects that are in the selection set.</span></span>

<span data-ttu-id="f301a-104">Konfigurációs elem (formátum) SelectionSets elem (formátum) SelectionSet elem (formátum) típusú elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="f301a-104">Configuration Element (Format) SelectionSets Element (Format) SelectionSet Element (Format) Types Element (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="f301a-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="f301a-105">Syntax</span></span>

```xml
<Types>
  <TypeName>Nameof.NetType</TypeName>
</Types>

```

## <a name="attributes-and-elements"></a><span data-ttu-id="f301a-106">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="f301a-106">Attributes and Elements</span></span>

<span data-ttu-id="f301a-107">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `Types` elemet.</span><span class="sxs-lookup"><span data-stu-id="f301a-107">The following sections describe the attributes, child elements, and the parent element of the `Types` element.</span></span> <span data-ttu-id="f301a-108">Legalább egy gyermek elemnek kell lennie, de nem adható hozzá gyermek elemek számának maximális korlátozott.</span><span class="sxs-lookup"><span data-stu-id="f301a-108">There must be at least one child element, but there is no maximum limit to the number of child elements that can be added.</span></span>

### <a name="attributes"></a><span data-ttu-id="f301a-109">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="f301a-109">Attributes</span></span>

<span data-ttu-id="f301a-110">Nincs.</span><span class="sxs-lookup"><span data-stu-id="f301a-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="f301a-111">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="f301a-111">Child Elements</span></span>

|<span data-ttu-id="f301a-112">Elem</span><span class="sxs-lookup"><span data-stu-id="f301a-112">Element</span></span>|<span data-ttu-id="f301a-113">Leírás</span><span class="sxs-lookup"><span data-stu-id="f301a-113">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="f301a-114">TypeName elem típusú (formátum)</span><span class="sxs-lookup"><span data-stu-id="f301a-114">TypeName Element of Types (Format)</span></span>](./typename-element-for-types-format.md)|<span data-ttu-id="f301a-115">Szükséges eleme.</span><span class="sxs-lookup"><span data-stu-id="f301a-115">Required element.</span></span><br /><br /> <span data-ttu-id="f301a-116">Megadja a .NET-objektum, amely a kijelölt csoporthoz tartozik.</span><span class="sxs-lookup"><span data-stu-id="f301a-116">Specifies the .NET object that belongs to the selection set.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="f301a-117">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="f301a-117">Parent Elements</span></span>

|<span data-ttu-id="f301a-118">Elem</span><span class="sxs-lookup"><span data-stu-id="f301a-118">Element</span></span>|<span data-ttu-id="f301a-119">Leírás</span><span class="sxs-lookup"><span data-stu-id="f301a-119">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="f301a-120">SelectionSet elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="f301a-120">SelectionSet Element (Format)</span></span>](./selectionset-element-format.md)|<span data-ttu-id="f301a-121">Meghatároz egy .NET-objektumokat a készlet neve szerint lehet hivatkozni.</span><span class="sxs-lookup"><span data-stu-id="f301a-121">Defines a set of .NET objects that can be referenced by the name of the set.</span></span>|

## <a name="remarks"></a><span data-ttu-id="f301a-122">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="f301a-122">Remarks</span></span>

<span data-ttu-id="f301a-123">Az objektumok, ez az elem által meghatározott nézet definíciójának által a nézet által használható kijelölés csoportjának győződjön meg arról, (nézetek rendelkezhet több definíciókat), vagy egy kiválasztási feltétel megadásakor.</span><span class="sxs-lookup"><span data-stu-id="f301a-123">The objects defined by this element make up a selection set that can be used by a view, by a definition of a view (views can have multiple definitions), or when specifying a selection condition.</span></span>  <span data-ttu-id="f301a-124">Kijelölt csoportok kapcsolatos további információkért lásd: [meghatározása beállítja az objektumok](./defining-selection-sets.md).</span><span class="sxs-lookup"><span data-stu-id="f301a-124">For more information about selection sets, see [Defining Sets of Objects](./defining-selection-sets.md).</span></span>

## <a name="example"></a><span data-ttu-id="f301a-125">Példa</span><span class="sxs-lookup"><span data-stu-id="f301a-125">Example</span></span>

<span data-ttu-id="f301a-126">Ez a példa bemutatja egy `SelectionSet` elem, amely négy .NET típusa határozza meg.</span><span class="sxs-lookup"><span data-stu-id="f301a-126">This example shows a `SelectionSet` element that defines four .NET types.</span></span>

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

## <a name="see-also"></a><span data-ttu-id="f301a-127">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="f301a-127">See Also</span></span>

[<span data-ttu-id="f301a-128">Az objektumok csoportok meghatározása</span><span class="sxs-lookup"><span data-stu-id="f301a-128">Defining Sets of Objects</span></span>](./defining-selection-sets.md)

[<span data-ttu-id="f301a-129">SelectionSet elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="f301a-129">SelectionSet Element (Format)</span></span>](./selectionset-element-format.md)

[<span data-ttu-id="f301a-130">TypeName elem típusú (formátum)</span><span class="sxs-lookup"><span data-stu-id="f301a-130">TypeName Element of Types (Format)</span></span>](./typename-element-for-types-format.md)

[<span data-ttu-id="f301a-131">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="f301a-131">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
