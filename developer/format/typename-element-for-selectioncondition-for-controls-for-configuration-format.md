---
title: TypeName elemet a vezérlők (formátum) konfiguráció SelectionCondition |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 477c8711-fffc-4f92-af45-6d4f80990474
caps.latest.revision: 7
ms.openlocfilehash: 60f02f3240c5574e1b1f9027b060bd9af89a11d2
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62083943"
---
# <a name="typename-element-for-selectioncondition-for-controls-for-configuration-format"></a><span data-ttu-id="c1a42-102">A Konfiguráció Vezérlők eleméhez tartozó SelectionCondition TypeName eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="c1a42-102">TypeName Element for SelectionCondition for Controls for Configuration (Format)</span></span>

<span data-ttu-id="c1a42-103">A .NET típusát, amely elindítja a feltételt határozza meg.</span><span class="sxs-lookup"><span data-stu-id="c1a42-103">Specifies a .NET type that triggers the condition.</span></span> <span data-ttu-id="c1a42-104">Ez az elem szolgál egy közös vezérlőelem a formázási fájlban az összes nézetek által használható meghatározásakor.</span><span class="sxs-lookup"><span data-stu-id="c1a42-104">This element is used when defining a common control that can be used by all the views in the formatting file.</span></span>

<span data-ttu-id="c1a42-105">Konfigurációs elem (formátum) vezérlők elem Configuration (formátum) vezérlőelem elem vezérlők Configuration (formátum) CustomEntries elemhez tartozó CustomControl vezérlők, a vezérlő konfigurációja (formátum) CustomControl elemhez Konfiguráció (formátum) CustomEntry elemet a vezérlők, a vezérlők, a Configuration (formátum) SelectionCondition elem esetében a CustomEntry EntrySelectedBy a CustomEntry Configuration (formátum) EntrySelectedBy elemhez CustomControl Konfiguráció (formátum) TypeName eleme SelectionCondition vezérlők konfiguráció (formátum)</span><span class="sxs-lookup"><span data-stu-id="c1a42-105">Configuration Element (Format) Controls Element of Configuration (Format) Control Element for Controls for Configuration (Format) CustomControl Element for Control for Configuration (Format) CustomEntries Element for CustomControl for Controls for Configuration (Format) CustomEntry Element for CustomControl for Controls for Configuration (Format) EntrySelectedBy Element for CustomEntry for Controls for Configuration (Format) SelectionCondition Element for EntrySelectedBy for CustomEntry for Configuration (Format) TypeName Element for SelectionCondition for Controls for Configuration (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="c1a42-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="c1a42-106">Syntax</span></span>

```xml
<TypeName>Nameof.NetType</TypeName>

```

## <a name="attributes-and-elements"></a><span data-ttu-id="c1a42-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="c1a42-107">Attributes and Elements</span></span>

<span data-ttu-id="c1a42-108">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `TypeName` elemet.</span><span class="sxs-lookup"><span data-stu-id="c1a42-108">The following sections describe attributes, child elements, and the parent element of the `TypeName` Element.</span></span>

### <a name="attributes"></a><span data-ttu-id="c1a42-109">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="c1a42-109">Attributes</span></span>

<span data-ttu-id="c1a42-110">Nincs.</span><span class="sxs-lookup"><span data-stu-id="c1a42-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="c1a42-111">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="c1a42-111">Child Elements</span></span>

<span data-ttu-id="c1a42-112">Nincs.</span><span class="sxs-lookup"><span data-stu-id="c1a42-112">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="c1a42-113">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="c1a42-113">Parent Elements</span></span>

|<span data-ttu-id="c1a42-114">Elem</span><span class="sxs-lookup"><span data-stu-id="c1a42-114">Element</span></span>|<span data-ttu-id="c1a42-115">Leírás</span><span class="sxs-lookup"><span data-stu-id="c1a42-115">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="c1a42-116">A konfiguráció (formátum) CustomEntry EntrySelectedBy SelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="c1a42-116">SelectionCondition Element for EntrySelectedBy for CustomEntry for Configuration (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-controls-for-configuration-format.md)|<span data-ttu-id="c1a42-117">Határozza meg egy feltételt, amely a vezérlőelem definíciójában használt léteznie kell.</span><span class="sxs-lookup"><span data-stu-id="c1a42-117">Defines a condition that must exist for the control definition to be used.</span></span>|

## <a name="text-value"></a><span data-ttu-id="c1a42-118">A szöveges érték</span><span class="sxs-lookup"><span data-stu-id="c1a42-118">Text Value</span></span>

<span data-ttu-id="c1a42-119">Adja meg a teljes nevet, a .NET-típus, például `System.IO.DirectoryInfo`.</span><span class="sxs-lookup"><span data-stu-id="c1a42-119">Specify the fully qualified name of the .NET type, such as `System.IO.DirectoryInfo`.</span></span>

## <a name="remarks"></a><span data-ttu-id="c1a42-120">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="c1a42-120">Remarks</span></span>

## <a name="see-also"></a><span data-ttu-id="c1a42-121">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="c1a42-121">See Also</span></span>

[<span data-ttu-id="c1a42-122">A konfiguráció (formátum) CustomEntry EntrySelectedBy SelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="c1a42-122">SelectionCondition Element for EntrySelectedBy for CustomEntry for Configuration (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-controls-for-configuration-format.md)

[<span data-ttu-id="c1a42-123">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="c1a42-123">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
