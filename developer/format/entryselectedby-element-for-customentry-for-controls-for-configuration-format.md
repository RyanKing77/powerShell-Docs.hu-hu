---
title: EntrySelectedBy elemet a vezérlők (formátum) konfiguráció CustomEntry |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 30abae8f-c7f7-479d-ad85-19e07ddef204
caps.latest.revision: 10
ms.openlocfilehash: 81eca4f66f0057074612f2d60482b45adc36357b
ms.sourcegitcommit: caac7d098a448232304c9d6728e7340ec7517a71
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/16/2019
ms.locfileid: "58059218"
---
# <a name="entryselectedby-element-for-customentry-for-controls-for-configuration-format"></a><span data-ttu-id="d00af-102">A Konfiguráció Vezérlők eleméhez tartozó CustomEntry EntrySelectedBy eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="d00af-102">EntrySelectedBy Element for CustomEntry for Controls for Configuration (Format)</span></span>

<span data-ttu-id="d00af-103">A .NET-típusokat, amelyek a közös vezérlőelem vagy a feltételt, amelyet Pro tento ovládací prvek használandó léteznie kell a definíció határozza meg.</span><span class="sxs-lookup"><span data-stu-id="d00af-103">Defines the .NET types that use the definition of the common control or the condition that must exist for this control to be used.</span></span> <span data-ttu-id="d00af-104">Ez az elem szolgál egy közös vezérlőelem a formázási fájlban az összes nézetek által használható meghatározásakor.</span><span class="sxs-lookup"><span data-stu-id="d00af-104">This element is used when defining a common control that can be used by all the views in the formatting file.</span></span>

<span data-ttu-id="d00af-105">Konfigurációs elem (formátum) vezérlők elem Configuration (formátum) vezérlőelem elem vezérlők, a vezérlő konfigurációs (formátum) CustomEntries elemhez tartozó CustomControl Configuration (a Configuration (formátum) CustomControl elem Formátum) CustomEntry elemet a vezérlők CustomEntry vezérlők (formátum) konfiguráció esetén a Configuration (formátum) EntrySelectedBy elemhez CustomControl</span><span class="sxs-lookup"><span data-stu-id="d00af-105">Configuration Element (Format) Controls Element of Configuration (Format) Control Element for Controls for Configuration (Format) CustomControl Element for Control for Configuration (Format) CustomEntries Element for CustomControl for Configuration (Format) CustomEntry Element for CustomControl for Controls for Configuration (Format) EntrySelectedBy Element for CustomEntry for Controls for Configuration (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="d00af-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="d00af-106">Syntax</span></span>

```xml
<EntrySelectedBy>
  <TypeName>Nameof.NetType</TypeName>
  <SelectionSetName>SelectionSet</SelectionSetName>
  <SelectionCondition>...</SelectionCondition>
</EntrySelectedBy>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="d00af-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="d00af-107">Attributes and Elements</span></span>

<span data-ttu-id="d00af-108">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `EntrySelectedBy` elemet.</span><span class="sxs-lookup"><span data-stu-id="d00af-108">The following sections describe attributes, child elements, and the parent element of the `EntrySelectedBy` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="d00af-109">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="d00af-109">Attributes</span></span>

<span data-ttu-id="d00af-110">Nincs.</span><span class="sxs-lookup"><span data-stu-id="d00af-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="d00af-111">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="d00af-111">Child Elements</span></span>

|<span data-ttu-id="d00af-112">Elem</span><span class="sxs-lookup"><span data-stu-id="d00af-112">Element</span></span>|<span data-ttu-id="d00af-113">Leírás</span><span class="sxs-lookup"><span data-stu-id="d00af-113">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="d00af-114">Konfiguráció (formátum) vezérlők EntrySelectedBy SelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="d00af-114">SelectionCondition Element for EntrySelectedBy for Controls for Configuration (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-controls-for-configuration-format.md)|<span data-ttu-id="d00af-115">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="d00af-115">Optional element.</span></span><br /><br /> <span data-ttu-id="d00af-116">Határozza meg azt a feltételt, amelyet a közös ellenőrzési definíciójában használt léteznie kell.</span><span class="sxs-lookup"><span data-stu-id="d00af-116">Defines the condition that must exist for the common control definition to be used.</span></span>|
|[<span data-ttu-id="d00af-117">Konfiguráció (formátum) vezérlők EntrySelectedBy SelectionSetName elem.</span><span class="sxs-lookup"><span data-stu-id="d00af-117">SelectionSetName Element for EntrySelectedBy for Controls for Configuration (Format)</span></span>](./selectionsetname-element-for-selectioncondition-for-controls-for-configuration-format.md)|<span data-ttu-id="d00af-118">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="d00af-118">Optional element.</span></span><br /><br /> <span data-ttu-id="d00af-119">Ez a definíció, a közös ellenőrzési használó .NET-típusok egy halmazát határozza meg.</span><span class="sxs-lookup"><span data-stu-id="d00af-119">Specifies a set of .NET types that use this definition of the common control.</span></span>|
|[<span data-ttu-id="d00af-120">Konfiguráció (formátum) vezérlők EntrySelectedBy TypeName elem.</span><span class="sxs-lookup"><span data-stu-id="d00af-120">TypeName Element for EntrySelectedBy for Controls for Configuration (Format)</span></span>](./typename-element-for-entryselectedby-for-controls-for-configuration-format.md)|<span data-ttu-id="d00af-121">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="d00af-121">Optional element.</span></span><br /><br /> <span data-ttu-id="d00af-122">Ez a definíció, a közös ellenőrzési használó .NET típust határozzon meg.</span><span class="sxs-lookup"><span data-stu-id="d00af-122">Specifies a .NET type that uses this definition of the common control.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="d00af-123">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="d00af-123">Parent Elements</span></span>

|<span data-ttu-id="d00af-124">Elem</span><span class="sxs-lookup"><span data-stu-id="d00af-124">Element</span></span>|<span data-ttu-id="d00af-125">Leírás</span><span class="sxs-lookup"><span data-stu-id="d00af-125">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="d00af-126">Konfiguráció (formátum) vezérlők CustomControl CustomEntry elem.</span><span class="sxs-lookup"><span data-stu-id="d00af-126">CustomEntry Element for CustomControl for Controls for Configuration (Format)</span></span>](./customentry-element-for-customcontrol-for-controls-for-configuration-format.md)|<span data-ttu-id="d00af-127">A közös ellenőrzési definíciójának biztosít.</span><span class="sxs-lookup"><span data-stu-id="d00af-127">Provides a definition of the common control.</span></span>|

## <a name="remarks"></a><span data-ttu-id="d00af-128">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="d00af-128">Remarks</span></span>

<span data-ttu-id="d00af-129">Legalább egyes definíció rendelkeznie kell legalább egy .NET-típus, kijelölés set vagy a megadott kiválasztási feltétel.</span><span class="sxs-lookup"><span data-stu-id="d00af-129">At a minimum, each definition must have at least one .NET type, selection set, or selection condition specified.</span></span> <span data-ttu-id="d00af-130">Nincs típusa, a kijelölt csoportok, illetve a kiválasztási feltételek, Ön által megadott számú maximális korlátozva.</span><span class="sxs-lookup"><span data-stu-id="d00af-130">There is no maximum limit to the number of types, selection sets, or selection conditions that you can specify.</span></span>

## <a name="see-also"></a><span data-ttu-id="d00af-131">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="d00af-131">See Also</span></span>

[<span data-ttu-id="d00af-132">Konfiguráció (formátum) vezérlők EntrySelectedBy SelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="d00af-132">SelectionCondition Element for EntrySelectedBy for Controls for Configuration (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-controls-for-configuration-format.md)

[<span data-ttu-id="d00af-133">Konfiguráció (formátum) vezérlők EntrySelectedBy SelectionSetName elem.</span><span class="sxs-lookup"><span data-stu-id="d00af-133">SelectionSetName Element for EntrySelectedBy for Controls for Configuration (Format)</span></span>](./selectionsetname-element-for-selectioncondition-for-controls-for-configuration-format.md)

[<span data-ttu-id="d00af-134">Konfiguráció (formátum) vezérlők CustomControl CustomEntry elem.</span><span class="sxs-lookup"><span data-stu-id="d00af-134">CustomEntry Element for CustomControl for Controls for Configuration (Format)</span></span>](./customentry-element-for-customcontrol-for-controls-for-configuration-format.md)

[<span data-ttu-id="d00af-135">Konfiguráció (formátum) vezérlők EntrySelectedBy TypeName elem.</span><span class="sxs-lookup"><span data-stu-id="d00af-135">TypeName Element for EntrySelectedBy for Controls for Configuration (Format)</span></span>](./typename-element-for-selectioncondition-for-controls-for-configuration-format.md)

[<span data-ttu-id="d00af-136">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="d00af-136">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
