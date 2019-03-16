---
title: Nézet (formátum) CustomControl-keret FirstLineIndent elem |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: bb4e1564-3fd3-4be3-b93e-ac90480e05c0
caps.latest.revision: 6
ms.openlocfilehash: 3130ecc69f7d1568bcbd392dd24e8cdcc3382905
ms.sourcegitcommit: caac7d098a448232304c9d6728e7340ec7517a71
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/16/2019
ms.locfileid: "58054849"
---
# <a name="firstlineindent-element-for-frame-for-customcontrol-for-view-format"></a><span data-ttu-id="412cc-102">A Nézet CustomControl eleméhez tartozó Keret FirstLineIndent eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="412cc-102">FirstLineIndent Element for Frame for CustomControl for View (Format)</span></span>

<span data-ttu-id="412cc-103">Megadja az adatok első sorának jobb úgy, hogy hány karakter.</span><span class="sxs-lookup"><span data-stu-id="412cc-103">Specifies how many characters the first line of data is shifted to the right.</span></span> <span data-ttu-id="412cc-104">Ehhez az elemhez használt egyéni vezérlő nézet definiálása.</span><span class="sxs-lookup"><span data-stu-id="412cc-104">This element is used when defining a custom control view.</span></span>

<span data-ttu-id="412cc-105">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézet elem (formátum) CustomControl elem (formátum) CustomEntries eleme CustomControl megtekintése (formátum) CustomEntry elem megtekintése (formátum) CustomItem elemhez tartozó CustomEntries számára A CustomControl megtekintése (formátum) FirstLineIndent elemhez tartozó CustomItem CustomControlView (formátum) keret elemhez CustomEntry</span><span class="sxs-lookup"><span data-stu-id="412cc-105">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) CustomControl Element (Format) CustomEntries Element for CustomControl for View (Format) CustomEntry Element for CustomEntries for View (Format) CustomItem Element for CustomEntry for CustomControlView (Format) Frame Element for CustomItem for CustomControl for View (Format) FirstLineIndent Element</span></span>

## <a name="syntax"></a><span data-ttu-id="412cc-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="412cc-106">Syntax</span></span>

```xml
<FirstLineIndent>NumberOfCharactersToShift</FirstLineIndent>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="412cc-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="412cc-107">Attributes and Elements</span></span>

<span data-ttu-id="412cc-108">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és szülőelemét a `FirstLineIndent` elemet.</span><span class="sxs-lookup"><span data-stu-id="412cc-108">The following sections describe attributes, child elements, and parent element of the `FirstLineIndent` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="412cc-109">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="412cc-109">Attributes</span></span>

<span data-ttu-id="412cc-110">Nincs.</span><span class="sxs-lookup"><span data-stu-id="412cc-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="412cc-111">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="412cc-111">Child Elements</span></span>

<span data-ttu-id="412cc-112">Nincs.</span><span class="sxs-lookup"><span data-stu-id="412cc-112">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="412cc-113">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="412cc-113">Parent Elements</span></span>

|<span data-ttu-id="412cc-114">Elem</span><span class="sxs-lookup"><span data-stu-id="412cc-114">Element</span></span>|<span data-ttu-id="412cc-115">Leírás</span><span class="sxs-lookup"><span data-stu-id="412cc-115">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="412cc-116">A nézet (formátum) CustomControl CustomItem keret elem.</span><span class="sxs-lookup"><span data-stu-id="412cc-116">Frame Element for CustomItem for CustomControl for View (Format)</span></span>](./frame-element-for-customitem-for-customcontrol-for-view-format.md)|<span data-ttu-id="412cc-117">Határozza meg, hogyan egy jelennek meg, például az adatok pótlása jobbra vagy balra.</span><span class="sxs-lookup"><span data-stu-id="412cc-117">Defines how the data is displayed, such as shifting the data to the left or right.</span></span>|

## <a name="text-value"></a><span data-ttu-id="412cc-118">Szöveges érték</span><span class="sxs-lookup"><span data-stu-id="412cc-118">Text Value</span></span>

<span data-ttu-id="412cc-119">Adja meg, hogy az adatok első sora shift kívánt karakterek száma.</span><span class="sxs-lookup"><span data-stu-id="412cc-119">Specify the number of characters that you want to shift the first line of the data.</span></span>

## <a name="remarks"></a><span data-ttu-id="412cc-120">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="412cc-120">Remarks</span></span>

<span data-ttu-id="412cc-121">Ha ez az elem meg van adva, nem adható meg a [FirstLineHanging](./firstlinehanging-element-for-frame-for-customcontrol-for-view-format.md) elemet.</span><span class="sxs-lookup"><span data-stu-id="412cc-121">If this element is specified, you cannot specify the [FirstLineHanging](./firstlinehanging-element-for-frame-for-customcontrol-for-view-format.md) element.</span></span>

## <a name="see-also"></a><span data-ttu-id="412cc-122">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="412cc-122">See Also</span></span>

[<span data-ttu-id="412cc-123">A nézet (formátum) CustomControl keret FirstLineHanging eleme</span><span class="sxs-lookup"><span data-stu-id="412cc-123">FirstLineHanging Element for Frame for CustomControl for View (Format)</span></span>](./firstlinehanging-element-for-frame-for-customcontrol-for-view-format.md)

[<span data-ttu-id="412cc-124">A nézet (formátum) CustomControl CustomItem keret elem.</span><span class="sxs-lookup"><span data-stu-id="412cc-124">Frame Element for CustomItem for CustomControl for View (Format)</span></span>](./frame-element-for-customitem-for-customcontrol-for-view-format.md)

[<span data-ttu-id="412cc-125">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="412cc-125">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
