---
title: TableControl (formátum) a TableRowEntry TableColumnItems eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: d43684ce-7c3d-4d14-8dbd-061c111ee805
caps.latest.revision: 12
ms.openlocfilehash: d05437aaa9652e7f81d0854d1a746acffe145699
ms.sourcegitcommit: caac7d098a448232304c9d6728e7340ec7517a71
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/16/2019
ms.locfileid: "58056906"
---
# <a name="tablecolumnitems-element-for-tablerowentry-for-tablecontrol-format"></a><span data-ttu-id="318eb-102">A TableControl TableRowEntry elemének TableColumnItems eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="318eb-102">TableColumnItems Element for TableRowEntry for TableControl (Format)</span></span>

<span data-ttu-id="318eb-103">A Tulajdonságok vagy parancsfájlok, melynek értékei jelennek meg a sor határoz meg.</span><span class="sxs-lookup"><span data-stu-id="318eb-103">Defines the properties or scripts whose values are displayed in a row.</span></span>

<span data-ttu-id="318eb-104">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem TableControl elem (formátum) TableRowEntries elem TableControl (formátum) TableRowEntry elemhez tartozó TableRowEntries TableControl (formátum) a A TableControl (formátum) TableControlEntry TableColumnItems elem.</span><span class="sxs-lookup"><span data-stu-id="318eb-104">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) TableControl Element (Format) TableRowEntries Element for TableControl (Format) TableRowEntry Element for TableRowEntries for TableControl (Format) TableColumnItems Element for TableControlEntry for TableControl (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="318eb-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="318eb-105">Syntax</span></span>

```xml
TableColumnItems>
  <TableColumnItem>...</TableColumnItem>
</TableColumnItems>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="318eb-106">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="318eb-106">Attributes and Elements</span></span>

<span data-ttu-id="318eb-107">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és szülőelemét a `TableColumnItems` elemet.</span><span class="sxs-lookup"><span data-stu-id="318eb-107">The following sections describe the attributes, child elements, and parent element of the `TableColumnItems` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="318eb-108">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="318eb-108">Attributes</span></span>

<span data-ttu-id="318eb-109">Nincs.</span><span class="sxs-lookup"><span data-stu-id="318eb-109">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="318eb-110">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="318eb-110">Child Elements</span></span>

|<span data-ttu-id="318eb-111">Elem</span><span class="sxs-lookup"><span data-stu-id="318eb-111">Element</span></span>|<span data-ttu-id="318eb-112">Leírás</span><span class="sxs-lookup"><span data-stu-id="318eb-112">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="318eb-113">A TableControl (formátum) TableColumnItems TableColumnItem elem.</span><span class="sxs-lookup"><span data-stu-id="318eb-113">TableColumnItem Element for TableColumnItems for TableControl (Format)</span></span>](./tablecolumnitem-element-for-tablecolumnitems-for-tablecontrol-format.md)|<span data-ttu-id="318eb-114">Szükséges eleme.</span><span class="sxs-lookup"><span data-stu-id="318eb-114">Required element.</span></span><br /><br /> <span data-ttu-id="318eb-115">Határozza meg, tulajdonság vagy parancsfájl, amelynek értéke megjelenik a sor egy oszlopban.</span><span class="sxs-lookup"><span data-stu-id="318eb-115">Defines the property or script whose value is displayed in a column of the row.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="318eb-116">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="318eb-116">Parent Elements</span></span>

|<span data-ttu-id="318eb-117">Elem</span><span class="sxs-lookup"><span data-stu-id="318eb-117">Element</span></span>|<span data-ttu-id="318eb-118">Leírás</span><span class="sxs-lookup"><span data-stu-id="318eb-118">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="318eb-119">A TableControl (formátum) TableRowEntries TableRowEntry elem.</span><span class="sxs-lookup"><span data-stu-id="318eb-119">TableRowEntry Element for TableRowEntries for TableControl (Format)</span></span>](./tablerowentry-element-for-tablerowentries-for-tablecontrol-format.md)|<span data-ttu-id="318eb-120">Határozza meg, amely egy sort a táblában megjelennek az adatok.</span><span class="sxs-lookup"><span data-stu-id="318eb-120">Defines the data that is displayed in a row of the table.</span></span>|

## <a name="remarks"></a><span data-ttu-id="318eb-121">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="318eb-121">Remarks</span></span>

<span data-ttu-id="318eb-122">A `TableColumnItem` elem megadása kötelező a sor minden oszlophoz.</span><span class="sxs-lookup"><span data-stu-id="318eb-122">A `TableColumnItem` element is required for each column of the row.</span></span> <span data-ttu-id="318eb-123">Az első bejegyzés jelenik meg az első oszlopban a második bejegyzés a második oszlopban, és így tovább.</span><span class="sxs-lookup"><span data-stu-id="318eb-123">The first entry is displayed in first column, the second entry in the second column, and so on.</span></span>

<span data-ttu-id="318eb-124">A táblázatos nézetre az összetevőivel kapcsolatos további információkért lásd: [tábla nézetek létrehozásával](./creating-a-table-view.md).</span><span class="sxs-lookup"><span data-stu-id="318eb-124">For more information about the components of a table view, see [Creating a Table View](./creating-a-table-view.md).</span></span>

## <a name="example"></a><span data-ttu-id="318eb-125">Példa</span><span class="sxs-lookup"><span data-stu-id="318eb-125">Example</span></span>

<span data-ttu-id="318eb-126">A következő példa bemutatja egy `TableColumnItems` elem, amely három tulajdonságainak meghatározása a [System.Diagnostics.Process](/dotnet/api/System.Diagnostics.Process) objektum.</span><span class="sxs-lookup"><span data-stu-id="318eb-126">The following example shows a `TableColumnItems` element that defines three properties of the [System.Diagnostics.Process](/dotnet/api/System.Diagnostics.Process) object.</span></span>

```xml
<TableColumnItems>
  <TableColumnItem>
    <PropertyName>Status</PropertyName>
  </TableColumnItem>
  <TableColumnItem>
    <PropertyName>Name</PropertyName>
  </TableColumnItem>
  <TableColumnItem>
    <PropertyName>DisplayName</PropertyName>
  </TableColumnItem>
</TableColumnItems>

```

## <a name="see-also"></a><span data-ttu-id="318eb-127">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="318eb-127">See Also</span></span>

[<span data-ttu-id="318eb-128">Tábla nézet létrehozása</span><span class="sxs-lookup"><span data-stu-id="318eb-128">Creating a Table View</span></span>](./creating-a-table-view.md)

[<span data-ttu-id="318eb-129">TableColumnItem elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="318eb-129">TableColumnItem Element (Format)</span></span>](./tablecolumnitem-element-for-tablecolumnitems-for-tablecontrol-format.md)

[<span data-ttu-id="318eb-130">TableRowEntry elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="318eb-130">TableRowEntry Element (Format)</span></span>](./tablerowentry-element-for-tablerowentries-for-tablecontrol-format.md)

[<span data-ttu-id="318eb-131">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="318eb-131">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
