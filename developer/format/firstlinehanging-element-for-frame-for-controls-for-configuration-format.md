---
title: Keret (formátum) konfiguráció vezérlők FirstLineHanging elem |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 679c8bcb-b49d-4bb4-91f5-ea1af6c217e3
caps.latest.revision: 8
ms.openlocfilehash: 4553f95e48a2b1440c00b4951bea56376b00628a
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62065886"
---
# <a name="firstlinehanging-element-for-frame-for-controls-for-configuration-format"></a><span data-ttu-id="55362-102">A Konfiguráció Vezérlők eleméhez tartozó Keret FirstLineHanging eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="55362-102">FirstLineHanging Element for Frame for Controls for Configuration (Format)</span></span>

<span data-ttu-id="55362-103">Megadja a bal oldali adatok első sora úgy, hogy hány karakter.</span><span class="sxs-lookup"><span data-stu-id="55362-103">Specifies how many characters the first line of data is shifted to the left.</span></span> <span data-ttu-id="55362-104">Ez az elem szolgál egy közös vezérlőelem a formázási fájlban az összes nézetek által használható meghatározásakor.</span><span class="sxs-lookup"><span data-stu-id="55362-104">This element is used when defining a common control that can be used by all the views in the formatting file.</span></span>

<span data-ttu-id="55362-105">Konfigurációs elem (formátum) vezérlők elem Configuration (formátum) vezérlőelem elem vezérlők, a vezérlő konfigurációs (formátum) CustomEntries elemhez tartozó CustomControl Configuration (a Configuration (formátum) CustomControl elem Formátum) CustomEntry elemet a vezérlők, a Configuration (formátum) CustomItem elemet a vezérlők, a konfiguráció keret elemet a vezérlők, a Configuration (formátum) FirstLineHanging elem keret CustomItem CustomEntry CustomControl vezérlők, a Configuration (formátum)</span><span class="sxs-lookup"><span data-stu-id="55362-105">Configuration Element (Format) Controls Element of Configuration (Format) Control Element for Controls for Configuration (Format) CustomControl Element for Control for Configuration (Format) CustomEntries Element for CustomControl for Configuration (Format) CustomEntry Element for CustomControl for Controls for Configuration (Format) CustomItem Element for CustomEntry for Controls for Configuration Frame Element for CustomItem for Controls for Configuration (Format) FirstLineHanging Element for Frame for Controls for Configuration (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="55362-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="55362-106">Syntax</span></span>

```xml
<FirstLineHanging>NumberOfCharactersToShift</FirstLineHanging>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="55362-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="55362-107">Attributes and Elements</span></span>

<span data-ttu-id="55362-108">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és szülőelemét a `FirstLineHanging` elemet.</span><span class="sxs-lookup"><span data-stu-id="55362-108">The following sections describe attributes, child elements, and parent element of the `FirstLineHanging` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="55362-109">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="55362-109">Attributes</span></span>

<span data-ttu-id="55362-110">Nincs.</span><span class="sxs-lookup"><span data-stu-id="55362-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="55362-111">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="55362-111">Child Elements</span></span>

<span data-ttu-id="55362-112">Nincs.</span><span class="sxs-lookup"><span data-stu-id="55362-112">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="55362-113">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="55362-113">Parent Elements</span></span>

|<span data-ttu-id="55362-114">Elem</span><span class="sxs-lookup"><span data-stu-id="55362-114">Element</span></span>|<span data-ttu-id="55362-115">Leírás</span><span class="sxs-lookup"><span data-stu-id="55362-115">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="55362-116">Keret eleme CustomItem vezérlők konfiguráció (formátum)</span><span class="sxs-lookup"><span data-stu-id="55362-116">Frame Element for CustomItem for Controls for Configuration (Format)</span></span>](./frame-element-for-customitem-for-controls-for-configuration-format.md)|<span data-ttu-id="55362-117">Határozza meg, hogyan egy jelennek meg, például az adatok pótlása jobbra vagy balra.</span><span class="sxs-lookup"><span data-stu-id="55362-117">Defines how the data is displayed, such as shifting the data to the left or right.</span></span>|

## <a name="text-value"></a><span data-ttu-id="55362-118">A szöveges érték</span><span class="sxs-lookup"><span data-stu-id="55362-118">Text Value</span></span>

<span data-ttu-id="55362-119">Adja meg, hogy az adatok első sora shift kívánt karakterek száma.</span><span class="sxs-lookup"><span data-stu-id="55362-119">Specify the number of characters that you want to shift the first line of the data.</span></span>

## <a name="remarks"></a><span data-ttu-id="55362-120">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="55362-120">Remarks</span></span>

<span data-ttu-id="55362-121">Ha ez az elem meg van adva, nem adható meg a `FirstLineIndent` elemet.</span><span class="sxs-lookup"><span data-stu-id="55362-121">If this element is specified, you cannot specify the `FirstLineIndent` element.</span></span>

## <a name="see-also"></a><span data-ttu-id="55362-122">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="55362-122">See Also</span></span>

[<span data-ttu-id="55362-123">Keret eleme CustomItem vezérlők konfiguráció (formátum)</span><span class="sxs-lookup"><span data-stu-id="55362-123">Frame Element for CustomItem for Controls for Configuration (Format)</span></span>](./frame-element-for-customitem-for-controls-for-configuration-format.md)

[<span data-ttu-id="55362-124">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="55362-124">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
