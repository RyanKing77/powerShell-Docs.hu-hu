---
ms.date: 06/12/2017
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: A DSC PackageManagement erőforrás
ms.openlocfilehash: f850c389214fe5adf139c3bd01fb60addc5ec238
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/16/2018
---
# <a name="dsc-packagemanagement-resource"></a>A DSC PackageManagement erőforrás

> Vonatkozik: A Windows PowerShell 4.0-s verzióját, a Windows PowerShell 5.0

A **PackageManagement** erőforrás a Windows PowerShell szükséges konfiguráló (DSC) telepítéséhez vagy eltávolításához egy célcsomóponttal csomag felügyeleti csomagok mechanizmust biztosít. Ehhez az erőforráshoz van szükség a **PackageManagement** modul, a rendelkezésre álló http://PowerShellGallery.com.

## <a name="syntax"></a>Szintaxis

```
PackageManagement [string] #ResourceName
{
    Name = [string]
    [ Source = [string] ]
    [ Ensure = [string] { Absent | Present }  ]
    [ RequiredVersion = [string] ]
    [ MinimumVersion = [string] ]
    [ MaximumVersion = [string] ]
    [ SourceCredential = [PSCredential] ]
    [ ProviderName = [string] ]
    [ AdditionalParameters = [Microsoft.Management.Infrastructure.CimInstance[]] ]
}
```

## <a name="properties"></a>Tulajdonságok
|  Tulajdonság  |  Leírás   |
|---|---|
| Név| Megadja a telepítendő vagy eltávolítandó-csomag nevét.|
| Forrás| Megadja a nevét, a csomag forrás, ahol a csomag található. Ez lehet egy URI-t, vagy egy adatforrás regisztrálva a Register-PackageSource vagy PackageManagementSource DSC erőforrás. A DSC-erőforrás MSFT_PackageManagementSource is regisztrálhatja a csomag forrásához.|
| Győződjön meg arról| Meghatározza, hogy a csomag telepítendő vagy eltávolítandó.|
| RequiredVersion| Adja meg a telepíteni kívánt csomag pontos verziójának. Ez a paraméter nincs megadva, a DSC-erőforrás a csomagot, amely megfelel a MaximumVersion paraméter által megadott maximális bármilyen elérhető legújabb verzióját telepíti.|
| MinimumVersion| Adja meg a munkaszálak a telepíteni kívánt csomag verzióját. Ha nem adja hozzá ezt a paramétert, a DSC-erőforrás intalls a csomagot, amely megfelel a megadott maximális verziója elérhető legmagasabb verzióját a MaximumVersion paraméterrel megadott.|
| MaximumVersion| Adja meg a megengedett a telepíteni kívánt csomag verzióját. Ha ez a paraméter nincs megadva, a DSC-erőforrás a legmagasabb számú elérhető verzióját telepíti a csomag.|
| SourceCredential | Adja meg egy felhasználói fiókot, amely a megadott csomag szolgáltató vagy a forrás csomag telepítéséhez jogosultsággal rendelkezik.|
| ProviderName| A csomag szolgáltató nevét, amelyhez a csomag keresés hatókörének megadása A Get-PackageProvider parancsmag futtatásával kaphat a csomag a szolgáltatói nevet.|
| AdditionalParameters| Szolgáltató adott paraméterek átadása pedig egy kivonattáblát. Például NuGet-szolgáltató is át további paraméterek, például a DestinationPath.|

## <a name="additional-parameters"></a>További paraméterek
A következő táblázat felsorolja a AdditionalParameters tulajdonság lehetőségeit.
|  Paraméter  | Leírás   |
|---|---|
| DestinationPath| Például a beépített Nuget-szolgáltatót a szolgáltatók használják. A csomagot a telepíteni kívánt fájl helyének megadása.|
| InstallationPolicy| Például a beépített Nuget-szolgáltatót a szolgáltatók használják. Meghatározza, hogy megbízható-e a csomag forrásához. Egyik: "Nem megbízható", "Megbízható".|

## <a name="example"></a>Példa

Ez a példa telepíti a **JQuery** NuGet-csomagot és **GistProvider** PowerShell modul használatával a **PackageManagement** DSC-erőforrás. Ez a példa első biztosítja a szükséges csomag források érhetők el, majd határozza meg a várt állapota a **JQuery** és **GistProvider** csomagok (NuGet és a PowerShell használatával, illetve).

```powershell
Configuration PackageTest
{
    PackageManagementSource SourceRepository
    {
        Ensure      = "Present"
        Name        = "MyNuget"
        ProviderName= "Nuget"
        SourceUri   = "http://nuget.org/api/v2/"
        InstallationPolicy ="Trusted"
    }

    PackageManagementSource PSGallery
    {
        Ensure      = "Present"
        Name        = "psgallery"
        ProviderName= "PowerShellGet"
        SourceUri   = "https://www.powershellgallery.com/api/v2/"
        InstallationPolicy ="Trusted"
    }

    PackageManagement NugetPackage
    {
        Ensure               = "Present"
        Name                 = "JQuery"
        AdditionalParameters = "$env:HomeDrive\nuget"
        RequiredVersion      = "2.0.1"
        DependsOn            = "[PackageManagementSource]SourceRepository"
    }

    PackageManagement PSModule
    {
        Ensure               = "Present"
        Name                 = "gistprovider"
        Source               = "PSGallery"
        DependsOn            = "[PackageManagementSource]PSGallery"
    }
}
```