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
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56848614"
---
# <a name="expand-element-format"></a><span data-ttu-id="0b074-102">Elem kibontása (Formátum)</span><span class="sxs-lookup"><span data-stu-id="0b074-102">Expand Element (Format)</span></span>

<span data-ttu-id="0b074-103">Itt adhatja meg, hogyan az objektum ki van bontva, a definíció.</span><span class="sxs-lookup"><span data-stu-id="0b074-103">Specifies how the collection object is expanded for this definition.</span></span>

<span data-ttu-id="0b074-104">Konfigurációs elem (formátum) DefaultSettings elem (formátum) EnumerableExpansions elem (formátum) EnumerableExpansion elem (formátum) bontsa ki az elemet (formátum)</span><span class="sxs-lookup"><span data-stu-id="0b074-104">Configuration Element (Format) DefaultSettings Element (Format) EnumerableExpansions Element (Format) EnumerableExpansion Element (Format) Expand Element (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="0b074-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="0b074-105">Syntax</span></span>

```xml
<Expand>EnumOnly, CoreOnly, Both</Expand>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="0b074-106">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="0b074-106">Attributes and Elements</span></span>

<span data-ttu-id="0b074-107">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `Expand` elemet.</span><span class="sxs-lookup"><span data-stu-id="0b074-107">The following sections describe attributes, child elements, and the parent element of the `Expand` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="0b074-108">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="0b074-108">Attributes</span></span>

<span data-ttu-id="0b074-109">Nincs.</span><span class="sxs-lookup"><span data-stu-id="0b074-109">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="0b074-110">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="0b074-110">Child Elements</span></span>

<span data-ttu-id="0b074-111">Nincs.</span><span class="sxs-lookup"><span data-stu-id="0b074-111">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="0b074-112">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="0b074-112">Parent Elements</span></span>

|<span data-ttu-id="0b074-113">Elem</span><span class="sxs-lookup"><span data-stu-id="0b074-113">Element</span></span>|<span data-ttu-id="0b074-114">Leírás</span><span class="sxs-lookup"><span data-stu-id="0b074-114">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="0b074-115">EnumerableExpansion elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="0b074-115">EnumerableExpansion Element (Format)</span></span>](./enumerableexpansion-element-format.md)|<span data-ttu-id="0b074-116">Határozza meg, hogyan adott .NET gyűjtemény objektumok kibontott nézetben megjelenésekor.</span><span class="sxs-lookup"><span data-stu-id="0b074-116">Defines how specific .NET collection objects are expanded when they are displayed in a view.</span></span>|

## <a name="text-value"></a><span data-ttu-id="0b074-117">Szöveges érték</span><span class="sxs-lookup"><span data-stu-id="0b074-117">Text Value</span></span>

<span data-ttu-id="0b074-118">Adja meg a következő értékek egyikét:</span><span class="sxs-lookup"><span data-stu-id="0b074-118">Specify one of the following values:</span></span>

- <span data-ttu-id="0b074-119">EnumOnly: Megjeleníti a gyűjtemény csak az objektumok tulajdonságait.</span><span class="sxs-lookup"><span data-stu-id="0b074-119">EnumOnly: Displays only the properties of the objects in the collection.</span></span>

- <span data-ttu-id="0b074-120">CoreOnly: Csak az objektum tulajdonságait jeleníti meg.</span><span class="sxs-lookup"><span data-stu-id="0b074-120">CoreOnly: Displays only the properties of the collection object.</span></span>

- <span data-ttu-id="0b074-121">Mindkettő: A gyűjtemény és az objektum tulajdonságait jeleníti meg az objektumok tulajdonságait.</span><span class="sxs-lookup"><span data-stu-id="0b074-121">Both: Displays the properties of the objects in the collection and the properties of the collection object.</span></span>

## <a name="remarks"></a><span data-ttu-id="0b074-122">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="0b074-122">Remarks</span></span>

<span data-ttu-id="0b074-123">Ez az elem gyűjtemény és az objektumok a gyűjtemény megjelenítését meghatározására szolgál.</span><span class="sxs-lookup"><span data-stu-id="0b074-123">This element is used to define how collection objects and the objects in the collection are displayed.</span></span> <span data-ttu-id="0b074-124">Ebben az esetben a gyűjteményobjektum objektumra hivatkozik, bármely, amely támogatja a **"System.Collections.ICollection"** felületet.</span><span class="sxs-lookup"><span data-stu-id="0b074-124">In this case, a collection object refers to any object that supports the  **System.Collections.ICollection** interface.</span></span>

<span data-ttu-id="0b074-125">Az alapértelmezett viselkedést, hogy csak az objektumok tulajdonságait megjeleníti a gyűjteményben.</span><span class="sxs-lookup"><span data-stu-id="0b074-125">The default behavior is to display only the properties of the objects in the collection.</span></span>

## <a name="see-also"></a><span data-ttu-id="0b074-126">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="0b074-126">See Also</span></span>

[<span data-ttu-id="0b074-127">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="0b074-127">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
