---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 3f73b7cf0cdf033cbd561b3412734692bb7decd7
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/16/2018
ms.locfileid: "34187536"
---
# <a name="allowing-for-identical-duplicate-resources-in-a-configuration"></a><span data-ttu-id="3661a-102">Lehetővé teszi a konfigurációban azonos ismétlődő erőforrások</span><span class="sxs-lookup"><span data-stu-id="3661a-102">Allowing for Identical Duplicate Resources in a Configuration</span></span>

<span data-ttu-id="3661a-103">A DSC engedélyezése vagy nem ütköző erőforrás-definíciókban belül a konfiguráció kezelésére.</span><span class="sxs-lookup"><span data-stu-id="3661a-103">DSC does not allow or handle conflicting resource definitions within a configuration.</span></span> <span data-ttu-id="3661a-104">Helyett megpróbálja feloldani az ütközést, egyszerűen meghiúsul.</span><span class="sxs-lookup"><span data-stu-id="3661a-104">Instead of trying to resolve the conflict, it simply fails.</span></span> <span data-ttu-id="3661a-105">A konfiguráció újbóli több összetett erőforrások révén válik funkcióját, stb. fogja akkor történik ütközés, gyakrabban.</span><span class="sxs-lookup"><span data-stu-id="3661a-105">As configuration reuse becomes more utilized through composite resources, etc. conflicts will occur more often.</span></span> <span data-ttu-id="3661a-106">Amikor ütköző erőforrás-definíciókban azonosak, DSC intelligens legyen, és hogy ez.</span><span class="sxs-lookup"><span data-stu-id="3661a-106">When conflicting resource definitions are identical, DSC should be smart and allow this.</span></span> <span data-ttu-id="3661a-107">Ebben a kiadásban támogatjuk, hogy több erőforrás példánya azonos definíciókkal rendelkeznek:</span><span class="sxs-lookup"><span data-stu-id="3661a-107">With this release, we support having multiple resource instances that have identical definitions:</span></span>

```powershell
Configuration IIS_FrontEnd
{
    WindowsFeature FE_IIS         #Identical resource
    {
        Ensure = 'Present'
        Name = 'Web-Server'
    }

    WindowsFeature FTP
    {
        Ensure = 'Present'
        Name = 'Web-FTP-Server'
    }
}

Configuration IIS_Worker
{
    WindowsFeature Worker_IIS      #Identical resource
    {
        Ensure = 'Present'
        Name = 'Web-Server'
    }

    WindowsFeature ASP
    {
        Ensure = 'Present'
        Name = 'Web-ASP-Net45'
    }
}

Configuration WebApplication
{
    IIS_Frontend Web {}

    IIS_Worker ASP {}
}
```

<span data-ttu-id="3661a-108">A korábbi kiadásokban az eredmény lenne egy WindowsFeature FE_IIS és annak biztosítása érdekében a webalkalmazás-Server szerepkört próbált WindowsFeature Worker_IIS példányok közötti ütközés miatt sikertelen fordítás telepítve van.</span><span class="sxs-lookup"><span data-stu-id="3661a-108">In previous releases, the result would be a failed compilation due to a conflict between the WindowsFeature FE_IIS and WindowsFeature Worker_IIS instances trying to ensure the 'Web-Server' role is installed.</span></span> <span data-ttu-id="3661a-109">Figyelje meg, hogy *összes* az éppen konfigurált tulajdonságok megegyeznek a két konfigurációban.</span><span class="sxs-lookup"><span data-stu-id="3661a-109">Notice that *all* of the properties that are being configured are identical in these two configurations.</span></span> <span data-ttu-id="3661a-110">Mivel *összes* Ez a két tulajdonságokat erőforrások azonosak, ez most a sikeres fordítás eredményez.</span><span class="sxs-lookup"><span data-stu-id="3661a-110">Since *all* of the properties in these two resources are identical, this will result in a successful compilation now.</span></span>

<span data-ttu-id="3661a-111">Tulajdonságok különböznek a két erőforrásnak, ha azok nem veszik figyelembe azonos, és a fordítás sikertelen lesz:</span><span class="sxs-lookup"><span data-stu-id="3661a-111">If any of the properties are different between the two resources, they will not be considered identical and compilation will fail:</span></span>

```powershell
Configuration IIS_FrontEnd
{
    WindowsFeature FE_IIS
    {
        Ensure = 'Present'     # Ensure is Present here
        Name = 'Web-Server'
    }

    WindowsFeature FTP
    {
        Ensure = 'Present'
        Name = 'Web-FTP-Server'
    }
}

Configuration IIS_Worker
{
    WindowsFeature Worker_IIS
    {
        Ensure = 'Absent'      # Ensure property is Absent instead of Present
        Name = 'Web-Server'
    }

    WindowsFeature ASP
    {
        Ensure = 'Present'
        Name = 'Web-ASP-Net45'
    }
}

Configuration WebApplication
{
    IIS_Frontend Web {}

    IIS_Worker ASP {}
}
```

<span data-ttu-id="3661a-112">Ez a nagyon hasonló konfiguráció sikertelen lesz, mert a WindowsFeature FE_IIS és WindowsFeature Worker_IIS erőforrás már nem azonosak, és ezért ütközés lép fel.</span><span class="sxs-lookup"><span data-stu-id="3661a-112">This very similar configuration will fail because the WindowsFeature FE_IIS and the WindowsFeature Worker_IIS resources are no longer identical and therefore conflict.</span></span>
