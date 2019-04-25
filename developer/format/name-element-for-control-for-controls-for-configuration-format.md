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
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62065189"
---
# <a name="name-element-for-control-for-controls-for-configuration-format"></a><span data-ttu-id="ca905-102">A Konfiguráció Vezérlők eleméhez tartozó Vezérlő Név eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="ca905-102">Name Element for Control for Controls for Configuration (Format)</span></span>

<span data-ttu-id="ca905-103">Megadja a vezérlő nevét.</span><span class="sxs-lookup"><span data-stu-id="ca905-103">Specifies the name of the control.</span></span> <span data-ttu-id="ca905-104">Ez az elem szolgál egy közös vezérlőelem a formázási fájlban az összes nézetek által használható meghatározásakor.</span><span class="sxs-lookup"><span data-stu-id="ca905-104">This element is used when defining a common control that can be used by all the views in the formatting file.</span></span>

<span data-ttu-id="ca905-105">Konfigurációs elem (formátum) vezérlők elem Configuration (formátum) vezérlőelem elem vezérlők vezérlők konfiguráció (formátum) vezérlő konfigurációs (formátum) neve elemhez</span><span class="sxs-lookup"><span data-stu-id="ca905-105">Configuration Element (Format) Controls Element of Configuration (Format) Control Element for Controls for Configuration (Format) Name Element for Control for Controls for Configuration (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="ca905-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="ca905-106">Syntax</span></span>

```xml
<Name>NameOfControl</Name>

```

## <a name="attributes-and-elements"></a><span data-ttu-id="ca905-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="ca905-107">Attributes and Elements</span></span>

<span data-ttu-id="ca905-108">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `Name` elemet.</span><span class="sxs-lookup"><span data-stu-id="ca905-108">The following sections describe attributes, child elements, and the parent element of the `Name` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="ca905-109">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="ca905-109">Attributes</span></span>

<span data-ttu-id="ca905-110">Nincs.</span><span class="sxs-lookup"><span data-stu-id="ca905-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="ca905-111">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="ca905-111">Child Elements</span></span>

<span data-ttu-id="ca905-112">Nincs.</span><span class="sxs-lookup"><span data-stu-id="ca905-112">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="ca905-113">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="ca905-113">Parent Elements</span></span>

|<span data-ttu-id="ca905-114">Elem</span><span class="sxs-lookup"><span data-stu-id="ca905-114">Element</span></span>|<span data-ttu-id="ca905-115">Leírás</span><span class="sxs-lookup"><span data-stu-id="ca905-115">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="ca905-116">Vezérlő elemet a vezérlők konfiguráció (formátum)</span><span class="sxs-lookup"><span data-stu-id="ca905-116">Control Element for Controls for Configuration (Format)</span></span>](./control-element-for-controls-for-configuration-format.md)|<span data-ttu-id="ca905-117">Meghatározza egy közös ellenőrzés, hogy a formázási fájlja és a neve, amellyel hivatkozni a vezérlőelem összes nézet is lehet.</span><span class="sxs-lookup"><span data-stu-id="ca905-117">Defines a common control that can be used by all the views of the formatting file and the name that is used to reference the control.</span></span>|

## <a name="text-value"></a><span data-ttu-id="ca905-118">A szöveges érték</span><span class="sxs-lookup"><span data-stu-id="ca905-118">Text Value</span></span>

<span data-ttu-id="ca905-119">Adja meg a nevét, amely a vezérlőelem hivatkozni.</span><span class="sxs-lookup"><span data-stu-id="ca905-119">Specify the name that is used to reference this control.</span></span>

## <a name="remarks"></a><span data-ttu-id="ca905-120">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="ca905-120">Remarks</span></span>

<span data-ttu-id="ca905-121">Az itt megadott név a vezérlő hivatkozni a következő elemeket is használható.</span><span class="sxs-lookup"><span data-stu-id="ca905-121">The name specified here can be used in the following elements to reference this control.</span></span>

- <span data-ttu-id="ca905-122">Egy táblázat, lista, szélesre vagy egyéni vezérlő nézetében létrehozásakor, a vezérlő határozhatja meg a következő elemet: [GroupBy elem nézet (formátum)](./groupby-element-for-view-format.md)</span><span class="sxs-lookup"><span data-stu-id="ca905-122">When creating a table, list, wide or custom control view, the control can be specified by the following element: [GroupBy Element for View (Format)](./groupby-element-for-view-format.md)</span></span>

- <span data-ttu-id="ca905-123">Egy másik gyakori vezérlő létrehozásakor ez a vezérlő határozhatja meg a következő elemet: [Konfiguráció (formátum) vezérlők CustomItem ExpressionBinding elem.](./expressionbinding-element-for-customitem-for-controls-for-configuration-format.md)</span><span class="sxs-lookup"><span data-stu-id="ca905-123">When creating another common control, this control can be specified by the following element: [ExpressionBinding Element for CustomItem for Controls for Configuration (Format)](./expressionbinding-element-for-customitem-for-controls-for-configuration-format.md)</span></span>

- <span data-ttu-id="ca905-124">Vezérlőelem létrehozása a nézet által használható, ha ez a vezérlő határozhatja meg a következő elemet: [Nézet (formátum) vezérlők CustomItem ExpressionBinding elem.](./expressionbinding-element-for-customitem-for-controls-for-view-format.md)</span><span class="sxs-lookup"><span data-stu-id="ca905-124">When creating a control that can be used by a view, this control can be specified by the following element: [ExpressionBinding Element for CustomItem for Controls for View (Format)](./expressionbinding-element-for-customitem-for-controls-for-view-format.md)</span></span>

## <a name="see-also"></a><span data-ttu-id="ca905-125">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="ca905-125">See Also</span></span>

[<span data-ttu-id="ca905-126">Vezérlő elemet a vezérlők konfiguráció (formátum)</span><span class="sxs-lookup"><span data-stu-id="ca905-126">Control Element for Controls for Configuration (Format)</span></span>](./control-element-for-controls-for-configuration-format.md)

[<span data-ttu-id="ca905-127">Konfiguráció (formátum) vezérlők CustomItem ExpressionBinding elem.</span><span class="sxs-lookup"><span data-stu-id="ca905-127">ExpressionBinding Element for CustomItem for Controls for Configuration (Format)</span></span>](./expressionbinding-element-for-customitem-for-controls-for-configuration-format.md)

[<span data-ttu-id="ca905-128">Nézet (formátum) vezérlők CustomItem ExpressionBinding elem.</span><span class="sxs-lookup"><span data-stu-id="ca905-128">ExpressionBinding Element for CustomItem for Controls for View (Format)</span></span>](./expressionbinding-element-for-customitem-for-controls-for-view-format.md)

[<span data-ttu-id="ca905-129">GroupBy elem nézet (formátum)</span><span class="sxs-lookup"><span data-stu-id="ca905-129">GroupBy Element for View (Format)</span></span>](./groupby-element-for-view-format.md)

[<span data-ttu-id="ca905-130">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="ca905-130">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
