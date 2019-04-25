---
title: GroupBy (formátum) CustomControlName eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 473d9b56-521b-479a-8010-67fe9f040063
caps.latest.revision: 8
ms.openlocfilehash: 3a386eff95044eae573c255a451c5c8b8f16714d
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62066540"
---
# <a name="customcontrolname-element-for-groupby-format"></a><span data-ttu-id="290c9-102">A GroupBy CustomControlName eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="290c9-102">CustomControlName Element for GroupBy (Format)</span></span>

<span data-ttu-id="290c9-103">Megadja az egyéni vezérlőt, amellyel megjelenjen az új csoport nevét.</span><span class="sxs-lookup"><span data-stu-id="290c9-103">Specifies the name of a custom control that is used to display the new group.</span></span> <span data-ttu-id="290c9-104">Ez az elem szolgál egy táblázat, lista, szélesre vagy egyéni vezérlő nézetében meghatározásakor.</span><span class="sxs-lookup"><span data-stu-id="290c9-104">This element is used when defining a table, list, wide or custom control view.</span></span>

<span data-ttu-id="290c9-105">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem GroupBy elem megtekintése (formátum) CustomControlName eleméhez GroupBy (formátum)</span><span class="sxs-lookup"><span data-stu-id="290c9-105">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) GroupBy Element for View (Format) CustomControlName Element of GroupBy (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="290c9-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="290c9-106">Syntax</span></span>

```xml
<CustomControlName>ControlName</CustomControlName>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="290c9-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="290c9-107">Attributes and Elements</span></span>

<span data-ttu-id="290c9-108">A következő szakaszok ismertetik az attribútumokat, a gyermekelemek és a szülő elemei a `CustomControlName` elemet.</span><span class="sxs-lookup"><span data-stu-id="290c9-108">The following sections describe the attributes, child elements, and parent elements of the `CustomControlName` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="290c9-109">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="290c9-109">Attributes</span></span>

<span data-ttu-id="290c9-110">Nincs.</span><span class="sxs-lookup"><span data-stu-id="290c9-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="290c9-111">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="290c9-111">Child Elements</span></span>

<span data-ttu-id="290c9-112">Nincs.</span><span class="sxs-lookup"><span data-stu-id="290c9-112">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="290c9-113">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="290c9-113">Parent Elements</span></span>

|<span data-ttu-id="290c9-114">Elem</span><span class="sxs-lookup"><span data-stu-id="290c9-114">Element</span></span>|<span data-ttu-id="290c9-115">Leírás</span><span class="sxs-lookup"><span data-stu-id="290c9-115">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="290c9-116">GroupBy elem nézet (formátum)</span><span class="sxs-lookup"><span data-stu-id="290c9-116">GroupBy Element for View (Format)</span></span>](./groupby-element-for-view-format.md)|<span data-ttu-id="290c9-117">Határozza meg, hogyan jeleníti meg a Windows PowerShell-objektumok egy új csoportot.</span><span class="sxs-lookup"><span data-stu-id="290c9-117">Defines how Windows PowerShell displays a new group of objects.</span></span>|

## <a name="text-value"></a><span data-ttu-id="290c9-118">A szöveges érték</span><span class="sxs-lookup"><span data-stu-id="290c9-118">Text Value</span></span>

<span data-ttu-id="290c9-119">Adja meg az egyéni vezérlő, amellyel új csoport megjelenítendő nevét.</span><span class="sxs-lookup"><span data-stu-id="290c9-119">Specify the name of the custom control that is used to display a new group.</span></span>

## <a name="remarks"></a><span data-ttu-id="290c9-120">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="290c9-120">Remarks</span></span>

<span data-ttu-id="290c9-121">A formázási fájl összes nézetek által használt Gyakori vezérlők hozhat létre, és hozhat létre, amely egy adott nézet által használható vezérlőkre.</span><span class="sxs-lookup"><span data-stu-id="290c9-121">You can create common controls that can be used by all the views of a formatting file, and you can create view controls that can be used by a specific view.</span></span> <span data-ttu-id="290c9-122">A következő elemeket adja meg az egyéni vezérlők nevét:</span><span class="sxs-lookup"><span data-stu-id="290c9-122">The following elements specify the names of these custom controls:</span></span>

- [<span data-ttu-id="290c9-123">A vezérlési konfiguráció (formátum) vezérlők Name elemet</span><span class="sxs-lookup"><span data-stu-id="290c9-123">Name Element for Control for Controls for Configuration (Format)</span></span>](./name-element-for-control-for-controls-for-configuration-format.md)

- [<span data-ttu-id="290c9-124">Vezérlő (formátum) nézet vezérlők Name elemet</span><span class="sxs-lookup"><span data-stu-id="290c9-124">Name Element for Control for Controls for View (Format)</span></span>](./name-element-for-control-for-controls-for-view-format.md)

## <a name="see-also"></a><span data-ttu-id="290c9-125">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="290c9-125">See Also</span></span>

[<span data-ttu-id="290c9-126">GroupBy elem nézet (formátum)</span><span class="sxs-lookup"><span data-stu-id="290c9-126">GroupBy Element for View (Format)</span></span>](./groupby-element-for-view-format.md)

[<span data-ttu-id="290c9-127">A vezérlési konfiguráció (formátum) vezérlők Name elemet</span><span class="sxs-lookup"><span data-stu-id="290c9-127">Name Element for Control for Controls for Configuration (Format)</span></span>](./name-element-for-control-for-controls-for-configuration-format.md)

[<span data-ttu-id="290c9-128">Vezérlő (formátum) nézet vezérlők Name elemet</span><span class="sxs-lookup"><span data-stu-id="290c9-128">Name Element for Control for Controls for View (Format)</span></span>](./name-element-for-control-for-controls-for-view-format.md)

[<span data-ttu-id="290c9-129">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="290c9-129">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
