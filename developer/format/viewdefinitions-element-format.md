---
title: ViewDefinitions elem (formátum) |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 29840c10-2b30-4bb1-a8a0-ddf84d19c2d0
caps.latest.revision: 18
ms.openlocfilehash: c5ec80350c7707ccd41112ab5e1952e5dc198cca
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56851071"
---
# <a name="viewdefinitions-element-format"></a><span data-ttu-id="39df9-102">ViewDefinitions elem (Formátum)</span><span class="sxs-lookup"><span data-stu-id="39df9-102">ViewDefinitions Element (Format)</span></span>

<span data-ttu-id="39df9-103">A .NET-objektumokat megjelenítő nézetek határozza meg.</span><span class="sxs-lookup"><span data-stu-id="39df9-103">Defines the views used to display .NET objects.</span></span> <span data-ttu-id="39df9-104">Ezek a nézetek megjelenítheti a tulajdonságok és parancsfájl-értékek az objektum egy táblázatos formátumú, listaformátumban, széles és egyéni vezérlő formátumban.</span><span class="sxs-lookup"><span data-stu-id="39df9-104">These views can display the properties and script values of an object  in a table format, list format, wide format, and custom control format.</span></span>

<span data-ttu-id="39df9-105">Konfigurációs elem (formátum) ViewDefinitions (XML formátum) elem</span><span class="sxs-lookup"><span data-stu-id="39df9-105">Configuration Element (Format) ViewDefinitions (Format XML) Element</span></span>

## <a name="syntax"></a><span data-ttu-id="39df9-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="39df9-106">Syntax</span></span>

```xml

<ViewDefinitions>
  <View>...</View>
</ViewDefinitions>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="39df9-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="39df9-107">Attributes and Elements</span></span>

<span data-ttu-id="39df9-108">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és szülőelemét a `ViewDefinitions` elemet.</span><span class="sxs-lookup"><span data-stu-id="39df9-108">The following sections describe the attributes, child elements, and parent element of the `ViewDefinitions` element.</span></span> <span data-ttu-id="39df9-109">Nem korlátozott a formázási-fájlban definiált nézetek számát, és bármilyen sorrendben követően adhatók hozzá.</span><span class="sxs-lookup"><span data-stu-id="39df9-109">There is no limit to the number of views that can be defined in a formatting file, and they can be added in any order.</span></span>

### <a name="attributes"></a><span data-ttu-id="39df9-110">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="39df9-110">Attributes</span></span>

<span data-ttu-id="39df9-111">Nincs.</span><span class="sxs-lookup"><span data-stu-id="39df9-111">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="39df9-112">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="39df9-112">Child Elements</span></span>

|<span data-ttu-id="39df9-113">Elem</span><span class="sxs-lookup"><span data-stu-id="39df9-113">Element</span></span>|<span data-ttu-id="39df9-114">Leírás</span><span class="sxs-lookup"><span data-stu-id="39df9-114">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="39df9-115">Nézet elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="39df9-115">View Element (Format)</span></span>](./view-element-format.md)|<span data-ttu-id="39df9-116">Meghatározza egy nézetet, amely legalább egy .NET-objektumokká megjelenítésére szolgál.</span><span class="sxs-lookup"><span data-stu-id="39df9-116">Defines a view that is used to display one or more .NET objects.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="39df9-117">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="39df9-117">Parent Elements</span></span>

|<span data-ttu-id="39df9-118">Elem</span><span class="sxs-lookup"><span data-stu-id="39df9-118">Element</span></span>|<span data-ttu-id="39df9-119">Leírás</span><span class="sxs-lookup"><span data-stu-id="39df9-119">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="39df9-120">Konfigurációs elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="39df9-120">Configuration Element (Format)</span></span>](./configuration-element-format.md)|<span data-ttu-id="39df9-121">A legfelső szintű elem egy formázási fájl jelöli.</span><span class="sxs-lookup"><span data-stu-id="39df9-121">Represents the top-level element of a formatting file.</span></span>|

## <a name="remarks"></a><span data-ttu-id="39df9-122">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="39df9-122">Remarks</span></span>

<span data-ttu-id="39df9-123">A nézetek különböző típusainak összetevőivel kapcsolatos további információkért lásd a következő témaköröket:</span><span class="sxs-lookup"><span data-stu-id="39df9-123">For more information about the components of the different types of views, see the following topics:</span></span>

- [<span data-ttu-id="39df9-124">Tábla nézet létrehozása</span><span class="sxs-lookup"><span data-stu-id="39df9-124">Creating a Table View</span></span>](./creating-a-table-view.md)

- [<span data-ttu-id="39df9-125">Lista nézet létrehozása</span><span class="sxs-lookup"><span data-stu-id="39df9-125">Creating a List View</span></span>](./creating-a-list-view.md)

- [<span data-ttu-id="39df9-126">Egy széles nézet létrehozása</span><span class="sxs-lookup"><span data-stu-id="39df9-126">Creating a Wide View</span></span>](./creating-a-wide-view.md)

- [<span data-ttu-id="39df9-127">Egyéni vezérlők</span><span class="sxs-lookup"><span data-stu-id="39df9-127">Custom Controls</span></span>](./creating-custom-controls.md)

## <a name="example"></a><span data-ttu-id="39df9-128">Példa</span><span class="sxs-lookup"><span data-stu-id="39df9-128">Example</span></span>

<span data-ttu-id="39df9-129">Ez a példa bemutatja egy `ViewDefinitions` elem, amely a táblázatos nézetre, és megjelenítheti a szülő elemeket tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="39df9-129">This example shows a `ViewDefinitions` element that contains the parent elements for a table view and a list view.</span></span>

```xml
<Configuration>
  <ViewDefinitions>
    <View>
      <TableControl>...</TableControl>
    </View>
    <View>
      <ListControl>...</ListControl>
    </View>
  </ViewDefinitions>
</Configuration>
```

## <a name="see-also"></a><span data-ttu-id="39df9-130">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="39df9-130">See Also</span></span>

[<span data-ttu-id="39df9-131">Konfigurációs elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="39df9-131">Configuration Element (Format)</span></span>](./configuration-element-format.md)

[<span data-ttu-id="39df9-132">Nézet elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="39df9-132">View Element (Format)</span></span>](./view-element-format.md)

[<span data-ttu-id="39df9-133">Tábla nézet létrehozása</span><span class="sxs-lookup"><span data-stu-id="39df9-133">Creating a Table View</span></span>](./creating-a-table-view.md)

[<span data-ttu-id="39df9-134">Lista nézet létrehozása</span><span class="sxs-lookup"><span data-stu-id="39df9-134">Creating a List View</span></span>](./creating-a-list-view.md)

[<span data-ttu-id="39df9-135">Egy széles nézet létrehozása</span><span class="sxs-lookup"><span data-stu-id="39df9-135">Creating a Wide View</span></span>](./creating-a-wide-view.md)

[<span data-ttu-id="39df9-136">Egyéni vezérlők</span><span class="sxs-lookup"><span data-stu-id="39df9-136">Custom Controls</span></span>](./creating-custom-controls.md)

[<span data-ttu-id="39df9-137">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="39df9-137">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
