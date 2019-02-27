---
title: WideControl elem (formátum) |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 715ea055-037b-46ad-b70f-87b3f5134403
caps.latest.revision: 14
ms.openlocfilehash: 2742be0389a1bf04af100a490a59c0d938165811
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56849489"
---
# <a name="widecontrol-element-format"></a><span data-ttu-id="444ea-102">WideControl elem (Formátum)</span><span class="sxs-lookup"><span data-stu-id="444ea-102">WideControl Element (Format)</span></span>

<span data-ttu-id="444ea-103">A wide (egyetlen érték) határozza meg a Nézet formátuma.</span><span class="sxs-lookup"><span data-stu-id="444ea-103">Defines a wide (single value) list format for the view.</span></span> <span data-ttu-id="444ea-104">Ez a nézet jeleníti meg, egy egyetlen tulajdonságát érték vagy parancsfájlt minden objektum esetén.</span><span class="sxs-lookup"><span data-stu-id="444ea-104">This view displays a single property value or script value for each object.</span></span>

<span data-ttu-id="444ea-105">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem WideControl elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="444ea-105">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) WideControl Element (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="444ea-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="444ea-106">Syntax</span></span>

```xml
<WideControl>
  <AutoSize/>
  <ColumnNumber>PositiveInteger</ColumnNumber>
  <WideEntries>...</WideEntries>
</WideControl>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="444ea-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="444ea-107">Attributes and Elements</span></span>

<span data-ttu-id="444ea-108">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és szülőelemét a `WideControl` elemet.</span><span class="sxs-lookup"><span data-stu-id="444ea-108">The following sections describe the attributes, child elements, and parent element of the `WideControl` element.</span></span> <span data-ttu-id="444ea-109">Nem adható meg a `AutoSize` és `ColumnNumber` elemek egy időben.</span><span class="sxs-lookup"><span data-stu-id="444ea-109">You cannot specify the `AutoSize` and `ColumnNumber` elements at the same time.</span></span>

### <a name="attributes"></a><span data-ttu-id="444ea-110">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="444ea-110">Attributes</span></span>

<span data-ttu-id="444ea-111">Nincs.</span><span class="sxs-lookup"><span data-stu-id="444ea-111">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="444ea-112">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="444ea-112">Child Elements</span></span>

|<span data-ttu-id="444ea-113">Elem</span><span class="sxs-lookup"><span data-stu-id="444ea-113">Element</span></span>|<span data-ttu-id="444ea-114">Leírás</span><span class="sxs-lookup"><span data-stu-id="444ea-114">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="444ea-115">Automatikus méretezés eleme WideControl (formátum)</span><span class="sxs-lookup"><span data-stu-id="444ea-115">AutoSize Element for WideControl (Format)</span></span>](./autosize-element-for-widecontrol-format.md)|<span data-ttu-id="444ea-116">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="444ea-116">Optional element.</span></span><br /><br /> <span data-ttu-id="444ea-117">Itt adhatja meg, hogy az oszlop méretét és az oszlopok számát módosulnak az adatok mérete alapján.</span><span class="sxs-lookup"><span data-stu-id="444ea-117">Specifies whether the column size and the number of columns are adjusted based on the size of the data.</span></span>|
|[<span data-ttu-id="444ea-118">ColumnNumber eleme WideControl (formátum)</span><span class="sxs-lookup"><span data-stu-id="444ea-118">ColumnNumber Element for WideControl (Format)</span></span>](./columnnumber-element-for-widecontrol-format.md)|<span data-ttu-id="444ea-119">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="444ea-119">Optional element.</span></span><br /><br /> <span data-ttu-id="444ea-120">A széles nézet oszlopainak számát adja meg.</span><span class="sxs-lookup"><span data-stu-id="444ea-120">Specifies the number of columns displayed in the wide view.</span></span>|
|[<span data-ttu-id="444ea-121">WideEntries elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="444ea-121">WideEntries Element (Format)</span></span>](./wideentries-element-for-widecontrol-format.md)|<span data-ttu-id="444ea-122">Szükséges eleme.</span><span class="sxs-lookup"><span data-stu-id="444ea-122">Required element.</span></span><br /><br /> <span data-ttu-id="444ea-123">A széles nézet a definíciókat tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="444ea-123">Provides the definitions of the wide view.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="444ea-124">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="444ea-124">Parent Elements</span></span>

|<span data-ttu-id="444ea-125">Elem</span><span class="sxs-lookup"><span data-stu-id="444ea-125">Element</span></span>|<span data-ttu-id="444ea-126">Leírás</span><span class="sxs-lookup"><span data-stu-id="444ea-126">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="444ea-127">Nézet elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="444ea-127">View Element (Format)</span></span>](./view-element-format.md)|<span data-ttu-id="444ea-128">Meghatározza egy nézetet, amely legalább egy .NET-objektumokká megjelenítésére szolgál.</span><span class="sxs-lookup"><span data-stu-id="444ea-128">Defines a view that is used to display one or more .NET objects.</span></span>|

## <a name="remarks"></a><span data-ttu-id="444ea-129">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="444ea-129">Remarks</span></span>

<span data-ttu-id="444ea-130">Egy széles nézet meghatározásakor adhat hozzá a `AutoSize` elem vagy a `ColumnNumber` , de nem adja hozzá mindkettőt.</span><span class="sxs-lookup"><span data-stu-id="444ea-130">When defining a wide view, you can add the `AutoSize` element or the `ColumnNumber` but you cannot add both.</span></span>

<span data-ttu-id="444ea-131">A legtöbb esetben csak egyetlen definíciót minden széles nézet megadása kötelező, de lehetséges több definíciókkal rendelkeznek, ha ugyanabban a nézetben különböző .NET-objektumok megjelenítéséhez használandó.</span><span class="sxs-lookup"><span data-stu-id="444ea-131">In most cases, only one definition is required for each wide view, but it is possible to have multiple definitions if you want to use the same view to display different .NET objects.</span></span> <span data-ttu-id="444ea-132">Ezekben az esetekben adja meg egy külön meghatározása az egyes objektumok vagy objektumok közül.</span><span class="sxs-lookup"><span data-stu-id="444ea-132">In those cases, you can provide a separate definition for each object or set of objects.</span></span>

<span data-ttu-id="444ea-133">Egy széles nézet az összetevőivel kapcsolatos további információkért lásd: [széles nézet összetevők](./creating-a-wide-view.md).</span><span class="sxs-lookup"><span data-stu-id="444ea-133">For more information about the components of a wide view, see [Wide View Components](./creating-a-wide-view.md).</span></span>

## <a name="example"></a><span data-ttu-id="444ea-134">Példa</span><span class="sxs-lookup"><span data-stu-id="444ea-134">Example</span></span>

<span data-ttu-id="444ea-135">A következő példa bemutatja egy `WideControl` elem, amely egy tulajdonságának megjelenítéséhez használja a [System.Diagnostics.Process](/dotnet/api/System.Diagnostics.Process) objektum.</span><span class="sxs-lookup"><span data-stu-id="444ea-135">The following example shows a `WideControl` element that is used to display a property of the [System.Diagnostics.Process](/dotnet/api/System.Diagnostics.Process) object.</span></span>

```xml
<View>
  <Name>process</Name>
  <ViewSelectedBy>
    <TypeName>System.Diagnostics.Process</TypeName>
  </ViewSelectedBy>
  <WideControl>
    <WideEntries>...</WideEntries>
  </WideControl>
</View>
```

<span data-ttu-id="444ea-136">Egy széles nézet egy teljes példa: [széles nézet (alapszintű)](./wide-view-basic.md).</span><span class="sxs-lookup"><span data-stu-id="444ea-136">For a complete example of a wide view, see [Wide View (Basic)](./wide-view-basic.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="444ea-137">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="444ea-137">See Also</span></span>

[<span data-ttu-id="444ea-138">Automatikus méretezés eleme WideControl (formátum)</span><span class="sxs-lookup"><span data-stu-id="444ea-138">Autosize Element for WideControl (Format)</span></span>](./autosize-element-for-widecontrol-format.md)

[<span data-ttu-id="444ea-139">ColumnNumber eleme WideControl (formátum)</span><span class="sxs-lookup"><span data-stu-id="444ea-139">ColumnNumber Element for WideControl (Format)</span></span>](./columnnumber-element-for-widecontrol-format.md)

[<span data-ttu-id="444ea-140">Nézet elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="444ea-140">View Element (Format)</span></span>](./view-element-format.md)

[<span data-ttu-id="444ea-141">WideEntries elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="444ea-141">WideEntries Element (Format)</span></span>](./wideentries-element-for-widecontrol-format.md)

[<span data-ttu-id="444ea-142">Széles nézet (alapszintű)</span><span class="sxs-lookup"><span data-stu-id="444ea-142">Wide View (Basic)</span></span>](./wide-view-basic.md)

[<span data-ttu-id="444ea-143">Egy széles nézet létrehozása</span><span class="sxs-lookup"><span data-stu-id="444ea-143">Creating a Wide View</span></span>](./creating-a-wide-view.md)

[<span data-ttu-id="444ea-144">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="444ea-144">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
