---
title: GroupBy (formátum)-keret FirstLineHanging elem |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 1cdcf66e-96a5-47b5-9269-b4330bde29f2
caps.latest.revision: 6
ms.openlocfilehash: 08db1f2d89c3fe6c1e9a5a522de3071425042c3f
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56846542"
---
# <a name="firstlinehanging-element-for-frame-for-groupby-format"></a><span data-ttu-id="25f20-102">A GroupBy elemhez tartozó Keret FirstLineHanging eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="25f20-102">FirstLineHanging Element for Frame for GroupBy (Format)</span></span>

<span data-ttu-id="25f20-103">Megadja a bal oldali adatok első sora úgy, hogy hány karakter.</span><span class="sxs-lookup"><span data-stu-id="25f20-103">Specifies how many characters the first line of data is shifted to the left.</span></span> <span data-ttu-id="25f20-104">Ez az elem szolgál, hogyan jelenjen meg az objektumok egy új csoportot meghatározásakor.</span><span class="sxs-lookup"><span data-stu-id="25f20-104">This element is used when defining how a new group of objects is displayed.</span></span>

<span data-ttu-id="25f20-105">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem GroupBy elem megtekintése (formátum) CustomControl elem a GroupBy (formátum) CustomEntry elemhez tartozó CustomControl GroupBy (formátum) CustomEntries elemhez GroupBy (formátum) CustomItem elem CustomEntry CustomItem GroupBy (formátum)-keret GroupBy (formátum) FirstLineHanging elemhez tartozó GroupBy (formátum) keret elemhez tartozó CustomControl</span><span class="sxs-lookup"><span data-stu-id="25f20-105">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) GroupBy Element for View (Format) CustomControl Element for GroupBy (Format) CustomEntries Element for CustomControl for GroupBy (Format) CustomEntry Element for CustomControl for GroupBy (Format) CustomItem Element for CustomEntry for GroupBy (Format) Frame Element for CustomItem for GroupBy (Format) FirstLineHanging Element for Frame for GroupBy (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="25f20-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="25f20-106">Syntax</span></span>

```xml
<FirstLineHanging>NumberOfCharactersToShift</FirstLineHanging>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="25f20-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="25f20-107">Attributes and Elements</span></span>

<span data-ttu-id="25f20-108">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és szülőelemét a `FirstLineHanging` elemet.</span><span class="sxs-lookup"><span data-stu-id="25f20-108">The following sections describe attributes, child elements, and parent element of the `FirstLineHanging` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="25f20-109">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="25f20-109">Attributes</span></span>

<span data-ttu-id="25f20-110">Nincs.</span><span class="sxs-lookup"><span data-stu-id="25f20-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="25f20-111">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="25f20-111">Child Elements</span></span>

<span data-ttu-id="25f20-112">Nincs.</span><span class="sxs-lookup"><span data-stu-id="25f20-112">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="25f20-113">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="25f20-113">Parent Elements</span></span>

|<span data-ttu-id="25f20-114">Elem</span><span class="sxs-lookup"><span data-stu-id="25f20-114">Element</span></span>|<span data-ttu-id="25f20-115">Leírás</span><span class="sxs-lookup"><span data-stu-id="25f20-115">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="25f20-116">Keret eleme CustomItem a GroupBy (formátum)</span><span class="sxs-lookup"><span data-stu-id="25f20-116">Frame Element for CustomItem for GroupBy (Format)</span></span>](./frame-element-for-customitem-for-groupby-format.md)|<span data-ttu-id="25f20-117">Határozza meg, hogyan egy jelennek meg, például az adatok pótlása jobbra vagy balra.</span><span class="sxs-lookup"><span data-stu-id="25f20-117">Defines how the data is displayed, such as shifting the data to the left or right.</span></span>|

## <a name="text-value"></a><span data-ttu-id="25f20-118">Szöveges érték</span><span class="sxs-lookup"><span data-stu-id="25f20-118">Text Value</span></span>

<span data-ttu-id="25f20-119">Adja meg, hogy az adatok első sora shift kívánt karakterek száma.</span><span class="sxs-lookup"><span data-stu-id="25f20-119">Specify the number of characters that you want to shift the first line of the data.</span></span>

## <a name="remarks"></a><span data-ttu-id="25f20-120">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="25f20-120">Remarks</span></span>

<span data-ttu-id="25f20-121">Ha ez az elem meg van adva, nem adható meg a [FirstLineIndent](./firstlineindent-element-for-frame-for-groupby-format.md) elemet.</span><span class="sxs-lookup"><span data-stu-id="25f20-121">If this element is specified, you cannot specify the [FirstLineIndent](./firstlineindent-element-for-frame-for-groupby-format.md) element.</span></span>

## <a name="see-also"></a><span data-ttu-id="25f20-122">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="25f20-122">See Also</span></span>

[<span data-ttu-id="25f20-123">GroupBy (formátum)-keret FirstLineIndent elem</span><span class="sxs-lookup"><span data-stu-id="25f20-123">FirstLineIndent Element for Frame for GroupBy (Format)</span></span>](./firstlineindent-element-for-frame-for-groupby-format.md)

[<span data-ttu-id="25f20-124">Keret eleme CustomItem a GroupBy (formátum)</span><span class="sxs-lookup"><span data-stu-id="25f20-124">Frame Element for CustomItem for GroupBy (Format)</span></span>](./frame-element-for-customitem-for-groupby-format.md)

[<span data-ttu-id="25f20-125">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="25f20-125">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
