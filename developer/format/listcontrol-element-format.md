---
title: ListControl elem (formátum) |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 37beeb0b-7a81-4747-becb-e309e17278fb
caps.latest.revision: 12
ms.openlocfilehash: 7a117c25b0d117dc846ba8e060e31e838b5edd52
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56847830"
---
# <a name="listcontrol-element-format"></a><span data-ttu-id="d70ce-102">ListControl elem (Formátum)</span><span class="sxs-lookup"><span data-stu-id="d70ce-102">ListControl Element (Format)</span></span>

<span data-ttu-id="d70ce-103">Határozza meg a nézet lista formájában.</span><span class="sxs-lookup"><span data-stu-id="d70ce-103">Defines a list format for the view.</span></span>

<span data-ttu-id="d70ce-104">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem ListControl elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="d70ce-104">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) ListControl Element (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="d70ce-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="d70ce-105">Syntax</span></span>

```xml
<ListControl>
  <ListEntries>...</ListEntries>
</ListControl>

```

## <a name="attributes-and-elements"></a><span data-ttu-id="d70ce-106">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="d70ce-106">Attributes and Elements</span></span>

<span data-ttu-id="d70ce-107">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `ListControl` elemet.</span><span class="sxs-lookup"><span data-stu-id="d70ce-107">The following sections describe the attributes, child elements, and the parent element of the `ListControl` element.</span></span> <span data-ttu-id="d70ce-108">Ez az elem csak egyetlen gyermekelemet kell tartalmaznia.</span><span class="sxs-lookup"><span data-stu-id="d70ce-108">This element must contain only a single child element.</span></span>

### <a name="attributes"></a><span data-ttu-id="d70ce-109">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="d70ce-109">Attributes</span></span>

<span data-ttu-id="d70ce-110">Nincs.</span><span class="sxs-lookup"><span data-stu-id="d70ce-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="d70ce-111">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="d70ce-111">Child Elements</span></span>

|<span data-ttu-id="d70ce-112">Elem</span><span class="sxs-lookup"><span data-stu-id="d70ce-112">Element</span></span>|<span data-ttu-id="d70ce-113">Leírás</span><span class="sxs-lookup"><span data-stu-id="d70ce-113">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="d70ce-114">ListEntries elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="d70ce-114">ListEntries Element (Format)</span></span>](./listentries-element-for-listcontrol-format.md)|<span data-ttu-id="d70ce-115">Szükséges eleme.</span><span class="sxs-lookup"><span data-stu-id="d70ce-115">Required element.</span></span><br /><br /> <span data-ttu-id="d70ce-116">A lista nézet a definíciókat tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="d70ce-116">Provides the definitions of the list view.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="d70ce-117">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="d70ce-117">Parent Elements</span></span>

|<span data-ttu-id="d70ce-118">Elem</span><span class="sxs-lookup"><span data-stu-id="d70ce-118">Element</span></span>|<span data-ttu-id="d70ce-119">Leírás</span><span class="sxs-lookup"><span data-stu-id="d70ce-119">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="d70ce-120">Nézet elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="d70ce-120">View Element (Format)</span></span>](./view-element-format.md)|<span data-ttu-id="d70ce-121">Meghatározza egy nézetet, amely egy vagy több objektum tagjait megjelenítésére szolgál.</span><span class="sxs-lookup"><span data-stu-id="d70ce-121">Defines a view that is used to display the members of one or more objects.</span></span>|

## <a name="remarks"></a><span data-ttu-id="d70ce-122">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="d70ce-122">Remarks</span></span>

<span data-ttu-id="d70ce-123">Lista nézet létrehozásával kapcsolatos további információkért lásd: [lista nézet létrehozásával](./creating-a-list-view.md).</span><span class="sxs-lookup"><span data-stu-id="d70ce-123">For more information about creating a list view, see [Creating a List View](./creating-a-list-view.md).</span></span>

## <a name="example"></a><span data-ttu-id="d70ce-124">Példa</span><span class="sxs-lookup"><span data-stu-id="d70ce-124">Example</span></span>

<span data-ttu-id="d70ce-125">Ez a példa bemutatja a megjelenítheti a [System.Serviceprocess.Servicecontroller](/dotnet/api/System.ServiceProcess.ServiceController) objektum.</span><span class="sxs-lookup"><span data-stu-id="d70ce-125">This example shows a list view for the [System.Serviceprocess.Servicecontroller](/dotnet/api/System.ServiceProcess.ServiceController) object.</span></span>

```
<View>
  <Name>System.ServiceProcess.ServiceController</Name>
  <ViewSelectedBy>
    <TypeName>System.ServiceProcess.ServiceController</TypeName>
  </ViewSelectedBy>
  <ListControl>
    <ListEntries>
      <ListEntry>...</ListEntry>
    </ListEntries>
  </ListControl>
</View>
```

## <a name="see-also"></a><span data-ttu-id="d70ce-126">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="d70ce-126">See Also</span></span>

[<span data-ttu-id="d70ce-127">Nézet elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="d70ce-127">View Element (Format)</span></span>](./view-element-format.md)

[<span data-ttu-id="d70ce-128">ListEntries elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="d70ce-128">ListEntries Element (Format)</span></span>](./listentries-element-for-listcontrol-format.md)

[<span data-ttu-id="d70ce-129">Lista nézet létrehozása</span><span class="sxs-lookup"><span data-stu-id="d70ce-129">Creating a List View</span></span>](./creating-a-list-view.md)

[<span data-ttu-id="d70ce-130">Egy Windows PowerShell formázás és a fájl típusai</span><span class="sxs-lookup"><span data-stu-id="d70ce-130">Writing a Windows PowerShell Formatting and Types File</span></span>](./writing-a-powershell-formatting-file.md)
