---
title: A nézet (formátum) CustomControl ItemSelectionCondition PropertyName eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f2b12006-8d52-486b-91a3-e6224ca80e56
caps.latest.revision: 6
ms.openlocfilehash: 52d0b0816eaef6752220e0c3b1249e5a0e44a3ee
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62064866"
---
# <a name="propertyname-element-for-itemselectioncondition-for-customcontrol-for-view-format"></a><span data-ttu-id="610e8-102">A Nézet CustomControl eleméhez tartozó ItemSelectionCondition PropertyName eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="610e8-102">PropertyName Element for ItemSelectionCondition for CustomControl for View (Format)</span></span>

<span data-ttu-id="610e8-103">Megadja a .NET-tulajdonság, amely elindítja a feltételt.</span><span class="sxs-lookup"><span data-stu-id="610e8-103">Specifies the .NET property that triggers the condition.</span></span> <span data-ttu-id="610e8-104">Ha ez a tulajdonság jelen-e, vagy ha való kiértékelése által `true`, a feltétel nem teljesül, és a vezérlő használatos.</span><span class="sxs-lookup"><span data-stu-id="610e8-104">When this property is present or when it evaluates to `true`, the condition is met, and the control is used.</span></span> <span data-ttu-id="610e8-105">Ehhez az elemhez használt egyéni vezérlő nézet definiálása.</span><span class="sxs-lookup"><span data-stu-id="610e8-105">This element is used when defining a custom control view.</span></span>

<span data-ttu-id="610e8-106">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézet elem (formátum) CustomControl elem (formátum) CustomEntries eleme CustomControl megtekintése (formátum) CustomEntry elem megtekintése (formátum) CustomItem elemhez tartozó CustomEntries számára A nézet (formátum) ItemSelectionCondition elemhez tartozó kifejezés kötésének CustomControl megtekintése (formátum) PropertyName elemhez tartozó ItemSelectionCondition a CustomControl CustomItem a nézet (formátum) ExpressionBinding elemhez CustomEntry CustomControl nézet (formátum</span><span class="sxs-lookup"><span data-stu-id="610e8-106">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) CustomControl Element (Format) CustomEntries Element for CustomControl for View (Format) CustomEntry Element for CustomEntries for View (Format) CustomItem Element for CustomEntry for View (Format) ExpressionBinding Element for CustomItem for CustomControl for View (Format) ItemSelectionCondition Element for Expression Binding for CustomControl for View (Format) PropertyName Element for ItemSelectionCondition for CustomControl for View (Format</span></span>

## <a name="syntax"></a><span data-ttu-id="610e8-107">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="610e8-107">Syntax</span></span>

```xml
<PropertyName>.NetTypeProperty</PropertyName>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="610e8-108">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="610e8-108">Attributes and Elements</span></span>

<span data-ttu-id="610e8-109">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `PropertyName` elemet.</span><span class="sxs-lookup"><span data-stu-id="610e8-109">The following sections describe attributes, child elements, and the parent element of the `PropertyName` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="610e8-110">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="610e8-110">Attributes</span></span>

<span data-ttu-id="610e8-111">Nincs.</span><span class="sxs-lookup"><span data-stu-id="610e8-111">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="610e8-112">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="610e8-112">Child Elements</span></span>

<span data-ttu-id="610e8-113">Nincs.</span><span class="sxs-lookup"><span data-stu-id="610e8-113">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="610e8-114">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="610e8-114">Parent Elements</span></span>

|<span data-ttu-id="610e8-115">Elem</span><span class="sxs-lookup"><span data-stu-id="610e8-115">Element</span></span>|<span data-ttu-id="610e8-116">Leírás</span><span class="sxs-lookup"><span data-stu-id="610e8-116">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="610e8-117">A nézet (formátum) kifejezés CustomControl kötésének ItemSelectionCondition elem</span><span class="sxs-lookup"><span data-stu-id="610e8-117">ItemSelectionCondition Element for Expression Binding for CustomControl for View (Format)</span></span>](./itemselectioncondition-element-for-expressionbinding-for-customcontrol-format.md)|<span data-ttu-id="610e8-118">Határozza meg azt a feltételt, amelyet Pro tento ovládací prvek használandó léteznie kell.</span><span class="sxs-lookup"><span data-stu-id="610e8-118">Defines the condition that must exist for this control to be used.</span></span>|

## <a name="text-value"></a><span data-ttu-id="610e8-119">A szöveges érték</span><span class="sxs-lookup"><span data-stu-id="610e8-119">Text Value</span></span>

<span data-ttu-id="610e8-120">Adja meg a .NET-tulajdonság, amely elindítja a feltétel nevét.</span><span class="sxs-lookup"><span data-stu-id="610e8-120">Specify the name of the .NET property that triggers the condition.</span></span>

## <a name="remarks"></a><span data-ttu-id="610e8-121">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="610e8-121">Remarks</span></span>

<span data-ttu-id="610e8-122">Ha ez az elem használata esetén nem adható meg a [ScriptBlock](./scriptblock-element-for-itemselectioncondition-for-customcontrol-for-view-format.md) elemet a kiválasztási feltétel meghatározásakor.</span><span class="sxs-lookup"><span data-stu-id="610e8-122">If this element is used, you cannot specify the [ScriptBlock](./scriptblock-element-for-itemselectioncondition-for-customcontrol-for-view-format.md) element when defining the selection condition.</span></span>

## <a name="see-also"></a><span data-ttu-id="610e8-123">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="610e8-123">See Also</span></span>

[<span data-ttu-id="610e8-124">A nézet (formátum) CustomControl ItemSelectionCondition ScriptBlock eleme</span><span class="sxs-lookup"><span data-stu-id="610e8-124">ScriptBlock Element for ItemSelectionCondition for CustomControl for View (Format)</span></span>](./scriptblock-element-for-itemselectioncondition-for-customcontrol-for-view-format.md)

[<span data-ttu-id="610e8-125">A nézet (formátum) kifejezés CustomControl kötésének ItemSelectionCondition elem</span><span class="sxs-lookup"><span data-stu-id="610e8-125">ItemSelectionCondition Element for Expression Binding for CustomControl for View (Format)</span></span>](./itemselectioncondition-element-for-expressionbinding-for-customcontrol-format.md)

[<span data-ttu-id="610e8-126">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="610e8-126">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
