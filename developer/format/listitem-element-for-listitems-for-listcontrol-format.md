---
title: ListControl (formátum) a ListItems elemek ListItem eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 0f96f4f5-8bd5-43ed-95e7-a7358115999a
caps.latest.revision: 11
ms.openlocfilehash: 1e0a1b2d20853650328b8cfd1513a08f7e167cd6
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62065767"
---
# <a name="listitem-element-for-listitems-for-listcontrol-format"></a><span data-ttu-id="4a5cc-102">A ListControl elemhez tartozó ListItems ListItem eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="4a5cc-102">ListItem Element for ListItems for ListControl (Format)</span></span>

<span data-ttu-id="4a5cc-103">A tulajdonság, vagy a parancsfájl, amelynek értéke megjelenik a lista nézet sorában lévő határoz meg.</span><span class="sxs-lookup"><span data-stu-id="4a5cc-103">Defines the property or script whose value is displayed in a row of the list view.</span></span>

<span data-ttu-id="4a5cc-104">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem ListControl elem (formátum) ListEntries elem ListControl (formátum) ListEntry elem ListControl (formátum) ListItems elemek elemhez tartozó ListControl (formátum) Listaelem ListControl elemhez (formátum)</span><span class="sxs-lookup"><span data-stu-id="4a5cc-104">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) ListControl Element (Format) ListEntries Element for ListControl (Format) ListEntry Element for ListControl (Format) ListItems Element for ListControl (Format) ListItem for ListControl Element (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="4a5cc-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="4a5cc-105">Syntax</span></span>

```xml
<ListItem>
  <PropertyName>PropertyToDisplay</PropertyName>
  <ScriptBlock>ScriptToExecute</ScriptBlock>
  <Label>LabelToDisplay</Label>
  <FormatString>FormatPattern</FormatString>
  <ItemSelectionCondition>...</ItemSelectionCondition>
</ListItem>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="4a5cc-106">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="4a5cc-106">Attributes and Elements</span></span>

<span data-ttu-id="4a5cc-107">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és szülőelemét a `ListItem` elemet.</span><span class="sxs-lookup"><span data-stu-id="4a5cc-107">The following sections describe the attributes, child elements, and parent element of the `ListItem` element.</span></span> <span data-ttu-id="4a5cc-108">Csak egy tulajdonságot vagy parancsfájl adható meg.</span><span class="sxs-lookup"><span data-stu-id="4a5cc-108">Only one property or script can be specified.</span></span>

### <a name="attributes"></a><span data-ttu-id="4a5cc-109">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="4a5cc-109">Attributes</span></span>

<span data-ttu-id="4a5cc-110">Egyik sem</span><span class="sxs-lookup"><span data-stu-id="4a5cc-110">None</span></span>

### <a name="child-elements"></a><span data-ttu-id="4a5cc-111">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="4a5cc-111">Child Elements</span></span>

|<span data-ttu-id="4a5cc-112">Elem</span><span class="sxs-lookup"><span data-stu-id="4a5cc-112">Element</span></span>|<span data-ttu-id="4a5cc-113">Leírás</span><span class="sxs-lookup"><span data-stu-id="4a5cc-113">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="4a5cc-114">Listaelem ListControl (formátum) a FormatString elem.</span><span class="sxs-lookup"><span data-stu-id="4a5cc-114">FormatString Element for ListItem for ListControl (Format)</span></span>](./formatstring-element-for-listitem-for-listcontrol-format.md)|<span data-ttu-id="4a5cc-115">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="4a5cc-115">Optional element.</span></span><br /><br /> <span data-ttu-id="4a5cc-116">Megadja egy formázó karakterlánc, amely meghatározza, hogy a tulajdonság vagy parancsfájl érték hogyan jelenjen meg.</span><span class="sxs-lookup"><span data-stu-id="4a5cc-116">Specifies a format string that defines how the property or script value is displayed.</span></span>|
|[<span data-ttu-id="4a5cc-117">A ListControl (formátum) ListItem ItemSelectionCondition eleme</span><span class="sxs-lookup"><span data-stu-id="4a5cc-117">ItemSelectionCondition Element for ListItem for ListControl (Format)</span></span>](./itemselectioncondition-element-for-listitem-for-listcontrol-format.md)|<span data-ttu-id="4a5cc-118">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="4a5cc-118">Optional element.</span></span><br /><br /> <span data-ttu-id="4a5cc-119">Határozza meg azt a feltételt, amelyet a listaelem használandó léteznie kell.</span><span class="sxs-lookup"><span data-stu-id="4a5cc-119">Defines the condition that must exist for this list item to be used.</span></span>|
|[<span data-ttu-id="4a5cc-120">Listaelem ListControl (formátum) a címke elem.</span><span class="sxs-lookup"><span data-stu-id="4a5cc-120">Label Element for ListItem for ListControl (Format)</span></span>](./label-element-for-listitem-for-listcontrol-format.md)|<span data-ttu-id="4a5cc-121">Választható elem</span><span class="sxs-lookup"><span data-stu-id="4a5cc-121">Optional element</span></span><br /><br /> <span data-ttu-id="4a5cc-122">Adja meg a címke bal oldalán a tulajdonság, vagy parancsprogram érték sorában megjelenik.</span><span class="sxs-lookup"><span data-stu-id="4a5cc-122">Specifies the label that is displayed to the left of the property or script value in the row.</span></span>|
|[<span data-ttu-id="4a5cc-123">Listaelem ListControl (formátum) a PropertyName elem.</span><span class="sxs-lookup"><span data-stu-id="4a5cc-123">PropertyName Element for ListItem for ListControl (Format)</span></span>](./propertyname-element-for-listitem-for-listcontrol-format.md)|<span data-ttu-id="4a5cc-124">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="4a5cc-124">Optional element.</span></span><br /><br /> <span data-ttu-id="4a5cc-125">Adja meg azt a .NET tulajdonságot, amelynek értéke megjelenik a sorban.</span><span class="sxs-lookup"><span data-stu-id="4a5cc-125">Specifies the .NET property whose value is displayed in the row.</span></span>|
|[<span data-ttu-id="4a5cc-126">Listaelem ListControl (formátum) a scriptblock kulcsszót elem.</span><span class="sxs-lookup"><span data-stu-id="4a5cc-126">ScriptBlock Element for ListItem for ListControl (Format)</span></span>](./scriptblock-element-for-listitem-for-listcontrol-format.md)|<span data-ttu-id="4a5cc-127">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="4a5cc-127">Optional element.</span></span><br /><br /> <span data-ttu-id="4a5cc-128">Megadja a parancsprogramot, amelynek értéke megjelenik a sorban.</span><span class="sxs-lookup"><span data-stu-id="4a5cc-128">Specifies the script whose value is displayed in the row.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="4a5cc-129">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="4a5cc-129">Parent Elements</span></span>

|<span data-ttu-id="4a5cc-130">Elem</span><span class="sxs-lookup"><span data-stu-id="4a5cc-130">Element</span></span>|<span data-ttu-id="4a5cc-131">Leírás</span><span class="sxs-lookup"><span data-stu-id="4a5cc-131">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="4a5cc-132">ListItems elemek elem a lista vezérlőelem (formátum)</span><span class="sxs-lookup"><span data-stu-id="4a5cc-132">ListItems Element for List Control (Format)</span></span>](./listitems-element-for-listentry-for-listcontrol-format.md)|<span data-ttu-id="4a5cc-133">Meghatározza a tulajdonságok és a parancsfájlok, melynek értékei jelennek meg a listanézetben.</span><span class="sxs-lookup"><span data-stu-id="4a5cc-133">Defines the properties and scripts whose values are displayed in the list view.</span></span>|

## <a name="remarks"></a><span data-ttu-id="4a5cc-134">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="4a5cc-134">Remarks</span></span>

<span data-ttu-id="4a5cc-135">Megjelenítheti az összetevőivel kapcsolatos további információk: [lista nézet létrehozásával](./creating-a-list-view.md).</span><span class="sxs-lookup"><span data-stu-id="4a5cc-135">For more information about the components of a list view, see [Creating a List View](./creating-a-list-view.md).</span></span>

## <a name="example"></a><span data-ttu-id="4a5cc-136">Példa</span><span class="sxs-lookup"><span data-stu-id="4a5cc-136">Example</span></span>

<span data-ttu-id="4a5cc-137">Ez a példa bemutatja az XML-elemeket, amelyek meghatározzák a listanézet három sort.</span><span class="sxs-lookup"><span data-stu-id="4a5cc-137">This example shows the XML elements that define three rows of the list view.</span></span> <span data-ttu-id="4a5cc-138">Az első két sort a .NET-tulajdonság értéket jeleníti meg, és az utolsó sort a szkript által létrehozott értéket jeleníti meg.</span><span class="sxs-lookup"><span data-stu-id="4a5cc-138">The first two rows display the value of a .NET property, and the last row displays a value generated by a script.</span></span>

```xml
<ListEntry>
    <ListItems>
      <ListItem>
        <Label>Property1: </Label>
        <PropertyName>DotNetProperty1</PropertyName>
      </ListItem>
      <ListItem>
        <PropertyName>DotNetProperty2</PropertyName>
      </ListItem>
      <ListItem>
        <ScriptBlock>$_.ProcessName + ":" $_.Id</ScriptBlock>
      </ListItem>
    </ListItems>
</ListEntry>

```

## <a name="see-also"></a><span data-ttu-id="4a5cc-139">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="4a5cc-139">See Also</span></span>

[<span data-ttu-id="4a5cc-140">ListItems elemek elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="4a5cc-140">ListItems Element (Format)</span></span>](./listitems-element-for-listentry-for-listcontrol-format.md)

[<span data-ttu-id="4a5cc-141">FormatString eleme ListItem (formátum)</span><span class="sxs-lookup"><span data-stu-id="4a5cc-141">FormatString Element for ListItem (Format)</span></span>](./formatstring-element-for-listitem-for-listcontrol-format.md)

[<span data-ttu-id="4a5cc-142">Címke eleme ListItem (formátum)</span><span class="sxs-lookup"><span data-stu-id="4a5cc-142">Label Element for ListItem (Format)</span></span>](./label-element-for-listitem-for-listcontrol-format.md)

[<span data-ttu-id="4a5cc-143">A PropertyName eleme ListItem (formátum)</span><span class="sxs-lookup"><span data-stu-id="4a5cc-143">PropertyName Element for ListItem (Format)</span></span>](./propertyname-element-for-listitem-for-listcontrol-format.md)

[<span data-ttu-id="4a5cc-144">ScriptBlock eleme ListItem (formátum)</span><span class="sxs-lookup"><span data-stu-id="4a5cc-144">ScriptBlock Element for ListItem (Format)</span></span>](./scriptblock-element-for-listitem-for-listcontrol-format.md)

[<span data-ttu-id="4a5cc-145">Lista nézet létrehozása</span><span class="sxs-lookup"><span data-stu-id="4a5cc-145">Creating a List View</span></span>](./creating-a-list-view.md)

[<span data-ttu-id="4a5cc-146">Egy Windows PowerShell formázás és a fájl típusai</span><span class="sxs-lookup"><span data-stu-id="4a5cc-146">Writing a Windows PowerShell Formatting and Types File</span></span>](./writing-a-powershell-formatting-file.md)
