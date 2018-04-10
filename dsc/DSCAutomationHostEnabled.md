---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: DSCAutomationHostEnabled beállításkulcs
ms.openlocfilehash: 9fd71120b4959a7b14094922b453b05b217f3736
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
><span data-ttu-id="784ca-103">A következőkre vonatkozik: a Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="784ca-103">Applies to: Windows PowerShell 5.0</span></span>

# <a name="dscautomationhostenabled-registry-key"></a><span data-ttu-id="784ca-104">DSCAutomationHostEnabled beállításkulcs</span><span class="sxs-lookup"><span data-stu-id="784ca-104">DSCAutomationHostEnabled registry key</span></span>

<span data-ttu-id="784ca-105">DSC használja a **DSCAutomationHostEnabled** kulcs alatt **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies** ahhoz, hogy a kezdeti állítja a gép konfigurációját.</span><span class="sxs-lookup"><span data-stu-id="784ca-105">DSC uses the **DSCAutomationHostEnabled** registry key under **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies** to enable configuration of the machine at initial boot-up.</span></span>
<span data-ttu-id="784ca-106">DSCAutomationHostEnabled három módot támogat:</span><span class="sxs-lookup"><span data-stu-id="784ca-106">DSCAutomationHostEnabled supports three modes:</span></span>

|  <span data-ttu-id="784ca-107">DSCAutomationHostEnabled Value</span><span class="sxs-lookup"><span data-stu-id="784ca-107">DSCAutomationHostEnabled Value</span></span>  |  <span data-ttu-id="784ca-108">Leírás</span><span class="sxs-lookup"><span data-stu-id="784ca-108">Description</span></span>   |
|---|---|
<span data-ttu-id="784ca-109">0</span><span class="sxs-lookup"><span data-stu-id="784ca-109">0</span></span> | <span data-ttu-id="784ca-110">Tiltsa le a gép konfigurál állítja.</span><span class="sxs-lookup"><span data-stu-id="784ca-110">Disable configuring the machine at boot-up.</span></span> |
<span data-ttu-id="784ca-111">1</span><span class="sxs-lookup"><span data-stu-id="784ca-111">1</span></span> | <span data-ttu-id="784ca-112">Engedélyezze a gép konfigurál állítja.</span><span class="sxs-lookup"><span data-stu-id="784ca-112">Enable configuring the machine at boot-up.</span></span> |
<span data-ttu-id="784ca-113">2</span><span class="sxs-lookup"><span data-stu-id="784ca-113">2</span></span> | <span data-ttu-id="784ca-114">A gép konfigurálása, csak ha DSC engedélyezése folyamatban lévő vagy a jelenlegi állapot.</span><span class="sxs-lookup"><span data-stu-id="784ca-114">Enable configuring the machine only if DSC is in pending or current state.</span></span> <span data-ttu-id="784ca-115">Ez az alapértelmezett érték.</span><span class="sxs-lookup"><span data-stu-id="784ca-115">This is the default value.</span></span> |

## <a name="see-also"></a><span data-ttu-id="784ca-116">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="784ca-116">See Also</span></span>

<span data-ttu-id="784ca-117">A példa bemutatja, hogyan futtathat konfigurációk kezdeti állítja a szolgáltatás használatához, tekintse meg a [DSC segítségével konfigurálhatja a virtuális gépek kezdeti állítja](bootstrapDsc.md).</span><span class="sxs-lookup"><span data-stu-id="784ca-117">For an example of how to use this feature to run configurations at initial boot-up, see [Configure a virtual machines at initial boot-up by using DSC](bootstrapDsc.md).</span></span>