---
ms.date: 2017-08-25
keywords: PowerShell parancsmag
title: A ObjectModelRoot objektum
ms.openlocfilehash: eb3424ff147c35364fa08543d59ebd30f6d2d857
ms.sourcegitcommit: d6ab9ab5909ed59cce4ce30e29457e0e75c7ac12
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/08/2017
---
# <a name="the-objectmodelroot-object"></a><span data-ttu-id="7f317-103">A ObjectModelRoot objektum</span><span class="sxs-lookup"><span data-stu-id="7f317-103">The ObjectModelRoot Object</span></span>

<span data-ttu-id="7f317-104">A **$psISE** objektum, amely a Windows PowerShell® integrált parancsfájl-kezelési környezet (ISE) egyszerű főtanúsítvány-objektum az Microsoft.PowerShell.Host.ISE.ObjectModelRoot osztály egy példányát.</span><span class="sxs-lookup"><span data-stu-id="7f317-104">The **$psISE** object, which is the principal root object in Windows PowerShell® Integrated Scripting Environment (ISE) is an instance of the Microsoft.PowerShell.Host.ISE.ObjectModelRoot class.</span></span>
<span data-ttu-id="7f317-105">Ez a témakör azon tulajdonságait ismerteti a **ObjectModelRoot** objektum.</span><span class="sxs-lookup"><span data-stu-id="7f317-105">This topic describes the properties of the **ObjectModelRoot** object.</span></span>

## <a name="properties"></a><span data-ttu-id="7f317-106">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="7f317-106">Properties</span></span>

### <a name="currentfile"></a><span data-ttu-id="7f317-107">CurrentFile</span><span class="sxs-lookup"><span data-stu-id="7f317-107">CurrentFile</span></span>

> <span data-ttu-id="7f317-108">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="7f317-108">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

<span data-ttu-id="7f317-109">A csak olvasható tulajdonság, amely lekérdezi a fájlt, amely az összes állomás objektum, amely éppen fókuszban van társítva.</span><span class="sxs-lookup"><span data-stu-id="7f317-109">The read-only property that gets the file, which is associated with this host object that currently has the focus.</span></span>

### <a name="currentpowershelltab"></a><span data-ttu-id="7f317-110">CurrentPowerShellTab</span><span class="sxs-lookup"><span data-stu-id="7f317-110">CurrentPowerShellTab</span></span>

> <span data-ttu-id="7f317-111">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="7f317-111">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="7f317-112">A csak olvasható tulajdonság, amely lekérdezi a fókusszal rendelkező PowerShell fülre.</span><span class="sxs-lookup"><span data-stu-id="7f317-112">The read-only property that gets the PowerShell tab that has the focus.</span></span>

### <a name="currentvisiblehorizontaltool"></a><span data-ttu-id="7f317-113">CurrentVisibleHorizontalTool</span><span class="sxs-lookup"><span data-stu-id="7f317-113">CurrentVisibleHorizontalTool</span></span>

> <span data-ttu-id="7f317-114">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="7f317-114">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="7f317-115">A csak olvasható tulajdonság, amely a jelenleg látható a Windows PowerShell ISE-bővítmény eszköz, amely lekérdezi a vízszintes eszköz panelen a szerkesztő alján található.</span><span class="sxs-lookup"><span data-stu-id="7f317-115">The read-only property that gets the currently visible Windows PowerShell ISE add-on tool that is located in the horizontal tool pane at the bottom of the editor.</span></span>

### <a name="currentvisibleverticaltool"></a><span data-ttu-id="7f317-116">CurrentVisibleVerticalTool</span><span class="sxs-lookup"><span data-stu-id="7f317-116">CurrentVisibleVerticalTool</span></span>

> <span data-ttu-id="7f317-117">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="7f317-117">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

<span data-ttu-id="7f317-118">A csak olvasható tulajdonság, amely a jelenleg látható a Windows PowerShell ISE-bővítmény eszköz, amely lekérdezi a függőleges eszközpanelt szerkesztő jobb oldalán található.</span><span class="sxs-lookup"><span data-stu-id="7f317-118">The read-only property that gets the currently visible Windows PowerShell ISE add-on tool that is located in the vertical tool pane on the right side of the editor.</span></span>

### <a name="options"></a><span data-ttu-id="7f317-119">Lehetőségek</span><span class="sxs-lookup"><span data-stu-id="7f317-119">Options</span></span>

> <span data-ttu-id="7f317-120">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="7f317-120">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

<span data-ttu-id="7f317-121">A csak olvasható tulajdonság, amely lekérdezi a különböző lehetőségek, amely a Windows PowerShell ISE beállításait módosíthatja.</span><span class="sxs-lookup"><span data-stu-id="7f317-121">The read-only property that gets the various options that can change settings in Windows PowerShell ISE.</span></span>

### <a name="powershelltabs"></a><span data-ttu-id="7f317-122">PowerShellTabs</span><span class="sxs-lookup"><span data-stu-id="7f317-122">PowerShellTabs</span></span>

> <span data-ttu-id="7f317-123">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="7f317-123">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

<span data-ttu-id="7f317-124">A csak olvasható tulajdonság, amely lekérdezi a PowerShell lapokat, nyissa meg a Windows PowerShell ISE gyűjteménye.</span><span class="sxs-lookup"><span data-stu-id="7f317-124">The read-only property that gets the collection of the PowerShell tabs, which are open in Windows PowerShell ISE.</span></span> <span data-ttu-id="7f317-125">Alapértelmezés szerint ez az objektum tartalmaz egy PowerShell-lapon. Azonban adhat hozzá további PowerShell lapok Ez az objektum-parancsfájlok használatával, vagy a Windows PowerShell ISE a menük használatával.</span><span class="sxs-lookup"><span data-stu-id="7f317-125">By default, this object contains one PowerShell tab. However, you can add more PowerShell tabs to this object by using scripts or by using the menus in Windows PowerShell ISE.</span></span>

## <a name="see-also"></a><span data-ttu-id="7f317-126">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="7f317-126">See Also</span></span>

- [<span data-ttu-id="7f317-127">A Windows PowerShell ISE Scripting Hálózatiobjektum-modellje</span><span class="sxs-lookup"><span data-stu-id="7f317-127">The Windows PowerShell ISE Scripting Object Model</span></span>](The-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [<span data-ttu-id="7f317-128">A Windows PowerShell ISE objektumhivatkozás modell</span><span class="sxs-lookup"><span data-stu-id="7f317-128">Windows PowerShell ISE Object Model Reference</span></span>](Windows-PowerShell-ISE-Object-Model-Reference.md)
- [<span data-ttu-id="7f317-129">A ISE objektum modell hierarchia</span><span class="sxs-lookup"><span data-stu-id="7f317-129">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md)
