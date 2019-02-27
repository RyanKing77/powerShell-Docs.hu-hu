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
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56849846"
---
# <a name="formatstring-element-for-listitem-for-listcontrol--format"></a><span data-ttu-id="fdd24-102">A ListControl ListItem eleméhez tartozó FormatString elem (Formátum)</span><span class="sxs-lookup"><span data-stu-id="fdd24-102">FormatString Element for ListItem for ListControl  (Format)</span></span>

<span data-ttu-id="fdd24-103">Itt adhatja meg, amely meghatározza, hogyan jelenjen meg a tulajdonság vagy parancsfájl érték formátuma mintát.</span><span class="sxs-lookup"><span data-stu-id="fdd24-103">Specifies a format pattern that defines how the property or script value is displayed.</span></span>

<span data-ttu-id="fdd24-104">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem ListControl elem (formátum) ListEntries elem ListControl (formátum) ListEntry elem ListControl (formátum) ListItems elemek elemhez tartozó ListControl (formátum) Listaelem eleme ListItem ListControl (formátum) a FormatString eleme ListControl (formátum)</span><span class="sxs-lookup"><span data-stu-id="fdd24-104">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) ListControl Element (Format) ListEntries Element for ListControl (Format) ListEntry Element for ListControl (Format) ListItems Element for ListControl (Format) ListItem Element for ListControl (Format) FormatString Element for ListItem for ListControl (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="fdd24-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="fdd24-105">Syntax</span></span>

```xml
<FormatString>PropertyPattern</FormatString>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="fdd24-106">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="fdd24-106">Attributes and Elements</span></span>

<span data-ttu-id="fdd24-107">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `FormatString` elemet.</span><span class="sxs-lookup"><span data-stu-id="fdd24-107">The following sections describe the attributes, child elements, and the parent element of the `FormatString` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="fdd24-108">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="fdd24-108">Attributes</span></span>

<span data-ttu-id="fdd24-109">Nincs.</span><span class="sxs-lookup"><span data-stu-id="fdd24-109">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="fdd24-110">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="fdd24-110">Child Elements</span></span>

<span data-ttu-id="fdd24-111">Nincs.</span><span class="sxs-lookup"><span data-stu-id="fdd24-111">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="fdd24-112">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="fdd24-112">Parent Elements</span></span>

|<span data-ttu-id="fdd24-113">Elem</span><span class="sxs-lookup"><span data-stu-id="fdd24-113">Element</span></span>|<span data-ttu-id="fdd24-114">Leírás</span><span class="sxs-lookup"><span data-stu-id="fdd24-114">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="fdd24-115">Listaelem elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="fdd24-115">ListItem Element (Format)</span></span>](./listitem-element-for-listitems-for-listcontrol-format.md)|<span data-ttu-id="fdd24-116">A tulajdonság, vagy a parancsfájl, amelynek értéke megjelenik a lista nézet sorában lévő határoz meg.</span><span class="sxs-lookup"><span data-stu-id="fdd24-116">Defines the property or script whose value is displayed in a row of the list view.</span></span>|

## <a name="text-value"></a><span data-ttu-id="fdd24-117">Szöveges érték</span><span class="sxs-lookup"><span data-stu-id="fdd24-117">Text Value</span></span>

<span data-ttu-id="fdd24-118">Adja meg az adatok formázásához használt mintáját.</span><span class="sxs-lookup"><span data-stu-id="fdd24-118">Specify the pattern that is used to format the data.</span></span> <span data-ttu-id="fdd24-119">Például használhatja ezt a mintát bármilyen típusú tulajdonság értékének [System.Timespan](/dotnet/api/System.TimeSpan): {0: MMM} {0:dd} {0:HH}: {0:mm}.</span><span class="sxs-lookup"><span data-stu-id="fdd24-119">For example, you can use this pattern to format the value of any property that is of type [System.Timespan](/dotnet/api/System.TimeSpan): {0:MMM}{0:dd}{0:HH}:{0:mm}.</span></span>

## <a name="remarks"></a><span data-ttu-id="fdd24-120">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="fdd24-120">Remarks</span></span>

<span data-ttu-id="fdd24-121">Formázási karakterláncokat is használható, nézetek, nézetek, széles nézetek vagy az egyéni nézetek létrehozása során.</span><span class="sxs-lookup"><span data-stu-id="fdd24-121">Format strings can be used when creating table views, list views, wide views, or custom views.</span></span> <span data-ttu-id="fdd24-122">További információ a nézetben megjelenített érték formázása: [megjelenített adatok formázása](./formatting-displayed-data.md).</span><span class="sxs-lookup"><span data-stu-id="fdd24-122">For more information about formatting a value displayed in a view, see [Formatting Displayed Data](./formatting-displayed-data.md).</span></span>

<span data-ttu-id="fdd24-123">Listanézetek a formázási karakterláncokat használatával kapcsolatos további információkért lásd: [lista nézet létrehozása](./creating-a-list-view.md).</span><span class="sxs-lookup"><span data-stu-id="fdd24-123">For more information about using format strings in list views, see [Creating List View](./creating-a-list-view.md).</span></span>

## <a name="example"></a><span data-ttu-id="fdd24-124">Példa</span><span class="sxs-lookup"><span data-stu-id="fdd24-124">Example</span></span>

<span data-ttu-id="fdd24-125">Az alábbi példa bemutatja, hogyan definiáljon értékét formázási karakterláncot a `StartTime` tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="fdd24-125">The following example shows how to define a formatting string for the value of the `StartTime` property.</span></span>

```xml
<ListItem>
  <PropertyName>StartTime</PropertyName>
  <FormatString>{0:MMM} (0:DD) (0:HH):(0:MM)</FormatString>
</ListItem>
```

## <a name="see-also"></a><span data-ttu-id="fdd24-126">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="fdd24-126">See Also</span></span>

[<span data-ttu-id="fdd24-127">Lista nézet létrehozása</span><span class="sxs-lookup"><span data-stu-id="fdd24-127">Creating a List View</span></span>](./creating-a-list-view.md)

[<span data-ttu-id="fdd24-128">Listaelem elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="fdd24-128">ListItem Element (Format)</span></span>](./listitem-element-for-listitems-for-listcontrol-format.md)

[<span data-ttu-id="fdd24-129">Egy Windows PowerShell formázás és a fájl típusai</span><span class="sxs-lookup"><span data-stu-id="fdd24-129">Writing a Windows PowerShell Formatting and Types File</span></span>](./writing-a-powershell-formatting-file.md)
