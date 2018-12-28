---
ms.date: 12/12/2018
keywords: DSC, powershell, erőforrás, katalógus, beállítása
title: További DSC-erőforrások telepítése
ms.openlocfilehash: ecaf176230ccd934b57b1c27d72ff83e6ba906e9
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404355"
---
# <a name="install-additional-dsc-resources"></a>További DSC-erőforrások telepítése

PowerShell Desired State Configuration (DSC) tartalmaz a több-az-beépített erőforrás. A **PSDesiredStateConfiguration** modul tartalmazza az összes elérhető a PowerShell, a meghatározott példányának OOB DSC-erőforrások.

Ez az a PowerShell 4.0-s verzióját és leírását, az erőforrás-funkciókat az OOB-erőforrások listáját.

> [!NOTE]
> Ez a lehetőség egy nem teljes listája az OOB-erőforrások számát az egyes PowerShell-verzió nőtt.

|Forrásanyag  |Leírás  |
|---------|---------|
|**Fájl**|Fájlok és könyvtárak állapotát vezérli. Átmásolja a fájlokat egy **forrás** , egy **cél** frissíti őket, és amikor a **forrás** módosítások összehasonlítja a dátumok, az ellenőrzőösszegek és kivonatokat.|
|**Archívum**|Kibontja a archívumok és a egy adott helyre. Ellenőrzi a megadott archívum **ellenőrzőösszeg**.|
|**Környezet**|Kezeli a környezeti változókat.|
|**Csoport**|Helyi csoportok kezeli, és ellenőrzi a csoport tagságát.|
|**Log**|Írja az üzeneteket a `Microsoft-Windows-Desired State Configuration/Analytic` Eseménynapló.|
|**Csomag**|Telepíti vagy eltávolítja a csomagokat **argumentumok**, **LogPath**, **ReturnCode**, egyéb beállításokat.|
|**Registry**|Kezeli a beállításjegyzék-kulcsokat és értékeket.|
|**Parancsfájl**|Lehetővé teszi, hogy tervezheti meg a saját [get-teszt – set](../resources/get-test-set.md) parancsfájl-blokk.|
|**Service**|Konfigurálja a Windows-szolgáltatások.|
|**Felhasználó** |A helyi felhasználók és attribútumok kezeli.|
|**WindowsFeature**|Szerepkörök és szolgáltatások kezelése.|
|**WindowsProcess**|Konfigurálja a Windows folyamatokat.|

Az OOB-erőforrások lehetővé teszik a gyakori műveletekhez egy jó kiindulási pont. Ha az OOB-erőforrások nem felelnek meg igényeinek, írhat saját [egyéni erőforrás](../resources/authoringResource.md). Ír egy egyéni erőforrás megoldani a problémát, mielőtt a DSC-erőforrások, Microsoft és a PowerShell-Közösség által létrehozott hatalmas számát keresztül kell keresnie.

DSC-erőforrások is talál a [PowerShell-galériából](https://www.powershellgallery.com/) és [GitHub](https://github.com/). DSC-erőforrások is telepítheti közvetlenül a PowerShell konzol használata a [PowerShellGet](/powershell/module/powershellget/).

## <a name="installing-powershellget"></a>A PowerShellGet telepítése

Annak megállapításához, ha már rendelkezik **PowerShell** beszerzése, illetve telepíti azt segítséget szeretne kérni, tekintse meg a következő útmutatót: [A PowerShellGet telepítése](/powershell/gallery/installing-psget).

## <a name="finding-dsc-resources-using-powershellget"></a>A PowerShellGet-modul DSC-erőforrások keresése

Egyszer **PowerShellGet** van telepítve a rendszerén, keresése és telepítése lévő üzemeltetett DSC-erőforrások a [PowerShell-galériából](https://www.powershellgallery.com/).

Először a [Find-DSCResource](/powershell/module/powershellget/find-dscresource) parancsmag DSC-erőforrások megkereséséhez. Futtatásakor `Find-DSCResource` , először, a következő üzenet jelenik meg a "NuGet-szolgáltató" telepítéséhez.

```
PS> Find-DSCResource

NuGet provider is required to continue
PowerShellGet requires NuGet provider version '2.8.5.201' or newer to interact with NuGet-based repositories. The
NuGet provider must be available in 'C:\Program Files\PackageManagement\ProviderAssemblies' or
'C:\Users\xAdministrator\AppData\Local\PackageManagement\ProviderAssemblies'. You can also install the NuGet provider
 by running 'Install-PackageProvider -Name NuGet -MinimumVersion 2.8.5.201 -Force'. Do you want PowerShellGet to
install and import the NuGet provider now?
[Y] Yes  [N] No  [?] Help (default is "Y"):
```

Után lenyomja "y" a "NuGet" szolgáltató van telepítve, telepítheti a PowerShell-galériából DSC-erőforrások listájának megtekintéséhez.

> [!NOTE]
> Listán nem jelenik meg, mert nagyon nagy méretű.

Azt is megadhatja a `-Name` helyettesítő karaktereket használ, paraméter vagy `-Filter` paraméter a keresés szűkítéséhez helyettesítő karakterek nélkül. Ebben a példában megkísérli megtalálni a helyettesítő karakterek használatával "Időzóna" DSC erőforrás.

> [!IMPORTANT]
> Jelenleg nincs tárkötetek a `Find-DSCResource` parancsmagot, amely megakadályozza, hogy a helyettesítő karakterek használatával is a `-Name` és `-Filter` paramétereket. A lenti második példában látható, hogy egy megkerülő megoldás az `Where-Object`.

```
PS> Find-DSCResource -Name *Time*

Name                                Version    ModuleName                          Repository
----                                -------    ----------                          ----------
Carbon_EnvironmentVariable          2.6.0      Carbon                              PSGallery
Carbon_FirewallRule                 2.6.0      Carbon                              PSGallery
Carbon_Group                        2.6.0      Carbon                              PSGallery
Carbon_IniFile                      2.6.0      Carbon                              PSGallery
Carbon_Permission                   2.6.0      Carbon                              PSGallery
Carbon_Privilege                    2.6.0      Carbon                              PSGallery
Carbon_ScheduledTask                2.6.0      Carbon                              PSGallery
Carbon_Service                      2.6.0      Carbon                              PSGallery
TimeZone                            6.0.0.0    ComputerManagementDsc               PSGallery
xTimeZone                           1.8.0.0    xTimeZone                           PSGallery
xSqlServerDefaultDir                1.0.0      mlSqlServerDSC                      PSGallery
xSqlServerMoveDatabaseFiles         1.0.0      mlSqlServerDSC                      PSGallery
xSqlServerSQLDataRoot               1.0.0      mlSqlServerDSC                      PSGallery
xSqlServerStartupParam              1.0.0      mlSqlServerDSC                      PSGallery
```

Is `Where-Object` szűrés részletesebb DSC-erőforrások megkereséséhez. Ez a megközelítés a szűrési paramétereket lévő beépített lassabb lesz.

```
PS> Find-DSCResource | Where-Object {$_.Name -like "Time*"}

Name                                Version    ModuleName                          Repository
----                                -------    ----------                          ----------
TimeZone                            6.0.0.0    ComputerManagementDsc               PSGallery
```

A szűrés további információkért lásd: [Where-Object](/powershell/module/microsoft.powershell.core/where-object).

## <a name="installing-dsc-resources-using-powershellget"></a>DSC-erőforrások a PowerShellGet-modul telepítése

A DSC-erőforrások telepítéséhez használja a [Install-Module](/powershell/module/PowershellGet/Install-Module) megadása mezőben látható a modul neve, a parancsmag **modul** nevét a keresési eredmények között.

A "Időzóna" erőforrás ezért ez a modul telepíti a ebben a példában a "ComputerManagementDSC" modul létezik.

> [!NOTE]
> Nem bízik meg a PowerShell-galériából, ha az alábbi megerősítés a figyelmeztetést látja, és amely az ezt követő utasításokat elkerülésével telepíti.

```
PS> Install-Module -Name ComputerManagementDSC

Untrusted repository
You are installing the modules from an untrusted repository. If you trust this repository, change its
InstallationPolicy value by running the Set-PSRepository cmdlet. Are you sure you want to install the modules from
'PSGallery'?
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "N"):
```

Nyomja le az "y", a modul telepítésének folytatásához. Telepítés után ellenőrizheti, hogy az új erőforrás segítségével telepítve [Get-DSCResource](/powershell/module/PSDesiredStateConfiguration/Get-DscResource).

```
PS> Get-DSCResource -Name TimeZone -Syntax

TimeZone [String] #ResourceName
{
    IsSingleInstance = [string]{ Yes }
    TimeZone = [string]
    [DependsOn = [string[]]]
    [PsDscRunAsCredential = [PSCredential]]
}
```

Megtekintheti továbbá más erőforrások az újonnan telepített modul megadásával a `-ModuleName` paraméter.

```
PS> Get-DSCResource -Module ComputerManagementDSC

ImplementedAs   Name                      ModuleName                     Version    Properties
-------------   ----                      ----------                     -------    ----------
PowerShell      Computer                  ComputerManagementDsc          6.0.0.0    {Name, Credential, DependsOn, ...
PowerShell      OfflineDomainJoin         ComputerManagementDsc          6.0.0.0    {IsSingleInstance, RequestFile...
PowerShell      PowerPlan                 ComputerManagementDsc          6.0.0.0    {IsSingleInstance, Name, Depen...
PowerShell      PowerShellExecutionPolicy ComputerManagementDsc          6.0.0.0    {ExecutionPolicy, ExecutionPol...
PowerShell      ScheduledTask             ComputerManagementDsc          6.0.0.0    {TaskName, ActionArguments, Ac...
PowerShell      TimeZone                  ComputerManagementDsc          6.0.0.0    {IsSingleInstance, TimeZone, D...
PowerShell      VirtualMemory             ComputerManagementDsc          6.0.0.0    {Drive, Type, DependsOn, Initi...
```

## <a name="see-also"></a>Lásd még:

- [Mik azok az erőforrások?](../resources/resources.md)
