---
title: Elem name (formátum) nézet |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 3a31010d-1db9-44ae-a7f3-6ed32cb641cb
caps.latest.revision: 16
ms.openlocfilehash: 097d20cb6a04635124d1f96823248df6095ca1af
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62065070"
---
# <a name="name-element-for-view-format"></a><span data-ttu-id="635a0-102">A Nézet Név eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="635a0-102">Name Element for View (Format)</span></span>

<span data-ttu-id="635a0-103">Itt adhatja meg, amely azonosítja a nézet nevét.</span><span class="sxs-lookup"><span data-stu-id="635a0-103">Specifies the name that is used to identify the view.</span></span>

<span data-ttu-id="635a0-104">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem Name elemet (formátum)</span><span class="sxs-lookup"><span data-stu-id="635a0-104">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) Name Element (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="635a0-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="635a0-105">Syntax</span></span>

```xml
<Name>ViewName</Name>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="635a0-106">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="635a0-106">Attributes and Elements</span></span>

<span data-ttu-id="635a0-107">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `Name` elemet.</span><span class="sxs-lookup"><span data-stu-id="635a0-107">The following sections describe attributes, child elements, and the parent element of the `Name` element.</span></span> <span data-ttu-id="635a0-108">Csak egy `Name` elem engedélyezett-e meg.</span><span class="sxs-lookup"><span data-stu-id="635a0-108">Only one `Name` element is allowed for each view.</span></span>

### <a name="attributes"></a><span data-ttu-id="635a0-109">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="635a0-109">Attributes</span></span>

<span data-ttu-id="635a0-110">Nincs.</span><span class="sxs-lookup"><span data-stu-id="635a0-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="635a0-111">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="635a0-111">Child Elements</span></span>

<span data-ttu-id="635a0-112">Nincs.</span><span class="sxs-lookup"><span data-stu-id="635a0-112">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="635a0-113">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="635a0-113">Parent Elements</span></span>

|<span data-ttu-id="635a0-114">Elem</span><span class="sxs-lookup"><span data-stu-id="635a0-114">Element</span></span>|<span data-ttu-id="635a0-115">Leírás</span><span class="sxs-lookup"><span data-stu-id="635a0-115">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="635a0-116">Nézet elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="635a0-116">View Element (Format)</span></span>](./view-element-format.md)|<span data-ttu-id="635a0-117">Meghatározza egy nézetet, amely legalább egy .NET-objektumokká tagjai megjelenítésére szolgál.</span><span class="sxs-lookup"><span data-stu-id="635a0-117">Defines a view that is used to display the members of one or more .NET objects.</span></span>|

## <a name="text-value"></a><span data-ttu-id="635a0-118">A szöveges érték</span><span class="sxs-lookup"><span data-stu-id="635a0-118">Text Value</span></span>

<span data-ttu-id="635a0-119">Adjon meg egy egyedi rövid nevet a nézetet.</span><span class="sxs-lookup"><span data-stu-id="635a0-119">Specify a unique friendly name for the view.</span></span> <span data-ttu-id="635a0-120">Ez a név tartalmazhat egy hivatkozást a nézet (például egy táblázat vagy lista nézetben), mely objektum vagy objektumcsoport használja a nézetet, mely a parancs visszaadja az objektumokat, vagy ezek kombinációja típusát.</span><span class="sxs-lookup"><span data-stu-id="635a0-120">This name can include a reference to the type of the view (such as a table view or list view), which object or set of objects use the view, what command returns the objects, or a combination of these.</span></span>

## <a name="remarks"></a><span data-ttu-id="635a0-121">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="635a0-121">Remarks</span></span>

<span data-ttu-id="635a0-122">A nézetek különböző típusú kapcsolatos további információkért lásd: a következő témaköröket: [Tábla nézet](./creating-a-table-view.md), [listanézet](./creating-a-list-view.md), [széles nézet](./creating-a-wide-view.md), és [egyéni nézet](./creating-custom-controls.md).</span><span class="sxs-lookup"><span data-stu-id="635a0-122">For more information about the different types of views, see the following topics: [Table View](./creating-a-table-view.md), [List View](./creating-a-list-view.md), [Wide View](./creating-a-wide-view.md), and [Custom View](./creating-custom-controls.md).</span></span>

## <a name="example"></a><span data-ttu-id="635a0-123">Példa</span><span class="sxs-lookup"><span data-stu-id="635a0-123">Example</span></span>

<span data-ttu-id="635a0-124">A következő példa bemutatja egy `View` elem, amely meghatározza a táblázatos nézetre a [System.Serviceprocess.Servicecontroller](/dotnet/api/System.ServiceProcess.ServiceController) objektum.</span><span class="sxs-lookup"><span data-stu-id="635a0-124">The following example shows a `View` element that defines a table view for the [System.Serviceprocess.Servicecontroller](/dotnet/api/System.ServiceProcess.ServiceController) object.</span></span> <span data-ttu-id="635a0-125">A nézet neve "szolgáltatás".</span><span class="sxs-lookup"><span data-stu-id="635a0-125">The name of the view is "service".</span></span>

```xml
<View>
  <Name>service</Name>
  <ViewSelectedBy>
    <TypeName>System.ServiceProcess.ServiceController</TypeName>
  </ViewSelectedBy>
  <TableControl>...</TableControl>
</View>

```

## <a name="see-also"></a><span data-ttu-id="635a0-126">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="635a0-126">See Also</span></span>

[<span data-ttu-id="635a0-127">Lista nézet létrehozása</span><span class="sxs-lookup"><span data-stu-id="635a0-127">Creating a List View</span></span>](./creating-a-list-view.md)

[<span data-ttu-id="635a0-128">Tábla nézet létrehozása</span><span class="sxs-lookup"><span data-stu-id="635a0-128">Creating a Table View</span></span>](./creating-a-table-view.md)

[<span data-ttu-id="635a0-129">Egy széles nézet létrehozása</span><span class="sxs-lookup"><span data-stu-id="635a0-129">Creating a Wide View</span></span>](./creating-a-wide-view.md)

[<span data-ttu-id="635a0-130">Egyéni vezérlők létrehozását</span><span class="sxs-lookup"><span data-stu-id="635a0-130">Creating Custom Controls</span></span>](./creating-custom-controls.md)

[<span data-ttu-id="635a0-131">Nézet elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="635a0-131">View Element (Format)</span></span>](./view-element-format.md)

[<span data-ttu-id="635a0-132">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="635a0-132">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
