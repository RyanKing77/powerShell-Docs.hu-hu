---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "DSCAutomationHostEnabled beállításkulcs"
ms.openlocfilehash: e47c929b366f93738343eabc431aab5a4428352d
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
><span data-ttu-id="e2ce4-103">A következőkre vonatkozik: a Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="e2ce4-103">Applies to: Windows PowerShell 5.0</span></span>

# <a name="dscautomationhostenabled-registry-key"></a><span data-ttu-id="e2ce4-104">DSCAutomationHostEnabled beállításkulcs</span><span class="sxs-lookup"><span data-stu-id="e2ce4-104">DSCAutomationHostEnabled registry key</span></span>

<span data-ttu-id="e2ce4-105">DSC használja a **DSCAutomationHostEnabled** kulcs alatt **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies** ahhoz, hogy a kezdeti állítja a gép konfigurációját.</span><span class="sxs-lookup"><span data-stu-id="e2ce4-105">DSC uses the **DSCAutomationHostEnabled** registry key under **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies** to enable configuration of the machine at initial boot-up.</span></span>
<span data-ttu-id="e2ce4-106">DSCAutomationHostEnabled három módot támogat:</span><span class="sxs-lookup"><span data-stu-id="e2ce4-106">DSCAutomationHostEnabled supports three modes:</span></span>

|  <span data-ttu-id="e2ce4-107">DSCAutomationHostEnabled érték</span><span class="sxs-lookup"><span data-stu-id="e2ce4-107">DSCAutomationHostEnabled Value</span></span>  |  <span data-ttu-id="e2ce4-108">Leírás</span><span class="sxs-lookup"><span data-stu-id="e2ce4-108">Description</span></span>   | 
|---|---| 
<span data-ttu-id="e2ce4-109">0</span><span class="sxs-lookup"><span data-stu-id="e2ce4-109">0</span></span> | <span data-ttu-id="e2ce4-110">Tiltsa le a gép konfigurál állítja.</span><span class="sxs-lookup"><span data-stu-id="e2ce4-110">Disable configuring the machine at boot-up.</span></span> |
<span data-ttu-id="e2ce4-111">1</span><span class="sxs-lookup"><span data-stu-id="e2ce4-111">1</span></span> | <span data-ttu-id="e2ce4-112">Engedélyezze a gép konfigurál állítja.</span><span class="sxs-lookup"><span data-stu-id="e2ce4-112">Enable configuring the machine at boot-up.</span></span> |
<span data-ttu-id="e2ce4-113">2</span><span class="sxs-lookup"><span data-stu-id="e2ce4-113">2</span></span> | <span data-ttu-id="e2ce4-114">A gép konfigurálása, csak ha DSC engedélyezése folyamatban lévő vagy a jelenlegi állapot.</span><span class="sxs-lookup"><span data-stu-id="e2ce4-114">Enable configuring the machine only if DSC is in pending or current state.</span></span> <span data-ttu-id="e2ce4-115">Ez az alapértelmezett érték.</span><span class="sxs-lookup"><span data-stu-id="e2ce4-115">This is the default value.</span></span> |

## <a name="see-also"></a><span data-ttu-id="e2ce4-116">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="e2ce4-116">See Also</span></span>

<span data-ttu-id="e2ce4-117">A példa bemutatja, hogyan futtathat konfigurációk kezdeti állítja a szolgáltatás használatához, tekintse meg a [DSC segítségével konfigurálhatja a virtuális gépek kezdeti állítja](bootstrapDsc.md).</span><span class="sxs-lookup"><span data-stu-id="e2ce4-117">For an example of how to use this feature to run configurations at initial boot-up, see [Configure a virtual machines at initial boot-up by using DSC](bootstrapDsc.md).</span></span>


