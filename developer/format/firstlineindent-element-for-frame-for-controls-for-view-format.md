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
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56845632"
---
# <a name="firstlineindent-element-for-frame-for-controls-for-view-format"></a><span data-ttu-id="05f36-102">A Nézet Vezérlők eleméhez tartozó Keret FirstLineIndent eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="05f36-102">FirstLineIndent Element for Frame for Controls for View (Format)</span></span>

<span data-ttu-id="05f36-103">Megadja az adatok első sorának jobb úgy, hogy hány karakter.</span><span class="sxs-lookup"><span data-stu-id="05f36-103">Specifies how many characters the first line of data is shifted to the right.</span></span> <span data-ttu-id="05f36-104">Ez az elem szolgál a nézet által használható vezérlők meghatározásakor.</span><span class="sxs-lookup"><span data-stu-id="05f36-104">This element is used when defining controls that can be used by a view.</span></span>

<span data-ttu-id="05f36-105">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem vezérlők elem (formátum) vezérlőelem elem vezérlők, a nézet (formátum) CustomControl elem megtekintése (formátum) CustomEntries elemet a vezérlők a vezérlő A nézet (formátum) CustomEntry elem CustomEntries vezérlők, a vezérlők, a vezérlők, a nézet (formátum) FirstLineIndent elem keret CustomItem megtekintése (formátum) keret elemhez CustomEntry megtekintése (formátum) CustomItem elemhez tartozó CustomControl a vezérlőelemek nézet (formátum)</span><span class="sxs-lookup"><span data-stu-id="05f36-105">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) Controls Element (Format) Control Element for Controls for View (Format) CustomControl Element for Control for Controls for View (Format) CustomEntries Element for CustomControl for View (Format) CustomEntry Element for CustomEntries for Controls for View (Format) CustomItem Element for CustomEntry for Controls for View (Format) Frame Element for CustomItem for Controls for View (Format) FirstLineIndent Element of Frame of Controls of View (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="05f36-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="05f36-106">Syntax</span></span>

```xml
<FirstLineIndent>NumberOfCharactersToShift</FirstLineIndent>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="05f36-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="05f36-107">Attributes and Elements</span></span>

<span data-ttu-id="05f36-108">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és szülőelemét a `FirstLineIndent` elemet.</span><span class="sxs-lookup"><span data-stu-id="05f36-108">The following sections describe attributes, child elements, and parent element of the `FirstLineIndent` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="05f36-109">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="05f36-109">Attributes</span></span>

<span data-ttu-id="05f36-110">Nincs.</span><span class="sxs-lookup"><span data-stu-id="05f36-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="05f36-111">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="05f36-111">Child Elements</span></span>

<span data-ttu-id="05f36-112">Nincs.</span><span class="sxs-lookup"><span data-stu-id="05f36-112">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="05f36-113">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="05f36-113">Parent Elements</span></span>

|<span data-ttu-id="05f36-114">Elem</span><span class="sxs-lookup"><span data-stu-id="05f36-114">Element</span></span>|<span data-ttu-id="05f36-115">Leírás</span><span class="sxs-lookup"><span data-stu-id="05f36-115">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="05f36-116">Keret eleme CustomItem vezérlők nézet (formátum)</span><span class="sxs-lookup"><span data-stu-id="05f36-116">Frame Element for CustomItem for Controls for View (Format)</span></span>](./frame-element-for-customitem-for-controls-for-view-format.md)|<span data-ttu-id="05f36-117">Határozza meg, hogyan egy jelennek meg, például az adatok pótlása jobbra vagy balra.</span><span class="sxs-lookup"><span data-stu-id="05f36-117">Defines how the data is displayed, such as shifting the data to the left or right.</span></span>|

## <a name="text-value"></a><span data-ttu-id="05f36-118">Szöveges érték</span><span class="sxs-lookup"><span data-stu-id="05f36-118">Text Value</span></span>

<span data-ttu-id="05f36-119">Adja meg, hogy az adatok első sora shift kívánt karakterek száma.</span><span class="sxs-lookup"><span data-stu-id="05f36-119">Specify the number of characters that you want to shift the first line of the data.</span></span>

## <a name="remarks"></a><span data-ttu-id="05f36-120">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="05f36-120">Remarks</span></span>

<span data-ttu-id="05f36-121">Ha ez az elem meg van adva, nem adható meg a [FirstLineHanging](./firstlinehanging-element-for-frame-for-controls-for-view-format.md) elemet.</span><span class="sxs-lookup"><span data-stu-id="05f36-121">If this element is specified, you cannot specify the [FirstLineHanging](./firstlinehanging-element-for-frame-for-controls-for-view-format.md) element.</span></span>

## <a name="see-also"></a><span data-ttu-id="05f36-122">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="05f36-122">See Also</span></span>

[<span data-ttu-id="05f36-123">Keret (formátum) nézet vezérlők FirstLineHanging elem.</span><span class="sxs-lookup"><span data-stu-id="05f36-123">FirstLineHanging Element for Frame for Controls for View (Format)</span></span>](./firstlinehanging-element-for-frame-for-controls-for-view-format.md)

[<span data-ttu-id="05f36-124">Keret eleme CustomItem vezérlők nézet (formátum)</span><span class="sxs-lookup"><span data-stu-id="05f36-124">Frame Element for CustomItem for Controls for View (Format)</span></span>](./frame-element-for-customitem-for-controls-for-view-format.md)

[<span data-ttu-id="05f36-125">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="05f36-125">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
