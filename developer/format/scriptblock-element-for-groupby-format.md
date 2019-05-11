---
title: GroupBy (formátum) a scriptblock kulcsszót elem |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 30183927-6f0e-4717-b6f5-f07a6e134cfb
caps.latest.revision: 6
ms.openlocfilehash: 37a297228eb33ff75daf94a12635d42b52c6cc9f
ms.sourcegitcommit: 58fb23c854f5a8b40ad1f952d3323aeeccac7a24
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/07/2019
ms.locfileid: "65229319"
---
# <a name="scriptblock-element-for-groupby-format"></a><span data-ttu-id="ed874-102">A GroupBy ScriptBlock eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="ed874-102">ScriptBlock Element for GroupBy (Format)</span></span>

<span data-ttu-id="ed874-103">Adja meg a parancsfájl, amely elindítja egy új csoportot, amikor annak értéke módosul.</span><span class="sxs-lookup"><span data-stu-id="ed874-103">Specifies the script that starts a new group whenever its value changes.</span></span>

<span data-ttu-id="ed874-104">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem GroupBy elem a scriptblock kulcsszót elem megtekintése (formátum) a GroupBy (formátum)</span><span class="sxs-lookup"><span data-stu-id="ed874-104">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) GroupBy Element for View (Format) ScriptBlock Element for GroupBy (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="ed874-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="ed874-105">Syntax</span></span>

```xml
<ScriptBlock>ScriptToEvaluate</ScriptBlock>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="ed874-106">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="ed874-106">Attributes and Elements</span></span>

<span data-ttu-id="ed874-107">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `ScriptBlock` elemet.</span><span class="sxs-lookup"><span data-stu-id="ed874-107">The following sections describe attributes, child elements, and the parent element of the `ScriptBlock` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="ed874-108">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="ed874-108">Attributes</span></span>

<span data-ttu-id="ed874-109">Nincs.</span><span class="sxs-lookup"><span data-stu-id="ed874-109">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="ed874-110">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="ed874-110">Child Elements</span></span>

<span data-ttu-id="ed874-111">Nincs.</span><span class="sxs-lookup"><span data-stu-id="ed874-111">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="ed874-112">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="ed874-112">Parent Elements</span></span>

|<span data-ttu-id="ed874-113">Elem</span><span class="sxs-lookup"><span data-stu-id="ed874-113">Element</span></span>|<span data-ttu-id="ed874-114">Leírás</span><span class="sxs-lookup"><span data-stu-id="ed874-114">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="ed874-115">GroupBy elem nézet (formátum)</span><span class="sxs-lookup"><span data-stu-id="ed874-115">GroupBy Element for View (Format)</span></span>](./groupby-element-for-view-format.md)|<span data-ttu-id="ed874-116">Határozza meg, hogyan jelenjen meg a .NET-objektumokká csoportja.</span><span class="sxs-lookup"><span data-stu-id="ed874-116">Defines how a group of .NET objects is displayed.</span></span>|

## <a name="text-value"></a><span data-ttu-id="ed874-117">A szöveges érték</span><span class="sxs-lookup"><span data-stu-id="ed874-117">Text Value</span></span>

<span data-ttu-id="ed874-118">Adja meg a parancsfájl, amely ki lesz értékelve.</span><span class="sxs-lookup"><span data-stu-id="ed874-118">Specify the script that is evaluated.</span></span>

## <a name="remarks"></a><span data-ttu-id="ed874-119">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="ed874-119">Remarks</span></span>

<span data-ttu-id="ed874-120">PowerShell elindul egy új csoportot, minden alkalommal, amikor ez a szkript értékét módosítja.</span><span class="sxs-lookup"><span data-stu-id="ed874-120">PowerShell starts a new group whenever the value of this script changes.</span></span>

<span data-ttu-id="ed874-121">Ha ez az elem meg van adva, nem adható meg a [PropertyName](propertyname-element-for-groupby-format.md) elem elindítani egy új csoportot.</span><span class="sxs-lookup"><span data-stu-id="ed874-121">When this element is specified, you cannot specify the [PropertyName](propertyname-element-for-groupby-format.md) element to start a new group.</span></span>

## <a name="see-also"></a><span data-ttu-id="ed874-122">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="ed874-122">See Also</span></span>

[<span data-ttu-id="ed874-123">A PropertyName elemet a GroupBy (formátum)</span><span class="sxs-lookup"><span data-stu-id="ed874-123">PropertyName Element for GroupBy (Format)</span></span>](propertyname-element-for-groupby-format.md)

[<span data-ttu-id="ed874-124">GroupBy elem nézet (formátum)</span><span class="sxs-lookup"><span data-stu-id="ed874-124">GroupBy Element for View (Format)</span></span>](groupby-element-for-view-format.md)

[<span data-ttu-id="ed874-125">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="ed874-125">Writing a PowerShell Formatting File</span></span>](writing-a-powershell-formatting-file.md)
