---
title: WideItem WideControl (formátum) a FormatString eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 5bc6ea26-3ca6-4bab-8a13-29189821ba15
caps.latest.revision: 7
ms.openlocfilehash: a1dc145864a6904fd4af6c3b9187819c49e224b0
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62065682"
---
# <a name="formatstring-element-for-wideitem-for-widecontrol-format"></a><span data-ttu-id="769c8-102">A WideControl WideItem elemének FormatString eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="769c8-102">FormatString Element for WideItem for WideControl (Format)</span></span>

<span data-ttu-id="769c8-103">Meghatározza formátumú mintát, amely meghatározza, hogy a tulajdonság vagy parancsfájl érték hogyan jelenjen meg a nézetben.</span><span class="sxs-lookup"><span data-stu-id="769c8-103">Specifies a format pattern that defines how the property or script value is displayed in the view.</span></span>

<span data-ttu-id="769c8-104">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem WideControl elem (formátum) WideEntries elem (formátum) WideEntry elem WideControl (formátum) FormatString elemhez (formátum) WideControl WideItem elemhez a WideItem a WideControl (formátum)</span><span class="sxs-lookup"><span data-stu-id="769c8-104">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) WideControl Element (Format) WideEntries Element (Format) WideEntry Element for WideControl (Format) WideItem Element for WideControl (Format) FormatString Element for WideItem for WideControl (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="769c8-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="769c8-105">Syntax</span></span>

```xml
<FormatString>PropertyPattern</FormatString>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="769c8-106">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="769c8-106">Attributes and Elements</span></span>

<span data-ttu-id="769c8-107">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `FormatString` elemet.</span><span class="sxs-lookup"><span data-stu-id="769c8-107">The following sections describe the attributes, child elements, and the parent element of the `FormatString` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="769c8-108">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="769c8-108">Attributes</span></span>

<span data-ttu-id="769c8-109">Nincs.</span><span class="sxs-lookup"><span data-stu-id="769c8-109">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="769c8-110">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="769c8-110">Child Elements</span></span>

<span data-ttu-id="769c8-111">Nincs.</span><span class="sxs-lookup"><span data-stu-id="769c8-111">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="769c8-112">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="769c8-112">Parent Elements</span></span>

|<span data-ttu-id="769c8-113">Elem</span><span class="sxs-lookup"><span data-stu-id="769c8-113">Element</span></span>|<span data-ttu-id="769c8-114">Leírás</span><span class="sxs-lookup"><span data-stu-id="769c8-114">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="769c8-115">WideItem eleme WideControl (formátum)</span><span class="sxs-lookup"><span data-stu-id="769c8-115">WideItem Element for WideControl (Format)</span></span>](./wideitem-element-for-widecontrol-format.md)|<span data-ttu-id="769c8-116">A tulajdonság, vagy a parancsfájl, amelynek értéke megjelenik a lista nézet sorában lévő határoz meg.</span><span class="sxs-lookup"><span data-stu-id="769c8-116">Defines the property or script whose value is displayed in a row of the list view.</span></span>|

## <a name="text-value"></a><span data-ttu-id="769c8-117">A szöveges érték</span><span class="sxs-lookup"><span data-stu-id="769c8-117">Text Value</span></span>

<span data-ttu-id="769c8-118">Adja meg az adatok formázásához használt mintáját.</span><span class="sxs-lookup"><span data-stu-id="769c8-118">Specify the pattern that is used to format the data.</span></span> <span data-ttu-id="769c8-119">Például használhatja ezt a mintát bármilyen típusú tulajdonság értékének [System.Timespan](/dotnet/api/System.TimeSpan): {0: MMM} {0:dd} {0:HH}: {0:mm}.</span><span class="sxs-lookup"><span data-stu-id="769c8-119">For example, you can use this pattern to format the value of any property that is of type [System.Timespan](/dotnet/api/System.TimeSpan): {0:MMM}{0:dd}{0:HH}:{0:mm}.</span></span>

## <a name="remarks"></a><span data-ttu-id="769c8-120">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="769c8-120">Remarks</span></span>

<span data-ttu-id="769c8-121">Formázási karakterláncokat is használható, nézetek, nézetek, széles nézetek vagy az egyéni nézetek létrehozása során.</span><span class="sxs-lookup"><span data-stu-id="769c8-121">Format strings can be used when creating table views, list views, wide views, or custom views.</span></span> <span data-ttu-id="769c8-122">További információ a nézetben megjelenített érték formázása: [megjelenített adatok formázása](./formatting-displayed-data.md).</span><span class="sxs-lookup"><span data-stu-id="769c8-122">For more information about formatting a value displayed in a view, see [Formatting Displayed Data](./formatting-displayed-data.md).</span></span>

<span data-ttu-id="769c8-123">A széles körű nézetekben formázási karakterláncokat használatával kapcsolatos további információkért lásd: [széles nézet létrehozásával](./creating-a-wide-view.md).</span><span class="sxs-lookup"><span data-stu-id="769c8-123">For more information about using format strings in wide views, see [Creating a Wide View](./creating-a-wide-view.md).</span></span>

## <a name="example"></a><span data-ttu-id="769c8-124">Példa</span><span class="sxs-lookup"><span data-stu-id="769c8-124">Example</span></span>

<span data-ttu-id="769c8-125">Az alábbi példa bemutatja, hogyan definiáljon értékét formázási karakterláncot a `StartTime` tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="769c8-125">The following example shows how to define a formatting string for the value of the `StartTime` property.</span></span>

```xml
<WideItem>
  <PropertyName>StartTime</PropertyName>
  <FormatString>{0:MMM} (0:DD) (0:HH):(0:MM)</FormatString>
</WideItem>
```

## <a name="see-also"></a><span data-ttu-id="769c8-126">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="769c8-126">See Also</span></span>

[<span data-ttu-id="769c8-127">Egy széles nézet létrehozása</span><span class="sxs-lookup"><span data-stu-id="769c8-127">Creating a Wide View</span></span>](./creating-a-wide-view.md)

[<span data-ttu-id="769c8-128">WideItem eleme WideControl (formátum)</span><span class="sxs-lookup"><span data-stu-id="769c8-128">WideItem Element for WideControl (Format)</span></span>](./wideitem-element-for-widecontrol-format.md)

[<span data-ttu-id="769c8-129">Egy Windows PowerShell formázás és a fájl típusai</span><span class="sxs-lookup"><span data-stu-id="769c8-129">Writing a Windows PowerShell Formatting and Types File</span></span>](./writing-a-powershell-formatting-file.md)
