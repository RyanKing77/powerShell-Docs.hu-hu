---
title: TableHeaders elem (formátum) |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f9fa2b6f-b99a-42de-9779-44e9cb583f71
caps.latest.revision: 15
ms.openlocfilehash: bd44fcf4878c858afe81fb071ce72f627ac465dc
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56847424"
---
# <a name="tableheaders-element-format"></a><span data-ttu-id="374f6-102">TableHeaders elem (Formátum)</span><span class="sxs-lookup"><span data-stu-id="374f6-102">TableHeaders Element (Format)</span></span>

<span data-ttu-id="374f6-103">Meghatározza egy tábla oszlopait az fejlécek.</span><span class="sxs-lookup"><span data-stu-id="374f6-103">Defines the headers for the columns of a table.</span></span>

<span data-ttu-id="374f6-104">ViewDefinitions elem (formátum) nézetben (formátum) elem TableControl elem (formátum) TableHeaders elem TableControl (formátum)</span><span class="sxs-lookup"><span data-stu-id="374f6-104">ViewDefinitions Element (Format) View Element (Format) TableControl Element (Format) TableHeaders Element for TableControl (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="374f6-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="374f6-105">Syntax</span></span>

```xml
<TableHeaders>
  <TableColumnHeader>...</TableColumnHeader>
</TableHeaders>

```

## <a name="attributes-and-elements"></a><span data-ttu-id="374f6-106">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="374f6-106">Attributes and Elements</span></span>

<span data-ttu-id="374f6-107">A következő szakaszok ismertetik az attribútumokat, a gyermekelemek és a szülő elemei a `TableHeaders` elemet.</span><span class="sxs-lookup"><span data-stu-id="374f6-107">The following sections describe the attributes, child elements, and parent elements of the `TableHeaders` element.</span></span> <span data-ttu-id="374f6-108">A megjelenítendő objektum minden egyes tulajdonság gyermekelemet kell lennie.</span><span class="sxs-lookup"><span data-stu-id="374f6-108">There must be a child element for each property of the object that is to be displayed.</span></span> <span data-ttu-id="374f6-109">Az oszlop fejléc információk jelennek meg, hogy a gyermekelemek megadott sorrendben.</span><span class="sxs-lookup"><span data-stu-id="374f6-109">The column header information is displayed in the order that the child elements are specified.</span></span>

### <a name="attributes"></a><span data-ttu-id="374f6-110">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="374f6-110">Attributes</span></span>

<span data-ttu-id="374f6-111">Nincs.</span><span class="sxs-lookup"><span data-stu-id="374f6-111">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="374f6-112">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="374f6-112">Child Elements</span></span>

|<span data-ttu-id="374f6-113">Elem</span><span class="sxs-lookup"><span data-stu-id="374f6-113">Element</span></span>|<span data-ttu-id="374f6-114">Leírás</span><span class="sxs-lookup"><span data-stu-id="374f6-114">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="374f6-115">TableColumnHeader elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="374f6-115">TableColumnHeader Element (Format)</span></span>](./tablecolumnheader-element-format.md)|<span data-ttu-id="374f6-116">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="374f6-116">Optional element.</span></span><br /><br /> <span data-ttu-id="374f6-117">Határozza meg a címke, a szélesség és az adatokat egy oszlopában táblázatban igazítását.</span><span class="sxs-lookup"><span data-stu-id="374f6-117">Defines the label, the width, and the alignment of the data for a column of a table view.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="374f6-118">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="374f6-118">Parent Elements</span></span>

|<span data-ttu-id="374f6-119">Elem</span><span class="sxs-lookup"><span data-stu-id="374f6-119">Element</span></span>|<span data-ttu-id="374f6-120">Leírás</span><span class="sxs-lookup"><span data-stu-id="374f6-120">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="374f6-121">TableControl elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="374f6-121">TableControl Element (Format)</span></span>](./tablecontrol-element-format.md)|<span data-ttu-id="374f6-122">Határozza meg a nézet táblázatos formában.</span><span class="sxs-lookup"><span data-stu-id="374f6-122">Defines a table format for a view.</span></span>|

## <a name="remarks"></a><span data-ttu-id="374f6-123">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="374f6-123">Remarks</span></span>

<span data-ttu-id="374f6-124">A táblázatos nézetre az összetevőivel kapcsolatos további információkért lásd: [tábla nézetek létrehozásával](./creating-a-table-view.md).</span><span class="sxs-lookup"><span data-stu-id="374f6-124">For more information about the components of a table view, see [Creating a Table View](./creating-a-table-view.md).</span></span>

## <a name="example"></a><span data-ttu-id="374f6-125">Példa</span><span class="sxs-lookup"><span data-stu-id="374f6-125">Example</span></span>

<span data-ttu-id="374f6-126">Ez a példa bemutatja egy `TableHeaders` elem, amely meghatározza a két oszlopfejléceket.</span><span class="sxs-lookup"><span data-stu-id="374f6-126">This example shows a `TableHeaders` element that defines two column headers.</span></span>

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

## <a name="see-also"></a><span data-ttu-id="374f6-127">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="374f6-127">See Also</span></span>

[<span data-ttu-id="374f6-128">Tábla nézet létrehozása</span><span class="sxs-lookup"><span data-stu-id="374f6-128">Creating a Table View</span></span>](./creating-a-table-view.md)

[<span data-ttu-id="374f6-129">TableColumnHeader elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="374f6-129">TableColumnHeader Element (Format)</span></span>](./tablecolumnheader-element-format.md)

[<span data-ttu-id="374f6-130">TableControl elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="374f6-130">TableControl Element (Format)</span></span>](./tablecontrol-element-format.md)

[<span data-ttu-id="374f6-131">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="374f6-131">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
