---
title: A nézet (formátum) CustomControl CustomItem ExpressionBinding eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 7f5ebea5-ee9c-4b90-a116-12a1daa28fc7
caps.latest.revision: 7
ms.openlocfilehash: 226bbea1d7613ad3099e05e8caa9817ff16c1f42
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56850091"
---
# <a name="expressionbinding-element-for-customitem-for-customcontrol-for-view-format"></a><span data-ttu-id="2db39-102">A Nézet CustomControl eleméhez tartozó CustomItem ExpressionBinding eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="2db39-102">ExpressionBinding Element for CustomItem for CustomControl for View (Format)</span></span>

<span data-ttu-id="2db39-103">Határozza meg a vezérlő által megjelenített adatokat.</span><span class="sxs-lookup"><span data-stu-id="2db39-103">Defines the data that is displayed by the control.</span></span> <span data-ttu-id="2db39-104">Ehhez az elemhez használt egyéni vezérlő nézet definiálása.</span><span class="sxs-lookup"><span data-stu-id="2db39-104">This element is used when defining a custom control view.</span></span>

<span data-ttu-id="2db39-105">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézet elem (formátum) CustomControl elem a CustomControl megtekintése (formátum) CustomEntry elemhez tartozó CustomEntries CustomControl a nézet (a nézetben (formátum) CustomEntries elemhez CustomControl CustomItem CustomControl nézet (formátum) esetében a nézet (formátum) ExpressionBinding elemhez tartozó CustomEntry CustomItem eleme formátumban)</span><span class="sxs-lookup"><span data-stu-id="2db39-105">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) CustomControl Element for View (Format) CustomEntries Element for CustomControl for View (Format) CustomEntry Element for CustomEntries for CustomControl for View (Format) CustomItem Element for CustomEntry for CustomControl for View (Format) ExpressionBinding Element for CustomItem for CustomControl for View (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="2db39-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="2db39-106">Syntax</span></span>

```xml
<ExpressionBinding>
  <CustomControl>...</CustomControl>
  <CustomControlName>NameofCommonCustomControl</CustomControlName>
  <EnumerateCollection/>
  <ItemSelectionCondition>...</ItemSelectionCondition>
  <PropertyName>Nameof.NetTypeProperty</PropertyName>
  <ScriptBlock>ScriptToEvaluate></ScriptBlock>
</ExpressionBinding>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="2db39-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="2db39-107">Attributes and Elements</span></span>

<span data-ttu-id="2db39-108">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `ExpressionBinding` elemet.</span><span class="sxs-lookup"><span data-stu-id="2db39-108">The following sections describe attributes, child elements, and the parent element of the `ExpressionBinding` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="2db39-109">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="2db39-109">Attributes</span></span>

<span data-ttu-id="2db39-110">Nincs.</span><span class="sxs-lookup"><span data-stu-id="2db39-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="2db39-111">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="2db39-111">Child Elements</span></span>

|<span data-ttu-id="2db39-112">Elem</span><span class="sxs-lookup"><span data-stu-id="2db39-112">Element</span></span>|<span data-ttu-id="2db39-113">Leírás</span><span class="sxs-lookup"><span data-stu-id="2db39-113">Description</span></span>|
|-------------|-----------------|
|`CustomControl Element`|<span data-ttu-id="2db39-114">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="2db39-114">Optional element.</span></span><br /><br /> <span data-ttu-id="2db39-115">Határozza meg olyan vezérlő, amely használja ezt a vezérlőt.</span><span class="sxs-lookup"><span data-stu-id="2db39-115">Defines a control that is used by this control.</span></span>|
|[<span data-ttu-id="2db39-116">A nézet (formátum) CustomControl ExpressionBinding CustomControlName elem.</span><span class="sxs-lookup"><span data-stu-id="2db39-116">CustomControlName Element for ExpressionBinding for CustomControl for View (Format)</span></span>](./customcontrolname-element-for-expressionbinding-for-customcontrol-for-view-format.md)|<span data-ttu-id="2db39-117">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="2db39-117">Optional element.</span></span><br /><br /> <span data-ttu-id="2db39-118">Megadja egy közös vezérlőelem vagy a nézet nevét.</span><span class="sxs-lookup"><span data-stu-id="2db39-118">Specifies the name of a common control or a view control.</span></span>|
|[<span data-ttu-id="2db39-119">A nézet (formátum) CustomControl ExpressionBinding EnumerateCollection elem.</span><span class="sxs-lookup"><span data-stu-id="2db39-119">EnumerateCollection Element for ExpressionBinding for CustomControl for View (Format)</span></span>](./enumeratecollection-element-for-expressionbinding-for-customcontrol-for-view-format.md)|<span data-ttu-id="2db39-120">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="2db39-120">Optional element.</span></span><br /><br /> <span data-ttu-id="2db39-121">A megadott jelennek meg, hogy a gyűjtemény elemeit.</span><span class="sxs-lookup"><span data-stu-id="2db39-121">Specified that the elements of collections are displayed.</span></span>|
|[<span data-ttu-id="2db39-122">A nézet (formátum) CustomControl ExpressionBinding ItemSelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="2db39-122">ItemSelectionCondition Element for ExpressionBinding for CustomControl for View (Format)</span></span>](./itemselectioncondition-element-for-expressionbinding-for-customcontrol-format.md)|<span data-ttu-id="2db39-123">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="2db39-123">Optional element.</span></span><br /><br /> <span data-ttu-id="2db39-124">Határozza meg azt a feltételt, amelyet Pro tento ovládací prvek használandó léteznie kell.</span><span class="sxs-lookup"><span data-stu-id="2db39-124">Defines the condition that must exist for this control to be used.</span></span>|
|[<span data-ttu-id="2db39-125">A nézet (formátum) CustomControl ExpressionBinding PropertyName elem.</span><span class="sxs-lookup"><span data-stu-id="2db39-125">PropertyName Element for ExpressionBinding for CustomControl for View (Format)</span></span>](./propertyname-element-for-expressionbinding-for-customcontrol-for-view-format.md)|<span data-ttu-id="2db39-126">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="2db39-126">Optional element.</span></span><br /><br /> <span data-ttu-id="2db39-127">Megadja a .NET-tulajdonságot, amelynek értéke megjelenik a vezérlőelem által.</span><span class="sxs-lookup"><span data-stu-id="2db39-127">Specifies the .NET property whose value is displayed by the control.</span></span>|
|[<span data-ttu-id="2db39-128">A nézet (formátum) CustomCustomControl ExpressionBinding ScriptBlock eleme</span><span class="sxs-lookup"><span data-stu-id="2db39-128">ScriptBlock Element for ExpressionBinding for CustomCustomControl for View (Format)</span></span>](./scriptblock-element-for-expressionbinding-for-customcontrol-for-view-format.md)|<span data-ttu-id="2db39-129">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="2db39-129">Optional element.</span></span><br /><br /> <span data-ttu-id="2db39-130">Megadja a parancsprogramot, amelynek értéke megjelenik a vezérlőelem által.</span><span class="sxs-lookup"><span data-stu-id="2db39-130">Specifies the script whose value is displayed by the control.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="2db39-131">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="2db39-131">Parent Elements</span></span>

|<span data-ttu-id="2db39-132">Elem</span><span class="sxs-lookup"><span data-stu-id="2db39-132">Element</span></span>|<span data-ttu-id="2db39-133">Leírás</span><span class="sxs-lookup"><span data-stu-id="2db39-133">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="2db39-134">A nézet (formátum) CustomControl CustomEntry CustomItem elem.</span><span class="sxs-lookup"><span data-stu-id="2db39-134">CustomItem Element for CustomEntry for CustomControl for View (Format)</span></span>](./customitem-element-for-customentry-for-customcontrol-for-view-format.md)|<span data-ttu-id="2db39-135">Határozza meg az egyéni vezérlőt a nézetben megjelenített adatok, és hogyan jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="2db39-135">Defines what data is displayed by the custom control view and how it is displayed.</span></span>|

## <a name="remarks"></a><span data-ttu-id="2db39-136">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="2db39-136">Remarks</span></span>

## <a name="see-also"></a><span data-ttu-id="2db39-137">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="2db39-137">See Also</span></span>

[<span data-ttu-id="2db39-138">A nézet (formátum) CustomControl ExpressionBinding CustomControlName elem.</span><span class="sxs-lookup"><span data-stu-id="2db39-138">CustomControlName Element for ExpressionBinding for CustomControl for View (Format)</span></span>](./customcontrolname-element-for-expressionbinding-for-customcontrol-for-view-format.md)

[<span data-ttu-id="2db39-139">A nézet (formátum) CustomControl ExpressionBinding EnumerateCollection elem.</span><span class="sxs-lookup"><span data-stu-id="2db39-139">EnumerateCollection Element for ExpressionBinding for CustomControl for View (Format)</span></span>](./enumeratecollection-element-for-expressionbinding-for-customcontrol-for-view-format.md)

[<span data-ttu-id="2db39-140">A nézet (formátum) CustomControl ExpressionBinding ItemSelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="2db39-140">ItemSelectionCondition Element for ExpressionBinding for CustomControl for View (Format)</span></span>](./itemselectioncondition-element-for-expressionbinding-for-customcontrol-format.md)

[<span data-ttu-id="2db39-141">A nézet (formátum) CustomControl ExpressionBinding PropertyName elem.</span><span class="sxs-lookup"><span data-stu-id="2db39-141">PropertyName Element for ExpressionBinding for CustomControl for View (Format)</span></span>](./propertyname-element-for-expressionbinding-for-customcontrol-for-view-format.md)

[<span data-ttu-id="2db39-142">A nézet (formátum) CustomControl ExpressionBinding ScriptBlock eleme</span><span class="sxs-lookup"><span data-stu-id="2db39-142">ScriptBlock Element for ExpressionBinding for CustomControl for View (Format)</span></span>](./scriptblock-element-for-expressionbinding-for-customcontrol-for-view-format.md)

[<span data-ttu-id="2db39-143">A nézet (formátum) CustomControl CustomEntry CustomItem elem.</span><span class="sxs-lookup"><span data-stu-id="2db39-143">CustomItem Element for CustomEntry for CustomControl for View (Format)</span></span>](./customitem-element-for-customentry-for-customcontrol-for-view-format.md)

[<span data-ttu-id="2db39-144">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="2db39-144">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
