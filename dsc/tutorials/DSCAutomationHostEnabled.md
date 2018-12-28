---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSCAutomationHostEnabled beállításkulcs
ms.openlocfilehash: 38e3189323c39a522b2ccad89f5cfcadf5e45616
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404155"
---
><span data-ttu-id="61e30-103">Érintett kiadások: Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="61e30-103">Applies to: Windows PowerShell 5.0</span></span>

# <a name="dscautomationhostenabled-registry-key"></a><span data-ttu-id="61e30-104">DSCAutomationHostEnabled beállításkulcs</span><span class="sxs-lookup"><span data-stu-id="61e30-104">DSCAutomationHostEnabled registry key</span></span>

<span data-ttu-id="61e30-105">DSC használja a **DSCAutomationHostEnabled** beállításkulcs alatt **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies** engedélyezéséhez az első, a gép konfigurációját.</span><span class="sxs-lookup"><span data-stu-id="61e30-105">DSC uses the **DSCAutomationHostEnabled** registry key under **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies** to enable configuration of the machine at initial boot-up.</span></span>
<span data-ttu-id="61e30-106">DSCAutomationHostEnabled három módot támogat:</span><span class="sxs-lookup"><span data-stu-id="61e30-106">DSCAutomationHostEnabled supports three modes:</span></span>

|  <span data-ttu-id="61e30-107">DSCAutomationHostEnabled érték</span><span class="sxs-lookup"><span data-stu-id="61e30-107">DSCAutomationHostEnabled Value</span></span>  |  <span data-ttu-id="61e30-108">Leírás</span><span class="sxs-lookup"><span data-stu-id="61e30-108">Description</span></span>   |
|---|---|
<span data-ttu-id="61e30-109">0</span><span class="sxs-lookup"><span data-stu-id="61e30-109">0</span></span> | <span data-ttu-id="61e30-110">Tiltsa le a rendszerindítás, a gép konfigurálásával.</span><span class="sxs-lookup"><span data-stu-id="61e30-110">Disable configuring the machine at boot-up.</span></span> |
<span data-ttu-id="61e30-111">1</span><span class="sxs-lookup"><span data-stu-id="61e30-111">1</span></span> | <span data-ttu-id="61e30-112">Engedélyezze a gép konfigurál a rendszerindítás.</span><span class="sxs-lookup"><span data-stu-id="61e30-112">Enable configuring the machine at boot-up.</span></span> |
<span data-ttu-id="61e30-113">2</span><span class="sxs-lookup"><span data-stu-id="61e30-113">2</span></span> | <span data-ttu-id="61e30-114">Engedélyezze a konfigurálása a gép csak akkor, ha a DSC van függőben lévő vagy a jelenlegi állapotban.</span><span class="sxs-lookup"><span data-stu-id="61e30-114">Enable configuring the machine only if DSC is in pending or current state.</span></span> <span data-ttu-id="61e30-115">Ez az alapértelmezett érték.</span><span class="sxs-lookup"><span data-stu-id="61e30-115">This is the default value.</span></span> |

## <a name="see-also"></a><span data-ttu-id="61e30-116">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="61e30-116">See Also</span></span>

<span data-ttu-id="61e30-117">Ez a funkció használata első konfigurációk futtatni egy példa: [konfigurálása a virtuális gépek első indításkor DSC használatával](bootstrapDsc.md).</span><span class="sxs-lookup"><span data-stu-id="61e30-117">For an example of how to use this feature to run configurations at initial boot-up, see [Configure a virtual machines at initial boot-up by using DSC](bootstrapDsc.md).</span></span>