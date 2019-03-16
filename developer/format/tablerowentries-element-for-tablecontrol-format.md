---
title: (Formátum) TableControl TableRowEntries eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: d10b68ca-256c-4c58-b503-73f7777b39ae
caps.latest.revision: 15
ms.openlocfilehash: 88de19be02de4933f892e02093403a82ccdd5788
ms.sourcegitcommit: caac7d098a448232304c9d6728e7340ec7517a71
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/16/2019
ms.locfileid: "58055733"
---
# <a name="tablerowentries-element-for-tablecontrol-format"></a><span data-ttu-id="68fad-102">A TableControl TableRowEntries eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="68fad-102">TableRowEntries Element for TableControl (Format)</span></span>

<span data-ttu-id="68fad-103">Határozza meg a tábla sorait.</span><span class="sxs-lookup"><span data-stu-id="68fad-103">Defines the rows of the table.</span></span>

<span data-ttu-id="68fad-104">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem TableControl elem (formátum) TableRowEntries eleme TableControl (formátum)</span><span class="sxs-lookup"><span data-stu-id="68fad-104">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) TableControl Element (Format) TableRowEntries Element for TableControl (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="68fad-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="68fad-105">Syntax</span></span>

```xml
<TableRowEntries>
  <TableRowEntry>...</TableRowEntry>
</TableRowEntries>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="68fad-106">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="68fad-106">Attributes and Elements</span></span>

<span data-ttu-id="68fad-107">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és szülőelemét a `TableRowEntries` elemet.</span><span class="sxs-lookup"><span data-stu-id="68fad-107">The following sections describe the attributes, child elements, and parent element of the `TableRowEntries` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="68fad-108">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="68fad-108">Attributes</span></span>

<span data-ttu-id="68fad-109">Nincs.</span><span class="sxs-lookup"><span data-stu-id="68fad-109">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="68fad-110">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="68fad-110">Child Elements</span></span>

|<span data-ttu-id="68fad-111">Elem</span><span class="sxs-lookup"><span data-stu-id="68fad-111">Element</span></span>|<span data-ttu-id="68fad-112">Leírás</span><span class="sxs-lookup"><span data-stu-id="68fad-112">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="68fad-113">A TableControl (formátum) TableRowEntries TableRowEntry elem.</span><span class="sxs-lookup"><span data-stu-id="68fad-113">TableRowEntry Element for TableRowEntries for TableControl (Format)</span></span>](./tablerowentry-element-for-tablerowentries-for-tablecontrol-format.md)|<span data-ttu-id="68fad-114">Szükséges eleme.</span><span class="sxs-lookup"><span data-stu-id="68fad-114">Required element.</span></span><br /><br /> <span data-ttu-id="68fad-115">Határozza meg, amely egy sort a táblában megjelennek az adatok.</span><span class="sxs-lookup"><span data-stu-id="68fad-115">Defines the data that is displayed in a row of the table.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="68fad-116">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="68fad-116">Parent Elements</span></span>

|<span data-ttu-id="68fad-117">Elem</span><span class="sxs-lookup"><span data-stu-id="68fad-117">Element</span></span>|<span data-ttu-id="68fad-118">Leírás</span><span class="sxs-lookup"><span data-stu-id="68fad-118">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="68fad-119">TableControl elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="68fad-119">TableControl Element (Format)</span></span>](./tablecontrol-element-format.md)|<span data-ttu-id="68fad-120">Határozza meg a nézet táblázatos formában.</span><span class="sxs-lookup"><span data-stu-id="68fad-120">Defines a table format for a view.</span></span>|

## <a name="remarks"></a><span data-ttu-id="68fad-121">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="68fad-121">Remarks</span></span>

<span data-ttu-id="68fad-122">Meg kell adnia egy vagy több `TableRowEntry` elemei a táblázatos nézetre.</span><span class="sxs-lookup"><span data-stu-id="68fad-122">You must specify one or more `TableRowEntry` elements for the table view.</span></span> <span data-ttu-id="68fad-123">Nem maximális korlátozott számú `TableRowEntry` elemeket, amelyeket hozzáadhat se nem jelentős sorrendjét.</span><span class="sxs-lookup"><span data-stu-id="68fad-123">There is no maximum limit to the number of `TableRowEntry` elements that can be added nor is their order significant.</span></span>

<span data-ttu-id="68fad-124">A táblázatos nézetre az összetevőivel kapcsolatos további információkért lásd: [tábla nézetek létrehozásával](./creating-a-table-view.md).</span><span class="sxs-lookup"><span data-stu-id="68fad-124">For more information about the components of a table view, see [Creating a Table View](./creating-a-table-view.md).</span></span>

## <a name="example"></a><span data-ttu-id="68fad-125">Példa</span><span class="sxs-lookup"><span data-stu-id="68fad-125">Example</span></span>

<span data-ttu-id="68fad-126">A következő példa bemutatja egy `TableRowEntries` elem, amely meghatározza egy sort, amely két tulajdonságának értékét jeleníti meg a [System.Diagnostics.Process](/dotnet/api/System.Diagnostics.Process) objektum.</span><span class="sxs-lookup"><span data-stu-id="68fad-126">The following example shows a `TableRowEntries` element that defines a row that displays the values of two properties of the [System.Diagnostics.Process](/dotnet/api/System.Diagnostics.Process) object.</span></span>

```xml
<TableRowEntries>
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
</TableRowEntries>

```

## <a name="see-also"></a><span data-ttu-id="68fad-127">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="68fad-127">See Also</span></span>

[<span data-ttu-id="68fad-128">Tábla nézet létrehozása</span><span class="sxs-lookup"><span data-stu-id="68fad-128">Creating a Table View</span></span>](./creating-a-table-view.md)

[<span data-ttu-id="68fad-129">TableControl elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="68fad-129">TableControl Element (Format)</span></span>](./tablecontrol-element-format.md)

[<span data-ttu-id="68fad-130">TableRowEntry elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="68fad-130">TableRowEntry Element (Format)</span></span>](./tablerowentry-element-for-tablerowentries-for-tablecontrol-format.md)

[<span data-ttu-id="68fad-131">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="68fad-131">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
