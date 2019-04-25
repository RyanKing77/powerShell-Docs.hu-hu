---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSCAutomationHostEnabled beállításkulcs
ms.openlocfilehash: 2bccd2738b9f61efd656fdf0f98cf71affdbe781
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62076485"
---
><span data-ttu-id="07085-103">Érintett kiadások: Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="07085-103">Applies to: Windows PowerShell 5.0</span></span>

# <a name="dscautomationhostenabled-registry-key"></a><span data-ttu-id="07085-104">DSCAutomationHostEnabled beállításkulcs</span><span class="sxs-lookup"><span data-stu-id="07085-104">DSCAutomationHostEnabled registry key</span></span>

<span data-ttu-id="07085-105">DSC használja a **DSCAutomationHostEnabled** beállításkulcs alatt **localaccounttokenfilterpolicy** ahhoz, hogy a gép kezdeti konfiguráció rendszerindítás.</span><span class="sxs-lookup"><span data-stu-id="07085-105">DSC uses the **DSCAutomationHostEnabled** registry key under **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System** to enable configuration of the machine at initial boot-up.</span></span>
<span data-ttu-id="07085-106">**DSCAutomationHostEnabled** három módot támogat:</span><span class="sxs-lookup"><span data-stu-id="07085-106">**DSCAutomationHostEnabled** supports three modes:</span></span>

|  <span data-ttu-id="07085-107">DSCAutomationHostEnabled érték</span><span class="sxs-lookup"><span data-stu-id="07085-107">DSCAutomationHostEnabled Value</span></span>  |  <span data-ttu-id="07085-108">Leírás</span><span class="sxs-lookup"><span data-stu-id="07085-108">Description</span></span>   |
|---|---|
<span data-ttu-id="07085-109">0</span><span class="sxs-lookup"><span data-stu-id="07085-109">0</span></span> | <span data-ttu-id="07085-110">Tiltsa le a rendszerindítás, a gép konfigurálásával.</span><span class="sxs-lookup"><span data-stu-id="07085-110">Disable configuring the machine at boot-up.</span></span> |
<span data-ttu-id="07085-111">1</span><span class="sxs-lookup"><span data-stu-id="07085-111">1</span></span> | <span data-ttu-id="07085-112">Engedélyezze a gép konfigurál a rendszerindítás.</span><span class="sxs-lookup"><span data-stu-id="07085-112">Enable configuring the machine at boot-up.</span></span> |
<span data-ttu-id="07085-113">2</span><span class="sxs-lookup"><span data-stu-id="07085-113">2</span></span> | <span data-ttu-id="07085-114">Engedélyezze a konfigurálása a gép csak akkor, ha a DSC van függőben lévő vagy a jelenlegi állapotban.</span><span class="sxs-lookup"><span data-stu-id="07085-114">Enable configuring the machine only if DSC is in pending or current state.</span></span> <span data-ttu-id="07085-115">Ez az alapértelmezett érték.</span><span class="sxs-lookup"><span data-stu-id="07085-115">This is the default value.</span></span> |

## <a name="see-also"></a><span data-ttu-id="07085-116">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="07085-116">See Also</span></span>

<span data-ttu-id="07085-117">Ez a funkció használata első konfigurációk futtatni egy példa: [konfigurálása a virtuális gépek első indításkor DSC használatával](bootstrapDsc.md).</span><span class="sxs-lookup"><span data-stu-id="07085-117">For an example of how to use this feature to run configurations at initial boot-up, see [Configure a virtual machines at initial boot-up by using DSC](bootstrapDsc.md).</span></span>
