---
title: Szélesség eleme TableColumnHeader TableControl (formátum) a |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 94eb0535-8002-4f17-9a2b-4be75ec20e5c
caps.latest.revision: 18
ms.openlocfilehash: 4a25c9d81df670dc10955065bfb66766cdb1bd33
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62083620"
---
# <a name="width-element-for-tablecolumnheader-for-tablecontrol-format"></a><span data-ttu-id="9d718-102">A TableControl TableColumnHeader elemének Szélesség eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="9d718-102">Width Element for TableColumnHeader for TableControl (Format)</span></span>

<span data-ttu-id="9d718-103">Határozza meg az oszlopok szélességét (a karakter).</span><span class="sxs-lookup"><span data-stu-id="9d718-103">Defines the width (in characters) of a column.</span></span>

<span data-ttu-id="9d718-104">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézet elem (formátum) TableControl elem (formátum) TableHeaders eleme TableControl (formátum) TableColumnHeader elem TableHeaders TableControl (formátum) szélesség elem számára TableColumnHeader a TableControl (formátum)</span><span class="sxs-lookup"><span data-stu-id="9d718-104">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) TableControl Element (Format) TableHeaders Element for TableControl (Format) TableColumnHeader Element TableHeaders for TableControl (Format) Width Element for TableColumnHeader for TableControl (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="9d718-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="9d718-105">Syntax</span></span>

```xml
<Width>NumberOfCharacters</Width>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="9d718-106">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="9d718-106">Attributes and Elements</span></span>

<span data-ttu-id="9d718-107">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és szülőelemét a `Width` elem oszlopfejlécek meghatározásakor.</span><span class="sxs-lookup"><span data-stu-id="9d718-107">The following sections describe the attributes, child elements, and parent element of the `Width` element used when defining column headers.</span></span>

### <a name="attributes"></a><span data-ttu-id="9d718-108">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="9d718-108">Attributes</span></span>

<span data-ttu-id="9d718-109">Nincs.</span><span class="sxs-lookup"><span data-stu-id="9d718-109">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="9d718-110">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="9d718-110">Child Elements</span></span>

<span data-ttu-id="9d718-111">Nincs.</span><span class="sxs-lookup"><span data-stu-id="9d718-111">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="9d718-112">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="9d718-112">Parent Elements</span></span>

|<span data-ttu-id="9d718-113">Elem</span><span class="sxs-lookup"><span data-stu-id="9d718-113">Element</span></span>|<span data-ttu-id="9d718-114">Leírás</span><span class="sxs-lookup"><span data-stu-id="9d718-114">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="9d718-115">A TableControl (formátum) TableHeaders TableColumnHeader elem.</span><span class="sxs-lookup"><span data-stu-id="9d718-115">TableColumnHeader Element for TableHeaders for TableControl (Format)</span></span>](./tablecolumnheader-element-format.md)|<span data-ttu-id="9d718-116">Határozza meg, egy címke, a szélesség és a egy oszlop a tábla adatai igazítását.</span><span class="sxs-lookup"><span data-stu-id="9d718-116">Defines a label, width, and alignment of the data for a column of the table.</span></span>|

## <a name="text-value"></a><span data-ttu-id="9d718-117">A szöveges érték</span><span class="sxs-lookup"><span data-stu-id="9d718-117">Text Value</span></span>

<span data-ttu-id="9d718-118">Amikor csak lehet, adja meg, amely nagyobb, mint a megjelenített tulajdonságértékek hossza szélessége (a karakter).</span><span class="sxs-lookup"><span data-stu-id="9d718-118">When at all possible, specify a width (in characters) that is greater than the length of the displayed property values.</span></span>

## <a name="remarks"></a><span data-ttu-id="9d718-119">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="9d718-119">Remarks</span></span>

<span data-ttu-id="9d718-120">A táblázatos nézetre az összetevőivel kapcsolatos további információkért lásd: [tábla nézetek létrehozásával](./creating-a-table-view.md).</span><span class="sxs-lookup"><span data-stu-id="9d718-120">For more information about the components of a table view, see [Creating a Table View](./creating-a-table-view.md).</span></span>

## <a name="example"></a><span data-ttu-id="9d718-121">Példa</span><span class="sxs-lookup"><span data-stu-id="9d718-121">Example</span></span>

<span data-ttu-id="9d718-122">A következő példa bemutatja egy `TableColumnHeader` elem, amelynek 16 karakternél.</span><span class="sxs-lookup"><span data-stu-id="9d718-122">The following example shows a `TableColumnHeader` element whose width is 16 characters.</span></span>

```xml
<TableColumnHeader>
  <Label>Column 1</Label)
  <Width>16</Width>
  <Alignment>Left</Alignment>
</TableColumnHeader>
```

## <a name="see-also"></a><span data-ttu-id="9d718-123">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="9d718-123">See Also</span></span>

[<span data-ttu-id="9d718-124">Tábla nézet létrehozása</span><span class="sxs-lookup"><span data-stu-id="9d718-124">Creating a Table View</span></span>](./creating-a-table-view.md)

[<span data-ttu-id="9d718-125">A TableControl (formátum) TableHeader TableColumnHeader elem.</span><span class="sxs-lookup"><span data-stu-id="9d718-125">TableColumnHeader Element for TableHeader for TableControl (Format)</span></span>](./tablecolumnheader-element-format.md)

[<span data-ttu-id="9d718-126">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="9d718-126">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
