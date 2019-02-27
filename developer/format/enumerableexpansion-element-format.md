---
title: EnumerableExpansion elem (formátum) |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 93d27173-9ae4-46e5-bb78-90525915cd70
caps.latest.revision: 9
ms.openlocfilehash: bc1e58c00ca8419f9204076f0a46050281e704db
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56847396"
---
# <a name="enumerableexpansion-element-format"></a><span data-ttu-id="246a4-102">EnumerableExpansion elem (Formátum)</span><span class="sxs-lookup"><span data-stu-id="246a4-102">EnumerableExpansion Element (Format)</span></span>

<span data-ttu-id="246a4-103">Határozza meg, hogyan adott .NET gyűjtemény objektumok kibontott nézetben megjelenésekor.</span><span class="sxs-lookup"><span data-stu-id="246a4-103">Defines how specific .NET collection objects are expanded when they are displayed in a view.</span></span>

<span data-ttu-id="246a4-104">Konfigurációs elem (formátum) DefaultSettings elem (formátum) EnumerableExpansions elem (formátum) EnumerableExpansion elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="246a4-104">Configuration Element (Format) DefaultSettings Element (Format) EnumerableExpansions Element (Format) EnumerableExpansion Element (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="246a4-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="246a4-105">Syntax</span></span>

```xml
<EnumerableExpansion>
  <EntrySelectedBy>...</EntrySelectedBy>
  <Expand>EnumOnly, CoreOnly, Both</Expand>
</EnumerableExpansion>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="246a4-106">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="246a4-106">Attributes and Elements</span></span>

<span data-ttu-id="246a4-107">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `EnumerableExpansion` elemet.</span><span class="sxs-lookup"><span data-stu-id="246a4-107">The following sections describe attributes, child elements, and the parent element of the `EnumerableExpansion` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="246a4-108">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="246a4-108">Attributes</span></span>

<span data-ttu-id="246a4-109">Nincs.</span><span class="sxs-lookup"><span data-stu-id="246a4-109">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="246a4-110">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="246a4-110">Child Elements</span></span>

|<span data-ttu-id="246a4-111">Elem</span><span class="sxs-lookup"><span data-stu-id="246a4-111">Element</span></span>|<span data-ttu-id="246a4-112">Leírás</span><span class="sxs-lookup"><span data-stu-id="246a4-112">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="246a4-113">EntrySelectedBy eleme EnumerableExpansion (formátum)</span><span class="sxs-lookup"><span data-stu-id="246a4-113">EntrySelectedBy Element for EnumerableExpansion (Format)</span></span>](./entryselectedby-element-for-enumerableexpansion-format.md)|<span data-ttu-id="246a4-114">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="246a4-114">Optional element.</span></span><br /><br /> <span data-ttu-id="246a4-115">Határozza meg, melyik gyűjtemény .NET-objektumokat a definíció szerint bontva.</span><span class="sxs-lookup"><span data-stu-id="246a4-115">Defines which .NET collection objects are expanded by this definition.</span></span>|
|[<span data-ttu-id="246a4-116">Bontsa ki az elemet (formátum)</span><span class="sxs-lookup"><span data-stu-id="246a4-116">Expand Element (Format)</span></span>](./expand-element-format.md)|<span data-ttu-id="246a4-117">Itt adhatja meg, hogyan az objektum ki van bontva, a definíció.</span><span class="sxs-lookup"><span data-stu-id="246a4-117">Specifies how the collection object is expanded for this definition.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="246a4-118">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="246a4-118">Parent Elements</span></span>

|<span data-ttu-id="246a4-119">Elem</span><span class="sxs-lookup"><span data-stu-id="246a4-119">Element</span></span>|<span data-ttu-id="246a4-120">Leírás</span><span class="sxs-lookup"><span data-stu-id="246a4-120">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="246a4-121">EnumerableExpansions elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="246a4-121">EnumerableExpansions Element (Format)</span></span>](./enumerableexpansions-element-format.md)|<span data-ttu-id="246a4-122">Határozza meg a különböző módokon objektumok kibontott nézetben megjelenésekor .NET gyűjteménynek.</span><span class="sxs-lookup"><span data-stu-id="246a4-122">Defines the different ways that .NET collection objects are expanded when they are displayed in a view.</span></span>|

## <a name="remarks"></a><span data-ttu-id="246a4-123">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="246a4-123">Remarks</span></span>

<span data-ttu-id="246a4-124">Ez az elem gyűjtemény és az objektumok a gyűjtemény megjelenítését meghatározására szolgál.</span><span class="sxs-lookup"><span data-stu-id="246a4-124">This element is used to define how collection objects and the objects in the collection are displayed.</span></span> <span data-ttu-id="246a4-125">Ebben az esetben a gyűjteményobjektum objektumra hivatkozik, bármely, amely támogatja a **"System.Collections.ICollection"** felületet.</span><span class="sxs-lookup"><span data-stu-id="246a4-125">In this case, a collection object refers to any object that supports the  **System.Collections.ICollection** interface.</span></span>

<span data-ttu-id="246a4-126">Az alapértelmezett viselkedést, hogy csak az objektumok tulajdonságait megjeleníti a gyűjteményben.</span><span class="sxs-lookup"><span data-stu-id="246a4-126">The default behavior is to display only the properties of the objects in the collection.</span></span>

## <a name="see-also"></a><span data-ttu-id="246a4-127">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="246a4-127">See Also</span></span>

[<span data-ttu-id="246a4-128">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="246a4-128">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
