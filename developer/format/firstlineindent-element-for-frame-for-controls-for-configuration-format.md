---
title: Keret (formátum) konfiguráció vezérlők FirstLineIndent elem |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 2f489720-11f6-4019-940e-07f423d4278d
caps.latest.revision: 6
ms.openlocfilehash: c5b2d971fe1590116f96b024ae8769334768acf2
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62065988"
---
# <a name="firstlineindent-element-for-frame-for-controls-for-configuration-format"></a><span data-ttu-id="bf619-102">A Konfiguráció Vezérlők eleméhez tartozó Keret FirstLineIndent eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="bf619-102">FirstLineIndent Element for Frame for Controls for Configuration (Format)</span></span>

<span data-ttu-id="bf619-103">Megadja az adatok első sorának jobb úgy, hogy hány karakter.</span><span class="sxs-lookup"><span data-stu-id="bf619-103">Specifies how many characters the first line of data is shifted to the right.</span></span> <span data-ttu-id="bf619-104">Ez az elem szolgál egy közös vezérlőelem a formázási fájlban az összes nézetek által használható meghatározásakor.</span><span class="sxs-lookup"><span data-stu-id="bf619-104">This element is used when defining a common control that can be used by all the views in the formatting file.</span></span>

<span data-ttu-id="bf619-105">Konfigurációs elem (formátum) vezérlők elem Configuration (formátum) vezérlőelem elem vezérlők, a vezérlő konfigurációs (formátum) CustomEntries elemhez tartozó CustomControl Configuration (a Configuration (formátum) CustomControl elem Formátum) CustomEntry elemet a vezérlők, a Configuration (formátum) CustomItem elemet a vezérlők, a konfiguráció keret elemet a vezérlők, a Configuration (formátum) FirstLineIndent elem keret CustomItem CustomEntry CustomControl vezérlők, a Configuration (formátum)</span><span class="sxs-lookup"><span data-stu-id="bf619-105">Configuration Element (Format) Controls Element of Configuration (Format) Control Element for Controls for Configuration (Format) CustomControl Element for Control for Configuration (Format) CustomEntries Element for CustomControl for Configuration (Format) CustomEntry Element for CustomControl for Controls for Configuration (Format) CustomItem Element for CustomEntry for Controls for Configuration Frame Element for CustomItem for Controls for Configuration (Format) FirstLineIndent Element for Frame for Controls for Configuration (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="bf619-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="bf619-106">Syntax</span></span>

```xml
<FirstLineIndent>NumberOfCharactersToShift</FirstLineIndent>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="bf619-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="bf619-107">Attributes and Elements</span></span>

<span data-ttu-id="bf619-108">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és szülőelemét a `FirstLineIndent` elemet.</span><span class="sxs-lookup"><span data-stu-id="bf619-108">The following sections describe attributes, child elements, and parent element of the `FirstLineIndent` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="bf619-109">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="bf619-109">Attributes</span></span>

<span data-ttu-id="bf619-110">Nincs.</span><span class="sxs-lookup"><span data-stu-id="bf619-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="bf619-111">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="bf619-111">Child Elements</span></span>

<span data-ttu-id="bf619-112">Nincs.</span><span class="sxs-lookup"><span data-stu-id="bf619-112">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="bf619-113">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="bf619-113">Parent Elements</span></span>

|<span data-ttu-id="bf619-114">Elem</span><span class="sxs-lookup"><span data-stu-id="bf619-114">Element</span></span>|<span data-ttu-id="bf619-115">Leírás</span><span class="sxs-lookup"><span data-stu-id="bf619-115">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="bf619-116">Keret eleme CustomItem vezérlők konfiguráció (formátum)</span><span class="sxs-lookup"><span data-stu-id="bf619-116">Frame Element for CustomItem for Controls for Configuration (Format)</span></span>](./frame-element-for-customitem-for-controls-for-configuration-format.md)|<span data-ttu-id="bf619-117">Határozza meg, hogyan egy jelennek meg, például az adatok pótlása jobbra vagy balra.</span><span class="sxs-lookup"><span data-stu-id="bf619-117">Defines how the data is displayed, such as shifting the data to the left or right.</span></span>|

## <a name="text-value"></a><span data-ttu-id="bf619-118">A szöveges érték</span><span class="sxs-lookup"><span data-stu-id="bf619-118">Text Value</span></span>

<span data-ttu-id="bf619-119">Adja meg, hogy az adatok első sora shift kívánt karakterek száma.</span><span class="sxs-lookup"><span data-stu-id="bf619-119">Specify the number of characters that you want to shift the first line of the data.</span></span>

## <a name="remarks"></a><span data-ttu-id="bf619-120">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="bf619-120">Remarks</span></span>

<span data-ttu-id="bf619-121">Ha ez az elem meg van adva, nem adható meg a [FirstLineHanging](./firstlinehanging-element-for-frame-for-controls-for-configuration-format.md) elemet.</span><span class="sxs-lookup"><span data-stu-id="bf619-121">If this element is specified, you cannot specify the [FirstLineHanging](./firstlinehanging-element-for-frame-for-controls-for-configuration-format.md) element.</span></span>

## <a name="see-also"></a><span data-ttu-id="bf619-122">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="bf619-122">See Also</span></span>

[<span data-ttu-id="bf619-123">Keret (formátum) konfiguráció vezérlők FirstLineHanging elem.</span><span class="sxs-lookup"><span data-stu-id="bf619-123">FirstLineHanging Element for Frame for Controls for Configuration (Format)</span></span>](./firstlinehanging-element-for-frame-for-controls-for-configuration-format.md)

[<span data-ttu-id="bf619-124">Keret eleme CustomItem vezérlők konfiguráció (formátum)</span><span class="sxs-lookup"><span data-stu-id="bf619-124">Frame Element for CustomItem for Controls for Configuration (Format)</span></span>](./frame-element-for-customitem-for-controls-for-configuration-format.md)

[<span data-ttu-id="bf619-125">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="bf619-125">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
