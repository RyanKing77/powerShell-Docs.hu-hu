---
title: CustomControl elemet a vezérlési konfiguráció (formátum) vezérlők |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: d9d92a9e-c680-46ca-962e-e82452726953
caps.latest.revision: 10
ms.openlocfilehash: 1d72ce5b18e89bd81c7f81b27f4b8c60bed99764
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56847977"
---
# <a name="customcontrol-element-for-control-for-controls-for-configuration-format"></a><span data-ttu-id="f3c1b-102">A Konfiguráció Vezérlők eleméhez tartozó Vezérlő CustomControl eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="f3c1b-102">CustomControl Element for Control for Controls for Configuration (Format)</span></span>

<span data-ttu-id="f3c1b-103">Határozza meg olyan vezérlő.</span><span class="sxs-lookup"><span data-stu-id="f3c1b-103">Defines a control.</span></span> <span data-ttu-id="f3c1b-104">Ez az elem szolgál egy közös vezérlőelem a formázási fájlban az összes nézetek által használható meghatározásakor.</span><span class="sxs-lookup"><span data-stu-id="f3c1b-104">This element is used when defining a common control that can be used by all the views in the formatting file.</span></span>

<span data-ttu-id="f3c1b-105">Konfigurációs elem (formátum) vezérlők elem Configuration (formátum) vezérlőelem elem vezérlők, a Configuration (formátum) CustomControl elem a vezérlési konfiguráció (formátum)</span><span class="sxs-lookup"><span data-stu-id="f3c1b-105">Configuration Element (Format) Controls Element of Configuration (Format) Control Element for Controls for Configuration (Format) CustomControl Element for Control for Configuration (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="f3c1b-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="f3c1b-106">Syntax</span></span>

```xml
<CustomControl>
  <CustomEntries>...</CustomEntries>
</CustomControl>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="f3c1b-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="f3c1b-107">Attributes and Elements</span></span>

<span data-ttu-id="f3c1b-108">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `CustomControl` elemet.</span><span class="sxs-lookup"><span data-stu-id="f3c1b-108">The following sections describe the attributes, child elements, and the parent element of the `CustomControl` element.</span></span> <span data-ttu-id="f3c1b-109">Ez az elem rendelkeznie kell legalább egy gyermekelemet.</span><span class="sxs-lookup"><span data-stu-id="f3c1b-109">This element must have at least one child element.</span></span> <span data-ttu-id="f3c1b-110">Nincs maximális megadható az alárendelt elemek száma korlátozva van.</span><span class="sxs-lookup"><span data-stu-id="f3c1b-110">There is no maximum limit to the number of child elements that can be specified.</span></span>

### <a name="attributes"></a><span data-ttu-id="f3c1b-111">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="f3c1b-111">Attributes</span></span>

<span data-ttu-id="f3c1b-112">Nincs.</span><span class="sxs-lookup"><span data-stu-id="f3c1b-112">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="f3c1b-113">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="f3c1b-113">Child Elements</span></span>

|<span data-ttu-id="f3c1b-114">Elem</span><span class="sxs-lookup"><span data-stu-id="f3c1b-114">Element</span></span>|<span data-ttu-id="f3c1b-115">Leírás</span><span class="sxs-lookup"><span data-stu-id="f3c1b-115">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="f3c1b-116">Konfiguráció (formátum) CustomControl CustomEntries elem.</span><span class="sxs-lookup"><span data-stu-id="f3c1b-116">CustomEntries Element for CustomControl for Configuration (Format)</span></span>](./customentries-element-for-customcontrol-for-controls-for-configuration-format.md)|<span data-ttu-id="f3c1b-117">Szükséges eleme.</span><span class="sxs-lookup"><span data-stu-id="f3c1b-117">Required element.</span></span><br /><br /> <span data-ttu-id="f3c1b-118">A vezérlőelem definícióit tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="f3c1b-118">Provides the definitions of a control.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="f3c1b-119">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="f3c1b-119">Parent Elements</span></span>

|<span data-ttu-id="f3c1b-120">Elem</span><span class="sxs-lookup"><span data-stu-id="f3c1b-120">Element</span></span>|<span data-ttu-id="f3c1b-121">Leírás</span><span class="sxs-lookup"><span data-stu-id="f3c1b-121">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="f3c1b-122">Vezérlő elemet a vezérlők konfiguráció (formátum)</span><span class="sxs-lookup"><span data-stu-id="f3c1b-122">Control Element for Controls for Configuration (Format)</span></span>](./control-element-for-controls-for-configuration-format.md)|<span data-ttu-id="f3c1b-123">Meghatározza egy közös ellenőrzés, hogy a formázási fájlja és a neve, amellyel hivatkozni a vezérlőelem összes nézet is lehet.</span><span class="sxs-lookup"><span data-stu-id="f3c1b-123">Defines a common control that can be used by all the views of the formatting file and the name that is used to reference the control.</span></span>|

## <a name="remarks"></a><span data-ttu-id="f3c1b-124">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="f3c1b-124">Remarks</span></span>

## <a name="see-also"></a><span data-ttu-id="f3c1b-125">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="f3c1b-125">See Also</span></span>

[<span data-ttu-id="f3c1b-126">Vezérlő elemet a vezérlők konfiguráció (formátum)</span><span class="sxs-lookup"><span data-stu-id="f3c1b-126">Control Element for Controls for Configuration (Format)</span></span>](./control-element-for-controls-for-configuration-format.md)

[<span data-ttu-id="f3c1b-127">Konfiguráció (formátum) CustomControl CustomEntries elem.</span><span class="sxs-lookup"><span data-stu-id="f3c1b-127">CustomEntries Element for CustomControl for Configuration (Format)</span></span>](./customentries-element-for-customcontrol-for-controls-for-configuration-format.md)

[<span data-ttu-id="f3c1b-128">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="f3c1b-128">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
