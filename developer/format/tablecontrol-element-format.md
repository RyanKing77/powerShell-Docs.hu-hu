---
title: TableControl elem (formátum) |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 1550b068-dfbc-4ae0-9aa1-72c9a680ec59
caps.latest.revision: 15
ms.openlocfilehash: 3942c008e026b0b99db3c77af4a0152b50fffc4e
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62063828"
---
# <a name="tablecontrol-element-format"></a><span data-ttu-id="b092a-102">TableControl elem (Formátum)</span><span class="sxs-lookup"><span data-stu-id="b092a-102">TableControl Element (Format)</span></span>

<span data-ttu-id="b092a-103">Határozza meg a nézet táblázatos formában.</span><span class="sxs-lookup"><span data-stu-id="b092a-103">Defines a table format for a view.</span></span>

<span data-ttu-id="b092a-104">ViewDefinitions elem (formátum) nézetben (formátum) elem TableControl elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="b092a-104">ViewDefinitions Element (Format) View Element (Format) TableControl Element (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="b092a-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="b092a-105">Syntax</span></span>

```xml
<TableControl>
  <AutoSize/>
  <HideTableHeaders/>
  <TableHeaders>...</TableHeaders>
  <TableRowEntries>...</TableRowEntries>
</TableControl>

```

## <a name="attributes-and-elements"></a><span data-ttu-id="b092a-106">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="b092a-106">Attributes and Elements</span></span>

<span data-ttu-id="b092a-107">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és szülőelemét a `TableControl` elemet.</span><span class="sxs-lookup"><span data-stu-id="b092a-107">The following sections describe attributes, child elements, and parent element of the `TableControl` element.</span></span> <span data-ttu-id="b092a-108">Meg kell adnia a tábla sorait.</span><span class="sxs-lookup"><span data-stu-id="b092a-108">You must specify the rows of the table.</span></span> <span data-ttu-id="b092a-109">Minden más alárendelt elemek egyike sem kötelező.</span><span class="sxs-lookup"><span data-stu-id="b092a-109">All other child elements are optional.</span></span>

### <a name="attributes"></a><span data-ttu-id="b092a-110">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="b092a-110">Attributes</span></span>

<span data-ttu-id="b092a-111">Nincs.</span><span class="sxs-lookup"><span data-stu-id="b092a-111">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="b092a-112">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="b092a-112">Child Elements</span></span>

|<span data-ttu-id="b092a-113">Elem</span><span class="sxs-lookup"><span data-stu-id="b092a-113">Element</span></span>|<span data-ttu-id="b092a-114">Leírás</span><span class="sxs-lookup"><span data-stu-id="b092a-114">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="b092a-115">Automatikus méretezés eleme TableControl (formátum)</span><span class="sxs-lookup"><span data-stu-id="b092a-115">AutoSize Element for TableControl (Format)</span></span>](./autosize-element-for-tablecontrol-format.md)|<span data-ttu-id="b092a-116">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="b092a-116">Optional element.</span></span><br /><br /> <span data-ttu-id="b092a-117">Itt adhatja meg, hogy az oszlop méretét és az oszlopok számát módosulnak az adatok mérete alapján.</span><span class="sxs-lookup"><span data-stu-id="b092a-117">Specifies whether the column size and the number of columns are adjusted based on the size of the data.</span></span>|
|[<span data-ttu-id="b092a-118">HideTableHeaders eleme TableControl (formátum)</span><span class="sxs-lookup"><span data-stu-id="b092a-118">HideTableHeaders Element for TableControl (Format)</span></span>](./hidetableheaders-element-format.md)|<span data-ttu-id="b092a-119">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="b092a-119">Optional element.</span></span><br /><br /> <span data-ttu-id="b092a-120">Azt jelzi, hogy a táblázat fejlécében nem jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="b092a-120">Indicates whether the header of the table is not displayed.</span></span>|
|[<span data-ttu-id="b092a-121">TableHeaders eleme TableControl (formátum)</span><span class="sxs-lookup"><span data-stu-id="b092a-121">TableHeaders Element for TableControl (Format)</span></span>](./tableheaders-element-format.md)|<span data-ttu-id="b092a-122">Szükséges eleme.</span><span class="sxs-lookup"><span data-stu-id="b092a-122">Required element.</span></span><br /><br /> <span data-ttu-id="b092a-123">A címkék a szélességet és az adatok az oszlopok a tábla nézet zarovnání határozza meg.</span><span class="sxs-lookup"><span data-stu-id="b092a-123">Defines the labels, the widths, and the alignment of the data for the columns of the table view.</span></span>|
|[<span data-ttu-id="b092a-124">TableRowEntries eleme TableControl (formátum)</span><span class="sxs-lookup"><span data-stu-id="b092a-124">TableRowEntries Element for TableControl (Format)</span></span>](./tablerowentries-element-for-tablecontrol-format.md)|<span data-ttu-id="b092a-125">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="b092a-125">Optional element.</span></span><br /><br /> <span data-ttu-id="b092a-126">A táblázatos nézetre a definíciókat tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="b092a-126">Provides the definitions of the table view.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="b092a-127">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="b092a-127">Parent Elements</span></span>

|<span data-ttu-id="b092a-128">Elem</span><span class="sxs-lookup"><span data-stu-id="b092a-128">Element</span></span>|<span data-ttu-id="b092a-129">Leírás</span><span class="sxs-lookup"><span data-stu-id="b092a-129">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="b092a-130">Nézet elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="b092a-130">View Element (Format)</span></span>](./view-element-format.md)|<span data-ttu-id="b092a-131">Meghatározza egy nézetet, amely egy vagy több objektum tagjait megjelenítésére szolgál.</span><span class="sxs-lookup"><span data-stu-id="b092a-131">Defines a view that is used to display the members of one or more objects.</span></span>|

## <a name="remarks"></a><span data-ttu-id="b092a-132">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="b092a-132">Remarks</span></span>

<span data-ttu-id="b092a-133">A táblázatos nézetre az összetevőivel kapcsolatos további információkért lásd: [tábla nézetek létrehozásával](./creating-a-table-view.md).</span><span class="sxs-lookup"><span data-stu-id="b092a-133">For more information about the components of a table view, see [Creating a Table View](./creating-a-table-view.md).</span></span>

## <a name="example"></a><span data-ttu-id="b092a-134">Példa</span><span class="sxs-lookup"><span data-stu-id="b092a-134">Example</span></span>

<span data-ttu-id="b092a-135">Ez a példa bemutatja egy `TableControl` elem, amellyel a tulajdonságainak megjelenítéséhez a [System.Serviceprocess.Servicecontroller](/dotnet/api/System.ServiceProcess.ServiceController) objektum.</span><span class="sxs-lookup"><span data-stu-id="b092a-135">This example shows a `TableControl` element that is used to display the properties of the [System.Serviceprocess.Servicecontroller](/dotnet/api/System.ServiceProcess.ServiceController) object.</span></span>

```xml
<View>
  <Name>service</Name>
  <ViewSelectedBy>
    <TypeName>System.ServiceProcess.ServiceController</TypeName>
  </ViewSelectedBy>
  <TableControl>
    <TableHeaders>...</TableHeaders>
    <TableRowEntries>...</TableRowEntries>
  </TableControl>
</View>

```

## <a name="see-also"></a><span data-ttu-id="b092a-136">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="b092a-136">See Also</span></span>

[<span data-ttu-id="b092a-137">Tábla nézet létrehozása</span><span class="sxs-lookup"><span data-stu-id="b092a-137">Creating a Table View</span></span>](./creating-a-table-view.md)

[<span data-ttu-id="b092a-138">Nézet elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="b092a-138">View Element (Format)</span></span>](./view-element-format.md)

[<span data-ttu-id="b092a-139">Automatikus méretezés eleme TableControl (formátum)</span><span class="sxs-lookup"><span data-stu-id="b092a-139">AutoSize Element for TableControl (Format)</span></span>](./autosize-element-for-tablecontrol-format.md)

[<span data-ttu-id="b092a-140">HideTableHeaders elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="b092a-140">HideTableHeaders Element (Format)</span></span>](./hidetableheaders-element-format.md)

[<span data-ttu-id="b092a-141">TableHeaders elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="b092a-141">TableHeaders Element (Format)</span></span>](./tableheaders-element-format.md)

[<span data-ttu-id="b092a-142">TableRowEntries elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="b092a-142">TableRowEntries Element (Format)</span></span>](./tablerowentries-element-for-tablecontrol-format.md)

[<span data-ttu-id="b092a-143">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="b092a-143">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
