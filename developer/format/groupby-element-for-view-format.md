---
title: GroupBy elem (formátum) nézet |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 67a2b061-2a4a-4ad1-84f9-cdbefb64aaab
caps.latest.revision: 8
ms.openlocfilehash: abb8b91626128b3deaa2db24a9fd8b34a6563410
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56849279"
---
# <a name="groupby-element-for-view-format"></a><span data-ttu-id="21cb8-102">A Nézet GroupBy eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="21cb8-102">GroupBy Element for View (Format)</span></span>

<span data-ttu-id="21cb8-103">Határozza meg, hogyan jelenjen meg az objektumok egy új csoportot.</span><span class="sxs-lookup"><span data-stu-id="21cb8-103">Defines how a new group of objects is displayed.</span></span> <span data-ttu-id="21cb8-104">Ez az elem szolgál egy táblázat, lista, szélesre vagy egyéni vezérlő nézetében meghatározásakor.</span><span class="sxs-lookup"><span data-stu-id="21cb8-104">This element is used when defining a table, list, wide, or custom control view.</span></span>

<span data-ttu-id="21cb8-105">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem GroupBy elem nézet (formátum)</span><span class="sxs-lookup"><span data-stu-id="21cb8-105">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) GroupBy Element for View (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="21cb8-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="21cb8-106">Syntax</span></span>

```xml
<GroupBy>
  <PropertyName>.NetTypeProperty</PropertyName>
  <ScriptBlock>ScriptToEvaluate</ScriptBlock>
  <Label>TextToDisplay</Label>
  <CustomControl>...</CustomControl>
  <CustomControlName>NameOfControl</CustomControlName>
</GroupBy>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="21cb8-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="21cb8-107">Attributes and Elements</span></span>

<span data-ttu-id="21cb8-108">A következő szakaszok ismertetik az attribútumokat, a gyermekelemek és a szülő elemeket.</span><span class="sxs-lookup"><span data-stu-id="21cb8-108">The following sections describe attributes, child elements, and parent elements.</span></span>

### <a name="attributes"></a><span data-ttu-id="21cb8-109">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="21cb8-109">Attributes</span></span>

<span data-ttu-id="21cb8-110">Nincs.</span><span class="sxs-lookup"><span data-stu-id="21cb8-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="21cb8-111">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="21cb8-111">Child Elements</span></span>

|<span data-ttu-id="21cb8-112">Elem</span><span class="sxs-lookup"><span data-stu-id="21cb8-112">Element</span></span>|<span data-ttu-id="21cb8-113">Leírás</span><span class="sxs-lookup"><span data-stu-id="21cb8-113">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="21cb8-114">GroupBy (formátum) CustomControl elem.</span><span class="sxs-lookup"><span data-stu-id="21cb8-114">CustomControl Element for GroupBy (Format)</span></span>](./customcontrol-element-for-groupby-format.md)|<span data-ttu-id="21cb8-115">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="21cb8-115">Optional element.</span></span><br /><br /> <span data-ttu-id="21cb8-116">Határozza meg az egyéni vezérlő, amely az új csoport megjelenítéséhez.</span><span class="sxs-lookup"><span data-stu-id="21cb8-116">Defines the custom control that display new groups.</span></span>|
|[<span data-ttu-id="21cb8-117">GroupBy (formátum) CustomControlName elem.</span><span class="sxs-lookup"><span data-stu-id="21cb8-117">CustomControlName Element for GroupBy (Format)</span></span>](./customcontrolname-element-for-groupby-format.md)|<span data-ttu-id="21cb8-118">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="21cb8-118">Optional element.</span></span><br /><br /> <span data-ttu-id="21cb8-119">Megadja egy olyan vezérlőelem, amellyel megjelenjen az új csoport nevét.</span><span class="sxs-lookup"><span data-stu-id="21cb8-119">Specifies the name of a control that is used to display the new group.</span></span>|
|[<span data-ttu-id="21cb8-120">Címke elemet a GroupBy (formátum)</span><span class="sxs-lookup"><span data-stu-id="21cb8-120">Label Element for GroupBy (Format)</span></span>](./label-element-for-groupby-format.md)|<span data-ttu-id="21cb8-121">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="21cb8-121">Optional element.</span></span><br /><br /> <span data-ttu-id="21cb8-122">Meghatározza a felirat jelenik meg, ha egy új csoportot észlelt.</span><span class="sxs-lookup"><span data-stu-id="21cb8-122">Specifies a label that is displayed when a new group is encountered.</span></span>|
|[<span data-ttu-id="21cb8-123">A PropertyName elemet a GroupBy (formátum)</span><span class="sxs-lookup"><span data-stu-id="21cb8-123">PropertyName Element for GroupBy (Format)</span></span>](./propertyname-element-for-groupby-format.md)|<span data-ttu-id="21cb8-124">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="21cb8-124">Optional element.</span></span><br /><br /> <span data-ttu-id="21cb8-125">Megadja a .NET-tulajdonság a elindul egy új csoportot, amikor annak értéke módosul.</span><span class="sxs-lookup"><span data-stu-id="21cb8-125">Specifies the .NET property the starts a new group whenever its value changes.</span></span>|
|[<span data-ttu-id="21cb8-126">GroupBy (formátum) a scriptblock kulcsszót elem</span><span class="sxs-lookup"><span data-stu-id="21cb8-126">ScriptBlock Element for GroupBy (Format)</span></span>](./scriptblock-element-for-groupby-format.md)|<span data-ttu-id="21cb8-127">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="21cb8-127">Optional element.</span></span><br /><br /> <span data-ttu-id="21cb8-128">Adja meg a parancsfájl, amely elindítja egy új csoportot, amikor annak értéke módosul.</span><span class="sxs-lookup"><span data-stu-id="21cb8-128">Specifies the script that starts a new group whenever its value changes.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="21cb8-129">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="21cb8-129">Parent Elements</span></span>

|<span data-ttu-id="21cb8-130">Elem</span><span class="sxs-lookup"><span data-stu-id="21cb8-130">Element</span></span>|<span data-ttu-id="21cb8-131">Leírás</span><span class="sxs-lookup"><span data-stu-id="21cb8-131">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="21cb8-132">Nézet elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="21cb8-132">View Element (Format)</span></span>](./view-element-format.md)|<span data-ttu-id="21cb8-133">Legalább egy .NET-objektumokat megjelenítő nézet határozza meg.</span><span class="sxs-lookup"><span data-stu-id="21cb8-133">Defines a view that displays one or more .NET objects.</span></span>|

## <a name="remarks"></a><span data-ttu-id="21cb8-134">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="21cb8-134">Remarks</span></span>

<span data-ttu-id="21cb8-135">Határozza meg, hogyan jelenjen meg az objektumok egy új csoportot, amikor meg kell adnia a tulajdonságot vagy parancsfájlt, amely megkezdi az új csoport; azonban mindkettő megadására nincs lehetőség.</span><span class="sxs-lookup"><span data-stu-id="21cb8-135">When defining how a new group of objects is displayed, you must specify the property or script that will start the new group; however, you cannot specify both.</span></span>

## <a name="see-also"></a><span data-ttu-id="21cb8-136">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="21cb8-136">See Also</span></span>

[<span data-ttu-id="21cb8-137">GroupBy (formátum) CustomControlName elem.</span><span class="sxs-lookup"><span data-stu-id="21cb8-137">CustomControlName Element for GroupBy (Format)</span></span>](./customcontrolname-element-for-groupby-format.md)

[<span data-ttu-id="21cb8-138">Címke elemet a GroupBy (formátum)</span><span class="sxs-lookup"><span data-stu-id="21cb8-138">Label Element for GroupBy (Format)</span></span>](./label-element-for-groupby-format.md)

[<span data-ttu-id="21cb8-139">A PropertyName elemet a GroupBy (formátum)</span><span class="sxs-lookup"><span data-stu-id="21cb8-139">PropertyName Element for GroupBy (Format)</span></span>](./propertyname-element-for-groupby-format.md)

[<span data-ttu-id="21cb8-140">GroupBy (formátum) a scriptblock kulcsszót elem</span><span class="sxs-lookup"><span data-stu-id="21cb8-140">ScriptBlock Element for GroupBy (Format)</span></span>](./scriptblock-element-for-groupby-format.md)

[<span data-ttu-id="21cb8-141">Nézet elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="21cb8-141">View Element (Format)</span></span>](./view-element-format.md)

[<span data-ttu-id="21cb8-142">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="21cb8-142">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
