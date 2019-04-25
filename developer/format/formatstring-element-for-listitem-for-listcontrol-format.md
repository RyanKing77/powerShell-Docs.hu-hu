---
title: Listaelem ListControl (formátum) a FormatString eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: fd2cac66-88bb-449f-9d47-bd2cd4fe1801
caps.latest.revision: 13
ms.openlocfilehash: e6024ec4f7fc490c92408047c8c15c775e45bf9d
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62065620"
---
# <a name="formatstring-element-for-listitem-for-listcontrol--format"></a><span data-ttu-id="2cceb-102">A ListControl ListItem eleméhez tartozó FormatString elem (Formátum)</span><span class="sxs-lookup"><span data-stu-id="2cceb-102">FormatString Element for ListItem for ListControl  (Format)</span></span>

<span data-ttu-id="2cceb-103">Itt adhatja meg, amely meghatározza, hogyan jelenjen meg a tulajdonság vagy parancsfájl érték formátuma mintát.</span><span class="sxs-lookup"><span data-stu-id="2cceb-103">Specifies a format pattern that defines how the property or script value is displayed.</span></span>

<span data-ttu-id="2cceb-104">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem ListControl elem (formátum) ListEntries elem ListControl (formátum) ListEntry elem ListControl (formátum) ListItems elemek elemhez tartozó ListControl (formátum) Listaelem eleme ListItem ListControl (formátum) a FormatString eleme ListControl (formátum)</span><span class="sxs-lookup"><span data-stu-id="2cceb-104">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) ListControl Element (Format) ListEntries Element for ListControl (Format) ListEntry Element for ListControl (Format) ListItems Element for ListControl (Format) ListItem Element for ListControl (Format) FormatString Element for ListItem for ListControl (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="2cceb-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="2cceb-105">Syntax</span></span>

```xml
<FormatString>PropertyPattern</FormatString>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="2cceb-106">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="2cceb-106">Attributes and Elements</span></span>

<span data-ttu-id="2cceb-107">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `FormatString` elemet.</span><span class="sxs-lookup"><span data-stu-id="2cceb-107">The following sections describe the attributes, child elements, and the parent element of the `FormatString` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="2cceb-108">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="2cceb-108">Attributes</span></span>

<span data-ttu-id="2cceb-109">Nincs.</span><span class="sxs-lookup"><span data-stu-id="2cceb-109">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="2cceb-110">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="2cceb-110">Child Elements</span></span>

<span data-ttu-id="2cceb-111">Nincs.</span><span class="sxs-lookup"><span data-stu-id="2cceb-111">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="2cceb-112">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="2cceb-112">Parent Elements</span></span>

|<span data-ttu-id="2cceb-113">Elem</span><span class="sxs-lookup"><span data-stu-id="2cceb-113">Element</span></span>|<span data-ttu-id="2cceb-114">Leírás</span><span class="sxs-lookup"><span data-stu-id="2cceb-114">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="2cceb-115">Listaelem elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="2cceb-115">ListItem Element (Format)</span></span>](./listitem-element-for-listitems-for-listcontrol-format.md)|<span data-ttu-id="2cceb-116">A tulajdonság, vagy a parancsfájl, amelynek értéke megjelenik a lista nézet sorában lévő határoz meg.</span><span class="sxs-lookup"><span data-stu-id="2cceb-116">Defines the property or script whose value is displayed in a row of the list view.</span></span>|

## <a name="text-value"></a><span data-ttu-id="2cceb-117">A szöveges érték</span><span class="sxs-lookup"><span data-stu-id="2cceb-117">Text Value</span></span>

<span data-ttu-id="2cceb-118">Adja meg az adatok formázásához használt mintáját.</span><span class="sxs-lookup"><span data-stu-id="2cceb-118">Specify the pattern that is used to format the data.</span></span> <span data-ttu-id="2cceb-119">Például használhatja ezt a mintát bármilyen típusú tulajdonság értékének [System.Timespan](/dotnet/api/System.TimeSpan): {0: MMM} {0:dd} {0:HH}: {0:mm}.</span><span class="sxs-lookup"><span data-stu-id="2cceb-119">For example, you can use this pattern to format the value of any property that is of type [System.Timespan](/dotnet/api/System.TimeSpan): {0:MMM}{0:dd}{0:HH}:{0:mm}.</span></span>

## <a name="remarks"></a><span data-ttu-id="2cceb-120">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="2cceb-120">Remarks</span></span>

<span data-ttu-id="2cceb-121">Formázási karakterláncokat is használható, nézetek, nézetek, széles nézetek vagy az egyéni nézetek létrehozása során.</span><span class="sxs-lookup"><span data-stu-id="2cceb-121">Format strings can be used when creating table views, list views, wide views, or custom views.</span></span> <span data-ttu-id="2cceb-122">További információ a nézetben megjelenített érték formázása: [megjelenített adatok formázása](./formatting-displayed-data.md).</span><span class="sxs-lookup"><span data-stu-id="2cceb-122">For more information about formatting a value displayed in a view, see [Formatting Displayed Data](./formatting-displayed-data.md).</span></span>

<span data-ttu-id="2cceb-123">Listanézetek a formázási karakterláncokat használatával kapcsolatos további információkért lásd: [lista nézet létrehozása](./creating-a-list-view.md).</span><span class="sxs-lookup"><span data-stu-id="2cceb-123">For more information about using format strings in list views, see [Creating List View](./creating-a-list-view.md).</span></span>

## <a name="example"></a><span data-ttu-id="2cceb-124">Példa</span><span class="sxs-lookup"><span data-stu-id="2cceb-124">Example</span></span>

<span data-ttu-id="2cceb-125">Az alábbi példa bemutatja, hogyan definiáljon értékét formázási karakterláncot a `StartTime` tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="2cceb-125">The following example shows how to define a formatting string for the value of the `StartTime` property.</span></span>

```xml
<ListItem>
  <PropertyName>StartTime</PropertyName>
  <FormatString>{0:MMM} (0:DD) (0:HH):(0:MM)</FormatString>
</ListItem>
```

## <a name="see-also"></a><span data-ttu-id="2cceb-126">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="2cceb-126">See Also</span></span>

[<span data-ttu-id="2cceb-127">Lista nézet létrehozása</span><span class="sxs-lookup"><span data-stu-id="2cceb-127">Creating a List View</span></span>](./creating-a-list-view.md)

[<span data-ttu-id="2cceb-128">Listaelem elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="2cceb-128">ListItem Element (Format)</span></span>](./listitem-element-for-listitems-for-listcontrol-format.md)

[<span data-ttu-id="2cceb-129">Egy Windows PowerShell formázás és a fájl típusai</span><span class="sxs-lookup"><span data-stu-id="2cceb-129">Writing a Windows PowerShell Formatting and Types File</span></span>](./writing-a-powershell-formatting-file.md)
