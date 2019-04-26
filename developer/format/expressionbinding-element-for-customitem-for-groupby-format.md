---
title: A GroupBy (formátum) CustomItem ExpressionBinding eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 5eae5088-7605-4ef2-a703-faf3e5a5fc94
caps.latest.revision: 8
ms.openlocfilehash: 4714bfd1530585aa80aabc010b86d25bf0c7f9c4
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62065903"
---
# <a name="expressionbinding-element-for-customitem-for-groupby-format"></a><span data-ttu-id="9a090-102">A GroupBy elemhez tartozó CustomItem ExpressionBinding eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="9a090-102">ExpressionBinding Element for CustomItem for GroupBy (Format)</span></span>

<span data-ttu-id="9a090-103">Határozza meg a vezérlő által megjelenített adatokat.</span><span class="sxs-lookup"><span data-stu-id="9a090-103">Defines the data that is displayed by the control.</span></span> <span data-ttu-id="9a090-104">Ez az elem szolgál, hogyan jelenjen meg az objektumok egy új csoportot meghatározásakor.</span><span class="sxs-lookup"><span data-stu-id="9a090-104">This element is used when defining how a new group of objects is displayed.</span></span>

<span data-ttu-id="9a090-105">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem GroupBy elem megtekintése (formátum) CustomControl elem a GroupBy (formátum) CustomEntry elemhez tartozó CustomControl GroupBy (formátum) CustomEntries elemhez GroupBy (formátum) CustomItem elem CustomEntry CustomItem GroupBy (formátum) esetében a GroupBy (formátum) ExpressionBinding elemhez tartozó CustomControl</span><span class="sxs-lookup"><span data-stu-id="9a090-105">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) GroupBy Element for View (Format) CustomControl Element for GroupBy (Format) CustomEntries Element for CustomControl for GroupBy (Format) CustomEntry Element for CustomControl for GroupBy (Format) CustomItem Element for CustomEntry for GroupBy (Format) ExpressionBinding Element for CustomItem for GroupBy (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="9a090-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="9a090-106">Syntax</span></span>

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

## <a name="attributes-and-elements"></a><span data-ttu-id="9a090-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="9a090-107">Attributes and Elements</span></span>

<span data-ttu-id="9a090-108">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `ExpressionBinding` elemet.</span><span class="sxs-lookup"><span data-stu-id="9a090-108">The following sections describe attributes, child elements, and the parent element of the `ExpressionBinding` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="9a090-109">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="9a090-109">Attributes</span></span>

<span data-ttu-id="9a090-110">Nincs.</span><span class="sxs-lookup"><span data-stu-id="9a090-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="9a090-111">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="9a090-111">Child Elements</span></span>

|<span data-ttu-id="9a090-112">Elem</span><span class="sxs-lookup"><span data-stu-id="9a090-112">Element</span></span>|<span data-ttu-id="9a090-113">Leírás</span><span class="sxs-lookup"><span data-stu-id="9a090-113">Description</span></span>|
|-------------|-----------------|
|`CustomControl Element`|<span data-ttu-id="9a090-114">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="9a090-114">Optional element.</span></span><br /><br /> <span data-ttu-id="9a090-115">Határozza meg olyan vezérlő, amely használja ezt a vezérlőt.</span><span class="sxs-lookup"><span data-stu-id="9a090-115">Defines a control that is used by this control.</span></span>|
|[<span data-ttu-id="9a090-116">A GroupBy (formátum) ExpressionBinding CustomControlName elem.</span><span class="sxs-lookup"><span data-stu-id="9a090-116">CustomControlName Element for ExpressionBinding for GroupBy (Format)</span></span>](./customcontrolname-element-for-expressionbinding-for-groupby-format.md)|<span data-ttu-id="9a090-117">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="9a090-117">Optional element.</span></span><br /><br /> <span data-ttu-id="9a090-118">Megadja egy közös vezérlőelem vagy a nézet nevét.</span><span class="sxs-lookup"><span data-stu-id="9a090-118">Specifies the name of a common control or a view control.</span></span>|
|<span data-ttu-id="9a090-119">[A GroupBy (formátum) ExpressionBinding EnumerateCollection eleme](./enumeratecollection-element-for-expressionbinding-for-groupby-format.md)EnumerateCollection eleme ExpressionBinding a GroupBy (formátum)</span><span class="sxs-lookup"><span data-stu-id="9a090-119">[EnumerateCollection Element for ExpressionBinding for GroupBy (Format)](./enumeratecollection-element-for-expressionbinding-for-groupby-format.md)EnumerateCollection Element for ExpressionBinding for GroupBy (Format)</span></span>|<span data-ttu-id="9a090-120">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="9a090-120">Optional element.</span></span><br /><br /> <span data-ttu-id="9a090-121">A megadott jelennek meg, hogy a gyűjtemény elemeit.</span><span class="sxs-lookup"><span data-stu-id="9a090-121">Specified that the elements of collections are displayed.</span></span>|
|[<span data-ttu-id="9a090-122">A GroupBy (formátum) ExpressionBinding ItemSelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="9a090-122">ItemSelectionCondition Element for ExpressionBinding for GroupBy (Format)</span></span>](./itemselectioncondition-element-for-expressionbinding-for-groupby-format.md)|<span data-ttu-id="9a090-123">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="9a090-123">Optional element.</span></span><br /><br /> <span data-ttu-id="9a090-124">Határozza meg azt a feltételt, amelyet Pro tento ovládací prvek használandó léteznie kell.</span><span class="sxs-lookup"><span data-stu-id="9a090-124">Defines the condition that must exist for this control to be used.</span></span>|
|[<span data-ttu-id="9a090-125">A GroupBy (formátum) ExpressionBinding PropertyName elem.</span><span class="sxs-lookup"><span data-stu-id="9a090-125">PropertyName Element for ExpressionBinding for GroupBy (Format)</span></span>](./propertyname-element-for-expressionbinding-for-groupby-format.md)|<span data-ttu-id="9a090-126">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="9a090-126">Optional element.</span></span><br /><br /> <span data-ttu-id="9a090-127">Megadja a .NET-tulajdonságot, amelynek értéke megjelenik a vezérlőelem által.</span><span class="sxs-lookup"><span data-stu-id="9a090-127">Specifies the .NET property whose value is displayed by the control.</span></span>|
|[<span data-ttu-id="9a090-128">ExpressionBinding GroupBy (formátum) a scriptblock kulcsszót elem.</span><span class="sxs-lookup"><span data-stu-id="9a090-128">ScriptBlock Element for ExpressionBinding for GroupBy (Format)</span></span>](./scriptblock-element-for-expressionbinding-for-groupby-format.md)|<span data-ttu-id="9a090-129">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="9a090-129">Optional element.</span></span><br /><br /> <span data-ttu-id="9a090-130">Megadja a parancsprogramot, amelynek értéke megjelenik a vezérlőelem által.</span><span class="sxs-lookup"><span data-stu-id="9a090-130">Specifies the script whose value is displayed by the control.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="9a090-131">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="9a090-131">Parent Elements</span></span>

|<span data-ttu-id="9a090-132">Elem</span><span class="sxs-lookup"><span data-stu-id="9a090-132">Element</span></span>|<span data-ttu-id="9a090-133">Leírás</span><span class="sxs-lookup"><span data-stu-id="9a090-133">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="9a090-134">A GroupBy (formátum) CustomEntry CustomItem elem.</span><span class="sxs-lookup"><span data-stu-id="9a090-134">CustomItem Element for CustomEntry for GroupBy (Format)</span></span>](./customitem-element-for-customentry-for-groupby-format.md)|<span data-ttu-id="9a090-135">Határozza meg az egyéni vezérlőt a nézetben megjelenített adatok, és hogyan jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="9a090-135">Defines what data is displayed by the custom control view and how it is displayed.</span></span>|

## <a name="see-also"></a><span data-ttu-id="9a090-136">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="9a090-136">See Also</span></span>

[<span data-ttu-id="9a090-137">A GroupBy (formátum) ExpressionBinding CustomControlName elem.</span><span class="sxs-lookup"><span data-stu-id="9a090-137">CustomControlName Element for ExpressionBinding for GroupBy (Format)</span></span>](./customcontrolname-element-for-expressionbinding-for-groupby-format.md)

[<span data-ttu-id="9a090-138">A GroupBy (formátum) ExpressionBinding EnumerateCollection elem.</span><span class="sxs-lookup"><span data-stu-id="9a090-138">EnumerateCollection Element for ExpressionBinding for GroupBy (Format)</span></span>](./enumeratecollection-element-for-expressionbinding-for-groupby-format.md)

[<span data-ttu-id="9a090-139">A GroupBy (formátum) ExpressionBinding ItemSelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="9a090-139">ItemSelectionCondition Element for ExpressionBinding for GroupBy (Format)</span></span>](./itemselectioncondition-element-for-expressionbinding-for-groupby-format.md)

[<span data-ttu-id="9a090-140">A GroupBy (formátum) ExpressionBinding PropertyName elem.</span><span class="sxs-lookup"><span data-stu-id="9a090-140">PropertyName Element for ExpressionBinding for GroupBy (Format)</span></span>](./propertyname-element-for-expressionbinding-for-groupby-format.md)

[<span data-ttu-id="9a090-141">ExpressionBinding GroupBy (formátum) a scriptblock kulcsszót elem.</span><span class="sxs-lookup"><span data-stu-id="9a090-141">ScriptBlock Element for ExpressionBinding for GroupBy (Format)</span></span>](./scriptblock-element-for-expressionbinding-for-groupby-format.md)

[<span data-ttu-id="9a090-142">A GroupBy (formátum) CustomEntry CustomItem elem.</span><span class="sxs-lookup"><span data-stu-id="9a090-142">CustomItem Element for CustomEntry for GroupBy (Format)</span></span>](./customitem-element-for-customentry-for-groupby-format.md)

[<span data-ttu-id="9a090-143">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="9a090-143">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
