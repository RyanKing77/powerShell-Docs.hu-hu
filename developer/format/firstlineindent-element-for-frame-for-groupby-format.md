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
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62065852"
---
# <a name="firstlineindent-element-for-frame-for-groupby-format"></a><span data-ttu-id="63e81-102">A GroupBy elemhez tartozó Keret FirstLineIndent eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="63e81-102">FirstLineIndent Element for Frame for GroupBy (Format)</span></span>

<span data-ttu-id="63e81-103">Megadja az adatok első sorának jobb úgy, hogy hány karakter.</span><span class="sxs-lookup"><span data-stu-id="63e81-103">Specifies how many characters the first line of data is shifted to the right.</span></span> <span data-ttu-id="63e81-104">Ez az elem szolgál, hogyan jelenjen meg az objektumok egy új csoportot meghatározásakor.</span><span class="sxs-lookup"><span data-stu-id="63e81-104">This element is used when defining how a new group of objects is displayed.</span></span>

<span data-ttu-id="63e81-105">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem GroupBy elem megtekintése (formátum) CustomControl elem a GroupBy (formátum) CustomEntry elemhez tartozó CustomControl GroupBy (formátum) CustomEntries elemhez GroupBy (formátum) CustomItem elem CustomEntry CustomItem GroupBy (formátum)-keret GroupBy (formátum) FirstLineIndent elemhez tartozó GroupBy (formátum) keret elemhez tartozó CustomControl</span><span class="sxs-lookup"><span data-stu-id="63e81-105">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) GroupBy Element for View (Format) CustomControl Element for GroupBy (Format) CustomEntries Element for CustomControl for GroupBy (Format) CustomEntry Element for CustomControl for GroupBy (Format) CustomItem Element for CustomEntry for GroupBy (Format) Frame Element for CustomItem for GroupBy (Format) FirstLineIndent Element for Frame for GroupBy (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="63e81-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="63e81-106">Syntax</span></span>

```xml
<FirstLineIndent>NumberOfCharactersToShift</FirstLineIndent>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="63e81-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="63e81-107">Attributes and Elements</span></span>

<span data-ttu-id="63e81-108">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és szülőelemét a `FirstLineIndent` elemet.</span><span class="sxs-lookup"><span data-stu-id="63e81-108">The following sections describe attributes, child elements, and parent element of the `FirstLineIndent` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="63e81-109">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="63e81-109">Attributes</span></span>

<span data-ttu-id="63e81-110">Nincs.</span><span class="sxs-lookup"><span data-stu-id="63e81-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="63e81-111">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="63e81-111">Child Elements</span></span>

<span data-ttu-id="63e81-112">Nincs.</span><span class="sxs-lookup"><span data-stu-id="63e81-112">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="63e81-113">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="63e81-113">Parent Elements</span></span>

|<span data-ttu-id="63e81-114">Elem</span><span class="sxs-lookup"><span data-stu-id="63e81-114">Element</span></span>|<span data-ttu-id="63e81-115">Leírás</span><span class="sxs-lookup"><span data-stu-id="63e81-115">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="63e81-116">Keret eleme CustomItem a GroupBy (formátum)</span><span class="sxs-lookup"><span data-stu-id="63e81-116">Frame Element for CustomItem for GroupBy (Format)</span></span>](./frame-element-for-customitem-for-groupby-format.md)|<span data-ttu-id="63e81-117">Határozza meg, hogyan egy jelennek meg, például az adatok pótlása jobbra vagy balra.</span><span class="sxs-lookup"><span data-stu-id="63e81-117">Defines how the data is displayed, such as shifting the data to the left or right.</span></span>|

## <a name="text-value"></a><span data-ttu-id="63e81-118">A szöveges érték</span><span class="sxs-lookup"><span data-stu-id="63e81-118">Text Value</span></span>

<span data-ttu-id="63e81-119">Adja meg, hogy az adatok első sora shift kívánt karakterek száma.</span><span class="sxs-lookup"><span data-stu-id="63e81-119">Specify the number of characters that you want to shift the first line of the data.</span></span>

## <a name="remarks"></a><span data-ttu-id="63e81-120">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="63e81-120">Remarks</span></span>

<span data-ttu-id="63e81-121">Ha ez az elem meg van adva, nem adható meg a [FirstLineHanging](./firstlinehanging-element-for-frame-for-groupby-format.md) elemet.</span><span class="sxs-lookup"><span data-stu-id="63e81-121">If this element is specified, you cannot specify the [FirstLineHanging](./firstlinehanging-element-for-frame-for-groupby-format.md) element.</span></span>

## <a name="see-also"></a><span data-ttu-id="63e81-122">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="63e81-122">See Also</span></span>

[<span data-ttu-id="63e81-123">GroupBy (formátum)-keret FirstLineHanging elem</span><span class="sxs-lookup"><span data-stu-id="63e81-123">FirstLineHanging Element for Frame for GroupBy (Format)</span></span>](./firstlinehanging-element-for-frame-for-groupby-format.md)

[<span data-ttu-id="63e81-124">Keret eleme CustomItem a GroupBy (formátum)</span><span class="sxs-lookup"><span data-stu-id="63e81-124">Frame Element for CustomItem for GroupBy (Format)</span></span>](./frame-element-for-customitem-for-groupby-format.md)

[<span data-ttu-id="63e81-125">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="63e81-125">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
