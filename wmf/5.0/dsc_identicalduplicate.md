---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "WMF, a powershell, a beállítása"
ms.openlocfilehash: d3a625d05eaf4e7448b4abf90499f6a94e2f7718
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
# <a name="allowing-for-identical-duplicate-resources-in-a-configuration"></a>Lehetővé teszi a konfigurációban azonos ismétlődő erőforrások

A DSC engedélyezése vagy nem ütköző erőforrás-definíciókban belül a konfiguráció kezelésére. Helyett megpróbálja feloldani az ütközést, egyszerűen meghiúsul. A konfiguráció újbóli több összetett erőforrások révén válik funkcióját, stb. fogja akkor történik ütközés, gyakrabban. Amikor ütköző erőforrás-definíciókban azonosak, DSC intelligens legyen, és hogy ez. Ebben a kiadásban támogatjuk, hogy több erőforrás példánya azonos definíciókkal rendelkeznek:

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

A korábbi kiadásokban az eredmény lenne egy WindowsFeature FE_IIS és annak biztosítása érdekében a webalkalmazás-Server szerepkört próbált WindowsFeature Worker_IIS példányok közötti ütközés miatt sikertelen fordítás telepítve van. Figyelje meg, hogy *összes* az éppen konfigurált tulajdonságok megegyeznek a két konfigurációban. Mivel *összes* Ez a két tulajdonságokat erőforrások azonosak, ez most a sikeres fordítás eredményez. 

Tulajdonságok különböznek a két erőforrásnak, ha azok nem veszik figyelembe azonos, és a fordítás sikertelen lesz:

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

Ez a nagyon hasonló konfiguráció sikertelen lesz, mert a WindowsFeature FE_IIS és WindowsFeature Worker_IIS erőforrás már nem azonosak, és ezért ütközés lép fel.

