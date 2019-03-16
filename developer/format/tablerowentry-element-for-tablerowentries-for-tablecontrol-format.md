---
title: TableControl (formátum) a TableRowEntries TableRowEntry eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 18d86af7-7ff9-4968-81be-2caa61937d49
caps.latest.revision: 10
ms.openlocfilehash: 946ffb3fe857503c02b9000238a86775969abbd6
ms.sourcegitcommit: caac7d098a448232304c9d6728e7340ec7517a71
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/15/2019
ms.locfileid: "58059845"
---
# <a name="tablerowentry-element-for-tablerowentries-for-tablecontrol-format"></a><span data-ttu-id="3bb0c-102">A TableControl (formátum) TableRowEntries TableRowEntry elem.</span><span class="sxs-lookup"><span data-stu-id="3bb0c-102">TableRowEntry Element for TableRowEntries for TableControl (Format)</span></span>

<span data-ttu-id="3bb0c-103">Határozza meg, amely egy sort a táblában megjelennek az adatok.</span><span class="sxs-lookup"><span data-stu-id="3bb0c-103">Defines the data that is displayed in a row of the table.</span></span>

<span data-ttu-id="3bb0c-104">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem TableControl elem (formátum) TableRowEntries elem TableControl (formátum) TableRowEntry elemhez tartozó TableRowEntries TableControl (formátum) a</span><span class="sxs-lookup"><span data-stu-id="3bb0c-104">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) TableControl Element (Format) TableRowEntries Element for TableControl (Format) TableRowEntry Element for TableRowEntries for TableControl (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="3bb0c-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="3bb0c-105">Syntax</span></span>

```xml
<TableRowEntry>
  <Wrap/>
  <EntrySelectedBy>...</EntrySelectedBy>
  <TableColumnItems>...</TableColumnItems>
</TableRowEntry>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="3bb0c-106">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="3bb0c-106">Attributes and Elements</span></span>

<span data-ttu-id="3bb0c-107">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és szülőelemét a `TableRowEntry` elemet.</span><span class="sxs-lookup"><span data-stu-id="3bb0c-107">The following sections describe attributes, child elements, and parent element of the `TableRowEntry` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="3bb0c-108">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="3bb0c-108">Attributes</span></span>

<span data-ttu-id="3bb0c-109">Nincs.</span><span class="sxs-lookup"><span data-stu-id="3bb0c-109">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="3bb0c-110">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="3bb0c-110">Child Elements</span></span>

|<span data-ttu-id="3bb0c-111">Elem</span><span class="sxs-lookup"><span data-stu-id="3bb0c-111">Element</span></span>|<span data-ttu-id="3bb0c-112">Leírás</span><span class="sxs-lookup"><span data-stu-id="3bb0c-112">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="3bb0c-113">A TableControl (formátum) TableRowEntry EntrySelectedBy elem.</span><span class="sxs-lookup"><span data-stu-id="3bb0c-113">EntrySelectedBy Element for TableRowEntry for TableControl (Format)</span></span>](./entryselectedby-element-for-tablerowentry-for-tablecontrol-format.md)|<span data-ttu-id="3bb0c-114">Szükséges eleme.</span><span class="sxs-lookup"><span data-stu-id="3bb0c-114">Required element.</span></span><br /><br /> <span data-ttu-id="3bb0c-115">Meghatározza az objektumok, amelyek tulajdonság értékét a sorban jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="3bb0c-115">Defines the objects whose property values are displayed in the row.</span></span>|
|[<span data-ttu-id="3bb0c-116">A TableControl (formátum) TableRowEntry TableColumnItems elem.</span><span class="sxs-lookup"><span data-stu-id="3bb0c-116">TableColumnItems Element for TableRowEntry for TableControl (Format)</span></span>](./tablecolumnitems-element-for-tablerowentry-for-tablecontrol-format.md)|<span data-ttu-id="3bb0c-117">Szükséges eleme.</span><span class="sxs-lookup"><span data-stu-id="3bb0c-117">Required element.</span></span><br /><br /> <span data-ttu-id="3bb0c-118">Határozza meg a Tulajdonságok vagy parancsfájlok, melynek értékei jelennek meg.</span><span class="sxs-lookup"><span data-stu-id="3bb0c-118">Defines the properties or scripts whose values are displayed.</span></span>|
|[<span data-ttu-id="3bb0c-119">Elem burkolása TableRowEntry számára a TableControl (formátum)</span><span class="sxs-lookup"><span data-stu-id="3bb0c-119">Wrap Element for TableRowEntry for TableControl (Format)</span></span>](./wrap-element-for-tablerowentry-for-tablecontrol-format.md)|<span data-ttu-id="3bb0c-120">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="3bb0c-120">Optional element.</span></span><br /><br /> <span data-ttu-id="3bb0c-121">Megadja a szöveg, amely meghaladja a Oszlopszélesség a következő sorban jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="3bb0c-121">Specifies that text that exceeds the column width is displayed on the next line.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="3bb0c-122">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="3bb0c-122">Parent Elements</span></span>

|<span data-ttu-id="3bb0c-123">Elem</span><span class="sxs-lookup"><span data-stu-id="3bb0c-123">Element</span></span>|<span data-ttu-id="3bb0c-124">Leírás</span><span class="sxs-lookup"><span data-stu-id="3bb0c-124">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="3bb0c-125">TableRowEntries eleme TableControl (formátum)</span><span class="sxs-lookup"><span data-stu-id="3bb0c-125">TableRowEntries Element for TableControl (Format)</span></span>](./tablerowentries-element-for-tablecontrol-format.md)|<span data-ttu-id="3bb0c-126">Határozza meg a tábla sorait.</span><span class="sxs-lookup"><span data-stu-id="3bb0c-126">Defines the rows of the table.</span></span>|

## <a name="remarks"></a><span data-ttu-id="3bb0c-127">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="3bb0c-127">Remarks</span></span>

<span data-ttu-id="3bb0c-128">Egy `TableColumnItems` elem és a egy `EntrySelectedBy` elemet meg kell adni.</span><span class="sxs-lookup"><span data-stu-id="3bb0c-128">One `TableColumnItems` element and one `EntrySelectedBy` element must be specified.</span></span>

<span data-ttu-id="3bb0c-129">A táblázatos nézetre az összetevőivel kapcsolatos további információkért lásd: [tábla nézetek létrehozásával](./creating-a-table-view.md).</span><span class="sxs-lookup"><span data-stu-id="3bb0c-129">For more information about the components of a table view, see [Creating a Table View](./creating-a-table-view.md).</span></span>

## <a name="example"></a><span data-ttu-id="3bb0c-130">Példa</span><span class="sxs-lookup"><span data-stu-id="3bb0c-130">Example</span></span>

<span data-ttu-id="3bb0c-131">A következő példa bemutatja egy `TableRowEntry` elem, amely meghatározza egy sort, amely két tulajdonságának értékét jeleníti meg a [System.Diagnostics.Process](/dotnet/api/System.Diagnostics.Process) objektum.</span><span class="sxs-lookup"><span data-stu-id="3bb0c-131">The following example shows a `TableRowEntry` element that defines a row that displays the values of two properties of the [System.Diagnostics.Process](/dotnet/api/System.Diagnostics.Process) object.</span></span>

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

## <a name="see-also"></a><span data-ttu-id="3bb0c-132">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="3bb0c-132">See Also</span></span>

[<span data-ttu-id="3bb0c-133">Tábla nézet létrehozása</span><span class="sxs-lookup"><span data-stu-id="3bb0c-133">Creating a Table View</span></span>](./creating-a-table-view.md)

[<span data-ttu-id="3bb0c-134">A TableControl (formátum) TableRowEntry EntrySelectedBy elem.</span><span class="sxs-lookup"><span data-stu-id="3bb0c-134">EntrySelectedBy Element for TableRowEntry for TableControl (Format)</span></span>](./entryselectedby-element-for-tablerowentry-for-tablecontrol-format.md)

[<span data-ttu-id="3bb0c-135">A TableControl (formátum) TableRowEntry TableColumnItems elem.</span><span class="sxs-lookup"><span data-stu-id="3bb0c-135">TableColumnItems Element for TableRowEntry for TableControl (Format)</span></span>](./tablecolumnitems-element-for-tablerowentry-for-tablecontrol-format.md)

[<span data-ttu-id="3bb0c-136">TableRowEntries eleme TableControl (formátum)</span><span class="sxs-lookup"><span data-stu-id="3bb0c-136">TableRowEntries Element for TableControl (Format)</span></span>](./tablerowentries-element-for-tablecontrol-format.md)

[<span data-ttu-id="3bb0c-137">Elem burkolása TableRowEntry számára a TableControl (formátum)</span><span class="sxs-lookup"><span data-stu-id="3bb0c-137">Wrap Element for TableRowEntry for TableControl (Format)</span></span>](./wrap-element-for-tablerowentry-for-tablecontrol-format.md)

[<span data-ttu-id="3bb0c-138">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="3bb0c-138">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
