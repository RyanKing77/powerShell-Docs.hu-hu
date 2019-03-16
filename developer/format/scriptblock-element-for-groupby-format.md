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
ms.openlocfilehash: f2f6b9af7740b1231881294c2f32bf97b5a1568b
ms.sourcegitcommit: caac7d098a448232304c9d6728e7340ec7517a71
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/16/2019
ms.locfileid: "58054425"
---
# <a name="scriptblock-element-for-groupby-format"></a><span data-ttu-id="50ad3-102">A GroupBy ScriptBlock eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="50ad3-102">ScriptBlock Element for GroupBy (Format)</span></span>

<span data-ttu-id="50ad3-103">Adja meg a parancsfájl, amely elindítja egy új csoportot, amikor annak értéke módosul.</span><span class="sxs-lookup"><span data-stu-id="50ad3-103">Specifies the script that starts a new group whenever its value changes.</span></span>

<span data-ttu-id="50ad3-104">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem GroupBy elem a scriptblock kulcsszót elem megtekintése (formátum) a GroupBy (formátum)</span><span class="sxs-lookup"><span data-stu-id="50ad3-104">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) GroupBy Element for View (Format) ScriptBlock Element for GroupBy (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="50ad3-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="50ad3-105">Syntax</span></span>

```xml
<ScriptBlock>ScriptToEvaluate</ScriptBlock>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="50ad3-106">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="50ad3-106">Attributes and Elements</span></span>

<span data-ttu-id="50ad3-107">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `ScriptBlock` elemet.</span><span class="sxs-lookup"><span data-stu-id="50ad3-107">The following sections describe attributes, child elements, and the parent element of the `ScriptBlock` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="50ad3-108">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="50ad3-108">Attributes</span></span>

<span data-ttu-id="50ad3-109">Nincs.</span><span class="sxs-lookup"><span data-stu-id="50ad3-109">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="50ad3-110">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="50ad3-110">Child Elements</span></span>

<span data-ttu-id="50ad3-111">Nincs.</span><span class="sxs-lookup"><span data-stu-id="50ad3-111">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="50ad3-112">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="50ad3-112">Parent Elements</span></span>

|<span data-ttu-id="50ad3-113">Elem</span><span class="sxs-lookup"><span data-stu-id="50ad3-113">Element</span></span>|<span data-ttu-id="50ad3-114">Leírás</span><span class="sxs-lookup"><span data-stu-id="50ad3-114">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="50ad3-115">GroupBy elem nézet (formátum)</span><span class="sxs-lookup"><span data-stu-id="50ad3-115">GroupBy Element for View (Format)</span></span>](./groupby-element-for-view-format.md)|<span data-ttu-id="50ad3-116">Határozza meg, hogyan jelenjen meg a .NET-objektumokká csoportja.</span><span class="sxs-lookup"><span data-stu-id="50ad3-116">Defines how a group of .NET objects is displayed.</span></span>|

## <a name="text-value"></a><span data-ttu-id="50ad3-117">Szöveges érték</span><span class="sxs-lookup"><span data-stu-id="50ad3-117">Text Value</span></span>

<span data-ttu-id="50ad3-118">Adja meg a parancsfájl, amely ki lesz értékelve.</span><span class="sxs-lookup"><span data-stu-id="50ad3-118">Specify the script that is evaluated.</span></span>

## <a name="remarks"></a><span data-ttu-id="50ad3-119">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="50ad3-119">Remarks</span></span>

<span data-ttu-id="50ad3-120">Windows PowerShell elindul egy új csoportot, minden alkalommal, amikor ez a szkript értékét módosítja.</span><span class="sxs-lookup"><span data-stu-id="50ad3-120">Windows PowerShell starts a new group whenever the value of this script changes.</span></span>

<span data-ttu-id="50ad3-121">Ha ez az elem meg van adva, nem adható meg a [PropertyName](http://msdn.microsoft.com/en-us/396dede0-039a-4a87-a5ef-3ecabb729676) elem elindítani egy új csoportot.</span><span class="sxs-lookup"><span data-stu-id="50ad3-121">When this element is specified, you cannot specify the [PropertyName](http://msdn.microsoft.com/en-us/396dede0-039a-4a87-a5ef-3ecabb729676) element to start a new group.</span></span>

## <a name="see-also"></a><span data-ttu-id="50ad3-122">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="50ad3-122">See Also</span></span>

[<span data-ttu-id="50ad3-123">A PropertyName elemet a GroupBy (formátum)</span><span class="sxs-lookup"><span data-stu-id="50ad3-123">PropertyName Element for GroupBy (Format)</span></span>](./propertyname-element-for-groupby-format.md)

[<span data-ttu-id="50ad3-124">GroupBy elem nézet (formátum)</span><span class="sxs-lookup"><span data-stu-id="50ad3-124">GroupBy Element for View (Format)</span></span>](./groupby-element-for-view-format.md)

[<span data-ttu-id="50ad3-125">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="50ad3-125">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
