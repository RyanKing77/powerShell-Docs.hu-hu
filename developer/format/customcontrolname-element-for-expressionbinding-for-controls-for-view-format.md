---
title: CustomControlName elemet a vezérlők (formátum) nézet ExpressionBinding |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 4b6ee11e-9086-41d2-afd3-42fb9f24da69
caps.latest.revision: 7
ms.openlocfilehash: bf1d57447f9018f1535af14466427aaeabc048f3
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62066651"
---
# <a name="customcontrolname-element-for-expressionbinding-for-controls-for-view-format"></a><span data-ttu-id="4e967-102">A Nézet Vezérlők eleméhez tartozó ExpressionBinding CustomControlName eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="4e967-102">CustomControlName Element for ExpressionBinding for Controls for View (Format)</span></span>

<span data-ttu-id="4e967-103">Megadja egy közös vezérlőelem vagy a nézet nevét.</span><span class="sxs-lookup"><span data-stu-id="4e967-103">Specifies the name of a common control or a view control.</span></span> <span data-ttu-id="4e967-104">Ez az elem szolgál a nézet által használható vezérlők meghatározásakor.</span><span class="sxs-lookup"><span data-stu-id="4e967-104">This element is used when defining controls that can be used by a view.</span></span>

<span data-ttu-id="4e967-105">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem vezérlők elem (formátum) vezérlőelem elem vezérlők, a nézet (formátum) CustomControl elem megtekintése (formátum) CustomEntries elemet a vezérlők a vezérlő A nézet (formátum) CustomEntry elem CustomEntries vezérlők, a vezérlők, a nézet (formátum) ExpressionBinding elemet a vezérlők, a nézet (formátum) CustomControlName CustomItem CustomEntry megtekintése (formátum) CustomItem elemhez tartozó CustomControl Elem a ExpressionBindine vezérlők nézet (formátum)</span><span class="sxs-lookup"><span data-stu-id="4e967-105">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) Controls Element (Format) Control Element for Controls for View (Format) CustomControl Element for Control for Controls for View (Format) CustomEntries Element for CustomControl for View (Format) CustomEntry Element for CustomEntries for Controls for View (Format) CustomItem Element for CustomEntry for Controls for View (Format) ExpressionBinding Element for CustomItem for Controls for View (Format) CustomControlName Element for ExpressionBindine for Controls for View (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="4e967-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="4e967-106">Syntax</span></span>

```xml
<CustomControlName>NameofCustomControl</CustomControlName>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="4e967-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="4e967-107">Attributes and Elements</span></span>

<span data-ttu-id="4e967-108">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `CustomControlName` elemet.</span><span class="sxs-lookup"><span data-stu-id="4e967-108">The following sections describe attributes, child elements, and the parent element of the `CustomControlName` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="4e967-109">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="4e967-109">Attributes</span></span>

<span data-ttu-id="4e967-110">Nincs.</span><span class="sxs-lookup"><span data-stu-id="4e967-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="4e967-111">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="4e967-111">Child Elements</span></span>

<span data-ttu-id="4e967-112">Nincs.</span><span class="sxs-lookup"><span data-stu-id="4e967-112">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="4e967-113">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="4e967-113">Parent Elements</span></span>

|<span data-ttu-id="4e967-114">Elem</span><span class="sxs-lookup"><span data-stu-id="4e967-114">Element</span></span>|<span data-ttu-id="4e967-115">Leírás</span><span class="sxs-lookup"><span data-stu-id="4e967-115">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="4e967-116">Nézet (formátum) vezérlők CustomItem ExpressionBinding elem.</span><span class="sxs-lookup"><span data-stu-id="4e967-116">ExpressionBinding Element for CustomItem for Controls for View (Format)</span></span>](./expressionbinding-element-for-customitem-for-controls-for-view-format.md)|<span data-ttu-id="4e967-117">Határozza meg a vezérlő által megjelenített adatokat.</span><span class="sxs-lookup"><span data-stu-id="4e967-117">Defines the data that is displayed by the control.</span></span>|

## <a name="text-value"></a><span data-ttu-id="4e967-118">A szöveges érték</span><span class="sxs-lookup"><span data-stu-id="4e967-118">Text Value</span></span>

<span data-ttu-id="4e967-119">Adja meg a vezérlő nevét.</span><span class="sxs-lookup"><span data-stu-id="4e967-119">Specify the name of the control.</span></span>

## <a name="remarks"></a><span data-ttu-id="4e967-120">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="4e967-120">Remarks</span></span>

<span data-ttu-id="4e967-121">A formázási fájl összes nézetek által használt Gyakori vezérlők hozhat létre, és hozhat létre, amely egy adott nézet által használható vezérlőkre.</span><span class="sxs-lookup"><span data-stu-id="4e967-121">You can create common controls that can be used by all the views of a formatting file, and you can create view controls that can be used by a specific view.</span></span> <span data-ttu-id="4e967-122">A következő elemeket adja meg, hogy ezek a vezérlők nevét:</span><span class="sxs-lookup"><span data-stu-id="4e967-122">The following elements specify the names of these controls:</span></span>

- [<span data-ttu-id="4e967-123">A vezérlési konfiguráció (formátum) vezérlők Name elemet</span><span class="sxs-lookup"><span data-stu-id="4e967-123">Name Element for Control for Controls for Configuration (Format)</span></span>](./name-element-for-control-for-controls-for-configuration-format.md)

- [<span data-ttu-id="4e967-124">Vezérlő (formátum) nézet vezérlők Name elemet</span><span class="sxs-lookup"><span data-stu-id="4e967-124">Name Element for Control for Controls for View (Format)</span></span>](./name-element-for-control-for-controls-for-view-format.md)

## <a name="see-also"></a><span data-ttu-id="4e967-125">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="4e967-125">See Also</span></span>

[<span data-ttu-id="4e967-126">A vezérlési konfiguráció (formátum) vezérlők Name elemet</span><span class="sxs-lookup"><span data-stu-id="4e967-126">Name Element for Control for Controls for Configuration (Format)</span></span>](./name-element-for-control-for-controls-for-configuration-format.md)

[<span data-ttu-id="4e967-127">Vezérlő (formátum) nézet vezérlők Name elemet</span><span class="sxs-lookup"><span data-stu-id="4e967-127">Name Element for Control for Controls for View (Format)</span></span>](./name-element-for-control-for-controls-for-view-format.md)

[<span data-ttu-id="4e967-128">Nézet (formátum) vezérlők CustomItem ExpressionBinding elem.</span><span class="sxs-lookup"><span data-stu-id="4e967-128">ExpressionBinding Element for CustomItem for Controls for View (Format)</span></span>](./expressionbinding-element-for-customitem-for-controls-for-view-format.md)

[<span data-ttu-id="4e967-129">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="4e967-129">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
