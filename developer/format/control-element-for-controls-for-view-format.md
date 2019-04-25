---
title: Elem vezérlők megtekintése (formátum) vezérlőelemet |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 1fd53f55-698d-4df5-bb9a-fe28dc3193e1
caps.latest.revision: 11
ms.openlocfilehash: df568ccb36a2646b983622cdf95718dd5cac62c3
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62066770"
---
# <a name="control-element-for-controls-for-view--format"></a><span data-ttu-id="7fb57-102">A Nézet Vezérlők elemének vezérlőeleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="7fb57-102">Control Element for Controls for View  (Format)</span></span>

<span data-ttu-id="7fb57-103">Határozza meg olyan vezérlő, amely a nézet és a neve, amellyel hivatkozni a vezérlő által használható.</span><span class="sxs-lookup"><span data-stu-id="7fb57-103">Defines a control that can be used by the view and the name that is used to reference the control.</span></span>

<span data-ttu-id="7fb57-104">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézet elem (formátum) szabályozza elem (formátum) vezérlőelem elem vezérlők megtekintése (formátum)</span><span class="sxs-lookup"><span data-stu-id="7fb57-104">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) Controls Element (Format) Control Element for Controls for View (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="7fb57-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="7fb57-105">Syntax</span></span>

```xml
<Control>
  <Name>NameOfControl</Name>
  <CustomControl>...</CustomControl>
</Control>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="7fb57-106">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="7fb57-106">Attributes and Elements</span></span>

<span data-ttu-id="7fb57-107">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `Control` elemet.</span><span class="sxs-lookup"><span data-stu-id="7fb57-107">The following sections describe the attributes, child elements, and the parent element of the `Control` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="7fb57-108">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="7fb57-108">Attributes</span></span>

<span data-ttu-id="7fb57-109">Nincs.</span><span class="sxs-lookup"><span data-stu-id="7fb57-109">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="7fb57-110">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="7fb57-110">Child Elements</span></span>

|<span data-ttu-id="7fb57-111">Elem</span><span class="sxs-lookup"><span data-stu-id="7fb57-111">Element</span></span>|<span data-ttu-id="7fb57-112">Leírás</span><span class="sxs-lookup"><span data-stu-id="7fb57-112">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="7fb57-113">Vezérlő (formátum) nézet Name elemet</span><span class="sxs-lookup"><span data-stu-id="7fb57-113">Name Element for Control for View (Format)</span></span>](./name-element-for-control-for-controls-for-view-format.md)|<span data-ttu-id="7fb57-114">Szükséges eleme.</span><span class="sxs-lookup"><span data-stu-id="7fb57-114">Required element.</span></span><br /><br /> <span data-ttu-id="7fb57-115">Megadja a vezérlő nevét.</span><span class="sxs-lookup"><span data-stu-id="7fb57-115">Specifies the name of the control.</span></span>|
|[<span data-ttu-id="7fb57-116">Vezérlő (formátum) nézet vezérlők CustomControl elem</span><span class="sxs-lookup"><span data-stu-id="7fb57-116">CustomControl Element for Control for Controls for View (Format)</span></span>](./customcontrol-element-for-control-for-controls-for-view-format.md)|<span data-ttu-id="7fb57-117">Szükséges eleme.</span><span class="sxs-lookup"><span data-stu-id="7fb57-117">Required element.</span></span><br /><br /> <span data-ttu-id="7fb57-118">Ez a nézet által használt vezérlő határozza meg.</span><span class="sxs-lookup"><span data-stu-id="7fb57-118">Defines the control used by this view.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="7fb57-119">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="7fb57-119">Parent Elements</span></span>

|<span data-ttu-id="7fb57-120">Elem</span><span class="sxs-lookup"><span data-stu-id="7fb57-120">Element</span></span>|<span data-ttu-id="7fb57-121">Leírás</span><span class="sxs-lookup"><span data-stu-id="7fb57-121">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="7fb57-122">Vezérlők elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="7fb57-122">Controls Element (Format)</span></span>](./controls-element-for-view-format.md)|<span data-ttu-id="7fb57-123">Határozza meg a nézet szabályozza, hogy egy adott nézet is lehet.</span><span class="sxs-lookup"><span data-stu-id="7fb57-123">Defines the view controls that can be used by a specific view.</span></span>|

## <a name="remarks"></a><span data-ttu-id="7fb57-124">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="7fb57-124">Remarks</span></span>

<span data-ttu-id="7fb57-125">Ez a vezérlő határozhatja meg a következő elemeket:</span><span class="sxs-lookup"><span data-stu-id="7fb57-125">This control can be specified by the following elements:</span></span>

- [<span data-ttu-id="7fb57-126">Nézet (formátum) vezérlők ExpressionBinding CustomControlName elem.</span><span class="sxs-lookup"><span data-stu-id="7fb57-126">CustomControlName Element for ExpressionBinding for Controls for View (Format)</span></span>](./customcontrolname-element-for-expressionbinding-for-controls-for-view-format.md)

- [<span data-ttu-id="7fb57-127">A nézet (formátum) CustomControl ExpressionBinding CustomControlName elem.</span><span class="sxs-lookup"><span data-stu-id="7fb57-127">CustomControlName Element for ExpressionBinding for CustomControl for View (Format)</span></span>](./customcontrolname-element-for-expressionbinding-for-customcontrol-for-view-format.md)

- [<span data-ttu-id="7fb57-128">A GroupBy (formátum) ExpressionBinding CustomControlName elem.</span><span class="sxs-lookup"><span data-stu-id="7fb57-128">CustomControlName Element for ExpressionBinding for GroupBy (Format)</span></span>](./customcontrolname-element-for-expressionbinding-for-groupby-format.md)

- [<span data-ttu-id="7fb57-129">GroupBy (formátum) CustomControlName elem.</span><span class="sxs-lookup"><span data-stu-id="7fb57-129">CustomControlName Element for GroupBy (Format)</span></span>](./customcontrolname-element-for-groupby-format.md)

## <a name="see-also"></a><span data-ttu-id="7fb57-130">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="7fb57-130">See Also</span></span>

[<span data-ttu-id="7fb57-131">Vezérlő (formátum) nézet vezérlők CustomControl elem</span><span class="sxs-lookup"><span data-stu-id="7fb57-131">CustomControl Element for Control for Controls for View (Format)</span></span>](./customcontrol-element-for-control-for-controls-for-view-format.md)

[<span data-ttu-id="7fb57-132">Nézet (formátum) vezérlők ExpressionBinding CustomControlName elem.</span><span class="sxs-lookup"><span data-stu-id="7fb57-132">CustomControlName Element for ExpressionBinding for Controls for View (Format)</span></span>](./customcontrolname-element-for-expressionbinding-for-controls-for-view-format.md)

[<span data-ttu-id="7fb57-133">A nézet (formátum) CustomControl ExpressionBinding CustomControlName elem.</span><span class="sxs-lookup"><span data-stu-id="7fb57-133">CustomControlName Element for ExpressionBinding for CustomControl for View (Format)</span></span>](./customcontrolname-element-for-expressionbinding-for-customcontrol-for-view-format.md)

[<span data-ttu-id="7fb57-134">A GroupBy (formátum) ExpressionBinding CustomControlName elem.</span><span class="sxs-lookup"><span data-stu-id="7fb57-134">CustomControlName Element for ExpressionBinding for GroupBy (Format)</span></span>](./customcontrolname-element-for-expressionbinding-for-groupby-format.md)

[<span data-ttu-id="7fb57-135">A GroupBy (formátum) ExpressionBinding CustomControlName elem.</span><span class="sxs-lookup"><span data-stu-id="7fb57-135">CustomControlName Element for ExpressionBinding for GroupBy (Format)</span></span>](./customcontrolname-element-for-expressionbinding-for-groupby-format.md)

[<span data-ttu-id="7fb57-136">Vezérlők elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="7fb57-136">Controls Element (Format)</span></span>](./controls-element-for-view-format.md)

[<span data-ttu-id="7fb57-137">Vezérlő (formátum) nézet vezérlők Name elemet</span><span class="sxs-lookup"><span data-stu-id="7fb57-137">Name Element for Control for Controls for View (Format)</span></span>](./name-element-for-control-for-controls-for-view-format.md)

[<span data-ttu-id="7fb57-138">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="7fb57-138">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
