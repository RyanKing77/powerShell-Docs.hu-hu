---
title: Keret (formátum) nézet vezérlők FirstLineHanging elem |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 53694f08-57f7-4185-b443-1636a0918afc
caps.latest.revision: 8
ms.openlocfilehash: 387340cd9b0aae2ad0419b187d96ab4fee183d5a
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56848712"
---
# <a name="firstlinehanging-element-for-frame-for-controls-for-view-format"></a><span data-ttu-id="5a27a-102">A Nézet Vezérlők eleméhez tartozó Keret FirstLineHanging eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="5a27a-102">FirstLineHanging Element for Frame for Controls for View (Format)</span></span>

<span data-ttu-id="5a27a-103">Megadja a bal oldali adatok első sora úgy, hogy hány karakter.</span><span class="sxs-lookup"><span data-stu-id="5a27a-103">Specifies how many characters the first line of data is shifted to the left.</span></span> <span data-ttu-id="5a27a-104">Ez az elem szolgál a nézet által használható vezérlők meghatározásakor.</span><span class="sxs-lookup"><span data-stu-id="5a27a-104">This element is used when defining controls that can be used by a view.</span></span>

<span data-ttu-id="5a27a-105">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem vezérlők elem (formátum) vezérlőelem elem vezérlők, a nézet (formátum) CustomControl elem megtekintése (formátum) CustomEntries elemet a vezérlők a vezérlő A nézet (formátum) CustomEntry elem CustomEntries vezérlők, a vezérlők, a nézet (formátum) keret elem CustomItem vezérlők megtekintése (formátum) FirstLineHanging eleméhez tartozó CustomEntry megtekintése (formátum) CustomItem elemhez tartozó CustomControl Keret vezérlők nézet (formátum)</span><span class="sxs-lookup"><span data-stu-id="5a27a-105">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) Controls Element (Format) Control Element for Controls for View (Format) CustomControl Element for Control for Controls for View (Format) CustomEntries Element for CustomControl for View (Format) CustomEntry Element for CustomEntries for Controls for View (Format) CustomItem Element for CustomEntry for Controls for View (Format) Frame Element for CustomItem for Controls for View (Format) FirstLineHanging Element of Frame of Controls of View (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="5a27a-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="5a27a-106">Syntax</span></span>

```xml
<FirstLineHanging>NumberOfCharactersToShift</FirstLineHanging>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="5a27a-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="5a27a-107">Attributes and Elements</span></span>

<span data-ttu-id="5a27a-108">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és szülőelemét a `FirstLineHanging` elemet.</span><span class="sxs-lookup"><span data-stu-id="5a27a-108">The following sections describe attributes, child elements, and parent element of the `FirstLineHanging` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="5a27a-109">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="5a27a-109">Attributes</span></span>

<span data-ttu-id="5a27a-110">Nincs.</span><span class="sxs-lookup"><span data-stu-id="5a27a-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="5a27a-111">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="5a27a-111">Child Elements</span></span>

<span data-ttu-id="5a27a-112">Nincs.</span><span class="sxs-lookup"><span data-stu-id="5a27a-112">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="5a27a-113">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="5a27a-113">Parent Elements</span></span>

|<span data-ttu-id="5a27a-114">Elem</span><span class="sxs-lookup"><span data-stu-id="5a27a-114">Element</span></span>|<span data-ttu-id="5a27a-115">Leírás</span><span class="sxs-lookup"><span data-stu-id="5a27a-115">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="5a27a-116">Keret eleme CustomItem vezérlők nézet (formátum)</span><span class="sxs-lookup"><span data-stu-id="5a27a-116">Frame Element for CustomItem for Controls for View (Format)</span></span>](./frame-element-for-customitem-for-controls-for-view-format.md)|<span data-ttu-id="5a27a-117">Határozza meg, hogyan egy jelennek meg, például az adatok pótlása jobbra vagy balra.</span><span class="sxs-lookup"><span data-stu-id="5a27a-117">Defines how the data is displayed, such as shifting the data to the left or right.</span></span>|

## <a name="text-value"></a><span data-ttu-id="5a27a-118">Szöveges érték</span><span class="sxs-lookup"><span data-stu-id="5a27a-118">Text Value</span></span>

<span data-ttu-id="5a27a-119">Adja meg, hogy az adatok első sora shift kívánt karakterek száma.</span><span class="sxs-lookup"><span data-stu-id="5a27a-119">Specify the number of characters that you want to shift the first line of the data.</span></span>

## <a name="remarks"></a><span data-ttu-id="5a27a-120">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="5a27a-120">Remarks</span></span>

<span data-ttu-id="5a27a-121">Ha ez az elem meg van adva, nem adható meg a [FirstLineIndent](./firstlineindent-element-for-frame-for-controls-for-view-format.md) elemet.</span><span class="sxs-lookup"><span data-stu-id="5a27a-121">If this element is specified, you cannot specify the [FirstLineIndent](./firstlineindent-element-for-frame-for-controls-for-view-format.md) element.</span></span>

## <a name="see-also"></a><span data-ttu-id="5a27a-122">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="5a27a-122">See Also</span></span>

[<span data-ttu-id="5a27a-123">Keret (formátum) nézet vezérlők FirstLineIndent elem.</span><span class="sxs-lookup"><span data-stu-id="5a27a-123">FirstLineIndent Element for Frame for Controls for View (Format)</span></span>](./firstlineindent-element-for-frame-for-controls-for-view-format.md)

[<span data-ttu-id="5a27a-124">Keret eleme CustomItem vezérlők nézet (formátum)</span><span class="sxs-lookup"><span data-stu-id="5a27a-124">Frame Element for CustomItem for Controls for View (Format)</span></span>](./frame-element-for-customitem-for-controls-for-view-format.md)

[<span data-ttu-id="5a27a-125">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="5a27a-125">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
