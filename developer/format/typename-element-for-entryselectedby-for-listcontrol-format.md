---
title: EntrySelectedBy ListControl (formátum) a TypeName eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 33c7345c-b808-4c1e-bd54-cb870b407432
caps.latest.revision: 14
ms.openlocfilehash: 0f7216d4dcc0380bceb47ea7c15b3d4a7e5ceeb2
ms.sourcegitcommit: caac7d098a448232304c9d6728e7340ec7517a71
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/16/2019
ms.locfileid: "58059694"
---
# <a name="typename-element-for-entryselectedby-for-listcontrol-format"></a><span data-ttu-id="74192-102">A ListControl elemhez tartozó EntrySelectedBy TypeName eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="74192-102">TypeName Element for EntrySelectedBy for ListControl (Format)</span></span>

<span data-ttu-id="74192-103">Ez a bejegyzés a listanézet használó .NET típust határozzon meg.</span><span class="sxs-lookup"><span data-stu-id="74192-103">Specifies a .NET type that uses this entry of the list view.</span></span> <span data-ttu-id="74192-104">Regisztrációslista-bejegyzés adható meg-típusok száma nincs korlátozva van.</span><span class="sxs-lookup"><span data-stu-id="74192-104">There is no limit to the number of types that can be specified for a list entry.</span></span>

<span data-ttu-id="74192-105">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézet elem (formátum) ListControl elem (formátum) ListEntries elem (formátum) ListEntry elem (formátum) EntrySelectedBy elem ListEntry (formátum) TypeName elem számára EntrySelectedBy a ListControl (formátum)</span><span class="sxs-lookup"><span data-stu-id="74192-105">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) ListControl Element (Format) ListEntries Element (Format) ListEntry Element (Format) EntrySelectedBy Element for ListEntry (Format) TypeName Element for EntrySelectedBy for ListControl (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="74192-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="74192-106">Syntax</span></span>

```xml
<TypeName>Nameof.NetType</TypeName>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="74192-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="74192-107">Attributes and Elements</span></span>

<span data-ttu-id="74192-108">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `TypeName` elemet.</span><span class="sxs-lookup"><span data-stu-id="74192-108">The following sections describe attributes, child elements, and the parent element of the `TypeName` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="74192-109">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="74192-109">Attributes</span></span>

<span data-ttu-id="74192-110">Nincs.</span><span class="sxs-lookup"><span data-stu-id="74192-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="74192-111">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="74192-111">Child Elements</span></span>

<span data-ttu-id="74192-112">Nincs.</span><span class="sxs-lookup"><span data-stu-id="74192-112">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="74192-113">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="74192-113">Parent Elements</span></span>

|<span data-ttu-id="74192-114">Elem</span><span class="sxs-lookup"><span data-stu-id="74192-114">Element</span></span>|<span data-ttu-id="74192-115">Leírás</span><span class="sxs-lookup"><span data-stu-id="74192-115">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="74192-116">EntrySelectedBy eleme ListEntry (formátum)</span><span class="sxs-lookup"><span data-stu-id="74192-116">EntrySelectedBy Element for ListEntry (Format)</span></span>](./entryselectedby-element-for-listentry-for-listcontrol-format.md)|<span data-ttu-id="74192-117">A .NET-típusokat, amelyek a regisztrációslista-bejegyzés vagy a feltétellel, hogy léteznie kell használni a bejegyzés határozza meg.</span><span class="sxs-lookup"><span data-stu-id="74192-117">Defines the .NET types that use this list entry or the condition that must exist for this entry to be used.</span></span>|

## <a name="text-value"></a><span data-ttu-id="74192-118">Szöveges érték</span><span class="sxs-lookup"><span data-stu-id="74192-118">Text Value</span></span>

<span data-ttu-id="74192-119">Adja meg például a .NET-típus teljes neve `System.IO.DirectoryInfo`.</span><span class="sxs-lookup"><span data-stu-id="74192-119">Specify the fully-qualified name of the .NET type, such as `System.IO.DirectoryInfo`.</span></span>

## <a name="remarks"></a><span data-ttu-id="74192-120">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="74192-120">Remarks</span></span>

<span data-ttu-id="74192-121">Minden egyes regisztrációslista-bejegyzés rendelkeznie kell legalább egy típusnév, kijelölés set vagy meghatározott kiválasztási feltételnek.</span><span class="sxs-lookup"><span data-stu-id="74192-121">Each list entry must have at least one type name, selection set, or selection condition defined.</span></span>

<span data-ttu-id="74192-122">Ez az elem használatának módja a következőben megjelenítheti kapcsolatos további információkért lásd: [listanézet](./creating-a-list-view.md).</span><span class="sxs-lookup"><span data-stu-id="74192-122">For more information about how this element is used in a list view, see [List View](./creating-a-list-view.md).</span></span>

## <a name="example"></a><span data-ttu-id="74192-123">Példa</span><span class="sxs-lookup"><span data-stu-id="74192-123">Example</span></span>

<span data-ttu-id="74192-124">Az alábbi példa bemutatja, hogyan adjon meg egy kiválasztása a lista nézet bejegyzés.</span><span class="sxs-lookup"><span data-stu-id="74192-124">The following example shows how to specify a selection set for an entry of a list view.</span></span>

```xml
<ListEntry>
  <EntrySelectedBy>
    <TypeName>Nameof.NetType</TypeName>
  </EntrySelectedBy>
  <ListItems>...</ListItems>
</ListEntry>
```

## <a name="see-also"></a><span data-ttu-id="74192-125">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="74192-125">See Also</span></span>

[<span data-ttu-id="74192-126">Lista nézet létrehozása</span><span class="sxs-lookup"><span data-stu-id="74192-126">Creating a List View</span></span>](./creating-a-list-view.md)

[<span data-ttu-id="74192-127">EntrySelectedBy eleme ListEntry (formátum)</span><span class="sxs-lookup"><span data-stu-id="74192-127">EntrySelectedBy Element for ListEntry (Format)</span></span>](./entryselectedby-element-for-listentry-for-listcontrol-format.md)

[<span data-ttu-id="74192-128">A ListEntry (formátum) EntrySelectedBy SelectionSetName elem.</span><span class="sxs-lookup"><span data-stu-id="74192-128">SelectionSetName Element for EntrySelectedBy for ListEntry (Format)</span></span>](./selectionsetname-element-for-entryselectedby-for-listcontrol-format.md)

[<span data-ttu-id="74192-129">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="74192-129">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
