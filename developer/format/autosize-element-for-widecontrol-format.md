---
title: Automatikus méretezés eleme WideControl (formátum) |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: def37479-7b6e-40cf-bc81-0f7cbc651b31
caps.latest.revision: 11
ms.openlocfilehash: 6dbaef5886a0600bd9fe96dbc8d21f00a674dfcf
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56847571"
---
# <a name="autosize-element-for-widecontrol-format"></a><span data-ttu-id="04c69-102">A WideControl AutoSize eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="04c69-102">AutoSize Element for WideControl (Format)</span></span>

<span data-ttu-id="04c69-103">Itt adhatja meg, hogy az oszlop méretét és az oszlopok számát módosulnak az adatok mérete alapján.</span><span class="sxs-lookup"><span data-stu-id="04c69-103">Specifies whether the column size and the number of columns are adjusted based on the size of the data.</span></span>

<span data-ttu-id="04c69-104">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem WideControl elem (formátum) Autosize eleme WideControl (formátum)</span><span class="sxs-lookup"><span data-stu-id="04c69-104">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) WideControl Element (Format) Autosize Element for WideControl (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="04c69-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="04c69-105">Syntax</span></span>

```xml
<AutoSize/>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="04c69-106">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="04c69-106">Attributes and Elements</span></span>

<span data-ttu-id="04c69-107">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `AutoSize` elemet.</span><span class="sxs-lookup"><span data-stu-id="04c69-107">The following sections describe attributes, child elements, and the parent element of the `AutoSize` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="04c69-108">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="04c69-108">Attributes</span></span>

<span data-ttu-id="04c69-109">Nincs.</span><span class="sxs-lookup"><span data-stu-id="04c69-109">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="04c69-110">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="04c69-110">Child Elements</span></span>

<span data-ttu-id="04c69-111">Egyik sem</span><span class="sxs-lookup"><span data-stu-id="04c69-111">None</span></span>

### <a name="parent-elements"></a><span data-ttu-id="04c69-112">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="04c69-112">Parent Elements</span></span>

|<span data-ttu-id="04c69-113">Elem</span><span class="sxs-lookup"><span data-stu-id="04c69-113">Element</span></span>|<span data-ttu-id="04c69-114">Leírás</span><span class="sxs-lookup"><span data-stu-id="04c69-114">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="04c69-115">WideControl elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="04c69-115">WideControl Element (Format)</span></span>](./widecontrol-element-format.md)|<span data-ttu-id="04c69-116">A wide (egyetlen érték) határozza meg a Nézet formátuma.</span><span class="sxs-lookup"><span data-stu-id="04c69-116">Defines a wide (single value) list format for the view.</span></span>|

## <a name="remarks"></a><span data-ttu-id="04c69-117">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="04c69-117">Remarks</span></span>

<span data-ttu-id="04c69-118">Egy széles nézet meghatározásakor adhat hozzá a `AutoSize` elem vagy a [ColumnNumber](./columnnumber-element-for-widecontrol-format.md) elem, de mindkettő nem adható hozzá.</span><span class="sxs-lookup"><span data-stu-id="04c69-118">When defining a wide view, you can add the `AutoSize` element or the [ColumnNumber](./columnnumber-element-for-widecontrol-format.md) element, but you cannot add both.</span></span>

<span data-ttu-id="04c69-119">Egy széles nézet az összetevőivel kapcsolatos további információkért lásd: [széles nézet létrehozásával](./creating-a-wide-view.md).</span><span class="sxs-lookup"><span data-stu-id="04c69-119">For more information about the components of a wide view, see [Creating a Wide View](./creating-a-wide-view.md).</span></span>

<span data-ttu-id="04c69-120">Egy széles nézet egy példa: [széles nézet (alapszintű)](./wide-view-basic.md).</span><span class="sxs-lookup"><span data-stu-id="04c69-120">For an example of a wide view, see [Wide View (Basic)](./wide-view-basic.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="04c69-121">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="04c69-121">See Also</span></span>

[<span data-ttu-id="04c69-122">ColumnNumber eleme WideControl (formátum)</span><span class="sxs-lookup"><span data-stu-id="04c69-122">ColumnNumber Element for WideControl (Format)</span></span>](./columnnumber-element-for-widecontrol-format.md)

[<span data-ttu-id="04c69-123">Egy széles nézet létrehozása</span><span class="sxs-lookup"><span data-stu-id="04c69-123">Creating a Wide View</span></span>](./creating-a-wide-view.md)

[<span data-ttu-id="04c69-124">WideControl elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="04c69-124">WideControl Element (Format)</span></span>](./widecontrol-element-format.md)

[<span data-ttu-id="04c69-125">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="04c69-125">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
