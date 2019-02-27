---
title: WideItem WideControl (formátum) a scriptblock kulcsszót eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: e00e8f36-76f2-49a0-9b02-3a2a7fceb2dd
caps.latest.revision: 8
ms.openlocfilehash: 6534e9dbfbe0dedf60dadd6467cff9ad9b447ba4
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56848229"
---
# <a name="scriptblock-element-for-wideitem-for-widecontrol-format"></a><span data-ttu-id="c21ab-102">A WideControl WideControl elemének ScriptBlock eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="c21ab-102">ScriptBlock Element for WideItem for WideControl (Format)</span></span>

<span data-ttu-id="c21ab-103">Megadja a parancsprogramot, amelynek az értéke az széles nézetben jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="c21ab-103">Specifies the script whose value is displayed in the wide view.</span></span>

<span data-ttu-id="c21ab-104">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem WideControl elem (formátum) WideEntries elem (formátum) WideEntry elem (formátum) WideItem elem (formátum) ScriptBlock eleme WideItem (formátum)</span><span class="sxs-lookup"><span data-stu-id="c21ab-104">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) WideControl Element (Format) WideEntries Element (Format) WideEntry Element (Format) WideItem Element (Format) ScriptBlock Element for WideItem (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="c21ab-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="c21ab-105">Syntax</span></span>

```xml
<ScriptBlock>ScriptToExecute</ScriptBlock>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="c21ab-106">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="c21ab-106">Attributes and Elements</span></span>

<span data-ttu-id="c21ab-107">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és szülőelemét a `ScriptBlock` elemet.</span><span class="sxs-lookup"><span data-stu-id="c21ab-107">The following sections describe the attributes, child elements, and parent element of the `ScriptBlock` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="c21ab-108">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="c21ab-108">Attributes</span></span>

<span data-ttu-id="c21ab-109">Nincs.</span><span class="sxs-lookup"><span data-stu-id="c21ab-109">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="c21ab-110">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="c21ab-110">Child Elements</span></span>

<span data-ttu-id="c21ab-111">Nincs.</span><span class="sxs-lookup"><span data-stu-id="c21ab-111">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="c21ab-112">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="c21ab-112">Parent Elements</span></span>

|<span data-ttu-id="c21ab-113">Elem</span><span class="sxs-lookup"><span data-stu-id="c21ab-113">Element</span></span>|<span data-ttu-id="c21ab-114">Leírás</span><span class="sxs-lookup"><span data-stu-id="c21ab-114">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="c21ab-115">WideItem elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="c21ab-115">WideItem Element (Format)</span></span>](./wideitem-element-for-widecontrol-format.md)|<span data-ttu-id="c21ab-116">Meghatározza a tulajdonság, vagy parancsprogram blokkot, amelynek az értéke az széles nézetben jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="c21ab-116">Defines the property or script block whose value is displayed in the wide view.</span></span>|

## <a name="text-value"></a><span data-ttu-id="c21ab-117">Szöveges érték</span><span class="sxs-lookup"><span data-stu-id="c21ab-117">Text Value</span></span>

<span data-ttu-id="c21ab-118">Adja meg a parancsfájl, amelynek értéke megjelenik.</span><span class="sxs-lookup"><span data-stu-id="c21ab-118">Specify the script whose value is displayed.</span></span>

## <a name="remarks"></a><span data-ttu-id="c21ab-119">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="c21ab-119">Remarks</span></span>

<span data-ttu-id="c21ab-120">Egy széles nézet az összetevőivel kapcsolatos további információkért lásd: [széles nézet létrehozásával](./creating-a-wide-view.md).</span><span class="sxs-lookup"><span data-stu-id="c21ab-120">For more information about the components of a wide view, see [Creating a Wide View](./creating-a-wide-view.md).</span></span>

## <a name="example"></a><span data-ttu-id="c21ab-121">Példa</span><span class="sxs-lookup"><span data-stu-id="c21ab-121">Example</span></span>

<span data-ttu-id="c21ab-122">Ez a példa bemutatja egy `WideItem` elem, amely meghatározza egy parancsfájlt, amelynek értéke megjelenik a nézetben.</span><span class="sxs-lookup"><span data-stu-id="c21ab-122">This example shows a `WideItem` element that defines a script whose value is displayed in the view.</span></span>

```xml
<WideItem>
  <ScriptBlock>ScriptToExecute</ScriptBlock>
</WideItem>
```

## <a name="see-also"></a><span data-ttu-id="c21ab-123">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="c21ab-123">See Also</span></span>

[<span data-ttu-id="c21ab-124">WideItem elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="c21ab-124">WideItem Element (Format)</span></span>](./wideitem-element-for-widecontrol-format.md)

[<span data-ttu-id="c21ab-125">Egy széles nézet létrehozása</span><span class="sxs-lookup"><span data-stu-id="c21ab-125">Creating a Wide View</span></span>](./creating-a-wide-view.md)

[<span data-ttu-id="c21ab-126">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="c21ab-126">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
