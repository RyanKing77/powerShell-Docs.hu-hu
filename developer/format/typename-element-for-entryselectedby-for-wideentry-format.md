---
title: EntrySelectedBy WideEntry (formátum) a TypeName eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 81a91c74-6229-4b64-aa2b-9123e8b7e9e5
caps.latest.revision: 11
ms.openlocfilehash: be35f6e9e2ad0b2d9a21a91c053aa0f70cafaf9c
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56851463"
---
# <a name="typename-element-for-entryselectedby-for-wideentry-format"></a><span data-ttu-id="1a6d1-102">A WideEntry elemhez tartozó EntrySelectedBy TypeName eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="1a6d1-102">TypeName Element for EntrySelectedBy for WideEntry (Format)</span></span>

<span data-ttu-id="1a6d1-103">A definíció egy .NET típusát határozza meg.</span><span class="sxs-lookup"><span data-stu-id="1a6d1-103">Specifies a .NET type for the definition.</span></span> <span data-ttu-id="1a6d1-104">A definíció használatos, amikor az objektum jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="1a6d1-104">The definition is used whenever this object is displayed.</span></span>

<span data-ttu-id="1a6d1-105">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem WideControl elem (formátum) WideEntries elem (formátum) WideEntry elem (formátum) EntrySelectedBy elem WideEntry (formátum) TypeName elemhez tartozó WideEntry) Formátum)</span><span class="sxs-lookup"><span data-stu-id="1a6d1-105">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) WideControl Element (Format) WideEntries Element (Format) WideEntry Element (Format) EntrySelectedBy Element for WideEntry (Format) TypeName Element for WideEntry (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="1a6d1-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="1a6d1-106">Syntax</span></span>

```xml
<TypeName>Nameof.NetType</TypeName>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="1a6d1-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="1a6d1-107">Attributes and Elements</span></span>

<span data-ttu-id="1a6d1-108">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `TypeName` elemet.</span><span class="sxs-lookup"><span data-stu-id="1a6d1-108">The following sections describe the attributes, child elements, and the parent element of the `TypeName` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="1a6d1-109">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="1a6d1-109">Attributes</span></span>

<span data-ttu-id="1a6d1-110">Nincs.</span><span class="sxs-lookup"><span data-stu-id="1a6d1-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="1a6d1-111">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="1a6d1-111">Child Elements</span></span>

<span data-ttu-id="1a6d1-112">Nincs.</span><span class="sxs-lookup"><span data-stu-id="1a6d1-112">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="1a6d1-113">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="1a6d1-113">Parent Elements</span></span>

|<span data-ttu-id="1a6d1-114">Elem</span><span class="sxs-lookup"><span data-stu-id="1a6d1-114">Element</span></span>|<span data-ttu-id="1a6d1-115">Leírás</span><span class="sxs-lookup"><span data-stu-id="1a6d1-115">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="1a6d1-116">EntrySelectedBy eleme WideEntry (formátum)</span><span class="sxs-lookup"><span data-stu-id="1a6d1-116">EntrySelectedBy Element for WideEntry (Format)</span></span>](./entryselectedby-element-for-wideentry-format.md)|<span data-ttu-id="1a6d1-117">A .NET-típusokat, amelyek a széles körű bejegyzés vagy a feltétellel, hogy léteznie kell használni a bejegyzés határozza meg.</span><span class="sxs-lookup"><span data-stu-id="1a6d1-117">Defines the .NET types that use this wide entry or the condition that must exist for this entry to be used.</span></span>|

## <a name="text-value"></a><span data-ttu-id="1a6d1-118">Szöveges érték</span><span class="sxs-lookup"><span data-stu-id="1a6d1-118">Text Value</span></span>

<span data-ttu-id="1a6d1-119">Adja meg a teljes nevet, a .NET-típus, például `System.IO.DirectoryInfo`.</span><span class="sxs-lookup"><span data-stu-id="1a6d1-119">Specify the fully qualified name of the .NET type, such as `System.IO.DirectoryInfo`.</span></span>

## <a name="remarks"></a><span data-ttu-id="1a6d1-120">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="1a6d1-120">Remarks</span></span>

<span data-ttu-id="1a6d1-121">Minden egyes széles bejegyzést adjon meg legalább egy .NET-típusok, egy kijelölt készlet vagy a kiválasztási feltételnek, amely a definíciójában használt léteznie kell.</span><span class="sxs-lookup"><span data-stu-id="1a6d1-121">Each wide entry must specify one or more .NET types, a selection set, or the selection condition that must exist for the definition to be used.</span></span>

<span data-ttu-id="1a6d1-122">Egy széles nézet egyéb összetevőivel kapcsolatos további információkért lásd: [széles nézet létrehozásával](./creating-a-wide-view.md).</span><span class="sxs-lookup"><span data-stu-id="1a6d1-122">For more information about other components of a wide view, see [Creating a Wide View](./creating-a-wide-view.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="1a6d1-123">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="1a6d1-123">See Also</span></span>

[<span data-ttu-id="1a6d1-124">Egy széles nézet létrehozása</span><span class="sxs-lookup"><span data-stu-id="1a6d1-124">Creating a Wide View</span></span>](./creating-a-wide-view.md)

[<span data-ttu-id="1a6d1-125">EntrySelectedBy eleme WideEntry (formátum)</span><span class="sxs-lookup"><span data-stu-id="1a6d1-125">EntrySelectedBy Element for WideEntry (Format)</span></span>](./entryselectedby-element-for-wideentry-format.md)

[<span data-ttu-id="1a6d1-126">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="1a6d1-126">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
