---
title: ExpressionBinding elemet a vezérlők (formátum) nézet CustomItem |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 2b9da6c5-548b-480f-86ae-6de6fecabaca
caps.latest.revision: 8
ms.openlocfilehash: 06089730008839f18c471711a4b4411722f99c38
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62065947"
---
# <a name="expressionbinding-element-for-customitem-for-controls-for-view-format"></a><span data-ttu-id="acb12-102">A Nézet Vezérlők eleméhez tartozó CustomItem ExpressionBinding eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="acb12-102">ExpressionBinding Element for CustomItem for Controls for View (Format)</span></span>

<span data-ttu-id="acb12-103">Határozza meg a vezérlő által megjelenített adatokat.</span><span class="sxs-lookup"><span data-stu-id="acb12-103">Defines the data that is displayed by the control.</span></span> <span data-ttu-id="acb12-104">Ez az elem szolgál a nézet által használható vezérlők meghatározásakor.</span><span class="sxs-lookup"><span data-stu-id="acb12-104">This element is used when defining controls that can be used by a view.</span></span>

<span data-ttu-id="acb12-105">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem vezérlők elem (formátum) vezérlőelem elem vezérlők, a nézet (formátum) CustomControl elem megtekintése (formátum) CustomEntries elemet a vezérlők a vezérlő A nézet (formátum) CustomEntry elem CustomEntries vezérlők, a vezérlők, a vezérlők (formátum) nézet CustomItem megtekintése (formátum) ExpressionBinding elemhez CustomEntry megtekintése (formátum) CustomItem elemhez tartozó CustomControl</span><span class="sxs-lookup"><span data-stu-id="acb12-105">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) Controls Element (Format) Control Element for Controls for View (Format) CustomControl Element for Control for Controls for View (Format) CustomEntries Element for CustomControl for View (Format) CustomEntry Element for CustomEntries for Controls for View (Format) CustomItem Element for CustomEntry for Controls for View (Format) ExpressionBinding Element for CustomItem for Controls for View (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="acb12-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="acb12-106">Syntax</span></span>

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

## <a name="attributes-and-elements"></a><span data-ttu-id="acb12-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="acb12-107">Attributes and Elements</span></span>

<span data-ttu-id="acb12-108">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `ExpressionBinding` elemet.</span><span class="sxs-lookup"><span data-stu-id="acb12-108">The following sections describe attributes, child elements, and the parent element of the `ExpressionBinding` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="acb12-109">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="acb12-109">Attributes</span></span>

<span data-ttu-id="acb12-110">Nincs.</span><span class="sxs-lookup"><span data-stu-id="acb12-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="acb12-111">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="acb12-111">Child Elements</span></span>

|<span data-ttu-id="acb12-112">Elem</span><span class="sxs-lookup"><span data-stu-id="acb12-112">Element</span></span>|<span data-ttu-id="acb12-113">Leírás</span><span class="sxs-lookup"><span data-stu-id="acb12-113">Description</span></span>|
|-------------|-----------------|
|`CustomControl Element`|<span data-ttu-id="acb12-114">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="acb12-114">Optional element.</span></span><br /><br /> <span data-ttu-id="acb12-115">Határozza meg olyan vezérlő, amely használja ezt a vezérlőt.</span><span class="sxs-lookup"><span data-stu-id="acb12-115">Defines a control that is used by this control.</span></span>|
|[<span data-ttu-id="acb12-116">Nézet (formátum) vezérlők ExpressionBinding CustomControlName elem.</span><span class="sxs-lookup"><span data-stu-id="acb12-116">CustomControlName Element for ExpressionBinding for Controls for View (Format)</span></span>](./customcontrolname-element-for-expressionbinding-for-controls-for-view-format.md)|<span data-ttu-id="acb12-117">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="acb12-117">Optional element.</span></span><br /><br /> <span data-ttu-id="acb12-118">Megadja egy közös vezérlőelem vagy a nézet nevét.</span><span class="sxs-lookup"><span data-stu-id="acb12-118">Specifies the name of a common control or a view control.</span></span>|
|[<span data-ttu-id="acb12-119">Nézet (formátum) vezérlők ExpressionBinding EnumerateCollection elem.</span><span class="sxs-lookup"><span data-stu-id="acb12-119">EnumerateCollection Element for ExpressionBinding for Controls for View (Format)</span></span>](./enumeratecollection-element-for-expressionbinding-for-controls-for-view-format.md)|<span data-ttu-id="acb12-120">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="acb12-120">Optional element.</span></span><br /><br /> <span data-ttu-id="acb12-121">Itt adhatja meg, hogy megjelenik-e a gyűjtemény elemeinek.</span><span class="sxs-lookup"><span data-stu-id="acb12-121">Specifies that the elements of collections are displayed.</span></span>|
|[<span data-ttu-id="acb12-122">Nézet (formátum) vezérlők ExpressionBinding ItemSelectionCondition eleme</span><span class="sxs-lookup"><span data-stu-id="acb12-122">ItemSelectionCondition Element of ExpressionBinding for Controls for View (Format)</span></span>](./itemselectioncondition-element-for-expressionbinding-for-controls-for-view-format.md)|<span data-ttu-id="acb12-123">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="acb12-123">Optional element.</span></span><br /><br /> <span data-ttu-id="acb12-124">Határozza meg azt a feltételt, amelyet Pro tento ovládací prvek használandó léteznie kell.</span><span class="sxs-lookup"><span data-stu-id="acb12-124">Defines the condition that must exist for this control to be used.</span></span>|
|[<span data-ttu-id="acb12-125">A PropertyName eleme ExpressionBinding vezérlők nézet (formátum)</span><span class="sxs-lookup"><span data-stu-id="acb12-125">PropertyName Element for ExpressionBinding for Controls for View (Format)</span></span>](./propertyname-element-for-expressionbinding-for-controls-for-view-format.md)|<span data-ttu-id="acb12-126">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="acb12-126">Optional element.</span></span><br /><br /> <span data-ttu-id="acb12-127">Megadja a .NET-tulajdonságot, amelynek értéke megjelenik a vezérlőelem által.</span><span class="sxs-lookup"><span data-stu-id="acb12-127">Specifies the .NET property whose value is displayed by the control.</span></span>|
|[<span data-ttu-id="acb12-128">Nézet (formátum) vezérlők ExpressionBinding ScriptBlock elem.</span><span class="sxs-lookup"><span data-stu-id="acb12-128">ScriptBlock Element for ExpressionBinding for Controls for View (Format)</span></span>](./scriptblock-element-for-expressionbinding-for-controls-for-view-format.md)|<span data-ttu-id="acb12-129">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="acb12-129">Optional element.</span></span><br /><br /> <span data-ttu-id="acb12-130">Megadja a parancsprogramot, amelynek értéke megjelenik a vezérlőelem által.</span><span class="sxs-lookup"><span data-stu-id="acb12-130">Specifies the script whose value is displayed by the control.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="acb12-131">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="acb12-131">Parent Elements</span></span>

|<span data-ttu-id="acb12-132">Elem</span><span class="sxs-lookup"><span data-stu-id="acb12-132">Element</span></span>|<span data-ttu-id="acb12-133">Leírás</span><span class="sxs-lookup"><span data-stu-id="acb12-133">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="acb12-134">Nézet (formátum) vezérlők CustomEntry CustomItem elem.</span><span class="sxs-lookup"><span data-stu-id="acb12-134">CustomItem Element for CustomEntry for Controls for View (Format)</span></span>](./customitem-element-for-customentry-for-controls-for-view-format.md)|<span data-ttu-id="acb12-135">Határozza meg a vezérlő által megjelenített adatokat, és hogyan jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="acb12-135">Defines what data is displayed by the control and how it is displayed.</span></span>|

## <a name="remarks"></a><span data-ttu-id="acb12-136">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="acb12-136">Remarks</span></span>

## <a name="see-also"></a><span data-ttu-id="acb12-137">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="acb12-137">See Also</span></span>

[<span data-ttu-id="acb12-138">Nézet (formátum) vezérlők CustomEntry CustomItem elem.</span><span class="sxs-lookup"><span data-stu-id="acb12-138">CustomItem Element for CustomEntry for Controls for View (Format)</span></span>](./customitem-element-for-customentry-for-controls-for-view-format.md)

[<span data-ttu-id="acb12-139">Nézet (formátum) vezérlők ExpressionBinding CustomControlName elem.</span><span class="sxs-lookup"><span data-stu-id="acb12-139">CustomControlName Element for ExpressionBinding for Controls for View (Format)</span></span>](./customcontrolname-element-for-expressionbinding-for-controls-for-view-format.md)

[<span data-ttu-id="acb12-140">Nézet (formátum) vezérlők ExpressionBinding EnumerateCollection elem.</span><span class="sxs-lookup"><span data-stu-id="acb12-140">EnumerateCollection Element for ExpressionBinding for Controls for View (Format)</span></span>](./enumeratecollection-element-for-expressionbinding-for-controls-for-view-format.md)

[<span data-ttu-id="acb12-141">Nézet (formátum) vezérlők ExpressionBinding ItemSelectionCondition eleme</span><span class="sxs-lookup"><span data-stu-id="acb12-141">ItemSelectionCondition Element of ExpressionBinding for Controls for View (Format)</span></span>](./itemselectioncondition-element-for-expressionbinding-for-controls-for-view-format.md)

[<span data-ttu-id="acb12-142">A PropertyName eleme ExpressionBinding vezérlők nézet (formátum)</span><span class="sxs-lookup"><span data-stu-id="acb12-142">PropertyName Element for ExpressionBinding for Controls for View (Format)</span></span>](./propertyname-element-for-expressionbinding-for-controls-for-view-format.md)

[<span data-ttu-id="acb12-143">Nézet (formátum) vezérlők ExpressionBinding ScriptBlock elem.</span><span class="sxs-lookup"><span data-stu-id="acb12-143">ScriptBlock Element for ExpressionBinding for Controls for View (Format)</span></span>](./scriptblock-element-for-expressionbinding-for-controls-for-view-format.md)

[<span data-ttu-id="acb12-144">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="acb12-144">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
