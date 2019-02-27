---
title: Zarovnání eleme TableColumnItem TableControl (formátum) a |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: b07a53df-64f1-49b0-8cea-c993b3f1f76b
caps.latest.revision: 10
ms.openlocfilehash: 1bc936b94ee6fd6239e9e3c4afcdb8f14fbe36eb
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56848355"
---
# <a name="alignment-element-for-tablecolumnitem-for-tablecontrol-format"></a><span data-ttu-id="d73d7-102">A TableControl TableColumnItem elemének igazítási eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="d73d7-102">Alignment Element for TableColumnItem for TableControl (Format)</span></span>

<span data-ttu-id="d73d7-103">Határozza meg, hogyan jelenjen meg a sor egy oszlopban lévő adatokat.</span><span class="sxs-lookup"><span data-stu-id="d73d7-103">Defines how the data in a column of the row is displayed.</span></span>

<span data-ttu-id="d73d7-104">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem TableControl elem (formátum) TableRowEntries elem (formátum) TableRowEntry elem (formátum) TableColumnItems elem (formátum) TableColumnItem elem (formátum) Zarovnání eleme TableColumnItem (formátum)</span><span class="sxs-lookup"><span data-stu-id="d73d7-104">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) TableControl Element (Format) TableRowEntries Element (Format) TableRowEntry Element (Format) TableColumnItems Element (Format) TableColumnItem Element (Format) Alignment Element for TableColumnItem (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="d73d7-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="d73d7-105">Syntax</span></span>

```xml
<Alignment>AlignmentType</Alignment>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="d73d7-106">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="d73d7-106">Attributes and Elements</span></span>

<span data-ttu-id="d73d7-107">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és szülőelemét a `Alignment` elemet.</span><span class="sxs-lookup"><span data-stu-id="d73d7-107">The following sections describe the attributes, child elements, and parent element of the `Alignment` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="d73d7-108">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="d73d7-108">Attributes</span></span>

<span data-ttu-id="d73d7-109">Nincs.</span><span class="sxs-lookup"><span data-stu-id="d73d7-109">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="d73d7-110">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="d73d7-110">Child Elements</span></span>

<span data-ttu-id="d73d7-111">Nincs.</span><span class="sxs-lookup"><span data-stu-id="d73d7-111">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="d73d7-112">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="d73d7-112">Parent Elements</span></span>

|<span data-ttu-id="d73d7-113">Elem</span><span class="sxs-lookup"><span data-stu-id="d73d7-113">Element</span></span>|<span data-ttu-id="d73d7-114">Leírás</span><span class="sxs-lookup"><span data-stu-id="d73d7-114">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="d73d7-115">TableColumnItem elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="d73d7-115">TableColumnItem Element (Format)</span></span>](./tablecolumnitem-element-for-tablecolumnitems-for-tablecontrol-format.md)|<span data-ttu-id="d73d7-116">Egy címke, a szélesség és az adatok egy oszlop a tábla zarovnání határozza meg.</span><span class="sxs-lookup"><span data-stu-id="d73d7-116">Defines a label, the width, and the alignment of the data for a column of the table.</span></span>|

## <a name="text-value"></a><span data-ttu-id="d73d7-117">Szöveges érték</span><span class="sxs-lookup"><span data-stu-id="d73d7-117">Text Value</span></span>

<span data-ttu-id="d73d7-118">Adja meg a következő értékek egyikét.</span><span class="sxs-lookup"><span data-stu-id="d73d7-118">Specify one of the following values.</span></span> <span data-ttu-id="d73d7-119">(Ezek az értékek nem számítanak különbözőnek.)</span><span class="sxs-lookup"><span data-stu-id="d73d7-119">(These values are not case-sensitive.)</span></span>

<span data-ttu-id="d73d7-120">Bal oldali műszakok az oszlopot a bal oldalon megjelenő adatokat.</span><span class="sxs-lookup"><span data-stu-id="d73d7-120">Left Shifts the data displayed in the column to the left.</span></span> <span data-ttu-id="d73d7-121">(Ez az alapértelmezés szerint ha ez az elem nincs megadva.)</span><span class="sxs-lookup"><span data-stu-id="d73d7-121">(This is the default if this element is not specified.)</span></span>

<span data-ttu-id="d73d7-122">Jobb oldali műszakok az oszlopot a jobb oldalon megjelenő adatokat.</span><span class="sxs-lookup"><span data-stu-id="d73d7-122">Right Shifts the data displayed in the column to the right.</span></span>

<span data-ttu-id="d73d7-123">Center központok az oszlopban megjelenített adatokat.</span><span class="sxs-lookup"><span data-stu-id="d73d7-123">Center Centers the data displayed in the column.</span></span>

## <a name="remarks"></a><span data-ttu-id="d73d7-124">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="d73d7-124">Remarks</span></span>

<span data-ttu-id="d73d7-125">A táblázatos nézetre az összetevőivel kapcsolatos további információkért lásd: [táblázatos nézetre](./creating-a-table-view.md).</span><span class="sxs-lookup"><span data-stu-id="d73d7-125">For more information about the components of a table view, see [Table View](./creating-a-table-view.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="d73d7-126">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="d73d7-126">See Also</span></span>

[<span data-ttu-id="d73d7-127">Tábla nézet</span><span class="sxs-lookup"><span data-stu-id="d73d7-127">Table View</span></span>](./creating-a-table-view.md)

[<span data-ttu-id="d73d7-128">TableColumnItem elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="d73d7-128">TableColumnItem Element (Format)</span></span>](./tablecolumnitem-element-for-tablecolumnitems-for-tablecontrol-format.md)
