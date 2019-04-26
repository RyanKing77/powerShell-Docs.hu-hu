---
title: CustomControlName elemet a vezérlők (formátum) konfiguráció ExpressionBinding |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: c5242935-2782-4d23-84f5-2446b2b7ba83
caps.latest.revision: 8
ms.openlocfilehash: c9abd9f22907b87323c16d603a9f75bb3d375a03
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62066634"
---
# <a name="customcontrolname-element-for-expressionbinding-for-controls-for-configuration-format"></a><span data-ttu-id="ce28c-102">A Konfiguráció Vezérlők eleméhez tartozó ExpressionBinding CustomControlName eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="ce28c-102">CustomControlName Element for ExpressionBinding for Controls for Configuration (Format)</span></span>

<span data-ttu-id="ce28c-103">Megadja egy közös vezérlőelem neve.</span><span class="sxs-lookup"><span data-stu-id="ce28c-103">Specifies the name of a common control.</span></span> <span data-ttu-id="ce28c-104">Ez az elem szolgál egy közös vezérlőelem a formázási fájlban az összes nézetek által használható meghatározásakor.</span><span class="sxs-lookup"><span data-stu-id="ce28c-104">This element is used when defining a common control that can be used by all the views in the formatting file.</span></span>

<span data-ttu-id="ce28c-105">Konfigurációs elem (formátum) vezérlők elem Configuration (formátum) vezérlőelem elem vezérlők, a vezérlő konfigurációs (formátum) CustomEntries elemhez tartozó CustomControl Configuration (a Configuration (formátum) CustomControl elem Formátum) CustomEntry elemet a vezérlők, a Configuration (formátum) CustomItem elemet a vezérlők, a konfiguráció ExpressionBinding elemet a vezérlők, a Configuration (formátum) CustomControlName CustomItem CustomEntry CustomControl Konfiguráció (formátum) vezérlők ExpressionBinding elem.</span><span class="sxs-lookup"><span data-stu-id="ce28c-105">Configuration Element (Format) Controls Element of Configuration (Format) Control Element for Controls for Configuration (Format) CustomControl Element for Control for Configuration (Format) CustomEntries Element for CustomControl for Configuration (Format) CustomEntry Element for CustomControl for Controls for Configuration (Format) CustomItem Element for CustomEntry for Controls for Configuration ExpressionBinding Element for CustomItem for Controls for Configuration (Format) CustomControlName Element for ExpressionBinding for Controls for Configuration (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="ce28c-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="ce28c-106">Syntax</span></span>

```xml
<CustomControlName>NameofCustomControl</CustomControlName>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="ce28c-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="ce28c-107">Attributes and Elements</span></span>

<span data-ttu-id="ce28c-108">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `CustomControlName` elemet.</span><span class="sxs-lookup"><span data-stu-id="ce28c-108">The following sections describe attributes, child elements, and the parent element of the `CustomControlName` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="ce28c-109">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="ce28c-109">Attributes</span></span>

<span data-ttu-id="ce28c-110">Nincs.</span><span class="sxs-lookup"><span data-stu-id="ce28c-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="ce28c-111">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="ce28c-111">Child Elements</span></span>

<span data-ttu-id="ce28c-112">Nincs.</span><span class="sxs-lookup"><span data-stu-id="ce28c-112">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="ce28c-113">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="ce28c-113">Parent Elements</span></span>

|<span data-ttu-id="ce28c-114">Elem</span><span class="sxs-lookup"><span data-stu-id="ce28c-114">Element</span></span>|<span data-ttu-id="ce28c-115">Leírás</span><span class="sxs-lookup"><span data-stu-id="ce28c-115">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="ce28c-116">Konfiguráció (formátum) vezérlők CustomItem ExpressionBinding elem.</span><span class="sxs-lookup"><span data-stu-id="ce28c-116">ExpressionBinding Element for CustomItem for Controls for Configuration (Format)</span></span>](./expressionbinding-element-for-customitem-for-controls-for-configuration-format.md)|<span data-ttu-id="ce28c-117">Határozza meg a vezérlő által megjelenített adatokat.</span><span class="sxs-lookup"><span data-stu-id="ce28c-117">Defines the data that is displayed by the control.</span></span>|

## <a name="text-value"></a><span data-ttu-id="ce28c-118">A szöveges érték</span><span class="sxs-lookup"><span data-stu-id="ce28c-118">Text Value</span></span>

<span data-ttu-id="ce28c-119">Adja meg a vezérlő nevét.</span><span class="sxs-lookup"><span data-stu-id="ce28c-119">Specify the name of the control.</span></span>

## <a name="remarks"></a><span data-ttu-id="ce28c-120">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="ce28c-120">Remarks</span></span>

<span data-ttu-id="ce28c-121">A formázási fájl összes nézetek által használt Gyakori vezérlők hozhat létre, és hozhat létre, amely egy adott nézet által használható vezérlőkre.</span><span class="sxs-lookup"><span data-stu-id="ce28c-121">You can create common controls that can be used by all the views of a formatting file, and you can create view controls that can be used by a specific view.</span></span> <span data-ttu-id="ce28c-122">A következő elemeket adja meg, hogy ezek a vezérlők nevét:</span><span class="sxs-lookup"><span data-stu-id="ce28c-122">The following elements specify the names of these controls:</span></span>

- [<span data-ttu-id="ce28c-123">A vezérlési konfiguráció (formátum) vezérlők Name elemet</span><span class="sxs-lookup"><span data-stu-id="ce28c-123">Name Element for Control for Controls for Configuration (Format)</span></span>](./name-element-for-control-for-controls-for-configuration-format.md)

- [<span data-ttu-id="ce28c-124">Vezérlő (formátum) nézet vezérlők Name elemet</span><span class="sxs-lookup"><span data-stu-id="ce28c-124">Name Element for Control for Controls for View (Format)</span></span>](./name-element-for-control-for-controls-for-view-format.md)

## <a name="see-also"></a><span data-ttu-id="ce28c-125">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="ce28c-125">See Also</span></span>

[<span data-ttu-id="ce28c-126">A vezérlési konfiguráció (formátum) vezérlők Name elemet</span><span class="sxs-lookup"><span data-stu-id="ce28c-126">Name Element for Control for Controls for Configuration (Format)</span></span>](./name-element-for-control-for-controls-for-configuration-format.md)

[<span data-ttu-id="ce28c-127">Vezérlő (formátum) nézet vezérlők Name elemet</span><span class="sxs-lookup"><span data-stu-id="ce28c-127">Name Element for Control for Controls for View (Format)</span></span>](./name-element-for-control-for-controls-for-view-format.md)

[<span data-ttu-id="ce28c-128">Konfiguráció (formátum) vezérlők CustomItem ExpressionBinding elem.</span><span class="sxs-lookup"><span data-stu-id="ce28c-128">ExpressionBinding Element for CustomItem for Controls for Configuration (Format)</span></span>](./expressionbinding-element-for-customitem-for-controls-for-configuration-format.md)

[<span data-ttu-id="ce28c-129">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="ce28c-129">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
