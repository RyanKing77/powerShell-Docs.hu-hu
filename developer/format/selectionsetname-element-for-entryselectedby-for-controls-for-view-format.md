---
title: SelectionSetName elemet a vezérlők (formátum) nézet EntrySelectedBy |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: b594a064-746f-4900-99e4-7be7bf5aa5a2
caps.latest.revision: 7
ms.openlocfilehash: d540c99707f4e0796b2d408f2161a9208257ab32
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56850308"
---
# <a name="selectionsetname-element-for-entryselectedby-for-controls-for-view-format"></a><span data-ttu-id="14001-102">A Nézet Vezérlők eleméhez tartozó EntrySelectedBy SelectionSetName eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="14001-102">SelectionSetName Element for EntrySelectedBy for Controls for View (Format)</span></span>

<span data-ttu-id="14001-103">Ez a definíció, a vezérlő használó .NET-típusok egy halmazát határozza meg.</span><span class="sxs-lookup"><span data-stu-id="14001-103">Specifies a set of .NET types that use this definition of the control.</span></span> <span data-ttu-id="14001-104">Ez az elem szolgál a nézet által használható vezérlők meghatározásakor.</span><span class="sxs-lookup"><span data-stu-id="14001-104">This element is used when defining controls that can be used by a view.</span></span>

<span data-ttu-id="14001-105">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem vezérlők elem (formátum) vezérlőelem elem vezérlők, a nézet (formátum) CustomControl elem megtekintése (formátum) CustomEntries elemet a vezérlők a vezérlő CustomControl vezérlők, a vezérlők, a vezérlők, a vezérlők, a nézet (EntrySelectedBy megtekintése (formátum) SelectionSetName elemhez CustomEntry megtekintése (formátum) EntrySelectedBy elemhez CustomEntries megtekintése (formátum) CustomEntry elemhez Formátum)</span><span class="sxs-lookup"><span data-stu-id="14001-105">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) Controls Element (Format) Control Element for Controls for View (Format) CustomControl Element for Control for Controls for View (Format) CustomEntries Element for CustomControl for Controls for View (Format) CustomEntry Element for CustomEntries for Controls for View (Format) EntrySelectedBy Element for CustomEntry for Controls for View (Format) SelectionSetName Element for EntrySelectedBy for Controls for View (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="14001-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="14001-106">Syntax</span></span>

```xml
<SelectionSetName>NameofSelectionSet</SelectionSetName>

```

## <a name="attributes-and-elements"></a><span data-ttu-id="14001-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="14001-107">Attributes and Elements</span></span>

<span data-ttu-id="14001-108">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `SelectionSetName` elemet.</span><span class="sxs-lookup"><span data-stu-id="14001-108">The following sections describe attributes, child elements, and the parent element of the `SelectionSetName` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="14001-109">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="14001-109">Attributes</span></span>

<span data-ttu-id="14001-110">Egyik sem</span><span class="sxs-lookup"><span data-stu-id="14001-110">None</span></span>

### <a name="child-elements"></a><span data-ttu-id="14001-111">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="14001-111">Child Elements</span></span>

<span data-ttu-id="14001-112">Nincs.</span><span class="sxs-lookup"><span data-stu-id="14001-112">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="14001-113">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="14001-113">Parent Elements</span></span>

|<span data-ttu-id="14001-114">Elem</span><span class="sxs-lookup"><span data-stu-id="14001-114">Element</span></span>|<span data-ttu-id="14001-115">Leírás</span><span class="sxs-lookup"><span data-stu-id="14001-115">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="14001-116">Nézet (formátum) vezérlők CustomEntry EntrySelectedBy elem.</span><span class="sxs-lookup"><span data-stu-id="14001-116">EntrySelectedBy Element for CustomEntry for Controls for View (Format)</span></span>](./entryselectedby-element-for-customentry-for-controls-for-view-format.md)|<span data-ttu-id="14001-117">A .NET-típusokat, amelyek a vezérlő definition vagy a feltétellel, hogy léteznie kell a definíció használandó határozza meg.</span><span class="sxs-lookup"><span data-stu-id="14001-117">Defines the .NET types that use this control definition or the condition that must exist for this definition to be used.</span></span>|

## <a name="text-value"></a><span data-ttu-id="14001-118">Szöveges érték</span><span class="sxs-lookup"><span data-stu-id="14001-118">Text Value</span></span>

<span data-ttu-id="14001-119">Adja meg a kijelölt csoport nevét.</span><span class="sxs-lookup"><span data-stu-id="14001-119">Specify the name of the selection set.</span></span>

## <a name="remarks"></a><span data-ttu-id="14001-120">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="14001-120">Remarks</span></span>

<span data-ttu-id="14001-121">Minden vezérlő definíció rendelkeznie kell legalább egy típusnév, kijelölés set vagy meghatározott kiválasztási feltételnek.</span><span class="sxs-lookup"><span data-stu-id="14001-121">Each control definition must have at least one type name, selection set, or selection condition defined.</span></span>

<span data-ttu-id="14001-122">Kijelölt csoportok általában akkor használják, ha meg szeretné több nézetében lévő meghatározott felhasználói csoporttal használt objektumok.</span><span class="sxs-lookup"><span data-stu-id="14001-122">Selection sets are typically used when you want to define a group of objects that are used in multiple views.</span></span> <span data-ttu-id="14001-123">Kijelölt csoportok meghatározása kapcsolatos további információkért lásd: [meghatározása beállítja a kijelölés](./defining-selection-sets.md).</span><span class="sxs-lookup"><span data-stu-id="14001-123">For more information about defining selection sets, see [Defining Selection Sets](./defining-selection-sets.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="14001-124">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="14001-124">See Also</span></span>

[<span data-ttu-id="14001-125">Nézet (formátum) vezérlők CustomEntry EntrySelectedBy elem.</span><span class="sxs-lookup"><span data-stu-id="14001-125">EntrySelectedBy Element for CustomEntry for Controls for View (Format)</span></span>](./entryselectedby-element-for-customentry-for-controls-for-view-format.md)

[<span data-ttu-id="14001-126">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="14001-126">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
