---
title: GroupBy (formátum)-keret FirstLineIndent elem |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 33be3b9e-53c8-433f-8c11-c65b0d46744c
caps.latest.revision: 6
ms.openlocfilehash: 9ba6fc1b9924a4b0d5b56ee15290a2293217403c
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56848600"
---
# <a name="firstlineindent-element-for-frame-for-groupby-format"></a><span data-ttu-id="33942-102">A GroupBy elemhez tartozó Keret FirstLineIndent eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="33942-102">FirstLineIndent Element for Frame for GroupBy (Format)</span></span>

<span data-ttu-id="33942-103">Megadja az adatok első sorának jobb úgy, hogy hány karakter.</span><span class="sxs-lookup"><span data-stu-id="33942-103">Specifies how many characters the first line of data is shifted to the right.</span></span> <span data-ttu-id="33942-104">Ez az elem szolgál, hogyan jelenjen meg az objektumok egy új csoportot meghatározásakor.</span><span class="sxs-lookup"><span data-stu-id="33942-104">This element is used when defining how a new group of objects is displayed.</span></span>

<span data-ttu-id="33942-105">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem GroupBy elem megtekintése (formátum) CustomControl elem a GroupBy (formátum) CustomEntry elemhez tartozó CustomControl GroupBy (formátum) CustomEntries elemhez GroupBy (formátum) CustomItem elem CustomEntry CustomItem GroupBy (formátum)-keret GroupBy (formátum) FirstLineIndent elemhez tartozó GroupBy (formátum) keret elemhez tartozó CustomControl</span><span class="sxs-lookup"><span data-stu-id="33942-105">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) GroupBy Element for View (Format) CustomControl Element for GroupBy (Format) CustomEntries Element for CustomControl for GroupBy (Format) CustomEntry Element for CustomControl for GroupBy (Format) CustomItem Element for CustomEntry for GroupBy (Format) Frame Element for CustomItem for GroupBy (Format) FirstLineIndent Element for Frame for GroupBy (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="33942-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="33942-106">Syntax</span></span>

```xml
<FirstLineIndent>NumberOfCharactersToShift</FirstLineIndent>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="33942-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="33942-107">Attributes and Elements</span></span>

<span data-ttu-id="33942-108">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és szülőelemét a `FirstLineIndent` elemet.</span><span class="sxs-lookup"><span data-stu-id="33942-108">The following sections describe attributes, child elements, and parent element of the `FirstLineIndent` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="33942-109">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="33942-109">Attributes</span></span>

<span data-ttu-id="33942-110">Nincs.</span><span class="sxs-lookup"><span data-stu-id="33942-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="33942-111">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="33942-111">Child Elements</span></span>

<span data-ttu-id="33942-112">Nincs.</span><span class="sxs-lookup"><span data-stu-id="33942-112">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="33942-113">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="33942-113">Parent Elements</span></span>

|<span data-ttu-id="33942-114">Elem</span><span class="sxs-lookup"><span data-stu-id="33942-114">Element</span></span>|<span data-ttu-id="33942-115">Leírás</span><span class="sxs-lookup"><span data-stu-id="33942-115">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="33942-116">Keret eleme CustomItem a GroupBy (formátum)</span><span class="sxs-lookup"><span data-stu-id="33942-116">Frame Element for CustomItem for GroupBy (Format)</span></span>](./frame-element-for-customitem-for-groupby-format.md)|<span data-ttu-id="33942-117">Határozza meg, hogyan egy jelennek meg, például az adatok pótlása jobbra vagy balra.</span><span class="sxs-lookup"><span data-stu-id="33942-117">Defines how the data is displayed, such as shifting the data to the left or right.</span></span>|

## <a name="text-value"></a><span data-ttu-id="33942-118">Szöveges érték</span><span class="sxs-lookup"><span data-stu-id="33942-118">Text Value</span></span>

<span data-ttu-id="33942-119">Adja meg, hogy az adatok első sora shift kívánt karakterek száma.</span><span class="sxs-lookup"><span data-stu-id="33942-119">Specify the number of characters that you want to shift the first line of the data.</span></span>

## <a name="remarks"></a><span data-ttu-id="33942-120">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="33942-120">Remarks</span></span>

<span data-ttu-id="33942-121">Ha ez az elem meg van adva, nem adható meg a [FirstLineHanging](./firstlinehanging-element-for-frame-for-groupby-format.md) elemet.</span><span class="sxs-lookup"><span data-stu-id="33942-121">If this element is specified, you cannot specify the [FirstLineHanging](./firstlinehanging-element-for-frame-for-groupby-format.md) element.</span></span>

## <a name="see-also"></a><span data-ttu-id="33942-122">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="33942-122">See Also</span></span>

[<span data-ttu-id="33942-123">GroupBy (formátum)-keret FirstLineHanging elem</span><span class="sxs-lookup"><span data-stu-id="33942-123">FirstLineHanging Element for Frame for GroupBy (Format)</span></span>](./firstlinehanging-element-for-frame-for-groupby-format.md)

[<span data-ttu-id="33942-124">Keret eleme CustomItem a GroupBy (formátum)</span><span class="sxs-lookup"><span data-stu-id="33942-124">Frame Element for CustomItem for GroupBy (Format)</span></span>](./frame-element-for-customitem-for-groupby-format.md)

[<span data-ttu-id="33942-125">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="33942-125">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
