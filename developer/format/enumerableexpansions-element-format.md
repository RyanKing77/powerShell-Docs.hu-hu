---
title: EnumerableExpansions elem (formátum) |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 50c33892-2ade-44c2-906c-81e5f5ca21f2
caps.latest.revision: 9
ms.openlocfilehash: 1ecbda8a3b623757517019105e3b1ee46ccbb55c
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56849790"
---
# <a name="enumerableexpansions-element-format"></a><span data-ttu-id="caaa1-102">EnumerableExpansions elem (Formátum)</span><span class="sxs-lookup"><span data-stu-id="caaa1-102">EnumerableExpansions Element (Format)</span></span>

<span data-ttu-id="caaa1-103">Határozza meg, hogyan .NET gyűjtemény objektumok kibontott nézetben megjelenésekor.</span><span class="sxs-lookup"><span data-stu-id="caaa1-103">Defines how .NET collection objects are expanded when they are displayed in a view.</span></span>

<span data-ttu-id="caaa1-104">Konfigurációs elem (formátum) DefaultSettings elem (formátum) EnumerableExpansions elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="caaa1-104">Configuration Element (Format) DefaultSettings Element (Format) EnumerableExpansions Element (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="caaa1-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="caaa1-105">Syntax</span></span>

```xml
<EnumerableExpansions>
  <EnumerableExpansion>...</EnumerableExpansion>
</EnumerableExpansions>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="caaa1-106">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="caaa1-106">Attributes and Elements</span></span>

<span data-ttu-id="caaa1-107">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `EnumerableExpansions` elemet.</span><span class="sxs-lookup"><span data-stu-id="caaa1-107">The following sections describe attributes, child elements, and the parent element of the `EnumerableExpansions` element.</span></span> <span data-ttu-id="caaa1-108">Gyermekelemek használható száma nincs korlátozva van.</span><span class="sxs-lookup"><span data-stu-id="caaa1-108">There is no limit to the number of child elements that you can use.</span></span>

### <a name="attributes"></a><span data-ttu-id="caaa1-109">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="caaa1-109">Attributes</span></span>

<span data-ttu-id="caaa1-110">Nincs.</span><span class="sxs-lookup"><span data-stu-id="caaa1-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="caaa1-111">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="caaa1-111">Child Elements</span></span>

|<span data-ttu-id="caaa1-112">Elem</span><span class="sxs-lookup"><span data-stu-id="caaa1-112">Element</span></span>|<span data-ttu-id="caaa1-113">Leírás</span><span class="sxs-lookup"><span data-stu-id="caaa1-113">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="caaa1-114">EnumerableExpansion elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="caaa1-114">EnumerableExpansion Element (Format)</span></span>](./enumerableexpansion-element-format.md)|<span data-ttu-id="caaa1-115">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="caaa1-115">Optional element.</span></span><br /><br /> <span data-ttu-id="caaa1-116">Határozza meg a konkrét .NET gyűjtemény objektumokat, amelyeket a nézetben megjelenésekor bontva.</span><span class="sxs-lookup"><span data-stu-id="caaa1-116">Defines the specific .NET collection objects that are expanded when they are displayed in a view.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="caaa1-117">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="caaa1-117">Parent Elements</span></span>

|<span data-ttu-id="caaa1-118">Elem</span><span class="sxs-lookup"><span data-stu-id="caaa1-118">Element</span></span>|<span data-ttu-id="caaa1-119">Leírás</span><span class="sxs-lookup"><span data-stu-id="caaa1-119">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="caaa1-120">DefaultSettings elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="caaa1-120">DefaultSettings Element (Format)</span></span>](./defaultsettings-element-format.md)|<span data-ttu-id="caaa1-121">Határozza meg a formázási fájl összes nézet vonatkozó általános beállításokat.</span><span class="sxs-lookup"><span data-stu-id="caaa1-121">Defines common settings that apply to all the views of the formatting file.</span></span>|

## <a name="remarks"></a><span data-ttu-id="caaa1-122">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="caaa1-122">Remarks</span></span>

<span data-ttu-id="caaa1-123">Ez az elem gyűjtemény és az objektumok a gyűjtemény megjelenítését meghatározására szolgál.</span><span class="sxs-lookup"><span data-stu-id="caaa1-123">This element is used to define how collection objects and the objects in the collection are displayed.</span></span> <span data-ttu-id="caaa1-124">Ebben az esetben a gyűjteményobjektum objektumra hivatkozik, bármely, amely támogatja a **"System.Collections.ICollection"** felületet.</span><span class="sxs-lookup"><span data-stu-id="caaa1-124">In this case, a collection object refers to any object that supports the  **System.Collections.ICollection** interface.</span></span>

## <a name="see-also"></a><span data-ttu-id="caaa1-125">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="caaa1-125">See Also</span></span>

[<span data-ttu-id="caaa1-126">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="caaa1-126">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
