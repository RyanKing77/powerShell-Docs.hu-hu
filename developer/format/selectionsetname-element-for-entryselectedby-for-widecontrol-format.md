---
title: WideControl (formátum) a EntrySelectedBy SelectionSetName eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: c9c6e18f-6cca-465c-bd20-3969e7897a96
caps.latest.revision: 10
ms.openlocfilehash: 6b6a4a4647412d11d947f1dc4ea12d1e05ff536e
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56847368"
---
# <a name="selectionsetname-element-for-entryselectedby-for-widecontrol-format"></a><span data-ttu-id="e654a-102">A WideControl elemhez tartozó EntrySelectedBy SelectionSetName eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="e654a-102">SelectionSetName Element for EntrySelectedBy for WideControl (Format)</span></span>

<span data-ttu-id="e654a-103">.NET-objektumokat a definíció egy halmazát határozza meg.</span><span class="sxs-lookup"><span data-stu-id="e654a-103">Specifies a set of .NET objects for the definition.</span></span> <span data-ttu-id="e654a-104">A definíció használatos, amikor ezek az objektumok egyike jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="e654a-104">The definition is used whenever one of these objects is displayed.</span></span>

<span data-ttu-id="e654a-105">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézet elem (formátum) WideControl elem (formátum) WideEntries elem (formátum) WideEntry elem (formátum) EntrySelectedBy elem WideEntry (formátum) SelectionSetName elem számára EntrySelectedBy a WideEntry (formátum)</span><span class="sxs-lookup"><span data-stu-id="e654a-105">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) WideControl Element (Format) WideEntries Element (Format) WideEntry Element (Format) EntrySelectedBy Element for WideEntry (Format) SelectionSetName Element for EntrySelectedBy for WideEntry (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="e654a-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="e654a-106">Syntax</span></span>

```xml
<SelectionSetName>NameofSelectionSet</SelectionSetName>

```

## <a name="attributes-and-elements"></a><span data-ttu-id="e654a-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="e654a-107">Attributes and Elements</span></span>

<span data-ttu-id="e654a-108">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `SelectionSetName` elemet.</span><span class="sxs-lookup"><span data-stu-id="e654a-108">The following sections describe the attributes, child elements, and the parent element of the `SelectionSetName` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="e654a-109">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="e654a-109">Attributes</span></span>

<span data-ttu-id="e654a-110">Nincs.</span><span class="sxs-lookup"><span data-stu-id="e654a-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="e654a-111">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="e654a-111">Child Elements</span></span>

<span data-ttu-id="e654a-112">Nincs.</span><span class="sxs-lookup"><span data-stu-id="e654a-112">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="e654a-113">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="e654a-113">Parent Elements</span></span>

|<span data-ttu-id="e654a-114">Elem</span><span class="sxs-lookup"><span data-stu-id="e654a-114">Element</span></span>|<span data-ttu-id="e654a-115">Leírás</span><span class="sxs-lookup"><span data-stu-id="e654a-115">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="e654a-116">EntrySelectedBy eleme WideEntry (formátum)</span><span class="sxs-lookup"><span data-stu-id="e654a-116">EntrySelectedBy Element for WideEntry (Format)</span></span>](./entryselectedby-element-for-wideentry-format.md)|<span data-ttu-id="e654a-117">A .NET-típusokat, amelyek a széles körű bejegyzés vagy a feltétellel, hogy léteznie kell használni a bejegyzés határozza meg.</span><span class="sxs-lookup"><span data-stu-id="e654a-117">Defines the .NET types that use this wide entry or the condition that must exist for this entry to be used.</span></span>|

## <a name="text-value"></a><span data-ttu-id="e654a-118">Szöveges érték</span><span class="sxs-lookup"><span data-stu-id="e654a-118">Text Value</span></span>

<span data-ttu-id="e654a-119">Adja meg a kijelölt csoport nevét.</span><span class="sxs-lookup"><span data-stu-id="e654a-119">Specify the name of the selection set.</span></span>

## <a name="remarks"></a><span data-ttu-id="e654a-120">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="e654a-120">Remarks</span></span>

<span data-ttu-id="e654a-121">Minden egyes definíciójában meg kell adni, egy típusnév, kijelölés set vagy kiválasztási feltételnek.</span><span class="sxs-lookup"><span data-stu-id="e654a-121">Each definition must specify one type name, selection set, or selection condition.</span></span>

<span data-ttu-id="e654a-122">Kijelölt csoportok általában akkor használják, ha meg szeretné több nézetében lévő meghatározott felhasználói csoporttal használt objektumok.</span><span class="sxs-lookup"><span data-stu-id="e654a-122">Selection sets are typically used when you want to define a group of objects that are used in multiple views.</span></span> <span data-ttu-id="e654a-123">Például előfordulhat, hogy szeretne létrehozni a táblázatos nézetre, és megjelenítheti a ugyanazt az objektumhalmazt tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="e654a-123">For example, you might want to create a table view and a list view for the same set of objects.</span></span> <span data-ttu-id="e654a-124">Kijelölt csoportok meghatározása kapcsolatos további információkért lásd: [meghatározása beállítja az objektumok megjelenítéséhez](./defining-selection-sets.md).</span><span class="sxs-lookup"><span data-stu-id="e654a-124">For more information about defining selection sets, see [Defining Sets of Objects for a View](./defining-selection-sets.md).</span></span>

<span data-ttu-id="e654a-125">Egy széles nézet egyéb összetevőivel kapcsolatos további információkért lásd: [széles nézet létrehozásával](./creating-a-wide-view.md).</span><span class="sxs-lookup"><span data-stu-id="e654a-125">For more information about other components of a wide view, see [Creating a Wide View](./creating-a-wide-view.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="e654a-126">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="e654a-126">See Also</span></span>

[<span data-ttu-id="e654a-127">Egy széles nézet létrehozása</span><span class="sxs-lookup"><span data-stu-id="e654a-127">Creating a Wide View</span></span>](./creating-a-wide-view.md)

[<span data-ttu-id="e654a-128">Kijelölt csoportok meghatározása</span><span class="sxs-lookup"><span data-stu-id="e654a-128">Defining Selection Sets</span></span>](./defining-selection-sets.md)

[<span data-ttu-id="e654a-129">EntrySelectedBy eleme WideEntry (formátum)</span><span class="sxs-lookup"><span data-stu-id="e654a-129">EntrySelectedBy Element for WideEntry (Format)</span></span>](./entryselectedby-element-for-wideentry-format.md)

[<span data-ttu-id="e654a-130">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="e654a-130">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
