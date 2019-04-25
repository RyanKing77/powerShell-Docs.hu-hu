---
title: ItemSelectionCondition ListControl (formátum) a scriptblock kulcsszót eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: c929a6df-d050-416a-9de0-e913dd5a035c
caps.latest.revision: 8
ms.openlocfilehash: a0768a9c1ac66cd9dcf1848c4b031ccbc722b4c2
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62064407"
---
# <a name="scriptblock-element-for-itemselectioncondition-for-listcontrol-format"></a><span data-ttu-id="fa67a-102">A ListControl elemhez tartozó ItemSelectionCondition ScriptBlock eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="fa67a-102">ScriptBlock Element for ItemSelectionCondition for ListControl (Format)</span></span>

<span data-ttu-id="fa67a-103">Megadja a parancsprogramot, amely elindítja a feltétel.</span><span class="sxs-lookup"><span data-stu-id="fa67a-103">Specifies the script that triggers the condition.</span></span> <span data-ttu-id="fa67a-104">Ha ez a parancsfájl kiértékelése `true`, a feltétel nem teljesül, és a listaelem szolgál.</span><span class="sxs-lookup"><span data-stu-id="fa67a-104">When this script is evaluated to `true`, the condition is met, and the list item is used.</span></span> <span data-ttu-id="fa67a-105">Ez az elem akkor használatos, ha a lista nézet definiálása.</span><span class="sxs-lookup"><span data-stu-id="fa67a-105">This element is used when defining a list view.</span></span>

<span data-ttu-id="fa67a-106">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézet elem (formátum) ListControl elem (formátum) ListEntries eleme ListEntries ListControl (formátum) ListItems elemek elemhez tartozó ListEntry ListEntry eleme ListControl (formátum) ListControl (formátum) ListItem elem a lista ListItems elemek szabályozása (formátum) ItemSelectionCondition eleme ListItem ListControl (formátum) ScriptBlock elemhez tartozó ItemSelectionCondition ListControl (formátum)</span><span class="sxs-lookup"><span data-stu-id="fa67a-106">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) ListControl Element (Format) ListEntries Element for ListControl (Format) ListEntry Element for ListEntries for ListControl (Format) ListItems Element for ListEntry for ListControl (Format) ListItem Element for ListItems for List Control (Format) ItemSelectionCondition Element for ListItem for ListControl (Format) ScriptBlock Element for ItemSelectionCondition for ListControl  (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="fa67a-107">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="fa67a-107">Syntax</span></span>

```xml
<ScriptBlock>ScriptToEvaluate</ScriptBlock>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="fa67a-108">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="fa67a-108">Attributes and Elements</span></span>

<span data-ttu-id="fa67a-109">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a szülő elemei a `ScriptBlock` elemet.</span><span class="sxs-lookup"><span data-stu-id="fa67a-109">The following sections describe attributes, child elements, and the parent elements of the `ScriptBlock` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="fa67a-110">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="fa67a-110">Attributes</span></span>

<span data-ttu-id="fa67a-111">Nincs.</span><span class="sxs-lookup"><span data-stu-id="fa67a-111">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="fa67a-112">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="fa67a-112">Child Elements</span></span>

<span data-ttu-id="fa67a-113">Nincs.</span><span class="sxs-lookup"><span data-stu-id="fa67a-113">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="fa67a-114">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="fa67a-114">Parent Elements</span></span>

|<span data-ttu-id="fa67a-115">Elem</span><span class="sxs-lookup"><span data-stu-id="fa67a-115">Element</span></span>|<span data-ttu-id="fa67a-116">Leírás</span><span class="sxs-lookup"><span data-stu-id="fa67a-116">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="fa67a-117">A ListControl (formátum) ListItem ItemSelectionCondition eleme</span><span class="sxs-lookup"><span data-stu-id="fa67a-117">ItemSelectionCondition Element for ListItem for ListControl (Format)</span></span>](./itemselectioncondition-element-for-listitem-for-listcontrol-format.md)|<span data-ttu-id="fa67a-118">Határozza meg azt a feltételt, amelyet a listaelem használandó léteznie kell.</span><span class="sxs-lookup"><span data-stu-id="fa67a-118">Defines the condition that must exist for this list item to be used.</span></span>|

## <a name="text-value"></a><span data-ttu-id="fa67a-119">A szöveges érték</span><span class="sxs-lookup"><span data-stu-id="fa67a-119">Text Value</span></span>

<span data-ttu-id="fa67a-120">Adja meg a parancsfájl, amely ki lesz értékelve.</span><span class="sxs-lookup"><span data-stu-id="fa67a-120">Specify the script that is evaluated.</span></span>

## <a name="remarks"></a><span data-ttu-id="fa67a-121">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="fa67a-121">Remarks</span></span>

<span data-ttu-id="fa67a-122">Ha ez az elem használata esetén nem adható meg a `PropertyName` elemet a kiválasztási feltétel meghatározásakor.</span><span class="sxs-lookup"><span data-stu-id="fa67a-122">If this element is used, you cannot specify the `PropertyName` element when defining the selection condition.</span></span>

## <a name="see-also"></a><span data-ttu-id="fa67a-123">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="fa67a-123">See Also</span></span>

[<span data-ttu-id="fa67a-124">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="fa67a-124">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
