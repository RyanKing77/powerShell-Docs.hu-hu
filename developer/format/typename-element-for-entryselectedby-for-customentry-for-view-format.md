---
title: A nézet (formátum) CustomEntry EntrySelectedBy TypeName eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 76548af7-05bd-4d12-bf71-6fb69c434ef2
caps.latest.revision: 10
ms.openlocfilehash: c3dd761cd9b6c468d4833ea35b897ba5d425f598
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56848796"
---
# <a name="typename-element-for-entryselectedby-for-customentry-for-view-format"></a><span data-ttu-id="474ba-102">A Nézet CustomEntry eleméhez tartozó EntrySelectedBy TypeName eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="474ba-102">TypeName Element for EntrySelectedBy for CustomEntry for View (Format)</span></span>

<span data-ttu-id="474ba-103">Ez a definíció az egyéni vezérlő nézet használó .NET típust határozzon meg.</span><span class="sxs-lookup"><span data-stu-id="474ba-103">Specifies a .NET type that uses this definition of the custom control view.</span></span> <span data-ttu-id="474ba-104">Nincs korlátozva a definíciófrissítés számára megadható típusok számával.</span><span class="sxs-lookup"><span data-stu-id="474ba-104">There is no limit to the number of types that can be specified for a definition.</span></span>

<span data-ttu-id="474ba-105">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézet elem (formátum) CustomControl elem (formátum) CustomEntries eleme CustomControl számára a nézet (formátum) EntrySelectedBy CustomEntries megtekintése (formátum) CustomEntry elemhez Megtekintése (formátum) TypeName elemhez tartozó EntrySelectedBy CustomEntry nézet (formátum) a CustomEntry elem.</span><span class="sxs-lookup"><span data-stu-id="474ba-105">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) CustomControl Element (Format) CustomEntries Element for CustomControl for View (Format) CustomEntry Element for CustomEntries for View (Format) EntrySelectedBy Element for CustomEntry for View (Format) TypeName Element for EntrySelectedBy for CustomEntry for View (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="474ba-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="474ba-106">Syntax</span></span>

```xml
<TypeName>Nameof.NetType</TypeName>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="474ba-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="474ba-107">Attributes and Elements</span></span>

<span data-ttu-id="474ba-108">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `TypeName` elemet.</span><span class="sxs-lookup"><span data-stu-id="474ba-108">The following sections describe attributes, child elements, and the parent element of the `TypeName` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="474ba-109">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="474ba-109">Attributes</span></span>

<span data-ttu-id="474ba-110">Nincs.</span><span class="sxs-lookup"><span data-stu-id="474ba-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="474ba-111">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="474ba-111">Child Elements</span></span>

<span data-ttu-id="474ba-112">Nincs.</span><span class="sxs-lookup"><span data-stu-id="474ba-112">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="474ba-113">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="474ba-113">Parent Elements</span></span>

|<span data-ttu-id="474ba-114">Elem</span><span class="sxs-lookup"><span data-stu-id="474ba-114">Element</span></span>|<span data-ttu-id="474ba-115">Leírás</span><span class="sxs-lookup"><span data-stu-id="474ba-115">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="474ba-116">A nézet (formátum) CustomEntry EntrySelectedBy elem</span><span class="sxs-lookup"><span data-stu-id="474ba-116">EntrySelectedBy Element for CustomEntry for View (Format)</span></span>](./entryselectedby-element-for-customentry-for-customcontrol-for-view-format.md)|<span data-ttu-id="474ba-117">A .NET-típusokat, amelyek az egyéni vezérlő nézetdefinícióban, vagy a feltétellel, hogy léteznie kell a definíció használandó határoz meg.</span><span class="sxs-lookup"><span data-stu-id="474ba-117">Defines the .NET types that use this custom control view definition or the condition that must exist for this definition to be used.</span></span>|

## <a name="text-value"></a><span data-ttu-id="474ba-118">Szöveges érték</span><span class="sxs-lookup"><span data-stu-id="474ba-118">Text Value</span></span>

<span data-ttu-id="474ba-119">Adja meg a teljes nevet, a .NET-típus, például `System.IO.DirectoryInfo`.</span><span class="sxs-lookup"><span data-stu-id="474ba-119">Specify the fully qualified name of the .NET type, such as `System.IO.DirectoryInfo`.</span></span>

## <a name="remarks"></a><span data-ttu-id="474ba-120">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="474ba-120">Remarks</span></span>

<span data-ttu-id="474ba-121">Minden egyes egyéni vezérlőt nézetdefiníció rendelkeznie kell legalább egy típusnév, kijelölés set vagy meghatározott kiválasztási feltételnek.</span><span class="sxs-lookup"><span data-stu-id="474ba-121">Each custom control view definition must have at least one type name, selection set, or selection condition defined.</span></span>

<span data-ttu-id="474ba-122">Egyéni vezérlő nézet az összetevőivel kapcsolatos további információkért lásd: [egyéni vezérlők létrehozását](./creating-custom-controls.md).</span><span class="sxs-lookup"><span data-stu-id="474ba-122">For more information about the components of a custom control view, see [Creating Custom Controls](./creating-custom-controls.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="474ba-123">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="474ba-123">See Also</span></span>

[<span data-ttu-id="474ba-124">Egyéni vezérlők létrehozását</span><span class="sxs-lookup"><span data-stu-id="474ba-124">Creating Custom Controls</span></span>](./creating-custom-controls.md)

[<span data-ttu-id="474ba-125">A nézet (formátum) CustomEntry EntrySelectedBy elem</span><span class="sxs-lookup"><span data-stu-id="474ba-125">EntrySelectedBy Element for CustomEntry for View (Format)</span></span>](./entryselectedby-element-for-customentry-for-customcontrol-for-view-format.md)

[<span data-ttu-id="474ba-126">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="474ba-126">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
