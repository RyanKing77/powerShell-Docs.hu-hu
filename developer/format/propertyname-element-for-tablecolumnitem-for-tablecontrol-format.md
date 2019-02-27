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
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56849237"
---
# <a name="propertyname-element-for-tablecolumnitem-for-tablecontrol-format"></a><span data-ttu-id="2a13a-102">A TableControl TableColumnItem elemének PropertyName eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="2a13a-102">PropertyName Element for TableColumnItem for TableControl (Format)</span></span>

<span data-ttu-id="2a13a-103">Megadja a tulajdonságot, amelynek értéke megjelenik a sor oszlopában.</span><span class="sxs-lookup"><span data-stu-id="2a13a-103">Specifies the property whose value is displayed in the column of the row.</span></span>

<span data-ttu-id="2a13a-104">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem TableControl elem (formátum) TableRowEntries elem (formátum) TableRowEntry elem (formátum) TableColumnItems elem (formátum) TableColumnItem elem (formátum) A PropertyName eleme TableColumnItem (formátum)</span><span class="sxs-lookup"><span data-stu-id="2a13a-104">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) TableControl Element (Format) TableRowEntries Element (Format) TableRowEntry Element (Format) TableColumnItems Element (Format) TableColumnItem Element (Format) PropertyName Element for TableColumnItem (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="2a13a-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="2a13a-105">Syntax</span></span>

```xml
<PropertyName>.NetTypeProperty</PropertyName>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="2a13a-106">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="2a13a-106">Attributes and Elements</span></span>

<span data-ttu-id="2a13a-107">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és szülőelemét a `PropertyName` elemet.</span><span class="sxs-lookup"><span data-stu-id="2a13a-107">The following sections describe attributes, child elements, and parent element of the `PropertyName` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="2a13a-108">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="2a13a-108">Attributes</span></span>

<span data-ttu-id="2a13a-109">Nincs.</span><span class="sxs-lookup"><span data-stu-id="2a13a-109">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="2a13a-110">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="2a13a-110">Child Elements</span></span>

<span data-ttu-id="2a13a-111">Nincs.</span><span class="sxs-lookup"><span data-stu-id="2a13a-111">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="2a13a-112">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="2a13a-112">Parent Elements</span></span>

|<span data-ttu-id="2a13a-113">Elem</span><span class="sxs-lookup"><span data-stu-id="2a13a-113">Element</span></span>|<span data-ttu-id="2a13a-114">Leírás</span><span class="sxs-lookup"><span data-stu-id="2a13a-114">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="2a13a-115">TableColumnItem elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="2a13a-115">TableColumnItem Element (Format)</span></span>](./tablecolumnitem-element-for-tablecolumnitems-for-tablecontrol-format.md)|<span data-ttu-id="2a13a-116">A tulajdonság, vagy a parancsfájl, amelynek értéke megjelenik a sor oszlop határozza meg.</span><span class="sxs-lookup"><span data-stu-id="2a13a-116">Defines the property or script whose value is displayed in the column of the row.</span></span>|

## <a name="text-value"></a><span data-ttu-id="2a13a-117">Szöveges érték</span><span class="sxs-lookup"><span data-stu-id="2a13a-117">Text Value</span></span>

<span data-ttu-id="2a13a-118">Adja meg, amelynek értéke megjelenik a tulajdonság nevét.</span><span class="sxs-lookup"><span data-stu-id="2a13a-118">Specify the name of the property whose value is displayed.</span></span>

## <a name="remarks"></a><span data-ttu-id="2a13a-119">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="2a13a-119">Remarks</span></span>

<span data-ttu-id="2a13a-120">A táblázatos nézetre az összetevőivel kapcsolatos további információkért lásd: [tábla nézetek létrehozásával](./creating-a-table-view.md).</span><span class="sxs-lookup"><span data-stu-id="2a13a-120">For more information about the components of a table view, see [Creating a Table View](./creating-a-table-view.md).</span></span>

## <a name="example"></a><span data-ttu-id="2a13a-121">Példa</span><span class="sxs-lookup"><span data-stu-id="2a13a-121">Example</span></span>

<span data-ttu-id="2a13a-122">Ez a példa bemutatja egy `TableColumnItem` elem, amely meghatározza a `Status` tulajdonságát a [System.Diagnostics.Process](/dotnet/api/System.Diagnostics.Process) objektum.</span><span class="sxs-lookup"><span data-stu-id="2a13a-122">This example shows a `TableColumnItem` element that specifies the `Status` property of the [System.Diagnostics.Process](/dotnet/api/System.Diagnostics.Process) object.</span></span>

```xml
<TableColumnItem>
   <Alignment>Centered</Alignment>
  <PropertyName>Status</PropertyName>
</TableColumnItem>

```

## <a name="see-also"></a><span data-ttu-id="2a13a-123">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="2a13a-123">See Also</span></span>

[<span data-ttu-id="2a13a-124">Tábla nézet létrehozása</span><span class="sxs-lookup"><span data-stu-id="2a13a-124">Creating a Table View</span></span>](./creating-a-table-view.md)

[<span data-ttu-id="2a13a-125">TableColumnItem elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="2a13a-125">TableColumnItem Element (Format)</span></span>](./tablecolumnitem-element-for-tablecolumnitems-for-tablecontrol-format.md)

[<span data-ttu-id="2a13a-126">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="2a13a-126">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
