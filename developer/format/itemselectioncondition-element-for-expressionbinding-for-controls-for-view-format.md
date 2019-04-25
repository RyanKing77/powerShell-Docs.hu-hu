---
title: ItemSelectionCondition elemet a vezérlők (formátum) nézet ExpressionBinding |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 82c15014-2440-410d-b02d-b7f1a49240a0
caps.latest.revision: 7
ms.openlocfilehash: 80f375c53c205c793600655fa6031d114871618e
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62065478"
---
# <a name="itemselectioncondition-element-for-expressionbinding-for-controls-for-view-format"></a><span data-ttu-id="783c8-102">A Nézet Vezérlők eleméhez tartozó ExpressionBinding ItemSelectionCondition eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="783c8-102">ItemSelectionCondition Element for ExpressionBinding for Controls for View (Format)</span></span>

<span data-ttu-id="783c8-103">Határozza meg azt a feltételt, amelyet Pro tento ovládací prvek használandó léteznie kell.</span><span class="sxs-lookup"><span data-stu-id="783c8-103">Defines the condition that must exist for this control to be used.</span></span> <span data-ttu-id="783c8-104">Ez az elem szolgál a nézet által használható vezérlők meghatározásakor.</span><span class="sxs-lookup"><span data-stu-id="783c8-104">This element is used when defining controls that can be used by a view.</span></span>

<span data-ttu-id="783c8-105">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem vezérlők elem (formátum) vezérlőelem elem vezérlők, a nézet (formátum) CustomControl elem megtekintése (formátum) CustomEntries elemet a vezérlők a vezérlő A nézet (formátum) CustomEntry elem CustomEntries vezérlők, a vezérlők, a vezérlők (formátum) nézet CustomItem megtekintése (formátum) ExpressionBinding elemhez CustomEntry megtekintése (formátum) CustomItem elemhez tartozó CustomControl Nézet (formátum) vezérlők ExpressionBinding ItemSelectionCondition eleme</span><span class="sxs-lookup"><span data-stu-id="783c8-105">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) Controls Element (Format) Control Element for Controls for View (Format) CustomControl Element for Control for Controls for View (Format) CustomEntries Element for CustomControl for View (Format) CustomEntry Element for CustomEntries for Controls for View (Format) CustomItem Element for CustomEntry for Controls for View (Format) ExpressionBinding Element for CustomItem for Controls for View (Format) ItemSelectionCondition Element of ExpressionBinding for Controls for View (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="783c8-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="783c8-106">Syntax</span></span>

```xml
<ItemSelectionCondition>
  <PropertyName>.NetTypeProperty</PropertyName>
  <ScriptBlock>ScriptToEvaluate</ScriptBlock>
</ItemSelectionCondition>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="783c8-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="783c8-107">Attributes and Elements</span></span>

<span data-ttu-id="783c8-108">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `ItemSelectionCondition` elemet.</span><span class="sxs-lookup"><span data-stu-id="783c8-108">The following sections describe attributes, child elements, and the parent element of the `ItemSelectionCondition` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="783c8-109">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="783c8-109">Attributes</span></span>

<span data-ttu-id="783c8-110">Nincs.</span><span class="sxs-lookup"><span data-stu-id="783c8-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="783c8-111">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="783c8-111">Child Elements</span></span>

|<span data-ttu-id="783c8-112">Elem</span><span class="sxs-lookup"><span data-stu-id="783c8-112">Element</span></span>|<span data-ttu-id="783c8-113">Leírás</span><span class="sxs-lookup"><span data-stu-id="783c8-113">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="783c8-114">A PropertyName eleme ItemSelectionCondition vezérlők nézet (formátum)</span><span class="sxs-lookup"><span data-stu-id="783c8-114">PropertyName Element for ItemSelectionCondition for Controls for View (Format)</span></span>](./propertyname-element-for-itemselectioncondition-for-controls-for-view-format.md)|<span data-ttu-id="783c8-115">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="783c8-115">Optional element.</span></span><br /><br /> <span data-ttu-id="783c8-116">Megadja a .NET-tulajdonság, amely elindítja a feltételt.</span><span class="sxs-lookup"><span data-stu-id="783c8-116">Specifies the .NET property that triggers the condition.</span></span>|
|[<span data-ttu-id="783c8-117">Nézet (formátum) vezérlők ItemSelectionCondition ScriptBlock elem.</span><span class="sxs-lookup"><span data-stu-id="783c8-117">ScriptBlock Element for ItemSelectionCondition for Controls for View (Format)</span></span>](./scriptblock-element-for-itemselectioncondition-for-controls-for-view-format.md)|<span data-ttu-id="783c8-118">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="783c8-118">Optional element.</span></span><br /><br /> <span data-ttu-id="783c8-119">Megadja a parancsprogramot, amely elindítja a feltétel.</span><span class="sxs-lookup"><span data-stu-id="783c8-119">Specifies the script that triggers the condition.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="783c8-120">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="783c8-120">Parent Elements</span></span>

|<span data-ttu-id="783c8-121">Elem</span><span class="sxs-lookup"><span data-stu-id="783c8-121">Element</span></span>|<span data-ttu-id="783c8-122">Leírás</span><span class="sxs-lookup"><span data-stu-id="783c8-122">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="783c8-123">Nézet (formátum) vezérlők CustomItem ExpressionBinding elem.</span><span class="sxs-lookup"><span data-stu-id="783c8-123">ExpressionBinding Element for CustomItem for Controls for View (Format)</span></span>](./expressionbinding-element-for-customitem-for-controls-for-view-format.md)|<span data-ttu-id="783c8-124">Határozza meg a vezérlő által megjelenített adatokat.</span><span class="sxs-lookup"><span data-stu-id="783c8-124">Defines the data that is displayed by the control.</span></span>|

## <a name="remarks"></a><span data-ttu-id="783c8-125">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="783c8-125">Remarks</span></span>

<span data-ttu-id="783c8-126">Egy tulajdonság neve vagy az ehhez a feltételhez parancsfájlt is megadhat, de nem adható meg egyszerre.</span><span class="sxs-lookup"><span data-stu-id="783c8-126">You can specify one property name or a script for this condition but cannot specify both.</span></span>

## <a name="see-also"></a><span data-ttu-id="783c8-127">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="783c8-127">See Also</span></span>

[<span data-ttu-id="783c8-128">A PropertyName eleme ItemSelectionCondition vezérlők nézet (formátum)</span><span class="sxs-lookup"><span data-stu-id="783c8-128">PropertyName Element for ItemSelectionCondition for Controls for View (Format)</span></span>](./propertyname-element-for-itemselectioncondition-for-controls-for-view-format.md)

[<span data-ttu-id="783c8-129">Nézet (formátum) vezérlők ItemSelectionCondition ScriptBlock elem.</span><span class="sxs-lookup"><span data-stu-id="783c8-129">ScriptBlock Element for ItemSelectionCondition for Controls for View (Format)</span></span>](./scriptblock-element-for-itemselectioncondition-for-controls-for-view-format.md)

[<span data-ttu-id="783c8-130">Nézet (formátum) vezérlők CustomItem ExpressionBinding elem.</span><span class="sxs-lookup"><span data-stu-id="783c8-130">ExpressionBinding Element for CustomItem for Controls for View (Format)</span></span>](./expressionbinding-element-for-customitem-for-controls-for-view-format.md)

[<span data-ttu-id="783c8-131">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="783c8-131">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
