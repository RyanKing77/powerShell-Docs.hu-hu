---
title: ListControl (formátum) ListEntries eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: b62e81cc-4175-40fa-829f-634245b09f86
caps.latest.revision: 12
ms.openlocfilehash: aaf16702e485135b5299ccb43a2b62db2d9f5762
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56847361"
---
# <a name="listentries-element-for-listcontrol-format"></a><span data-ttu-id="7cbfa-102">A ListControl elemhez tartozó ListEntries elem (Formátum)</span><span class="sxs-lookup"><span data-stu-id="7cbfa-102">ListEntries Element for ListControl (Format)</span></span>

<span data-ttu-id="7cbfa-103">A lista nézet a definíciókat tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="7cbfa-103">Provides the definitions of the list view.</span></span> <span data-ttu-id="7cbfa-104">A listanézet meg kell adnia egy vagy több definíciót.</span><span class="sxs-lookup"><span data-stu-id="7cbfa-104">The list view must specify one or more definitions.</span></span>

<span data-ttu-id="7cbfa-105">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem ListControl elem (formátum) ListEntries elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="7cbfa-105">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) ListControl Element (Format) ListEntries Element (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="7cbfa-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="7cbfa-106">Syntax</span></span>

```xml
<ListEntries>
  <ListEntry>...</ListEntry>
</ListEntries>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="7cbfa-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="7cbfa-107">Attributes and Elements</span></span>

<span data-ttu-id="7cbfa-108">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `ListEntries` elemet.</span><span class="sxs-lookup"><span data-stu-id="7cbfa-108">The following sections describe the attributes, child elements, and the parent element of the `ListEntries` element.</span></span> <span data-ttu-id="7cbfa-109">Meg kell adni legalább egy gyermekelemet.</span><span class="sxs-lookup"><span data-stu-id="7cbfa-109">At least one child element must be specified.</span></span>

### <a name="attributes"></a><span data-ttu-id="7cbfa-110">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="7cbfa-110">Attributes</span></span>

<span data-ttu-id="7cbfa-111">Nincs.</span><span class="sxs-lookup"><span data-stu-id="7cbfa-111">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="7cbfa-112">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="7cbfa-112">Child Elements</span></span>

|<span data-ttu-id="7cbfa-113">Elem</span><span class="sxs-lookup"><span data-stu-id="7cbfa-113">Element</span></span>|<span data-ttu-id="7cbfa-114">Leírás</span><span class="sxs-lookup"><span data-stu-id="7cbfa-114">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="7cbfa-115">ListEntry elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="7cbfa-115">ListEntry Element (Format)</span></span>](./listentry-element-for-listcontrol-format.md)|<span data-ttu-id="7cbfa-116">A lista nézet definíciójának biztosít.</span><span class="sxs-lookup"><span data-stu-id="7cbfa-116">Provides a definition of the list view.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="7cbfa-117">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="7cbfa-117">Parent Elements</span></span>

|<span data-ttu-id="7cbfa-118">Elem</span><span class="sxs-lookup"><span data-stu-id="7cbfa-118">Element</span></span>|<span data-ttu-id="7cbfa-119">Leírás</span><span class="sxs-lookup"><span data-stu-id="7cbfa-119">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="7cbfa-120">ListControl elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="7cbfa-120">ListControl Element (Format)</span></span>](./listcontrol-element-format.md)|<span data-ttu-id="7cbfa-121">Határozza meg a nézet lista formájában.</span><span class="sxs-lookup"><span data-stu-id="7cbfa-121">Defines a list format for the view.</span></span>|

## <a name="remarks"></a><span data-ttu-id="7cbfa-122">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="7cbfa-122">Remarks</span></span>

<span data-ttu-id="7cbfa-123">Listanézetek kapcsolatos további információkért lásd: [listanézet](./creating-a-list-view.md).</span><span class="sxs-lookup"><span data-stu-id="7cbfa-123">For more information about list views, see [List View](./creating-a-list-view.md).</span></span>

## <a name="example"></a><span data-ttu-id="7cbfa-124">Példa</span><span class="sxs-lookup"><span data-stu-id="7cbfa-124">Example</span></span>

<span data-ttu-id="7cbfa-125">Ez a példa bemutatja az XML-elemeket, amelyek meghatározzák a listanézet a [System.Serviceprocess.Servicecontroller](/dotnet/api/System.ServiceProcess.ServiceController) objektum.</span><span class="sxs-lookup"><span data-stu-id="7cbfa-125">This example shows the XML elements that define the list view for the [System.Serviceprocess.Servicecontroller](/dotnet/api/System.ServiceProcess.ServiceController) object.</span></span>

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

## <a name="see-also"></a><span data-ttu-id="7cbfa-126">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="7cbfa-126">See Also</span></span>

[<span data-ttu-id="7cbfa-127">ListControl elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="7cbfa-127">ListControl Element (Format)</span></span>](./listcontrol-element-format.md)

[<span data-ttu-id="7cbfa-128">ListEntry elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="7cbfa-128">ListEntry Element (Format)</span></span>](./listentry-element-for-listcontrol-format.md)

[<span data-ttu-id="7cbfa-129">Listanézet</span><span class="sxs-lookup"><span data-stu-id="7cbfa-129">List View</span></span>](./creating-a-list-view.md)

[<span data-ttu-id="7cbfa-130">Egy Windows PowerShell formázás és a fájl típusai</span><span class="sxs-lookup"><span data-stu-id="7cbfa-130">Writing a Windows PowerShell Formatting and Types File</span></span>](./writing-a-powershell-formatting-file.md)
