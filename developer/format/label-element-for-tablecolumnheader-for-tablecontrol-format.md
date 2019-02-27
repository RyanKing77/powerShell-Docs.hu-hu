---
title: Címke elem a TableColumnHeader TableControl (formátum) a |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 7196f039-2f6a-41fd-b252-5b1623ebb9f9
caps.latest.revision: 11
ms.openlocfilehash: 59dfd40b95d5088a711eb89cf101eb31a4b159f5
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56846871"
---
# <a name="label-element-for-tablecolumnheader-for-tablecontrol-format"></a><span data-ttu-id="58d3c-102">A TableControl TableColumnHeader elemének Címke eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="58d3c-102">Label Element for TableColumnHeader for TableControl (Format)</span></span>

<span data-ttu-id="58d3c-103">Határozza meg a címke az oszlop tetején jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="58d3c-103">Defines the label that is displayed at the top of a column.</span></span> <span data-ttu-id="58d3c-104">Ez az elem szolgál a táblázatos nézetre meghatározásakor.</span><span class="sxs-lookup"><span data-stu-id="58d3c-104">This element is used when defining a table view.</span></span>

<span data-ttu-id="58d3c-105">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézet elem (formátum) TableControl elem (formátum) TableHeaders elem TableControl (formátum) TableColumnHeader elem a TableHeaders TableControl (formátum) címke elem számára TableColumnHeader a TablControl (formátum)</span><span class="sxs-lookup"><span data-stu-id="58d3c-105">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) TableControl Element (Format) TableHeaders Element for TableControl (Format) TableColumnHeader Element for TableHeaders for TableControl (Format) Label Element  for TableColumnHeader for TablControl (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="58d3c-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="58d3c-106">Syntax</span></span>

```xml
<Label>DisplayedLabel</Label>

```

## <a name="attributes-and-elements"></a><span data-ttu-id="58d3c-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="58d3c-107">Attributes and Elements</span></span>

<span data-ttu-id="58d3c-108">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `Label` elemet.</span><span class="sxs-lookup"><span data-stu-id="58d3c-108">The following sections describe the attributes, child elements, and the parent element of the `Label` element.</span></span> <span data-ttu-id="58d3c-109">Csak egy címke minden oszlophoz engedélyezett.</span><span class="sxs-lookup"><span data-stu-id="58d3c-109">Only one label is allowed for each column.</span></span>

### <a name="attributes"></a><span data-ttu-id="58d3c-110">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="58d3c-110">Attributes</span></span>

<span data-ttu-id="58d3c-111">Nincs.</span><span class="sxs-lookup"><span data-stu-id="58d3c-111">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="58d3c-112">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="58d3c-112">Child Elements</span></span>

<span data-ttu-id="58d3c-113">Nincs.</span><span class="sxs-lookup"><span data-stu-id="58d3c-113">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="58d3c-114">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="58d3c-114">Parent Elements</span></span>

|<span data-ttu-id="58d3c-115">Elem</span><span class="sxs-lookup"><span data-stu-id="58d3c-115">Element</span></span>|<span data-ttu-id="58d3c-116">Leírás</span><span class="sxs-lookup"><span data-stu-id="58d3c-116">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="58d3c-117">A TableControl (formátum) TableHeaders TableColumnHeader elem.</span><span class="sxs-lookup"><span data-stu-id="58d3c-117">TableColumnHeader Element for TableHeaders for TableControl  (Format)</span></span>](./tablecolumnheader-element-format.md)|<span data-ttu-id="58d3c-118">Egy címke, a szélesség és az adatok egy oszlop a tábla zarovnání határozza meg.</span><span class="sxs-lookup"><span data-stu-id="58d3c-118">Defines a label, the width, and the alignment of the data for a column of the table.</span></span>|

## <a name="text-value"></a><span data-ttu-id="58d3c-119">Szöveges érték</span><span class="sxs-lookup"><span data-stu-id="58d3c-119">Text Value</span></span>

<span data-ttu-id="58d3c-120">Adja meg az oszlop a tábla tetején megjelenő szöveg.</span><span class="sxs-lookup"><span data-stu-id="58d3c-120">Specify the text that is displayed at the top of the column of the table.</span></span> <span data-ttu-id="58d3c-121">Nem áll a korlátozott karakter oszlop címkére.</span><span class="sxs-lookup"><span data-stu-id="58d3c-121">There are no restricted characters for the column label.</span></span>

## <a name="remarks"></a><span data-ttu-id="58d3c-122">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="58d3c-122">Remarks</span></span>

<span data-ttu-id="58d3c-123">Ha nincs címke van megadva, a tulajdonságot, amelynek az értéke megjelenik a sorok nevét használja.</span><span class="sxs-lookup"><span data-stu-id="58d3c-123">If no label is specified, the name of the property whose value is displayed in the rows is used.</span></span>

<span data-ttu-id="58d3c-124">A táblázatos nézetre az összetevőivel kapcsolatos további információkért lásd: [tábla nézetek létrehozásával](./creating-a-table-view.md).</span><span class="sxs-lookup"><span data-stu-id="58d3c-124">For more information about the components of a table view, see [Creating a Table View](./creating-a-table-view.md).</span></span>

## <a name="example"></a><span data-ttu-id="58d3c-125">Példa</span><span class="sxs-lookup"><span data-stu-id="58d3c-125">Example</span></span>

<span data-ttu-id="58d3c-126">Ez a példa bemutatja egy `TableColumnHeader` elem, amelynek címkét az "1. oszlop".</span><span class="sxs-lookup"><span data-stu-id="58d3c-126">This example shows a `TableColumnHeader` element whose label is "Column 1".</span></span>

```xml
<TableColumnHeader>
  <Label>Column 1</Label)
  <Width>16</Width>
  <Alignment>Left</Alignment>
</TableColumnHeader>
```

## <a name="see-also"></a><span data-ttu-id="58d3c-127">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="58d3c-127">See Also</span></span>

[<span data-ttu-id="58d3c-128">Tábla nézet létrehozása</span><span class="sxs-lookup"><span data-stu-id="58d3c-128">Creating a Table View</span></span>](./creating-a-table-view.md)

[<span data-ttu-id="58d3c-129">TableColumnHeader elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="58d3c-129">TableColumnHeader Element (Format)</span></span>](./tablecolumnheader-element-format.md)

[<span data-ttu-id="58d3c-130">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="58d3c-130">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
