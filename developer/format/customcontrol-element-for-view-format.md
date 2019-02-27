---
title: Nézet (formátum) CustomControl elem |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 2edac16c-0b30-4985-ac84-0821aa9a9f6d
caps.latest.revision: 12
ms.openlocfilehash: bd0f7ca4de8dede97d1553cd62884ea45876e0c7
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56850490"
---
# <a name="customcontrol-element-for-view-format"></a><span data-ttu-id="6fa42-102">A Nézet CustomControl eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="6fa42-102">CustomControl Element for View (Format)</span></span>

<span data-ttu-id="6fa42-103">A nézet egy egyéni vezérlő formátumát határozza meg.</span><span class="sxs-lookup"><span data-stu-id="6fa42-103">Defines a custom control format for the view.</span></span>

<span data-ttu-id="6fa42-104">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem CustomControl elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="6fa42-104">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) CustomControl Element (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="6fa42-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="6fa42-105">Syntax</span></span>

```xml
<CustomControl>
  <CustomEntries>...</CustomEntries>
</CustomControl>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="6fa42-106">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="6fa42-106">Attributes and Elements</span></span>

<span data-ttu-id="6fa42-107">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `CustomControl` elemet.</span><span class="sxs-lookup"><span data-stu-id="6fa42-107">The following sections describe attributes, child elements, and the parent element of the `CustomControl` element.</span></span> <span data-ttu-id="6fa42-108">Több gyermekelemet kell megadnia.</span><span class="sxs-lookup"><span data-stu-id="6fa42-108">You must specify one child element.</span></span>

### <a name="attributes"></a><span data-ttu-id="6fa42-109">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="6fa42-109">Attributes</span></span>

<span data-ttu-id="6fa42-110">Nincs.</span><span class="sxs-lookup"><span data-stu-id="6fa42-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="6fa42-111">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="6fa42-111">Child Elements</span></span>

|<span data-ttu-id="6fa42-112">Elem</span><span class="sxs-lookup"><span data-stu-id="6fa42-112">Element</span></span>|<span data-ttu-id="6fa42-113">Leírás</span><span class="sxs-lookup"><span data-stu-id="6fa42-113">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="6fa42-114">A nézet (formátum) CustomControl CustomEntries elem</span><span class="sxs-lookup"><span data-stu-id="6fa42-114">CustomEntries Element for CustomControl for View (Format)</span></span>](./customentries-element-for-customcontrol-for-view-format.md)|<span data-ttu-id="6fa42-115">Szükséges eleme.</span><span class="sxs-lookup"><span data-stu-id="6fa42-115">Required element.</span></span><br /><br /> <span data-ttu-id="6fa42-116">Az egyéni vezérlő nézetében a definíciókat tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="6fa42-116">Provides the definitions of the custom control view.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="6fa42-117">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="6fa42-117">Parent Elements</span></span>

|<span data-ttu-id="6fa42-118">Elem</span><span class="sxs-lookup"><span data-stu-id="6fa42-118">Element</span></span>|<span data-ttu-id="6fa42-119">Leírás</span><span class="sxs-lookup"><span data-stu-id="6fa42-119">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="6fa42-120">Nézet elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="6fa42-120">View Element (Format)</span></span>](./view-element-format.md)|<span data-ttu-id="6fa42-121">Meghatározza egy nézetet, amely legalább egy .NET-objektumokká megjelenítésére szolgál.</span><span class="sxs-lookup"><span data-stu-id="6fa42-121">Defines a view that is used to display one or more .NET objects.</span></span>|

## <a name="remarks"></a><span data-ttu-id="6fa42-122">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="6fa42-122">Remarks</span></span>

<span data-ttu-id="6fa42-123">A legtöbb esetben csak egyetlen definíciót minden vezérlő nézet megadása kötelező, de lehetséges víc definic adja meg, ha ugyanabban a nézetben különböző .NET-objektumok megjelenítéséhez használandó.</span><span class="sxs-lookup"><span data-stu-id="6fa42-123">In most cases, only one definition is required for each control view, but it is possible to provide multiple definitions if you want to use the same view to display different .NET objects.</span></span> <span data-ttu-id="6fa42-124">Ezekben az esetekben adja meg egy külön meghatározása az egyes objektumok vagy objektumok közül.</span><span class="sxs-lookup"><span data-stu-id="6fa42-124">In those cases, you can provide a separate definition for each object or set of objects.</span></span>

## <a name="see-also"></a><span data-ttu-id="6fa42-125">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="6fa42-125">See Also</span></span>

[<span data-ttu-id="6fa42-126">A nézet (formátum) CustomControl CustomEntries elem</span><span class="sxs-lookup"><span data-stu-id="6fa42-126">CustomEntries Element for CustomControl for View (Format)</span></span>](./customentries-element-for-customcontrol-for-view-format.md)

[<span data-ttu-id="6fa42-127">Nézet elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="6fa42-127">View Element (Format)</span></span>](./view-element-format.md)

[<span data-ttu-id="6fa42-128">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="6fa42-128">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
