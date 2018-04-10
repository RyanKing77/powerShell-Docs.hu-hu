---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: WMF, powershell, beállítás
title: A WMF 5.1 kibocsátási megjegyzései
ms.openlocfilehash: eb22267c1af28a9fcdd049c76d363fff687f6167
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="windows-management-framework-wmf-51-release-notes"></a>A Windows Management Framework (WMF) 5.1 kibocsátási megjegyzések #

WMF 5.1 összetevői a PowerShell, a WMI, a Rendszerfelügyeleti webszolgáltatások és a szoftverleltár-naplózási (SIL) a Windows Server 2016 kiadott.
A WMF 5.1 Windows 7, Windows 8.1, Windows Server 2008 R2, 2012 és 2012 R2 rendszerre telepíthető, és számos javítást tartalmaz a WMF 5.0 RTM-hez képest, melyek többek között a következők:

- Új parancsmagok: helyi felhasználók és csoportok; Get-ComputerInfo
- A PowerShellGet javításai, többek között az aláírt modulok használatának kényszerítése és a JEA-modulok telepítése
- A PackageManagement mostantól támogatja a Containers szolgáltatást, a CBS-beállítást, az EXE-alapú beállítást és a CAB-csomagokat
- DSC- és PowerShell-osztályok hibakeresési javításai
- Biztonsági fejlesztések: katalógus által aláírt modulok használatának kényszerítése a lekérési kiszolgálóról érkező modulok, illetve PowerShellGet-parancsmagok használata esetén
- Válaszok néhány felhasználói kérésre és problémára

**Fontos megjegyzések:**

- **WMF 5.1 a .NET-keretrendszer 4.5.2-es szükséges** (vagy újabb). Telepítés sikeres lesz, azonban a legfontosabb jellemzők sikertelen lesz, ha a .NET 4.5.2 (vagy újabb) nincs telepítve. Útmutatás a érhető el a [telepítése és konfigurálása a WMF 5.1 ](https://msdn.microsoft.com/powershell/wmf/5.1/install-configure) témakör.
- WMF 5.1 Preview WMF 5.1 RTM telepítése előtt el kell távolítani.
- WMF 5.1 WMF 5.0 vagy a WMF 4.0 keresztül közvetlenül is telepíthető.
- Az __nem szükséges__ WMF 4.0 telepítése WMF 5.1 a Windows 7 és Windows Server 2008 R2 telepítése előtt. Amely WMF 5.1 előzetes problémát, és lett feloldva.