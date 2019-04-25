---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 28f4f8ae2bbddc8fb5ef9d95d3061a91fcc8ffe2
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62058726"
---
# <a name="allowing-for-identical-duplicate-resources-in-a-configuration"></a><span data-ttu-id="8884c-102">Azonos ismétlődő erőforrások engedélyezése</span><span class="sxs-lookup"><span data-stu-id="8884c-102">Allowing for Identical Duplicate Resources in a Configuration</span></span>

<span data-ttu-id="8884c-103">Nem engedélyezi a DSC, vagy ütköző erőforrás-definíciókban belül a konfiguráció kezelésére.</span><span class="sxs-lookup"><span data-stu-id="8884c-103">DSC does not allow or handle conflicting resource definitions within a configuration.</span></span> <span data-ttu-id="8884c-104">Az ütközés feloldása helyett egyszerűen meghiúsul.</span><span class="sxs-lookup"><span data-stu-id="8884c-104">Instead of trying to resolve the conflict, it simply fails.</span></span> <span data-ttu-id="8884c-105">Konfiguráció újbóli több összetett erőforrások révén válik fel, mert ütközés stb. fogja gyakrabban fordulnak elő.</span><span class="sxs-lookup"><span data-stu-id="8884c-105">As configuration reuse becomes more utilized through composite resources, etc. conflicts will occur more often.</span></span> <span data-ttu-id="8884c-106">Amikor az ütköző erőforrás-definíciókban azonosak, DSC legyen intelligens és ez lehetővé teszi.</span><span class="sxs-lookup"><span data-stu-id="8884c-106">When conflicting resource definitions are identical, DSC should be smart and allow this.</span></span> <span data-ttu-id="8884c-107">Ebben a kiadásban támogatott több, azonos definíciókkal rendelkező erőforrás példánnyal rendelkező:</span><span class="sxs-lookup"><span data-stu-id="8884c-107">With this release, we support having multiple resource instances that have identical definitions:</span></span>

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

<span data-ttu-id="8884c-108">A korábbi kiadásokban az eredmény lehet a WindowsFeature FE_IIS és annak biztosítása érdekében a webalkalmazás-kiszolgáló szerepkört próbált WindowsFeature Worker_IIS példányok közötti ütközés miatt nem sikerült rendszerezve van telepítve.</span><span class="sxs-lookup"><span data-stu-id="8884c-108">In previous releases, the result would be a failed compilation due to a conflict between the WindowsFeature FE_IIS and WindowsFeature Worker_IIS instances trying to ensure the 'Web-Server' role is installed.</span></span> <span data-ttu-id="8884c-109">Figyelje meg, hogy *összes* a folyamatban konfigurált tulajdonságok megegyeznek az alábbi két konfigurációk.</span><span class="sxs-lookup"><span data-stu-id="8884c-109">Notice that *all* of the properties that are being configured are identical in these two configurations.</span></span> <span data-ttu-id="8884c-110">Mivel *összes* Ez a két tulajdonság azonos erőforrásokat, emiatt most a sikeres fordítás.</span><span class="sxs-lookup"><span data-stu-id="8884c-110">Since *all* of the properties in these two resources are identical, this will result in a successful compilation now.</span></span>

<span data-ttu-id="8884c-111">Ha bármely tulajdonsága eltérő a két erőforrás között, nem minősülnek azonos, és a fordítás sikertelen lesz:</span><span class="sxs-lookup"><span data-stu-id="8884c-111">If any of the properties are different between the two resources, they will not be considered identical and compilation will fail:</span></span>

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

<span data-ttu-id="8884c-112">Ez nagyon hasonló konfigurálása sikertelen lesz, mert a WindowsFeature FE_IIS és a WindowsFeature Worker_IIS erőforrások nem lesznek azonos, és ezért ütköznek.</span><span class="sxs-lookup"><span data-stu-id="8884c-112">This very similar configuration will fail because the WindowsFeature FE_IIS and the WindowsFeature Worker_IIS resources are no longer identical and therefore conflict.</span></span>
