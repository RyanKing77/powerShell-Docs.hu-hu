---
title: A GroupBy (formátum) ItemSelectionCondition PropertyName eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 221cbdc2-f794-4f3a-9d40-bfdd8cba1013
caps.latest.revision: 6
ms.openlocfilehash: aae65789cf5572cbcc9251eca802a2d43065e49f
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56848397"
---
# <a name="propertyname-element-for-itemselectioncondition-for-groupby-format"></a><span data-ttu-id="630e3-102">A GroupBy elemhez tartozó ItemSelectionCondition PropertyName eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="630e3-102">PropertyName Element for ItemSelectionCondition for GroupBy (Format)</span></span>

<span data-ttu-id="630e3-103">Megadja a .NET-tulajdonság, amely elindítja a feltételt.</span><span class="sxs-lookup"><span data-stu-id="630e3-103">Specifies the .NET property that triggers the condition.</span></span> <span data-ttu-id="630e3-104">Ha ez a tulajdonság jelen-e, vagy ha való kiértékelése által `true`, a feltétel nem teljesül, és a vezérlő használatos.</span><span class="sxs-lookup"><span data-stu-id="630e3-104">When this property is present or when it evaluates to `true`, the condition is met, and the control is used.</span></span> <span data-ttu-id="630e3-105">Ez az elem szolgál, hogyan jelenjen meg az objektumok egy új csoportot meghatározásakor.</span><span class="sxs-lookup"><span data-stu-id="630e3-105">This element is used when defining how a new group of objects is displayed.</span></span>

<span data-ttu-id="630e3-106">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem GroupBy elem megtekintése (formátum) CustomControl elem a GroupBy (formátum) CustomEntry elemhez tartozó CustomControl GroupBy (formátum) CustomEntries elemhez GroupBy (formátum) CustomItem elem CustomEntry CustomItem ExpressionBinding a GroupBy (formátum) PropertyName elemhez tartozó GroupBy (formátum) ItemSelectionCondition elemhez tartozó GroupBy (formátum) ExpressionBinding elemhez tartozó CustomControl ItemSelectionCondition a GroupBy (formátum)</span><span class="sxs-lookup"><span data-stu-id="630e3-106">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) GroupBy Element for View (Format) CustomControl Element for GroupBy (Format) CustomEntries Element for CustomControl for GroupBy (Format) CustomEntry Element for CustomControl for GroupBy (Format) CustomItem Element for CustomEntry for GroupBy (Format) ExpressionBinding Element for CustomItem for GroupBy (Format) ItemSelectionCondition Element for ExpressionBinding for GroupBy (Format) PropertyName Element for ItemSelectionCondition for GroupBy (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="630e3-107">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="630e3-107">Syntax</span></span>

```xml
<PropertyName>.NetTypeProperty</PropertyName>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="630e3-108">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="630e3-108">Attributes and Elements</span></span>

<span data-ttu-id="630e3-109">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `PropertyName` elemet.</span><span class="sxs-lookup"><span data-stu-id="630e3-109">The following sections describe attributes, child elements, and the parent element of the `PropertyName` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="630e3-110">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="630e3-110">Attributes</span></span>

<span data-ttu-id="630e3-111">Nincs.</span><span class="sxs-lookup"><span data-stu-id="630e3-111">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="630e3-112">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="630e3-112">Child Elements</span></span>

<span data-ttu-id="630e3-113">Nincs.</span><span class="sxs-lookup"><span data-stu-id="630e3-113">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="630e3-114">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="630e3-114">Parent Elements</span></span>

|<span data-ttu-id="630e3-115">Elem</span><span class="sxs-lookup"><span data-stu-id="630e3-115">Element</span></span>|<span data-ttu-id="630e3-116">Leírás</span><span class="sxs-lookup"><span data-stu-id="630e3-116">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="630e3-117">A GroupBy (formátum) ExpressionBinding ItemSelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="630e3-117">ItemSelectionCondition Element for ExpressionBinding for GroupBy (Format)</span></span>](./itemselectioncondition-element-for-expressionbinding-for-groupby-format.md)|<span data-ttu-id="630e3-118">Határozza meg azt a feltételt, amelyet Pro tento ovládací prvek használandó léteznie kell.</span><span class="sxs-lookup"><span data-stu-id="630e3-118">Defines the condition that must exist for this control to be used.</span></span>|

## <a name="text-value"></a><span data-ttu-id="630e3-119">Szöveges érték</span><span class="sxs-lookup"><span data-stu-id="630e3-119">Text Value</span></span>

<span data-ttu-id="630e3-120">Adja meg a .NET-tulajdonság, amely elindítja a feltétel nevét.</span><span class="sxs-lookup"><span data-stu-id="630e3-120">Specify the name of the .NET property that triggers the condition.</span></span>

## <a name="remarks"></a><span data-ttu-id="630e3-121">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="630e3-121">Remarks</span></span>

<span data-ttu-id="630e3-122">Ha ez az elem használata esetén nem adható meg a [ScriptBlock](./scriptblock-element-for-itemselectioncondition-for-groupby-format.md) elemet a kiválasztási feltétel meghatározásakor.</span><span class="sxs-lookup"><span data-stu-id="630e3-122">If this element is used, you cannot specify the [ScriptBlock](./scriptblock-element-for-itemselectioncondition-for-groupby-format.md) element when defining the selection condition.</span></span>

## <a name="see-also"></a><span data-ttu-id="630e3-123">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="630e3-123">See Also</span></span>

[<span data-ttu-id="630e3-124">ItemSelectionCondition GroupBy (formátum) a scriptblock kulcsszót elem.</span><span class="sxs-lookup"><span data-stu-id="630e3-124">ScriptBlock Element for ItemSelectionCondition for GroupBy (Format)</span></span>](./scriptblock-element-for-itemselectioncondition-for-groupby-format.md)

[<span data-ttu-id="630e3-125">A GroupBy (formátum) ExpressionBinding ItemSelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="630e3-125">ItemSelectionCondition Element for ExpressionBinding for GroupBy (Format)</span></span>](./itemselectioncondition-element-for-expressionbinding-for-groupby-format.md)

[<span data-ttu-id="630e3-126">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="630e3-126">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
