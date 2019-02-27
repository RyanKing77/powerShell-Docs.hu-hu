---
title: Zarovnání eleme TableColumnHeader TableControl (formátum) a |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ff85e83a-c9c2-4c37-accc-e6a27c182f3c
caps.latest.revision: 19
ms.openlocfilehash: 16b41535109ca503e679a135f5ba30054e33de5b
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56845240"
---
# <a name="alignment-element-for-tablecolumnheader-for-tablecontrol-format"></a><span data-ttu-id="bff59-102">A TableControl TableColumnHeader elemének igazítási eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="bff59-102">Alignment Element for TableColumnHeader for TableControl (Format)</span></span>

<span data-ttu-id="bff59-103">Határozza meg, hogyan jelenjen meg az adatok egy oszlopfejlécre.</span><span class="sxs-lookup"><span data-stu-id="bff59-103">Defines how the data in a column header is displayed.</span></span>

<span data-ttu-id="bff59-104">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézet elem (formátum) TableControl elem (formátum) TableHeaders elem (formátum) TableColumnHeader elem (formátum) igazítás elem a TableColumnHeader (formátum)</span><span class="sxs-lookup"><span data-stu-id="bff59-104">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) TableControl Element (Format) TableHeaders Element (Format) TableColumnHeader Element (Format) Alignment Element for TableColumnHeader (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="bff59-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="bff59-105">Syntax</span></span>

```xml
<Alignment>AlignmentType</Alignment>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="bff59-106">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="bff59-106">Attributes and Elements</span></span>

<span data-ttu-id="bff59-107">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és szülőelemét a `Alignment` elemet.</span><span class="sxs-lookup"><span data-stu-id="bff59-107">The following sections describe the attributes, child elements, and parent element of the `Alignment` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="bff59-108">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="bff59-108">Attributes</span></span>

<span data-ttu-id="bff59-109">Nincs.</span><span class="sxs-lookup"><span data-stu-id="bff59-109">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="bff59-110">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="bff59-110">Child Elements</span></span>

<span data-ttu-id="bff59-111">Nincs.</span><span class="sxs-lookup"><span data-stu-id="bff59-111">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="bff59-112">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="bff59-112">Parent Elements</span></span>

|<span data-ttu-id="bff59-113">Elem</span><span class="sxs-lookup"><span data-stu-id="bff59-113">Element</span></span>|<span data-ttu-id="bff59-114">Leírás</span><span class="sxs-lookup"><span data-stu-id="bff59-114">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="bff59-115">TableColumnHeader elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="bff59-115">TableColumnHeader Element (Format)</span></span>](./tablecolumnheader-element-format.md)|<span data-ttu-id="bff59-116">Egy címke, a szélesség és az adatok egy oszlop a tábla zarovnání határozza meg.</span><span class="sxs-lookup"><span data-stu-id="bff59-116">Defines a label, the width, and the alignment of the data for a column of the table.</span></span>|

## <a name="text-value"></a><span data-ttu-id="bff59-117">Szöveges érték</span><span class="sxs-lookup"><span data-stu-id="bff59-117">Text Value</span></span>

<span data-ttu-id="bff59-118">Adja meg a következő értékek egyikét.</span><span class="sxs-lookup"><span data-stu-id="bff59-118">Specify one of the following values.</span></span> <span data-ttu-id="bff59-119">Ezek az értékek nem különböznek.</span><span class="sxs-lookup"><span data-stu-id="bff59-119">These values are not case-sensitive.</span></span>

<span data-ttu-id="bff59-120">Balra igazítása jelennek meg az oszlopot a bal oldali Ez az alapértelmezés szerint ha ez az elem nincs megadva.</span><span class="sxs-lookup"><span data-stu-id="bff59-120">Left Aligns the data displayed in the column on the left This is the default if this element is not specified.</span></span>

<span data-ttu-id="bff59-121">Jobbra igazítja az adatok az oszlopban látható a jobb oldalon.</span><span class="sxs-lookup"><span data-stu-id="bff59-121">Right Aligns the data displayed in the column on the right.</span></span>

<span data-ttu-id="bff59-122">Center központok az oszlopban megjelenített adatokat.</span><span class="sxs-lookup"><span data-stu-id="bff59-122">Center Centers the data displayed in the column.</span></span>

## <a name="remarks"></a><span data-ttu-id="bff59-123">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="bff59-123">Remarks</span></span>

<span data-ttu-id="bff59-124">A táblázatos nézetre az összetevőivel kapcsolatos további információkért lásd: [tábla nézetek létrehozásával](./creating-a-table-view.md).</span><span class="sxs-lookup"><span data-stu-id="bff59-124">For more information about the components of a table view, see [Creating a Table View](./creating-a-table-view.md).</span></span>

## <a name="example"></a><span data-ttu-id="bff59-125">Példa</span><span class="sxs-lookup"><span data-stu-id="bff59-125">Example</span></span>

<span data-ttu-id="bff59-126">Ez a példa bemutatja egy `TableColumnHeader` elem, amelynek az adatait a bal oldali van igazítva.</span><span class="sxs-lookup"><span data-stu-id="bff59-126">This example shows a `TableColumnHeader` element whose data is aligned on the left.</span></span>

```xml
<TableColumnHeader>
  <Label>Column 1</Label)
  <Width>16</Width>
  <Alignment>Left</Alignment>
</TableColumnHeader>
```

## <a name="see-also"></a><span data-ttu-id="bff59-127">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="bff59-127">See Also</span></span>

[<span data-ttu-id="bff59-128">Tábla nézet létrehozása</span><span class="sxs-lookup"><span data-stu-id="bff59-128">Creating a Table View</span></span>](./creating-a-table-view.md)

[<span data-ttu-id="bff59-129">TableColumnHeader elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="bff59-129">TableColumnHeader Element (Format)</span></span>](./tablecolumnheader-element-format.md)

[<span data-ttu-id="bff59-130">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="bff59-130">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
