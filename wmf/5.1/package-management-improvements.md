---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: WMF, powershell, beállítás
contributor: jianyunt, quoctruong
title: A WMF 5.1 csomagkezelés fejlesztései
ms.openlocfilehash: 30ef59ed9dc0d56636d85cc6e53523a9a73963a4
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62055615"
---
# <a name="improvements-to-package-management-in-wmf-51"></a>A WMF 5.1 csomagkezelés fejlesztései

## <a name="improvements-in-packagemanagement"></a>A PackageManagement fejlesztései

A WMF 5.1 a javításokat az alábbiak:

### <a name="version-alias"></a>Version Alias

**A forgatókönyv**: 1.0-s és a egy csomagot, P1, a rendszerre telepített 2.0-s verziót használja-e, és el szeretné távolítani az 1.0-s verzióját, futtatná `Uninstall-Package -Name P1 -Version 1.0` és a parancsmag futtatása után el kell távolítani az 1.0-s verzióját. Azonban az eredmény a 2.0-s verziójának beolvasása eltávolítja.

Ez akkor fordul elő, mert a `-Version` paraméter egy aliast a `-MinimumVersion` paraméter. A PackageManagement az 1.0-s verziójával minősített csomagot keres, ha a legújabb verziót adja vissza. Ez a viselkedés a normál esetben elvárható, hiszen a keresés, a legújabb verzióra általában a kívánt eredményt. Azonban ez nem vonatkozik a `Uninstall-Package` eset.

**Megoldás**: eltávolított `-Version` alias teljes egészében a PackageManagement (más néven) OneGet), és a PowerShellGet.

### <a name="multiple-prompts-for-bootstrapping-the-nuget-provider"></a>A NuGet-szolgáltató rendszerindításra több utasításokat

**A forgatókönyv**: Futtatásakor `Find-Module` vagy `Install-Module` vagy más PackageManagement-parancsmagok a számítógép első elindításakor a PackageManagement próbál meg a NuGet-szolgáltató elindíthat. Ezt hajtja végre, mert a PowerShellGet szolgáltató is használ a NuGet-szolgáltató letöltése a PowerShell-modulok. A PackageManagement majd felszólítja a felhasználót, telepítse a NuGet-szolgáltató engedélyt. Miután a felhasználó az "Igen", a rendszerindításra választja, a NuGet-szolgáltató legújabb verzióját telepíti.

Azonban bizonyos esetekben egy régi verziója NuGet-szolgáltató ugyanarra a számítógépre telepítve, a régebbi verzió néha lekérdezi betöltötte először (Ez a versenyhelyzet PackageManagement) PowerShell-munkamenetbe. Azonban az PowerShellGet a NuGet-szolgáltató használatát újabb verziója szükséges, így a PowerShellGet PackageManagement újra elindíthat a NuGet-szolgáltató. Ennek eredményeképpen a NuGet-szolgáltató rendszerindításra több utasításokat.

**Megoldás**: PackageManagement WMF5.1, betölti a NuGet-szolgáltató rendszerindításra több utasításokat elkerülése érdekében a NuGet-szolgáltató legújabb verzióját.

Ezt a problémát úgy is működhetnek (NuGet-Anycpu.exe) NuGet-szolgáltató régebbi verzióját manuálisan törlésével, ha a probléma $env létezik: ProgramFiles\PackageManagement\ProviderAssemblies $env: LOCALAPPDATA\PackageManagement\ProviderAssemblies


### <a name="support-for-packagemanagement-on-computers-with-intranet-access-only"></a>A PackageManagement a számítógépeken csak az intranetes hozzáférés támogatása

**A forgatókönyv**: A vállalati forgatókönyvhöz az ember dolgozik környezet alapján, ha ott nem nincs Internet-hozzáférést, de az intranetes csak. A PackageManagement ebben az esetben a WMF 5.0 nem támogat.

**A forgatókönyv**: A WMF 5.0-s PackageManagement nem támogatták a csak Intranet (de nem az interneten) rendelkező számítógépek hozzáférést.

**Megoldás**: A WMF 5.1 hajtsa végre ezeket a lépéseket, hogy az intranetes számítógépekhez PackageManagement használatára:

1. Töltse le a NuGet-szolgáltató használatával egy másik számítógépre, az internetkapcsolattal rendelkező `Install-PackageProvider -Name NuGet`.

2. Keresse meg a NuGet-szolgáltató szakaszban `$env:ProgramFiles\PackageManagement\ProviderAssemblies\nuget` vagy `$env:LOCALAPPDATA\PackageManagement\ProviderAssemblies\nuget`.

3. A bináris fájlok másolását egy mappát vagy hálózati megosztási helyre, amely az intranetes számítógép eléréséhez, és telepítse a NuGet-szolgáltató `Install-PackageProvider -Name NuGet -Source <Path to folder>`.


### <a name="event-logging-improvements"></a>Esemény naplózása fejlesztései

Csomagokat telepíteni, ha módosítja a számítógép állapotát. A WMF 5.1-es, a PackageManagement mostantól rögzíti eseményeket, a Windows eseménynaplójában keresse meg a `Install-Package`, `Uninstall-Package`, és `Save-Package` tevékenységeket. Az Eseménynapló rendszer ugyanaz, mint a PowerShell-lel, azt jelenti, `Microsoft-Windows-PowerShell, Operational`.

### <a name="support-for-basic-authentication"></a>Alapszintű hitelesítés támogatása

A WMF 5.1-es a PackageManagement támogatja a Keresés és a egy adattárból, amely egyszerű hitelesítés szükséges csomagok telepítése. A hitelesítő adatokat, megadhatja a `Find-Package` és `Install-Package` parancsmagok. Például:

``` PowerShell
Find-Package -Source <SourceWithCredential> -Credential (Get-Credential)
```

### <a name="support-for-using-packagemanagement-behind-a-proxy"></a>PackageManagement használatával a rendszer proxy mögött támogatása

A WMF 5.1-es, a PackageManagement mostantól új proxy paraméter szükséges `-ProxyCredential` és `-Proxy`. Ezeket a paramétereket használja, megadhatja a proxykiszolgáló URL-cím és a PackageManagement-parancsmagok hitelesítő adatait. Alapértelmezés szerint systémová nastavení proxy serveru szolgálnak. Például:

``` PowerShell
Find-Package -Source http://www.nuget.org/api/v2/ -Proxy http://www.myproxyserver.com -ProxyCredential (Get-Credential)
```
