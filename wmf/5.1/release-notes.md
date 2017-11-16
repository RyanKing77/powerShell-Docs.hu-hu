---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "WMF, a powershell, a beállítása"
title: "WMF 5.1 kibocsátási megjegyzései"
ms.openlocfilehash: ce9bc7791facfcc2cce9468689e88a26154bda7d
ms.sourcegitcommit: 3f49bd2e0b786e69c71393c00ad85d05a8466753
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/04/2017
---
# <a name="windows-management-framework-wmf-51-release-notes"></a>A Windows Management Framework (WMF) 5.1 kibocsátási megjegyzések #

WMF 5.1 összetevői a PowerShell, a WMI, a Rendszerfelügyeleti webszolgáltatások és a szoftverleltár-naplózási (SIL) a Windows Server 2016 kiadott.
WMF 5.1 telepíthető Windows 7, Windows 8.1, Windows Server 2008 R2, 2012 és 2012 R2-ben, és számos fejlesztéssel biztosítanak WMF 5.0 RTM többek között:

- Új parancsmagok: helyi felhasználók és csoportok; Get-ComputerInfo
- PowerShellGet fejlesztései magukban foglalják a aláírt modulok érvényesítése és a JEA-modulok telepítése
- PackageManagement tárolók, CBS telepítő EXE-alapú telepítő, a CAB-csomagok támogatása
- A DSC-ből és a PowerShell osztályok hibakeresési fejlesztései
- Biztonsági fejlesztések többek között a katalógus által aláírt modulok PowerShellGet parancsmagok használata esetén a lekérni a kiszolgálóról, és onnan érkező érvényesítése
- Válaszokat ad a felhasználói kérelmek és problémák száma

**Fontos megjegyzések:**

- **WMF 5.1 a .NET-keretrendszer 4.5.2-es szükséges** (vagy újabb). Telepítés sikeres lesz, azonban a legfontosabb jellemzők sikertelen lesz, ha a .NET 4.5.2 (vagy újabb) nincs telepítve. Útmutatás a érhető el a [telepítése és konfigurálása a WMF 5.1 ](https://msdn.microsoft.com/en-us/powershell/wmf/5.1/install-configure) témakör.
- WMF 5.1 Preview WMF 5.1 RTM telepítése előtt el kell távolítani.
- WMF 5.1 WMF 5.0 vagy a WMF 4.0 keresztül közvetlenül is telepíthető.
- Az __nem szükséges__ WMF 4.0 telepítése WMF 5.1 a Windows 7 és Windows Server 2008 R2 telepítése előtt. Amely WMF 5.1 előzetes problémát, és lett feloldva.  


