---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: Az ISE objektummodell-hierarchiája
ms.openlocfilehash: 0159707b1050c412a74da3d3ca02a46cea982556
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404467"
---
# <a name="the-ise-object-model-hierarchy"></a><span data-ttu-id="10ebd-103">Az ISE objektummodell-hierarchiája</span><span class="sxs-lookup"><span data-stu-id="10ebd-103">The ISE Object Model Hierarchy</span></span>

<span data-ttu-id="10ebd-104">Ez a témakör bemutatja a Windows PowerShell integrált parancsfájlkezelési környezet (ISE) részét képező objektumok hierarchiáját.</span><span class="sxs-lookup"><span data-stu-id="10ebd-104">This topic shows the hierarchy of objects that are part of Windows PowerShell Integrated Scripting Environment (ISE).</span></span>
<span data-ttu-id="10ebd-105">Windows PowerShell ISE-ben megtalálható a Windows PowerShell 3.0 és a Windows PowerShell 4.0-s verzióját.</span><span class="sxs-lookup"><span data-stu-id="10ebd-105">Windows PowerShell ISE is included in Windows PowerShell 3.0 and in Windows PowerShell 4.0.</span></span>
<span data-ttu-id="10ebd-106">Kattintson egy objektum, amelyben az osztály, amely meghatározza az objektum a hivatkozási dokumentációját.</span><span class="sxs-lookup"><span data-stu-id="10ebd-106">Click an object to take you to the reference documentation for the class that defines the object.</span></span>

## <a name="psise-object"></a><span data-ttu-id="10ebd-107">$psISE objektum</span><span class="sxs-lookup"><span data-stu-id="10ebd-107">$psISE Object</span></span>

<span data-ttu-id="10ebd-108">A **$psISE** objektum a [gyökérobjektum](The-ObjectModelRoot-Object.md) a Windows PowerShell ISE-objektum hierarchia.</span><span class="sxs-lookup"><span data-stu-id="10ebd-108">The **$psISE** object is the [root object](The-ObjectModelRoot-Object.md) of the Windows PowerShell ISE object hierarchy.</span></span>
<span data-ttu-id="10ebd-109">A legfelső szintű helyen található, azt elérhetővé teszi a következő objektumok scripting:</span><span class="sxs-lookup"><span data-stu-id="10ebd-109">Located at the top level, it makes the following objects available for scripting:</span></span>

## <a name="psisecurrentfilethe-isefile-objectmd"></a>[<span data-ttu-id="10ebd-110">$psISE.CurrentFile</span><span class="sxs-lookup"><span data-stu-id="10ebd-110">$psISE.CurrentFile</span></span>](The-ISEFile-Object.md)

<span data-ttu-id="10ebd-111">A **$psISE.CurrentFile** objektum egy példányát a [ISEFile](The-ISEFile-Object.md) osztály.</span><span class="sxs-lookup"><span data-stu-id="10ebd-111">The **$psISE.CurrentFile** object is an instance of the [ISEFile](The-ISEFile-Object.md) class.</span></span>

## <a name="psisecurrentpowershelltabthe-powershelltab-objectmd"></a>[<span data-ttu-id="10ebd-112">$psISE.CurrentPowerShellTab</span><span class="sxs-lookup"><span data-stu-id="10ebd-112">$psISE.CurrentPowerShellTab</span></span>](The-PowerShellTab-Object.md)

<span data-ttu-id="10ebd-113">A **$psISE.CurrentPowerShellTab** objektum egy példányát a [PowerShellTab](The-PowerShellTab-Object.md) osztály.</span><span class="sxs-lookup"><span data-stu-id="10ebd-113">The **$psISE.CurrentPowerShellTab** object is an instance of the [PowerShellTab](The-PowerShellTab-Object.md) class.</span></span>

## <a name="psisecurrentvisiblehorizontaltool"></a><span data-ttu-id="10ebd-114">$psISE.CurrentVisibleHorizontalTool</span><span class="sxs-lookup"><span data-stu-id="10ebd-114">$psISE.CurrentVisibleHorizontalTool</span></span>

<span data-ttu-id="10ebd-115">A **$psISE.CurrentVisibleHorizontalTool** objektum egy példányát a [ISEAddOnTool](The-ISEAddOnTool-Object.md) osztály.</span><span class="sxs-lookup"><span data-stu-id="10ebd-115">The **$psISE.CurrentVisibleHorizontalTool** object is an instance of the [ISEAddOnTool](The-ISEAddOnTool-Object.md) class.</span></span>
<span data-ttu-id="10ebd-116">A telepített kiegészítő eszköz, amely jelenleg rögzítve van a Windows PowerShell ISE-ben ablak felső széle képviseli.</span><span class="sxs-lookup"><span data-stu-id="10ebd-116">It represents the installed add-on tool that is currently docked to the top edge of the Windows PowerShell ISE window.</span></span>

## <a name="psisecurrentvisibleverticaltool"></a><span data-ttu-id="10ebd-117">$psISE.CurrentVisibleVerticalTool</span><span class="sxs-lookup"><span data-stu-id="10ebd-117">$psISE.CurrentVisibleVerticalTool</span></span>

<span data-ttu-id="10ebd-118">A **$psISE.CurrentVisibleHorizontalTool** objektum egy példányát a [ISEAddOnTool](The-ISEAddOnTool-Object.md) osztály.</span><span class="sxs-lookup"><span data-stu-id="10ebd-118">The **$psISE.CurrentVisibleHorizontalTool** object is an instance of the [ISEAddOnTool](The-ISEAddOnTool-Object.md) class.</span></span>
<span data-ttu-id="10ebd-119">A telepített kiegészítő eszköz, amely jelenleg rögzítve van a Windows PowerShell ISE-ablak jobb oldali széle képviseli.</span><span class="sxs-lookup"><span data-stu-id="10ebd-119">It represents the installed add-on tool that is currently docked to the right-hand edge of the Windows PowerShell ISE window.</span></span>

## <a name="psiseoptionsthe-iseoptions-objectmd"></a>[<span data-ttu-id="10ebd-120">$psISE.Options</span><span class="sxs-lookup"><span data-stu-id="10ebd-120">$psISE.Options</span></span>](The-ISEOptions-Object.md)

<span data-ttu-id="10ebd-121">A **$psISE.Options** objektum egy példányát a [ISEOptions](The-ISEOptions-Object.md) osztály.</span><span class="sxs-lookup"><span data-stu-id="10ebd-121">The **$psISE.Options** object is an instance of the [ISEOptions](The-ISEOptions-Object.md) class.</span></span>
<span data-ttu-id="10ebd-122">Az ISEOptions objektum Windows PowerShell ISE-ben különböző beállításait jelöli.</span><span class="sxs-lookup"><span data-stu-id="10ebd-122">The ISEOptions object represents various settings for Windows PowerShell ISE.</span></span>
<span data-ttu-id="10ebd-123">Fontos a Microsoft.PowerShell.Host.ISE.ISEOptions osztály egy példányát.</span><span class="sxs-lookup"><span data-stu-id="10ebd-123">It is an instance of the Microsoft.PowerShell.Host.ISE.ISEOptions class.</span></span>

## <a name="psisepowershelltabsthe-powershelltabcollection-objectmd"></a>[<span data-ttu-id="10ebd-124">$psISE.PowerShellTabs</span><span class="sxs-lookup"><span data-stu-id="10ebd-124">$psISE.PowerShellTabs</span></span>](The-PowerShellTabCollection-Object.md)

<span data-ttu-id="10ebd-125">A **$psISE.PowerShellTabs** objektum egy példányát a [PowerShellTabCollection](The-PowerShellTabCollection-Object.md) osztály.</span><span class="sxs-lookup"><span data-stu-id="10ebd-125">The **$psISE.PowerShellTabs** object is an instance of the [PowerShellTabCollection](The-PowerShellTabCollection-Object.md) class.</span></span>
<span data-ttu-id="10ebd-126">Az összes a jelenleg megnyitott PowerShell lapok, amelyek az elérhető Windows PowerShell környezetben futtatni, a helyi számítógépen vagy a csatlakoztatott távoli számítógépeken lévő gyűjteménye.</span><span class="sxs-lookup"><span data-stu-id="10ebd-126">It is a collection of all the currently open PowerShell tabs that represent the available Windows PowerShell run environments on the local computer or on connected remote computers.</span></span>
<span data-ttu-id="10ebd-127">A gyűjtemény minden tagja egy példányát a [PowerShellTab](The-PowerShellTab-Object.md) osztály.</span><span class="sxs-lookup"><span data-stu-id="10ebd-127">Each member in the collection is an instance of the [PowerShellTab](The-PowerShellTab-Object.md) class.</span></span>

## <a name="see-also"></a><span data-ttu-id="10ebd-128">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="10ebd-128">See Also</span></span>

- [<span data-ttu-id="10ebd-129">A Windows PowerShell ISE parancsfájl-kezelési objektummodelljének célja</span><span class="sxs-lookup"><span data-stu-id="10ebd-129">Purpose of the Windows PowerShell ISE Scripting Object Model</span></span>](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [<span data-ttu-id="10ebd-130">Az ISE objektummodell-hierarchiája</span><span class="sxs-lookup"><span data-stu-id="10ebd-130">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md)