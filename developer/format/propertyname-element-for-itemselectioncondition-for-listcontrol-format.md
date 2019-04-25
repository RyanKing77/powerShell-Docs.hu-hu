---
title: ItemSelectionCondition ListControl (formátum) a PropertyName eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: d5e707ae-3c84-4ceb-ba31-56b3ffde6d6c
caps.latest.revision: 7
ms.openlocfilehash: b15e26e18126f69eee7c3a857f9a461d4bdf5848
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62064747"
---
# <a name="propertyname-element-for-itemselectioncondition-for-listcontrol-format"></a><span data-ttu-id="c3c76-102">A ListControl elemhez tartozó ItemSelectionCondition PropertyName eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="c3c76-102">PropertyName Element for ItemSelectionCondition for ListControl (Format)</span></span>

<span data-ttu-id="c3c76-103">Megadja a .NET-tulajdonság, amely elindítja a feltételt.</span><span class="sxs-lookup"><span data-stu-id="c3c76-103">Specifies the .NET property that triggers the condition.</span></span> <span data-ttu-id="c3c76-104">Ha ez a tulajdonság jelen-e, vagy ha való kiértékelése által `true`, a feltétel nem teljesül, és a nézetet használja.</span><span class="sxs-lookup"><span data-stu-id="c3c76-104">When this property is present or when it evaluates to `true`, the condition is met, and the view is used.</span></span> <span data-ttu-id="c3c76-105">Ez az elem akkor használatos, ha a lista nézet definiálása.</span><span class="sxs-lookup"><span data-stu-id="c3c76-105">This element is used when defining a list view.</span></span>

<span data-ttu-id="c3c76-106">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézet elem (formátum) ListControl elem (formátum) ListEntries elem (formátum) ListEntry elem a ListControl (formátum) ListItem ListEntry a ListControl (formátum) ListItems elemek elemhez ListControl (formátum) ItemSelectionCondition elemhez tartozó ListItem ListControls PropertyName elemhez tartozó ItemSelectionCondition ListControl (formátum) a ListItems elemek elem.</span><span class="sxs-lookup"><span data-stu-id="c3c76-106">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) ListControl Element (Format) ListEntries Element (Format) ListEntry Element for ListControl (Format) ListItems Element for ListEntry for ListControl (Format) ListItem Element for ListItems for ListControl (Format) ItemSelectionCondition Element for ListItem for ListControls PropertyName Element for ItemSelectionCondition for ListControl (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="c3c76-107">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="c3c76-107">Syntax</span></span>

```xml
<PropertyName>.NetTypeProperty</PropertyName>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="c3c76-108">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="c3c76-108">Attributes and Elements</span></span>

<span data-ttu-id="c3c76-109">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a szülő elemei a `PropertyName` elemet.</span><span class="sxs-lookup"><span data-stu-id="c3c76-109">The following sections describe attributes, child elements, and the parent elements of the `PropertyName` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="c3c76-110">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="c3c76-110">Attributes</span></span>

<span data-ttu-id="c3c76-111">Nincs.</span><span class="sxs-lookup"><span data-stu-id="c3c76-111">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="c3c76-112">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="c3c76-112">Child Elements</span></span>

<span data-ttu-id="c3c76-113">Nincs.</span><span class="sxs-lookup"><span data-stu-id="c3c76-113">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="c3c76-114">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="c3c76-114">Parent Elements</span></span>

|<span data-ttu-id="c3c76-115">Elem</span><span class="sxs-lookup"><span data-stu-id="c3c76-115">Element</span></span>|<span data-ttu-id="c3c76-116">Leírás</span><span class="sxs-lookup"><span data-stu-id="c3c76-116">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="c3c76-117">A ListControl (formátum) ListItem ItemSelectionCondition eleme</span><span class="sxs-lookup"><span data-stu-id="c3c76-117">ItemSelectionCondition Element for ListItem for ListControl (Format)</span></span>](./itemselectioncondition-element-for-listitem-for-listcontrol-format.md)||

## <a name="text-value"></a><span data-ttu-id="c3c76-118">A szöveges érték</span><span class="sxs-lookup"><span data-stu-id="c3c76-118">Text Value</span></span>

<span data-ttu-id="c3c76-119">Adja meg, amelynek értéke megjelenik a tulajdonság nevét.</span><span class="sxs-lookup"><span data-stu-id="c3c76-119">Specify the name of the property whose value is displayed.</span></span>

## <a name="remarks"></a><span data-ttu-id="c3c76-120">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="c3c76-120">Remarks</span></span>

<span data-ttu-id="c3c76-121">Ha ez az elem használata esetén nem adható meg a [ScriptBlock](./scriptblock-element-for-itemselectioncondition-for-listcontrol-format.md) elemet a kiválasztási feltétel meghatározásakor.</span><span class="sxs-lookup"><span data-stu-id="c3c76-121">If this element is used, you cannot specify the [ScriptBlock](./scriptblock-element-for-itemselectioncondition-for-listcontrol-format.md) element when defining the selection condition.</span></span>

## <a name="see-also"></a><span data-ttu-id="c3c76-122">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="c3c76-122">See Also</span></span>

[<span data-ttu-id="c3c76-123">ItemSelectionCondition ListIControl (formátum) a scriptblock kulcsszót elem.</span><span class="sxs-lookup"><span data-stu-id="c3c76-123">ScriptBlock Element for ItemSelectionCondition for ListIControl (Format)</span></span>](./scriptblock-element-for-itemselectioncondition-for-listcontrol-format.md)

[<span data-ttu-id="c3c76-124">A ListControl (formátum) ListItem ItemSelectionCondition eleme</span><span class="sxs-lookup"><span data-stu-id="c3c76-124">ItemSelectionCondition Element for ListItem for ListControl (Format)</span></span>](./itemselectioncondition-element-for-listitem-for-listcontrol-format.md)

[<span data-ttu-id="c3c76-125">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="c3c76-125">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
