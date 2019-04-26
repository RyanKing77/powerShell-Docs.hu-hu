---
title: CustomEntries elemet a nézet (formátum) CustomControl |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: cb412831-94f7-4054-b19e-32c1b14c66dd
caps.latest.revision: 11
ms.openlocfilehash: 827baacd22ef258dd9b0c8a383a23fce7d975f7f
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62066515"
---
# <a name="customentries-element-for-customcontrol-for-view-format"></a><span data-ttu-id="0a579-102">A Nézet CustomControl elemének CustomEntries eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="0a579-102">CustomEntries Element for CustomControl for View (Format)</span></span>

<span data-ttu-id="0a579-103">Az egyéni vezérlő nézetében a definíciókat tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="0a579-103">Provides the definitions of the custom control view.</span></span> <span data-ttu-id="0a579-104">Az egyéni vezérlő nézetében meg kell adnia egy vagy több definíciót.</span><span class="sxs-lookup"><span data-stu-id="0a579-104">The custom control view must specify one or more definitions.</span></span>

<span data-ttu-id="0a579-105">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem CustomControl elem (formátum) CustomEntries eleme CustomControl nézet (formátum)</span><span class="sxs-lookup"><span data-stu-id="0a579-105">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) CustomControl Element (Format) CustomEntries Element for CustomControl for View (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="0a579-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="0a579-106">Syntax</span></span>

```xml
<CustomEntries>
  <CustomEntry>...</CustomEntry>
</CustomEntries>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="0a579-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="0a579-107">Attributes and Elements</span></span>

<span data-ttu-id="0a579-108">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `CustomControlEntries` elemet.</span><span class="sxs-lookup"><span data-stu-id="0a579-108">The following sections describe attributes, child elements, and the parent element of the `CustomControlEntries` element.</span></span> <span data-ttu-id="0a579-109">Meg kell adnia egy vagy több gyermekelemet.</span><span class="sxs-lookup"><span data-stu-id="0a579-109">You must specify one or more child elements.</span></span>

### <a name="attributes"></a><span data-ttu-id="0a579-110">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="0a579-110">Attributes</span></span>

<span data-ttu-id="0a579-111">Nincs.</span><span class="sxs-lookup"><span data-stu-id="0a579-111">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="0a579-112">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="0a579-112">Child Elements</span></span>

|<span data-ttu-id="0a579-113">Elem</span><span class="sxs-lookup"><span data-stu-id="0a579-113">Element</span></span>|<span data-ttu-id="0a579-114">Leírás</span><span class="sxs-lookup"><span data-stu-id="0a579-114">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="0a579-115">A nézet (formátum) CustomEntries CustomEntry elem</span><span class="sxs-lookup"><span data-stu-id="0a579-115">CustomEntry Element for CustomEntries for View (Format)</span></span>](./customentry-element-for-customentries-for-customcontrol-for-view-format.md)|<span data-ttu-id="0a579-116">Szükséges eleme.</span><span class="sxs-lookup"><span data-stu-id="0a579-116">Required element.</span></span><br /><br /> <span data-ttu-id="0a579-117">Az egyéni vezérlő nézet definíciójának biztosít.</span><span class="sxs-lookup"><span data-stu-id="0a579-117">Provides a definition of the custom control view.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="0a579-118">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="0a579-118">Parent Elements</span></span>

|<span data-ttu-id="0a579-119">Elem</span><span class="sxs-lookup"><span data-stu-id="0a579-119">Element</span></span>|<span data-ttu-id="0a579-120">Leírás</span><span class="sxs-lookup"><span data-stu-id="0a579-120">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="0a579-121">CustomControl elem nézet (formátum)</span><span class="sxs-lookup"><span data-stu-id="0a579-121">CustomControl Element for View (Format)</span></span>](./customcontrol-element-for-view-format.md)|<span data-ttu-id="0a579-122">Szükséges eleme.</span><span class="sxs-lookup"><span data-stu-id="0a579-122">Required element.</span></span><br /><br /> <span data-ttu-id="0a579-123">A nézet egy egyéni vezérlő formátumát határozza meg.</span><span class="sxs-lookup"><span data-stu-id="0a579-123">Defines a custom control format for the view.</span></span>|

## <a name="remarks"></a><span data-ttu-id="0a579-124">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="0a579-124">Remarks</span></span>

<span data-ttu-id="0a579-125">A legtöbb esetben egy vezérlőelem még csak egy definíciót, amely egy meghatározott `CustomEntry` elemet.</span><span class="sxs-lookup"><span data-stu-id="0a579-125">In most cases, a control has only one definition, which is defined in a single `CustomEntry` element.</span></span> <span data-ttu-id="0a579-126">Azonban lehetőség a több definíciókkal rendelkeznek, ha különböző .NET-objektumok megjelenítése ugyanazon vezérlő használata.</span><span class="sxs-lookup"><span data-stu-id="0a579-126">However it is possible to have multiple definitions if you want to use the same control to display different .NET objects.</span></span> <span data-ttu-id="0a579-127">Ezekben az esetekben definiálhat egy `CustomEntry` elem az egyes objektumok vagy objektumok közül.</span><span class="sxs-lookup"><span data-stu-id="0a579-127">In those cases, you can define a `CustomEntry` element for each object or set of objects.</span></span>

## <a name="see-also"></a><span data-ttu-id="0a579-128">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="0a579-128">See Also</span></span>

[<span data-ttu-id="0a579-129">CustomControl elem nézet (formátum)</span><span class="sxs-lookup"><span data-stu-id="0a579-129">CustomControl Element for View (Format)</span></span>](./customcontrol-element-for-view-format.md)

[<span data-ttu-id="0a579-130">A nézet (formátum) CustomEntries CustomEntry elem</span><span class="sxs-lookup"><span data-stu-id="0a579-130">CustomEntry Element for CustomEntries for View (Format)</span></span>](./customentry-element-for-customentries-for-customcontrol-for-view-format.md)

[<span data-ttu-id="0a579-131">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="0a579-131">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
