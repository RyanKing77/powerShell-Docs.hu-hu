---
title: ItemSelectionCondition CustomControl nézet (formátum) a scriptblock kulcsszót eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 946cd2b5-ac37-4a13-bb49-29fbc70ec8d7
caps.latest.revision: 6
ms.openlocfilehash: 0c07ab0e5d04c4056a7e7215bfa55773bfccb41d
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56851176"
---
# <a name="scriptblock-element-for-itemselectioncondition-for-customcontrol-for-view-format"></a><span data-ttu-id="b1c72-102">A Nézet CustomControl eleméhez tartozó ItemSelectionCondition ScriptBlock eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="b1c72-102">ScriptBlock Element for ItemSelectionCondition for CustomControl for View (Format)</span></span>

<span data-ttu-id="b1c72-103">Megadja a parancsprogramot, amely elindítja a feltétel.</span><span class="sxs-lookup"><span data-stu-id="b1c72-103">Specifies the script that triggers the condition.</span></span> <span data-ttu-id="b1c72-104">Ha ez a parancsfájl kiértékelése `true`, a feltétel nem teljesül, és a vezérlő használatos.</span><span class="sxs-lookup"><span data-stu-id="b1c72-104">When this script is evaluated to `true`, the condition is met, and the control is used.</span></span> <span data-ttu-id="b1c72-105">Ehhez az elemhez használt egyéni vezérlő nézet definiálása.</span><span class="sxs-lookup"><span data-stu-id="b1c72-105">This element is used when defining a custom control view.</span></span>

<span data-ttu-id="b1c72-106">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézet elem (formátum) CustomControl elem (formátum) CustomEntries eleme CustomControl megtekintése (formátum) CustomEntry elem megtekintése (formátum) CustomItem elemhez tartozó CustomEntries számára A nézet (formátum) ExpressionBinding elem a CustomItem CustomControl megtekintése (formátum) ScriptBlock elem ItemSelectionCondition az a kifejezés CustomControl kötése a nézet (formátum) ItemSelectionCondition elemhez tartozó CustomEntry CustomControl nézet (formátum)</span><span class="sxs-lookup"><span data-stu-id="b1c72-106">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) CustomControl Element (Format) CustomEntries Element for CustomControl for View (Format) CustomEntry Element for CustomEntries for View (Format) CustomItem Element for CustomEntry for View (Format) ExpressionBinding Element for CustomItem for CustomControl for View (Format) ItemSelectionCondition Element for Expression Binding for CustomControl for View (Format) ScriptBlock Element for ItemSelectionCondition for CustomControl for View (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="b1c72-107">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="b1c72-107">Syntax</span></span>

```xml
<ScriptBlock>ScriptToEvaluate</ScriptBlock>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="b1c72-108">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="b1c72-108">Attributes and Elements</span></span>

<span data-ttu-id="b1c72-109">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `ScriptBlock` elemet.</span><span class="sxs-lookup"><span data-stu-id="b1c72-109">The following sections describe attributes, child elements, and the parent element of the `ScriptBlock` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="b1c72-110">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="b1c72-110">Attributes</span></span>

<span data-ttu-id="b1c72-111">Nincs.</span><span class="sxs-lookup"><span data-stu-id="b1c72-111">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="b1c72-112">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="b1c72-112">Child Elements</span></span>

<span data-ttu-id="b1c72-113">Nincs.</span><span class="sxs-lookup"><span data-stu-id="b1c72-113">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="b1c72-114">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="b1c72-114">Parent Elements</span></span>

|<span data-ttu-id="b1c72-115">Elem</span><span class="sxs-lookup"><span data-stu-id="b1c72-115">Element</span></span>|<span data-ttu-id="b1c72-116">Leírás</span><span class="sxs-lookup"><span data-stu-id="b1c72-116">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="b1c72-117">A nézet (formátum) kifejezés CustomControl kötésének ItemSelectionCondition elem</span><span class="sxs-lookup"><span data-stu-id="b1c72-117">ItemSelectionCondition Element for Expression Binding for CustomControl for View (Format)</span></span>](./itemselectioncondition-element-for-expressionbinding-for-customcontrol-format.md)|<span data-ttu-id="b1c72-118">Határozza meg azt a feltételt, amelyet Pro tento ovládací prvek használandó léteznie kell.</span><span class="sxs-lookup"><span data-stu-id="b1c72-118">Defines the condition that must exist for this control to be used.</span></span>|

## <a name="text-value"></a><span data-ttu-id="b1c72-119">Szöveges érték</span><span class="sxs-lookup"><span data-stu-id="b1c72-119">Text Value</span></span>

<span data-ttu-id="b1c72-120">Adja meg a parancsfájl, amely ki lesz értékelve.</span><span class="sxs-lookup"><span data-stu-id="b1c72-120">Specify the script that is evaluated.</span></span>

## <a name="remarks"></a><span data-ttu-id="b1c72-121">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="b1c72-121">Remarks</span></span>

<span data-ttu-id="b1c72-122">Ha ez az elem használata esetén nem adható meg a [PropertyName](./propertyname-element-for-itemselectioncondition-for-customcontrol-for-view-format.md) elemet a kiválasztási feltétel meghatározásakor.</span><span class="sxs-lookup"><span data-stu-id="b1c72-122">If this element is used, you cannot specify the [PropertyName](./propertyname-element-for-itemselectioncondition-for-customcontrol-for-view-format.md) element when defining the selection condition.</span></span>

## <a name="see-also"></a><span data-ttu-id="b1c72-123">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="b1c72-123">See Also</span></span>

[<span data-ttu-id="b1c72-124">A nézet (formátum) CustomControl ItemSelectionCondition PropertyName elem.</span><span class="sxs-lookup"><span data-stu-id="b1c72-124">PropertyName Element for ItemSelectionCondition for CustomControl for View (Format)</span></span>](./propertyname-element-for-itemselectioncondition-for-customcontrol-for-view-format.md)

[<span data-ttu-id="b1c72-125">A nézet (formátum) kifejezés CustomControl kötésének ItemSelectionCondition elem</span><span class="sxs-lookup"><span data-stu-id="b1c72-125">ItemSelectionCondition Element for Expression Binding for CustomControl for View (Format)</span></span>](./itemselectioncondition-element-for-expressionbinding-for-customcontrol-format.md)

[<span data-ttu-id="b1c72-126">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="b1c72-126">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
