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
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62066668"
---
# <a name="customcontrol-element-for-view-format"></a><span data-ttu-id="0d130-102">A Nézet CustomControl eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="0d130-102">CustomControl Element for View (Format)</span></span>

<span data-ttu-id="0d130-103">A nézet egy egyéni vezérlő formátumát határozza meg.</span><span class="sxs-lookup"><span data-stu-id="0d130-103">Defines a custom control format for the view.</span></span>

<span data-ttu-id="0d130-104">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem CustomControl elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="0d130-104">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) CustomControl Element (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="0d130-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="0d130-105">Syntax</span></span>

```xml
<CustomControl>
  <CustomEntries>...</CustomEntries>
</CustomControl>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="0d130-106">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="0d130-106">Attributes and Elements</span></span>

<span data-ttu-id="0d130-107">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `CustomControl` elemet.</span><span class="sxs-lookup"><span data-stu-id="0d130-107">The following sections describe attributes, child elements, and the parent element of the `CustomControl` element.</span></span> <span data-ttu-id="0d130-108">Több gyermekelemet kell megadnia.</span><span class="sxs-lookup"><span data-stu-id="0d130-108">You must specify one child element.</span></span>

### <a name="attributes"></a><span data-ttu-id="0d130-109">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="0d130-109">Attributes</span></span>

<span data-ttu-id="0d130-110">Nincs.</span><span class="sxs-lookup"><span data-stu-id="0d130-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="0d130-111">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="0d130-111">Child Elements</span></span>

|<span data-ttu-id="0d130-112">Elem</span><span class="sxs-lookup"><span data-stu-id="0d130-112">Element</span></span>|<span data-ttu-id="0d130-113">Leírás</span><span class="sxs-lookup"><span data-stu-id="0d130-113">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="0d130-114">A nézet (formátum) CustomControl CustomEntries elem</span><span class="sxs-lookup"><span data-stu-id="0d130-114">CustomEntries Element for CustomControl for View (Format)</span></span>](./customentries-element-for-customcontrol-for-view-format.md)|<span data-ttu-id="0d130-115">Szükséges eleme.</span><span class="sxs-lookup"><span data-stu-id="0d130-115">Required element.</span></span><br /><br /> <span data-ttu-id="0d130-116">Az egyéni vezérlő nézetében a definíciókat tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="0d130-116">Provides the definitions of the custom control view.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="0d130-117">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="0d130-117">Parent Elements</span></span>

|<span data-ttu-id="0d130-118">Elem</span><span class="sxs-lookup"><span data-stu-id="0d130-118">Element</span></span>|<span data-ttu-id="0d130-119">Leírás</span><span class="sxs-lookup"><span data-stu-id="0d130-119">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="0d130-120">Nézet elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="0d130-120">View Element (Format)</span></span>](./view-element-format.md)|<span data-ttu-id="0d130-121">Meghatározza egy nézetet, amely legalább egy .NET-objektumokká megjelenítésére szolgál.</span><span class="sxs-lookup"><span data-stu-id="0d130-121">Defines a view that is used to display one or more .NET objects.</span></span>|

## <a name="remarks"></a><span data-ttu-id="0d130-122">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="0d130-122">Remarks</span></span>

<span data-ttu-id="0d130-123">A legtöbb esetben csak egyetlen definíciót minden vezérlő nézet megadása kötelező, de lehetséges víc definic adja meg, ha ugyanabban a nézetben különböző .NET-objektumok megjelenítéséhez használandó.</span><span class="sxs-lookup"><span data-stu-id="0d130-123">In most cases, only one definition is required for each control view, but it is possible to provide multiple definitions if you want to use the same view to display different .NET objects.</span></span> <span data-ttu-id="0d130-124">Ezekben az esetekben adja meg egy külön meghatározása az egyes objektumok vagy objektumok közül.</span><span class="sxs-lookup"><span data-stu-id="0d130-124">In those cases, you can provide a separate definition for each object or set of objects.</span></span>

## <a name="see-also"></a><span data-ttu-id="0d130-125">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="0d130-125">See Also</span></span>

[<span data-ttu-id="0d130-126">A nézet (formátum) CustomControl CustomEntries elem</span><span class="sxs-lookup"><span data-stu-id="0d130-126">CustomEntries Element for CustomControl for View (Format)</span></span>](./customentries-element-for-customcontrol-for-view-format.md)

[<span data-ttu-id="0d130-127">Nézet elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="0d130-127">View Element (Format)</span></span>](./view-element-format.md)

[<span data-ttu-id="0d130-128">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="0d130-128">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
