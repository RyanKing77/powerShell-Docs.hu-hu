---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: DSCAutomationHostEnabled registry key
ms.openlocfilehash: c58b7a8f2485ff02f09763749a3de8a75f882d19
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 01/17/2018
---
><span data-ttu-id="76ce8-103">A következőkre vonatkozik: a Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="76ce8-103">Applies to: Windows PowerShell 5.0</span></span>

# <a name="dscautomationhostenabled-registry-key"></a><span data-ttu-id="76ce8-104">DSCAutomationHostEnabled registry key</span><span class="sxs-lookup"><span data-stu-id="76ce8-104">DSCAutomationHostEnabled registry key</span></span>

<span data-ttu-id="76ce8-105">DSC használja a **DSCAutomationHostEnabled** kulcs alatt **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies** ahhoz, hogy a kezdeti állítja a gép konfigurációját.</span><span class="sxs-lookup"><span data-stu-id="76ce8-105">DSC uses the **DSCAutomationHostEnabled** registry key under **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies** to enable configuration of the machine at initial boot-up.</span></span>
<span data-ttu-id="76ce8-106">DSCAutomationHostEnabled három módot támogat:</span><span class="sxs-lookup"><span data-stu-id="76ce8-106">DSCAutomationHostEnabled supports three modes:</span></span>

|  <span data-ttu-id="76ce8-107">DSCAutomationHostEnabled Value</span><span class="sxs-lookup"><span data-stu-id="76ce8-107">DSCAutomationHostEnabled Value</span></span>  |  <span data-ttu-id="76ce8-108">Leírás</span><span class="sxs-lookup"><span data-stu-id="76ce8-108">Description</span></span>   | 
|---|---| 
<span data-ttu-id="76ce8-109">0</span><span class="sxs-lookup"><span data-stu-id="76ce8-109">0</span></span> | <span data-ttu-id="76ce8-110">Tiltsa le a gép konfigurál állítja.</span><span class="sxs-lookup"><span data-stu-id="76ce8-110">Disable configuring the machine at boot-up.</span></span> |
<span data-ttu-id="76ce8-111">1</span><span class="sxs-lookup"><span data-stu-id="76ce8-111">1</span></span> | <span data-ttu-id="76ce8-112">Engedélyezze a gép konfigurál állítja.</span><span class="sxs-lookup"><span data-stu-id="76ce8-112">Enable configuring the machine at boot-up.</span></span> |
<span data-ttu-id="76ce8-113">2</span><span class="sxs-lookup"><span data-stu-id="76ce8-113">2</span></span> | <span data-ttu-id="76ce8-114">A gép konfigurálása, csak ha DSC engedélyezése folyamatban lévő vagy a jelenlegi állapot.</span><span class="sxs-lookup"><span data-stu-id="76ce8-114">Enable configuring the machine only if DSC is in pending or current state.</span></span> <span data-ttu-id="76ce8-115">Ez az alapértelmezett érték.</span><span class="sxs-lookup"><span data-stu-id="76ce8-115">This is the default value.</span></span> |

## <a name="see-also"></a><span data-ttu-id="76ce8-116">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="76ce8-116">See Also</span></span>

<span data-ttu-id="76ce8-117">A példa bemutatja, hogyan futtathat konfigurációk kezdeti állítja a szolgáltatás használatához, tekintse meg a [DSC segítségével konfigurálhatja a virtuális gépek kezdeti állítja](bootstrapDsc.md).</span><span class="sxs-lookup"><span data-stu-id="76ce8-117">For an example of how to use this feature to run configurations at initial boot-up, see [Configure a virtual machines at initial boot-up by using DSC](bootstrapDsc.md).</span></span>


