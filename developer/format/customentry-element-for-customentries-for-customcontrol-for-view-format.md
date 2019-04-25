---
title: A nézet (formátum) CustomControl CustomEntries CustomEntry eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ac3c0a25-f2ca-4e28-b3dc-9cb06a76d92a
caps.latest.revision: 11
ms.openlocfilehash: 7804155bffeb1f0df8339f797bf59f8def56a3fc
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62066447"
---
# <a name="customentry-element-for-customentries-for-customcontrol-for-view-format"></a><span data-ttu-id="1dd76-102">A Nézet CustomControl eleméhez tartozó CustomEntries CustomEntry eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="1dd76-102">CustomEntry Element for CustomEntries for CustomControl for View (Format)</span></span>

<span data-ttu-id="1dd76-103">Az egyéni vezérlő nézet definíciójának biztosít.</span><span class="sxs-lookup"><span data-stu-id="1dd76-103">Provides a definition of the custom control view.</span></span>

<span data-ttu-id="1dd76-104">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem CustomControl elem (formátum) CustomEntries eleme CustomControl megtekintése (formátum) CustomEntry elemhez tartozó CustomEntries nézet (formátum)</span><span class="sxs-lookup"><span data-stu-id="1dd76-104">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) CustomControl Element (Format) CustomEntries Element for CustomControl for View (Format) CustomEntry Element for CustomEntries for View (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="1dd76-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="1dd76-105">Syntax</span></span>

```xml
<CustomEntry>
  <EntrySelectedBy>...</EntrySelectedBy>
  <CustomItem>...</CustomItem>
</CustomEntry>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="1dd76-106">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="1dd76-106">Attributes and Elements</span></span>

<span data-ttu-id="1dd76-107">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `CustomEntry` elemet.</span><span class="sxs-lookup"><span data-stu-id="1dd76-107">The following sections describe attributes, child elements, and the parent element of the `CustomEntry` element.</span></span> <span data-ttu-id="1dd76-108">Meg kell adnia a cikkeket a definíció szerint jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="1dd76-108">You must specify the items displayed by the definition.</span></span>

### <a name="attributes"></a><span data-ttu-id="1dd76-109">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="1dd76-109">Attributes</span></span>

<span data-ttu-id="1dd76-110">Nincs.</span><span class="sxs-lookup"><span data-stu-id="1dd76-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="1dd76-111">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="1dd76-111">Child Elements</span></span>

|<span data-ttu-id="1dd76-112">Elem</span><span class="sxs-lookup"><span data-stu-id="1dd76-112">Element</span></span>|<span data-ttu-id="1dd76-113">Leírás</span><span class="sxs-lookup"><span data-stu-id="1dd76-113">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="1dd76-114">A nézet (formátum) CustomEntry EntrySelectedBy elem</span><span class="sxs-lookup"><span data-stu-id="1dd76-114">EntrySelectedBy Element for CustomEntry for View (Format)</span></span>](./entryselectedby-element-for-customentry-for-customcontrol-for-view-format.md)|<span data-ttu-id="1dd76-115">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="1dd76-115">Optional element.</span></span><br /><br /> <span data-ttu-id="1dd76-116">A .NET-típusokat, amelyek az egyéni vezérlő nézet vagy a feltétellel, hogy léteznie kell a definíció használandó meghatározását, határozza meg.</span><span class="sxs-lookup"><span data-stu-id="1dd76-116">Defines the .NET types that use the definition of the custom control view or the condition that must exist for this definition to be used.</span></span>|
|[<span data-ttu-id="1dd76-117">A nézet (formátum) CustomEntry CustomItem elem</span><span class="sxs-lookup"><span data-stu-id="1dd76-117">CustomItem Element for CustomEntry for View (Format)</span></span>](./customitem-element-for-customentry-for-customcontrol-for-view-format.md)|<span data-ttu-id="1dd76-118">Határozza meg az egyéni vezérlő definíciója egy vezérlőelemet.</span><span class="sxs-lookup"><span data-stu-id="1dd76-118">Defines a control for the custom control definition.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="1dd76-119">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="1dd76-119">Parent Elements</span></span>

|<span data-ttu-id="1dd76-120">Elem</span><span class="sxs-lookup"><span data-stu-id="1dd76-120">Element</span></span>|<span data-ttu-id="1dd76-121">Leírás</span><span class="sxs-lookup"><span data-stu-id="1dd76-121">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="1dd76-122">A nézet (formátum) CustomControl CustomEntries elem</span><span class="sxs-lookup"><span data-stu-id="1dd76-122">CustomEntries Element for CustomControl for View (Format)</span></span>](./customentries-element-for-customcontrol-for-view-format.md)|<span data-ttu-id="1dd76-123">Az egyéni vezérlő nézetében a definíciókat tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="1dd76-123">Provides the definitions of the custom control view.</span></span> <span data-ttu-id="1dd76-124">Az egyéni vezérlő nézetében meg kell adnia egy vagy több definíciót.</span><span class="sxs-lookup"><span data-stu-id="1dd76-124">The custom control view must specify one or more definitions.</span></span>|

## <a name="remarks"></a><span data-ttu-id="1dd76-125">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="1dd76-125">Remarks</span></span>

<span data-ttu-id="1dd76-126">A legtöbb esetben csak egyetlen definíciót minden egyes egyéni vezérlőt nézet megadása kötelező, de lehetséges több definíciókkal rendelkeznek, ha ugyanabban a nézetben különböző .NET-objektumok megjelenítéséhez használandó.</span><span class="sxs-lookup"><span data-stu-id="1dd76-126">In most cases, only one definition is required for each custom control view, but it is possible to have multiple definitions if you want to use the same view to display different .NET objects.</span></span> <span data-ttu-id="1dd76-127">Ezekben az esetekben adja meg egy külön meghatározása az egyes objektumok vagy objektumok közül.</span><span class="sxs-lookup"><span data-stu-id="1dd76-127">In those cases, you can provide a separate definition for each object or set of objects.</span></span>

## <a name="see-also"></a><span data-ttu-id="1dd76-128">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="1dd76-128">See Also</span></span>

[<span data-ttu-id="1dd76-129">CustomControl elem nézet (formátum)</span><span class="sxs-lookup"><span data-stu-id="1dd76-129">CustomControl Element for View (Format)</span></span>](./customcontrol-element-for-view-format.md)

[<span data-ttu-id="1dd76-130">A nézet (formátum) CustomEntry CustomItem elem</span><span class="sxs-lookup"><span data-stu-id="1dd76-130">CustomItem Element for CustomEntry for View (Format)</span></span>](./customitem-element-for-customentry-for-customcontrol-for-view-format.md)

[<span data-ttu-id="1dd76-131">A nézet (formátum) CustomEntry EntrySelectedBy elem</span><span class="sxs-lookup"><span data-stu-id="1dd76-131">EntrySelectedBy Element for CustomEntry for View (Format)</span></span>](./entryselectedby-element-for-customentry-for-customcontrol-for-view-format.md)

[<span data-ttu-id="1dd76-132">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="1dd76-132">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
