---
title: PropertyName elemet a vezérlők (formátum) nézet ItemSelectionCondition |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ba3955bc-f3a1-4ef6-86ac-80ffc133ad1b
caps.latest.revision: 6
ms.openlocfilehash: 28ad31be4be7be20f1f43ea1b69ad5d294de86f6
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56847949"
---
# <a name="propertyname-element-for-itemselectioncondition-for-controls-for-view-format"></a><span data-ttu-id="40127-102">A Nézet Vezérlők eleméhez tartozó ItemSelectionCondition PropertyName eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="40127-102">PropertyName Element for ItemSelectionCondition for Controls for View (Format)</span></span>

<span data-ttu-id="40127-103">Megadja a .NET-tulajdonság, amely elindítja a feltételt.</span><span class="sxs-lookup"><span data-stu-id="40127-103">Specifies the .NET property that triggers the condition.</span></span> <span data-ttu-id="40127-104">Ha ez a tulajdonság jelen-e, vagy ha való kiértékelése által `true`, a feltétel nem teljesül, és a vezérlő használatos.</span><span class="sxs-lookup"><span data-stu-id="40127-104">When this property is present or when it evaluates to `true`, the condition is met, and the control is used.</span></span> <span data-ttu-id="40127-105">Ez az elem szolgál a nézet által használható vezérlők meghatározásakor.</span><span class="sxs-lookup"><span data-stu-id="40127-105">This element is used when defining controls that can be used by a view.</span></span>

<span data-ttu-id="40127-106">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem vezérlők elem (formátum) vezérlőelem elem vezérlők, a nézet (formátum) CustomControl elem megtekintése (formátum) CustomEntries elemet a vezérlők a vezérlő A nézet (formátum) CustomEntry elem CustomEntries vezérlők, a vezérlők, a vezérlők (formátum) nézet CustomItem megtekintése (formátum) ExpressionBinding elemhez CustomEntry megtekintése (formátum) CustomItem elemhez tartozó CustomControl Vezérlők, a vezérlők (formátum) nézet ItemSelectionCondition megtekintése (formátum) PropertyName elemhez ExpressionBinding ItemSelectionCondition eleme</span><span class="sxs-lookup"><span data-stu-id="40127-106">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) Controls Element (Format) Control Element for Controls for View (Format) CustomControl Element for Control for Controls for View (Format) CustomEntries Element for CustomControl for View (Format) CustomEntry Element for CustomEntries for Controls for View (Format) CustomItem Element for CustomEntry for Controls for View (Format) ExpressionBinding Element for CustomItem for Controls for View (Format) ItemSelectionCondition Element of ExpressionBinding for Controls for View (Format) PropertyName Element for ItemSelectionCondition for Controls for View (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="40127-107">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="40127-107">Syntax</span></span>

```xml
<PropertyName>.NetTypeProperty</PropertyName>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="40127-108">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="40127-108">Attributes and Elements</span></span>

<span data-ttu-id="40127-109">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `PropertyName` elemet.</span><span class="sxs-lookup"><span data-stu-id="40127-109">The following sections describe attributes, child elements, and the parent element of the `PropertyName` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="40127-110">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="40127-110">Attributes</span></span>

<span data-ttu-id="40127-111">Nincs.</span><span class="sxs-lookup"><span data-stu-id="40127-111">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="40127-112">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="40127-112">Child Elements</span></span>

<span data-ttu-id="40127-113">Nincs.</span><span class="sxs-lookup"><span data-stu-id="40127-113">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="40127-114">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="40127-114">Parent Elements</span></span>

|<span data-ttu-id="40127-115">Elem</span><span class="sxs-lookup"><span data-stu-id="40127-115">Element</span></span>|<span data-ttu-id="40127-116">Leírás</span><span class="sxs-lookup"><span data-stu-id="40127-116">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="40127-117">Nézet (formátum) vezérlők ExpressionBinding ItemSelectionCondition eleme</span><span class="sxs-lookup"><span data-stu-id="40127-117">ItemSelectionCondition Element of ExpressionBinding for Controls for View (Format)</span></span>](./itemselectioncondition-element-for-expressionbinding-for-controls-for-view-format.md)|<span data-ttu-id="40127-118">Határozza meg azt a feltételt, amelyet Pro tento ovládací prvek használandó léteznie kell.</span><span class="sxs-lookup"><span data-stu-id="40127-118">Defines the condition that must exist for this control to be used.</span></span>|

## <a name="text-value"></a><span data-ttu-id="40127-119">Szöveges érték</span><span class="sxs-lookup"><span data-stu-id="40127-119">Text Value</span></span>

<span data-ttu-id="40127-120">Adja meg a .NET-tulajdonság, amely elindítja a feltétel nevét.</span><span class="sxs-lookup"><span data-stu-id="40127-120">Specify the name of the .NET property that triggers the condition.</span></span>

## <a name="remarks"></a><span data-ttu-id="40127-121">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="40127-121">Remarks</span></span>

<span data-ttu-id="40127-122">Ha ez az elem használata esetén nem adható meg a [ScriptBlock](./scriptblock-element-for-itemselectioncondition-for-controls-for-view-format.md) elemet a kiválasztási feltétel meghatározásakor.</span><span class="sxs-lookup"><span data-stu-id="40127-122">If this element is used, you cannot specify the [ScriptBlock](./scriptblock-element-for-itemselectioncondition-for-controls-for-view-format.md) element when defining the selection condition.</span></span>

## <a name="see-also"></a><span data-ttu-id="40127-123">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="40127-123">See Also</span></span>

[<span data-ttu-id="40127-124">Nézet (formátum) vezérlők ItemSelectionCondition ScriptBlock elem.</span><span class="sxs-lookup"><span data-stu-id="40127-124">ScriptBlock Element for ItemSelectionCondition for Controls for View (Format)</span></span>](./scriptblock-element-for-itemselectioncondition-for-controls-for-view-format.md)

[<span data-ttu-id="40127-125">Nézet (formátum) vezérlők ExpressionBinding ItemSelectionCondition eleme</span><span class="sxs-lookup"><span data-stu-id="40127-125">ItemSelectionCondition Element of ExpressionBinding for Controls for View (Format)</span></span>](./itemselectioncondition-element-for-expressionbinding-for-controls-for-view-format.md)

[<span data-ttu-id="40127-126">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="40127-126">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
