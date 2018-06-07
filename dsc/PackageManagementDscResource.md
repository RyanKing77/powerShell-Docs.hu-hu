---
ms.date: 06/20/2018
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: A DSC PackageManagement erőforrás
ms.openlocfilehash: 3d52934b130d59acee4d7f8a92da2c743c1eb305
ms.sourcegitcommit: 01d6985ed190a222e9da1da41596f524f607a5bc
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/04/2018
ms.locfileid: "34753787"
---
# <a name="dsc-packagemanagement-resource"></a>A DSC PackageManagement erőforrás

> Vonatkozik: A Windows PowerShell 4.0-s verzióját, a Windows PowerShell 5.0, 5.1 Windows PowerShell

A **PackageManagement** erőforrás a Windows PowerShell szükséges konfiguráló (DSC) telepítéséhez vagy eltávolításához egy célcsomóponttal csomag felügyeleti csomagok mechanizmust biztosít. Ehhez az erőforráshoz van szükség a **PackageManagement** modul, a rendelkezésre álló http://PowerShellGallery.com.

> [!IMPORTANT]
> A **PackageManagement** modul kell lennie, mint a következő tulajdonság információk csak akkor lehet helyes 1.1.7.0 verziója.

## <a name="syntax"></a>Szintaxis

```
PackageManagement [string] #ResourceName
{
    Name = [string]
    [AdditionalParameters = [HashTable]]
    [DependsOn = [string[]]]
    [Ensure = [string]{ Absent | Present }]
    [MaximumVersion = [string]]
    [MinimumVersion = [string]]
    [ProviderName = [string]]
    [PsDscRunAsCredential = [PSCredential]]
    [RequiredVersion = [string]]
    [Source = [string]]
    [SourceCredential = [PSCredential]]
}
```

## <a name="properties"></a>Tulajdonságok

|  Tulajdonság  |  Leírás   |
|---|---|
| Név| Megadja a telepítendő vagy eltávolítandó-csomag nevét.|
| AdditionalParameters| Szolgáltató adott kivonattábla, amely átadandó paraméterek `Get-Package -AdditionalArguments`. Például NuGet-szolgáltató is át további paraméterek, például a DestinationPath.|
| Győződjön meg arról| Meghatározza, hogy a csomag telepítendő vagy eltávolítandó.|
| MaximumVersion|Adja meg a megengedett a csomagot, amely a keresett verzióját. Ha nem adja hozzá ezt a paramétert, az erőforrás megkeresése a csomag legmagasabb rendelkezésre álló verziója.|
| MinimumVersion|Adja meg a minimális verziója a csomagot, amely a keresett engedélyezett. Ha nem adja hozzá ezt a paramétert, az erőforrás megkeresése a csomagot, amely megfelel minden maximális megadott verziója által megadott legmagasabb rendelkezésre álló verziója a _MaximumVersion_ paraméter.|
| ProviderName| A csomag szolgáltató nevét, amelyhez a csomag keresés hatókörének megadása Csomag a szolgáltatói nevet lekéréséhez futtassa a `Get-PackageProvider` parancsmag.|
| RequiredVersion| Adja meg a telepíteni kívánt csomag pontos verziójának. Ha ez a paraméter nincs megadva, a DSC-erőforrás telepíti-e a csomagot, amely megfelel a megadott maximális verziója elérhető legújabb verzióját a _MaximumVersion_ paraméter.|
| Forrás| Megadja a nevét, a csomag forrás, ahol a csomag található. Ez lehet egy URI-t, vagy egy adatforrás regisztrálva a `Register-PackageSource` vagy PackageManagementSource DSC-erőforrást.|
| SourceCredential | Adja meg egy felhasználói fiókot, amely a megadott csomag szolgáltató vagy a forrás csomag telepítéséhez jogosultsággal rendelkezik.|

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
        SourceLocation   = "http://nuget.org/api/v2/"
        InstallationPolicy ="Trusted"
    }

    PackageManagementSource PSGallery
    {
        Ensure      = "Present"
        Name        = "psgallery"
        ProviderName= "PowerShellGet"
        SourceLocation   = "https://www.powershellgallery.com/api/v2/"
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