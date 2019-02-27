---
title: Konfigurációs elem (formátum) |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: d46df0cb-50b7-4b81-82ba-37186a7b7a7f
caps.latest.revision: 28
ms.openlocfilehash: 296c63d0c774a0bf56e90dbaa32f2c221d4c3dbd
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56847039"
---
# <a name="configuration-element-format"></a><span data-ttu-id="34890-102">Konfigurációs elem (Formátum)</span><span class="sxs-lookup"><span data-stu-id="34890-102">Configuration Element (Format)</span></span>

<span data-ttu-id="34890-103">A legfelső szintű elem egy formázási fájl jelöli.</span><span class="sxs-lookup"><span data-stu-id="34890-103">Represents the top-level element of a formatting file.</span></span>

<span data-ttu-id="34890-104">Konfigurációs elem</span><span class="sxs-lookup"><span data-stu-id="34890-104">Configuration Element</span></span>

## <a name="syntax"></a><span data-ttu-id="34890-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="34890-105">Syntax</span></span>

```xml
<Configuration>
  <DefaultSettings>...</DefaultSettings>
  <SelectionSets>...</SelectionSets>
  <Controls>...</Controls>
  <ViewDefinitions>...</ViewDefinitions>
</Configuration>

```

## <a name="attributes-and-elements"></a><span data-ttu-id="34890-106">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="34890-106">Attributes and Elements</span></span>

<span data-ttu-id="34890-107">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `Configuration` elemet.</span><span class="sxs-lookup"><span data-stu-id="34890-107">The following sections describe the attributes, child elements, and the parent element of the `Configuration` element.</span></span> <span data-ttu-id="34890-108">Ez az elemnek kell lennie a gyökérelem formázási fájl esetében, és ezt az elemet tartalmaznia kell legalább egy gyermekelemet.</span><span class="sxs-lookup"><span data-stu-id="34890-108">This element must be the root element for each formatting file, and this element must contain at least one child element.</span></span>

### <a name="attributes"></a><span data-ttu-id="34890-109">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="34890-109">Attributes</span></span>

<span data-ttu-id="34890-110">Nincs.</span><span class="sxs-lookup"><span data-stu-id="34890-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="34890-111">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="34890-111">Child Elements</span></span>

|<span data-ttu-id="34890-112">Elem</span><span class="sxs-lookup"><span data-stu-id="34890-112">Element</span></span>|<span data-ttu-id="34890-113">Leírás</span><span class="sxs-lookup"><span data-stu-id="34890-113">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="34890-114">Vezérlők elemet a konfigurációs (formátum)</span><span class="sxs-lookup"><span data-stu-id="34890-114">Controls Element for Configuration (Format)</span></span>](./controls-element-for-configuration-format.md)|<span data-ttu-id="34890-115">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="34890-115">Optional element.</span></span><br /><br /> <span data-ttu-id="34890-116">A Gyakori vezérlők, amelyek segítségével az összes nézetben megtekinthetők a formázási fájl határozza meg.</span><span class="sxs-lookup"><span data-stu-id="34890-116">Defines the common controls that can be used by all views of the formatting file.</span></span>|
|[<span data-ttu-id="34890-117">DefaultSettings elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="34890-117">DefaultSettings Element (Format)</span></span>](./defaultsettings-element-format.md)|<span data-ttu-id="34890-118">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="34890-118">Optional element.</span></span><br /><br /> <span data-ttu-id="34890-119">Határozza meg a formázási fájl összes nézet vonatkozó általános beállításokat.</span><span class="sxs-lookup"><span data-stu-id="34890-119">Defines common settings that apply to all the views of the formatting file.</span></span>|
|[<span data-ttu-id="34890-120">SelectionSets elem formátuma</span><span class="sxs-lookup"><span data-stu-id="34890-120">SelectionSets Element Format</span></span>](./selectionsets-element-format.md)|<span data-ttu-id="34890-121">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="34890-121">Optional element.</span></span><br /><br /> <span data-ttu-id="34890-122">Határozza meg a gyakori eljárások egyikét a formázási fájl összes nézetek által használható .NET-objektumokat.</span><span class="sxs-lookup"><span data-stu-id="34890-122">Defines the common sets of .NET objects that can be used by all views of the formatting file.</span></span>|
|[<span data-ttu-id="34890-123">ViewDefinitions elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="34890-123">ViewDefinitions Element (Format)</span></span>](./viewdefinitions-element-format.md)|<span data-ttu-id="34890-124">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="34890-124">Optional element.</span></span><br /><br /> <span data-ttu-id="34890-125">Határozza meg az objektumokat megjelenítő nézetek.</span><span class="sxs-lookup"><span data-stu-id="34890-125">Defines the views used to display objects.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="34890-126">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="34890-126">Parent Elements</span></span>

<span data-ttu-id="34890-127">Nincs.</span><span class="sxs-lookup"><span data-stu-id="34890-127">None.</span></span>

## <a name="remarks"></a><span data-ttu-id="34890-128">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="34890-128">Remarks</span></span>

<span data-ttu-id="34890-129">Formázási fájlokat adja meg, hogyan jelennek meg objektumok.</span><span class="sxs-lookup"><span data-stu-id="34890-129">Formatting files define how objects are displayed.</span></span> <span data-ttu-id="34890-130">A legtöbb esetben a legfelső szintű elem tartalmaz egy [ViewDefinitions](./viewdefinitions-element-format.md) elem, amely meghatározza a táblázat, lista és a formázási fájl széles nézetek.</span><span class="sxs-lookup"><span data-stu-id="34890-130">In most cases, this root element contains a [ViewDefinitions](./viewdefinitions-element-format.md) element that defines the table, list, and wide views of the formatting file.</span></span> <span data-ttu-id="34890-131">A nézetdefiníciókból mellett a formázási fájl határozhatja meg közös kijelölt csoportok, a beállításokat és a vezérlőket, amellyel adott nézeteket létrehozták.</span><span class="sxs-lookup"><span data-stu-id="34890-131">In addition to the view definitions, the formatting file can define common selection sets, settings, and controls that those views can use.</span></span>

## <a name="see-also"></a><span data-ttu-id="34890-132">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="34890-132">See Also</span></span>

[<span data-ttu-id="34890-133">Vezérlők elemet a konfigurációs (formátum)</span><span class="sxs-lookup"><span data-stu-id="34890-133">Controls Element for Configuration (Format)</span></span>](./controls-element-for-configuration-format.md)

[<span data-ttu-id="34890-134">DefaultSettings elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="34890-134">DefaultSettings Element (Format)</span></span>](./defaultsettings-element-format.md)

[<span data-ttu-id="34890-135">SelectionSets elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="34890-135">SelectionSets Element (Format)</span></span>](./selectionsets-element-format.md)

[<span data-ttu-id="34890-136">ViewDefinitions elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="34890-136">ViewDefinitions Element (Format)</span></span>](./viewdefinitions-element-format.md)

[<span data-ttu-id="34890-137">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="34890-137">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
