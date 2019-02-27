---
title: CustomEntries elemet a vezérlők (formátum) konfiguráció CustomControl |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 80fc4de2-208f-4506-9a6a-c2675bb83be4
caps.latest.revision: 11
ms.openlocfilehash: abef6c91500f665c2366f221496d4cfd6444f5c9
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56847025"
---
# <a name="customentries-element-for-customcontrol-for-controls-for-configuration-format"></a><span data-ttu-id="153e6-102">A Konfiguráció Vezérlők eleméhez tartozó CustomControl CustomEntries eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="153e6-102">CustomEntries Element for CustomControl for Controls for Configuration (Format)</span></span>

<span data-ttu-id="153e6-103">A közös ellenőrzési definícióit tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="153e6-103">Provides the definitions of a common control.</span></span> <span data-ttu-id="153e6-104">Ez az elem szolgál egy közös vezérlőelem a formázási fájlban az összes nézetek által használható meghatározásakor.</span><span class="sxs-lookup"><span data-stu-id="153e6-104">This element is used when defining a common control that can be used by all the views in the formatting file.</span></span>

<span data-ttu-id="153e6-105">Konfigurációs elem (formátum) vezérlők elem Configuration (formátum) vezérlőelem elem vezérlők, a vezérlő konfigurációs (formátum) CustomEntries elemhez tartozó CustomControl Configuration (a Configuration (formátum) CustomControl elem Formátum)</span><span class="sxs-lookup"><span data-stu-id="153e6-105">Configuration Element (Format) Controls Element of Configuration (Format) Control Element for Controls for Configuration (Format) CustomControl Element for Control for Configuration (Format) CustomEntries Element for CustomControl for Configuration (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="153e6-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="153e6-106">Syntax</span></span>

```xml
<CustomEntries>
  <CustomEntry>...</CustomEntry>
</CustomEntries>

```

## <a name="attributes-and-elements"></a><span data-ttu-id="153e6-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="153e6-107">Attributes and Elements</span></span>

<span data-ttu-id="153e6-108">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `CustomEntries` elemet.</span><span class="sxs-lookup"><span data-stu-id="153e6-108">The following sections describe attributes, child elements, and the parent element of the `CustomEntries` element.</span></span> <span data-ttu-id="153e6-109">Meg kell adnia egy vagy több gyermekelemet.</span><span class="sxs-lookup"><span data-stu-id="153e6-109">You must specify one or more child elements.</span></span>

### <a name="attributes"></a><span data-ttu-id="153e6-110">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="153e6-110">Attributes</span></span>

<span data-ttu-id="153e6-111">Nincs.</span><span class="sxs-lookup"><span data-stu-id="153e6-111">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="153e6-112">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="153e6-112">Child Elements</span></span>

|<span data-ttu-id="153e6-113">Elem</span><span class="sxs-lookup"><span data-stu-id="153e6-113">Element</span></span>|<span data-ttu-id="153e6-114">Leírás</span><span class="sxs-lookup"><span data-stu-id="153e6-114">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="153e6-115">Konfiguráció (formátum) vezérlők CustomControl CustomEntry elem.</span><span class="sxs-lookup"><span data-stu-id="153e6-115">CustomEntry Element for CustomControl for Controls for Configuration (Format)</span></span>](./customentry-element-for-customcontrol-for-controls-for-configuration-format.md)|<span data-ttu-id="153e6-116">A közös ellenőrzési definíciójának biztosít.</span><span class="sxs-lookup"><span data-stu-id="153e6-116">Provides a definition of the common control.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="153e6-117">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="153e6-117">Parent Elements</span></span>

|<span data-ttu-id="153e6-118">Elem</span><span class="sxs-lookup"><span data-stu-id="153e6-118">Element</span></span>|<span data-ttu-id="153e6-119">Leírás</span><span class="sxs-lookup"><span data-stu-id="153e6-119">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="153e6-120">CustomControl elemet a vezérlési konfiguráció (formátum)</span><span class="sxs-lookup"><span data-stu-id="153e6-120">CustomControl Element for Control for Configuration (Format)</span></span>](./customcontrol-element-for-control-for-controls-for-configuration-format.md)|<span data-ttu-id="153e6-121">A közös ellenőrzési határozza meg.</span><span class="sxs-lookup"><span data-stu-id="153e6-121">Defines a common control.</span></span>|

## <a name="remarks"></a><span data-ttu-id="153e6-122">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="153e6-122">Remarks</span></span>

<span data-ttu-id="153e6-123">A legtöbb esetben egy vezérlőelem még csak egy definíciót, amely egy meghatározott `CustomEntry` elemet.</span><span class="sxs-lookup"><span data-stu-id="153e6-123">In most cases, a control has only one definition, which is defined in a single `CustomEntry` element.</span></span> <span data-ttu-id="153e6-124">Azonban lehetőség a több definíciókkal rendelkeznek, ha különböző .NET-objektumok megjelenítése ugyanazon vezérlő használata.</span><span class="sxs-lookup"><span data-stu-id="153e6-124">However it is possible to have multiple definitions if you want to use the same control to display different .NET objects.</span></span> <span data-ttu-id="153e6-125">Ezekben az esetekben definiálhat egy `CustomEntry` elem az egyes objektumok vagy objektumok közül.</span><span class="sxs-lookup"><span data-stu-id="153e6-125">In those cases, you can define a `CustomEntry` element for each object or set of objects.</span></span>

## <a name="see-also"></a><span data-ttu-id="153e6-126">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="153e6-126">See Also</span></span>

[<span data-ttu-id="153e6-127">CustomControl elemet a vezérlési konfiguráció (formátum)</span><span class="sxs-lookup"><span data-stu-id="153e6-127">CustomControl Element for Control for Configuration (Format)</span></span>](./customcontrol-element-for-control-for-controls-for-configuration-format.md)

[<span data-ttu-id="153e6-128">Konfiguráció (formátum) vezérlők CustomControl CustomEntry elem.</span><span class="sxs-lookup"><span data-stu-id="153e6-128">CustomEntry Element for CustomControl for Controls for Configuration (Format)</span></span>](./customentry-element-for-customcontrol-for-controls-for-configuration-format.md)

[<span data-ttu-id="153e6-129">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="153e6-129">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
