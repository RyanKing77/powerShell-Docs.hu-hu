---
title: ScriptBlock elemet a vezérlők (formátum) konfiguráció ItemSeclectionCondition |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 51f7aec9-7b01-4370-84f4-1e58508a851f
caps.latest.revision: 6
ms.openlocfilehash: e92b2dfff07358132c480c47c34279e5365fe400
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56850910"
---
# <a name="scriptblock-element-for-itemseclectioncondition-for-controls-for-configuration-format"></a><span data-ttu-id="8112e-102">A Konfiguráció Vezérlők eleméhez tartozó ItemSelectionCondition ScriptBlock eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="8112e-102">ScriptBlock Element for ItemSeclectionCondition for Controls for Configuration (Format)</span></span>

<span data-ttu-id="8112e-103">Megadja a parancsprogramot, amely elindítja a feltétel.</span><span class="sxs-lookup"><span data-stu-id="8112e-103">Specifies the script that triggers the condition.</span></span> <span data-ttu-id="8112e-104">Ha ez a parancsfájl kiértékelése `true`, a feltétel nem teljesül, és a vezérlő használatos.</span><span class="sxs-lookup"><span data-stu-id="8112e-104">When this script is evaluated to `true`, the condition is met, and the control is used.</span></span> <span data-ttu-id="8112e-105">Ez az elem szolgál egy közös vezérlőelem a formázási fájlban az összes nézetek által használható meghatározásakor.</span><span class="sxs-lookup"><span data-stu-id="8112e-105">This element is used when defining a common control that can be used by all the views in the formatting file.</span></span>

<span data-ttu-id="8112e-106">Konfigurációs elem (formátum) vezérlők elem Configuration (formátum) vezérlőelem elem vezérlők, a vezérlő konfigurációs (formátum) CustomEntries elemhez tartozó CustomControl Configuration (a Configuration (formátum) CustomControl elem Formátum) CustomEntry elemet a vezérlők, a vezérlők, a konfiguráció ExpressionBinding elem CustomItem vezérlők (formátum) konfiguráció esetén a CustomEntry Configuration (formátum) CustomItem elemhez CustomControl Vezérlők ItemSelectionCondition vezérlők (formátum) konfiguráció esetén a Configuration (formátum) ScriptBlock elemhez ExpressionBinding ItemSelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="8112e-106">Configuration Element (Format) Controls Element of Configuration (Format) Control Element for Controls for Configuration (Format) CustomControl Element for Control for Configuration (Format) CustomEntries Element for CustomControl for Configuration (Format) CustomEntry Element for CustomControl for Controls for Configuration (Format) CustomItem Element for CustomEntry for Controls for Configuration ExpressionBinding Element for CustomItem for Controls for Configuration (Format) ItemSelectionCondition Element for ExpressionBinding for Controls for Configuration (Format) ScriptBlock Element for ItemSelectionCondition for Controls for Configuration (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="8112e-107">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="8112e-107">Syntax</span></span>

```xml
<ScriptBlock>ScriptToEvaluate</ScriptBlock>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="8112e-108">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="8112e-108">Attributes and Elements</span></span>

<span data-ttu-id="8112e-109">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `ScriptBlock` elemet.</span><span class="sxs-lookup"><span data-stu-id="8112e-109">The following sections describe attributes, child elements, and the parent element of the `ScriptBlock` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="8112e-110">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="8112e-110">Attributes</span></span>

<span data-ttu-id="8112e-111">Nincs.</span><span class="sxs-lookup"><span data-stu-id="8112e-111">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="8112e-112">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="8112e-112">Child Elements</span></span>

<span data-ttu-id="8112e-113">Nincs.</span><span class="sxs-lookup"><span data-stu-id="8112e-113">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="8112e-114">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="8112e-114">Parent Elements</span></span>

|<span data-ttu-id="8112e-115">Elem</span><span class="sxs-lookup"><span data-stu-id="8112e-115">Element</span></span>|<span data-ttu-id="8112e-116">Leírás</span><span class="sxs-lookup"><span data-stu-id="8112e-116">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="8112e-117">Konfiguráció (formátum) vezérlők ExpressionBinding ItemSelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="8112e-117">ItemSelectionCondition Element for ExpressionBinding for Controls for Configuration (Format)</span></span>](./itemselectioncondition-element-for-expressionbinding-for-controls-for-configuration-format.md)|<span data-ttu-id="8112e-118">Határozza meg azt a feltételt, amelyet Pro tento ovládací prvek használandó léteznie kell.</span><span class="sxs-lookup"><span data-stu-id="8112e-118">Defines the condition that must exist for this control to be used.</span></span>|

## <a name="text-value"></a><span data-ttu-id="8112e-119">Szöveges érték</span><span class="sxs-lookup"><span data-stu-id="8112e-119">Text Value</span></span>

<span data-ttu-id="8112e-120">Adja meg a parancsfájl, amely ki lesz értékelve.</span><span class="sxs-lookup"><span data-stu-id="8112e-120">Specify the script that is evaluated.</span></span>

## <a name="remarks"></a><span data-ttu-id="8112e-121">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="8112e-121">Remarks</span></span>

<span data-ttu-id="8112e-122">Ha ez az elem használata esetén nem adható meg a [PropertyName](./propertyname-element-for-itemseclectioncondition-for-controls-for-configuration-format.md) elemet a kiválasztási feltétel meghatározásakor.</span><span class="sxs-lookup"><span data-stu-id="8112e-122">If this element is used, you cannot specify the [PropertyName](./propertyname-element-for-itemseclectioncondition-for-controls-for-configuration-format.md) element when defining the selection condition.</span></span>

## <a name="see-also"></a><span data-ttu-id="8112e-123">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="8112e-123">See Also</span></span>

[<span data-ttu-id="8112e-124">Konfiguráció (formátum) vezérlők ItemSeclectionCondition PropertyName elem.</span><span class="sxs-lookup"><span data-stu-id="8112e-124">PropertyName Element for ItemSeclectionCondition for Controls for Configuration (Format)</span></span>](./propertyname-element-for-itemseclectioncondition-for-controls-for-configuration-format.md)

[<span data-ttu-id="8112e-125">Konfiguráció (formátum) vezérlők ExpressionBinding ItemSelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="8112e-125">ItemSelectionCondition Element for ExpressionBinding for Controls for Configuration (Format)</span></span>](./itemselectioncondition-element-for-expressionbinding-for-controls-for-configuration-format.md)

[<span data-ttu-id="8112e-126">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="8112e-126">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
