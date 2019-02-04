---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 28f4f8ae2bbddc8fb5ef9d95d3061a91fcc8ffe2
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55687362"
---
# <a name="allowing-for-identical-duplicate-resources-in-a-configuration"></a>Azonos ismétlődő erőforrások engedélyezése

Nem engedélyezi a DSC, vagy ütköző erőforrás-definíciókban belül a konfiguráció kezelésére. Az ütközés feloldása helyett egyszerűen meghiúsul. Konfiguráció újbóli több összetett erőforrások révén válik fel, mert ütközés stb. fogja gyakrabban fordulnak elő. Amikor az ütköző erőforrás-definíciókban azonosak, DSC legyen intelligens és ez lehetővé teszi. Ebben a kiadásban támogatott több, azonos definíciókkal rendelkező erőforrás példánnyal rendelkező:

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

A korábbi kiadásokban az eredmény lehet a WindowsFeature FE_IIS és annak biztosítása érdekében a webalkalmazás-kiszolgáló szerepkört próbált WindowsFeature Worker_IIS példányok közötti ütközés miatt nem sikerült rendszerezve van telepítve. Figyelje meg, hogy *összes* a folyamatban konfigurált tulajdonságok megegyeznek az alábbi két konfigurációk. Mivel *összes* Ez a két tulajdonság azonos erőforrásokat, emiatt most a sikeres fordítás.

Ha bármely tulajdonsága eltérő a két erőforrás között, nem minősülnek azonos, és a fordítás sikertelen lesz:

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

Ez nagyon hasonló konfigurálása sikertelen lesz, mert a WindowsFeature FE_IIS és a WindowsFeature Worker_IIS erőforrások nem lesznek azonos, és ezért ütköznek.
