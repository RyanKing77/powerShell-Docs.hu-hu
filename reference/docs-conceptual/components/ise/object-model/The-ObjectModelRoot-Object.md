---
ms.date: 08/25/2017
keywords: PowerShell, a parancsmag
title: Az ObjectModelRoot objektum
ms.openlocfilehash: 2670321ebac1eac4ecc8457afb796f9f260da471
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55684373"
---
# <a name="the-objectmodelroot-object"></a><span data-ttu-id="9d68f-103">Az ObjectModelRoot objektum</span><span class="sxs-lookup"><span data-stu-id="9d68f-103">The ObjectModelRoot Object</span></span>

<span data-ttu-id="9d68f-104">A **$psISE** objektum, amely a Windows PowerShell® integrált parancsfájl-kezelési környezet (ISE) egyszerű gyökérszintű objektum a Microsoft.PowerShell.Host.ISE.ObjectModelRoot osztály egy példányát.</span><span class="sxs-lookup"><span data-stu-id="9d68f-104">The **$psISE** object, which is the principal root object in Windows PowerShell® Integrated Scripting Environment (ISE) is an instance of the Microsoft.PowerShell.Host.ISE.ObjectModelRoot class.</span></span>
<span data-ttu-id="9d68f-105">Ez a témakör ismerteti a tulajdonságait a **ObjectModelRoot** objektum.</span><span class="sxs-lookup"><span data-stu-id="9d68f-105">This topic describes the properties of the **ObjectModelRoot** object.</span></span>

## <a name="properties"></a><span data-ttu-id="9d68f-106">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="9d68f-106">Properties</span></span>

### <a name="currentfile"></a><span data-ttu-id="9d68f-107">CurrentFile</span><span class="sxs-lookup"><span data-stu-id="9d68f-107">CurrentFile</span></span>

> <span data-ttu-id="9d68f-108">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="9d68f-108">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="9d68f-109">A csak olvasható tulajdonság, amely lekérdezi a fájlt, amely a gazdagép objektum, amely a fókusz van társítva.</span><span class="sxs-lookup"><span data-stu-id="9d68f-109">The read-only property that gets the file, which is associated with this host object that currently has the focus.</span></span>

### <a name="currentpowershelltab"></a><span data-ttu-id="9d68f-110">CurrentPowerShellTab</span><span class="sxs-lookup"><span data-stu-id="9d68f-110">CurrentPowerShellTab</span></span>

> <span data-ttu-id="9d68f-111">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="9d68f-111">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="9d68f-112">A csak olvasható tulajdonság, amely lekérdezi a PowerShell-lap, amely rendelkezik a fókuszt.</span><span class="sxs-lookup"><span data-stu-id="9d68f-112">The read-only property that gets the PowerShell tab that has the focus.</span></span>

### <a name="currentvisiblehorizontaltool"></a><span data-ttu-id="9d68f-113">CurrentVisibleHorizontalTool</span><span class="sxs-lookup"><span data-stu-id="9d68f-113">CurrentVisibleHorizontalTool</span></span>

> <span data-ttu-id="9d68f-114">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="9d68f-114">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="9d68f-115">A csak olvasható tulajdonság, amely a jelenleg látható Windows PowerShell ISE-bővítmény eszköz, amely lekérdezi a vízszintes eszköz panel alsó részén a szerkesztő található.</span><span class="sxs-lookup"><span data-stu-id="9d68f-115">The read-only property that gets the currently visible Windows PowerShell ISE add-on tool that is located in the horizontal tool pane at the bottom of the editor.</span></span>

### <a name="currentvisibleverticaltool"></a><span data-ttu-id="9d68f-116">CurrentVisibleVerticalTool</span><span class="sxs-lookup"><span data-stu-id="9d68f-116">CurrentVisibleVerticalTool</span></span>

> <span data-ttu-id="9d68f-117">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="9d68f-117">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="9d68f-118">A csak olvasható tulajdonság, amely a jelenleg látható Windows PowerShell ISE-bővítmény eszköz, amely lekérdezi a függőleges eszköz panelen a szerkesztő jobb oldalán található.</span><span class="sxs-lookup"><span data-stu-id="9d68f-118">The read-only property that gets the currently visible Windows PowerShell ISE add-on tool that is located in the vertical tool pane on the right side of the editor.</span></span>

### <a name="options"></a><span data-ttu-id="9d68f-119">Lehetőségek</span><span class="sxs-lookup"><span data-stu-id="9d68f-119">Options</span></span>

> <span data-ttu-id="9d68f-120">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="9d68f-120">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="9d68f-121">A csak olvasható tulajdonság, amely lekérdezi a különböző lehetőségek, amelyek a Windows PowerShell ISE-ben beállításait módosíthatja.</span><span class="sxs-lookup"><span data-stu-id="9d68f-121">The read-only property that gets the various options that can change settings in Windows PowerShell ISE.</span></span>

### <a name="powershelltabs"></a><span data-ttu-id="9d68f-122">PowerShellTabs</span><span class="sxs-lookup"><span data-stu-id="9d68f-122">PowerShellTabs</span></span>

> <span data-ttu-id="9d68f-123">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="9d68f-123">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="9d68f-124">A csak olvasható tulajdonság, amely lekérdezi a PowerShell lapok, amelyek a Windows PowerShell ISE-ben nyissa meg a gyűjteményben.</span><span class="sxs-lookup"><span data-stu-id="9d68f-124">The read-only property that gets the collection of the PowerShell tabs, which are open in Windows PowerShell ISE.</span></span> <span data-ttu-id="9d68f-125">Alapértelmezés szerint ez az objektum tartalmaz egy PowerShell-lap. Azonban hozzáadhat további PowerShell-lapok ehhez az objektumhoz menüket használja a Windows PowerShell ISE-ben vagy parancsfájlok használatával.</span><span class="sxs-lookup"><span data-stu-id="9d68f-125">By default, this object contains one PowerShell tab. However, you can add more PowerShell tabs to this object by using scripts or by using the menus in Windows PowerShell ISE.</span></span>

## <a name="see-also"></a><span data-ttu-id="9d68f-126">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="9d68f-126">See Also</span></span>

- [<span data-ttu-id="9d68f-127">A Windows PowerShell ISE parancsfájl-kezelési objektummodelljének célja</span><span class="sxs-lookup"><span data-stu-id="9d68f-127">Purpose of the Windows PowerShell ISE Scripting Object Model</span></span>](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [<span data-ttu-id="9d68f-128">Az ISE objektummodell-hierarchiája</span><span class="sxs-lookup"><span data-stu-id="9d68f-128">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md)