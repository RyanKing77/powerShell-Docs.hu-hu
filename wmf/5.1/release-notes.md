---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: WMF, powershell, beállítás
title: A WMF 5.1 kibocsátási megjegyzései
ms.openlocfilehash: 61ca854cf8f26a9e96c6c5b5c06f6b54d08fb4ea
ms.sourcegitcommit: 5990f04b8042ef2d8e571bec6d5b051e64c9921c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/12/2019
ms.locfileid: "57795011"
---
# <a name="windows-management-framework-wmf-51-release-notes"></a>Windows Management Framework (WMF) 5.1 kibocsátási megjegyzései

A WMF 5.1 összetevői a PowerShell, a WMI, a Rendszerfelügyeleti webszolgáltatások és a szoftverleltár-naplózási (SIL) kiadott – Windows Server 2016-ban.
A WMF 5.1 Windows 7, Windows 8.1, Windows Server 2008 R2, 2012 és 2012 R2 rendszerre telepíthető, és számos javítást tartalmaz a WMF 5.0 RTM-hez képest, melyek többek között a következők:

- Új parancsmagok: helyi felhasználók és csoportok; Get-ComputerInfo
- A PowerShellGet javításai, többek között az aláírt modulok használatának kényszerítése és a JEA-modulok telepítése
- A PackageManagement mostantól támogatja a Containers szolgáltatást, a CBS-beállítást, az EXE-alapú beállítást és a CAB-csomagokat
- DSC- és PowerShell-osztályok hibakeresési javításai
- Biztonsági fejlesztések: katalógus által aláírt modulok használatának kényszerítése a lekérési kiszolgálóról érkező modulok, illetve PowerShellGet-parancsmagok használata esetén
- Válaszok néhány felhasználói kérésre és problémára

**Fontos megjegyzések:**

- **A WMF 5.1 szükséges a .NET-keretrendszer 4.5.2-es** (vagy újabb). Telepítés sikeres lesz, de a legfontosabb jellemzők sikertelen lesz, ha a .NET 4.5.2-es (vagy újabb) nincs telepítve. Útmutatást a [telepítése és konfigurálása a WMF 5.1-es](https://msdn.microsoft.com/powershell/wmf/5.1/install-configure) témakör.
- A WMF 5.1-es előzetes verzió a WMF 5.1 RTM telepítése előtt el kell távolítani.
- A WMF 5.1 közvetlenül a WMF 5.0 vagy a WMF 4.0 keresztül lehet telepíteni.
- Ez __nem szükséges__ WMF 4.0 telepítése a WMF 5.1 Windows 7 és Windows Server 2008 R2 telepítése előtt. Amely a WMF 5.1-es előzetes kiadásban történt, és lett feloldva.
