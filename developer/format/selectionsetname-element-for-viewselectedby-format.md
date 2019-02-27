---
title: (Formátum) ViewSelectedBy SelectionSetName eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 8ab0f033-df09-4435-a8bd-76ec2d01f13b
caps.latest.revision: 13
ms.openlocfilehash: d1de2b30860bac80bf17508f40eec33c2794c4b2
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56848446"
---
# <a name="selectionsetname-element-for-viewselectedby-format"></a><span data-ttu-id="de06d-102">A ViewSelectedBy elem SelectionSetName eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="de06d-102">SelectionSetName Element for ViewSelectedBy (Format)</span></span>

<span data-ttu-id="de06d-103">.NET-objektumokat a nézet által megjelenített egy halmazát határozza meg.</span><span class="sxs-lookup"><span data-stu-id="de06d-103">Specifies a set of .NET objects that are displayed by the view.</span></span>

<span data-ttu-id="de06d-104">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem ViewSelectedBy elem (formátum) SelectionSetName eleme ViewSelectedBy (formátum)</span><span class="sxs-lookup"><span data-stu-id="de06d-104">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) ViewSelectedBy Element (Format) SelectionSetName Element for ViewSelectedBy (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="de06d-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="de06d-105">Syntax</span></span>

```xml
<SelectionSetName>Name of selection set<SelectionSetName>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="de06d-106">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="de06d-106">Attributes and Elements</span></span>

<span data-ttu-id="de06d-107">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `SelectionSetName` elemet.</span><span class="sxs-lookup"><span data-stu-id="de06d-107">The following sections describe the attributes, child elements, and the parent element of the `SelectionSetName` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="de06d-108">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="de06d-108">Attributes</span></span>

<span data-ttu-id="de06d-109">Nincs.</span><span class="sxs-lookup"><span data-stu-id="de06d-109">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="de06d-110">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="de06d-110">Child Elements</span></span>

<span data-ttu-id="de06d-111">Nincs.</span><span class="sxs-lookup"><span data-stu-id="de06d-111">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="de06d-112">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="de06d-112">Parent Elements</span></span>

|<span data-ttu-id="de06d-113">Elem</span><span class="sxs-lookup"><span data-stu-id="de06d-113">Element</span></span>|<span data-ttu-id="de06d-114">Leírás</span><span class="sxs-lookup"><span data-stu-id="de06d-114">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="de06d-115">ViewSelectedBy elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="de06d-115">ViewSelectedBy Element (Format)</span></span>](./viewselectedby-element-format.md)|<span data-ttu-id="de06d-116">A .NET-objektumokat a nézet által megjelenített határozza meg.</span><span class="sxs-lookup"><span data-stu-id="de06d-116">Defines the .NET objects that are displayed by the view.</span></span>|

## <a name="text-value"></a><span data-ttu-id="de06d-117">Szöveges érték</span><span class="sxs-lookup"><span data-stu-id="de06d-117">Text Value</span></span>

<span data-ttu-id="de06d-118">Adja meg a kijelölési beállítása által meghatározott nevét a `Name` elem a kijelölés van állítva.</span><span class="sxs-lookup"><span data-stu-id="de06d-118">Specify the name of the selection set that is defined by the `Name` element for the selection set.</span></span>

## <a name="remarks"></a><span data-ttu-id="de06d-119">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="de06d-119">Remarks</span></span>

<span data-ttu-id="de06d-120">Kijelölt csoportok is használhatja, ha egyetlen nevet, például az öröklődés kapcsolódó objektumok közül a hivatkozni kívánt kapcsolódó objektumok közül.</span><span class="sxs-lookup"><span data-stu-id="de06d-120">You can use selection sets when you have a set of related objects that you want to reference by using a single name, such as a set of objects that are related through inheritance.</span></span> <span data-ttu-id="de06d-121">Meghatározása és a kijelölt csoportok hivatkozó kapcsolatos további információkért lásd: [meghatározása beállítja az objektumok](./defining-selection-sets.md).</span><span class="sxs-lookup"><span data-stu-id="de06d-121">For more information about defining and referencing selection sets, see [Defining Sets of Objects](./defining-selection-sets.md).</span></span>

## <a name="example"></a><span data-ttu-id="de06d-122">Példa</span><span class="sxs-lookup"><span data-stu-id="de06d-122">Example</span></span>

<span data-ttu-id="de06d-123">Az alábbi példa bemutatja, hogyan állítsa be az adott nézet kijelölés megadásához.</span><span class="sxs-lookup"><span data-stu-id="de06d-123">The following example shows how to specify a selection set for a list view.</span></span> <span data-ttu-id="de06d-124">Tábla, széles és egyéni nézetekben használható ugyanazzal a sémával.</span><span class="sxs-lookup"><span data-stu-id="de06d-124">The same schema is used for table, wide, and custom views.</span></span>

```xml
<View>
  <Name>Name of View</Name>
  <ViewSelectedBy>
    <SelectionSetName>NameofSelectionSet</SelectionSetName>>
  </ViewSelectedBy>
  <ListControl>...</ListControl>
</View>
```

## <a name="see-also"></a><span data-ttu-id="de06d-125">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="de06d-125">See Also</span></span>

[<span data-ttu-id="de06d-126">Kijelölt csoportok meghatározása</span><span class="sxs-lookup"><span data-stu-id="de06d-126">Defining Selection Sets</span></span>](./defining-selection-sets.md)

[<span data-ttu-id="de06d-127">ViewSelectedBy elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="de06d-127">ViewSelectedBy Element (Format)</span></span>](./viewselectedby-element-format.md)

[<span data-ttu-id="de06d-128">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="de06d-128">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
