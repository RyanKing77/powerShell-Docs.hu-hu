---
title: A GroupBy (formátum) SelectionCondition TypeName eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 290d38e3-b9bd-4382-9671-2e28b32b7260
caps.latest.revision: 6
ms.openlocfilehash: a4036b1e9de85da7e0029e02cca9e0eaed462f70
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56848775"
---
# <a name="typename-element-for-selectioncondition-for-groupby-format"></a><span data-ttu-id="93c3f-102">A GroupBy elemhez tartozó SelectionCondition TypeName eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="93c3f-102">TypeName Element for SelectionCondition for GroupBy (Format)</span></span>

<span data-ttu-id="93c3f-103">A .NET típusát, amely elindítja a feltételt határozza meg.</span><span class="sxs-lookup"><span data-stu-id="93c3f-103">Specifies a .NET type that triggers the condition.</span></span> <span data-ttu-id="93c3f-104">Ez az elem szolgál, hogyan jelenjen meg az objektumok egy új csoportot meghatározásakor.</span><span class="sxs-lookup"><span data-stu-id="93c3f-104">This element is used when defining how a new group of objects is displayed.</span></span>

<span data-ttu-id="93c3f-105">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem GroupBy elem megtekintése (formátum) CustomControl elem a GroupBy (formátum) CustomEntry elemhez tartozó CustomControl GroupBy (formátum) CustomEntries elemhez GroupBy (formátum) EntrySelectedBy elem CustomEntry EntrySelectedBy SelectionCondition GroupBy (formátum) esetében a GroupBy (formátum) TypeName elemhez tartozó GroupBy (formátum) SelectionCondition elemhez tartozó CustomControl</span><span class="sxs-lookup"><span data-stu-id="93c3f-105">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) GroupBy Element for View (Format) CustomControl Element for GroupBy (Format) CustomEntries Element for CustomControl for GroupBy (Format) CustomEntry Element for CustomControl for GroupBy (Format) EntrySelectedBy Element for CustomEntry for GroupBy (Format) SelectionCondition Element for EntrySelectedBy for GroupBy (Format) TypeName Element for SelectionCondition for GroupBy  (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="93c3f-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="93c3f-106">Syntax</span></span>

```xml
<TypeName>Nameof.NetType</TypeName>

```

## <a name="attributes-and-elements"></a><span data-ttu-id="93c3f-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="93c3f-107">Attributes and Elements</span></span>

<span data-ttu-id="93c3f-108">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `TypeName` elemet.</span><span class="sxs-lookup"><span data-stu-id="93c3f-108">The following sections describe attributes, child elements, and the parent element of the `TypeName` Element.</span></span>

### <a name="attributes"></a><span data-ttu-id="93c3f-109">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="93c3f-109">Attributes</span></span>

<span data-ttu-id="93c3f-110">Nincs.</span><span class="sxs-lookup"><span data-stu-id="93c3f-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="93c3f-111">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="93c3f-111">Child Elements</span></span>

<span data-ttu-id="93c3f-112">Nincs.</span><span class="sxs-lookup"><span data-stu-id="93c3f-112">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="93c3f-113">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="93c3f-113">Parent Elements</span></span>

|<span data-ttu-id="93c3f-114">Elem</span><span class="sxs-lookup"><span data-stu-id="93c3f-114">Element</span></span>|<span data-ttu-id="93c3f-115">Leírás</span><span class="sxs-lookup"><span data-stu-id="93c3f-115">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="93c3f-116">A GroupBy (formátum) EntrySelectedBy SelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="93c3f-116">SelectionCondition Element for EntrySelectedBy for GroupBy (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-groupby-format.md)|<span data-ttu-id="93c3f-117">Határozza meg egy feltételt, amely a vezérlőelem definíciójában használt léteznie kell.</span><span class="sxs-lookup"><span data-stu-id="93c3f-117">Defines a condition that must exist for the control definition to be used.</span></span>|

## <a name="text-value"></a><span data-ttu-id="93c3f-118">Szöveges érték</span><span class="sxs-lookup"><span data-stu-id="93c3f-118">Text Value</span></span>

<span data-ttu-id="93c3f-119">Adja meg a teljes nevet, a .NET-típus, például `System.IO.DirectoryInfo`.</span><span class="sxs-lookup"><span data-stu-id="93c3f-119">Specify the fully qualified name of the .NET type, such as `System.IO.DirectoryInfo`.</span></span>

## <a name="remarks"></a><span data-ttu-id="93c3f-120">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="93c3f-120">Remarks</span></span>

<span data-ttu-id="93c3f-121">Ha ez az elem meg van adva, nem adható meg a `SelectionSetName` elemet.</span><span class="sxs-lookup"><span data-stu-id="93c3f-121">When this element is specified, you cannot specify the `SelectionSetName` element.</span></span> <span data-ttu-id="93c3f-122">További információ a kiválasztási feltételek meghatározása: [feltételek meghatározása az adatok megjelenítése](./defining-conditions-for-displaying-data.md).</span><span class="sxs-lookup"><span data-stu-id="93c3f-122">For more information about defining selection conditions, see [Defining Conditions for Displaying Data](./defining-conditions-for-displaying-data.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="93c3f-123">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="93c3f-123">See Also</span></span>

[<span data-ttu-id="93c3f-124">A GroupBy (formátum) EntrySelectedBy SelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="93c3f-124">SelectionCondition Element for EntrySelectedBy for GroupBy (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-groupby-format.md)

[<span data-ttu-id="93c3f-125">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="93c3f-125">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
