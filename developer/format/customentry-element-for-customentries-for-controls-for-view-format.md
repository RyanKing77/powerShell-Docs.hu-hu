---
title: CustomEntry elemet a vezérlők (formátum) nézet CustomEntries |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: c6739205-2bc9-4507-b2af-d19d548c2057
caps.latest.revision: 6
ms.openlocfilehash: b92b99d88992cf13dbf7bfbe88aad603615f3138
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62066498"
---
# <a name="customentry-element-for-customentries-for-controls-for-view-format"></a><span data-ttu-id="6003a-102">A Nézet Vezérlők eleméhez tartozó CustomEntries CustomEntry eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="6003a-102">CustomEntry Element for CustomEntries for Controls for View (Format)</span></span>

<span data-ttu-id="6003a-103">A vezérlőelem egy definíciót tartalmaz.</span><span class="sxs-lookup"><span data-stu-id="6003a-103">Provides a definition of the control.</span></span> <span data-ttu-id="6003a-104">Ez az elem szolgál a nézet által használható vezérlők meghatározásakor.</span><span class="sxs-lookup"><span data-stu-id="6003a-104">This element is used when defining controls that can be used by a view.</span></span>

<span data-ttu-id="6003a-105">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem vezérlők elem (formátum) vezérlőelem elem vezérlők, a nézet (formátum) CustomControl elem megtekintése (formátum) CustomEntries elemet a vezérlők a vezérlő A vezérlők (formátum) nézet CustomEntries megtekintése (formátum) CustomEntry elemhez CustomControl</span><span class="sxs-lookup"><span data-stu-id="6003a-105">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) Controls Element (Format) Control Element for Controls for View (Format) CustomControl Element for Control for Controls for View (Format) CustomEntries Element for CustomControl for View (Format) CustomEntry Element for CustomEntries for Controls for View (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="6003a-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="6003a-106">Syntax</span></span>

```xml
<CustomEntry>
  <EntrySelectedBy>...</EntrySelectedBy>
  <CustomItem>...</CustomItem>
</CustomEntry>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="6003a-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="6003a-107">Attributes and Elements</span></span>

<span data-ttu-id="6003a-108">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a szülő elemei a `CustomEntry` elemet.</span><span class="sxs-lookup"><span data-stu-id="6003a-108">The following sections describe attributes, child elements, and the parent elements of the `CustomEntry` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="6003a-109">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="6003a-109">Attributes</span></span>

<span data-ttu-id="6003a-110">Nincs.</span><span class="sxs-lookup"><span data-stu-id="6003a-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="6003a-111">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="6003a-111">Child Elements</span></span>

|<span data-ttu-id="6003a-112">Elem</span><span class="sxs-lookup"><span data-stu-id="6003a-112">Element</span></span>|<span data-ttu-id="6003a-113">Leírás</span><span class="sxs-lookup"><span data-stu-id="6003a-113">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="6003a-114">Nézet (formátum) vezérlők CustomEntry EntrySelectedBy elem.</span><span class="sxs-lookup"><span data-stu-id="6003a-114">EntrySelectedBy Element for CustomEntry for Controls for View (Format)</span></span>](./entryselectedby-element-for-customentry-for-controls-for-view-format.md)|<span data-ttu-id="6003a-115">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="6003a-115">Optional element.</span></span><br /><br /> <span data-ttu-id="6003a-116">A .NET-típusokat, amelyek a vezérlő definition vagy a feltétellel, hogy léteznie kell a definíció használandó határozza meg.</span><span class="sxs-lookup"><span data-stu-id="6003a-116">Defines the .NET types that use this control definition or the condition that must exist for this definition to be used.</span></span>|
|[<span data-ttu-id="6003a-117">Nézet (formátum) vezérlők CustomEntry CustomItem elem.</span><span class="sxs-lookup"><span data-stu-id="6003a-117">CustomItem Element for CustomEntry for Controls for View (Format)</span></span>](./customitem-element-for-customentry-for-controls-for-view-format.md)|<span data-ttu-id="6003a-118">Szükséges eleme.</span><span class="sxs-lookup"><span data-stu-id="6003a-118">Required element.</span></span><br /><br /> <span data-ttu-id="6003a-119">Határozza meg, hogyan a vezérlőelem megjeleníti-e az adatokat.</span><span class="sxs-lookup"><span data-stu-id="6003a-119">Defines how the control displays the data.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="6003a-120">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="6003a-120">Parent Elements</span></span>

|<span data-ttu-id="6003a-121">Elem</span><span class="sxs-lookup"><span data-stu-id="6003a-121">Element</span></span>|<span data-ttu-id="6003a-122">Leírás</span><span class="sxs-lookup"><span data-stu-id="6003a-122">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="6003a-123">A nézet (formátum) CustomControl CustomEntries elem</span><span class="sxs-lookup"><span data-stu-id="6003a-123">CustomEntries Element for CustomControl for View (Format)</span></span>](./customentries-element-for-customcontrol-for-view-format.md)|<span data-ttu-id="6003a-124">A definíciók vezérlő biztosít.</span><span class="sxs-lookup"><span data-stu-id="6003a-124">Provides the definitions for the control.</span></span>|

## <a name="remarks"></a><span data-ttu-id="6003a-125">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="6003a-125">Remarks</span></span>

## <a name="see-also"></a><span data-ttu-id="6003a-126">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="6003a-126">See Also</span></span>

[<span data-ttu-id="6003a-127">A nézet (formátum) CustomControl CustomEntries elem</span><span class="sxs-lookup"><span data-stu-id="6003a-127">CustomEntries Element for CustomControl for View (Format)</span></span>](./customentries-element-for-customcontrol-for-view-format.md)

[<span data-ttu-id="6003a-128">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="6003a-128">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
