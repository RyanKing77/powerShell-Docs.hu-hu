---
title: ScriptBlock elemet a vezérlők (formátum) nézet SelectionCondition |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 08512496-5682-4539-ab56-0c5394ce1f01
caps.latest.revision: 6
ms.openlocfilehash: 0137886437f01518f396613c564517e7910e657a
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62064390"
---
# <a name="scriptblock-element-for-selectioncondition-for-controls-for-view-format"></a><span data-ttu-id="23b07-102">A Nézet Vezérlők eleméhez tartozó SelectionCondition ScriptBlock eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="23b07-102">ScriptBlock Element for SelectionCondition for Controls for View (Format)</span></span>

<span data-ttu-id="23b07-103">Megadja a parancsprogramot, amely elindítja a feltétel.</span><span class="sxs-lookup"><span data-stu-id="23b07-103">Specifies the script that triggers the condition.</span></span> <span data-ttu-id="23b07-104">Ha ez a parancsfájl kiértékelése `true`, a feltétel nem teljesül, és a definíció szolgál.</span><span class="sxs-lookup"><span data-stu-id="23b07-104">When this script is evaluated to `true`, the condition is met, and the definition is used.</span></span> <span data-ttu-id="23b07-105">Ez az elem szolgál a nézet által használható vezérlők meghatározásakor.</span><span class="sxs-lookup"><span data-stu-id="23b07-105">This element is used when defining controls that can be used by a view.</span></span>

<span data-ttu-id="23b07-106">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem vezérlők elem (formátum) vezérlőelem elem vezérlők, a nézet (formátum) CustomControl elem megtekintése (formátum) CustomEntries elemet a vezérlők a vezérlő CustomControl vezérlők, a vezérlők, a vezérlők, a vezérlők, a nézet (EntrySelectedBy megtekintése (formátum) SelectionCondition elemhez CustomEntry megtekintése (formátum) EntrySelectedBy elemhez CustomEntries megtekintése (formátum) CustomEntry elemhez Formátum) ScriptBlock eleme SelectionCondition vezérlők nézet (formátum)</span><span class="sxs-lookup"><span data-stu-id="23b07-106">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) Controls Element (Format) Control Element for Controls for View (Format) CustomControl Element for Control for Controls for View (Format) CustomEntries Element for CustomControl for Controls for View (Format) CustomEntry Element for CustomEntries for Controls for View (Format) EntrySelectedBy Element for CustomEntry for Controls for View (Format) SelectionCondition Element for EntrySelectedBy for Controls for View (Format) ScriptBlock Element for SelectionCondition for Controls for View (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="23b07-107">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="23b07-107">Syntax</span></span>

```xml
<ScriptBlock>ScriptToEvaluate</ScriptBlock>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="23b07-108">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="23b07-108">Attributes and Elements</span></span>

<span data-ttu-id="23b07-109">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `ScriptBlock` elemet.</span><span class="sxs-lookup"><span data-stu-id="23b07-109">The following sections describe attributes, child elements, and the parent element of the `ScriptBlock` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="23b07-110">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="23b07-110">Attributes</span></span>

<span data-ttu-id="23b07-111">Nincs.</span><span class="sxs-lookup"><span data-stu-id="23b07-111">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="23b07-112">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="23b07-112">Child Elements</span></span>

<span data-ttu-id="23b07-113">Nincs.</span><span class="sxs-lookup"><span data-stu-id="23b07-113">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="23b07-114">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="23b07-114">Parent Elements</span></span>

|<span data-ttu-id="23b07-115">Elem</span><span class="sxs-lookup"><span data-stu-id="23b07-115">Element</span></span>|<span data-ttu-id="23b07-116">Leírás</span><span class="sxs-lookup"><span data-stu-id="23b07-116">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="23b07-117">Nézet (formátum) vezérlők EntrySelectedBy SelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="23b07-117">SelectionCondition Element for EntrySelectedBy for Controls for View (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-controls-for-view-format.md)|<span data-ttu-id="23b07-118">Határozza meg egy feltételt, amely a vezérlőelem definíciójában használt léteznie kell.</span><span class="sxs-lookup"><span data-stu-id="23b07-118">Defines a condition that must exist for the control definition to be used.</span></span>|

## <a name="text-value"></a><span data-ttu-id="23b07-119">A szöveges érték</span><span class="sxs-lookup"><span data-stu-id="23b07-119">Text Value</span></span>

<span data-ttu-id="23b07-120">Adja meg a parancsfájl, amely ki lesz értékelve.</span><span class="sxs-lookup"><span data-stu-id="23b07-120">Specify the script that is evaluated.</span></span>

## <a name="remarks"></a><span data-ttu-id="23b07-121">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="23b07-121">Remarks</span></span>

<span data-ttu-id="23b07-122">A kiválasztási feltétel adjon meg egy legalább egy parancsfájl vagy a tulajdonság nevét értékelése, de nem adható meg egyszerre.</span><span class="sxs-lookup"><span data-stu-id="23b07-122">The selection condition must specify a least one script or property name to evaluate, but cannot specify both.</span></span> <span data-ttu-id="23b07-123">Hogyan használható a kiválasztási feltételek kapcsolatos további információkért lásd: [feltételek meghatározása az adatok megjelenítése](./defining-conditions-for-displaying-data.md).</span><span class="sxs-lookup"><span data-stu-id="23b07-123">For more information about how selection conditions can be used, see [Defining Conditions for Displaying Data](./defining-conditions-for-displaying-data.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="23b07-124">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="23b07-124">See Also</span></span>

[<span data-ttu-id="23b07-125">Nézet (formátum) vezérlők EntrySelectedBy SelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="23b07-125">SelectionCondition Element for EntrySelectedBy for Controls for View (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-controls-for-view-format.md)

[<span data-ttu-id="23b07-126">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="23b07-126">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
