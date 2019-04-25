---
title: A GroupBy (formátum) CustomControl CustomEntry eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 2987cb45-f646-45d4-b81b-7871e77af36f
caps.latest.revision: 5
ms.openlocfilehash: dcf4f8b2bbd422067ffdf9b3b4972e279e91edf9
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62066484"
---
# <a name="customentry-element-for-customcontrol-for-groupby-format"></a><span data-ttu-id="cde40-102">A GroupBy CustomControl elemének CustomEntry eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="cde40-102">CustomEntry Element for CustomControl for GroupBy (Format)</span></span>

<span data-ttu-id="cde40-103">A vezérlőelem egy definíciót tartalmaz.</span><span class="sxs-lookup"><span data-stu-id="cde40-103">Provides a definition of the control.</span></span> <span data-ttu-id="cde40-104">Ez az elem szolgál, hogyan jelenjen meg az objektumok egy új csoportot meghatározásakor.</span><span class="sxs-lookup"><span data-stu-id="cde40-104">This element is used when defining how a new group of objects is displayed.</span></span>

<span data-ttu-id="cde40-105">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem GroupBy elem megtekintése (formátum) CustomControl elem a GroupBy (formátum) CustomEntry elemhez tartozó CustomControl GroupBy (formátum) CustomEntries elemhez CustomControl a GroupBy (formátum)</span><span class="sxs-lookup"><span data-stu-id="cde40-105">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) GroupBy Element for View (Format) CustomControl Element for GroupBy (Format) CustomEntries Element for CustomControl for GroupBy (Format) CustomEntry Element for CustomControl for GroupBy (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="cde40-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="cde40-106">Syntax</span></span>

```xml
<CustomEntry>
  <EntrySelectedBy>...</EntrySelectedBy>
  <CustomItem>...</CustomItem>
</CustomEntry>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="cde40-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="cde40-107">Attributes and Elements</span></span>

<span data-ttu-id="cde40-108">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a szülő elemei a `CustomEntry` elemet.</span><span class="sxs-lookup"><span data-stu-id="cde40-108">The following sections describe attributes, child elements, and the parent elements of the `CustomEntry` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="cde40-109">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="cde40-109">Attributes</span></span>

<span data-ttu-id="cde40-110">Nincs.</span><span class="sxs-lookup"><span data-stu-id="cde40-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="cde40-111">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="cde40-111">Child Elements</span></span>

|<span data-ttu-id="cde40-112">Elem</span><span class="sxs-lookup"><span data-stu-id="cde40-112">Element</span></span>|<span data-ttu-id="cde40-113">Leírás</span><span class="sxs-lookup"><span data-stu-id="cde40-113">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="cde40-114">A GroupBy (formátum) CustomEntry EntrySelectedBy elem.</span><span class="sxs-lookup"><span data-stu-id="cde40-114">EntrySelectedBy Element for CustomEntry for GroupBy (Format)</span></span>](./entryselectedby-element-for-customentry-for-groupby-format.md)|<span data-ttu-id="cde40-115">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="cde40-115">Optional element.</span></span><br /><br /> <span data-ttu-id="cde40-116">A .NET-típusokat, amelyek a vezérlő definition vagy a feltétellel, hogy léteznie kell a definíció használandó határozza meg.</span><span class="sxs-lookup"><span data-stu-id="cde40-116">Defines the .NET types that use this control definition or the condition that must exist for this definition to be used.</span></span>|
|[<span data-ttu-id="cde40-117">A GroupBy (formátum) CustomEntry CustomItem elem.</span><span class="sxs-lookup"><span data-stu-id="cde40-117">CustomItem Element for CustomEntry for GroupBy (Format)</span></span>](./customitem-element-for-customentry-for-groupby-format.md)|<span data-ttu-id="cde40-118">Szükséges eleme.</span><span class="sxs-lookup"><span data-stu-id="cde40-118">Required element.</span></span><br /><br /> <span data-ttu-id="cde40-119">Határozza meg, hogyan a vezérlőelem megjeleníti-e az adatokat.</span><span class="sxs-lookup"><span data-stu-id="cde40-119">Defines how the control displays the data.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="cde40-120">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="cde40-120">Parent Elements</span></span>

|<span data-ttu-id="cde40-121">Elem</span><span class="sxs-lookup"><span data-stu-id="cde40-121">Element</span></span>|<span data-ttu-id="cde40-122">Leírás</span><span class="sxs-lookup"><span data-stu-id="cde40-122">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="cde40-123">A GroupBy (formátum) CustomControl CustomEntries elem.</span><span class="sxs-lookup"><span data-stu-id="cde40-123">CustomEntries Element for CustomControl for GroupBy (Format)</span></span>](./customentries-element-for-customcontrol-for-groupby-format.md)|<span data-ttu-id="cde40-124">A definíciók vezérlő biztosít.</span><span class="sxs-lookup"><span data-stu-id="cde40-124">Provides the definitions for the control.</span></span>|

## <a name="remarks"></a><span data-ttu-id="cde40-125">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="cde40-125">Remarks</span></span>

## <a name="see-also"></a><span data-ttu-id="cde40-126">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="cde40-126">See Also</span></span>

[<span data-ttu-id="cde40-127">A GroupBy (formátum) CustomEntry EntrySelectedBy elem.</span><span class="sxs-lookup"><span data-stu-id="cde40-127">EntrySelectedBy Element for CustomEntry for GroupBy (Format)</span></span>](./entryselectedby-element-for-customentry-for-groupby-format.md)

[<span data-ttu-id="cde40-128">A GroupBy (formátum) CustomEntry CustomItem elem.</span><span class="sxs-lookup"><span data-stu-id="cde40-128">CustomItem Element for CustomEntry for GroupBy (Format)</span></span>](./customitem-element-for-customentry-for-groupby-format.md)

[<span data-ttu-id="cde40-129">A GroupBy (formátum) CustomControl CustomEntries elem.</span><span class="sxs-lookup"><span data-stu-id="cde40-129">CustomEntries Element for CustomControl for GroupBy (Format)</span></span>](./customentries-element-for-customcontrol-for-groupby-format.md)

[<span data-ttu-id="cde40-130">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="cde40-130">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
