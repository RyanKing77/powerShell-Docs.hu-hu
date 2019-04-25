---
title: TableControl (formátum) a TableColumnItems TableColumnItem eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ef8395aa-4b31-48c0-a0b8-b481fd0b3738
caps.latest.revision: 15
ms.openlocfilehash: 159f943f6bfb33c5403b5714380631351523789f
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62063938"
---
# <a name="tablecolumnitem-element-for-tablecolumnitems-for-tablecontrol-format"></a><span data-ttu-id="c04af-102">A TableControl TableColumnItems elemének TableColumnItem eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="c04af-102">TableColumnItem Element for TableColumnItems for TableControl (Format)</span></span>

<span data-ttu-id="c04af-103">A tulajdonság, vagy a parancsfájl, amelynek értéke megjelenik a sor oszlop határozza meg.</span><span class="sxs-lookup"><span data-stu-id="c04af-103">Defines the property or script whose value is displayed in the column of the row.</span></span>

<span data-ttu-id="c04af-104">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem TableControl elem (formátum) TableRowEntries elem TableControl (formátum) TableRowEntry elemhez tartozó TableRowEntries TableControl (formátum) a TableControl (formátum) TableColumnItem elemhez tartozó TableColumnItems TableControl (formátum) a TableControlEntry TableColumnItems elem.</span><span class="sxs-lookup"><span data-stu-id="c04af-104">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) TableControl Element (Format) TableRowEntries Element for TableControl (Format) TableRowEntry Element for TableRowEntries for TableControl (Format) TableColumnItems Element for TableControlEntry for TableControl (Format) TableColumnItem Element for TableColumnItems for TableControl (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="c04af-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="c04af-105">Syntax</span></span>

```xml
<TableColumnItem>
  <Alignment>Left, Right, or Center</Alignment>
  <PropertyName>Nameof.NetProperty</PropertyName>
  <ScriptBlock>ScriptToEvaluate</ScriptBlock>
</TableColumnItem>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="c04af-106">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="c04af-106">Attributes and Elements</span></span>

<span data-ttu-id="c04af-107">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és szülőelemét a `TableColumnItem` elemet.</span><span class="sxs-lookup"><span data-stu-id="c04af-107">The following sections describe the attributes, child elements, and parent element of the `TableColumnItem` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="c04af-108">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="c04af-108">Attributes</span></span>

<span data-ttu-id="c04af-109">Nincs.</span><span class="sxs-lookup"><span data-stu-id="c04af-109">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="c04af-110">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="c04af-110">Child Elements</span></span>

|<span data-ttu-id="c04af-111">Elem</span><span class="sxs-lookup"><span data-stu-id="c04af-111">Element</span></span>|<span data-ttu-id="c04af-112">Leírás</span><span class="sxs-lookup"><span data-stu-id="c04af-112">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="c04af-113">Zarovnání eleme TableColumnItem a TableControl (formátum)</span><span class="sxs-lookup"><span data-stu-id="c04af-113">Alignment Element for TableColumnItem for TableControl (Format)</span></span>](./alignment-element-for-tablecolumnitem-for-tablecontrol-format.md)|<span data-ttu-id="c04af-114">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="c04af-114">Optional element.</span></span><br /><br /> <span data-ttu-id="c04af-115">Határozza meg, hogyan jelenjen meg a sor egy oszlopban lévő adatokat.</span><span class="sxs-lookup"><span data-stu-id="c04af-115">Defines how the data in a column of the row is displayed.</span></span>|
|[<span data-ttu-id="c04af-116">TableColumnItem TableControl (formátum) a FormatString elem.</span><span class="sxs-lookup"><span data-stu-id="c04af-116">FormatString Element for TableColumnItem for TableControl (Format)</span></span>](./formatstring-element-for-tablecolumnitem-for-tablecontrol-format.md)|<span data-ttu-id="c04af-117">Megadja a sor az oszlopban lévő adatok formázásához használt formátum mintát.</span><span class="sxs-lookup"><span data-stu-id="c04af-117">Specifies a format pattern that is used to format the data in the column of the row.</span></span>|
|[<span data-ttu-id="c04af-118">TableColumnItem TableControl (formátum) a PropertyName elem.</span><span class="sxs-lookup"><span data-stu-id="c04af-118">PropertyName Element for TableColumnItem for TableControl (Format)</span></span>](./propertyname-element-for-tablecolumnitem-for-tablecontrol-format.md)|<span data-ttu-id="c04af-119">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="c04af-119">Optional element.</span></span><br /><br /> <span data-ttu-id="c04af-120">Meghatározza a tulajdonságot, amelynek értéke megjelenik a nevét.</span><span class="sxs-lookup"><span data-stu-id="c04af-120">Specifies the name of the property whose value is displayed.</span></span>|
|[<span data-ttu-id="c04af-121">TableColumnItem TableControl (formátum) a scriptblock kulcsszót elem.</span><span class="sxs-lookup"><span data-stu-id="c04af-121">ScriptBlock Element for TableColumnItem for TableControl (Format)</span></span>](./scriptblock-element-for-tablecolumnitem-for-tablecontrol-format.md)|<span data-ttu-id="c04af-122">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="c04af-122">Optional element.</span></span><br /><br /> <span data-ttu-id="c04af-123">Megadja a parancsprogramot, amelynek az értéke az oszlop egy sor jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="c04af-123">Specifies the script whose value is displayed in the column of a row.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="c04af-124">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="c04af-124">Parent Elements</span></span>

|<span data-ttu-id="c04af-125">Elem</span><span class="sxs-lookup"><span data-stu-id="c04af-125">Element</span></span>|<span data-ttu-id="c04af-126">Leírás</span><span class="sxs-lookup"><span data-stu-id="c04af-126">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="c04af-127">A TableControl (formátum) TableControlEntry TableColumnItems elem.</span><span class="sxs-lookup"><span data-stu-id="c04af-127">TableColumnItems Element for TableControlEntry for TableControl (Format)</span></span>](./tablecolumnitems-element-for-tablerowentry-for-tablecontrol-format.md)|<span data-ttu-id="c04af-128">Határozza meg a Tulajdonságok vagy parancsfájlok, melynek értékei jelennek meg a sorban.</span><span class="sxs-lookup"><span data-stu-id="c04af-128">Defines the properties or scripts whose values are displayed in the row.</span></span>|

## <a name="remarks"></a><span data-ttu-id="c04af-129">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="c04af-129">Remarks</span></span>

<span data-ttu-id="c04af-130">A sor összes oszlopában egy tulajdonságát egy objektum vagy egy parancsfájlt is megadhat.</span><span class="sxs-lookup"><span data-stu-id="c04af-130">You can specify a property of an object or a script in each column of the row.</span></span> <span data-ttu-id="c04af-131">Ha nincs alárendelt elem meg van adva, az elem nem egy helyőrző és adatok nem van megjelenítve.</span><span class="sxs-lookup"><span data-stu-id="c04af-131">If no child elements are specified, the item is a placeholder, and no data is displayed.</span></span>

<span data-ttu-id="c04af-132">A táblázatos nézetre az összetevőivel kapcsolatos további információkért lásd: [tábla nézetek létrehozásával](./creating-a-table-view.md).</span><span class="sxs-lookup"><span data-stu-id="c04af-132">For more information about the components of a table view, see [Creating a Table View](./creating-a-table-view.md).</span></span>

## <a name="example"></a><span data-ttu-id="c04af-133">Példa</span><span class="sxs-lookup"><span data-stu-id="c04af-133">Example</span></span>

<span data-ttu-id="c04af-134">Ez a példa bemutatja egy `TableColumnItem` elem, amely értékét jeleníti meg a `Status` tulajdonságát a [System.Diagnostics.Process](/dotnet/api/System.Diagnostics.Process) objektum.</span><span class="sxs-lookup"><span data-stu-id="c04af-134">This example shows a `TableColumnItem` element that displays the value of the `Status` property of the [System.Diagnostics.Process](/dotnet/api/System.Diagnostics.Process) object.</span></span>

```xml
<TableColumnItem>
   <Alignment>Centered</Alignment>
  <PropertyName>Status</PropertyName>
</TableColumnItem>

```

## <a name="see-also"></a><span data-ttu-id="c04af-135">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="c04af-135">See Also</span></span>

[<span data-ttu-id="c04af-136">Tábla nézet létrehozása</span><span class="sxs-lookup"><span data-stu-id="c04af-136">Creating a Table View</span></span>](./creating-a-table-view.md)

[<span data-ttu-id="c04af-137">Zarovnání eleme TableColumnItem a TableControl (formátum)</span><span class="sxs-lookup"><span data-stu-id="c04af-137">Alignment Element for TableColumnItem for TableControl (Format)</span></span>](./alignment-element-for-tablecolumnitem-for-tablecontrol-format.md)

[<span data-ttu-id="c04af-138">TableColumnItems elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="c04af-138">TableColumnItems Element (Format)</span></span>](./tablecolumnitems-element-for-tablerowentry-for-tablecontrol-format.md)

[<span data-ttu-id="c04af-139">TableColumnItem TableControl (formátum) a FormatString elem.</span><span class="sxs-lookup"><span data-stu-id="c04af-139">FormatString Element for TableColumnItem for TableControl (Format)</span></span>](./formatstring-element-for-tablecolumnitem-for-tablecontrol-format.md)

[<span data-ttu-id="c04af-140">TableColumnItem TableControl (formátum) a PropertyName elem.</span><span class="sxs-lookup"><span data-stu-id="c04af-140">PropertyName Element for TableColumnItem for TableControl (Format)</span></span>](./propertyname-element-for-tablecolumnitem-for-tablecontrol-format.md)

[<span data-ttu-id="c04af-141">TableColumnItem TableControl (formátum) a scriptblock kulcsszót elem.</span><span class="sxs-lookup"><span data-stu-id="c04af-141">ScriptBlock Element for TableColumnItem for TableControl (Format)</span></span>](./scriptblock-element-for-tablecolumnitem-for-tablecontrol-format.md)

[<span data-ttu-id="c04af-142">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="c04af-142">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
