---
title: TableColumnItem TableControl (formátum) a FormatString eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 8a150731-d4b4-4d63-8db5-f14d463c8c37
caps.latest.revision: 13
ms.openlocfilehash: b7e1d0adc43254141056a729e1c1cc9699b6ac9b
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62065630"
---
# <a name="formatstring-element-for-tablecolumnitem-for-tablecontrol-format"></a><span data-ttu-id="e9e56-102">A TableControl TableColumnItem elemének FormatString eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="e9e56-102">FormatString Element for TableColumnItem for TableControl (Format)</span></span>

<span data-ttu-id="e9e56-103">Meghatározza formátumú mintát, amely meghatározza, hogyan jelenjen meg a táblázat tulajdonság, vagy parancsprogram értékét.</span><span class="sxs-lookup"><span data-stu-id="e9e56-103">Specifies a format pattern that defines how the property or script value of the table is displayed.</span></span>

<span data-ttu-id="e9e56-104">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem TableControl elem (formátum) TableRowEntries elem (formátum) TableRowEntry elem (formátum) TableColumnItems elem (formátum) TableColumnItem elem (formátum) FormatString eleme TableColumnItem (formátum)</span><span class="sxs-lookup"><span data-stu-id="e9e56-104">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) TableControl Element (Format) TableRowEntries Element (Format) TableRowEntry Element (Format) TableColumnItems Element (Format) TableColumnItem Element (Format) FormatString Element for TableColumnItem (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="e9e56-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="e9e56-105">Syntax</span></span>

```xml
<FormatString>FormatPattern</FormatString>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="e9e56-106">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="e9e56-106">Attributes and Elements</span></span>

<span data-ttu-id="e9e56-107">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `FormatString` elemet.</span><span class="sxs-lookup"><span data-stu-id="e9e56-107">The following sections describe attributes, child elements, and the parent element of the `FormatString` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="e9e56-108">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="e9e56-108">Attributes</span></span>

<span data-ttu-id="e9e56-109">Nincs.</span><span class="sxs-lookup"><span data-stu-id="e9e56-109">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="e9e56-110">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="e9e56-110">Child Elements</span></span>

<span data-ttu-id="e9e56-111">Nincs.</span><span class="sxs-lookup"><span data-stu-id="e9e56-111">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="e9e56-112">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="e9e56-112">Parent Elements</span></span>

|<span data-ttu-id="e9e56-113">Elem</span><span class="sxs-lookup"><span data-stu-id="e9e56-113">Element</span></span>|<span data-ttu-id="e9e56-114">Leírás</span><span class="sxs-lookup"><span data-stu-id="e9e56-114">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="e9e56-115">TableColumnItem elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="e9e56-115">TableColumnItem Element (Format)</span></span>](./tablecolumnitem-element-for-tablecolumnitems-for-tablecontrol-format.md)|<span data-ttu-id="e9e56-116">A tulajdonság, vagy a parancsfájl, amelynek értéke megjelenik a sor oszlop határozza meg.</span><span class="sxs-lookup"><span data-stu-id="e9e56-116">Defines the property or script whose value is displayed in the column of the row.</span></span>|

## <a name="text-value"></a><span data-ttu-id="e9e56-117">A szöveges érték</span><span class="sxs-lookup"><span data-stu-id="e9e56-117">Text Value</span></span>

<span data-ttu-id="e9e56-118">Adja meg az adatok formázásához használt mintáját.</span><span class="sxs-lookup"><span data-stu-id="e9e56-118">Specify the pattern that is used to format the data.</span></span> <span data-ttu-id="e9e56-119">Például ez a minta segítségével bármilyen típusú tulajdonság értékének [System.Timespan](/dotnet/api/System.TimeSpan): {0: MMM} {0:dd} {0:HH}: {0:mm}.</span><span class="sxs-lookup"><span data-stu-id="e9e56-119">For example, this pattern can be used to format the value of any property that is of type [System.Timespan](/dotnet/api/System.TimeSpan): {0:MMM}{0:dd}{0:HH}:{0:mm}.</span></span>

## <a name="remarks"></a><span data-ttu-id="e9e56-120">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="e9e56-120">Remarks</span></span>

<span data-ttu-id="e9e56-121">Formázási karakterláncokat is használható, nézetek, nézetek, széles nézetek vagy az egyéni nézetek létrehozása során.</span><span class="sxs-lookup"><span data-stu-id="e9e56-121">Format strings can be used when creating table views, list views, wide views, or custom views.</span></span> <span data-ttu-id="e9e56-122">További információ a nézetben megjelenített érték formázása: [megjelenített adatok formázása](./formatting-displayed-data.md).</span><span class="sxs-lookup"><span data-stu-id="e9e56-122">For more information about formatting a value displayed in a view, see [Formatting Displayed Data](./formatting-displayed-data.md).</span></span>

<span data-ttu-id="e9e56-123">A táblázatos nézetre az összetevőivel kapcsolatos további információkért lásd: [táblázatos nézetre](./creating-a-table-view.md).</span><span class="sxs-lookup"><span data-stu-id="e9e56-123">For more information about the components of a table view, see [Table View](./creating-a-table-view.md).</span></span>

## <a name="example"></a><span data-ttu-id="e9e56-124">Példa</span><span class="sxs-lookup"><span data-stu-id="e9e56-124">Example</span></span>

<span data-ttu-id="e9e56-125">Az alábbi példa bemutatja, hogyan definiáljon értékét formázási karakterláncot a `StartTime` tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="e9e56-125">The following example shows how to define a formatting string for the value of the `StartTime` property.</span></span>

```xml
<TableColumnItem>
  <PropertyName>StartTime</PropertyName>
  <FormatString>{0:MMM} (0:DD) (0:HH):(0:MM)</FormatString>
</TableColumnItem>
```

## <a name="see-also"></a><span data-ttu-id="e9e56-126">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="e9e56-126">See Also</span></span>

[<span data-ttu-id="e9e56-127">Tábla nézet létrehozása</span><span class="sxs-lookup"><span data-stu-id="e9e56-127">Creating a Table View</span></span>](./creating-a-table-view.md)

[<span data-ttu-id="e9e56-128">Adatok formázása jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="e9e56-128">Formatting Displayed Data</span></span>](./formatting-displayed-data.md)

[<span data-ttu-id="e9e56-129">TableColumnItem elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="e9e56-129">TableColumnItem Element (Format)</span></span>](./tablecolumnitem-element-for-tablecolumnitems-for-tablecontrol-format.md)

[<span data-ttu-id="e9e56-130">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="e9e56-130">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
