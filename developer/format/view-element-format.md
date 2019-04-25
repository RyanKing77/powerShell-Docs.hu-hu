---
title: (Formátum) elem megtekintése |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: d837d5d4-ed2e-4d84-a306-0b5d2ad2d0bf
caps.latest.revision: 24
ms.openlocfilehash: 2361c1117757569bef0815018c75764430a9e7a8
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62083722"
---
# <a name="view-element-format"></a><span data-ttu-id="7577b-102">Nézet elem (Formátum)</span><span class="sxs-lookup"><span data-stu-id="7577b-102">View Element (Format)</span></span>

<span data-ttu-id="7577b-103">Legalább egy .NET-objektumokat megjelenítő nézet határozza meg.</span><span class="sxs-lookup"><span data-stu-id="7577b-103">Defines a view that displays one or more .NET objects.</span></span> <span data-ttu-id="7577b-104">Formázási-fájlban definiált nézetek száma nincs korlátozva van.</span><span class="sxs-lookup"><span data-stu-id="7577b-104">There is no limit to the number of views that can be defined in a formatting file.</span></span>

<span data-ttu-id="7577b-105">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézet elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="7577b-105">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="7577b-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="7577b-106">Syntax</span></span>

```xml
<View>
  <Name>Friendly name of view.</Name>
  <ViewSelectedBy>...</ViewSelectedBy>
  <Controls>...</Controls>
  <GroupBy>...</GroupBy>
  <TableControl>...</TableControl>
  <ListControl>...</ListControl>
  <WideControl>...</WideControl>
  <CustomControl>...</CustomControl>
</View>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="7577b-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="7577b-107">Attributes and Elements</span></span>

<span data-ttu-id="7577b-108">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `View` elemet.</span><span class="sxs-lookup"><span data-stu-id="7577b-108">The following sections describe the attributes, child elements, and the parent element of the `View` element.</span></span> <span data-ttu-id="7577b-109">Meg kell adnia az egyiket a vezérlő gyermekelemek, és meg kell adnia a nézet és az objektumok, amelyek a nézet nevét.</span><span class="sxs-lookup"><span data-stu-id="7577b-109">You must specify one and only one of the control child elements, and you must specify the name of the view and the objects that use the view.</span></span> <span data-ttu-id="7577b-110">Egyéni vezérlők meghatározása, hogyan csoportosítsa objektumokat, és ha a nézet-e a sávon kívüli megadása nem kötelező.</span><span class="sxs-lookup"><span data-stu-id="7577b-110">Defining custom controls, how to group objects, and specifying if the view is out-of-band are optional.</span></span>

### <a name="attributes"></a><span data-ttu-id="7577b-111">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="7577b-111">Attributes</span></span>

<span data-ttu-id="7577b-112">Nincs.</span><span class="sxs-lookup"><span data-stu-id="7577b-112">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="7577b-113">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="7577b-113">Child Elements</span></span>

|<span data-ttu-id="7577b-114">Elem</span><span class="sxs-lookup"><span data-stu-id="7577b-114">Element</span></span>|<span data-ttu-id="7577b-115">Leírás</span><span class="sxs-lookup"><span data-stu-id="7577b-115">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="7577b-116">Vezérlők elem nézet (formátum)</span><span class="sxs-lookup"><span data-stu-id="7577b-116">Controls Element for View (Format)</span></span>](./controls-element-for-view-format.md)|<span data-ttu-id="7577b-117">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="7577b-117">Optional element.</span></span><br /><br /> <span data-ttu-id="7577b-118">Határozza meg, hogy a nézet belül vezérlőelemére név szerint lehet hivatkozni.</span><span class="sxs-lookup"><span data-stu-id="7577b-118">Defines a set of controls that can be referenced by their name from within the view.</span></span>|
|[<span data-ttu-id="7577b-119">CustomControl elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="7577b-119">CustomControl Element (Format)</span></span>](./customcontrol-element-for-groupby-format.md)|<span data-ttu-id="7577b-120">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="7577b-120">Optional element.</span></span><br /><br /> <span data-ttu-id="7577b-121">A nézet egy egyéni vezérlő formátumát határozza meg.</span><span class="sxs-lookup"><span data-stu-id="7577b-121">Defines a custom control format for the view.</span></span>|
|[<span data-ttu-id="7577b-122">GroupBy elem nézet (formátum)</span><span class="sxs-lookup"><span data-stu-id="7577b-122">GroupBy Element for View (Format)</span></span>](./groupby-element-for-view-format.md)|<span data-ttu-id="7577b-123">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="7577b-123">Optional element.</span></span><br /><br /> <span data-ttu-id="7577b-124">Határozza meg, hogy a .NET-objektumok tagjai vannak csoportosítva.</span><span class="sxs-lookup"><span data-stu-id="7577b-124">Defines how the members of the .NET objects are grouped.</span></span>|
|[<span data-ttu-id="7577b-125">ListControl elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="7577b-125">ListControl Element (Format)</span></span>](./listcontrol-element-format.md)|<span data-ttu-id="7577b-126">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="7577b-126">Optional element.</span></span><br /><br /> <span data-ttu-id="7577b-127">Határozza meg a nézet lista formájában.</span><span class="sxs-lookup"><span data-stu-id="7577b-127">Defines a list format for the view.</span></span>|
|[<span data-ttu-id="7577b-128">Name elemet a nézet (formátum)</span><span class="sxs-lookup"><span data-stu-id="7577b-128">Name Element for View (Format)</span></span>](./name-element-for-view-format.md)|<span data-ttu-id="7577b-129">Szükséges eleme.</span><span class="sxs-lookup"><span data-stu-id="7577b-129">Required element.</span></span><br /><br /> <span data-ttu-id="7577b-130">Megadja a mutató hivatkozás a nézet nevét.</span><span class="sxs-lookup"><span data-stu-id="7577b-130">Specifies the name used to reference the view.</span></span>|
|[<span data-ttu-id="7577b-131">TableControl elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="7577b-131">TableControl Element (Format)</span></span>](./tablecontrol-element-format.md)|<span data-ttu-id="7577b-132">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="7577b-132">Optional element.</span></span><br /><br /> <span data-ttu-id="7577b-133">Határozza meg a nézet táblázatos formában.</span><span class="sxs-lookup"><span data-stu-id="7577b-133">Defines a table format for the view.</span></span>|
|[<span data-ttu-id="7577b-134">ViewSelectedBy elem nézet (formátum)</span><span class="sxs-lookup"><span data-stu-id="7577b-134">ViewSelectedBy Element for View (Format)</span></span>](./viewselectedby-element-format.md)|<span data-ttu-id="7577b-135">Szükséges eleme.</span><span class="sxs-lookup"><span data-stu-id="7577b-135">Required element.</span></span><br /><br /> <span data-ttu-id="7577b-136">Határozza meg, hogy ez a nézet jeleníti meg a .NET-objektumokat.</span><span class="sxs-lookup"><span data-stu-id="7577b-136">Defines the .NET objects that this view displays.</span></span>|
|[<span data-ttu-id="7577b-137">WideControl elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="7577b-137">WideControl Element (Format)</span></span>](./widecontrol-element-format.md)|<span data-ttu-id="7577b-138">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="7577b-138">Optional element.</span></span><br /><br /> <span data-ttu-id="7577b-139">A wide (egyetlen érték) határozza meg a Nézet formátuma.</span><span class="sxs-lookup"><span data-stu-id="7577b-139">Defines a wide (single value) list format for the view.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="7577b-140">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="7577b-140">Parent Elements</span></span>

|<span data-ttu-id="7577b-141">Elem</span><span class="sxs-lookup"><span data-stu-id="7577b-141">Element</span></span>|<span data-ttu-id="7577b-142">Leírás</span><span class="sxs-lookup"><span data-stu-id="7577b-142">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="7577b-143">ViewDefinitions elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="7577b-143">ViewDefinitions Element (Format)</span></span>](./viewdefinitions-element-format.md)|<span data-ttu-id="7577b-144">Határozza meg az objektumokat megjelenítő nézetek.</span><span class="sxs-lookup"><span data-stu-id="7577b-144">Defines the views used to display objects.</span></span>|

## <a name="remarks"></a><span data-ttu-id="7577b-145">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="7577b-145">Remarks</span></span>

<span data-ttu-id="7577b-146">A különböző nézetek és az egyéni vezérlők az összetevőivel kapcsolatos további információkért lásd a következő témaköröket:</span><span class="sxs-lookup"><span data-stu-id="7577b-146">For more information about the components of different views and custom controls, see the following topics:</span></span>

- [<span data-ttu-id="7577b-147">Tábla nézet összetevők</span><span class="sxs-lookup"><span data-stu-id="7577b-147">Table View Components</span></span>](./creating-a-table-view.md)

- [<span data-ttu-id="7577b-148">Lista nézet összetevők</span><span class="sxs-lookup"><span data-stu-id="7577b-148">List View Components</span></span>](./creating-a-list-view.md)

- [<span data-ttu-id="7577b-149">Széles nézet összetevők</span><span class="sxs-lookup"><span data-stu-id="7577b-149">Wide View Components</span></span>](./creating-a-wide-view.md)

- [<span data-ttu-id="7577b-150">Egyéni vezérlők</span><span class="sxs-lookup"><span data-stu-id="7577b-150">Custom Controls</span></span>](./creating-custom-controls.md)

## <a name="example"></a><span data-ttu-id="7577b-151">Példa</span><span class="sxs-lookup"><span data-stu-id="7577b-151">Example</span></span>

<span data-ttu-id="7577b-152">Ez a példa bemutatja egy `View` elem, amely meghatározza a táblázatos nézetre a [System.Serviceprocess.Servicecontroller](/dotnet/api/System.ServiceProcess.ServiceController) objektum.</span><span class="sxs-lookup"><span data-stu-id="7577b-152">This example shows a `View` element that defines a table view for the [System.Serviceprocess.Servicecontroller](/dotnet/api/System.ServiceProcess.ServiceController) object.</span></span>

```xml
<ViewDefinitions>
  <View>
    <Name>service</Name>
    <ViewSelectedBy>
      <TypeName>System.ServiceProcess.ServiceController</TypeName>
    </ViewSelectedBy>
    <TableControl>...</TableControl>
  </View>
</ViewDefinitions>

```

## <a name="see-also"></a><span data-ttu-id="7577b-153">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="7577b-153">See Also</span></span>

[<span data-ttu-id="7577b-154">ViewDefinitions elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="7577b-154">ViewDefinitions Element (Format)</span></span>](./viewdefinitions-element-format.md)

[<span data-ttu-id="7577b-155">Name elemet a nézet (formátum)</span><span class="sxs-lookup"><span data-stu-id="7577b-155">Name Element for View (Format)</span></span>](./name-element-for-view-format.md)

[<span data-ttu-id="7577b-156">ViewSelectedBy elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="7577b-156">ViewSelectedBy Element (Format)</span></span>](./viewselectedby-element-format.md)

[<span data-ttu-id="7577b-157">Vezérlők elem nézet (formátum)</span><span class="sxs-lookup"><span data-stu-id="7577b-157">Controls Element for View (Format)</span></span>](./controls-element-for-view-format.md)

[<span data-ttu-id="7577b-158">GroupBy elem nézet (formátum)</span><span class="sxs-lookup"><span data-stu-id="7577b-158">GroupBy Element for View (Format)</span></span>](./groupby-element-for-view-format.md)

[<span data-ttu-id="7577b-159">TableControl elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="7577b-159">TableControl Element (Format)</span></span>](./tablecontrol-element-format.md)

[<span data-ttu-id="7577b-160">ListControl elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="7577b-160">ListControl Element (Format)</span></span>](./listcontrol-element-format.md)

[<span data-ttu-id="7577b-161">WideControl elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="7577b-161">WideControl Element (Format)</span></span>](./widecontrol-element-format.md)

[<span data-ttu-id="7577b-162">CustomControl elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="7577b-162">CustomControl Element (Format)</span></span>](./customcontrol-element-for-groupby-format.md)

[<span data-ttu-id="7577b-163">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="7577b-163">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
