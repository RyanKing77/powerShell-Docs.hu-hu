---
title: ItemSelectionCondition GroupBy (formátum) a scriptblock kulcsszót eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 58d25835-4636-4c58-9f6c-0332b9318051
caps.latest.revision: 6
ms.openlocfilehash: 4045196e306e766cd805b3e7ae31bfcb3de184ee
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56850273"
---
# <a name="scriptblock-element-for-itemselectioncondition-for-groupby-format"></a><span data-ttu-id="a219d-102">A GroupBy elemhez tartozó ItemSelectionCondition ScriptBlock eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="a219d-102">ScriptBlock Element for ItemSelectionCondition for GroupBy (Format)</span></span>

<span data-ttu-id="a219d-103">Megadja a parancsprogramot, amely elindítja a feltétel.</span><span class="sxs-lookup"><span data-stu-id="a219d-103">Specifies the script that triggers the condition.</span></span> <span data-ttu-id="a219d-104">Ha ez a parancsfájl kiértékelése `true`, a feltétel nem teljesül, és a vezérlő használatos.</span><span class="sxs-lookup"><span data-stu-id="a219d-104">When this script is evaluated to `true`, the condition is met, and the control is used.</span></span> <span data-ttu-id="a219d-105">Ez az elem szolgál, hogyan jelenjen meg az objektumok egy új csoportot meghatározásakor.</span><span class="sxs-lookup"><span data-stu-id="a219d-105">This element is used when defining how a new group of objects is displayed.</span></span>

<span data-ttu-id="a219d-106">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem GroupBy elem megtekintése (formátum) CustomControl elem a GroupBy (formátum) CustomEntry elemhez tartozó CustomControl GroupBy (formátum) CustomEntries elemhez GroupBy (formátum) CustomItem elem CustomEntry CustomItem ExpressionBinding a GroupBy (formátum) ScriptBlock elemhez tartozó GroupBy (formátum) ItemSelectionCondition elemhez tartozó GroupBy (formátum) ExpressionBinding elemhez tartozó CustomControl ItemSelectionCondition a GroupBy (formátum)</span><span class="sxs-lookup"><span data-stu-id="a219d-106">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) GroupBy Element for View (Format) CustomControl Element for GroupBy (Format) CustomEntries Element for CustomControl for GroupBy (Format) CustomEntry Element for CustomControl for GroupBy (Format) CustomItem Element for CustomEntry for GroupBy (Format) ExpressionBinding Element for CustomItem for GroupBy (Format) ItemSelectionCondition Element for ExpressionBinding for GroupBy (Format) ScriptBlock Element for ItemSelectionCondition for GroupBy (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="a219d-107">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="a219d-107">Syntax</span></span>

```xml
<ScriptBlock>ScriptToEvaluate</ScriptBlock>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="a219d-108">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="a219d-108">Attributes and Elements</span></span>

<span data-ttu-id="a219d-109">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `ScriptBlock` elemet.</span><span class="sxs-lookup"><span data-stu-id="a219d-109">The following sections describe attributes, child elements, and the parent element of the `ScriptBlock` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="a219d-110">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="a219d-110">Attributes</span></span>

<span data-ttu-id="a219d-111">Nincs.</span><span class="sxs-lookup"><span data-stu-id="a219d-111">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="a219d-112">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="a219d-112">Child Elements</span></span>

<span data-ttu-id="a219d-113">Nincs.</span><span class="sxs-lookup"><span data-stu-id="a219d-113">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="a219d-114">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="a219d-114">Parent Elements</span></span>

|<span data-ttu-id="a219d-115">Elem</span><span class="sxs-lookup"><span data-stu-id="a219d-115">Element</span></span>|<span data-ttu-id="a219d-116">Leírás</span><span class="sxs-lookup"><span data-stu-id="a219d-116">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="a219d-117">A GroupBy (formátum) ExpressionBinding ItemSelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="a219d-117">ItemSelectionCondition Element for ExpressionBinding for GroupBy (Format)</span></span>](./itemselectioncondition-element-for-expressionbinding-for-groupby-format.md)|<span data-ttu-id="a219d-118">Határozza meg azt a feltételt, amelyet Pro tento ovládací prvek használandó léteznie kell.</span><span class="sxs-lookup"><span data-stu-id="a219d-118">Defines the condition that must exist for this control to be used.</span></span>|

## <a name="text-value"></a><span data-ttu-id="a219d-119">Szöveges érték</span><span class="sxs-lookup"><span data-stu-id="a219d-119">Text Value</span></span>

<span data-ttu-id="a219d-120">Adja meg a parancsfájl, amely ki lesz értékelve.</span><span class="sxs-lookup"><span data-stu-id="a219d-120">Specify the script that is evaluated.</span></span>

## <a name="remarks"></a><span data-ttu-id="a219d-121">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="a219d-121">Remarks</span></span>

<span data-ttu-id="a219d-122">Ha ez az elem használata esetén nem adható meg a [PropertyName](./propertyname-element-for-itemselectioncondition-for-groupby-format.md) elemet a kiválasztási feltétel meghatározásakor.</span><span class="sxs-lookup"><span data-stu-id="a219d-122">If this element is used, you cannot specify the [PropertyName](./propertyname-element-for-itemselectioncondition-for-groupby-format.md) element when defining the selection condition.</span></span>

## <a name="see-also"></a><span data-ttu-id="a219d-123">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="a219d-123">See Also</span></span>

[<span data-ttu-id="a219d-124">A GroupBy (formátum) ExpressionBinding ItemSelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="a219d-124">ItemSelectionCondition Element for ExpressionBinding for GroupBy (Format)</span></span>](./itemselectioncondition-element-for-expressionbinding-for-groupby-format.md)

[<span data-ttu-id="a219d-125">A GroupBy (formátum) ItemSelectionCondition PropertyName elem.</span><span class="sxs-lookup"><span data-stu-id="a219d-125">PropertyName Element for ItemSelectionCondition for GroupBy (Format)</span></span>](./propertyname-element-for-itemselectioncondition-for-groupby-format.md)

[<span data-ttu-id="a219d-126">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="a219d-126">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
