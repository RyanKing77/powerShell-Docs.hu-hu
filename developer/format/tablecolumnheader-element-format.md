---
title: TableColumnHeader elem (formátum) |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 49ff3062-6396-4aa8-919b-3fd3ac60899a
caps.latest.revision: 19
ms.openlocfilehash: 15f47c97ac5d55cb76e153af86672b3ffaf176c9
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56848628"
---
# <a name="tablecolumnheader-element-format"></a><span data-ttu-id="83448-102">TableColumnHeader elem (Formátum)</span><span class="sxs-lookup"><span data-stu-id="83448-102">TableColumnHeader Element (Format)</span></span>

<span data-ttu-id="83448-103">A címke, az oszlopok szélességét és a egy oszlop a tábla a címke zarovnání határozza meg.</span><span class="sxs-lookup"><span data-stu-id="83448-103">Defines the label, the width of the column, and the alignment of the label for a column of the table.</span></span>

<span data-ttu-id="83448-104">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem TableControl elem (formátum) TableHeaders elem TableControl (formátum) TableColumnHeader elemhez tartozó TableHeaders TableControl (formátum) a</span><span class="sxs-lookup"><span data-stu-id="83448-104">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) TableControl Element (Format) TableHeaders Element for TableControl (Format) TableColumnHeader Element for TableHeaders for TableControl (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="83448-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="83448-105">Syntax</span></span>

```xml
<TableColumnHeader>
  <Label>DisplayedLabel</Label>
  <Width>NumberOfCharacters</Width>
  <Alignment>Left, Right, or Centered</Alignment>
</TableColumnHeader>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="83448-106">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="83448-106">Attributes and Elements</span></span>

<span data-ttu-id="83448-107">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `TableColumnHeader` elemet.</span><span class="sxs-lookup"><span data-stu-id="83448-107">The following sections describe attributes, child elements, and the parent element of the `TableColumnHeader` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="83448-108">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="83448-108">Attributes</span></span>

<span data-ttu-id="83448-109">Nincs.</span><span class="sxs-lookup"><span data-stu-id="83448-109">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="83448-110">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="83448-110">Child Elements</span></span>

|<span data-ttu-id="83448-111">Elem</span><span class="sxs-lookup"><span data-stu-id="83448-111">Element</span></span>|<span data-ttu-id="83448-112">Leírás</span><span class="sxs-lookup"><span data-stu-id="83448-112">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="83448-113">Címke eleme TableColumnHeader a TableControl (formátum)</span><span class="sxs-lookup"><span data-stu-id="83448-113">Label Element For TableColumnHeader for TableControl (Format)</span></span>](./label-element-for-tablecolumnheader-for-tablecontrol-format.md)|<span data-ttu-id="83448-114">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="83448-114">Optional element.</span></span><br /><br /> <span data-ttu-id="83448-115">Határozza meg a címke az az oszlop tetején jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="83448-115">Defines the label that is displayed at the top of the column.</span></span> <span data-ttu-id="83448-116">Ha nincs címke van megadva, a tulajdonságot, amelynek az értéke megjelenik a sorok nevét használja.</span><span class="sxs-lookup"><span data-stu-id="83448-116">If no label is specified, the name of the property whose value is displayed in the rows is used.</span></span>|
|[<span data-ttu-id="83448-117">Szélesség eleme TableColumnHeader a TableControl (formátum)</span><span class="sxs-lookup"><span data-stu-id="83448-117">Width Element for TableColumnHeader for TableControl (Format)</span></span>](./width-element-for-tablecolumnheader-for-tablecontrol-format.md)|<span data-ttu-id="83448-118">Szükséges eleme.</span><span class="sxs-lookup"><span data-stu-id="83448-118">Required element.</span></span><br /><br /> <span data-ttu-id="83448-119">Adja meg az oszlop szélessége (a karakter).</span><span class="sxs-lookup"><span data-stu-id="83448-119">Specifies the width (in characters) of the column.</span></span>|
|[<span data-ttu-id="83448-120">Zarovnání eleme TableColumbnHeader a TableControl (formátum)</span><span class="sxs-lookup"><span data-stu-id="83448-120">Alignment Element for TableColumbnHeader for TableControl (Format)</span></span>](./alignment-element-for-tablecolumnheader-for-tablecontrol-format.md)|<span data-ttu-id="83448-121">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="83448-121">Optional element.</span></span><br /><br /> <span data-ttu-id="83448-122">Itt adhatja meg, hogyan jelenjen meg az oszlop a címkét.</span><span class="sxs-lookup"><span data-stu-id="83448-122">Specifies how the label of the column is displayed.</span></span> <span data-ttu-id="83448-123">Ha igazítás nélkül van megadva, a címke a bal oldali van igazítva.</span><span class="sxs-lookup"><span data-stu-id="83448-123">If no alignment is specified, the label is aligned on the left.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="83448-124">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="83448-124">Parent Elements</span></span>

|<span data-ttu-id="83448-125">Elem</span><span class="sxs-lookup"><span data-stu-id="83448-125">Element</span></span>|<span data-ttu-id="83448-126">Leírás</span><span class="sxs-lookup"><span data-stu-id="83448-126">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="83448-127">TableHeaders elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="83448-127">TableHeaders Element (Format)</span></span>](./tableheaders-element-format.md)|<span data-ttu-id="83448-128">Határozza meg az oszlopok számos táblázatos nézetre.</span><span class="sxs-lookup"><span data-stu-id="83448-128">Defines the columns of a table view.</span></span>|

## <a name="remarks"></a><span data-ttu-id="83448-129">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="83448-129">Remarks</span></span>

<span data-ttu-id="83448-130">Adja meg a tábla minden oszlopához fejlécét.</span><span class="sxs-lookup"><span data-stu-id="83448-130">Specify a header for each column of the table.</span></span> <span data-ttu-id="83448-131">Az oszlopok jelennek meg a sorrendet, amely a `TableColumnHeader` elemek vannak definiálva.</span><span class="sxs-lookup"><span data-stu-id="83448-131">The columns are displayed in the order in which the `TableColumnHeader` elements are defined.</span></span>

<span data-ttu-id="83448-132">Egy táblának rendelkeznie kell azonos számú `TableColumnHeader` az elemek `TableRowEntry` elemeket.</span><span class="sxs-lookup"><span data-stu-id="83448-132">A table must have the same number of `TableColumnHeader` elements as `TableRowEntry` elements.</span></span> <span data-ttu-id="83448-133">Az oszlop fejlécére határozza meg, hogyan jelenjen meg a tábla tetején lévő szöveg.</span><span class="sxs-lookup"><span data-stu-id="83448-133">The column header defines how the text at the top of the table is displayed.</span></span> <span data-ttu-id="83448-134">A sor bejegyzések határozza meg, hogy milyen adatok jelenjenek meg a tábla sorait.</span><span class="sxs-lookup"><span data-stu-id="83448-134">The row entries define what data is displayed in the rows of the table.</span></span>

<span data-ttu-id="83448-135">A táblázatos nézetre az összetevőivel kapcsolatos további információkért lásd: [táblázatos nézetre](./creating-a-table-view.md).</span><span class="sxs-lookup"><span data-stu-id="83448-135">For more information about the components of a table view, see [Table View](./creating-a-table-view.md).</span></span>

## <a name="example"></a><span data-ttu-id="83448-136">Példa</span><span class="sxs-lookup"><span data-stu-id="83448-136">Example</span></span>

<span data-ttu-id="83448-137">A következő példában két `TableColumnHeader` elemeket.</span><span class="sxs-lookup"><span data-stu-id="83448-137">The following example shows two `TableColumnHeader` elements.</span></span> <span data-ttu-id="83448-138">Az első elemét határozza meg egy olyan oszlop, amelynek címke "1. oszlop", 16 karakterből álló szélessége és amelynek címke van igazítva a bal oldali.</span><span class="sxs-lookup"><span data-stu-id="83448-138">The first element defines a column whose label is "Column 1", has a width of 16 characters, and whose label is aligned on the left.</span></span> <span data-ttu-id="83448-139">A második elem oszlop határozza meg, amelynek címke "2. oszlop", a 10 karakterből álló szélessége, és amelynek felirat az oszlopban közepén.</span><span class="sxs-lookup"><span data-stu-id="83448-139">The second element defines a column whose label is "Column 2", has a width of 10 characters, and whose label is centered in the column.</span></span>

```xml
<TableHeaders>
  <TableColumnHeader>
    <Label>Column 1</Label)
    <Width>16</Width>
    <Alignment>Left</Alignment>
  </TableColumnHeader>
    <TableColumnHeader>
    <Label>Column 2</Label)
    <Width>10</Width>
    <Alignment>Centered</Alignment>
  </TableColumnHeader>
</TableHeaders>
```

## <a name="see-also"></a><span data-ttu-id="83448-140">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="83448-140">See Also</span></span>

[<span data-ttu-id="83448-141">Zarovnání eleme TableColumnHeader a TableContrl (formátum)</span><span class="sxs-lookup"><span data-stu-id="83448-141">Alignment Element for TableColumnHeader for TableContrl (Format)</span></span>](./alignment-element-for-tablecolumnheader-for-tablecontrol-format.md)

[<span data-ttu-id="83448-142">Tábla nézet létrehozása</span><span class="sxs-lookup"><span data-stu-id="83448-142">Creating a Table View</span></span>](./creating-a-table-view.md)

[<span data-ttu-id="83448-143">Címke eleme TableColumnHeader a TableControl (formátum)</span><span class="sxs-lookup"><span data-stu-id="83448-143">Label Element for TableColumnHeader for TableControl (Format)</span></span>](./label-element-for-tablecolumnheader-for-tablecontrol-format.md)

[<span data-ttu-id="83448-144">TableHeaders eleme TableControl (formátum)</span><span class="sxs-lookup"><span data-stu-id="83448-144">TableHeaders Element for TableControl (Format)</span></span>](./tableheaders-element-format.md)

[<span data-ttu-id="83448-145">TableColumnHeader TableControl elemhez (formátum) esetén a szélesség</span><span class="sxs-lookup"><span data-stu-id="83448-145">Width for TableColumnHeader for TableControl Element (Format)</span></span>](./width-element-for-tablecolumnheader-for-tablecontrol-format.md)

[<span data-ttu-id="83448-146">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="83448-146">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
