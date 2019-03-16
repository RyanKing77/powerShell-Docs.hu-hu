---
title: Nézet (formátum) CustomControl-keret FirstLineHanging elem |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: c6ac3d86-0529-4b93-9bc7-ee94fcef9618
caps.latest.revision: 8
ms.openlocfilehash: ea43e025f5f653ff000e1d7591b535e73da5c9e5
ms.sourcegitcommit: caac7d098a448232304c9d6728e7340ec7517a71
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/16/2019
ms.locfileid: "58054220"
---
# <a name="firstlinehanging-element-for-frame-for-customcontrol-for-view-format"></a><span data-ttu-id="86b88-102">A Nézet CustomControl eleméhez tartozó Keret FirstLineHanging eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="86b88-102">FirstLineHanging Element for Frame for CustomControl for View (Format)</span></span>

<span data-ttu-id="86b88-103">Megadja a bal oldali adatok első sora úgy, hogy hány karakter.</span><span class="sxs-lookup"><span data-stu-id="86b88-103">Specifies how many characters the first line of data is shifted to the left.</span></span> <span data-ttu-id="86b88-104">Ehhez az elemhez használt egyéni vezérlő nézet definiálása.</span><span class="sxs-lookup"><span data-stu-id="86b88-104">This element is used when defining a custom control view.</span></span>

<span data-ttu-id="86b88-105">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézet elem (formátum) CustomControl elem (formátum) CustomEntries eleme CustomControl megtekintése (formátum) CustomEntry elem megtekintése (formátum) CustomItem elemhez tartozó CustomEntries számára A CustomControl CustomControl nézet (formátum)-keret megtekintése (formátum) FirstLineHanging elemhez tartozó CustomItem CustomControlView (formátum) keret elemhez CustomEntry</span><span class="sxs-lookup"><span data-stu-id="86b88-105">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) CustomControl Element (Format) CustomEntries Element for CustomControl for View (Format) CustomEntry Element for CustomEntries for View (Format) CustomItem Element for CustomEntry for CustomControlView (Format) Frame Element for CustomItem for CustomControl for View (Format) FirstLineHanging Element for Frame for CustomControl for View (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="86b88-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="86b88-106">Syntax</span></span>

```xml
<FirstLineHanging>NumberOfCharactersToShift</FirstLineHanging>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="86b88-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="86b88-107">Attributes and Elements</span></span>

<span data-ttu-id="86b88-108">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és szülőelemét a `FirstLineHanging` elemet.</span><span class="sxs-lookup"><span data-stu-id="86b88-108">The following sections describe attributes, child elements, and parent element of the `FirstLineHanging` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="86b88-109">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="86b88-109">Attributes</span></span>

<span data-ttu-id="86b88-110">Nincs.</span><span class="sxs-lookup"><span data-stu-id="86b88-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="86b88-111">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="86b88-111">Child Elements</span></span>

<span data-ttu-id="86b88-112">Nincs.</span><span class="sxs-lookup"><span data-stu-id="86b88-112">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="86b88-113">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="86b88-113">Parent Elements</span></span>

|<span data-ttu-id="86b88-114">Elem</span><span class="sxs-lookup"><span data-stu-id="86b88-114">Element</span></span>|<span data-ttu-id="86b88-115">Leírás</span><span class="sxs-lookup"><span data-stu-id="86b88-115">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="86b88-116">A nézet (formátum) CustomControl CustomItem keret elem.</span><span class="sxs-lookup"><span data-stu-id="86b88-116">Frame Element for CustomItem for CustomControl for View (Format)</span></span>](./frame-element-for-customitem-for-customcontrol-for-view-format.md)|<span data-ttu-id="86b88-117">Határozza meg, hogyan egy jelennek meg, például az adatok pótlása jobbra vagy balra.</span><span class="sxs-lookup"><span data-stu-id="86b88-117">Defines how the data is displayed, such as shifting the data to the left or right.</span></span>|

## <a name="text-value"></a><span data-ttu-id="86b88-118">Szöveges érték</span><span class="sxs-lookup"><span data-stu-id="86b88-118">Text Value</span></span>

<span data-ttu-id="86b88-119">Adja meg, hogy az adatok első sora shift kívánt karakterek száma.</span><span class="sxs-lookup"><span data-stu-id="86b88-119">Specify the number of characters that you want to shift the first line of the data.</span></span>

## <a name="remarks"></a><span data-ttu-id="86b88-120">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="86b88-120">Remarks</span></span>

<span data-ttu-id="86b88-121">Ha ez az elem meg van adva, nem adható meg a [FirstLineIndent](./firstlineindent-element-for-frame-for-customcontrol-for-view-format.md) elemet.</span><span class="sxs-lookup"><span data-stu-id="86b88-121">If this element is specified, you cannot specify the [FirstLineIndent](./firstlineindent-element-for-frame-for-customcontrol-for-view-format.md) element.</span></span>

## <a name="see-also"></a><span data-ttu-id="86b88-122">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="86b88-122">See Also</span></span>

[<span data-ttu-id="86b88-123">A nézet (formátum) CustomControl keret FirstLineIndent eleme</span><span class="sxs-lookup"><span data-stu-id="86b88-123">FirstLineIndent Element for Frame for CustomControl for View (Format)</span></span>](./firstlineindent-element-for-frame-for-customcontrol-for-view-format.md)

[<span data-ttu-id="86b88-124">A nézet (formátum) CustomControl CustomItem keret elem.</span><span class="sxs-lookup"><span data-stu-id="86b88-124">Frame Element for CustomItem for CustomControl for View (Format)</span></span>](./frame-element-for-customitem-for-customcontrol-for-view-format.md)

[<span data-ttu-id="86b88-125">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="86b88-125">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
