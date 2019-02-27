---
title: SelectionSetName elemet a vezérlők (formátum) konfiguráció EntrySelectedBy |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 42143d1e-7cda-4c4a-b568-fa1951bb9417
caps.latest.revision: 6
ms.openlocfilehash: 9060ee54d6f88c7f910b16cf5c9b87f37844b736
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56850245"
---
# <a name="selectionsetname-element-for-entryselectedby-for-controls-for-configuration-format"></a><span data-ttu-id="34b20-102">A Konfiguráció Vezérlők eleméhez tartozó EntrySelectedBy SelectionSetName eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="34b20-102">SelectionSetName Element for EntrySelectedBy for Controls for Configuration (Format)</span></span>

<span data-ttu-id="34b20-103">Ez a definíció, a vezérlő használó .NET-típusok egy halmazát határozza meg.</span><span class="sxs-lookup"><span data-stu-id="34b20-103">Specifies a set of .NET types that use this definition of the control.</span></span> <span data-ttu-id="34b20-104">Ez az elem szolgál egy közös vezérlőelem a formázási fájlban az összes nézetek által használható meghatározásakor.</span><span class="sxs-lookup"><span data-stu-id="34b20-104">This element is used when defining a common control that can be used by all the views in the formatting file.</span></span>

<span data-ttu-id="34b20-105">Konfigurációs elem (formátum) vezérlők elem Configuration (formátum) vezérlőelem elem vezérlők, a vezérlő konfigurációs (formátum) CustomEntries elemhez tartozó CustomControl Configuration (a Configuration (formátum) CustomControl elem Formátum) CustomEntry elemet a vezérlők, a Configuration (formátum) EntrySelectedBy elem CustomEntry vezérlők EntrySelectedBy vezérlők (formátum) konfiguráció esetén a Configuration (formátum) SelectionSetName elemhez tartozó CustomControl</span><span class="sxs-lookup"><span data-stu-id="34b20-105">Configuration Element (Format) Controls Element of Configuration (Format) Control Element for Controls for Configuration (Format) CustomControl Element for Control for Configuration (Format) CustomEntries Element for CustomControl for Configuration (Format) CustomEntry Element for CustomControl for Controls for Configuration (Format) EntrySelectedBy Element for CustomEntry for Controls for Configuration (Format) SelectionSetName Element for EntrySelectedBy for Controls for Configuration (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="34b20-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="34b20-106">Syntax</span></span>

```xml
<SelectionSetName>NameofSelectionSet</SelectionSetName>

```

## <a name="attributes-and-elements"></a><span data-ttu-id="34b20-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="34b20-107">Attributes and Elements</span></span>

<span data-ttu-id="34b20-108">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `SelectionSetName` elemet.</span><span class="sxs-lookup"><span data-stu-id="34b20-108">The following sections describe attributes, child elements, and the parent element of the `SelectionSetName` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="34b20-109">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="34b20-109">Attributes</span></span>

<span data-ttu-id="34b20-110">Egyik sem</span><span class="sxs-lookup"><span data-stu-id="34b20-110">None</span></span>

### <a name="child-elements"></a><span data-ttu-id="34b20-111">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="34b20-111">Child Elements</span></span>

<span data-ttu-id="34b20-112">Nincs.</span><span class="sxs-lookup"><span data-stu-id="34b20-112">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="34b20-113">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="34b20-113">Parent Elements</span></span>

|<span data-ttu-id="34b20-114">Elem</span><span class="sxs-lookup"><span data-stu-id="34b20-114">Element</span></span>|<span data-ttu-id="34b20-115">Leírás</span><span class="sxs-lookup"><span data-stu-id="34b20-115">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="34b20-116">Konfiguráció (formátum) vezérlők CustomEntry EntrySelectedBy elem.</span><span class="sxs-lookup"><span data-stu-id="34b20-116">EntrySelectedBy Element for CustomEntry for Controls for Configuration (Format)</span></span>](./entryselectedby-element-for-customentry-for-controls-for-configuration-format.md)|<span data-ttu-id="34b20-117">A .NET-típusokat, amelyek a vezérlő definition vagy a feltétellel, hogy léteznie kell a definíció használandó határozza meg.</span><span class="sxs-lookup"><span data-stu-id="34b20-117">Defines the .NET types that use this control definition or the condition that must exist for this definition to be used.</span></span>|

## <a name="text-value"></a><span data-ttu-id="34b20-118">Szöveges érték</span><span class="sxs-lookup"><span data-stu-id="34b20-118">Text Value</span></span>

<span data-ttu-id="34b20-119">Adja meg a kijelölt csoport nevét.</span><span class="sxs-lookup"><span data-stu-id="34b20-119">Specify the name of the selection set.</span></span>

## <a name="remarks"></a><span data-ttu-id="34b20-120">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="34b20-120">Remarks</span></span>

<span data-ttu-id="34b20-121">Minden vezérlő definíció rendelkeznie kell legalább egy típusnév, kijelölés set vagy meghatározott kiválasztási feltételnek.</span><span class="sxs-lookup"><span data-stu-id="34b20-121">Each control definition must have at least one type name, selection set, or selection condition defined.</span></span>

<span data-ttu-id="34b20-122">Kijelölt csoportok általában akkor használják, ha meg szeretné több nézetében lévő meghatározott felhasználói csoporttal használt objektumok.</span><span class="sxs-lookup"><span data-stu-id="34b20-122">Selection sets are typically used when you want to define a group of objects that are used in multiple views.</span></span> <span data-ttu-id="34b20-123">Kijelölt csoportok meghatározása kapcsolatos további információkért lásd: [meghatározása beállítja a kijelölés](./defining-selection-sets.md).</span><span class="sxs-lookup"><span data-stu-id="34b20-123">For more information about defining selection sets, see [Defining Selection Sets](./defining-selection-sets.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="34b20-124">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="34b20-124">See Also</span></span>

[<span data-ttu-id="34b20-125">Konfiguráció (formátum) vezérlők CustomEntry EntrySelectedBy elem.</span><span class="sxs-lookup"><span data-stu-id="34b20-125">EntrySelectedBy Element for CustomEntry for Controls for Configuration (Format)</span></span>](./entryselectedby-element-for-customentry-for-controls-for-configuration-format.md)

[<span data-ttu-id="34b20-126">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="34b20-126">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
