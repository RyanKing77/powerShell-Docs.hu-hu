---
title: Nevezze el elem vezérlő vezérlők konfiguráció (formátum) |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: b4371d45-49a4-4303-8384-5b54105bd0d6
caps.latest.revision: 8
ms.openlocfilehash: 2704a530e0ae269efb772ac10e531bcbb12f6eff
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56849671"
---
# <a name="name-element-for-control-for-controls-for-configuration-format"></a><span data-ttu-id="bb7f4-102">A Konfiguráció Vezérlők eleméhez tartozó Vezérlő Név eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="bb7f4-102">Name Element for Control for Controls for Configuration (Format)</span></span>

<span data-ttu-id="bb7f4-103">Megadja a vezérlő nevét.</span><span class="sxs-lookup"><span data-stu-id="bb7f4-103">Specifies the name of the control.</span></span> <span data-ttu-id="bb7f4-104">Ez az elem szolgál egy közös vezérlőelem a formázási fájlban az összes nézetek által használható meghatározásakor.</span><span class="sxs-lookup"><span data-stu-id="bb7f4-104">This element is used when defining a common control that can be used by all the views in the formatting file.</span></span>

<span data-ttu-id="bb7f4-105">Konfigurációs elem (formátum) vezérlők elem Configuration (formátum) vezérlőelem elem vezérlők vezérlők konfiguráció (formátum) vezérlő konfigurációs (formátum) neve elemhez</span><span class="sxs-lookup"><span data-stu-id="bb7f4-105">Configuration Element (Format) Controls Element of Configuration (Format) Control Element for Controls for Configuration (Format) Name Element for Control for Controls for Configuration (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="bb7f4-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="bb7f4-106">Syntax</span></span>

```xml
<Name>NameOfControl</Name>

```

## <a name="attributes-and-elements"></a><span data-ttu-id="bb7f4-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="bb7f4-107">Attributes and Elements</span></span>

<span data-ttu-id="bb7f4-108">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `Name` elemet.</span><span class="sxs-lookup"><span data-stu-id="bb7f4-108">The following sections describe attributes, child elements, and the parent element of the `Name` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="bb7f4-109">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="bb7f4-109">Attributes</span></span>

<span data-ttu-id="bb7f4-110">Nincs.</span><span class="sxs-lookup"><span data-stu-id="bb7f4-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="bb7f4-111">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="bb7f4-111">Child Elements</span></span>

<span data-ttu-id="bb7f4-112">Nincs.</span><span class="sxs-lookup"><span data-stu-id="bb7f4-112">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="bb7f4-113">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="bb7f4-113">Parent Elements</span></span>

|<span data-ttu-id="bb7f4-114">Elem</span><span class="sxs-lookup"><span data-stu-id="bb7f4-114">Element</span></span>|<span data-ttu-id="bb7f4-115">Leírás</span><span class="sxs-lookup"><span data-stu-id="bb7f4-115">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="bb7f4-116">Vezérlő elemet a vezérlők konfiguráció (formátum)</span><span class="sxs-lookup"><span data-stu-id="bb7f4-116">Control Element for Controls for Configuration (Format)</span></span>](./control-element-for-controls-for-configuration-format.md)|<span data-ttu-id="bb7f4-117">Meghatározza egy közös ellenőrzés, hogy a formázási fájlja és a neve, amellyel hivatkozni a vezérlőelem összes nézet is lehet.</span><span class="sxs-lookup"><span data-stu-id="bb7f4-117">Defines a common control that can be used by all the views of the formatting file and the name that is used to reference the control.</span></span>|

## <a name="text-value"></a><span data-ttu-id="bb7f4-118">Szöveges érték</span><span class="sxs-lookup"><span data-stu-id="bb7f4-118">Text Value</span></span>

<span data-ttu-id="bb7f4-119">Adja meg a nevét, amely a vezérlőelem hivatkozni.</span><span class="sxs-lookup"><span data-stu-id="bb7f4-119">Specify the name that is used to reference this control.</span></span>

## <a name="remarks"></a><span data-ttu-id="bb7f4-120">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="bb7f4-120">Remarks</span></span>

<span data-ttu-id="bb7f4-121">Az itt megadott név a vezérlő hivatkozni a következő elemeket is használható.</span><span class="sxs-lookup"><span data-stu-id="bb7f4-121">The name specified here can be used in the following elements to reference this control.</span></span>

- <span data-ttu-id="bb7f4-122">Egy táblázat, lista, szélesre vagy egyéni vezérlő nézetében létrehozásakor, a vezérlő határozhatja meg a következő elemet: [GroupBy elem nézet (formátum)](./groupby-element-for-view-format.md)</span><span class="sxs-lookup"><span data-stu-id="bb7f4-122">When creating a table, list, wide or custom control view, the control can be specified by the following element: [GroupBy Element for View (Format)](./groupby-element-for-view-format.md)</span></span>

- <span data-ttu-id="bb7f4-123">Egy másik gyakori vezérlő létrehozásakor ez a vezérlő határozhatja meg a következő elemet: [Konfiguráció (formátum) vezérlők CustomItem ExpressionBinding elem.](./expressionbinding-element-for-customitem-for-controls-for-configuration-format.md)</span><span class="sxs-lookup"><span data-stu-id="bb7f4-123">When creating another common control, this control can be specified by the following element: [ExpressionBinding Element for CustomItem for Controls for Configuration (Format)](./expressionbinding-element-for-customitem-for-controls-for-configuration-format.md)</span></span>

- <span data-ttu-id="bb7f4-124">Vezérlőelem létrehozása a nézet által használható, ha ez a vezérlő határozhatja meg a következő elemet: [Nézet (formátum) vezérlők CustomItem ExpressionBinding elem.](./expressionbinding-element-for-customitem-for-controls-for-view-format.md)</span><span class="sxs-lookup"><span data-stu-id="bb7f4-124">When creating a control that can be used by a view, this control can be specified by the following element: [ExpressionBinding Element for CustomItem for Controls for View (Format)](./expressionbinding-element-for-customitem-for-controls-for-view-format.md)</span></span>

## <a name="see-also"></a><span data-ttu-id="bb7f4-125">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="bb7f4-125">See Also</span></span>

[<span data-ttu-id="bb7f4-126">Vezérlő elemet a vezérlők konfiguráció (formátum)</span><span class="sxs-lookup"><span data-stu-id="bb7f4-126">Control Element for Controls for Configuration (Format)</span></span>](./control-element-for-controls-for-configuration-format.md)

[<span data-ttu-id="bb7f4-127">Konfiguráció (formátum) vezérlők CustomItem ExpressionBinding elem.</span><span class="sxs-lookup"><span data-stu-id="bb7f4-127">ExpressionBinding Element for CustomItem for Controls for Configuration (Format)</span></span>](./expressionbinding-element-for-customitem-for-controls-for-configuration-format.md)

[<span data-ttu-id="bb7f4-128">Nézet (formátum) vezérlők CustomItem ExpressionBinding elem.</span><span class="sxs-lookup"><span data-stu-id="bb7f4-128">ExpressionBinding Element for CustomItem for Controls for View (Format)</span></span>](./expressionbinding-element-for-customitem-for-controls-for-view-format.md)

[<span data-ttu-id="bb7f4-129">GroupBy elem nézet (formátum)</span><span class="sxs-lookup"><span data-stu-id="bb7f4-129">GroupBy Element for View (Format)</span></span>](./groupby-element-for-view-format.md)

[<span data-ttu-id="bb7f4-130">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="bb7f4-130">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
