---
title: ListControl (formátum) ListEntry eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 6d16bca8-d025-432d-aa84-8b607b8af3ae
caps.latest.revision: 12
ms.openlocfilehash: 1a3bafd4ca94aee70e869c699f7a4ef8befc5511
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62065223"
---
# <a name="listentry-element-for-listcontrol-format"></a><span data-ttu-id="06ecc-102">A ListControl elemhez tartozó ListEntry elem (Formátum)</span><span class="sxs-lookup"><span data-stu-id="06ecc-102">ListEntry Element for ListControl (Format)</span></span>

<span data-ttu-id="06ecc-103">A lista nézet definíciójának biztosít.</span><span class="sxs-lookup"><span data-stu-id="06ecc-103">Provides a definition of the list view.</span></span>

<span data-ttu-id="06ecc-104">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem ListControl elem (formátum) ListEntries elem (formátum) ListEntry elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="06ecc-104">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) ListControl Element (Format) ListEntries Element (Format) ListEntry Element (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="06ecc-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="06ecc-105">Syntax</span></span>

```xml
<ListEntry>
  <EntrySelectedBy>...</EntrySelectedBy>
  <ListItems>...</ListItems>
</ListEntry>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="06ecc-106">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="06ecc-106">Attributes and Elements</span></span>

<span data-ttu-id="06ecc-107">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `ListEntry` elemet.</span><span class="sxs-lookup"><span data-stu-id="06ecc-107">The following sections describe the attributes, child elements, and the parent element of the `ListEntry` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="06ecc-108">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="06ecc-108">Attributes</span></span>

<span data-ttu-id="06ecc-109">Nincs.</span><span class="sxs-lookup"><span data-stu-id="06ecc-109">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="06ecc-110">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="06ecc-110">Child Elements</span></span>

|<span data-ttu-id="06ecc-111">Elem</span><span class="sxs-lookup"><span data-stu-id="06ecc-111">Element</span></span>|<span data-ttu-id="06ecc-112">Leírás</span><span class="sxs-lookup"><span data-stu-id="06ecc-112">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="06ecc-113">EntrySelectedBy eleme ListEntry (formátum)</span><span class="sxs-lookup"><span data-stu-id="06ecc-113">EntrySelectedBy Element for ListEntry (Format)</span></span>](./entryselectedby-element-for-listentry-for-listcontrol-format.md)|<span data-ttu-id="06ecc-114">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="06ecc-114">Optional element.</span></span><br /><br /> <span data-ttu-id="06ecc-115">A .NET-objektumok, amelyek a lista nézetdefinícióban, illetve a feltétellel, hogy léteznie kell a definíció használandó határozza meg.</span><span class="sxs-lookup"><span data-stu-id="06ecc-115">Defines the .NET objects that use this list view definition or the condition that must exist for this definition to be used.</span></span>|
|[<span data-ttu-id="06ecc-116">ListItems elemek elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="06ecc-116">ListItems Element (Format)</span></span>](./listitems-element-for-listentry-for-listcontrol-format.md)|<span data-ttu-id="06ecc-117">Szükséges eleme.</span><span class="sxs-lookup"><span data-stu-id="06ecc-117">Required element.</span></span><br /><br /> <span data-ttu-id="06ecc-118">Meghatározza a tulajdonságok és a parancsfájlok, melynek értékei szerint a listanézetet jelennek meg.</span><span class="sxs-lookup"><span data-stu-id="06ecc-118">Defines the properties and scripts whose values are displayed by the list view.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="06ecc-119">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="06ecc-119">Parent Elements</span></span>

|<span data-ttu-id="06ecc-120">Elem</span><span class="sxs-lookup"><span data-stu-id="06ecc-120">Element</span></span>|<span data-ttu-id="06ecc-121">Leírás</span><span class="sxs-lookup"><span data-stu-id="06ecc-121">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="06ecc-122">ListEntries elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="06ecc-122">ListEntries Element (Format)</span></span>](./listentries-element-for-listcontrol-format.md)|<span data-ttu-id="06ecc-123">A lista nézet a definíciókat tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="06ecc-123">Provides the definitions of the list view.</span></span>|

## <a name="remarks"></a><span data-ttu-id="06ecc-124">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="06ecc-124">Remarks</span></span>

<span data-ttu-id="06ecc-125">Lista nézetben, amely megjeleníti a tulajdonság vagy parancsfájl értékei az egyes objektumok lista formájában.</span><span class="sxs-lookup"><span data-stu-id="06ecc-125">A list view is a list format that displays property values or script values for each object.</span></span> <span data-ttu-id="06ecc-126">Listanézetek kapcsolatos további információkért lásd: [lista nézet létrehozásával](./creating-a-list-view.md).</span><span class="sxs-lookup"><span data-stu-id="06ecc-126">For more information about list views, see [Creating a List View](./creating-a-list-view.md).</span></span>

## <a name="example"></a><span data-ttu-id="06ecc-127">Példa</span><span class="sxs-lookup"><span data-stu-id="06ecc-127">Example</span></span>

<span data-ttu-id="06ecc-128">Ez a példa bemutatja az XML-elemeket, amelyek meghatározzák a listanézet a [System.Serviceprocess.Servicecontroller](/dotnet/api/System.ServiceProcess.ServiceController) objektum.</span><span class="sxs-lookup"><span data-stu-id="06ecc-128">This example shows the XML elements that define the list view for the [System.Serviceprocess.Servicecontroller](/dotnet/api/System.ServiceProcess.ServiceController) object.</span></span>

```xml
<View>
  <Name>System.ServiceProcess.ServiceController</Name>
  <ViewSelectedBy>
    <TypeName>System.ServiceProcess.ServiceController</TypeName>
  </ViewSelectedBy>
  <ListControl>
    <ListEntries>
      <ListEntry>
        <ListItems>...</ListItems>
      </ListEntry>
    </ListEntries>
  </ListControl>
</View>
```

## <a name="see-also"></a><span data-ttu-id="06ecc-129">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="06ecc-129">See Also</span></span>

[<span data-ttu-id="06ecc-130">Lista nézet létrehozása</span><span class="sxs-lookup"><span data-stu-id="06ecc-130">Creating a List View</span></span>](./creating-a-list-view.md)

[<span data-ttu-id="06ecc-131">EntrySelectedBy eleme ListEntry (formátum)</span><span class="sxs-lookup"><span data-stu-id="06ecc-131">EntrySelectedBy Element for ListEntry (Format)</span></span>](./entryselectedby-element-for-listentry-for-listcontrol-format.md)

[<span data-ttu-id="06ecc-132">ListEntries elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="06ecc-132">ListEntries Element (Format)</span></span>](./listentries-element-for-listcontrol-format.md)

[<span data-ttu-id="06ecc-133">ListItems elemek elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="06ecc-133">ListItems Element (Format)</span></span>](./listitems-element-for-listentry-for-listcontrol-format.md)

[<span data-ttu-id="06ecc-134">Egy Windows PowerShell formázás és a fájl típusai</span><span class="sxs-lookup"><span data-stu-id="06ecc-134">Writing a Windows PowerShell Formatting and Types File</span></span>](./writing-a-powershell-formatting-file.md)
