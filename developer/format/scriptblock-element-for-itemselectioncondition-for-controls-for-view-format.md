---
title: ScriptBlock elemet a vezérlők (formátum) nézet ItemSelectionCondition |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: b4191157-bf01-4831-b221-6f8cc581cd53
caps.latest.revision: 6
ms.openlocfilehash: 0cbefbb48427b56d4ae2a5ae27c7726dcfad7b84
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62064713"
---
# <a name="scriptblock-element-for-itemselectioncondition-for-controls-for-view-format"></a><span data-ttu-id="93279-102">A Nézet Vezérlők eleméhez tartozó ItemSelectionCondition ScriptBlock eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="93279-102">ScriptBlock Element for ItemSelectionCondition for Controls for View (Format)</span></span>

<span data-ttu-id="93279-103">Megadja a parancsprogramot, amely elindítja a feltétel.</span><span class="sxs-lookup"><span data-stu-id="93279-103">Specifies the script that triggers the condition.</span></span> <span data-ttu-id="93279-104">Ha ez a parancsfájl kiértékelése `true`, a feltétel nem teljesül, és a vezérlő használatos.</span><span class="sxs-lookup"><span data-stu-id="93279-104">When this script is evaluated to `true`, the condition is met, and the control is used.</span></span> <span data-ttu-id="93279-105">Ez az elem szolgál a nézet által használható vezérlők meghatározásakor.</span><span class="sxs-lookup"><span data-stu-id="93279-105">This element is used when defining controls that can be used by a view.</span></span>

<span data-ttu-id="93279-106">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem vezérlők elem (formátum) vezérlőelem elem vezérlők, a nézet (formátum) CustomControl elem megtekintése (formátum) CustomEntries elemet a vezérlők a vezérlő A nézet (formátum) CustomEntry elem CustomEntries vezérlők, a vezérlők, a vezérlők (formátum) nézet CustomItem megtekintése (formátum) ExpressionBinding elemhez CustomEntry megtekintése (formátum) CustomItem elemhez tartozó CustomControl Vezérlők megtekintése (formátum) ScriptBlock elem a vezérlők (formátum) nézet ItemSelectionCondition ExpressionBinding ItemSelectionCondition eleme</span><span class="sxs-lookup"><span data-stu-id="93279-106">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) Controls Element (Format) Control Element for Controls for View (Format) CustomControl Element for Control for Controls for View (Format) CustomEntries Element for CustomControl for View (Format) CustomEntry Element for CustomEntries for Controls for View (Format) CustomItem Element for CustomEntry for Controls for View (Format) ExpressionBinding Element for CustomItem for Controls for View (Format) ItemSelectionCondition Element of ExpressionBinding for Controls for View (Format) ScriptBlock Element for ItemSelectionCondition for Controls for View (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="93279-107">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="93279-107">Syntax</span></span>

```xml
<ScriptBlock>ScriptToEvaluate</ScriptBlock>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="93279-108">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="93279-108">Attributes and Elements</span></span>

<span data-ttu-id="93279-109">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `ScriptBlock` elemet.</span><span class="sxs-lookup"><span data-stu-id="93279-109">The following sections describe attributes, child elements, and the parent element of the `ScriptBlock` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="93279-110">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="93279-110">Attributes</span></span>

<span data-ttu-id="93279-111">Nincs.</span><span class="sxs-lookup"><span data-stu-id="93279-111">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="93279-112">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="93279-112">Child Elements</span></span>

<span data-ttu-id="93279-113">Nincs.</span><span class="sxs-lookup"><span data-stu-id="93279-113">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="93279-114">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="93279-114">Parent Elements</span></span>

|<span data-ttu-id="93279-115">Elem</span><span class="sxs-lookup"><span data-stu-id="93279-115">Element</span></span>|<span data-ttu-id="93279-116">Leírás</span><span class="sxs-lookup"><span data-stu-id="93279-116">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="93279-117">Nézet (formátum) vezérlők ExpressionBinding ItemSelectionCondition eleme</span><span class="sxs-lookup"><span data-stu-id="93279-117">ItemSelectionCondition Element of ExpressionBinding for Controls for View (Format)</span></span>](./itemselectioncondition-element-for-expressionbinding-for-controls-for-view-format.md)|<span data-ttu-id="93279-118">Határozza meg azt a feltételt, amelyet Pro tento ovládací prvek használandó léteznie kell.</span><span class="sxs-lookup"><span data-stu-id="93279-118">Defines the condition that must exist for this control to be used.</span></span>|

## <a name="text-value"></a><span data-ttu-id="93279-119">A szöveges érték</span><span class="sxs-lookup"><span data-stu-id="93279-119">Text Value</span></span>

<span data-ttu-id="93279-120">Adja meg a parancsfájl, amely ki lesz értékelve.</span><span class="sxs-lookup"><span data-stu-id="93279-120">Specify the script that is evaluated.</span></span>

## <a name="remarks"></a><span data-ttu-id="93279-121">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="93279-121">Remarks</span></span>

<span data-ttu-id="93279-122">Ha ez az elem használata esetén nem adható meg a [PropertyName](./propertyname-element-for-itemselectioncondition-for-controls-for-view-format.md) elemet a kiválasztási feltétel meghatározásakor.</span><span class="sxs-lookup"><span data-stu-id="93279-122">If this element is used, you cannot specify the [PropertyName](./propertyname-element-for-itemselectioncondition-for-controls-for-view-format.md) element when defining the selection condition.</span></span>

## <a name="see-also"></a><span data-ttu-id="93279-123">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="93279-123">See Also</span></span>

[<span data-ttu-id="93279-124">A PropertyName eleme ItemSelectionCondition vezérlők nézet (formátum)</span><span class="sxs-lookup"><span data-stu-id="93279-124">PropertyName Element for ItemSelectionCondition for Controls for View (Format)</span></span>](./propertyname-element-for-itemselectioncondition-for-controls-for-view-format.md)

[<span data-ttu-id="93279-125">Nézet (formátum) vezérlők ExpressionBinding ItemSelectionCondition eleme</span><span class="sxs-lookup"><span data-stu-id="93279-125">ItemSelectionCondition Element of ExpressionBinding for Controls for View (Format)</span></span>](./itemselectioncondition-element-for-expressionbinding-for-controls-for-view-format.md)

[<span data-ttu-id="93279-126">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="93279-126">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
