---
title: Listaelem ListControl (formátum) a scriptblock kulcsszót eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 74e30938-00ef-46fd-84e5-f0a83706a50e
caps.latest.revision: 11
ms.openlocfilehash: 76b600256af3f957f7fe0578f9fef810262aa5d5
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56846500"
---
# <a name="scriptblock-element-for-listitem-for-listcontrol-format"></a><span data-ttu-id="5f614-102">A ListControl elemhez tartozó ListItem ScriptBlock eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="5f614-102">ScriptBlock Element for ListItem for ListControl (Format)</span></span>

<span data-ttu-id="5f614-103">Megadja a parancsprogramot, amelynek értéke megjelenik a sorban.</span><span class="sxs-lookup"><span data-stu-id="5f614-103">Specifies the script whose value is displayed in the row.</span></span>

<span data-ttu-id="5f614-104">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézet elem (formátum) ListControl elem (formátum) ListEntries eleme ListEntries ListControl (formátum) ListItems elemek elemhez tartozó ListEntry ListEntry eleme ListControl (formátum) a ListItems elemek ListControl (formátum) ScriptBlock elemhez tartozó ListItem ListControl (formátum) a ListControl (formátum) ListItem elemhez</span><span class="sxs-lookup"><span data-stu-id="5f614-104">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) ListControl Element (Format) ListEntries Element for ListControl (Format) ListEntry Element for ListEntries for ListControl (Format) ListItems Element for ListEntry for ListControl (Format) ListItem Element for ListItems for ListControl (Format) ScriptBlock Element for ListItem for ListControl (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="5f614-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="5f614-105">Syntax</span></span>

```xml
<ScriptBlock>ScriptToEvaluate</ScriptBlock>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="5f614-106">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="5f614-106">Attributes and Elements</span></span>

<span data-ttu-id="5f614-107">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `ScriptBlock` elemet.</span><span class="sxs-lookup"><span data-stu-id="5f614-107">The following sections describe the attributes, child elements, and the parent element of the `ScriptBlock` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="5f614-108">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="5f614-108">Attributes</span></span>

<span data-ttu-id="5f614-109">Nincs.</span><span class="sxs-lookup"><span data-stu-id="5f614-109">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="5f614-110">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="5f614-110">Child Elements</span></span>

<span data-ttu-id="5f614-111">Nincs.</span><span class="sxs-lookup"><span data-stu-id="5f614-111">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="5f614-112">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="5f614-112">Parent Elements</span></span>

|<span data-ttu-id="5f614-113">Elem</span><span class="sxs-lookup"><span data-stu-id="5f614-113">Element</span></span>|<span data-ttu-id="5f614-114">Leírás</span><span class="sxs-lookup"><span data-stu-id="5f614-114">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="5f614-115">Listaelem elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="5f614-115">ListItem Element (Format)</span></span>](./listitem-element-for-listitems-for-listcontrol-format.md)|<span data-ttu-id="5f614-116">A tulajdonság, vagy a parancsfájl, amelynek értéke megjelenik a lista nézet sorában lévő határoz meg.</span><span class="sxs-lookup"><span data-stu-id="5f614-116">Defines the property or script whose value is displayed in a row of the list view.</span></span>|

## <a name="text-value"></a><span data-ttu-id="5f614-117">Szöveges érték</span><span class="sxs-lookup"><span data-stu-id="5f614-117">Text Value</span></span>

<span data-ttu-id="5f614-118">Adja meg a parancsfájl, amelynek értéke megjelenik a sorban.</span><span class="sxs-lookup"><span data-stu-id="5f614-118">Specify the script whose value is displayed in the row.</span></span>

## <a name="remarks"></a><span data-ttu-id="5f614-119">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="5f614-119">Remarks</span></span>

<span data-ttu-id="5f614-120">Ha ez az elem meg van adva, nem adható meg a [PropertyName](./propertyname-element-for-listitem-for-listcontrol-format.md) elemet.</span><span class="sxs-lookup"><span data-stu-id="5f614-120">When this element is specified, you cannot specify the [PropertyName](./propertyname-element-for-listitem-for-listcontrol-format.md) element.</span></span>

<span data-ttu-id="5f614-121">Lista nézetben parancsfájlok megadásával kapcsolatos további információkért lásd: [listanézet](./creating-a-list-view.md).</span><span class="sxs-lookup"><span data-stu-id="5f614-121">For more information about specifying scripts in a list view, see [List View](./creating-a-list-view.md).</span></span>

## <a name="example"></a><span data-ttu-id="5f614-122">Példa</span><span class="sxs-lookup"><span data-stu-id="5f614-122">Example</span></span>

<span data-ttu-id="5f614-123">Az alábbi példa bemutatja, hogyan adja meg a tulajdonságot, amelynek értéke megjelenik.</span><span class="sxs-lookup"><span data-stu-id="5f614-123">The following example shows how to specify the property whose value is displayed.</span></span>

```xml
<ListItem>
  <ScriptBlock>$_.ProcessName + ":" $_.Id</ScriptBlock>
</ListItem>

```

## <a name="see-also"></a><span data-ttu-id="5f614-124">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="5f614-124">See Also</span></span>

[<span data-ttu-id="5f614-125">Listaelem ListControl (formátum) a PropertyName elem.</span><span class="sxs-lookup"><span data-stu-id="5f614-125">PropertyName Element for ListItem for ListControl (Format)</span></span>](./propertyname-element-for-listitem-for-listcontrol-format.md)

[<span data-ttu-id="5f614-126">Lista nézet létrehozása</span><span class="sxs-lookup"><span data-stu-id="5f614-126">Creating a List View</span></span>](./creating-a-list-view.md)

[<span data-ttu-id="5f614-127">A ListControl (formátum) ListItems elemek ListItem elem.</span><span class="sxs-lookup"><span data-stu-id="5f614-127">ListItem Element for ListItems for ListControl (Format)</span></span>](./listitem-element-for-listitems-for-listcontrol-format.md)

[<span data-ttu-id="5f614-128">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="5f614-128">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
