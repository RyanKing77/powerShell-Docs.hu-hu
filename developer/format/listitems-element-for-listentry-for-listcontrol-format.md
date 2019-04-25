---
title: A ListControl (formátum) ListEntry ListItems elemek eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: d2c1da6d-acc7-4fe8-9e7d-6dcddc2787cd
caps.latest.revision: 9
ms.openlocfilehash: c25f18489d9c7abd8889758499dbbacd6ee29304
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62065240"
---
# <a name="listitems-element-for-listentry-for-listcontrol-format"></a><span data-ttu-id="0945f-102">A ListControl elemhez tartozó ListEntry ListItems eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="0945f-102">ListItems Element for ListEntry for ListControl (Format)</span></span>

<span data-ttu-id="0945f-103">A tulajdonságok és a parancsfájlok, melynek értékei jelennek meg a lista nézet sorainak határoz meg.</span><span class="sxs-lookup"><span data-stu-id="0945f-103">Defines the properties and scripts whose values are displayed in the rows of the list view.</span></span>

<span data-ttu-id="0945f-104">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem ListControl elem (formátum) ListEntries elem a lista vezérlőelem (formátum) ListEntry elem ListControl (formátum) ListItems elemek elemhez tartozó ListControl (formátum)</span><span class="sxs-lookup"><span data-stu-id="0945f-104">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) ListControl Element (Format) ListEntries Element for List Control (Format) ListEntry Element for ListControl (Format) ListItems Element for ListControl (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="0945f-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="0945f-105">Syntax</span></span>

```xml
<ListItems>
  <ListItem>...</ListItem>
</ListItems>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="0945f-106">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="0945f-106">Attributes and Elements</span></span>

<span data-ttu-id="0945f-107">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és szülőelemét a `ListItems` elemet.</span><span class="sxs-lookup"><span data-stu-id="0945f-107">The following sections describe the attributes, child elements, and parent element of the `ListItems` element.</span></span> <span data-ttu-id="0945f-108">Nincs nem adható meg az alárendelt elemek száma nincs korlátozva.</span><span class="sxs-lookup"><span data-stu-id="0945f-108">There is no limit to the number of child elements that can be specified.</span></span> <span data-ttu-id="0945f-109">Az alárendelt összetevők sorrendje határozza meg, hogy a listanézetet jelennek meg a értékei sorrendben.</span><span class="sxs-lookup"><span data-stu-id="0945f-109">The order of the child elements defines the order that values are displayed in the list view.</span></span>

### <a name="attributes"></a><span data-ttu-id="0945f-110">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="0945f-110">Attributes</span></span>

<span data-ttu-id="0945f-111">Nincs.</span><span class="sxs-lookup"><span data-stu-id="0945f-111">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="0945f-112">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="0945f-112">Child Elements</span></span>

|<span data-ttu-id="0945f-113">Elem</span><span class="sxs-lookup"><span data-stu-id="0945f-113">Element</span></span>|<span data-ttu-id="0945f-114">Leírás</span><span class="sxs-lookup"><span data-stu-id="0945f-114">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="0945f-115">Listaelem eleme ListControl (formátum)</span><span class="sxs-lookup"><span data-stu-id="0945f-115">ListItem Element for ListControl (Format)</span></span>](./listitem-element-for-listitems-for-listcontrol-format.md)|<span data-ttu-id="0945f-116">Szükséges eleme.</span><span class="sxs-lookup"><span data-stu-id="0945f-116">Required element.</span></span><br /><br /> <span data-ttu-id="0945f-117">A tulajdonság vagy parancsfájl, amelynek értéke megjelenik a lista nézet szerint határozza meg.</span><span class="sxs-lookup"><span data-stu-id="0945f-117">Defines the property or script whose value is displayed by the list view.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="0945f-118">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="0945f-118">Parent Elements</span></span>

|<span data-ttu-id="0945f-119">Elem</span><span class="sxs-lookup"><span data-stu-id="0945f-119">Element</span></span>|<span data-ttu-id="0945f-120">Leírás</span><span class="sxs-lookup"><span data-stu-id="0945f-120">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="0945f-121">ListEntry eleme ListControl (formátum)</span><span class="sxs-lookup"><span data-stu-id="0945f-121">ListEntry Element for ListControl (Format)</span></span>](./listentry-element-for-listcontrol-format.md)|<span data-ttu-id="0945f-122">A lista nézet definíciójának biztosít.</span><span class="sxs-lookup"><span data-stu-id="0945f-122">Provides a definition of the list view.</span></span>|

## <a name="remarks"></a><span data-ttu-id="0945f-123">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="0945f-123">Remarks</span></span>

<span data-ttu-id="0945f-124">Az ilyen típusú nézet kapcsolatos további információkért lásd: [lista nézet létrehozásával](./creating-a-list-view.md).</span><span class="sxs-lookup"><span data-stu-id="0945f-124">For more information about this type of view, see [Creating a List View](./creating-a-list-view.md).</span></span>

## <a name="example"></a><span data-ttu-id="0945f-125">Példa</span><span class="sxs-lookup"><span data-stu-id="0945f-125">Example</span></span>

<span data-ttu-id="0945f-126">Ez a példa bemutatja az XML-elemeket, amelyek meghatározzák a listanézet három sort.</span><span class="sxs-lookup"><span data-stu-id="0945f-126">This example shows the XML elements that define three rows of the list view.</span></span>

```xml
<ListEntry>
    <ListItems>
      <ListItem>
        <Label>Property1: </Label>
        <PropertyName>.NetTypeProperty1</PropertyName>
      </ListItem>
      <ListItem>
        <PropertyName>.NetTypeProperty2</PropertyName>
      </ListItem>
      <ListItem>
        <ScriptBlock>$_.ProcessName + ":" $_.Id</ScriptBlock>
      </ListItem>
  </ListEntry>
```

## <a name="see-also"></a><span data-ttu-id="0945f-127">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="0945f-127">See Also</span></span>

[<span data-ttu-id="0945f-128">ListEntry eleme ListControl (formátum)</span><span class="sxs-lookup"><span data-stu-id="0945f-128">ListEntry Element for ListControl (Format)</span></span>](./listentry-element-for-listcontrol-format.md)

[<span data-ttu-id="0945f-129">Listaelem eleme ListControl (formátum)</span><span class="sxs-lookup"><span data-stu-id="0945f-129">ListItem Element for ListControl (Format)</span></span>](./listitem-element-for-listitems-for-listcontrol-format.md)

[<span data-ttu-id="0945f-130">Lista nézet létrehozása</span><span class="sxs-lookup"><span data-stu-id="0945f-130">Creating a List View</span></span>](./creating-a-list-view.md)

[<span data-ttu-id="0945f-131">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="0945f-131">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
