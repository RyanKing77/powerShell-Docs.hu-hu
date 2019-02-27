---
title: DefaultSettings elem (formátum) |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 41c56499-ee20-4821-830a-478fdcc33f83
caps.latest.revision: 11
ms.openlocfilehash: 59cc0514087cc52438e0d1271b8b77a7799eb32c
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56846577"
---
# <a name="defaultsettings-element-format"></a><span data-ttu-id="8d9d4-102">DefaultSettings elem (Formátum)</span><span class="sxs-lookup"><span data-stu-id="8d9d4-102">DefaultSettings Element (Format)</span></span>

<span data-ttu-id="8d9d4-103">Határozza meg a formázási fájl összes nézet vonatkozó általános beállításokat.</span><span class="sxs-lookup"><span data-stu-id="8d9d4-103">Defines common settings that apply to all the views of the formatting file.</span></span> <span data-ttu-id="8d9d4-104">Általános beállítások közé tartozik a hibák megjelenítése a táblákat, hogyan gyűjtemények vannak bontva, definiálása, valamint további lehetőségek szöveg.</span><span class="sxs-lookup"><span data-stu-id="8d9d4-104">Common settings include displaying errors, wrapping text in tables, defining how collections are expanded, and more.</span></span>

<span data-ttu-id="8d9d4-105">Konfigurációs elem (formátum) DefaultSettings elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="8d9d4-105">Configuration Element (Format) DefaultSettings Element (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="8d9d4-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="8d9d4-106">Syntax</span></span>

```xml
<DefaultSettings>
  <ShowError/>
  <DisplayError/>
 <PropertyCountForTable>NumberOfProperties</PropertyCountFortable>
  <WrapTables/>
  <EnumerableExpansions>...</EnumerableExpansions>
</DefaultSettings>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="8d9d4-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="8d9d4-107">Attributes and Elements</span></span>

<span data-ttu-id="8d9d4-108">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `DefaultSettings` elemet.</span><span class="sxs-lookup"><span data-stu-id="8d9d4-108">The following sections describe attributes, child elements, and the parent element of the `DefaultSettings` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="8d9d4-109">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="8d9d4-109">Attributes</span></span>

<span data-ttu-id="8d9d4-110">Nincs.</span><span class="sxs-lookup"><span data-stu-id="8d9d4-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="8d9d4-111">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="8d9d4-111">Child Elements</span></span>

|<span data-ttu-id="8d9d4-112">Elem</span><span class="sxs-lookup"><span data-stu-id="8d9d4-112">Element</span></span>|<span data-ttu-id="8d9d4-113">Leírás</span><span class="sxs-lookup"><span data-stu-id="8d9d4-113">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="8d9d4-114">DisplayError elem (Frmat)</span><span class="sxs-lookup"><span data-stu-id="8d9d4-114">DisplayError Element (Frmat)</span></span>](./displayerror-element-format.md)|<span data-ttu-id="8d9d4-115">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="8d9d4-115">Optional element.</span></span><br /><br /> <span data-ttu-id="8d9d4-116">Itt adhatja meg, hogy a karakterlánc #ERR megjelenik-e, ha hiba történik az adatok megjelenítése közben.</span><span class="sxs-lookup"><span data-stu-id="8d9d4-116">Specifies that the string #ERR is displayed when an error occurs while displaying a piece of data.</span></span>|
|[<span data-ttu-id="8d9d4-117">EnumerableExpansions elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="8d9d4-117">EnumerableExpansions Element (Format)</span></span>](./enumerableexpansions-element-format.md)|<span data-ttu-id="8d9d4-118">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="8d9d4-118">Optional element.</span></span><br /><br /> <span data-ttu-id="8d9d4-119">Meghatározza a .NET-vannak bontva, amikor a nézetben megjelenített objektumok különböző lehetőségeket.</span><span class="sxs-lookup"><span data-stu-id="8d9d4-119">Defines the different ways that .NET objects are expanded when they are displayed in a view.</span></span>|
|[<span data-ttu-id="8d9d4-120">PropertyCountForTable (formátum)</span><span class="sxs-lookup"><span data-stu-id="8d9d4-120">PropertyCountForTable (Format)</span></span>](./propertycountfortable-element-format.md)|<span data-ttu-id="8d9d4-121">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="8d9d4-121">Optional element.</span></span><br /><br /> <span data-ttu-id="8d9d4-122">Meghatározza, hogy az objektum táblázatos nézetre az objektum megjelenítendő tulajdonságai minimális számát.</span><span class="sxs-lookup"><span data-stu-id="8d9d4-122">Specifies the minimum number of properties that an object must have to display the object in a table view.</span></span>|
|[<span data-ttu-id="8d9d4-123">ShowError elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="8d9d4-123">ShowError Element (Format)</span></span>](./showerror-element-format.md)|<span data-ttu-id="8d9d4-124">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="8d9d4-124">Optional element.</span></span><br /><br /> <span data-ttu-id="8d9d4-125">Itt adhatja meg, hogy megjelenik-e a teljes rekordot, ha hiba történik az adatok megjelenítése közben.</span><span class="sxs-lookup"><span data-stu-id="8d9d4-125">Specifies that the full error record is displayed when an error occurs while displaying a piece of data.</span></span>|
|[<span data-ttu-id="8d9d4-126">WrapTables elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="8d9d4-126">WrapTables Element (Format)</span></span>](./wraptables-element-format.md)|<span data-ttu-id="8d9d4-127">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="8d9d4-127">Optional element.</span></span><br /><br /> <span data-ttu-id="8d9d4-128">Itt adhatja meg, hogy a tábla adatainak áthelyezése a következő sorra, ha az oszlop szélessége nem illik-e.</span><span class="sxs-lookup"><span data-stu-id="8d9d4-128">Specifies that data in a table is moved to the next line if it does not fit into the width of the column.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="8d9d4-129">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="8d9d4-129">Parent Elements</span></span>

|<span data-ttu-id="8d9d4-130">Elem</span><span class="sxs-lookup"><span data-stu-id="8d9d4-130">Element</span></span>|<span data-ttu-id="8d9d4-131">Leírás</span><span class="sxs-lookup"><span data-stu-id="8d9d4-131">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="8d9d4-132">Konfigurációs elem</span><span class="sxs-lookup"><span data-stu-id="8d9d4-132">Configuration Element</span></span>](./configuration-element-format.md)|<span data-ttu-id="8d9d4-133">A legfelső szintű elem egy formázási fájl jelöli.</span><span class="sxs-lookup"><span data-stu-id="8d9d4-133">Represents the top-level element of a formatting file.</span></span>|

## <a name="remarks"></a><span data-ttu-id="8d9d4-134">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="8d9d4-134">Remarks</span></span>

## <a name="see-also"></a><span data-ttu-id="8d9d4-135">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="8d9d4-135">See Also</span></span>

[<span data-ttu-id="8d9d4-136">Konfigurációs elem</span><span class="sxs-lookup"><span data-stu-id="8d9d4-136">Configuration Element</span></span>](./configuration-element-format.md)

[<span data-ttu-id="8d9d4-137">DisplayError elem (Frmat)</span><span class="sxs-lookup"><span data-stu-id="8d9d4-137">DisplayError Element (Frmat)</span></span>](./displayerror-element-format.md)

[<span data-ttu-id="8d9d4-138">EnumerableExpansions elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="8d9d4-138">EnumerableExpansions Element (Format)</span></span>](./enumerableexpansions-element-format.md)

[<span data-ttu-id="8d9d4-139">PropertyCountForTable (formátum)</span><span class="sxs-lookup"><span data-stu-id="8d9d4-139">PropertyCountForTable (Format)</span></span>](./propertycountfortable-element-format.md)

[<span data-ttu-id="8d9d4-140">ShowError elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="8d9d4-140">ShowError Element (Format)</span></span>](./showerror-element-format.md)

[<span data-ttu-id="8d9d4-141">WrapTables elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="8d9d4-141">WrapTables Element (Format)</span></span>](./wraptables-element-format.md)

[<span data-ttu-id="8d9d4-142">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="8d9d4-142">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
