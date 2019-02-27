---
title: A GroupBy (formátum) EntrySelectedBy TypeName eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: b8b6739b-770c-432a-95ab-551c7507c51f
caps.latest.revision: 6
ms.openlocfilehash: 3b5ce60d3a0d76988af48f49445a5478a415d498
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56850777"
---
# <a name="typename-element-for-entryselectedby-for-groupby-format"></a><span data-ttu-id="3a8a0-102">A GroupBy elemhez tartozó EntrySelectedBy TypeName eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="3a8a0-102">TypeName Element for EntrySelectedBy for GroupBy (Format)</span></span>

<span data-ttu-id="3a8a0-103">Ez a definíció az egyéni vezérlő használó .NET típust határozzon meg.</span><span class="sxs-lookup"><span data-stu-id="3a8a0-103">Specifies a .NET type that uses this definition of the custom control.</span></span> <span data-ttu-id="3a8a0-104">Ez az elem szolgál, hogyan jelenjen meg az objektumok egy új csoportot meghatározásakor.</span><span class="sxs-lookup"><span data-stu-id="3a8a0-104">This element is used when defining how a new group of objects is displayed.</span></span>

<span data-ttu-id="3a8a0-105">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem GroupBy elem megtekintése (formátum) CustomControl elem a GroupBy (formátum) CustomEntry elemhez tartozó CustomControl GroupBy (formátum) CustomEntries elemhez CustomControl GroupBy (formátum) EntrySelectedBy elemhez tartozó CustomEntry GroupBy (formátum) TypeName elemhez tartozó EntrySelectedBy a GroupBy (formátum)</span><span class="sxs-lookup"><span data-stu-id="3a8a0-105">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) GroupBy Element for View (Format) CustomControl Element for GroupBy (Format) CustomEntries Element for CustomControl for GroupBy (Format) CustomEntry Element for CustomControl for GroupBy (Format) EntrySelectedBy Element for CustomEntry for GroupBy (Format) TypeName Element for EntrySelectedBy for GroupBy (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="3a8a0-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="3a8a0-106">Syntax</span></span>

```xml
<TypeName>Nameof.NetType</TypeName>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="3a8a0-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="3a8a0-107">Attributes and Elements</span></span>

<span data-ttu-id="3a8a0-108">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `TypeName` elemet.</span><span class="sxs-lookup"><span data-stu-id="3a8a0-108">The following sections describe attributes, child elements, and the parent element of the `TypeName` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="3a8a0-109">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="3a8a0-109">Attributes</span></span>

<span data-ttu-id="3a8a0-110">Nincs.</span><span class="sxs-lookup"><span data-stu-id="3a8a0-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="3a8a0-111">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="3a8a0-111">Child Elements</span></span>

<span data-ttu-id="3a8a0-112">Nincs.</span><span class="sxs-lookup"><span data-stu-id="3a8a0-112">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="3a8a0-113">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="3a8a0-113">Parent Elements</span></span>

|<span data-ttu-id="3a8a0-114">Elem</span><span class="sxs-lookup"><span data-stu-id="3a8a0-114">Element</span></span>|<span data-ttu-id="3a8a0-115">Leírás</span><span class="sxs-lookup"><span data-stu-id="3a8a0-115">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="3a8a0-116">A GroupBy (formátum) CustomEntry EntrySelectedBy elem.</span><span class="sxs-lookup"><span data-stu-id="3a8a0-116">EntrySelectedBy Element for CustomEntry for GroupBy (Format)</span></span>](./entryselectedby-element-for-customentry-for-groupby-format.md)|<span data-ttu-id="3a8a0-117">A .NET-típusokat, amelyek a vezérlő definition vagy a feltétellel, hogy léteznie kell a definíció használandó határozza meg.</span><span class="sxs-lookup"><span data-stu-id="3a8a0-117">Defines the .NET types that use this control definition or the condition that must exist for this definition to be used.</span></span>|

## <a name="text-value"></a><span data-ttu-id="3a8a0-118">Szöveges érték</span><span class="sxs-lookup"><span data-stu-id="3a8a0-118">Text Value</span></span>

<span data-ttu-id="3a8a0-119">Adja meg a teljes nevet, a .NET-típus, például `System.IO.DirectoryInfo`.</span><span class="sxs-lookup"><span data-stu-id="3a8a0-119">Specify the fully qualified name of the .NET type, such as `System.IO.DirectoryInfo`.</span></span>

## <a name="remarks"></a><span data-ttu-id="3a8a0-120">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="3a8a0-120">Remarks</span></span>

<span data-ttu-id="3a8a0-121">Minden vezérlő definíció rendelkeznie kell legalább egy típusnév, kijelölés set vagy meghatározott kiválasztási feltételnek.</span><span class="sxs-lookup"><span data-stu-id="3a8a0-121">Each control definition must have at least one type name, selection set, or selection condition defined.</span></span>

<span data-ttu-id="3a8a0-122">Egyéni vezérlő nézet az összetevőivel kapcsolatos további információkért lásd: [egyéni vezérlők létrehozását](./creating-custom-controls.md).</span><span class="sxs-lookup"><span data-stu-id="3a8a0-122">For more information about the components of a custom control view, see [Creating Custom Controls](./creating-custom-controls.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="3a8a0-123">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="3a8a0-123">See Also</span></span>

[<span data-ttu-id="3a8a0-124">Egyéni vezérlők létrehozását</span><span class="sxs-lookup"><span data-stu-id="3a8a0-124">Creating Custom Controls</span></span>](./creating-custom-controls.md)

[<span data-ttu-id="3a8a0-125">A GroupBy (formátum) CustomEntry EntrySelectedBy elem.</span><span class="sxs-lookup"><span data-stu-id="3a8a0-125">EntrySelectedBy Element for CustomEntry for GroupBy (Format)</span></span>](./entryselectedby-element-for-customentry-for-groupby-format.md)

[<span data-ttu-id="3a8a0-126">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="3a8a0-126">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
