---
title: Listaelem ListControl (formátum) a PropertyName eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 01ae8cbe-acdc-4043-bd6e-1118a5691a55
caps.latest.revision: 12
ms.openlocfilehash: 405184f7bdbf1955f1df7766bf2723c244dcc27f
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62064917"
---
# <a name="propertyname-element-for-listitem-for-listcontrol-format"></a><span data-ttu-id="0fc8a-102">A ListControl elemhez tartozó ListItem PropertyName eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="0fc8a-102">PropertyName Element for ListItem for ListControl (Format)</span></span>

<span data-ttu-id="0fc8a-103">Megadja a .NET-tulajdonságot, amelynek értéke megjelenik a listában.</span><span class="sxs-lookup"><span data-stu-id="0fc8a-103">Specifies the .NET property whose value is displayed in the list.</span></span>

<span data-ttu-id="0fc8a-104">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézet elem (formátum) ListControl elem (formátum) ListEntries elem (formátum) ListEntry elem (formátum) ListItems elemek elem (formátum) ListItem elem (formátum) PropertyName elem számára Listaelem (formátum)</span><span class="sxs-lookup"><span data-stu-id="0fc8a-104">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) ListControl Element (Format) ListEntries Element (Format) ListEntry Element (Format) ListItems Element (Format) ListItem Element (Format) PropertyName Element for ListItem (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="0fc8a-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="0fc8a-105">Syntax</span></span>

```xml
<PropertyName>.NetTypeProperty</PropertyName>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="0fc8a-106">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="0fc8a-106">Attributes and Elements</span></span>

<span data-ttu-id="0fc8a-107">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `PropertyName` elemet.</span><span class="sxs-lookup"><span data-stu-id="0fc8a-107">The following sections describe the attributes, child elements, and the parent element of the `PropertyName` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="0fc8a-108">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="0fc8a-108">Attributes</span></span>

<span data-ttu-id="0fc8a-109">Nincs.</span><span class="sxs-lookup"><span data-stu-id="0fc8a-109">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="0fc8a-110">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="0fc8a-110">Child Elements</span></span>

<span data-ttu-id="0fc8a-111">Nincs.</span><span class="sxs-lookup"><span data-stu-id="0fc8a-111">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="0fc8a-112">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="0fc8a-112">Parent Elements</span></span>

|<span data-ttu-id="0fc8a-113">Elem</span><span class="sxs-lookup"><span data-stu-id="0fc8a-113">Element</span></span>|<span data-ttu-id="0fc8a-114">Leírás</span><span class="sxs-lookup"><span data-stu-id="0fc8a-114">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="0fc8a-115">Listaelem elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="0fc8a-115">ListItem Element (Format)</span></span>](./listitem-element-for-listitems-for-listcontrol-format.md)|<span data-ttu-id="0fc8a-116">A tulajdonság, vagy a parancsfájl, amelynek értéke megjelenik a lista nézet sorában határoz meg.</span><span class="sxs-lookup"><span data-stu-id="0fc8a-116">Defines the property or script whose value is displayed in the row of the list view.</span></span>|

## <a name="text-value"></a><span data-ttu-id="0fc8a-117">A szöveges érték</span><span class="sxs-lookup"><span data-stu-id="0fc8a-117">Text Value</span></span>

<span data-ttu-id="0fc8a-118">Adja meg, amelynek értéke megjelenik a tulajdonság nevét.</span><span class="sxs-lookup"><span data-stu-id="0fc8a-118">Specify the name of the property whose value is displayed.</span></span>

## <a name="remarks"></a><span data-ttu-id="0fc8a-119">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="0fc8a-119">Remarks</span></span>

<span data-ttu-id="0fc8a-120">Ha ez az elem meg van adva, nem adható meg a [ScriptBlock](./scriptblock-element-for-listitem-for-listcontrol-format.md) elemet.</span><span class="sxs-lookup"><span data-stu-id="0fc8a-120">When this element is specified, you cannot specify the [ScriptBlock](./scriptblock-element-for-listitem-for-listcontrol-format.md) element.</span></span>

<span data-ttu-id="0fc8a-121">Mellett megjelenítése a tulajdonság értéke, egy címke vagy egy formázó karakterlánc, amely segítségével a érték jelenjen meg az értéket is megadhatja.</span><span class="sxs-lookup"><span data-stu-id="0fc8a-121">In addition to displaying the property value, you can also specify a label for the value or a format string that can be used to change the display of the value.</span></span> <span data-ttu-id="0fc8a-122">Lista nézetben adatok megadásával kapcsolatos további információkért lásd: [lista nézet létrehozásával](./creating-a-list-view.md).</span><span class="sxs-lookup"><span data-stu-id="0fc8a-122">For more information about specifying data in a list view, see [Creating a List View](./creating-a-list-view.md).</span></span>

## <a name="example"></a><span data-ttu-id="0fc8a-123">Példa</span><span class="sxs-lookup"><span data-stu-id="0fc8a-123">Example</span></span>

<span data-ttu-id="0fc8a-124">Az alábbi példa bemutatja, hogyan adhatja meg a címke és a tulajdonságot, amelynek értéke megjelenik.</span><span class="sxs-lookup"><span data-stu-id="0fc8a-124">The following example shows how to specify the label and property whose value is displayed.</span></span>

```xml
ListItem>
  <Label>NameOfProperty</Label>
  <PropertyName>.NetTypeProperty</PropertyName>
</ListItem>

```

## <a name="see-also"></a><span data-ttu-id="0fc8a-125">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="0fc8a-125">See Also</span></span>

[<span data-ttu-id="0fc8a-126">Listaelem ListControl (formátum) a scriptblock kulcsszót elem.</span><span class="sxs-lookup"><span data-stu-id="0fc8a-126">ScriptBlock Element for ListItem for ListControl (Format)</span></span>](./scriptblock-element-for-listitem-for-listcontrol-format.md)

[<span data-ttu-id="0fc8a-127">Lista nézet létrehozása</span><span class="sxs-lookup"><span data-stu-id="0fc8a-127">Creating a List View</span></span>](./creating-a-list-view.md)

[<span data-ttu-id="0fc8a-128">ListControl(Format) ListItem elem.</span><span class="sxs-lookup"><span data-stu-id="0fc8a-128">ListItem Element for ListControl(Format)</span></span>](./listitem-element-for-listitems-for-listcontrol-format.md)

[<span data-ttu-id="0fc8a-129">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="0fc8a-129">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
