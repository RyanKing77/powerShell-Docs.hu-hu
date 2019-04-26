---
ms.date: 06/20/2018
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC PackageManagement erőforrás
ms.openlocfilehash: 18cbbfe0715c82dcfdf4a5fb6ee36ee814e43d3b
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62077619"
---
# <a name="dsc-packagemanagement-resource"></a>DSC PackageManagement erőforrás

A következőkre vonatkozik: Windows PowerShell 4.0-s, Windows PowerShell 5.0, 5.1 Windows PowerShell

A **PackageManagement** erőforrás a Windows PowerShell Desired State Configuration (DSC) telepítéséhez, vagy távolítsa el a felügyeleti csomagban csomagokat a egy célcsomóponttal mechanizmust biztosít. Ezt az erőforrást igényel a **PackageManagement** modulban elérhető [ http://PowerShellGallery.com ](http://PowerShellGallery.com).

> [!IMPORTANT]
> A **PackageManagement** modul kell lennie, mint a következő tulajdonság információkat csak akkor lehet helyes 1.1.7.0 verzió.

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

| Tulajdonság | Leírás |
| --- | --- |
| Név| Megadja a telepítendő vagy eltávolítandó-csomag neve.|
| AdditionalParameters| Szolgáltató paramétereket, amelyek számára az adott szórótábla `Get-Package -AdditionalArguments`. Például a NuGet-szolgáltató adhat át további paraméterek, például a DestinationPath.|
| Győződjön meg, hogy| Meghatározza, hogy a csomag telepítése vagy eltávolítása.|
| MaximumVersion|Adja meg a megengedett maximális verziója a csomagot, amelyet meg szeretne keresni. Ha nem adja hozzá ezt a paramétert, az erőforrás megkeresése a csomag legmagasabb rendelkezésre álló verziója.|
| MinimumVersion|Adja meg a minimális verziója a csomagot, amelyet meg szeretne keresni. Ha nem adja hozzá ezt a paramétert, az erőforrás megkeresi a legmagasabb elérhető verziója a csomagot, amely bármely által megadott maximális megadott verziója is megfelel a _MaximumVersion_ paraméter.|
| ProviderName| Adja meg, amelyhez a csomag keresést, egy szolgáltató nevét. Alkalmazáscsomagok szolgáltató nevének lekéréséhez futtassa a `Get-PackageProvider` parancsmagot.|
| RequiredVersion| Adja meg a telepíteni kívánt csomag pontos verziójának. Ez a paraméter nincs megadva, a DSC-erőforrás telepíti a csomagot, amely bármely által megadott maximális verziója is megfelel a legújabb elérhető verziója a _MaximumVersion_ paraméter.|
| Forrás| A neve, a csomag forrásához, ahol a csomag található. Ez lehet egy URI-t, vagy egy adatforrás regisztrálva `Register-PackageSource` vagy PackageManagementSource DSC-erőforrás.|
| SourceCredential | Itt adható meg egy felhasználói fiókot, amely rendelkezik jogosultságokkal a megadott csomag szolgáltató vagy a forrás csomag telepítéséhez.|

## <a name="additional-parameters"></a>További paraméterek

A következő táblázat felsorolja a AdditionalParameters tulajdonság lehetőségeit.

| Paraméter | Leírás |
| --- | --- |
| DestinationPath| Szolgáltatók, például a beépített Nuget-szolgáltató által használt. A csomagot a telepíteni kívánt fájl helyének megadása.|
| InstallationPolicy| Szolgáltatók, például a beépített Nuget-szolgáltató által használt. Azt határozza meg, hogy megbízható-e a csomag forrásához. Egyik: `Untrusted`, `Trusted`.|

## <a name="example"></a>Példa

Ez a példa telepíti a **JQuery** NuGet-csomagot és **GistProvider** PowerShell modul használatával a **PackageManagement** DSC-erőforrás. Ebben a példában először biztosítja a szükséges csomag adatforrások érhetők el, majd határozza meg a várható állapotát a **JQuery** és **GistProvider** packages (NuGet és a PowerShell, jelölik).

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