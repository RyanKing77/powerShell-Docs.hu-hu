---
title: ItemSelectionCondition elemet a vezérlők (formátum) konfiguráció ExpressionBinding |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: fd3ddc33-b21c-4464-b3f2-a78dbe0062a8
caps.latest.revision: 8
ms.openlocfilehash: 4865d716ebe0460b662253a3019e93e82428b882
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56850791"
---
# <a name="itemselectioncondition-element-for-expressionbinding-for-controls-for-configuration-format"></a><span data-ttu-id="1713b-102">A Konfiguráció Vezérlők eleméhez tartozó ExpressionBinding ItemSelectionCondition eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="1713b-102">ItemSelectionCondition Element for ExpressionBinding for Controls for Configuration (Format)</span></span>

<span data-ttu-id="1713b-103">Határozza meg azt a feltételt, amelyet Pro tento ovládací prvek használandó léteznie kell.</span><span class="sxs-lookup"><span data-stu-id="1713b-103">Defines the condition that must exist for this control to be used.</span></span> <span data-ttu-id="1713b-104">Ez az elem szolgál egy közös vezérlőelem a formázási fájlban az összes nézetek által használható meghatározásakor.</span><span class="sxs-lookup"><span data-stu-id="1713b-104">This element is used when defining a common control that can be used by all the views in the formatting file.</span></span>

<span data-ttu-id="1713b-105">Konfigurációs elem (formátum) vezérlők elem Configuration (formátum) vezérlőelem elem vezérlők, a vezérlő konfigurációs (formátum) CustomEntries elemhez tartozó CustomControl Configuration (a Configuration (formátum) CustomControl elem Formátum) CustomEntry elemet a vezérlők, a vezérlők, a konfiguráció ExpressionBinding elem CustomItem vezérlők (formátum) konfiguráció esetén a CustomEntry Configuration (formátum) CustomItem elemhez CustomControl Konfiguráció (formátum) vezérlők ExpressionBinding ItemSelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="1713b-105">Configuration Element (Format) Controls Element of Configuration (Format) Control Element for Controls for Configuration (Format) CustomControl Element for Control for Configuration (Format) CustomEntries Element for CustomControl for Configuration (Format) CustomEntry Element for CustomControl for Controls for Configuration (Format) CustomItem Element for CustomEntry for Controls for Configuration ExpressionBinding Element for CustomItem for Controls for Configuration (Format) ItemSelectionCondition Element for ExpressionBinding for Controls for Configuration (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="1713b-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="1713b-106">Syntax</span></span>

```xml
<ItemSelectionCondition>
  <PropertyName>.NetTypeProperty</PropertyName>
  <ScriptBlock>ScriptToEvaluate</ScriptBlock>
</ItemSelectionCondition>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="1713b-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="1713b-107">Attributes and Elements</span></span>

<span data-ttu-id="1713b-108">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `ItemSelectionCondition` elemet.</span><span class="sxs-lookup"><span data-stu-id="1713b-108">The following sections describe attributes, child elements, and the parent element of the `ItemSelectionCondition` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="1713b-109">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="1713b-109">Attributes</span></span>

<span data-ttu-id="1713b-110">Nincs.</span><span class="sxs-lookup"><span data-stu-id="1713b-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="1713b-111">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="1713b-111">Child Elements</span></span>

|<span data-ttu-id="1713b-112">Elem</span><span class="sxs-lookup"><span data-stu-id="1713b-112">Element</span></span>|<span data-ttu-id="1713b-113">Leírás</span><span class="sxs-lookup"><span data-stu-id="1713b-113">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="1713b-114">Konfiguráció (formátum) vezérlők ItemSelectionCondition PropertyName elem.</span><span class="sxs-lookup"><span data-stu-id="1713b-114">PropertyName Element for ItemSelectionCondition for Controls for Configuration (Format)</span></span>](./propertyname-element-for-itemseclectioncondition-for-controls-for-configuration-format.md)|<span data-ttu-id="1713b-115">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="1713b-115">Optional element.</span></span><br /><br /> <span data-ttu-id="1713b-116">Megadja a .NET-tulajdonság, amely elindítja a feltételt.</span><span class="sxs-lookup"><span data-stu-id="1713b-116">Specifies the .NET property that triggers the condition.</span></span>|
|[<span data-ttu-id="1713b-117">Konfiguráció (formátum) vezérlők ItemSelectionCondition ScriptBlock eleme</span><span class="sxs-lookup"><span data-stu-id="1713b-117">ScriptBlock Element for ItemSelectionCondition for Controls for Configuration (Format)</span></span>](./scriptblock-element-for-itemseclectioncondition-for-controls-for-configuration-format.md)|<span data-ttu-id="1713b-118">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="1713b-118">Optional element.</span></span><br /><br /> <span data-ttu-id="1713b-119">Megadja a parancsprogramot, amely elindítja a feltétel.</span><span class="sxs-lookup"><span data-stu-id="1713b-119">Specifies the script that triggers the condition.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="1713b-120">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="1713b-120">Parent Elements</span></span>

|<span data-ttu-id="1713b-121">Elem</span><span class="sxs-lookup"><span data-stu-id="1713b-121">Element</span></span>|<span data-ttu-id="1713b-122">Leírás</span><span class="sxs-lookup"><span data-stu-id="1713b-122">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="1713b-123">Konfiguráció (formátum) vezérlők CustomItem ExpressionBinding elem.</span><span class="sxs-lookup"><span data-stu-id="1713b-123">ExpressionBinding Element for CustomItem for Controls for Configuration (Format)</span></span>](./expressionbinding-element-for-customitem-for-controls-for-configuration-format.md)|<span data-ttu-id="1713b-124">Határozza meg a vezérlő által megjelenített adatokat.</span><span class="sxs-lookup"><span data-stu-id="1713b-124">Defines the data that is displayed by the control.</span></span>|

## <a name="remarks"></a><span data-ttu-id="1713b-125">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="1713b-125">Remarks</span></span>

<span data-ttu-id="1713b-126">Egy tulajdonság neve vagy az ehhez a feltételhez parancsfájlt is megadhat, de nem adható meg egyszerre.</span><span class="sxs-lookup"><span data-stu-id="1713b-126">You can specify one property name or a script for this condition but cannot specify both.</span></span>

## <a name="see-also"></a><span data-ttu-id="1713b-127">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="1713b-127">See Also</span></span>

[<span data-ttu-id="1713b-128">Konfiguráció (formátum) vezérlők ItemSelectionCondition PropertyName elem.</span><span class="sxs-lookup"><span data-stu-id="1713b-128">PropertyName Element for ItemSelectionCondition for Controls for Configuration (Format)</span></span>](./propertyname-element-for-itemseclectioncondition-for-controls-for-configuration-format.md)

[<span data-ttu-id="1713b-129">Konfiguráció (formátum) vezérlők ItemSelectionCondition ScriptBlock eleme</span><span class="sxs-lookup"><span data-stu-id="1713b-129">ScriptBlock Element for ItemSelectionCondition for Controls for Configuration (Format)</span></span>](./scriptblock-element-for-itemseclectioncondition-for-controls-for-configuration-format.md)

[<span data-ttu-id="1713b-130">Konfiguráció (formátum) vezérlők CustomItem ExpressionBinding elem.</span><span class="sxs-lookup"><span data-stu-id="1713b-130">ExpressionBinding Element for CustomItem for Controls for Configuration (Format)</span></span>](./expressionbinding-element-for-customitem-for-controls-for-configuration-format.md)

[<span data-ttu-id="1713b-131">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="1713b-131">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
