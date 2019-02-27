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
ms.openlocfilehash: d93750f919c1075f173dc9ac70324cc003e36879
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56851141"
---
# <a name="tablerowentries-element-for-tablecontrol-format"></a><span data-ttu-id="19c15-102">A TableControl TableRowEntries eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="19c15-102">TableRowEntries Element for TableControl (Format)</span></span>

<span data-ttu-id="19c15-103">Határozza meg a tábla sorait.</span><span class="sxs-lookup"><span data-stu-id="19c15-103">Defines the rows of the table.</span></span>

<span data-ttu-id="19c15-104">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem TableControl elem (formátum) TableRowEntries eleme TableControl (formátum)</span><span class="sxs-lookup"><span data-stu-id="19c15-104">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) TableControl Element (Format) TableRowEntries Element for TableControl (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="19c15-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="19c15-105">Syntax</span></span>

```xml
<TableRowEntries>
  <TableRowEntry>...</TableRowEntry>
</TableRowEntries>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="19c15-106">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="19c15-106">Attributes and Elements</span></span>

<span data-ttu-id="19c15-107">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és szülőelemét a `TableRowEntries` elemet.</span><span class="sxs-lookup"><span data-stu-id="19c15-107">The following sections describe the attributes, child elements, and parent element of the `TableRowEntries` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="19c15-108">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="19c15-108">Attributes</span></span>

<span data-ttu-id="19c15-109">Nincs.</span><span class="sxs-lookup"><span data-stu-id="19c15-109">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="19c15-110">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="19c15-110">Child Elements</span></span>

|<span data-ttu-id="19c15-111">Elem</span><span class="sxs-lookup"><span data-stu-id="19c15-111">Element</span></span>|<span data-ttu-id="19c15-112">Leírás</span><span class="sxs-lookup"><span data-stu-id="19c15-112">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="19c15-113">A TableControl (formátum) TableRowEntries TableRowEntry elem.</span><span class="sxs-lookup"><span data-stu-id="19c15-113">TableRowEntry Element for TableRowEntries for TableControl (Format)</span></span>](./tablerowentry-element-for-tablerowentroes-for-tablecontrol-format.md)|<span data-ttu-id="19c15-114">Szükséges eleme.</span><span class="sxs-lookup"><span data-stu-id="19c15-114">Required element.</span></span><br /><br /> <span data-ttu-id="19c15-115">Határozza meg, amely egy sort a táblában megjelennek az adatok.</span><span class="sxs-lookup"><span data-stu-id="19c15-115">Defines the data that is displayed in a row of the table.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="19c15-116">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="19c15-116">Parent Elements</span></span>

|<span data-ttu-id="19c15-117">Elem</span><span class="sxs-lookup"><span data-stu-id="19c15-117">Element</span></span>|<span data-ttu-id="19c15-118">Leírás</span><span class="sxs-lookup"><span data-stu-id="19c15-118">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="19c15-119">TableControl elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="19c15-119">TableControl Element (Format)</span></span>](./tablecontrol-element-format.md)|<span data-ttu-id="19c15-120">Határozza meg a nézet táblázatos formában.</span><span class="sxs-lookup"><span data-stu-id="19c15-120">Defines a table format for a view.</span></span>|

## <a name="remarks"></a><span data-ttu-id="19c15-121">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="19c15-121">Remarks</span></span>

<span data-ttu-id="19c15-122">Meg kell adnia egy vagy több `TableRowEntry` elemei a táblázatos nézetre.</span><span class="sxs-lookup"><span data-stu-id="19c15-122">You must specify one or more `TableRowEntry` elements for the table view.</span></span> <span data-ttu-id="19c15-123">Nem maximális korlátozott számú `TableRowEntry` elemeket, amelyeket hozzáadhat se nem jelentős sorrendjét.</span><span class="sxs-lookup"><span data-stu-id="19c15-123">There is no maximum limit to the number of `TableRowEntry` elements that can be added nor is their order significant.</span></span>

<span data-ttu-id="19c15-124">A táblázatos nézetre az összetevőivel kapcsolatos további információkért lásd: [tábla nézetek létrehozásával](./creating-a-table-view.md).</span><span class="sxs-lookup"><span data-stu-id="19c15-124">For more information about the components of a table view, see [Creating a Table View](./creating-a-table-view.md).</span></span>

## <a name="example"></a><span data-ttu-id="19c15-125">Példa</span><span class="sxs-lookup"><span data-stu-id="19c15-125">Example</span></span>

<span data-ttu-id="19c15-126">A következő példa bemutatja egy `TableRowEntries` elem, amely meghatározza egy sort, amely két tulajdonságának értékét jeleníti meg a [System.Diagnostics.Process](/dotnet/api/System.Diagnostics.Process) objektum.</span><span class="sxs-lookup"><span data-stu-id="19c15-126">The following example shows a `TableRowEntries` element that defines a row that displays the values of two properties of the [System.Diagnostics.Process](/dotnet/api/System.Diagnostics.Process) object.</span></span>

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

## <a name="see-also"></a><span data-ttu-id="19c15-127">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="19c15-127">See Also</span></span>

[<span data-ttu-id="19c15-128">Tábla nézet létrehozása</span><span class="sxs-lookup"><span data-stu-id="19c15-128">Creating a Table View</span></span>](./creating-a-table-view.md)

[<span data-ttu-id="19c15-129">TableControl elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="19c15-129">TableControl Element (Format)</span></span>](./tablecontrol-element-format.md)

[<span data-ttu-id="19c15-130">TableRowEntry elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="19c15-130">TableRowEntry Element (Format)</span></span>](./tablerowentry-element-for-tablerowentroes-for-tablecontrol-format.md)

[<span data-ttu-id="19c15-131">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="19c15-131">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
