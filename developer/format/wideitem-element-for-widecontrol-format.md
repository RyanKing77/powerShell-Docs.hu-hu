---
title: (Formátum) WideControl WideItem eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 17352fc4-ba83-4f04-86bc-f591765d85a8
caps.latest.revision: 18
ms.openlocfilehash: fa9eda3ea1028c27dbfb3eb04747af3b817c1a81
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62083637"
---
# <a name="wideitem-element-for-widecontrol-format"></a><span data-ttu-id="5beea-102">A WideControl WideItem eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="5beea-102">WideItem Element for WideControl (Format)</span></span>

<span data-ttu-id="5beea-103">Határozza meg, tulajdonság vagy parancsfájl, amelynek értéke megjelenik.</span><span class="sxs-lookup"><span data-stu-id="5beea-103">Defines the property or script whose value is displayed.</span></span>

<span data-ttu-id="5beea-104">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem WideControl elem (formátum) WideEntries elem (formátum) WideEntry elem (formátum) WideItem elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="5beea-104">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) WideControl Element (Format) WideEntries Element (Format) WideEntry Element (Format) WideItem Element (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="5beea-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="5beea-105">Syntax</span></span>

```xml
<WideItem>
  <PropertyName>.NetTypeProperty</PropertyName>
  <ScriptBlock>ScriptToExecute</ScriptBlock>
  <FormatString>FormatPattern</FormatString>
</WideItem>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="5beea-106">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="5beea-106">Attributes and Elements</span></span>

<span data-ttu-id="5beea-107">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `WideItem` elemet.</span><span class="sxs-lookup"><span data-stu-id="5beea-107">The following sections describe the attributes, child elements, and the parent element of the `WideItem` element.</span></span> <span data-ttu-id="5beea-108">A `FormatString` elem nem kötelező.</span><span class="sxs-lookup"><span data-stu-id="5beea-108">The `FormatString` element is optional.</span></span> <span data-ttu-id="5beea-109">Azonban meg kell adnia egy `PropertyName` vagy `ScriptBlock` elem, de nem adható meg egyszerre.</span><span class="sxs-lookup"><span data-stu-id="5beea-109">However, you must specify a `PropertyName` or `ScriptBlock` element, but you cannot specify both.</span></span>

### <a name="attributes"></a><span data-ttu-id="5beea-110">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="5beea-110">Attributes</span></span>

<span data-ttu-id="5beea-111">Nincs.</span><span class="sxs-lookup"><span data-stu-id="5beea-111">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="5beea-112">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="5beea-112">Child Elements</span></span>

|<span data-ttu-id="5beea-113">Elem</span><span class="sxs-lookup"><span data-stu-id="5beea-113">Element</span></span>|<span data-ttu-id="5beea-114">Leírás</span><span class="sxs-lookup"><span data-stu-id="5beea-114">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="5beea-115">WideItem WideControl (formátum) a FormatString elem.</span><span class="sxs-lookup"><span data-stu-id="5beea-115">FormatString Element for WideItem for WideControl (Format)</span></span>](./formatstring-element-for-wideitem-for-widecontrol-format.md)|<span data-ttu-id="5beea-116">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="5beea-116">Optional element.</span></span><br /><br /> <span data-ttu-id="5beea-117">Meghatározza formátumú mintát, amely meghatározza, hogy a tulajdonság vagy parancsfájl érték hogyan jelenjen meg a nézetben.</span><span class="sxs-lookup"><span data-stu-id="5beea-117">Specifies a format pattern that defines how the property or script value is displayed in the view.</span></span>|
|[<span data-ttu-id="5beea-118">A PropertyName eleme WideItem (formátum)</span><span class="sxs-lookup"><span data-stu-id="5beea-118">PropertyName Element for WideItem (Format)</span></span>](./propertyname-element-for-wideitem-for-widecontrol-format.md)|<span data-ttu-id="5beea-119">Itt adhatja meg a tulajdonság az objektum, amelynek az értéke az széles nézetben jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="5beea-119">Specifies the property of the object whose value is displayed in the wide view.</span></span>|
|[<span data-ttu-id="5beea-120">ScriptBlock eleme WideItem (formátum)</span><span class="sxs-lookup"><span data-stu-id="5beea-120">ScriptBlock Element for WideItem (Format)</span></span>](./scriptblock-element-for-wideitem-for-widecontrol-format.md)|<span data-ttu-id="5beea-121">Megadja a parancsprogramot, amelynek az értéke az széles nézetben jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="5beea-121">Specifies the script whose value is displayed in the wide view.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="5beea-122">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="5beea-122">Parent Elements</span></span>

|<span data-ttu-id="5beea-123">Elem</span><span class="sxs-lookup"><span data-stu-id="5beea-123">Element</span></span>|<span data-ttu-id="5beea-124">Leírás</span><span class="sxs-lookup"><span data-stu-id="5beea-124">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="5beea-125">WideEntry elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="5beea-125">WideEntry Element (Format)</span></span>](./wideentry-element-for-widecontrol-format.md)|<span data-ttu-id="5beea-126">A széles nézet definíciójának biztosít.</span><span class="sxs-lookup"><span data-stu-id="5beea-126">Provides a definition of the wide view.</span></span>|

## <a name="remarks"></a><span data-ttu-id="5beea-127">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="5beea-127">Remarks</span></span>

<span data-ttu-id="5beea-128">Egy széles nézet az összetevőivel kapcsolatos további információkért lásd: [széles nézet](./creating-a-wide-view.md).</span><span class="sxs-lookup"><span data-stu-id="5beea-128">For more information about the components of a wide view, see [Wide View](./creating-a-wide-view.md).</span></span>

## <a name="example"></a><span data-ttu-id="5beea-129">Példa</span><span class="sxs-lookup"><span data-stu-id="5beea-129">Example</span></span>

<span data-ttu-id="5beea-130">A következő példa bemutatja egy `WideEntry` elem, amely meghatározza egy `WideItem` elemet.</span><span class="sxs-lookup"><span data-stu-id="5beea-130">The following example shows a `WideEntry` element that defines a single `WideItem` element.</span></span> <span data-ttu-id="5beea-131">A `WideItem` elem definiálja a tulajdonságot, vagy a parancsfájl, amelynek értéke megjelenik a nézetben.</span><span class="sxs-lookup"><span data-stu-id="5beea-131">The `WideItem` element defines the property or script whose value is displayed in the view.</span></span>

```xml
<WideEntry>
  <WideItem>
    <PropertyName>ProcessName</PropertyName>
  </WideItem>
</WideEntry>
```

<span data-ttu-id="5beea-132">Egy széles nézet egy teljes példa: [széles nézet (alapszintű)](./wide-view-basic.md).</span><span class="sxs-lookup"><span data-stu-id="5beea-132">For a complete example of a wide view, see [Wide View (Basic)](./wide-view-basic.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="5beea-133">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="5beea-133">See Also</span></span>

[<span data-ttu-id="5beea-134">WideItem WideControl (formátum) a FormatString elem.</span><span class="sxs-lookup"><span data-stu-id="5beea-134">FormatString Element for WideItem for WideControl (Format)</span></span>](./formatstring-element-for-wideitem-for-widecontrol-format.md)

[<span data-ttu-id="5beea-135">A PropertyName eleme WideItem (formátum)</span><span class="sxs-lookup"><span data-stu-id="5beea-135">PropertyName Element for WideItem (Format)</span></span>](./propertyname-element-for-wideitem-for-widecontrol-format.md)

[<span data-ttu-id="5beea-136">ScriptBlock eleme WideItem (formátum)</span><span class="sxs-lookup"><span data-stu-id="5beea-136">ScriptBlock Element for WideItem (Format)</span></span>](./scriptblock-element-for-wideitem-for-widecontrol-format.md)

[<span data-ttu-id="5beea-137">WideEntry elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="5beea-137">WideEntry Element (Format)</span></span>](./wideentry-element-for-widecontrol-format.md)

[<span data-ttu-id="5beea-138">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="5beea-138">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
