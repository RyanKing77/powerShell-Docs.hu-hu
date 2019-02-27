---
title: ExpressionBinding elemet a vezérlők (formátum) konfiguráció CustomItem |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: c6649d07-4762-4602-9b4b-d9e2e9e63312
caps.latest.revision: 13
ms.openlocfilehash: 531ff447f8407a737131a38351d7e4c6e7da90fb
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56846206"
---
# <a name="expressionbinding-element-for-customitem-for-controls-for-configuration-format"></a><span data-ttu-id="cba72-102">A Konfiguráció Vezérlők eleméhez tartozó CustomItem ExpressionBinding eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="cba72-102">ExpressionBinding Element for CustomItem for Controls for Configuration (Format)</span></span>

<span data-ttu-id="cba72-103">Határozza meg a vezérlő által megjelenített adatokat.</span><span class="sxs-lookup"><span data-stu-id="cba72-103">Defines the data that is displayed by the control.</span></span> <span data-ttu-id="cba72-104">Ez az elem szolgál egy közös vezérlőelem a formázási fájlban az összes nézetek által használható meghatározásakor.</span><span class="sxs-lookup"><span data-stu-id="cba72-104">This element is used when defining a common control that can be used by all the views in the formatting file.</span></span>

<span data-ttu-id="cba72-105">Konfigurációs elem (formátum) vezérlők elem Configuration (formátum) vezérlőelem elem vezérlők, a vezérlő konfigurációs (formátum) CustomEntries elemhez tartozó CustomControl Configuration (a Configuration (formátum) CustomControl elem Formátum) CustomEntry elemet a vezérlők, a vezérlők, a konfiguráció ExpressionBinding elem CustomItem vezérlők (formátum) konfiguráció esetén a CustomEntry Configuration (formátum) CustomItem elemhez CustomControl</span><span class="sxs-lookup"><span data-stu-id="cba72-105">Configuration Element (Format) Controls Element of Configuration (Format) Control Element for Controls for Configuration (Format) CustomControl Element for Control for Configuration (Format) CustomEntries Element for CustomControl for Configuration (Format) CustomEntry Element for CustomControl for Controls for Configuration (Format) CustomItem Element for CustomEntry for Controls for Configuration ExpressionBinding Element for CustomItem for Controls for Configuration (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="cba72-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="cba72-106">Syntax</span></span>

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

## <a name="attributes-and-elements"></a><span data-ttu-id="cba72-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="cba72-107">Attributes and Elements</span></span>

<span data-ttu-id="cba72-108">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `ExpressionBinding` elemet.</span><span class="sxs-lookup"><span data-stu-id="cba72-108">The following sections describe attributes, child elements, and the parent element of the `ExpressionBinding` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="cba72-109">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="cba72-109">Attributes</span></span>

<span data-ttu-id="cba72-110">Nincs.</span><span class="sxs-lookup"><span data-stu-id="cba72-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="cba72-111">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="cba72-111">Child Elements</span></span>

|<span data-ttu-id="cba72-112">Elem</span><span class="sxs-lookup"><span data-stu-id="cba72-112">Element</span></span>|<span data-ttu-id="cba72-113">Leírás</span><span class="sxs-lookup"><span data-stu-id="cba72-113">Description</span></span>|
|-------------|-----------------|
|`CustomControl Element`|<span data-ttu-id="cba72-114">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="cba72-114">Optional element.</span></span><br /><br /> <span data-ttu-id="cba72-115">Határozza meg olyan vezérlő, amely használja ezt a vezérlőt.</span><span class="sxs-lookup"><span data-stu-id="cba72-115">Defines a control that is used by this control.</span></span>|
|[<span data-ttu-id="cba72-116">Konfiguráció (formátum) vezérlők ExpressionBinding CustomControlName elem.</span><span class="sxs-lookup"><span data-stu-id="cba72-116">CustomControlName Element for ExpressionBinding for Controls for Configuration (Format)</span></span>](./customcontrolname-element-for-expressionbinding-for-controls-for-configuration-format.md)|<span data-ttu-id="cba72-117">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="cba72-117">Optional element.</span></span><br /><br /> <span data-ttu-id="cba72-118">Megadja egy közös vezérlőelem vagy a nézet nevét.</span><span class="sxs-lookup"><span data-stu-id="cba72-118">Specifies the name of a common control or a view control.</span></span>|
|[<span data-ttu-id="cba72-119">Konfiguráció (formátum) vezérlők ExpressionBinding EnumerateCollection elem.</span><span class="sxs-lookup"><span data-stu-id="cba72-119">EnumerateCollection Element for ExpressionBinding for Controls for Configuration (Format)</span></span>](./enumeratecollection-element-for-expressionbinding-for-controls-for-configuration-format.md)|<span data-ttu-id="cba72-120">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="cba72-120">Optional element.</span></span><br /><br /> <span data-ttu-id="cba72-121">A megadott, hogy az elemek a gyűjtemények jelennek meg a vezérlő által.</span><span class="sxs-lookup"><span data-stu-id="cba72-121">Specified that the elements of collections are displayed by the control.</span></span>|
|[<span data-ttu-id="cba72-122">Konfiguráció (formátum) vezérlők ExpressionBinding ItemSelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="cba72-122">ItemSelectionCondition Element for ExpressionBinding for Controls for Configuration (Format)</span></span>](./itemselectioncondition-element-for-expressionbinding-for-controls-for-configuration-format.md)|<span data-ttu-id="cba72-123">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="cba72-123">Optional element.</span></span><br /><br /> <span data-ttu-id="cba72-124">Határozza meg azt a feltételt, amelyet a használt gyakori vezérlőelemnél léteznie kell.</span><span class="sxs-lookup"><span data-stu-id="cba72-124">Defines the condition that must exist for this common control to be used.</span></span>|
|[<span data-ttu-id="cba72-125">Konfiguráció (formátum) vezérlők ExpressionBinding PropertyName elem.</span><span class="sxs-lookup"><span data-stu-id="cba72-125">PropertyName Element for ExpressionBinding for Controls for Configuration (Format)</span></span>](./propertyname-element-for-expressionbinding-for-controls-for-configuration-format.md)|<span data-ttu-id="cba72-126">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="cba72-126">Optional element.</span></span><br /><br /> <span data-ttu-id="cba72-127">Megadja a .NET tulajdonságot, amelynek értéke megjelenik a közös felügyelete által.</span><span class="sxs-lookup"><span data-stu-id="cba72-127">Specifies the .NET property whose value is displayed by the common control.</span></span>|
|[<span data-ttu-id="cba72-128">Konfiguráció (formátum) vezérlők ExpressionBinding ScriptBlock eleme</span><span class="sxs-lookup"><span data-stu-id="cba72-128">ScriptBlock Element for ExpressionBinding for Controls for Configuration (Format)</span></span>](./scriptblock-element-for-expressionbinding-for-controls-for-configuration-format.md)|<span data-ttu-id="cba72-129">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="cba72-129">Optional element.</span></span><br /><br /> <span data-ttu-id="cba72-130">Megadja a parancsprogramot, amelynek értéke megjelenik a közös felügyelete által.</span><span class="sxs-lookup"><span data-stu-id="cba72-130">Specifies the script whose value is displayed by the common control.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="cba72-131">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="cba72-131">Parent Elements</span></span>

|<span data-ttu-id="cba72-132">Elem</span><span class="sxs-lookup"><span data-stu-id="cba72-132">Element</span></span>|<span data-ttu-id="cba72-133">Leírás</span><span class="sxs-lookup"><span data-stu-id="cba72-133">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="cba72-134">Konfiguráció vezérlők CustomEntry CustomItem elem.</span><span class="sxs-lookup"><span data-stu-id="cba72-134">CustomItem Element for CustomEntry for Controls for Configuration</span></span>](./customitem-element-for-customentry-for-controls-for-configuration-format.md)|<span data-ttu-id="cba72-135">Határozza meg az egyéni vezérlőt a nézetben megjelenített adatok, és hogyan jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="cba72-135">Defines what data is displayed by the custom control view and how it is displayed.</span></span>|

## <a name="remarks"></a><span data-ttu-id="cba72-136">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="cba72-136">Remarks</span></span>

## <a name="see-also"></a><span data-ttu-id="cba72-137">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="cba72-137">See Also</span></span>

[<span data-ttu-id="cba72-138">Konfiguráció vezérlők CustomEntry CustomItem elem.</span><span class="sxs-lookup"><span data-stu-id="cba72-138">CustomItem Element for CustomEntry for Controls for Configuration</span></span>](./customitem-element-for-customentry-for-controls-for-configuration-format.md)

[<span data-ttu-id="cba72-139">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="cba72-139">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
