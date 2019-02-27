---
title: TableControl (formátum) a TableRowEntroes TableRowEntry eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 18d86af7-7ff9-4968-81be-2caa61937d49
caps.latest.revision: 10
ms.openlocfilehash: 001d46debde61f928c338b2f68112fb201f96216
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56845121"
---
# <a name="tablerowentry-element-for-tablerowentroes-for-tablecontrol-format"></a><span data-ttu-id="aeff0-102">A TableControl elemhez tartozó TableRowEntries TableRowEntry eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="aeff0-102">TableRowEntry Element for TableRowEntroes for TableControl (Format)</span></span>

<span data-ttu-id="aeff0-103">Határozza meg, amely egy sort a táblában megjelennek az adatok.</span><span class="sxs-lookup"><span data-stu-id="aeff0-103">Defines the data that is displayed in a row of the table.</span></span>

<span data-ttu-id="aeff0-104">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem TableControl elem (formátum) TableRowEntries elem TableControl (formátum) TableRowEntry elemhez tartozó TableRowEntries TableControl (formátum) a</span><span class="sxs-lookup"><span data-stu-id="aeff0-104">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) TableControl Element (Format) TableRowEntries Element for TableControl (Format) TableRowEntry Element for TableRowEntries for TableControl (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="aeff0-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="aeff0-105">Syntax</span></span>

```xml
<TableRowEntry>
  <Wrap/>
  <EntrySelectedBy>...</EntrySelectedBy>
  <TableColumnItems>...</TableColumnItems>
</TableRowEntry>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="aeff0-106">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="aeff0-106">Attributes and Elements</span></span>

<span data-ttu-id="aeff0-107">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és szülőelemét a `TableRowEntry` elemet.</span><span class="sxs-lookup"><span data-stu-id="aeff0-107">The following sections describe attributes, child elements, and parent element of the `TableRowEntry` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="aeff0-108">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="aeff0-108">Attributes</span></span>

<span data-ttu-id="aeff0-109">Nincs.</span><span class="sxs-lookup"><span data-stu-id="aeff0-109">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="aeff0-110">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="aeff0-110">Child Elements</span></span>

|<span data-ttu-id="aeff0-111">Elem</span><span class="sxs-lookup"><span data-stu-id="aeff0-111">Element</span></span>|<span data-ttu-id="aeff0-112">Leírás</span><span class="sxs-lookup"><span data-stu-id="aeff0-112">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="aeff0-113">A TableControl (formátum) TableRowEntry EntrySelectedBy elem.</span><span class="sxs-lookup"><span data-stu-id="aeff0-113">EntrySelectedBy Element for TableRowEntry for TableControl (Format)</span></span>](./entryselectedby-element-for-tablerowentry-for-tablecontrol-format.md)|<span data-ttu-id="aeff0-114">Szükséges eleme.</span><span class="sxs-lookup"><span data-stu-id="aeff0-114">Required element.</span></span><br /><br /> <span data-ttu-id="aeff0-115">Meghatározza az objektumok, amelyek tulajdonság értékét a sorban jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="aeff0-115">Defines the objects whose property values are displayed in the row.</span></span>|
|[<span data-ttu-id="aeff0-116">A TableControl (formátum) TableRowEntry TableColumnItems elem.</span><span class="sxs-lookup"><span data-stu-id="aeff0-116">TableColumnItems Element for TableRowEntry for TableControl (Format)</span></span>](./tablecolumnitems-element-for-tablerowentry-for-tablecontrol-format.md)|<span data-ttu-id="aeff0-117">Szükséges eleme.</span><span class="sxs-lookup"><span data-stu-id="aeff0-117">Required element.</span></span><br /><br /> <span data-ttu-id="aeff0-118">Határozza meg a Tulajdonságok vagy parancsfájlok, melynek értékei jelennek meg.</span><span class="sxs-lookup"><span data-stu-id="aeff0-118">Defines the properties or scripts whose values are displayed.</span></span>|
|[<span data-ttu-id="aeff0-119">Elem burkolása TableRowEntry számára a TableCntrol (formátum)</span><span class="sxs-lookup"><span data-stu-id="aeff0-119">Wrap Element for TableRowEntry for TableCntrol (Format)</span></span>](./wrap-element-for-tablerowentry-for-tablecontrl-format.md)|<span data-ttu-id="aeff0-120">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="aeff0-120">Optional element.</span></span><br /><br /> <span data-ttu-id="aeff0-121">Megadja a szöveg, amely meghaladja a Oszlopszélesség a következő sorban jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="aeff0-121">Specifies that text that exceeds the column width is displayed on the next line.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="aeff0-122">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="aeff0-122">Parent Elements</span></span>

|<span data-ttu-id="aeff0-123">Elem</span><span class="sxs-lookup"><span data-stu-id="aeff0-123">Element</span></span>|<span data-ttu-id="aeff0-124">Leírás</span><span class="sxs-lookup"><span data-stu-id="aeff0-124">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="aeff0-125">TableRowEntries eleme TableControl (formátum)</span><span class="sxs-lookup"><span data-stu-id="aeff0-125">TableRowEntries Element for TableControl (Format)</span></span>](./tablerowentries-element-for-tablecontrol-format.md)|<span data-ttu-id="aeff0-126">Határozza meg a tábla sorait.</span><span class="sxs-lookup"><span data-stu-id="aeff0-126">Defines the rows of the table.</span></span>|

## <a name="remarks"></a><span data-ttu-id="aeff0-127">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="aeff0-127">Remarks</span></span>

<span data-ttu-id="aeff0-128">Egy `TableColumnItems` elem és a egy `EntrySelectedBy` elemet meg kell adni.</span><span class="sxs-lookup"><span data-stu-id="aeff0-128">One `TableColumnItems` element and one `EntrySelectedBy` element must be specified.</span></span>

<span data-ttu-id="aeff0-129">A táblázatos nézetre az összetevőivel kapcsolatos további információkért lásd: [tábla nézetek létrehozásával](./creating-a-table-view.md).</span><span class="sxs-lookup"><span data-stu-id="aeff0-129">For more information about the components of a table view, see [Creating a Table View](./creating-a-table-view.md).</span></span>

## <a name="example"></a><span data-ttu-id="aeff0-130">Példa</span><span class="sxs-lookup"><span data-stu-id="aeff0-130">Example</span></span>

<span data-ttu-id="aeff0-131">A következő példa bemutatja egy `TableRowEntry` elem, amely meghatározza egy sort, amely két tulajdonságának értékét jeleníti meg a [System.Diagnostics.Process](/dotnet/api/System.Diagnostics.Process) objektum.</span><span class="sxs-lookup"><span data-stu-id="aeff0-131">The following example shows a `TableRowEntry` element that defines a row that displays the values of two properties of the [System.Diagnostics.Process](/dotnet/api/System.Diagnostics.Process) object.</span></span>

```xml
<TableRowEntry>
  <EntrySelectedBy>
    <TypeName>System.Diagnostics.Process</TypeName>
  </EntrySelectedBy>
  <TableColumnItems>
    <TableColumnItem>
      <PropertyName> Property for first column</PropertyName>
    </TableColumnItem>
    <TableColumnItem>
      <PropertyName> Property for second column</PropertyName>
    </TableColumnItem>
  </TableColumnItems>
</TableRowEntry>
```

## <a name="see-also"></a><span data-ttu-id="aeff0-132">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="aeff0-132">See Also</span></span>

[<span data-ttu-id="aeff0-133">Tábla nézet létrehozása</span><span class="sxs-lookup"><span data-stu-id="aeff0-133">Creating a Table View</span></span>](./creating-a-table-view.md)

[<span data-ttu-id="aeff0-134">A TableControl (formátum) TableRowEntry EntrySelectedBy elem.</span><span class="sxs-lookup"><span data-stu-id="aeff0-134">EntrySelectedBy Element for TableRowEntry for TableControl (Format)</span></span>](./entryselectedby-element-for-tablerowentry-for-tablecontrol-format.md)

[<span data-ttu-id="aeff0-135">A TableControl (formátum) TableRowEntry TableColumnItems elem.</span><span class="sxs-lookup"><span data-stu-id="aeff0-135">TableColumnItems Element for TableRowEntry for TableControl (Format)</span></span>](./tablecolumnitems-element-for-tablerowentry-for-tablecontrol-format.md)

[<span data-ttu-id="aeff0-136">TableRowEntries eleme TableControl (formátum)</span><span class="sxs-lookup"><span data-stu-id="aeff0-136">TableRowEntries Element for TableControl (Format)</span></span>](./tablerowentries-element-for-tablecontrol-format.md)

[<span data-ttu-id="aeff0-137">A TableControl (formátum) TableRowEntries TableRowEntry elem.</span><span class="sxs-lookup"><span data-stu-id="aeff0-137">TableRowEntry Element for TableRowEntries for TableControl (Format)</span></span>](./tablerowentry-element-for-tablerowentroes-for-tablecontrol-format.md)

[<span data-ttu-id="aeff0-138">Elem burkolása TableRowEntry számára a TableCntrol (formátum)</span><span class="sxs-lookup"><span data-stu-id="aeff0-138">Wrap Element for TableRowEntry for TableCntrol (Format)</span></span>](./wrap-element-for-tablerowentry-for-tablecontrl-format.md)

[<span data-ttu-id="aeff0-139">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="aeff0-139">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
