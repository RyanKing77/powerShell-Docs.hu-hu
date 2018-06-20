---
ms.date: 06/05/2017
keywords: PowerShell parancsmag
title: Az ISE objektummodell-hierarchiája
ms.openlocfilehash: 0159707b1050c412a74da3d3ca02a46cea982556
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
ms.locfileid: "30950692"
---
# <a name="the-ise-object-model-hierarchy"></a><span data-ttu-id="64f67-103">Az ISE objektummodell-hierarchiája</span><span class="sxs-lookup"><span data-stu-id="64f67-103">The ISE Object Model Hierarchy</span></span>

<span data-ttu-id="64f67-104">Ez a témakör bemutatja a Windows PowerShell integrált parancsfájlkezelési környezet (ISE) részét képező objektumok hierarchiáját.</span><span class="sxs-lookup"><span data-stu-id="64f67-104">This topic shows the hierarchy of objects that are part of Windows PowerShell Integrated Scripting Environment (ISE).</span></span>
<span data-ttu-id="64f67-105">A Windows PowerShell ISE megtalálható a Windows PowerShell 3.0 és a Windows PowerShell 4.0-s verzióját.</span><span class="sxs-lookup"><span data-stu-id="64f67-105">Windows PowerShell ISE is included in Windows PowerShell 3.0 and in Windows PowerShell 4.0.</span></span>
<span data-ttu-id="64f67-106">Kattintson egy objektumot léphet vissza az osztály, amely meghatározza az objektum dokumentációját.</span><span class="sxs-lookup"><span data-stu-id="64f67-106">Click an object to take you to the reference documentation for the class that defines the object.</span></span>

## <a name="psise-object"></a><span data-ttu-id="64f67-107">$psISE objektum</span><span class="sxs-lookup"><span data-stu-id="64f67-107">$psISE Object</span></span>

<span data-ttu-id="64f67-108">A **$psISE** objektum a [gyökérszintű objektum](The-ObjectModelRoot-Object.md) a Windows PowerShell ISE objektum hierarchia.</span><span class="sxs-lookup"><span data-stu-id="64f67-108">The **$psISE** object is the [root object](The-ObjectModelRoot-Object.md) of the Windows PowerShell ISE object hierarchy.</span></span>
<span data-ttu-id="64f67-109">A legfelső szintű helyen, akkor elérhetővé teszi a következő objektumok a parancsfájl-kezelési:</span><span class="sxs-lookup"><span data-stu-id="64f67-109">Located at the top level, it makes the following objects available for scripting:</span></span>

## <a name="psisecurrentfilethe-isefile-objectmd"></a>[<span data-ttu-id="64f67-110">$psISE.CurrentFile</span><span class="sxs-lookup"><span data-stu-id="64f67-110">$psISE.CurrentFile</span></span>](The-ISEFile-Object.md)

<span data-ttu-id="64f67-111">A **$psISE.CurrentFile** objektum példánya a [ISEFile](The-ISEFile-Object.md) osztály.</span><span class="sxs-lookup"><span data-stu-id="64f67-111">The **$psISE.CurrentFile** object is an instance of the [ISEFile](The-ISEFile-Object.md) class.</span></span>

## <a name="psisecurrentpowershelltabthe-powershelltab-objectmd"></a>[<span data-ttu-id="64f67-112">$psISE.CurrentPowerShellTab</span><span class="sxs-lookup"><span data-stu-id="64f67-112">$psISE.CurrentPowerShellTab</span></span>](The-PowerShellTab-Object.md)

<span data-ttu-id="64f67-113">A **$psISE.CurrentPowerShellTab** objektum példánya a [PowerShellTab](The-PowerShellTab-Object.md) osztály.</span><span class="sxs-lookup"><span data-stu-id="64f67-113">The **$psISE.CurrentPowerShellTab** object is an instance of the [PowerShellTab](The-PowerShellTab-Object.md) class.</span></span>

## <a name="psisecurrentvisiblehorizontaltool"></a><span data-ttu-id="64f67-114">$psISE.CurrentVisibleHorizontalTool</span><span class="sxs-lookup"><span data-stu-id="64f67-114">$psISE.CurrentVisibleHorizontalTool</span></span>

<span data-ttu-id="64f67-115">A **$psISE.CurrentVisibleHorizontalTool** objektum példánya a [ISEAddOnTool](The-ISEAddOnTool-Object.md) osztály.</span><span class="sxs-lookup"><span data-stu-id="64f67-115">The **$psISE.CurrentVisibleHorizontalTool** object is an instance of the [ISEAddOnTool](The-ISEAddOnTool-Object.md) class.</span></span>
<span data-ttu-id="64f67-116">A telepített bővítmény eszköz, amely jelenleg dokkolva van a Windows PowerShell ISE ablaka felső széle képviseli.</span><span class="sxs-lookup"><span data-stu-id="64f67-116">It represents the installed add-on tool that is currently docked to the top edge of the Windows PowerShell ISE window.</span></span>

## <a name="psisecurrentvisibleverticaltool"></a><span data-ttu-id="64f67-117">$psISE.CurrentVisibleVerticalTool</span><span class="sxs-lookup"><span data-stu-id="64f67-117">$psISE.CurrentVisibleVerticalTool</span></span>

<span data-ttu-id="64f67-118">A **$psISE.CurrentVisibleHorizontalTool** objektum példánya a [ISEAddOnTool](The-ISEAddOnTool-Object.md) osztály.</span><span class="sxs-lookup"><span data-stu-id="64f67-118">The **$psISE.CurrentVisibleHorizontalTool** object is an instance of the [ISEAddOnTool](The-ISEAddOnTool-Object.md) class.</span></span>
<span data-ttu-id="64f67-119">A telepített bővítmény eszköz, amely jelenleg dokkolva van a Windows PowerShell ISE ablak jobb oldali széle képviseli.</span><span class="sxs-lookup"><span data-stu-id="64f67-119">It represents the installed add-on tool that is currently docked to the right-hand edge of the Windows PowerShell ISE window.</span></span>

## <a name="psiseoptionsthe-iseoptions-objectmd"></a>[<span data-ttu-id="64f67-120">$psISE.Options</span><span class="sxs-lookup"><span data-stu-id="64f67-120">$psISE.Options</span></span>](The-ISEOptions-Object.md)

<span data-ttu-id="64f67-121">A **$psISE.Options** objektum példánya a [ISEOptions](The-ISEOptions-Object.md) osztály.</span><span class="sxs-lookup"><span data-stu-id="64f67-121">The **$psISE.Options** object is an instance of the [ISEOptions](The-ISEOptions-Object.md) class.</span></span>
<span data-ttu-id="64f67-122">A ISEOptions objektum a Windows PowerShell ISE különböző beállításokat adja meg.</span><span class="sxs-lookup"><span data-stu-id="64f67-122">The ISEOptions object represents various settings for Windows PowerShell ISE.</span></span>
<span data-ttu-id="64f67-123">A Microsoft.PowerShell.Host.ISE.ISEOptions osztály példánya.</span><span class="sxs-lookup"><span data-stu-id="64f67-123">It is an instance of the Microsoft.PowerShell.Host.ISE.ISEOptions class.</span></span>

## <a name="psisepowershelltabsthe-powershelltabcollection-objectmd"></a>[<span data-ttu-id="64f67-124">$psISE.PowerShellTabs</span><span class="sxs-lookup"><span data-stu-id="64f67-124">$psISE.PowerShellTabs</span></span>](The-PowerShellTabCollection-Object.md)

<span data-ttu-id="64f67-125">A **$psISE.PowerShellTabs** objektum példánya a [PowerShellTabCollection](The-PowerShellTabCollection-Object.md) osztály.</span><span class="sxs-lookup"><span data-stu-id="64f67-125">The **$psISE.PowerShellTabs** object is an instance of the [PowerShellTabCollection](The-PowerShellTabCollection-Object.md) class.</span></span>
<span data-ttu-id="64f67-126">Minden a jelenleg megnyitott PowerShell lapok, amelyek megfelelnek az elérhető Windows PowerShell környezetben futtatni, a helyi számítógépen vagy a csatlakoztatott távoli számítógépeken lévő gyűjteménye.</span><span class="sxs-lookup"><span data-stu-id="64f67-126">It is a collection of all the currently open PowerShell tabs that represent the available Windows PowerShell run environments on the local computer or on connected remote computers.</span></span>
<span data-ttu-id="64f67-127">A gyűjtemény minden tagja egy példányát a [PowerShellTab](The-PowerShellTab-Object.md) osztály.</span><span class="sxs-lookup"><span data-stu-id="64f67-127">Each member in the collection is an instance of the [PowerShellTab](The-PowerShellTab-Object.md) class.</span></span>

## <a name="see-also"></a><span data-ttu-id="64f67-128">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="64f67-128">See Also</span></span>

- [<span data-ttu-id="64f67-129">A Windows PowerShell ISE objektummodell Scripting célja</span><span class="sxs-lookup"><span data-stu-id="64f67-129">Purpose of the Windows PowerShell ISE Scripting Object Model</span></span>](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [<span data-ttu-id="64f67-130">Az ISE objektummodell-hierarchiája</span><span class="sxs-lookup"><span data-stu-id="64f67-130">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md)