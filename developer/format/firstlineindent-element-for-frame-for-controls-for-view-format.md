---
title: Keret (formátum) nézet vezérlők FirstLineIndent elem |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ec63f4f9-8858-4529-8646-ffbbc278f83e
caps.latest.revision: 7
ms.openlocfilehash: 694c5baaa5e90a772257276ba139d90acf7ec0e3
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62066022"
---
# <a name="firstlineindent-element-for-frame-for-controls-for-view-format"></a><span data-ttu-id="b58e4-102">A Nézet Vezérlők eleméhez tartozó Keret FirstLineIndent eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="b58e4-102">FirstLineIndent Element for Frame for Controls for View (Format)</span></span>

<span data-ttu-id="b58e4-103">Megadja az adatok első sorának jobb úgy, hogy hány karakter.</span><span class="sxs-lookup"><span data-stu-id="b58e4-103">Specifies how many characters the first line of data is shifted to the right.</span></span> <span data-ttu-id="b58e4-104">Ez az elem szolgál a nézet által használható vezérlők meghatározásakor.</span><span class="sxs-lookup"><span data-stu-id="b58e4-104">This element is used when defining controls that can be used by a view.</span></span>

<span data-ttu-id="b58e4-105">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem vezérlők elem (formátum) vezérlőelem elem vezérlők, a nézet (formátum) CustomControl elem megtekintése (formátum) CustomEntries elemet a vezérlők a vezérlő A nézet (formátum) CustomEntry elem CustomEntries vezérlők, a vezérlők, a vezérlők, a nézet (formátum) FirstLineIndent elem keret CustomItem megtekintése (formátum) keret elemhez CustomEntry megtekintése (formátum) CustomItem elemhez tartozó CustomControl a vezérlőelemek nézet (formátum)</span><span class="sxs-lookup"><span data-stu-id="b58e4-105">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) Controls Element (Format) Control Element for Controls for View (Format) CustomControl Element for Control for Controls for View (Format) CustomEntries Element for CustomControl for View (Format) CustomEntry Element for CustomEntries for Controls for View (Format) CustomItem Element for CustomEntry for Controls for View (Format) Frame Element for CustomItem for Controls for View (Format) FirstLineIndent Element of Frame of Controls of View (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="b58e4-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="b58e4-106">Syntax</span></span>

```xml
<FirstLineIndent>NumberOfCharactersToShift</FirstLineIndent>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="b58e4-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="b58e4-107">Attributes and Elements</span></span>

<span data-ttu-id="b58e4-108">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és szülőelemét a `FirstLineIndent` elemet.</span><span class="sxs-lookup"><span data-stu-id="b58e4-108">The following sections describe attributes, child elements, and parent element of the `FirstLineIndent` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="b58e4-109">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="b58e4-109">Attributes</span></span>

<span data-ttu-id="b58e4-110">Nincs.</span><span class="sxs-lookup"><span data-stu-id="b58e4-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="b58e4-111">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="b58e4-111">Child Elements</span></span>

<span data-ttu-id="b58e4-112">Nincs.</span><span class="sxs-lookup"><span data-stu-id="b58e4-112">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="b58e4-113">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="b58e4-113">Parent Elements</span></span>

|<span data-ttu-id="b58e4-114">Elem</span><span class="sxs-lookup"><span data-stu-id="b58e4-114">Element</span></span>|<span data-ttu-id="b58e4-115">Leírás</span><span class="sxs-lookup"><span data-stu-id="b58e4-115">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="b58e4-116">Keret eleme CustomItem vezérlők nézet (formátum)</span><span class="sxs-lookup"><span data-stu-id="b58e4-116">Frame Element for CustomItem for Controls for View (Format)</span></span>](./frame-element-for-customitem-for-controls-for-view-format.md)|<span data-ttu-id="b58e4-117">Határozza meg, hogyan egy jelennek meg, például az adatok pótlása jobbra vagy balra.</span><span class="sxs-lookup"><span data-stu-id="b58e4-117">Defines how the data is displayed, such as shifting the data to the left or right.</span></span>|

## <a name="text-value"></a><span data-ttu-id="b58e4-118">A szöveges érték</span><span class="sxs-lookup"><span data-stu-id="b58e4-118">Text Value</span></span>

<span data-ttu-id="b58e4-119">Adja meg, hogy az adatok első sora shift kívánt karakterek száma.</span><span class="sxs-lookup"><span data-stu-id="b58e4-119">Specify the number of characters that you want to shift the first line of the data.</span></span>

## <a name="remarks"></a><span data-ttu-id="b58e4-120">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="b58e4-120">Remarks</span></span>

<span data-ttu-id="b58e4-121">Ha ez az elem meg van adva, nem adható meg a [FirstLineHanging](./firstlinehanging-element-for-frame-for-controls-for-view-format.md) elemet.</span><span class="sxs-lookup"><span data-stu-id="b58e4-121">If this element is specified, you cannot specify the [FirstLineHanging](./firstlinehanging-element-for-frame-for-controls-for-view-format.md) element.</span></span>

## <a name="see-also"></a><span data-ttu-id="b58e4-122">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="b58e4-122">See Also</span></span>

[<span data-ttu-id="b58e4-123">Keret (formátum) nézet vezérlők FirstLineHanging elem.</span><span class="sxs-lookup"><span data-stu-id="b58e4-123">FirstLineHanging Element for Frame for Controls for View (Format)</span></span>](./firstlinehanging-element-for-frame-for-controls-for-view-format.md)

[<span data-ttu-id="b58e4-124">Keret eleme CustomItem vezérlők nézet (formátum)</span><span class="sxs-lookup"><span data-stu-id="b58e4-124">Frame Element for CustomItem for Controls for View (Format)</span></span>](./frame-element-for-customitem-for-controls-for-view-format.md)

[<span data-ttu-id="b58e4-125">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="b58e4-125">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
