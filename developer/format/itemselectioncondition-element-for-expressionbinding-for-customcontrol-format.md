---
title: CustomControl (formátum) a ExpressionBinding ItemSelectionCondition eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f4bea9d8-27ad-410e-ad48-287f807d3e4e
caps.latest.revision: 7
ms.openlocfilehash: 18b0113c9b7b0895a1093cb0b56cd2d02c74a6c1
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56848341"
---
# <a name="itemselectioncondition-element-for-expressionbinding-for-customcontrol-format"></a><span data-ttu-id="7b6f9-102">A CustomControl elemhez tartozó ExpressionBinding ItemSelectionCondition eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="7b6f9-102">ItemSelectionCondition Element for ExpressionBinding for CustomControl (Format)</span></span>

<span data-ttu-id="7b6f9-103">Határozza meg azt a feltételt, amelyet Pro tento ovládací prvek használandó léteznie kell.</span><span class="sxs-lookup"><span data-stu-id="7b6f9-103">Defines the condition that must exist for this control to be used.</span></span> <span data-ttu-id="7b6f9-104">Van egy vezérlő elemhez megadható kiválasztási feltételek száma nincs korlátozva.</span><span class="sxs-lookup"><span data-stu-id="7b6f9-104">There is no limit to the number of selection conditions that can be specified for a control item.</span></span> <span data-ttu-id="7b6f9-105">Ehhez az elemhez használt egyéni vezérlő nézet definiálása.</span><span class="sxs-lookup"><span data-stu-id="7b6f9-105">This element is used when defining a custom control view.</span></span>

<span data-ttu-id="7b6f9-106">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézet elem (formátum) CustomControl elem (formátum) CustomEntries eleme CustomControl megtekintése (formátum) CustomEntry elem megtekintése (formátum) CustomItem elemhez tartozó CustomEntries számára CustomEntry CustomItem CustomControl megtekintése (formátum) ItemSelectionCondition elemhez tartozó kifejezés kötésének CustomControl nézet (formátum) esetében a nézet (formátum) ExpressionBinding elemhez</span><span class="sxs-lookup"><span data-stu-id="7b6f9-106">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) CustomControl Element (Format) CustomEntries Element for CustomControl for View (Format) CustomEntry Element for CustomEntries for View (Format) CustomItem Element for CustomEntry for View (Format) ExpressionBinding Element for CustomItem for CustomControl for View (Format) ItemSelectionCondition Element for Expression Binding for CustomControl for View (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="7b6f9-107">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="7b6f9-107">Syntax</span></span>

```xml
<ItemSelectionCondition>
  <PropertyName>.NetTypeProperty</PropertyName>
  <ScriptBlock>ScriptToEvaluate</ScriptBlock>
</ItemSelectionCondition>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="7b6f9-108">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="7b6f9-108">Attributes and Elements</span></span>

<span data-ttu-id="7b6f9-109">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `ItemSelectionCondition` elemet.</span><span class="sxs-lookup"><span data-stu-id="7b6f9-109">The following sections describe attributes, child elements, and the parent element of the `ItemSelectionCondition` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="7b6f9-110">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="7b6f9-110">Attributes</span></span>

<span data-ttu-id="7b6f9-111">Nincs.</span><span class="sxs-lookup"><span data-stu-id="7b6f9-111">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="7b6f9-112">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="7b6f9-112">Child Elements</span></span>

|<span data-ttu-id="7b6f9-113">Elem</span><span class="sxs-lookup"><span data-stu-id="7b6f9-113">Element</span></span>|<span data-ttu-id="7b6f9-114">Leírás</span><span class="sxs-lookup"><span data-stu-id="7b6f9-114">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="7b6f9-115">A nézet (formátum CustomControl ItemSelectionCondition PropertyName elem.</span><span class="sxs-lookup"><span data-stu-id="7b6f9-115">PropertyName Element for ItemSelectionCondition for CustomControl for View (Format</span></span>](./propertyname-element-for-itemselectioncondition-for-customcontrol-for-view-format.md)|<span data-ttu-id="7b6f9-116">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="7b6f9-116">Optional element.</span></span><br /><br /> <span data-ttu-id="7b6f9-117">Megadja a .NET-tulajdonság, amely elindítja a feltételt.</span><span class="sxs-lookup"><span data-stu-id="7b6f9-117">Specifies the .NET property that triggers the condition.</span></span>|
|[<span data-ttu-id="7b6f9-118">A nézet (formátum) CustomControl ItemSelectionCondition ScriptBlock eleme</span><span class="sxs-lookup"><span data-stu-id="7b6f9-118">ScriptBlock Element for ItemSelectionCondition for CustomControl for View (Format)</span></span>](./scriptblock-element-for-itemselectioncondition-for-customcontrol-for-view-format.md)|<span data-ttu-id="7b6f9-119">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="7b6f9-119">Optional element.</span></span><br /><br /> <span data-ttu-id="7b6f9-120">Megadja a parancsprogramot, amely elindítja a feltétel.</span><span class="sxs-lookup"><span data-stu-id="7b6f9-120">Specifies the script that triggers the condition.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="7b6f9-121">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="7b6f9-121">Parent Elements</span></span>

|<span data-ttu-id="7b6f9-122">Elem</span><span class="sxs-lookup"><span data-stu-id="7b6f9-122">Element</span></span>|<span data-ttu-id="7b6f9-123">Leírás</span><span class="sxs-lookup"><span data-stu-id="7b6f9-123">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="7b6f9-124">A nézet (formátum) CustomControl CustomItem ExpressionBinding elem.</span><span class="sxs-lookup"><span data-stu-id="7b6f9-124">ExpressionBinding Element for CustomItem for CustomControl for View (Format)</span></span>](./expressionbinding-element-for-customitem-for-customcontrol-for-view-format.md)|<span data-ttu-id="7b6f9-125">Határozza meg a vezérlő által megjelenített adatokat.</span><span class="sxs-lookup"><span data-stu-id="7b6f9-125">Defines the data that is displayed by the control.</span></span>|

## <a name="remarks"></a><span data-ttu-id="7b6f9-126">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="7b6f9-126">Remarks</span></span>

<span data-ttu-id="7b6f9-127">Egy tulajdonság neve vagy az ehhez a feltételhez parancsfájlt is megadhat, de nem adható meg egyszerre.</span><span class="sxs-lookup"><span data-stu-id="7b6f9-127">You can specify one property name or a script for this condition but cannot specify both.</span></span>

## <a name="see-also"></a><span data-ttu-id="7b6f9-128">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="7b6f9-128">See Also</span></span>

[<span data-ttu-id="7b6f9-129">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="7b6f9-129">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)

[<span data-ttu-id="7b6f9-130">A nézet (formátum) CustomControl CustomItem ExpressionBinding elem.</span><span class="sxs-lookup"><span data-stu-id="7b6f9-130">ExpressionBinding Element for CustomItem for CustomControl for View (Format)</span></span>](./expressionbinding-element-for-customitem-for-customcontrol-for-view-format.md)
