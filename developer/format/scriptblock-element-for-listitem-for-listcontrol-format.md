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
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62064577"
---
# <a name="scriptblock-element-for-listitem-for-listcontrol-format"></a><span data-ttu-id="77ad6-102">A ListControl elemhez tartozó ListItem ScriptBlock eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="77ad6-102">ScriptBlock Element for ListItem for ListControl (Format)</span></span>

<span data-ttu-id="77ad6-103">Megadja a parancsprogramot, amelynek értéke megjelenik a sorban.</span><span class="sxs-lookup"><span data-stu-id="77ad6-103">Specifies the script whose value is displayed in the row.</span></span>

<span data-ttu-id="77ad6-104">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézet elem (formátum) ListControl elem (formátum) ListEntries eleme ListEntries ListControl (formátum) ListItems elemek elemhez tartozó ListEntry ListEntry eleme ListControl (formátum) a ListItems elemek ListControl (formátum) ScriptBlock elemhez tartozó ListItem ListControl (formátum) a ListControl (formátum) ListItem elemhez</span><span class="sxs-lookup"><span data-stu-id="77ad6-104">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) ListControl Element (Format) ListEntries Element for ListControl (Format) ListEntry Element for ListEntries for ListControl (Format) ListItems Element for ListEntry for ListControl (Format) ListItem Element for ListItems for ListControl (Format) ScriptBlock Element for ListItem for ListControl (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="77ad6-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="77ad6-105">Syntax</span></span>

```xml
<ScriptBlock>ScriptToEvaluate</ScriptBlock>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="77ad6-106">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="77ad6-106">Attributes and Elements</span></span>

<span data-ttu-id="77ad6-107">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `ScriptBlock` elemet.</span><span class="sxs-lookup"><span data-stu-id="77ad6-107">The following sections describe the attributes, child elements, and the parent element of the `ScriptBlock` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="77ad6-108">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="77ad6-108">Attributes</span></span>

<span data-ttu-id="77ad6-109">Nincs.</span><span class="sxs-lookup"><span data-stu-id="77ad6-109">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="77ad6-110">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="77ad6-110">Child Elements</span></span>

<span data-ttu-id="77ad6-111">Nincs.</span><span class="sxs-lookup"><span data-stu-id="77ad6-111">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="77ad6-112">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="77ad6-112">Parent Elements</span></span>

|<span data-ttu-id="77ad6-113">Elem</span><span class="sxs-lookup"><span data-stu-id="77ad6-113">Element</span></span>|<span data-ttu-id="77ad6-114">Leírás</span><span class="sxs-lookup"><span data-stu-id="77ad6-114">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="77ad6-115">Listaelem elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="77ad6-115">ListItem Element (Format)</span></span>](./listitem-element-for-listitems-for-listcontrol-format.md)|<span data-ttu-id="77ad6-116">A tulajdonság, vagy a parancsfájl, amelynek értéke megjelenik a lista nézet sorában lévő határoz meg.</span><span class="sxs-lookup"><span data-stu-id="77ad6-116">Defines the property or script whose value is displayed in a row of the list view.</span></span>|

## <a name="text-value"></a><span data-ttu-id="77ad6-117">A szöveges érték</span><span class="sxs-lookup"><span data-stu-id="77ad6-117">Text Value</span></span>

<span data-ttu-id="77ad6-118">Adja meg a parancsfájl, amelynek értéke megjelenik a sorban.</span><span class="sxs-lookup"><span data-stu-id="77ad6-118">Specify the script whose value is displayed in the row.</span></span>

## <a name="remarks"></a><span data-ttu-id="77ad6-119">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="77ad6-119">Remarks</span></span>

<span data-ttu-id="77ad6-120">Ha ez az elem meg van adva, nem adható meg a [PropertyName](./propertyname-element-for-listitem-for-listcontrol-format.md) elemet.</span><span class="sxs-lookup"><span data-stu-id="77ad6-120">When this element is specified, you cannot specify the [PropertyName](./propertyname-element-for-listitem-for-listcontrol-format.md) element.</span></span>

<span data-ttu-id="77ad6-121">Lista nézetben parancsfájlok megadásával kapcsolatos további információkért lásd: [listanézet](./creating-a-list-view.md).</span><span class="sxs-lookup"><span data-stu-id="77ad6-121">For more information about specifying scripts in a list view, see [List View](./creating-a-list-view.md).</span></span>

## <a name="example"></a><span data-ttu-id="77ad6-122">Példa</span><span class="sxs-lookup"><span data-stu-id="77ad6-122">Example</span></span>

<span data-ttu-id="77ad6-123">Az alábbi példa bemutatja, hogyan adja meg a tulajdonságot, amelynek értéke megjelenik.</span><span class="sxs-lookup"><span data-stu-id="77ad6-123">The following example shows how to specify the property whose value is displayed.</span></span>

```xml
<ListItem>
  <ScriptBlock>$_.ProcessName + ":" $_.Id</ScriptBlock>
</ListItem>

```

## <a name="see-also"></a><span data-ttu-id="77ad6-124">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="77ad6-124">See Also</span></span>

[<span data-ttu-id="77ad6-125">Listaelem ListControl (formátum) a PropertyName elem.</span><span class="sxs-lookup"><span data-stu-id="77ad6-125">PropertyName Element for ListItem for ListControl (Format)</span></span>](./propertyname-element-for-listitem-for-listcontrol-format.md)

[<span data-ttu-id="77ad6-126">Lista nézet létrehozása</span><span class="sxs-lookup"><span data-stu-id="77ad6-126">Creating a List View</span></span>](./creating-a-list-view.md)

[<span data-ttu-id="77ad6-127">A ListControl (formátum) ListItems elemek ListItem elem.</span><span class="sxs-lookup"><span data-stu-id="77ad6-127">ListItem Element for ListItems for ListControl (Format)</span></span>](./listitem-element-for-listitems-for-listcontrol-format.md)

[<span data-ttu-id="77ad6-128">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="77ad6-128">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
