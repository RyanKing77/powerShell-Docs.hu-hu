---
title: EntrySelectedBy TableControl (formátum) a TypeName eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: fd872ada-d476-4c4d-a788-ccac3f983070
caps.latest.revision: 10
ms.openlocfilehash: 7bbb47268a23fcb37a34e2287a6ce949313a13bb
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62083960"
---
# <a name="typename-element-for-entryselectedby-for-tablecontrol-format"></a><span data-ttu-id="116e1-102">A TableControl elemhez tartozó EntrySelectedBy TypeName eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="116e1-102">TypeName Element for EntrySelectedBy for TableControl (Format)</span></span>

<span data-ttu-id="116e1-103">Ez a bejegyzés a táblázat nézet használó .NET típust határozzon meg.</span><span class="sxs-lookup"><span data-stu-id="116e1-103">Specifies a .NET type that uses this entry of the table view.</span></span> <span data-ttu-id="116e1-104">A tábla bejegyzés adható meg-típusok száma nincs korlátozva van.</span><span class="sxs-lookup"><span data-stu-id="116e1-104">There is no limit to the number of types that can be specified for a table entry.</span></span>

<span data-ttu-id="116e1-105">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem TableControl elem (formátum) TableRowEntries elem (formátum) TableRowEntry elem (formátum) EntrySelectedBy elem (formátum) TypeName eleme EntrySelectedBy a TableRowEntry (formátum)</span><span class="sxs-lookup"><span data-stu-id="116e1-105">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) TableControl Element (Format) TableRowEntries Element (Format) TableRowEntry Element (Format) EntrySelectedBy Element (Format) TypeName Element for EntrySelectedBy for TableRowEntry (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="116e1-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="116e1-106">Syntax</span></span>

```xml
<TypeName>Nameof.NetType</TypeName>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="116e1-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="116e1-107">Attributes and Elements</span></span>

<span data-ttu-id="116e1-108">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `TypeName` elemet.</span><span class="sxs-lookup"><span data-stu-id="116e1-108">The following sections describe attributes, child elements, and the parent element of the `TypeName` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="116e1-109">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="116e1-109">Attributes</span></span>

<span data-ttu-id="116e1-110">Nincs.</span><span class="sxs-lookup"><span data-stu-id="116e1-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="116e1-111">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="116e1-111">Child Elements</span></span>

<span data-ttu-id="116e1-112">Nincs.</span><span class="sxs-lookup"><span data-stu-id="116e1-112">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="116e1-113">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="116e1-113">Parent Elements</span></span>

|<span data-ttu-id="116e1-114">Elem</span><span class="sxs-lookup"><span data-stu-id="116e1-114">Element</span></span>|<span data-ttu-id="116e1-115">Leírás</span><span class="sxs-lookup"><span data-stu-id="116e1-115">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="116e1-116">EntrySelectedBy elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="116e1-116">EntrySelectedBy Element (Format)</span></span>](./entryselectedby-element-for-tablerowentry-for-tablecontrol-format.md)|<span data-ttu-id="116e1-117">A .NET-típusokat, amelyek ezt a bejegyzést, vagy a feltétellel, hogy léteznie kell használni a bejegyzés határozza meg.</span><span class="sxs-lookup"><span data-stu-id="116e1-117">Defines the .NET types that use this entry or the condition that must exist for this entry to be used.</span></span>|

## <a name="text-value"></a><span data-ttu-id="116e1-118">A szöveges érték</span><span class="sxs-lookup"><span data-stu-id="116e1-118">Text Value</span></span>

<span data-ttu-id="116e1-119">Adja meg a .NET-típus nevét.</span><span class="sxs-lookup"><span data-stu-id="116e1-119">Specify the name of the .NET type.</span></span>

## <a name="remarks"></a><span data-ttu-id="116e1-120">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="116e1-120">Remarks</span></span>

<span data-ttu-id="116e1-121">Minden egyes regisztrációslista-bejegyzés rendelkeznie kell legalább egy típusnév, kijelölés set vagy meghatározott kiválasztási feltételnek.</span><span class="sxs-lookup"><span data-stu-id="116e1-121">Each list entry must have at least one type name, selection set, or selection condition defined.</span></span>

<span data-ttu-id="116e1-122">A táblázatos nézetre az összetevőivel kapcsolatos további információkért lásd: [tábla nézetek létrehozásával](./creating-a-table-view.md).</span><span class="sxs-lookup"><span data-stu-id="116e1-122">For more information about the components of a table view, see [Creating a Table View](./creating-a-table-view.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="116e1-123">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="116e1-123">See Also</span></span>

[<span data-ttu-id="116e1-124">Tábla nézet létrehozása</span><span class="sxs-lookup"><span data-stu-id="116e1-124">Creating a Table View</span></span>](./creating-a-table-view.md)

[<span data-ttu-id="116e1-125">EntrySelectedBy elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="116e1-125">EntrySelectedBy Element (Format)</span></span>](./entryselectedby-element-for-tablerowentry-for-tablecontrol-format.md)

[<span data-ttu-id="116e1-126">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="116e1-126">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
