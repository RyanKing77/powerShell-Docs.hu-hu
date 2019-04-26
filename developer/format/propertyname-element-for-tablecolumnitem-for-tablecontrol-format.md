---
title: TableColumnItem TableControl (formátum) a PropertyName eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: fb26d72c-2f77-4801-badf-0537ccc55e31
caps.latest.revision: 10
ms.openlocfilehash: 6e86b6a0874b385703121802bc8108a0410442cd
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62064612"
---
# <a name="propertyname-element-for-tablecolumnitem-for-tablecontrol-format"></a><span data-ttu-id="2e16b-102">A TableControl TableColumnItem elemének PropertyName eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="2e16b-102">PropertyName Element for TableColumnItem for TableControl (Format)</span></span>

<span data-ttu-id="2e16b-103">Megadja a tulajdonságot, amelynek értéke megjelenik a sor oszlopában.</span><span class="sxs-lookup"><span data-stu-id="2e16b-103">Specifies the property whose value is displayed in the column of the row.</span></span>

<span data-ttu-id="2e16b-104">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem TableControl elem (formátum) TableRowEntries elem (formátum) TableRowEntry elem (formátum) TableColumnItems elem (formátum) TableColumnItem elem (formátum) A PropertyName eleme TableColumnItem (formátum)</span><span class="sxs-lookup"><span data-stu-id="2e16b-104">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) TableControl Element (Format) TableRowEntries Element (Format) TableRowEntry Element (Format) TableColumnItems Element (Format) TableColumnItem Element (Format) PropertyName Element for TableColumnItem (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="2e16b-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="2e16b-105">Syntax</span></span>

```xml
<PropertyName>.NetTypeProperty</PropertyName>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="2e16b-106">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="2e16b-106">Attributes and Elements</span></span>

<span data-ttu-id="2e16b-107">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és szülőelemét a `PropertyName` elemet.</span><span class="sxs-lookup"><span data-stu-id="2e16b-107">The following sections describe attributes, child elements, and parent element of the `PropertyName` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="2e16b-108">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="2e16b-108">Attributes</span></span>

<span data-ttu-id="2e16b-109">Nincs.</span><span class="sxs-lookup"><span data-stu-id="2e16b-109">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="2e16b-110">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="2e16b-110">Child Elements</span></span>

<span data-ttu-id="2e16b-111">Nincs.</span><span class="sxs-lookup"><span data-stu-id="2e16b-111">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="2e16b-112">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="2e16b-112">Parent Elements</span></span>

|<span data-ttu-id="2e16b-113">Elem</span><span class="sxs-lookup"><span data-stu-id="2e16b-113">Element</span></span>|<span data-ttu-id="2e16b-114">Leírás</span><span class="sxs-lookup"><span data-stu-id="2e16b-114">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="2e16b-115">TableColumnItem elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="2e16b-115">TableColumnItem Element (Format)</span></span>](./tablecolumnitem-element-for-tablecolumnitems-for-tablecontrol-format.md)|<span data-ttu-id="2e16b-116">A tulajdonság, vagy a parancsfájl, amelynek értéke megjelenik a sor oszlop határozza meg.</span><span class="sxs-lookup"><span data-stu-id="2e16b-116">Defines the property or script whose value is displayed in the column of the row.</span></span>|

## <a name="text-value"></a><span data-ttu-id="2e16b-117">A szöveges érték</span><span class="sxs-lookup"><span data-stu-id="2e16b-117">Text Value</span></span>

<span data-ttu-id="2e16b-118">Adja meg, amelynek értéke megjelenik a tulajdonság nevét.</span><span class="sxs-lookup"><span data-stu-id="2e16b-118">Specify the name of the property whose value is displayed.</span></span>

## <a name="remarks"></a><span data-ttu-id="2e16b-119">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="2e16b-119">Remarks</span></span>

<span data-ttu-id="2e16b-120">A táblázatos nézetre az összetevőivel kapcsolatos további információkért lásd: [tábla nézetek létrehozásával](./creating-a-table-view.md).</span><span class="sxs-lookup"><span data-stu-id="2e16b-120">For more information about the components of a table view, see [Creating a Table View](./creating-a-table-view.md).</span></span>

## <a name="example"></a><span data-ttu-id="2e16b-121">Példa</span><span class="sxs-lookup"><span data-stu-id="2e16b-121">Example</span></span>

<span data-ttu-id="2e16b-122">Ez a példa bemutatja egy `TableColumnItem` elem, amely meghatározza a `Status` tulajdonságát a [System.Diagnostics.Process](/dotnet/api/System.Diagnostics.Process) objektum.</span><span class="sxs-lookup"><span data-stu-id="2e16b-122">This example shows a `TableColumnItem` element that specifies the `Status` property of the [System.Diagnostics.Process](/dotnet/api/System.Diagnostics.Process) object.</span></span>

```xml
<TableColumnItem>
   <Alignment>Centered</Alignment>
  <PropertyName>Status</PropertyName>
</TableColumnItem>

```

## <a name="see-also"></a><span data-ttu-id="2e16b-123">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="2e16b-123">See Also</span></span>

[<span data-ttu-id="2e16b-124">Tábla nézet létrehozása</span><span class="sxs-lookup"><span data-stu-id="2e16b-124">Creating a Table View</span></span>](./creating-a-table-view.md)

[<span data-ttu-id="2e16b-125">TableColumnItem elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="2e16b-125">TableColumnItem Element (Format)</span></span>](./tablecolumnitem-element-for-tablecolumnitems-for-tablecontrol-format.md)

[<span data-ttu-id="2e16b-126">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="2e16b-126">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
