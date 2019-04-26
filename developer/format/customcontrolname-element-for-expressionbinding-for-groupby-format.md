---
title: A GroupBy (formátum) ExpressionBinding CustomControlName eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 9e11da8f-1e75-4d3d-b4c8-b500dec3028e
caps.latest.revision: 6
ms.openlocfilehash: 32f8a71e9818c8c1a052f3b96f442f169c1bda4a
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62066568"
---
# <a name="customcontrolname-element-for-expressionbinding-for-groupby-format"></a><span data-ttu-id="56b7c-102">A GroupBy elem ExpressionBinding CustomControlName eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="56b7c-102">CustomControlName Element for ExpressionBinding for GroupBy (Format)</span></span>

<span data-ttu-id="56b7c-103">Megadja egy közös vezérlőelem vagy a nézet nevét.</span><span class="sxs-lookup"><span data-stu-id="56b7c-103">Specifies the name of a common control or a view control.</span></span> <span data-ttu-id="56b7c-104">Ez az elem szolgál, hogyan jelenjen meg az objektumok egy új csoportot meghatározásakor.</span><span class="sxs-lookup"><span data-stu-id="56b7c-104">This element is used when defining how a new group of objects is displayed.</span></span>

<span data-ttu-id="56b7c-105">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem GroupBy elem megtekintése (formátum) CustomControl elem a GroupBy (formátum) CustomEntry elemhez tartozó CustomControl GroupBy (formátum) CustomEntries elemhez GroupBy (formátum) CustomItem elem CustomEntry CustomItem ExpressionBinding GroupBy (formátum) esetében a GroupBy (formátum) CustomControlName elemhez tartozó GroupBy (formátum) ExpressionBinding elemhez tartozó CustomControl</span><span class="sxs-lookup"><span data-stu-id="56b7c-105">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) GroupBy Element for View (Format) CustomControl Element for GroupBy (Format) CustomEntries Element for CustomControl for GroupBy (Format) CustomEntry Element for CustomControl for GroupBy (Format) CustomItem Element for CustomEntry for GroupBy (Format) ExpressionBinding Element for CustomItem for GroupBy (Format) CustomControlName Element for ExpressionBinding for GroupBy (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="56b7c-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="56b7c-106">Syntax</span></span>

```xml
<CustomControlName>NameofCustomControl</CustomControlName>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="56b7c-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="56b7c-107">Attributes and Elements</span></span>

<span data-ttu-id="56b7c-108">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `CustomControlName` elemet.</span><span class="sxs-lookup"><span data-stu-id="56b7c-108">The following sections describe attributes, child elements, and the parent element of the `CustomControlName` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="56b7c-109">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="56b7c-109">Attributes</span></span>

<span data-ttu-id="56b7c-110">Nincs.</span><span class="sxs-lookup"><span data-stu-id="56b7c-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="56b7c-111">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="56b7c-111">Child Elements</span></span>

<span data-ttu-id="56b7c-112">Nincs.</span><span class="sxs-lookup"><span data-stu-id="56b7c-112">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="56b7c-113">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="56b7c-113">Parent Elements</span></span>

|<span data-ttu-id="56b7c-114">Elem</span><span class="sxs-lookup"><span data-stu-id="56b7c-114">Element</span></span>|<span data-ttu-id="56b7c-115">Leírás</span><span class="sxs-lookup"><span data-stu-id="56b7c-115">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="56b7c-116">A GroupBy (formátum) CustomItem ExpressionBinding elem.</span><span class="sxs-lookup"><span data-stu-id="56b7c-116">ExpressionBinding Element for CustomItem for GroupBy (Format)</span></span>](./expressionbinding-element-for-customitem-for-groupby-format.md)|<span data-ttu-id="56b7c-117">Határozza meg a vezérlő által megjelenített adatokat.</span><span class="sxs-lookup"><span data-stu-id="56b7c-117">Defines the data that is displayed by the control.</span></span>|

## <a name="text-value"></a><span data-ttu-id="56b7c-118">A szöveges érték</span><span class="sxs-lookup"><span data-stu-id="56b7c-118">Text Value</span></span>

<span data-ttu-id="56b7c-119">Adja meg a vezérlő nevét.</span><span class="sxs-lookup"><span data-stu-id="56b7c-119">Specify the name of the control.</span></span>

## <a name="remarks"></a><span data-ttu-id="56b7c-120">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="56b7c-120">Remarks</span></span>

<span data-ttu-id="56b7c-121">A formázási fájl összes nézetek által használt Gyakori vezérlők hozhat létre, és hozhat létre, amely egy adott nézet által használható vezérlőkre.</span><span class="sxs-lookup"><span data-stu-id="56b7c-121">You can create common controls that can be used by all the views of a formatting file, and you can create view controls that can be used by a specific view.</span></span> <span data-ttu-id="56b7c-122">A következő elemeket adja meg, hogy ezek a vezérlők nevét:</span><span class="sxs-lookup"><span data-stu-id="56b7c-122">The following elements specify the names of these controls:</span></span>

- [<span data-ttu-id="56b7c-123">A vezérlési konfiguráció (formátum) vezérlők Name elemet</span><span class="sxs-lookup"><span data-stu-id="56b7c-123">Name Element for Control for Controls for Configuration (Format)</span></span>](./name-element-for-control-for-controls-for-configuration-format.md)

- [<span data-ttu-id="56b7c-124">Vezérlő (formátum) nézet vezérlők Name elemet</span><span class="sxs-lookup"><span data-stu-id="56b7c-124">Name Element for Control for Controls for View (Format)</span></span>](./name-element-for-control-for-controls-for-view-format.md)

## <a name="see-also"></a><span data-ttu-id="56b7c-125">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="56b7c-125">See Also</span></span>

[<span data-ttu-id="56b7c-126">A vezérlési konfiguráció (formátum) vezérlők Name elemet</span><span class="sxs-lookup"><span data-stu-id="56b7c-126">Name Element for Control for Controls for Configuration (Format)</span></span>](./name-element-for-control-for-controls-for-configuration-format.md)

[<span data-ttu-id="56b7c-127">Vezérlő (formátum) nézet vezérlők Name elemet</span><span class="sxs-lookup"><span data-stu-id="56b7c-127">Name Element for Control for Controls for View (Format)</span></span>](./name-element-for-control-for-controls-for-view-format.md)

[<span data-ttu-id="56b7c-128">A GroupBy (formátum) CustomItem ExpressionBinding elem.</span><span class="sxs-lookup"><span data-stu-id="56b7c-128">ExpressionBinding Element for CustomItem for GroupBy (Format)</span></span>](./expressionbinding-element-for-customitem-for-groupby-format.md)

[<span data-ttu-id="56b7c-129">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="56b7c-129">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
