---
title: ListControl (formátum) a ListItem ItemSelectionCondition eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: d2668aea-37e9-4753-a4e9-7980ae5ec2eb
caps.latest.revision: 10
ms.openlocfilehash: 6bc0ccbcc5bd62429f63ed220da66dc66f44f7ca
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56850917"
---
# <a name="itemselectioncondition-element-for-listitem-for-listcontrol-format"></a><span data-ttu-id="34412-102">A ListControl elemhez tartozó ListItem ItemSelectionCondition eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="34412-102">ItemSelectionCondition Element for ListItem for ListControl (Format)</span></span>

<span data-ttu-id="34412-103">Határozza meg azt a feltételt, amelyet a listaelem használandó léteznie kell.</span><span class="sxs-lookup"><span data-stu-id="34412-103">Defines the condition that must exist for this list item to be used.</span></span>

<span data-ttu-id="34412-104">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézet elem (formátum) ListControl elem (formátum) ListEntries eleme ListEntries ListControl (formátum) ListItems elemek elemhez tartozó ListEntry ListEntry eleme ListControl (formátum) a ListItems elemek ListControl (formátum) ItemSelectionCondition elemhez tartozó ListItem ListControl (formátum) a ListControl (formátum) ListItem elemhez</span><span class="sxs-lookup"><span data-stu-id="34412-104">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) ListControl Element (Format) ListEntries Element for ListControl (Format) ListEntry Element for ListEntries for ListControl (Format) ListItems Element for ListEntry for ListControl (Format) ListItem Element for ListItems for ListControl (Format) ItemSelectionCondition Element for ListItem for ListControl (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="34412-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="34412-105">Syntax</span></span>

```xml
<ItemSelectionCondition>
  <PropertyName>.NetTypeProperty</PropertyName>
  <ScriptBlock>ScriptToEvaluate</ScriptBlock>
</ItemSelectionCondition>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="34412-106">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="34412-106">Attributes and Elements</span></span>

<span data-ttu-id="34412-107">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `ItemSelectionCondition` elemet.</span><span class="sxs-lookup"><span data-stu-id="34412-107">The following sections describe attributes, child elements, and the parent element of the `ItemSelectionCondition` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="34412-108">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="34412-108">Attributes</span></span>

<span data-ttu-id="34412-109">Nincs.</span><span class="sxs-lookup"><span data-stu-id="34412-109">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="34412-110">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="34412-110">Child Elements</span></span>

|<span data-ttu-id="34412-111">Elem</span><span class="sxs-lookup"><span data-stu-id="34412-111">Element</span></span>|<span data-ttu-id="34412-112">Leírás</span><span class="sxs-lookup"><span data-stu-id="34412-112">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="34412-113">ItemSelectionCondition ListControl (formátum) a PropertyName elem.</span><span class="sxs-lookup"><span data-stu-id="34412-113">PropertyName Element for ItemSelectionCondition for ListControl (Format)</span></span>](./propertyname-element-for-itemselectioncondition-for-listcontrol-format.md)|<span data-ttu-id="34412-114">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="34412-114">Optional element.</span></span><br /><br /> <span data-ttu-id="34412-115">Megadja a .NET-tulajdonság, amely elindítja a feltételt.</span><span class="sxs-lookup"><span data-stu-id="34412-115">Specifies the .NET property that triggers the condition.</span></span>|
|[<span data-ttu-id="34412-116">ItemSelectionCondition ListControl (formátum) a scriptblock kulcsszót elem.</span><span class="sxs-lookup"><span data-stu-id="34412-116">ScriptBlock Element for ItemSelectionCondition for ListControl (Format)</span></span>](./scriptblock-element-for-itemselectioncondition-for-listcontrol-format.md)|<span data-ttu-id="34412-117">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="34412-117">Optional element.</span></span><br /><br /> <span data-ttu-id="34412-118">Megadja a parancsprogramot, amely elindítja a feltétel.</span><span class="sxs-lookup"><span data-stu-id="34412-118">Specifies the script that triggers the condition.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="34412-119">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="34412-119">Parent Elements</span></span>

|<span data-ttu-id="34412-120">Elem</span><span class="sxs-lookup"><span data-stu-id="34412-120">Element</span></span>|<span data-ttu-id="34412-121">Leírás</span><span class="sxs-lookup"><span data-stu-id="34412-121">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="34412-122">A ListControl (formátum) ListItems elemek ListItem elem.</span><span class="sxs-lookup"><span data-stu-id="34412-122">ListItem Element for ListItems for ListControl (Format)</span></span>](./listitem-element-for-listitems-for-listcontrol-format.md)|<span data-ttu-id="34412-123">A tulajdonság, vagy a parancsfájl, amelynek értéke megjelenik a lista nézet sorában lévő határoz meg.</span><span class="sxs-lookup"><span data-stu-id="34412-123">Defines the property or script whose value is displayed in a row of the list view.</span></span>|

## <a name="remarks"></a><span data-ttu-id="34412-124">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="34412-124">Remarks</span></span>

<span data-ttu-id="34412-125">Egy tulajdonság neve vagy az ehhez a feltételhez parancsfájlt is megadhat, de nem adható meg egyszerre.</span><span class="sxs-lookup"><span data-stu-id="34412-125">You can specify one property name or a script for this condition but cannot specify both.</span></span>

## <a name="see-also"></a><span data-ttu-id="34412-126">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="34412-126">See Also</span></span>

[<span data-ttu-id="34412-127">A ListControl (formátum) ListItems elemek ListItem elem.</span><span class="sxs-lookup"><span data-stu-id="34412-127">ListItem Element for ListItems for ListControl (Format)</span></span>](./listitem-element-for-listitems-for-listcontrol-format.md)

[<span data-ttu-id="34412-128">ItemSelectionCondition ListControl (formátum) a PropertyName elem.</span><span class="sxs-lookup"><span data-stu-id="34412-128">PropertyName Element for ItemSelectionCondition for ListControl (Format)</span></span>](./propertyname-element-for-itemselectioncondition-for-listcontrol-format.md)

[<span data-ttu-id="34412-129">ItemSelectionCondition ListControl (formátum) a scriptblock kulcsszót elem.</span><span class="sxs-lookup"><span data-stu-id="34412-129">ScriptBlock Element for ItemSelectionCondition for ListControl (Format)</span></span>](./scriptblock-element-for-itemselectioncondition-for-listcontrol-format.md)

[<span data-ttu-id="34412-130">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="34412-130">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
