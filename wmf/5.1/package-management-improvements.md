---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: WMF, powershell, beállítás
contributor: jianyunt, quoctruong
title: A WMF 5.1 csomag felügyeleti fejlesztései
ms.openlocfilehash: d8b66cc101a6d963b484bba26a1bcd7f71437536
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="improvements-to-package-management-in-wmf-51"></a>A WMF 5.1# csomag felügyeleti fejlesztései

## <a name="improvements-in-packagemanagement"></a>PackageManagement fejlesztései ##
A WMF 5.1 a javításai a következők:

### <a name="version-alias"></a>Verzió-Alias

**A forgatókönyv**: Ha 1.0-s és 2.0-s egy csomagot, P1, a rendszerre telepített, és el szeretné távolítani az 1.0-s verzióját kell futtatni `Uninstall-Package -Name P1 -Version 1.0` , és elvárják, a parancsmag futtatása után a rendszer eltávolítja az 1.0-s verziója. Az eredménye, hogy 2.0-s verziójának lekérdezi eltávolítva.

Ez akkor fordul elő, mert a `-Version` paramétere az alias a `-MinimumVersion` paraméter. PackageManagement 1.0 minimális verziója minősített csomaghoz keres, amikor a legújabb verzióra adja vissza. Ez a viselkedés normál esetben elvárható, hiszen a legújabb verzió: általában a kívánt eredményt keresése. Azonban ez nem vonatkozik a `Uninstall-Package` eset.

**Megoldás**: eltávolított `-Version` alias teljes egészében a PackageManagement (más néven OneGet) és PowerShellGet.

### <a name="multiple-prompts-for-bootstrapping-the-nuget-provider"></a>Több kér a NuGet-szolgáltató rendszerindítása

**A forgatókönyv**: futtatásakor `Find-Module` vagy `Install-Module` vagy a NuGet-szolgáltató bootstrap próbál más PackageManagement parancsmagok PackageManagement első elindításakor a számítógépen. Teszi ezt, mert a PowerShellGet szolgáltató is használ a NuGet-szolgáltató letöltése a PowerShell-modulok. PackageManagement majd felszólítja a felhasználót, telepítse a NuGet-szolgáltatót engedélyt. Miután a felhasználó a "yes", a betöltéshez gombra kattint, a NuGet-szolgáltató legújabb verzióját telepíti.

Azonban bizonyos esetekben egy régi verziója NuGet-szolgáltató telepítve a számítógépre, hogy a régebbi verziójú NuGet néha lekérdezi betöltött először a PowerShell-munkamenetbe (Ez a versenyhelyzet PackageManagement). Azonban PowerShellGet hozni a NuGet-szolgáltató működése érdekében újabb verzióját, így PowerShellGet rendszerindításának újra a NuGet-szolgáltató PackageManagement kéri. Ennek eredményeképp a NuGet-szolgáltató rendszerindítása több kér.

**Megoldás**: WMF5.1, PackageManagement betölti a NuGet-szolgáltató több kér a NuGet-szolgáltató rendszerindítása elkerülése érdekében a legújabb verzióra.

Dolgozunk ennek sikerült is kézzel törölje a régi verzióját a NuGet-szolgáltató (NuGet-Anycpu.exe), ha a probléma van a $env: ProgramFiles\PackageManagement\ProviderAssemblies $env: LOCALAPPDATA\PackageManagement\ProviderAssemblies


### <a name="support-for-packagemanagement-on-computers-with-intranet-access-only"></a>Azokon a számítógépeken csak az intranetes hozzáférés PackageManagement támogatása

**A forgatókönyv**: a vállalati forgatókönyvhöz, személyek dolgozik a környezet esetén nincs Internet-hozzáféréssel, de az Intranet csak. PackageManagement ebben az esetben nem támogatja a WMF 5.0.

**A forgatókönyv**: A WMF 5.0, PackageManagement nem támogatja csak Intranet (de nem Internet) rendelkező számítógépek hozzáférést.

**Megoldás**: A WMF 5.1 teszi lehetővé az Intranet PackageManagement használni ezeket a lépéseket követheti:

1. Töltse le a NuGet-szolgáltató használatával internetkapcsolattal rendelkező másik számítógép segítségével `Install-PackageProvider -Name NuGet`.

2. A NuGet-szolgáltató vagy alatt található `$env:ProgramFiles\PackageManagement\ProviderAssemblies\nuget` vagy `$env:LOCALAPPDATA\PackageManagement\ProviderAssemblies\nuget`.

3. A bináris fájlok másolása egy mappát vagy hálózati megosztás helyét, az intranetes számítógép eléréséhez, és telepítse a NuGet-szolgáltató `Install-PackageProvider -Name NuGet -Source <Path to folder>`.


### <a name="event-logging-improvements"></a>Esemény naplózása fejlesztései

Csomagok telepítése, amikor módosítja a számítógép állapotát. A WMF 5.1 PackageManagement most események naplózása a Windows eseménynaplójában keresse meg `Install-Package`, `Uninstall-Package`, és `Save-Package` tevékenységeket. Az Eseménynapló számára ugyanúgy kell PowerShell, ez azt jelenti, hogy `Microsoft-Windows-PowerShell, Operational`.

### <a name="support-for-basic-authentication"></a>Alapszintű hitelesítés támogatása

WMF 5.1 PackageManagement keresése és csomagok telepítése a tárházból alapszintű hitelesítést támogatja. Megadhatja, hogy a hitelesítő adatait a `Find-Package` és `Install-Package` parancsmagok. Például:

``` PowerShell
Find-Package -Source <SourceWithCredential> -Credential (Get-Credential)
```
### <a name="support-for-using-packagemanagement-behind-a-proxy"></a>A rendszer proxy mögött PackageManagement használatának támogatása

A WMF 5.1 PackageManagement most paraméterek fogadja el új proxy `-ProxyCredential` és `-Proxy`. Ezek a paraméterek használatával megadhatja a proxy URL-címe és PackageManagement parancsmagokkal hitelesítő adatokat. Alapértelmezés szerint a rendszer proxybeállítások vannak érvényben. Például:

``` PowerShell
Find-Package -Source http://www.nuget.org/api/v2/ -Proxy http://www.myproxyserver.com -ProxyCredential (Get-Credential)
```