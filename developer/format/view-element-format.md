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
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56846913"
---
# <a name="view-element-format"></a><span data-ttu-id="43766-102">Nézet elem (Formátum)</span><span class="sxs-lookup"><span data-stu-id="43766-102">View Element (Format)</span></span>

<span data-ttu-id="43766-103">Legalább egy .NET-objektumokat megjelenítő nézet határozza meg.</span><span class="sxs-lookup"><span data-stu-id="43766-103">Defines a view that displays one or more .NET objects.</span></span> <span data-ttu-id="43766-104">Formázási-fájlban definiált nézetek száma nincs korlátozva van.</span><span class="sxs-lookup"><span data-stu-id="43766-104">There is no limit to the number of views that can be defined in a formatting file.</span></span>

<span data-ttu-id="43766-105">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézet elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="43766-105">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="43766-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="43766-106">Syntax</span></span>

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

## <a name="attributes-and-elements"></a><span data-ttu-id="43766-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="43766-107">Attributes and Elements</span></span>

<span data-ttu-id="43766-108">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `View` elemet.</span><span class="sxs-lookup"><span data-stu-id="43766-108">The following sections describe the attributes, child elements, and the parent element of the `View` element.</span></span> <span data-ttu-id="43766-109">Meg kell adnia az egyiket a vezérlő gyermekelemek, és meg kell adnia a nézet és az objektumok, amelyek a nézet nevét.</span><span class="sxs-lookup"><span data-stu-id="43766-109">You must specify one and only one of the control child elements, and you must specify the name of the view and the objects that use the view.</span></span> <span data-ttu-id="43766-110">Egyéni vezérlők meghatározása, hogyan csoportosítsa objektumokat, és ha a nézet-e a sávon kívüli megadása nem kötelező.</span><span class="sxs-lookup"><span data-stu-id="43766-110">Defining custom controls, how to group objects, and specifying if the view is out-of-band are optional.</span></span>

### <a name="attributes"></a><span data-ttu-id="43766-111">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="43766-111">Attributes</span></span>

<span data-ttu-id="43766-112">Nincs.</span><span class="sxs-lookup"><span data-stu-id="43766-112">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="43766-113">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="43766-113">Child Elements</span></span>

|<span data-ttu-id="43766-114">Elem</span><span class="sxs-lookup"><span data-stu-id="43766-114">Element</span></span>|<span data-ttu-id="43766-115">Leírás</span><span class="sxs-lookup"><span data-stu-id="43766-115">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="43766-116">Vezérlők elem nézet (formátum)</span><span class="sxs-lookup"><span data-stu-id="43766-116">Controls Element for View (Format)</span></span>](./controls-element-for-view-format.md)|<span data-ttu-id="43766-117">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="43766-117">Optional element.</span></span><br /><br /> <span data-ttu-id="43766-118">Határozza meg, hogy a nézet belül vezérlőelemére név szerint lehet hivatkozni.</span><span class="sxs-lookup"><span data-stu-id="43766-118">Defines a set of controls that can be referenced by their name from within the view.</span></span>|
|[<span data-ttu-id="43766-119">CustomControl elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="43766-119">CustomControl Element (Format)</span></span>](./customcontrol-element-for-groupby-format.md)|<span data-ttu-id="43766-120">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="43766-120">Optional element.</span></span><br /><br /> <span data-ttu-id="43766-121">A nézet egy egyéni vezérlő formátumát határozza meg.</span><span class="sxs-lookup"><span data-stu-id="43766-121">Defines a custom control format for the view.</span></span>|
|[<span data-ttu-id="43766-122">GroupBy elem nézet (formátum)</span><span class="sxs-lookup"><span data-stu-id="43766-122">GroupBy Element for View (Format)</span></span>](./groupby-element-for-view-format.md)|<span data-ttu-id="43766-123">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="43766-123">Optional element.</span></span><br /><br /> <span data-ttu-id="43766-124">Határozza meg, hogy a .NET-objektumok tagjai vannak csoportosítva.</span><span class="sxs-lookup"><span data-stu-id="43766-124">Defines how the members of the .NET objects are grouped.</span></span>|
|[<span data-ttu-id="43766-125">ListControl elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="43766-125">ListControl Element (Format)</span></span>](./listcontrol-element-format.md)|<span data-ttu-id="43766-126">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="43766-126">Optional element.</span></span><br /><br /> <span data-ttu-id="43766-127">Határozza meg a nézet lista formájában.</span><span class="sxs-lookup"><span data-stu-id="43766-127">Defines a list format for the view.</span></span>|
|[<span data-ttu-id="43766-128">Name elemet a nézet (formátum)</span><span class="sxs-lookup"><span data-stu-id="43766-128">Name Element for View (Format)</span></span>](./name-element-for-view-format.md)|<span data-ttu-id="43766-129">Szükséges eleme.</span><span class="sxs-lookup"><span data-stu-id="43766-129">Required element.</span></span><br /><br /> <span data-ttu-id="43766-130">Megadja a mutató hivatkozás a nézet nevét.</span><span class="sxs-lookup"><span data-stu-id="43766-130">Specifies the name used to reference the view.</span></span>|
|[<span data-ttu-id="43766-131">TableControl elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="43766-131">TableControl Element (Format)</span></span>](./tablecontrol-element-format.md)|<span data-ttu-id="43766-132">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="43766-132">Optional element.</span></span><br /><br /> <span data-ttu-id="43766-133">Határozza meg a nézet táblázatos formában.</span><span class="sxs-lookup"><span data-stu-id="43766-133">Defines a table format for the view.</span></span>|
|[<span data-ttu-id="43766-134">ViewSelectedBy elem nézet (formátum)</span><span class="sxs-lookup"><span data-stu-id="43766-134">ViewSelectedBy Element for View (Format)</span></span>](./viewselectedby-element-format.md)|<span data-ttu-id="43766-135">Szükséges eleme.</span><span class="sxs-lookup"><span data-stu-id="43766-135">Required element.</span></span><br /><br /> <span data-ttu-id="43766-136">Határozza meg, hogy ez a nézet jeleníti meg a .NET-objektumokat.</span><span class="sxs-lookup"><span data-stu-id="43766-136">Defines the .NET objects that this view displays.</span></span>|
|[<span data-ttu-id="43766-137">WideControl elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="43766-137">WideControl Element (Format)</span></span>](./widecontrol-element-format.md)|<span data-ttu-id="43766-138">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="43766-138">Optional element.</span></span><br /><br /> <span data-ttu-id="43766-139">A wide (egyetlen érték) határozza meg a Nézet formátuma.</span><span class="sxs-lookup"><span data-stu-id="43766-139">Defines a wide (single value) list format for the view.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="43766-140">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="43766-140">Parent Elements</span></span>

|<span data-ttu-id="43766-141">Elem</span><span class="sxs-lookup"><span data-stu-id="43766-141">Element</span></span>|<span data-ttu-id="43766-142">Leírás</span><span class="sxs-lookup"><span data-stu-id="43766-142">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="43766-143">ViewDefinitions elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="43766-143">ViewDefinitions Element (Format)</span></span>](./viewdefinitions-element-format.md)|<span data-ttu-id="43766-144">Határozza meg az objektumokat megjelenítő nézetek.</span><span class="sxs-lookup"><span data-stu-id="43766-144">Defines the views used to display objects.</span></span>|

## <a name="remarks"></a><span data-ttu-id="43766-145">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="43766-145">Remarks</span></span>

<span data-ttu-id="43766-146">A különböző nézetek és az egyéni vezérlők az összetevőivel kapcsolatos további információkért lásd a következő témaköröket:</span><span class="sxs-lookup"><span data-stu-id="43766-146">For more information about the components of different views and custom controls, see the following topics:</span></span>

- [<span data-ttu-id="43766-147">Tábla nézet összetevők</span><span class="sxs-lookup"><span data-stu-id="43766-147">Table View Components</span></span>](./creating-a-table-view.md)

- [<span data-ttu-id="43766-148">Lista nézet összetevők</span><span class="sxs-lookup"><span data-stu-id="43766-148">List View Components</span></span>](./creating-a-list-view.md)

- [<span data-ttu-id="43766-149">Széles nézet összetevők</span><span class="sxs-lookup"><span data-stu-id="43766-149">Wide View Components</span></span>](./creating-a-wide-view.md)

- [<span data-ttu-id="43766-150">Egyéni vezérlők</span><span class="sxs-lookup"><span data-stu-id="43766-150">Custom Controls</span></span>](./creating-custom-controls.md)

## <a name="example"></a><span data-ttu-id="43766-151">Példa</span><span class="sxs-lookup"><span data-stu-id="43766-151">Example</span></span>

<span data-ttu-id="43766-152">Ez a példa bemutatja egy `View` elem, amely meghatározza a táblázatos nézetre a [System.Serviceprocess.Servicecontroller](/dotnet/api/System.ServiceProcess.ServiceController) objektum.</span><span class="sxs-lookup"><span data-stu-id="43766-152">This example shows a `View` element that defines a table view for the [System.Serviceprocess.Servicecontroller](/dotnet/api/System.ServiceProcess.ServiceController) object.</span></span>

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

## <a name="see-also"></a><span data-ttu-id="43766-153">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="43766-153">See Also</span></span>

[<span data-ttu-id="43766-154">ViewDefinitions elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="43766-154">ViewDefinitions Element (Format)</span></span>](./viewdefinitions-element-format.md)

[<span data-ttu-id="43766-155">Name elemet a nézet (formátum)</span><span class="sxs-lookup"><span data-stu-id="43766-155">Name Element for View (Format)</span></span>](./name-element-for-view-format.md)

[<span data-ttu-id="43766-156">ViewSelectedBy elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="43766-156">ViewSelectedBy Element (Format)</span></span>](./viewselectedby-element-format.md)

[<span data-ttu-id="43766-157">Vezérlők elem nézet (formátum)</span><span class="sxs-lookup"><span data-stu-id="43766-157">Controls Element for View (Format)</span></span>](./controls-element-for-view-format.md)

[<span data-ttu-id="43766-158">GroupBy elem nézet (formátum)</span><span class="sxs-lookup"><span data-stu-id="43766-158">GroupBy Element for View (Format)</span></span>](./groupby-element-for-view-format.md)

[<span data-ttu-id="43766-159">TableControl elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="43766-159">TableControl Element (Format)</span></span>](./tablecontrol-element-format.md)

[<span data-ttu-id="43766-160">ListControl elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="43766-160">ListControl Element (Format)</span></span>](./listcontrol-element-format.md)

[<span data-ttu-id="43766-161">WideControl elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="43766-161">WideControl Element (Format)</span></span>](./widecontrol-element-format.md)

[<span data-ttu-id="43766-162">CustomControl elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="43766-162">CustomControl Element (Format)</span></span>](./customcontrol-element-for-groupby-format.md)

[<span data-ttu-id="43766-163">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="43766-163">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
