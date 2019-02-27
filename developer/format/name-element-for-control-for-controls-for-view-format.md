---
title: Nevezze el elem vezérlő vezérlők (formátum) nézet |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 26437467-d578-4e8d-8cdd-17dfe644957a
caps.latest.revision: 7
ms.openlocfilehash: 7e24aa60f7abae5768707d2527826c452b709002
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56851281"
---
# <a name="name-element-for-control-for-controls-for-view-format"></a><span data-ttu-id="867af-102">A Nézet Vezérlők eleméhez tartozó Vezérlő Név eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="867af-102">Name Element for Control for Controls for View (Format)</span></span>

<span data-ttu-id="867af-103">Megadja a vezérlő nevét.</span><span class="sxs-lookup"><span data-stu-id="867af-103">Specifies the name of the control.</span></span>

<span data-ttu-id="867af-104">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézet elem (formátum) szabályozza elem (formátum) vezérlőelem elem vezérlők megtekintése (formátum) elemhez vezérlő nézet (formátum)</span><span class="sxs-lookup"><span data-stu-id="867af-104">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) Controls Element (Format) Control Element for Controls for View (Format) Name Element for Control for View (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="867af-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="867af-105">Syntax</span></span>

```xml
<Name>ControlName</Name>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="867af-106">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="867af-106">Attributes and Elements</span></span>

<span data-ttu-id="867af-107">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `Name` elemet.</span><span class="sxs-lookup"><span data-stu-id="867af-107">The following sections describe attributes, child elements, and the parent element of the `Name` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="867af-108">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="867af-108">Attributes</span></span>

<span data-ttu-id="867af-109">Nincs.</span><span class="sxs-lookup"><span data-stu-id="867af-109">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="867af-110">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="867af-110">Child Elements</span></span>

<span data-ttu-id="867af-111">Nincs.</span><span class="sxs-lookup"><span data-stu-id="867af-111">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="867af-112">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="867af-112">Parent Elements</span></span>

|<span data-ttu-id="867af-113">Elem</span><span class="sxs-lookup"><span data-stu-id="867af-113">Element</span></span>|<span data-ttu-id="867af-114">Leírás</span><span class="sxs-lookup"><span data-stu-id="867af-114">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="867af-115">Vezérlő elemet a vezérlők megjelenítéséhez (formátum)</span><span class="sxs-lookup"><span data-stu-id="867af-115">Control Element for Controls for View (Format)</span></span>](./control-element-for-controls-for-view-format.md)|<span data-ttu-id="867af-116">Határozza meg olyan vezérlő, amely a nézet és a neve, amellyel hivatkozni a vezérlő által használható.</span><span class="sxs-lookup"><span data-stu-id="867af-116">Defines a control that can be used by the view and the name that is used to reference the control.</span></span>|

## <a name="text-value"></a><span data-ttu-id="867af-117">Szöveges érték</span><span class="sxs-lookup"><span data-stu-id="867af-117">Text Value</span></span>

<span data-ttu-id="867af-118">Adja meg a nevét, amely a vezérlőelem hivatkozni.</span><span class="sxs-lookup"><span data-stu-id="867af-118">Specify the name that is used to reference the control.</span></span>

## <a name="remarks"></a><span data-ttu-id="867af-119">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="867af-119">Remarks</span></span>

<span data-ttu-id="867af-120">Az itt megadott név a vezérlő hivatkozni a következő elemeket is használható.</span><span class="sxs-lookup"><span data-stu-id="867af-120">The name specified here can be used in the following elements to reference this control.</span></span>

- <span data-ttu-id="867af-121">Egy táblázat, lista, szélesre vagy egyéni vezérlő nézetében létrehozásakor, a vezérlő határozhatja meg a következő elemet: [GroupBy elem nézet (formátum)](./groupby-element-for-view-format.md)</span><span class="sxs-lookup"><span data-stu-id="867af-121">When creating a table, list, wide or custom control view, the control can be specified by the following element: [GroupBy Element for View (Format)](./groupby-element-for-view-format.md)</span></span>

- <span data-ttu-id="867af-122">Egy másik vezérlő létrehozása, amely a nézet által használható, ha ez a vezérlő is megadható a következő elemet: [Nézet (formátum) vezérlők CustomItem ExpressionBinding elem.](./expressionbinding-element-for-customitem-for-controls-for-view-format.md)</span><span class="sxs-lookup"><span data-stu-id="867af-122">When creating another control that can be used by a view, this control can be specified by the following element: [ExpressionBinding Element for CustomItem for Controls for View (Format)](./expressionbinding-element-for-customitem-for-controls-for-view-format.md)</span></span>

## <a name="see-also"></a><span data-ttu-id="867af-123">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="867af-123">See Also</span></span>

[<span data-ttu-id="867af-124">GroupBy elem nézet (formátum)</span><span class="sxs-lookup"><span data-stu-id="867af-124">GroupBy Element for View (Format)</span></span>](./groupby-element-for-view-format.md)

[<span data-ttu-id="867af-125">Nézet (formátum) vezérlők CustomItem ExpressionBinding elem.</span><span class="sxs-lookup"><span data-stu-id="867af-125">ExpressionBinding Element for CustomItem for Controls for View (Format)</span></span>](./expressionbinding-element-for-customitem-for-controls-for-view-format.md)

[<span data-ttu-id="867af-126">Vezérlő elemet a vezérlők megjelenítéséhez (formátum)</span><span class="sxs-lookup"><span data-stu-id="867af-126">Control Element for Controls for View (Format)</span></span>](./control-element-for-controls-for-view-format.md)

[<span data-ttu-id="867af-127">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="867af-127">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
