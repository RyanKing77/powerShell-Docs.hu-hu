---
title: ViewSelectedBy (formátum) TypeName eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 0ad807a9-d7d8-4e96-b799-9c6a7677cc2d
caps.latest.revision: 12
ms.openlocfilehash: e2028c479103cc414295dc24a0f9bb69190bfc66
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56848138"
---
# <a name="typename-element-for-viewselectedby-format"></a><span data-ttu-id="9eb50-102">A ViewSelectedBy elem TypeName eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="9eb50-102">TypeName Element for ViewSelectedBy (Format)</span></span>

<span data-ttu-id="9eb50-103">Megadja a nézet által megjelenített .NET-objektumokat.</span><span class="sxs-lookup"><span data-stu-id="9eb50-103">Specifies a .NET object that is displayed by the view.</span></span>

<span data-ttu-id="9eb50-104">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem ViewSelectedBy elem (formátum) TypeName eleme ViewSelectedBy (formátum)</span><span class="sxs-lookup"><span data-stu-id="9eb50-104">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) ViewSelectedBy Element (Format) TypeName Element for ViewSelectedBy (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="9eb50-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="9eb50-105">Syntax</span></span>

```xml
<TypeName>FullyQualifiedTypeName</TypeName>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="9eb50-106">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="9eb50-106">Attributes and Elements</span></span>

<span data-ttu-id="9eb50-107">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a szülő elemei a `TypeName` elemet.</span><span class="sxs-lookup"><span data-stu-id="9eb50-107">The following sections describe attributes, child elements, and the parent elements of the `TypeName` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="9eb50-108">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="9eb50-108">Attributes</span></span>

<span data-ttu-id="9eb50-109">Nincs.</span><span class="sxs-lookup"><span data-stu-id="9eb50-109">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="9eb50-110">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="9eb50-110">Child Elements</span></span>

<span data-ttu-id="9eb50-111">Nincs.</span><span class="sxs-lookup"><span data-stu-id="9eb50-111">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="9eb50-112">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="9eb50-112">Parent Elements</span></span>

|<span data-ttu-id="9eb50-113">Elem</span><span class="sxs-lookup"><span data-stu-id="9eb50-113">Element</span></span>|<span data-ttu-id="9eb50-114">Leírás</span><span class="sxs-lookup"><span data-stu-id="9eb50-114">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="9eb50-115">ViewSelectedBy elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="9eb50-115">ViewSelectedBy Element (Format)</span></span>](./viewselectedby-element-format.md)|<span data-ttu-id="9eb50-116">A .NET-objektumokat a nézet által megjelenített határozza meg.</span><span class="sxs-lookup"><span data-stu-id="9eb50-116">Defines the .NET objects that are displayed by the view.</span></span>|

## <a name="text-value"></a><span data-ttu-id="9eb50-117">Szöveges érték</span><span class="sxs-lookup"><span data-stu-id="9eb50-117">Text Value</span></span>

<span data-ttu-id="9eb50-118">Adja meg a teljes nevet, a .NET-típus, például `System.IO.DirectoryInfo`.</span><span class="sxs-lookup"><span data-stu-id="9eb50-118">Specify the fully qualified name of the .NET type, such as `System.IO.DirectoryInfo`.</span></span>

## <a name="remarks"></a><span data-ttu-id="9eb50-119">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="9eb50-119">Remarks</span></span>

<span data-ttu-id="9eb50-120">Ez az elem használatának módja a következőben különböző nézeteket kapcsolatos további információkért lásd: [tábla nézetek létrehozásával](./creating-a-table-view.md), [lista nézet létrehozásával](./creating-a-list-view.md), [széles nézet létrehozásával](./creating-a-wide-view.md), és [ Egyéni nézet összetevők](./creating-custom-controls.md).</span><span class="sxs-lookup"><span data-stu-id="9eb50-120">For more information about how this element is used in different views, see [Creating a Table View](./creating-a-table-view.md), [Creating a List View](./creating-a-list-view.md), [Creating a Wide View](./creating-a-wide-view.md), and [Custom View Components](./creating-custom-controls.md).</span></span>

## <a name="example"></a><span data-ttu-id="9eb50-121">Példa</span><span class="sxs-lookup"><span data-stu-id="9eb50-121">Example</span></span>

<span data-ttu-id="9eb50-122">Az alábbi példa bemutatja, hogyan adja meg a [System.Serviceprocess.Servicecontroller](/dotnet/api/System.ServiceProcess.ServiceController) objektum az adott nézet.</span><span class="sxs-lookup"><span data-stu-id="9eb50-122">The following example shows how to specify the [System.Serviceprocess.Servicecontroller](/dotnet/api/System.ServiceProcess.ServiceController) object for a list view.</span></span> <span data-ttu-id="9eb50-123">Tábla, széles és egyéni nézetekben használható ugyanazzal a sémával.</span><span class="sxs-lookup"><span data-stu-id="9eb50-123">The same schema is used for table, wide, and custom views.</span></span>

```xml
<View>
  <Name>System.ServiceProcess.ServiceController</Name>
  <ViewSelectedBy>
    <TypeName>System.ServiceProcess.ServiceController</TypeName>
  </ViewSelectedBy>
  <ListControl>...</ListControl>
</View>
```

## <a name="see-also"></a><span data-ttu-id="9eb50-124">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="9eb50-124">See Also</span></span>

[<span data-ttu-id="9eb50-125">Lista nézet létrehozása</span><span class="sxs-lookup"><span data-stu-id="9eb50-125">Creating a List View</span></span>](./creating-a-list-view.md)

[<span data-ttu-id="9eb50-126">Tábla nézet létrehozása</span><span class="sxs-lookup"><span data-stu-id="9eb50-126">Creating a Table View</span></span>](./creating-a-table-view.md)

[<span data-ttu-id="9eb50-127">Egy széles nézet létrehozása</span><span class="sxs-lookup"><span data-stu-id="9eb50-127">Creating a Wide View</span></span>](./creating-a-wide-view.md)

[<span data-ttu-id="9eb50-128">Egyéni vezérlők létrehozását</span><span class="sxs-lookup"><span data-stu-id="9eb50-128">Creating Custom Controls</span></span>](./creating-custom-controls.md)

[<span data-ttu-id="9eb50-129">ViewSelectedBy elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="9eb50-129">ViewSelectedBy Element (Format)</span></span>](./viewselectedby-element-format.md)

[<span data-ttu-id="9eb50-130">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="9eb50-130">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
