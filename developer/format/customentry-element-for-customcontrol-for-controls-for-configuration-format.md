---
title: CustomEntry elemet a vezérlők (formátum) konfiguráció CustomControl |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 9dfba86f-29b2-473c-9e98-9d679176acce
caps.latest.revision: 11
ms.openlocfilehash: 497485a388d1cdc834ecc1d1079b0714a7d7f9db
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56849475"
---
# <a name="customentry-element-for-customcontrol-for-controls-for-configuration-format"></a><span data-ttu-id="1290d-102">A Konfiguráció Vezérlők eleméhez tartozó CustomControl CustomEntry eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="1290d-102">CustomEntry Element for CustomControl for Controls for Configuration (Format)</span></span>

<span data-ttu-id="1290d-103">A közös ellenőrzési definíciójának biztosít.</span><span class="sxs-lookup"><span data-stu-id="1290d-103">Provides a definition of the common control.</span></span> <span data-ttu-id="1290d-104">Ez az elem szolgál egy közös vezérlőelem a formázási fájlban az összes nézetek által használható meghatározásakor.</span><span class="sxs-lookup"><span data-stu-id="1290d-104">This element is used when defining a common control that can be used by all the views in the formatting file.</span></span>

<span data-ttu-id="1290d-105">Konfigurációs elem (formátum) vezérlők elem Configuration (formátum) vezérlőelem elem vezérlők, a vezérlő konfigurációs (formátum) CustomEntries elemhez tartozó CustomControl Configuration (a Configuration (formátum) CustomControl elem Formátum) CustomEntry eleme CustomControl vezérlők konfiguráció (formátum)</span><span class="sxs-lookup"><span data-stu-id="1290d-105">Configuration Element (Format) Controls Element of Configuration (Format) Control Element for Controls for Configuration (Format) CustomControl Element for Control for Configuration (Format) CustomEntries Element for CustomControl for Configuration (Format) CustomEntry Element for CustomControl for Controls for Configuration (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="1290d-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="1290d-106">Syntax</span></span>

```xml
<CustomEntry>
  <EntrySelectedBy>...</EntrySelectedBy>
  <CustomItem>...</CustomItem>
</CustomEntry>

```

## <a name="attributes-and-elements"></a><span data-ttu-id="1290d-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="1290d-107">Attributes and Elements</span></span>

<span data-ttu-id="1290d-108">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `CustomEntry` elemet.</span><span class="sxs-lookup"><span data-stu-id="1290d-108">The following sections describe attributes, child elements, and the parent element of the `CustomEntry` element.</span></span> <span data-ttu-id="1290d-109">Meg kell adnia a cikkeket a definíció szerint jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="1290d-109">You must specify the items displayed by the definition.</span></span>

### <a name="attributes"></a><span data-ttu-id="1290d-110">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="1290d-110">Attributes</span></span>

<span data-ttu-id="1290d-111">Nincs.</span><span class="sxs-lookup"><span data-stu-id="1290d-111">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="1290d-112">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="1290d-112">Child Elements</span></span>

|<span data-ttu-id="1290d-113">Elem</span><span class="sxs-lookup"><span data-stu-id="1290d-113">Element</span></span>|<span data-ttu-id="1290d-114">Leírás</span><span class="sxs-lookup"><span data-stu-id="1290d-114">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="1290d-115">Konfiguráció (formátum) vezérlők CustomEntry EntrySelectedBy elem.</span><span class="sxs-lookup"><span data-stu-id="1290d-115">EntrySelectedBy Element for CustomEntry for Controls for Configuration (Format)</span></span>](./entryselectedby-element-for-customentry-for-controls-for-configuration-format.md)|<span data-ttu-id="1290d-116">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="1290d-116">Optional element.</span></span><br /><br /> <span data-ttu-id="1290d-117">A .NET-típusokat, amelyek a közös vezérlőelem vagy a feltételt, amelyet Pro tento ovládací prvek használandó léteznie kell a definíció határozza meg.</span><span class="sxs-lookup"><span data-stu-id="1290d-117">Defines the .NET types that use the definition of the common control or the condition that must exist for this control to be used.</span></span>|
|[<span data-ttu-id="1290d-118">Konfiguráció vezérlők CustomEntry CustomItem elem.</span><span class="sxs-lookup"><span data-stu-id="1290d-118">CustomItem Element for CustomEntry for Controls for Configuration</span></span>](./customitem-element-for-customentry-for-controls-for-configuration-format.md)|<span data-ttu-id="1290d-119">Szükséges eleme.</span><span class="sxs-lookup"><span data-stu-id="1290d-119">Required element.</span></span><br /><br /> <span data-ttu-id="1290d-120">Határozza meg a vezérlő által megjelenített adatokat, és hogyan jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="1290d-120">Defines what data is displayed by the control and how it is displayed.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="1290d-121">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="1290d-121">Parent Elements</span></span>

|<span data-ttu-id="1290d-122">Elem</span><span class="sxs-lookup"><span data-stu-id="1290d-122">Element</span></span>|<span data-ttu-id="1290d-123">Leírás</span><span class="sxs-lookup"><span data-stu-id="1290d-123">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="1290d-124">Konfiguráció (formátum) CustomControl CustomEntries elem.</span><span class="sxs-lookup"><span data-stu-id="1290d-124">CustomEntries Element for CustomControl for Configuration (Format)</span></span>](./customentries-element-for-customcontrol-for-controls-for-configuration-format.md)|<span data-ttu-id="1290d-125">A közös ellenőrzési a definíciókat tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="1290d-125">Provides the definitions of the common control.</span></span>|

## <a name="remarks"></a><span data-ttu-id="1290d-126">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="1290d-126">Remarks</span></span>

<span data-ttu-id="1290d-127">A legtöbb esetben csak egy-definícióra szükség minden egyes gyakori egyéni vezérlőt, de lehetséges több definíciókkal rendelkeznek, ha különböző .NET-objektumok megjelenítése ugyanazon vezérlő használata.</span><span class="sxs-lookup"><span data-stu-id="1290d-127">In most cases, only one definition is required for each common custom control, but it is possible to have multiple definitions if you want to use the same control to display different .NET objects.</span></span> <span data-ttu-id="1290d-128">Ezekben az esetekben adja meg egy külön meghatározása az egyes objektumok vagy objektumok közül.</span><span class="sxs-lookup"><span data-stu-id="1290d-128">In those cases, you can provide a separate definition for each object or set of objects.</span></span>

## <a name="see-also"></a><span data-ttu-id="1290d-129">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="1290d-129">See Also</span></span>

[<span data-ttu-id="1290d-130">Konfiguráció (formátum) CustomControl CustomEntries elem.</span><span class="sxs-lookup"><span data-stu-id="1290d-130">CustomEntries Element for CustomControl for Configuration (Format)</span></span>](./customentries-element-for-customcontrol-for-controls-for-configuration-format.md)

[<span data-ttu-id="1290d-131">Konfiguráció vezérlők CustomEntry CustomItem elem.</span><span class="sxs-lookup"><span data-stu-id="1290d-131">CustomItem Element for CustomEntry for Controls for Configuration</span></span>](./customitem-element-for-customentry-for-controls-for-configuration-format.md)

[<span data-ttu-id="1290d-132">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="1290d-132">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
