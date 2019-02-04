---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSCAutomationHostEnabled beállításkulcs
ms.openlocfilehash: 2bccd2738b9f61efd656fdf0f98cf71affdbe781
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55684800"
---
><span data-ttu-id="8b29c-103">Érintett kiadások: Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="8b29c-103">Applies to: Windows PowerShell 5.0</span></span>

# <a name="dscautomationhostenabled-registry-key"></a><span data-ttu-id="8b29c-104">DSCAutomationHostEnabled beállításkulcs</span><span class="sxs-lookup"><span data-stu-id="8b29c-104">DSCAutomationHostEnabled registry key</span></span>

<span data-ttu-id="8b29c-105">DSC használja a **DSCAutomationHostEnabled** beállításkulcs alatt **localaccounttokenfilterpolicy** ahhoz, hogy a gép kezdeti konfiguráció rendszerindítás.</span><span class="sxs-lookup"><span data-stu-id="8b29c-105">DSC uses the **DSCAutomationHostEnabled** registry key under **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System** to enable configuration of the machine at initial boot-up.</span></span>
<span data-ttu-id="8b29c-106">**DSCAutomationHostEnabled** három módot támogat:</span><span class="sxs-lookup"><span data-stu-id="8b29c-106">**DSCAutomationHostEnabled** supports three modes:</span></span>

|  <span data-ttu-id="8b29c-107">DSCAutomationHostEnabled érték</span><span class="sxs-lookup"><span data-stu-id="8b29c-107">DSCAutomationHostEnabled Value</span></span>  |  <span data-ttu-id="8b29c-108">Leírás</span><span class="sxs-lookup"><span data-stu-id="8b29c-108">Description</span></span>   |
|---|---|
<span data-ttu-id="8b29c-109">0</span><span class="sxs-lookup"><span data-stu-id="8b29c-109">0</span></span> | <span data-ttu-id="8b29c-110">Tiltsa le a rendszerindítás, a gép konfigurálásával.</span><span class="sxs-lookup"><span data-stu-id="8b29c-110">Disable configuring the machine at boot-up.</span></span> |
<span data-ttu-id="8b29c-111">1</span><span class="sxs-lookup"><span data-stu-id="8b29c-111">1</span></span> | <span data-ttu-id="8b29c-112">Engedélyezze a gép konfigurál a rendszerindítás.</span><span class="sxs-lookup"><span data-stu-id="8b29c-112">Enable configuring the machine at boot-up.</span></span> |
<span data-ttu-id="8b29c-113">2</span><span class="sxs-lookup"><span data-stu-id="8b29c-113">2</span></span> | <span data-ttu-id="8b29c-114">Engedélyezze a konfigurálása a gép csak akkor, ha a DSC van függőben lévő vagy a jelenlegi állapotban.</span><span class="sxs-lookup"><span data-stu-id="8b29c-114">Enable configuring the machine only if DSC is in pending or current state.</span></span> <span data-ttu-id="8b29c-115">Ez az alapértelmezett érték.</span><span class="sxs-lookup"><span data-stu-id="8b29c-115">This is the default value.</span></span> |

## <a name="see-also"></a><span data-ttu-id="8b29c-116">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="8b29c-116">See Also</span></span>

<span data-ttu-id="8b29c-117">Ez a funkció használata első konfigurációk futtatni egy példa: [konfigurálása a virtuális gépek első indításkor DSC használatával](bootstrapDsc.md).</span><span class="sxs-lookup"><span data-stu-id="8b29c-117">For an example of how to use this feature to run configurations at initial boot-up, see [Configure a virtual machines at initial boot-up by using DSC](bootstrapDsc.md).</span></span>
