---
title: ScriptBlock elemet a vezérlők (formátum) konfiguráció SelectionCondition |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: bb032dfc-9ef6-403c-b557-5858617e3483
caps.latest.revision: 6
ms.openlocfilehash: 102987970152420896a0c986f0973280ae209623
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56844862"
---
# <a name="scriptblock-element-for-selectioncondition-for-controls-for-configuration-format"></a><span data-ttu-id="18a31-102">A Konfiguráció Vezérlők eleméhez tartozó SelectionCondition ScriptBlock eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="18a31-102">ScriptBlock Element for SelectionCondition for Controls for Configuration (Format)</span></span>

<span data-ttu-id="18a31-103">Megadja a parancsprogramot, amely elindítja a feltétel.</span><span class="sxs-lookup"><span data-stu-id="18a31-103">Specifies the script that triggers the condition.</span></span> <span data-ttu-id="18a31-104">Ha ez a parancsfájl kiértékelése `true`, a feltétel nem teljesül, és a definíció szolgál.</span><span class="sxs-lookup"><span data-stu-id="18a31-104">When this script is evaluated to `true`, the condition is met, and the definition is used.</span></span> <span data-ttu-id="18a31-105">Ez az elem szolgál egy közös vezérlőelem a formázási fájlban az összes nézetek által használható meghatározásakor.</span><span class="sxs-lookup"><span data-stu-id="18a31-105">This element is used when defining a common control that can be used by all the views in the formatting file.</span></span>

<span data-ttu-id="18a31-106">Konfigurációs elem (formátum) vezérlők elem Configuration (formátum) vezérlőelem elem vezérlők, a vezérlő konfigurációs (formátum) CustomEntries elemhez tartozó CustomControl Configuration (a Configuration (formátum) CustomControl elem Formátum) CustomEntry elemet a vezérlők, a Configuration (formátum) EntrySelectedBy elem CustomEntry vezérlők EntrySelectedBy vezérlők (formátum) konfiguráció esetén a Configuration (formátum) SelectionCondition elemhez tartozó CustomControl Konfiguráció (formátum) vezérlők SelectionCondition ScriptBlock eleme</span><span class="sxs-lookup"><span data-stu-id="18a31-106">Configuration Element (Format) Controls Element of Configuration (Format) Control Element for Controls for Configuration (Format) CustomControl Element for Control for Configuration (Format) CustomEntries Element for CustomControl for Configuration (Format) CustomEntry Element for CustomControl for Controls for Configuration (Format) EntrySelectedBy Element for CustomEntry for Controls for Configuration (Format) SelectionCondition Element for EntrySelectedBy for Controls for Configuration (Format) ScriptBlock Element for SelectionCondition for Controls for Configuration (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="18a31-107">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="18a31-107">Syntax</span></span>

```xml
<ScriptBlock>ScriptToEvaluate</ScriptBlock>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="18a31-108">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="18a31-108">Attributes and Elements</span></span>

<span data-ttu-id="18a31-109">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `ScriptBlock` elemet.</span><span class="sxs-lookup"><span data-stu-id="18a31-109">The following sections describe attributes, child elements, and the parent element of the `ScriptBlock` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="18a31-110">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="18a31-110">Attributes</span></span>

<span data-ttu-id="18a31-111">Nincs.</span><span class="sxs-lookup"><span data-stu-id="18a31-111">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="18a31-112">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="18a31-112">Child Elements</span></span>

<span data-ttu-id="18a31-113">Nincs.</span><span class="sxs-lookup"><span data-stu-id="18a31-113">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="18a31-114">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="18a31-114">Parent Elements</span></span>

|<span data-ttu-id="18a31-115">Elem</span><span class="sxs-lookup"><span data-stu-id="18a31-115">Element</span></span>|<span data-ttu-id="18a31-116">Leírás</span><span class="sxs-lookup"><span data-stu-id="18a31-116">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="18a31-117">Konfiguráció (formátum) vezérlők EntrySelectedBy SelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="18a31-117">SelectionCondition Element for EntrySelectedBy for Controls for Configuration (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-controls-for-configuration-format.md)|<span data-ttu-id="18a31-118">Határozza meg egy feltételt, amely a közös ellenőrzési definíciójában használt léteznie kell.</span><span class="sxs-lookup"><span data-stu-id="18a31-118">Defines a condition that must exist for the common control definition to be used.</span></span>|

## <a name="text-value"></a><span data-ttu-id="18a31-119">Szöveges érték</span><span class="sxs-lookup"><span data-stu-id="18a31-119">Text Value</span></span>

<span data-ttu-id="18a31-120">Adja meg a parancsfájl, amely ki lesz értékelve.</span><span class="sxs-lookup"><span data-stu-id="18a31-120">Specify the script that is evaluated.</span></span>

## <a name="remarks"></a><span data-ttu-id="18a31-121">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="18a31-121">Remarks</span></span>

<span data-ttu-id="18a31-122">A kiválasztási feltétel adjon meg egy legalább egy parancsfájl vagy a tulajdonság nevét értékelése, de nem adható meg egyszerre.</span><span class="sxs-lookup"><span data-stu-id="18a31-122">The selection condition must specify a least one script or property name to evaluate, but cannot specify both.</span></span> <span data-ttu-id="18a31-123">Hogyan használható a kiválasztási feltételek kapcsolatos további információkért lásd: [feltételek meghatározása az adatok megjelenítése](./defining-conditions-for-displaying-data.md).</span><span class="sxs-lookup"><span data-stu-id="18a31-123">For more information about how selection conditions can be used, see [Defining Conditions for Displaying Data](./defining-conditions-for-displaying-data.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="18a31-124">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="18a31-124">See Also</span></span>

[<span data-ttu-id="18a31-125">Konfiguráció (formátum) vezérlők EntrySelectedBy SelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="18a31-125">SelectionCondition Element for EntrySelectedBy for Controls for Configuration (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-controls-for-configuration-format.md)

[<span data-ttu-id="18a31-126">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="18a31-126">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
