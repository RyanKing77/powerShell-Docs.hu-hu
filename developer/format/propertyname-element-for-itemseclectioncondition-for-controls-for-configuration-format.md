---
title: PropertyName elemet a vezérlők (formátum) konfiguráció ItemSeclectionCondition |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ad8ab181-c559-492e-a0cf-299e381fdcc3
caps.latest.revision: 6
ms.openlocfilehash: ce25789bdfc2679372ca9e42f99dcc6a30ae2def
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56850259"
---
# <a name="propertyname-element-for-itemseclectioncondition-for-controls-for-configuration-format"></a><span data-ttu-id="47956-102">A Konfiguráció Vezérlők eleméhez tartozó ItemSelectionCondition PropertyName eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="47956-102">PropertyName Element for ItemSeclectionCondition for Controls for Configuration (Format)</span></span>

<span data-ttu-id="47956-103">Megadja a .NET-tulajdonság, amely elindítja a feltételt.</span><span class="sxs-lookup"><span data-stu-id="47956-103">Specifies the .NET property that triggers the condition.</span></span> <span data-ttu-id="47956-104">Ha ez a tulajdonság jelen-e, vagy ha való kiértékelése által `true`, a feltétel nem teljesül, és a vezérlő használatos.</span><span class="sxs-lookup"><span data-stu-id="47956-104">When this property is present or when it evaluates to `true`, the condition is met, and the control is used.</span></span> <span data-ttu-id="47956-105">Ez az elem szolgál egy közös vezérlőelem a formázási fájlban az összes nézetek által használható meghatározásakor.</span><span class="sxs-lookup"><span data-stu-id="47956-105">This element is used when defining a common control that can be used by all the views in the formatting file.</span></span>

<span data-ttu-id="47956-106">Konfigurációs elem (formátum) vezérlők elem Configuration (formátum) vezérlőelem elem vezérlők, a vezérlő konfigurációs (formátum) CustomEntries elemhez tartozó CustomControl Configuration (a Configuration (formátum) CustomControl elem Formátum) CustomEntry elemet a vezérlők, a vezérlők, a konfiguráció ExpressionBinding elem CustomItem vezérlők (formátum) konfiguráció esetén a CustomEntry Configuration (formátum) CustomItem elemhez CustomControl Vezérlők ItemSeclectionCondition vezérlők (formátum) konfiguráció esetén a Configuration (formátum) PropertyName elemhez ExpressionBinding ItemSelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="47956-106">Configuration Element (Format) Controls Element of Configuration (Format) Control Element for Controls for Configuration (Format) CustomControl Element for Control for Configuration (Format) CustomEntries Element for CustomControl for Configuration (Format) CustomEntry Element for CustomControl for Controls for Configuration (Format) CustomItem Element for CustomEntry for Controls for Configuration ExpressionBinding Element for CustomItem for Controls for Configuration (Format) ItemSelectionCondition Element for ExpressionBinding for Controls for Configuration (Format) PropertyName Element for ItemSeclectionCondition for Controls for Configuration (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="47956-107">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="47956-107">Syntax</span></span>

```xml
<PropertyName>.NetTypeProperty</PropertyName>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="47956-108">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="47956-108">Attributes and Elements</span></span>

<span data-ttu-id="47956-109">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `PropertyName` elemet.</span><span class="sxs-lookup"><span data-stu-id="47956-109">The following sections describe attributes, child elements, and the parent element of the `PropertyName` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="47956-110">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="47956-110">Attributes</span></span>

<span data-ttu-id="47956-111">Nincs.</span><span class="sxs-lookup"><span data-stu-id="47956-111">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="47956-112">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="47956-112">Child Elements</span></span>

<span data-ttu-id="47956-113">Nincs.</span><span class="sxs-lookup"><span data-stu-id="47956-113">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="47956-114">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="47956-114">Parent Elements</span></span>

|<span data-ttu-id="47956-115">Elem</span><span class="sxs-lookup"><span data-stu-id="47956-115">Element</span></span>|<span data-ttu-id="47956-116">Leírás</span><span class="sxs-lookup"><span data-stu-id="47956-116">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="47956-117">Konfiguráció (formátum) vezérlők ExpressionBinding ItemSelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="47956-117">ItemSelectionCondition Element for ExpressionBinding for Controls for Configuration (Format)</span></span>](./itemselectioncondition-element-for-expressionbinding-for-controls-for-configuration-format.md)|<span data-ttu-id="47956-118">Határozza meg azt a feltételt, amelyet Pro tento ovládací prvek használandó léteznie kell.</span><span class="sxs-lookup"><span data-stu-id="47956-118">Defines the condition that must exist for this control to be used.</span></span>|

## <a name="text-value"></a><span data-ttu-id="47956-119">Szöveges érték</span><span class="sxs-lookup"><span data-stu-id="47956-119">Text Value</span></span>

<span data-ttu-id="47956-120">Adja meg a .NET-tulajdonság, amely elindítja a feltétel nevét.</span><span class="sxs-lookup"><span data-stu-id="47956-120">Specify the name of the .NET property that triggers the condition.</span></span>

## <a name="remarks"></a><span data-ttu-id="47956-121">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="47956-121">Remarks</span></span>

<span data-ttu-id="47956-122">Ha ez az elem használata esetén nem adható meg a [ScriptBlock](./scriptblock-element-for-itemseclectioncondition-for-controls-for-configuration-format.md) elemet a kiválasztási feltétel meghatározásakor.</span><span class="sxs-lookup"><span data-stu-id="47956-122">If this element is used, you cannot specify the [ScriptBlock](./scriptblock-element-for-itemseclectioncondition-for-controls-for-configuration-format.md) element when defining the selection condition.</span></span>

## <a name="see-also"></a><span data-ttu-id="47956-123">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="47956-123">See Also</span></span>

[<span data-ttu-id="47956-124">Konfiguráció (formátum) vezérlők ItemSeclectionCondition ScriptBlock eleme</span><span class="sxs-lookup"><span data-stu-id="47956-124">ScriptBlock Element for ItemSeclectionCondition for Controls for Configuration (Format)</span></span>](./scriptblock-element-for-itemseclectioncondition-for-controls-for-configuration-format.md)

[<span data-ttu-id="47956-125">Konfiguráció (formátum) vezérlők ExpressionBinding ItemSelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="47956-125">ItemSelectionCondition Element for ExpressionBinding for Controls for Configuration (Format)</span></span>](./itemselectioncondition-element-for-expressionbinding-for-controls-for-configuration-format.md)

[<span data-ttu-id="47956-126">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="47956-126">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
