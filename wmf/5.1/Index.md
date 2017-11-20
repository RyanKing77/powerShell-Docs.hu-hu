---
ms.date: 2017-08-12
author: JKeithB
ms.topic: reference
keywords: "WMF, powershell, beállítás"
title: "A WMF 5.1 kibocsátási megjegyzései"
ms.openlocfilehash: 3a6b7fb84d679d9bbe7a89e30c8c769e26f7381a
ms.sourcegitcommit: 4102ecc35d473211f50a453f6ae3fbea31cb3428
ms.translationtype: HT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/04/2017
---
# <a name="windows-management-framework-wmf-51"></a>Windows Management Framework (WMF) 5.1 #

A WMF-fel a felhasználók frissíthetik meglévő Windowsos rendszereiket a PowerShell-, a WMI-, a WinRM- és a Szoftverleltár-naplózási (SIL) összetevő a Windows Server 2016-ban kiadott verzióira. 

A WMF 5.1 Windows 7, Windows 8.1, Windows Server 2008 R2, 2012 és 2012 R2 rendszerre telepíthető, és számos javítást tartalmaz a WMF 5.0 RTM-hez képest, melyek többek között a következők:

- Új parancsmagok: helyi felhasználók és csoportok; Get-ComputerInfo
- A PowerShellGet javításai, többek között az aláírt modulok használatának kényszerítése és a JEA-modulok telepítése
- A PackageManagement mostantól támogatja a Containers szolgáltatást, a CBS-beállítást, az EXE-alapú beállítást és a CAB-csomagokat
- DSC- és PowerShell-osztályok hibakeresési javításai
- Biztonsági fejlesztések: katalógus által aláírt modulok használatának kényszerítése a lekérési kiszolgálóról érkező modulok, illetve PowerShellGet-parancsmagok használata esetén
- Válaszok néhány felhasználói kérésre és problémára

Ha többet szeretne megtudni a kiadás újdonságairól, tekintse meg az [Új forgatókönyvek és funkciók](https://docs.microsoft.com/en-us/powershell/wmf/5.1/scenarios-features) szakasz témaköreit. 

A [Telepítés és konfigurálás](https://docs.microsoft.com/en-us/powershell/wmf/5.1/install-configure) témakör a WMF követelményeit és telepítési utasításait ismerteti. 

A [Kompatibilitás](https://docs.microsoft.com/en-us/powershell/wmf/5.1/compatibility) témakör ismerteti, mely WMF-verziók mely Windows-kiadásokon telepíthetők. 

A [Termékkompatibilitás](https://docs.microsoft.com/en-us/powershell/wmf/5.1/productincompat) témakör azokat a Microsoft-alkalmazásokat sorolja fel, amelyek még nem támogatják a WMF 5.1 szolgáltatást. 

A WMF összetevőiről részletes információt az MSDN-dokumentációban találhat:

- [PowerShell 5.1](https://docs.microsoft.com/en-us/powershell/) 
- [WMI](https://msdn.microsoft.com/en-us/library/jj152383(v=vs.85).aspx)
- [WinRM](https://msdn.microsoft.com/en-us/library/aa384426(v=vs.85).aspx)
- [Szoftverleltár-naplózás](https://technet.microsoft.com/en-us/library/dn383584(v=ws.11).aspx)

