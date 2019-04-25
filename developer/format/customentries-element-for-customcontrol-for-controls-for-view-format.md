---
title: CustomEntries elemet a vezérlők (formátum) nézet CustomControl |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 3485958a-ba87-4932-907c-a8f140c4abdb
caps.latest.revision: 8
ms.openlocfilehash: 4856aee930285781a101868bd6cb67824585bce1
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62066583"
---
# <a name="customentries-element-for-customcontrol-for-controls-for-view-format"></a><span data-ttu-id="430be-102">A Nézet Vezérlők eleméhez tartozó CustomControl CustomEntries eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="430be-102">CustomEntries Element for CustomControl for Controls for View (Format)</span></span>

<span data-ttu-id="430be-103">A definíciók vezérlő biztosít.</span><span class="sxs-lookup"><span data-stu-id="430be-103">Provides the definitions for the control.</span></span> <span data-ttu-id="430be-104">Ez az elem szolgál a nézet által használható vezérlők meghatározásakor.</span><span class="sxs-lookup"><span data-stu-id="430be-104">This element is used when defining controls that can be used by a view.</span></span>

<span data-ttu-id="430be-105">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem vezérlők elem (formátum) vezérlőelem elem vezérlők, a nézet (formátum) CustomControl elem megtekintése (formátum) CustomEntries elemet a vezérlők a vezérlő CustomControl vezérlők nézet (formátum)</span><span class="sxs-lookup"><span data-stu-id="430be-105">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) Controls Element (Format) Control Element for Controls for View (Format) CustomControl Element for Control for Controls for View (Format) CustomEntries Element for CustomControl for Controls for View (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="430be-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="430be-106">Syntax</span></span>

```xml
<CustomEntries>
  <CustomEntry>...</CustomEntry>
</CustomEntries>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="430be-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="430be-107">Attributes and Elements</span></span>

<span data-ttu-id="430be-108">A következő szakaszok ismertetik az attribútumokat, a gyermekelemek és a szülő elemei a `CustomEntries` elemet.</span><span class="sxs-lookup"><span data-stu-id="430be-108">The following sections describe attributes, child elements, and parent elements of the `CustomEntries` element.</span></span> <span data-ttu-id="430be-109">Nincs maximális megadható az alárendelt elemek száma korlátozva van.</span><span class="sxs-lookup"><span data-stu-id="430be-109">There is no maximum limit to the number of child elements that can be specified.</span></span>

### <a name="attributes"></a><span data-ttu-id="430be-110">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="430be-110">Attributes</span></span>

<span data-ttu-id="430be-111">Nincs.</span><span class="sxs-lookup"><span data-stu-id="430be-111">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="430be-112">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="430be-112">Child Elements</span></span>

|<span data-ttu-id="430be-113">Elem</span><span class="sxs-lookup"><span data-stu-id="430be-113">Element</span></span>|<span data-ttu-id="430be-114">Leírás</span><span class="sxs-lookup"><span data-stu-id="430be-114">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="430be-115">Nézet (formátum) vezérlők CustomEntries CustomEntry elem.</span><span class="sxs-lookup"><span data-stu-id="430be-115">CustomEntry Element for CustomEntries for Controls for View (Format)</span></span>](./customentry-element-for-customentries-for-controls-for-view-format.md)|<span data-ttu-id="430be-116">Szükséges eleme.</span><span class="sxs-lookup"><span data-stu-id="430be-116">Required element.</span></span><br /><br /> <span data-ttu-id="430be-117">A vezérlőelem egy definíciót tartalmaz.</span><span class="sxs-lookup"><span data-stu-id="430be-117">Provides a definition of the control.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="430be-118">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="430be-118">Parent Elements</span></span>

|<span data-ttu-id="430be-119">Elem</span><span class="sxs-lookup"><span data-stu-id="430be-119">Element</span></span>|<span data-ttu-id="430be-120">Leírás</span><span class="sxs-lookup"><span data-stu-id="430be-120">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="430be-121">Vezérlő (formátum) nézet vezérlők CustomControl elem</span><span class="sxs-lookup"><span data-stu-id="430be-121">CustomControl Element for Control for Controls for View (Format)</span></span>](./customcontrol-element-for-control-for-controls-for-view-format.md)|<span data-ttu-id="430be-122">Határozza meg a nézet által használt vezérlő.</span><span class="sxs-lookup"><span data-stu-id="430be-122">Defines the control used by the view.</span></span>|

## <a name="remarks"></a><span data-ttu-id="430be-123">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="430be-123">Remarks</span></span>

<span data-ttu-id="430be-124">A legtöbb esetben egy vezérlőelem még csak egy definíciót, amely egy megadott `CustomEntry` elemet.</span><span class="sxs-lookup"><span data-stu-id="430be-124">In most cases, a control has only one definition, which is specified in a single `CustomEntry` element.</span></span> <span data-ttu-id="430be-125">Azonban úgy is víc definic adja meg, ha különböző .NET-objektumok megjelenítése ugyanazon vezérlő használata.</span><span class="sxs-lookup"><span data-stu-id="430be-125">However, it is possible to provide multiple definitions if you want to use the same control to display different .NET objects.</span></span> <span data-ttu-id="430be-126">Ezekben az esetekben definiálhat egy `CustomEntry` elem az egyes objektumok vagy objektumok közül.</span><span class="sxs-lookup"><span data-stu-id="430be-126">In those cases, you can define a `CustomEntry` element for each object or set of objects.</span></span>

## <a name="see-also"></a><span data-ttu-id="430be-127">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="430be-127">See Also</span></span>

[<span data-ttu-id="430be-128">Nézet (formátum) vezérlők CustomEntries CustomEntry elem.</span><span class="sxs-lookup"><span data-stu-id="430be-128">CustomEntry Element for CustomEntries for Controls for View (Format)</span></span>](./customentry-element-for-customentries-for-controls-for-view-format.md)

[<span data-ttu-id="430be-129">Vezérlő (formátum) nézet vezérlők CustomControl elem</span><span class="sxs-lookup"><span data-stu-id="430be-129">CustomControl Element for Control for Controls for View (Format)</span></span>](./customcontrol-element-for-control-for-controls-for-view-format.md)

[<span data-ttu-id="430be-130">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="430be-130">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
