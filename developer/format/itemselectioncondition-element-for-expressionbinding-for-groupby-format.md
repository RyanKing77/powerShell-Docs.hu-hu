---
title: A GroupBy (formátum) ExpressionBinding ItemSelectionCondition eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 6af3be7d-921e-4cf7-bd5a-d87aa0b4efbd
caps.latest.revision: 7
ms.openlocfilehash: b2b0a0d1996392614807e08b820a72978e38a0cb
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56844806"
---
# <a name="itemselectioncondition-element-for-expressionbinding-for-groupby-format"></a><span data-ttu-id="06b0f-102">A GroupBy elemhez tartozó ExpressionBinding ItemSelectionCondition eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="06b0f-102">ItemSelectionCondition Element for ExpressionBinding for GroupBy (Format)</span></span>

<span data-ttu-id="06b0f-103">Határozza meg azt a feltételt, amelyet Pro tento ovládací prvek használandó léteznie kell.</span><span class="sxs-lookup"><span data-stu-id="06b0f-103">Defines the condition that must exist for this control to be used.</span></span> <span data-ttu-id="06b0f-104">Van egy vezérlő elemhez megadható kiválasztási feltételek száma nincs korlátozva.</span><span class="sxs-lookup"><span data-stu-id="06b0f-104">There is no limit to the number of selection conditions that can be specified for a control item.</span></span> <span data-ttu-id="06b0f-105">Ez az elem szolgál, hogyan jelenjen meg az objektumok egy új csoportot meghatározásakor.</span><span class="sxs-lookup"><span data-stu-id="06b0f-105">This element is used when defining how a new group of objects is displayed.</span></span>

<span data-ttu-id="06b0f-106">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem GroupBy elem megtekintése (formátum) CustomControl elem a GroupBy (formátum) CustomEntry elemhez tartozó CustomControl GroupBy (formátum) CustomEntries elemhez GroupBy (formátum) CustomItem elem CustomEntry CustomItem ExpressionBinding GroupBy (formátum) esetében a GroupBy (formátum) ItemSelectionCondition elemhez tartozó GroupBy (formátum) ExpressionBinding elemhez tartozó CustomControl</span><span class="sxs-lookup"><span data-stu-id="06b0f-106">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) GroupBy Element for View (Format) CustomControl Element for GroupBy (Format) CustomEntries Element for CustomControl for GroupBy (Format) CustomEntry Element for CustomControl for GroupBy (Format) CustomItem Element for CustomEntry for GroupBy (Format) ExpressionBinding Element for CustomItem for GroupBy (Format) ItemSelectionCondition Element for ExpressionBinding for GroupBy (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="06b0f-107">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="06b0f-107">Syntax</span></span>

```xml
<ItemSelectionCondition>
  <PropertyName>.NetTypeProperty</PropertyName>
  <ScriptBlock>ScriptToEvaluate</ScriptBlock>
</ItemSelectionCondition>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="06b0f-108">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="06b0f-108">Attributes and Elements</span></span>

<span data-ttu-id="06b0f-109">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `ItemSelectionCondition` elemet.</span><span class="sxs-lookup"><span data-stu-id="06b0f-109">The following sections describe attributes, child elements, and the parent element of the `ItemSelectionCondition` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="06b0f-110">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="06b0f-110">Attributes</span></span>

<span data-ttu-id="06b0f-111">Nincs.</span><span class="sxs-lookup"><span data-stu-id="06b0f-111">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="06b0f-112">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="06b0f-112">Child Elements</span></span>

|<span data-ttu-id="06b0f-113">Elem</span><span class="sxs-lookup"><span data-stu-id="06b0f-113">Element</span></span>|<span data-ttu-id="06b0f-114">Leírás</span><span class="sxs-lookup"><span data-stu-id="06b0f-114">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="06b0f-115">A GroupBy (formátum) ItemSelectionCondition PropertyName elem.</span><span class="sxs-lookup"><span data-stu-id="06b0f-115">PropertyName Element for ItemSelectionCondition for GroupBy (Format)</span></span>](./propertyname-element-for-itemselectioncondition-for-groupby-format.md)|<span data-ttu-id="06b0f-116">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="06b0f-116">Optional element.</span></span><br /><br /> <span data-ttu-id="06b0f-117">Megadja a .NET-tulajdonság, amely elindítja a feltételt.</span><span class="sxs-lookup"><span data-stu-id="06b0f-117">Specifies the .NET property that triggers the condition.</span></span>|
|[<span data-ttu-id="06b0f-118">ItemSelectionCondition GroupBy (formátum) a scriptblock kulcsszót elem.</span><span class="sxs-lookup"><span data-stu-id="06b0f-118">ScriptBlock Element for ItemSelectionCondition for GroupBy (Format)</span></span>](./scriptblock-element-for-itemselectioncondition-for-groupby-format.md)|<span data-ttu-id="06b0f-119">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="06b0f-119">Optional element.</span></span><br /><br /> <span data-ttu-id="06b0f-120">Megadja a parancsprogramot, amely elindítja a feltétel.</span><span class="sxs-lookup"><span data-stu-id="06b0f-120">Specifies the script that triggers the condition.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="06b0f-121">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="06b0f-121">Parent Elements</span></span>

|<span data-ttu-id="06b0f-122">Elem</span><span class="sxs-lookup"><span data-stu-id="06b0f-122">Element</span></span>|<span data-ttu-id="06b0f-123">Leírás</span><span class="sxs-lookup"><span data-stu-id="06b0f-123">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="06b0f-124">A GroupBy (formátum) CustomItem ExpressionBinding elem.</span><span class="sxs-lookup"><span data-stu-id="06b0f-124">ExpressionBinding Element for CustomItem for GroupBy (Format)</span></span>](./expressionbinding-element-for-customitem-for-groupby-format.md)|<span data-ttu-id="06b0f-125">Határozza meg a vezérlő által megjelenített adatokat.</span><span class="sxs-lookup"><span data-stu-id="06b0f-125">Defines the data that is displayed by the control.</span></span>|

## <a name="remarks"></a><span data-ttu-id="06b0f-126">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="06b0f-126">Remarks</span></span>

<span data-ttu-id="06b0f-127">Egy tulajdonság neve vagy az ehhez a feltételhez parancsfájlt is megadhat, de nem adható meg egyszerre.</span><span class="sxs-lookup"><span data-stu-id="06b0f-127">You can specify one property name or a script for this condition but cannot specify both.</span></span>

## <a name="see-also"></a><span data-ttu-id="06b0f-128">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="06b0f-128">See Also</span></span>

[<span data-ttu-id="06b0f-129">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="06b0f-129">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)

[<span data-ttu-id="06b0f-130">A GroupBy (formátum) CustomItem ExpressionBinding elem.</span><span class="sxs-lookup"><span data-stu-id="06b0f-130">ExpressionBinding Element for CustomItem for GroupBy (Format)</span></span>](./expressionbinding-element-for-customitem-for-groupby-format.md)
