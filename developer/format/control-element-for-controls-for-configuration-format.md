---
title: Elem vezérlők Configuration (formátum) vezérlőelemet |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: bddf7ffa-04d3-4354-90b9-5e714e096260
caps.latest.revision: 13
ms.openlocfilehash: 26fe417c9ca60dda22bdc23d9d339d40135a0c9b
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56848831"
---
# <a name="control-element-for-controls-for-configuration-format"></a><span data-ttu-id="6742f-102">A Konfiguráció Vezérlők elemének vezérlőeleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="6742f-102">Control Element for Controls for Configuration (Format)</span></span>

<span data-ttu-id="6742f-103">Meghatározza egy közös ellenőrzés, hogy a formázási fájlja és a neve, amellyel hivatkozni a vezérlőelem összes nézet is lehet.</span><span class="sxs-lookup"><span data-stu-id="6742f-103">Defines a common control that can be used by all the views of the formatting file and the name that is used to reference the control.</span></span>

<span data-ttu-id="6742f-104">Konfigurációs elem (formátum) vezérlők elem Configuration (formátum) vezérlőelem elem vezérlők konfiguráció (formátum)</span><span class="sxs-lookup"><span data-stu-id="6742f-104">Configuration Element (Format) Controls Element of Configuration (Format) Control Element for Controls for Configuration (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="6742f-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="6742f-105">Syntax</span></span>

```xml
<Control>
  <Name>NameOfControl</Name>
  <CustomControl>...</CustomControl>
</Control>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="6742f-106">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="6742f-106">Attributes and Elements</span></span>

<span data-ttu-id="6742f-107">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `Control` elemet.</span><span class="sxs-lookup"><span data-stu-id="6742f-107">The following sections describe the attributes, child elements, and the parent element for the `Control` element.</span></span> <span data-ttu-id="6742f-108">Minden gyermek elem csak az egyiket meg kell adnia.</span><span class="sxs-lookup"><span data-stu-id="6742f-108">You must specify only one of each child element.</span></span>

### <a name="attributes"></a><span data-ttu-id="6742f-109">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="6742f-109">Attributes</span></span>

<span data-ttu-id="6742f-110">Nincs.</span><span class="sxs-lookup"><span data-stu-id="6742f-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="6742f-111">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="6742f-111">Child Elements</span></span>

|<span data-ttu-id="6742f-112">Elem</span><span class="sxs-lookup"><span data-stu-id="6742f-112">Element</span></span>|<span data-ttu-id="6742f-113">Leírás</span><span class="sxs-lookup"><span data-stu-id="6742f-113">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="6742f-114">A vezérlési konfiguráció (formátum) vezérlők CustomControl elem</span><span class="sxs-lookup"><span data-stu-id="6742f-114">CustomControl Element for Control for Controls for Configuration (Format)</span></span>](./customcontrol-element-for-control-for-controls-for-configuration-format.md)|<span data-ttu-id="6742f-115">Szükséges eleme.</span><span class="sxs-lookup"><span data-stu-id="6742f-115">Required element.</span></span><br /><br /> <span data-ttu-id="6742f-116">Határozza meg a vezérlő.</span><span class="sxs-lookup"><span data-stu-id="6742f-116">Defines the control.</span></span>|
|[<span data-ttu-id="6742f-117">Name elemet a vezérlési konfiguráció (formátum)</span><span class="sxs-lookup"><span data-stu-id="6742f-117">Name Element for Control for Configuration (Format)</span></span>](./name-element-for-control-for-controls-for-configuration-format.md)|<span data-ttu-id="6742f-118">Szükséges eleme.</span><span class="sxs-lookup"><span data-stu-id="6742f-118">Required element.</span></span><br /><br /> <span data-ttu-id="6742f-119">Megadja a mutató hivatkozás a vezérlő nevét.</span><span class="sxs-lookup"><span data-stu-id="6742f-119">Specifies the name used to reference the control.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="6742f-120">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="6742f-120">Parent Elements</span></span>

|<span data-ttu-id="6742f-121">Elem</span><span class="sxs-lookup"><span data-stu-id="6742f-121">Element</span></span>|<span data-ttu-id="6742f-122">Leírás</span><span class="sxs-lookup"><span data-stu-id="6742f-122">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="6742f-123">Vezérlők elem konfiguráció (formátum)</span><span class="sxs-lookup"><span data-stu-id="6742f-123">Controls Element of Configuration (Format)</span></span>](./controls-element-for-configuration-format.md)|<span data-ttu-id="6742f-124">Határozza meg a Gyakori vezérlők, amelyek az összes nézetben megtekinthetők a formázási fájl, vagy más vezérlőelemeket is használható.</span><span class="sxs-lookup"><span data-stu-id="6742f-124">Defines the common controls that can be used by all views of the formatting file or by other controls.</span></span>|

## <a name="remarks"></a><span data-ttu-id="6742f-125">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="6742f-125">Remarks</span></span>

<span data-ttu-id="6742f-126">Ez a vezérlő neve a következő elemeket lehet hivatkozni:</span><span class="sxs-lookup"><span data-stu-id="6742f-126">The name given to this control can be referenced in the following elements:</span></span>

- [<span data-ttu-id="6742f-127">ExpressionBinding eleme CustomItem (formátum)</span><span class="sxs-lookup"><span data-stu-id="6742f-127">ExpressionBinding Element for CustomItem (Format)</span></span>](./expressionbinding-element-for-customitem-for-controls-for-configuration-format.md)

- [<span data-ttu-id="6742f-128">GroupBy View(Format) elem.</span><span class="sxs-lookup"><span data-stu-id="6742f-128">GroupBy Element for View(Format)</span></span>](./groupby-element-for-view-format.md)

## <a name="see-also"></a><span data-ttu-id="6742f-129">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="6742f-129">See Also</span></span>

[<span data-ttu-id="6742f-130">Vezérlők elem konfiguráció (formátum)</span><span class="sxs-lookup"><span data-stu-id="6742f-130">Controls Element of Configuration (Format)</span></span>](./controls-element-for-configuration-format.md)

[<span data-ttu-id="6742f-131">CustomControl elemet a vezérlési konfiguráció (formátum)</span><span class="sxs-lookup"><span data-stu-id="6742f-131">CustomControl element for Control for Configuration (Format)</span></span>](./customcontrol-element-for-control-for-controls-for-configuration-format.md)

[<span data-ttu-id="6742f-132">ExpressionBinding eleme CustomItem (formátum)</span><span class="sxs-lookup"><span data-stu-id="6742f-132">ExpressionBinding Element for CustomItem (Format)</span></span>](./expressionbinding-element-for-customitem-for-controls-for-configuration-format.md)

[<span data-ttu-id="6742f-133">GroupBy View(Format) elem.</span><span class="sxs-lookup"><span data-stu-id="6742f-133">GroupBy Element for View(Format)</span></span>](./groupby-element-for-view-format.md)

[<span data-ttu-id="6742f-134">A vezérlési konfiguráció (formátum) vezérlők Name elemet</span><span class="sxs-lookup"><span data-stu-id="6742f-134">Name Element for Control for Controls for Configuration (Format)</span></span>](./name-element-for-control-for-controls-for-configuration-format.md)

[<span data-ttu-id="6742f-135">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="6742f-135">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
