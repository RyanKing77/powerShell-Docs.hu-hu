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
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62066736"
---
# <a name="customcontrol-element-for-control-for-controls-for-configuration-format"></a><span data-ttu-id="04cd7-102">A Konfiguráció Vezérlők eleméhez tartozó Vezérlő CustomControl eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="04cd7-102">CustomControl Element for Control for Controls for Configuration (Format)</span></span>

<span data-ttu-id="04cd7-103">Határozza meg olyan vezérlő.</span><span class="sxs-lookup"><span data-stu-id="04cd7-103">Defines a control.</span></span> <span data-ttu-id="04cd7-104">Ez az elem szolgál egy közös vezérlőelem a formázási fájlban az összes nézetek által használható meghatározásakor.</span><span class="sxs-lookup"><span data-stu-id="04cd7-104">This element is used when defining a common control that can be used by all the views in the formatting file.</span></span>

<span data-ttu-id="04cd7-105">Konfigurációs elem (formátum) vezérlők elem Configuration (formátum) vezérlőelem elem vezérlők, a Configuration (formátum) CustomControl elem a vezérlési konfiguráció (formátum)</span><span class="sxs-lookup"><span data-stu-id="04cd7-105">Configuration Element (Format) Controls Element of Configuration (Format) Control Element for Controls for Configuration (Format) CustomControl Element for Control for Configuration (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="04cd7-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="04cd7-106">Syntax</span></span>

```xml
<CustomControl>
  <CustomEntries>...</CustomEntries>
</CustomControl>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="04cd7-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="04cd7-107">Attributes and Elements</span></span>

<span data-ttu-id="04cd7-108">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `CustomControl` elemet.</span><span class="sxs-lookup"><span data-stu-id="04cd7-108">The following sections describe the attributes, child elements, and the parent element of the `CustomControl` element.</span></span> <span data-ttu-id="04cd7-109">Ez az elem rendelkeznie kell legalább egy gyermekelemet.</span><span class="sxs-lookup"><span data-stu-id="04cd7-109">This element must have at least one child element.</span></span> <span data-ttu-id="04cd7-110">Nincs maximális megadható az alárendelt elemek száma korlátozva van.</span><span class="sxs-lookup"><span data-stu-id="04cd7-110">There is no maximum limit to the number of child elements that can be specified.</span></span>

### <a name="attributes"></a><span data-ttu-id="04cd7-111">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="04cd7-111">Attributes</span></span>

<span data-ttu-id="04cd7-112">Nincs.</span><span class="sxs-lookup"><span data-stu-id="04cd7-112">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="04cd7-113">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="04cd7-113">Child Elements</span></span>

|<span data-ttu-id="04cd7-114">Elem</span><span class="sxs-lookup"><span data-stu-id="04cd7-114">Element</span></span>|<span data-ttu-id="04cd7-115">Leírás</span><span class="sxs-lookup"><span data-stu-id="04cd7-115">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="04cd7-116">Konfiguráció (formátum) CustomControl CustomEntries elem.</span><span class="sxs-lookup"><span data-stu-id="04cd7-116">CustomEntries Element for CustomControl for Configuration (Format)</span></span>](./customentries-element-for-customcontrol-for-controls-for-configuration-format.md)|<span data-ttu-id="04cd7-117">Szükséges eleme.</span><span class="sxs-lookup"><span data-stu-id="04cd7-117">Required element.</span></span><br /><br /> <span data-ttu-id="04cd7-118">A vezérlőelem definícióit tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="04cd7-118">Provides the definitions of a control.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="04cd7-119">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="04cd7-119">Parent Elements</span></span>

|<span data-ttu-id="04cd7-120">Elem</span><span class="sxs-lookup"><span data-stu-id="04cd7-120">Element</span></span>|<span data-ttu-id="04cd7-121">Leírás</span><span class="sxs-lookup"><span data-stu-id="04cd7-121">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="04cd7-122">Vezérlő elemet a vezérlők konfiguráció (formátum)</span><span class="sxs-lookup"><span data-stu-id="04cd7-122">Control Element for Controls for Configuration (Format)</span></span>](./control-element-for-controls-for-configuration-format.md)|<span data-ttu-id="04cd7-123">Meghatározza egy közös ellenőrzés, hogy a formázási fájlja és a neve, amellyel hivatkozni a vezérlőelem összes nézet is lehet.</span><span class="sxs-lookup"><span data-stu-id="04cd7-123">Defines a common control that can be used by all the views of the formatting file and the name that is used to reference the control.</span></span>|

## <a name="remarks"></a><span data-ttu-id="04cd7-124">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="04cd7-124">Remarks</span></span>

## <a name="see-also"></a><span data-ttu-id="04cd7-125">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="04cd7-125">See Also</span></span>

[<span data-ttu-id="04cd7-126">Vezérlő elemet a vezérlők konfiguráció (formátum)</span><span class="sxs-lookup"><span data-stu-id="04cd7-126">Control Element for Controls for Configuration (Format)</span></span>](./control-element-for-controls-for-configuration-format.md)

[<span data-ttu-id="04cd7-127">Konfiguráció (formátum) CustomControl CustomEntries elem.</span><span class="sxs-lookup"><span data-stu-id="04cd7-127">CustomEntries Element for CustomControl for Configuration (Format)</span></span>](./customentries-element-for-customcontrol-for-controls-for-configuration-format.md)

[<span data-ttu-id="04cd7-128">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="04cd7-128">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
