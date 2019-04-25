---
title: Bontsa ki az elemet (formátum) |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: faa0314b-f6f1-44fd-ad2b-b00cbe38923f
caps.latest.revision: 9
ms.openlocfilehash: 8b924c989133b47e4d95d8429778003c76595d58
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62066005"
---
# <a name="expand-element-format"></a><span data-ttu-id="c8e19-102">Elem kibontása (Formátum)</span><span class="sxs-lookup"><span data-stu-id="c8e19-102">Expand Element (Format)</span></span>

<span data-ttu-id="c8e19-103">Itt adhatja meg, hogyan az objektum ki van bontva, a definíció.</span><span class="sxs-lookup"><span data-stu-id="c8e19-103">Specifies how the collection object is expanded for this definition.</span></span>

<span data-ttu-id="c8e19-104">Konfigurációs elem (formátum) DefaultSettings elem (formátum) EnumerableExpansions elem (formátum) EnumerableExpansion elem (formátum) bontsa ki az elemet (formátum)</span><span class="sxs-lookup"><span data-stu-id="c8e19-104">Configuration Element (Format) DefaultSettings Element (Format) EnumerableExpansions Element (Format) EnumerableExpansion Element (Format) Expand Element (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="c8e19-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="c8e19-105">Syntax</span></span>

```xml
<Expand>EnumOnly, CoreOnly, Both</Expand>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="c8e19-106">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="c8e19-106">Attributes and Elements</span></span>

<span data-ttu-id="c8e19-107">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `Expand` elemet.</span><span class="sxs-lookup"><span data-stu-id="c8e19-107">The following sections describe attributes, child elements, and the parent element of the `Expand` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="c8e19-108">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="c8e19-108">Attributes</span></span>

<span data-ttu-id="c8e19-109">Nincs.</span><span class="sxs-lookup"><span data-stu-id="c8e19-109">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="c8e19-110">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="c8e19-110">Child Elements</span></span>

<span data-ttu-id="c8e19-111">Nincs.</span><span class="sxs-lookup"><span data-stu-id="c8e19-111">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="c8e19-112">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="c8e19-112">Parent Elements</span></span>

|<span data-ttu-id="c8e19-113">Elem</span><span class="sxs-lookup"><span data-stu-id="c8e19-113">Element</span></span>|<span data-ttu-id="c8e19-114">Leírás</span><span class="sxs-lookup"><span data-stu-id="c8e19-114">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="c8e19-115">EnumerableExpansion elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="c8e19-115">EnumerableExpansion Element (Format)</span></span>](./enumerableexpansion-element-format.md)|<span data-ttu-id="c8e19-116">Határozza meg, hogyan adott .NET gyűjtemény objektumok kibontott nézetben megjelenésekor.</span><span class="sxs-lookup"><span data-stu-id="c8e19-116">Defines how specific .NET collection objects are expanded when they are displayed in a view.</span></span>|

## <a name="text-value"></a><span data-ttu-id="c8e19-117">A szöveges érték</span><span class="sxs-lookup"><span data-stu-id="c8e19-117">Text Value</span></span>

<span data-ttu-id="c8e19-118">Adja meg a következő értékek egyikét:</span><span class="sxs-lookup"><span data-stu-id="c8e19-118">Specify one of the following values:</span></span>

- <span data-ttu-id="c8e19-119">EnumOnly: Megjeleníti a gyűjtemény csak az objektumok tulajdonságait.</span><span class="sxs-lookup"><span data-stu-id="c8e19-119">EnumOnly: Displays only the properties of the objects in the collection.</span></span>

- <span data-ttu-id="c8e19-120">CoreOnly: Csak az objektum tulajdonságait jeleníti meg.</span><span class="sxs-lookup"><span data-stu-id="c8e19-120">CoreOnly: Displays only the properties of the collection object.</span></span>

- <span data-ttu-id="c8e19-121">Mindkettő: A gyűjtemény és az objektum tulajdonságait jeleníti meg az objektumok tulajdonságait.</span><span class="sxs-lookup"><span data-stu-id="c8e19-121">Both: Displays the properties of the objects in the collection and the properties of the collection object.</span></span>

## <a name="remarks"></a><span data-ttu-id="c8e19-122">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="c8e19-122">Remarks</span></span>

<span data-ttu-id="c8e19-123">Ez az elem gyűjtemény és az objektumok a gyűjtemény megjelenítését meghatározására szolgál.</span><span class="sxs-lookup"><span data-stu-id="c8e19-123">This element is used to define how collection objects and the objects in the collection are displayed.</span></span> <span data-ttu-id="c8e19-124">Ebben az esetben a gyűjteményobjektum objektumra hivatkozik, bármely, amely támogatja a **"System.Collections.ICollection"** felületet.</span><span class="sxs-lookup"><span data-stu-id="c8e19-124">In this case, a collection object refers to any object that supports the  **System.Collections.ICollection** interface.</span></span>

<span data-ttu-id="c8e19-125">Az alapértelmezett viselkedést, hogy csak az objektumok tulajdonságait megjeleníti a gyűjteményben.</span><span class="sxs-lookup"><span data-stu-id="c8e19-125">The default behavior is to display only the properties of the objects in the collection.</span></span>

## <a name="see-also"></a><span data-ttu-id="c8e19-126">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="c8e19-126">See Also</span></span>

[<span data-ttu-id="c8e19-127">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="c8e19-127">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
