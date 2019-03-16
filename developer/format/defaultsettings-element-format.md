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
ms.openlocfilehash: bc95c62222eb2806f92499257a397c2e4ec5dbab
ms.sourcegitcommit: caac7d098a448232304c9d6728e7340ec7517a71
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/16/2019
ms.locfileid: "58059065"
---
# <a name="defaultsettings-element-format"></a><span data-ttu-id="14f45-102">DefaultSettings elem (Formátum)</span><span class="sxs-lookup"><span data-stu-id="14f45-102">DefaultSettings Element (Format)</span></span>

<span data-ttu-id="14f45-103">Határozza meg a formázási fájl összes nézet vonatkozó általános beállításokat.</span><span class="sxs-lookup"><span data-stu-id="14f45-103">Defines common settings that apply to all the views of the formatting file.</span></span> <span data-ttu-id="14f45-104">Általános beállítások közé tartozik a hibák megjelenítése a táblákat, hogyan gyűjtemények vannak bontva, definiálása, valamint további lehetőségek szöveg.</span><span class="sxs-lookup"><span data-stu-id="14f45-104">Common settings include displaying errors, wrapping text in tables, defining how collections are expanded, and more.</span></span>

<span data-ttu-id="14f45-105">Konfigurációs elem (formátum) DefaultSettings elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="14f45-105">Configuration Element (Format) DefaultSettings Element (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="14f45-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="14f45-106">Syntax</span></span>

```xml
<DefaultSettings>
  <ShowError/>
  <DisplayError/>
 <PropertyCountForTable>NumberOfProperties</PropertyCountFortable>
  <WrapTables/>
  <EnumerableExpansions>...</EnumerableExpansions>
</DefaultSettings>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="14f45-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="14f45-107">Attributes and Elements</span></span>

<span data-ttu-id="14f45-108">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `DefaultSettings` elemet.</span><span class="sxs-lookup"><span data-stu-id="14f45-108">The following sections describe attributes, child elements, and the parent element of the `DefaultSettings` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="14f45-109">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="14f45-109">Attributes</span></span>

<span data-ttu-id="14f45-110">Nincs.</span><span class="sxs-lookup"><span data-stu-id="14f45-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="14f45-111">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="14f45-111">Child Elements</span></span>

|<span data-ttu-id="14f45-112">Elem</span><span class="sxs-lookup"><span data-stu-id="14f45-112">Element</span></span>|<span data-ttu-id="14f45-113">Leírás</span><span class="sxs-lookup"><span data-stu-id="14f45-113">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="14f45-114">DisplayError elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="14f45-114">DisplayError Element (Format)</span></span>](./displayerror-element-format.md)|<span data-ttu-id="14f45-115">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="14f45-115">Optional element.</span></span><br /><br /> <span data-ttu-id="14f45-116">Itt adhatja meg, hogy a karakterlánc #ERR megjelenik-e, ha hiba történik az adatok megjelenítése közben.</span><span class="sxs-lookup"><span data-stu-id="14f45-116">Specifies that the string #ERR is displayed when an error occurs while displaying a piece of data.</span></span>|
|[<span data-ttu-id="14f45-117">EnumerableExpansions elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="14f45-117">EnumerableExpansions Element (Format)</span></span>](./enumerableexpansions-element-format.md)|<span data-ttu-id="14f45-118">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="14f45-118">Optional element.</span></span><br /><br /> <span data-ttu-id="14f45-119">Meghatározza a .NET-vannak bontva, amikor a nézetben megjelenített objektumok különböző lehetőségeket.</span><span class="sxs-lookup"><span data-stu-id="14f45-119">Defines the different ways that .NET objects are expanded when they are displayed in a view.</span></span>|
|[<span data-ttu-id="14f45-120">PropertyCountForTable (formátum)</span><span class="sxs-lookup"><span data-stu-id="14f45-120">PropertyCountForTable (Format)</span></span>](./propertycountfortable-element-format.md)|<span data-ttu-id="14f45-121">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="14f45-121">Optional element.</span></span><br /><br /> <span data-ttu-id="14f45-122">Meghatározza, hogy az objektum táblázatos nézetre az objektum megjelenítendő tulajdonságai minimális számát.</span><span class="sxs-lookup"><span data-stu-id="14f45-122">Specifies the minimum number of properties that an object must have to display the object in a table view.</span></span>|
|[<span data-ttu-id="14f45-123">ShowError elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="14f45-123">ShowError Element (Format)</span></span>](./showerror-element-format.md)|<span data-ttu-id="14f45-124">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="14f45-124">Optional element.</span></span><br /><br /> <span data-ttu-id="14f45-125">Itt adhatja meg, hogy megjelenik-e a teljes rekordot, ha hiba történik az adatok megjelenítése közben.</span><span class="sxs-lookup"><span data-stu-id="14f45-125">Specifies that the full error record is displayed when an error occurs while displaying a piece of data.</span></span>|
|[<span data-ttu-id="14f45-126">WrapTables elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="14f45-126">WrapTables Element (Format)</span></span>](./wraptables-element-format.md)|<span data-ttu-id="14f45-127">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="14f45-127">Optional element.</span></span><br /><br /> <span data-ttu-id="14f45-128">Itt adhatja meg, hogy a tábla adatainak áthelyezése a következő sorra, ha az oszlop szélessége nem illik-e.</span><span class="sxs-lookup"><span data-stu-id="14f45-128">Specifies that data in a table is moved to the next line if it does not fit into the width of the column.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="14f45-129">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="14f45-129">Parent Elements</span></span>

|<span data-ttu-id="14f45-130">Elem</span><span class="sxs-lookup"><span data-stu-id="14f45-130">Element</span></span>|<span data-ttu-id="14f45-131">Leírás</span><span class="sxs-lookup"><span data-stu-id="14f45-131">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="14f45-132">Konfigurációs elem</span><span class="sxs-lookup"><span data-stu-id="14f45-132">Configuration Element</span></span>](./configuration-element-format.md)|<span data-ttu-id="14f45-133">A legfelső szintű elem egy formázási fájl jelöli.</span><span class="sxs-lookup"><span data-stu-id="14f45-133">Represents the top-level element of a formatting file.</span></span>|

## <a name="remarks"></a><span data-ttu-id="14f45-134">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="14f45-134">Remarks</span></span>

## <a name="see-also"></a><span data-ttu-id="14f45-135">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="14f45-135">See Also</span></span>

[<span data-ttu-id="14f45-136">Konfigurációs elem</span><span class="sxs-lookup"><span data-stu-id="14f45-136">Configuration Element</span></span>](./configuration-element-format.md)

[<span data-ttu-id="14f45-137">DisplayError elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="14f45-137">DisplayError Element (Format)</span></span>](./displayerror-element-format.md)

[<span data-ttu-id="14f45-138">EnumerableExpansions elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="14f45-138">EnumerableExpansions Element (Format)</span></span>](./enumerableexpansions-element-format.md)

[<span data-ttu-id="14f45-139">PropertyCountForTable (formátum)</span><span class="sxs-lookup"><span data-stu-id="14f45-139">PropertyCountForTable (Format)</span></span>](./propertycountfortable-element-format.md)

[<span data-ttu-id="14f45-140">ShowError elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="14f45-140">ShowError Element (Format)</span></span>](./showerror-element-format.md)

[<span data-ttu-id="14f45-141">WrapTables elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="14f45-141">WrapTables Element (Format)</span></span>](./wraptables-element-format.md)

[<span data-ttu-id="14f45-142">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="14f45-142">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
