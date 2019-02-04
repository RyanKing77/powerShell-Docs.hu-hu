---
ms.date: 12/12/2018
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC-erőforrások
ms.openlocfilehash: 1f77b5e6630a2e3de6e1d1a05638f94d2df039ae
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55686067"
---
# <a name="dsc-resources"></a>DSC-erőforrások

>Érvényes: Windows PowerShell 4.0-s, a Windows PowerShell 5.0

Desired State Configuration (DSC) erőforrások építőelemeket biztosít a DSC-konfiguráció. Egy erőforrás vonatkozó beállított (séma) és a PowerShell parancsfájl függvényeket tartalmaz, amelyek a helyi Configuration Manager (LCM)-hívások "Győződjön meg arról, hogy így" tulajdonságok közzététele.

Erőforrás általános-fájlként vagy egy IIS server beállításként jako specifické valami is modellje.  Hasonló erőforrások csoportjainak egyesíti a DSC modul, amely rendszerezi az összes szükséges fájlt egy struktúra, amely hordozható, és hogyan az erőforrások célja, hogy használható azonosításához metaadatokat tartalmaz.

Minden erőforrás rendelkezik egy * sémában, amely meghatározza, hogy az erőforrás használata szükséges a szintaxis egy [konfigurációs](../configurations/configurations.md). Az erőforrás-séma a következő módokon lehet definiálni:

- **"Schema.Mof"** fájlt: A legtöbb erőforrások meghatározása a *séma* "schema.mof" a fájl használatával [Managed Object Format](/windows/desktop/wmisdk/managed-object-format--mof-).
- **"\<Erőforrásnév\>. schema.psm1"** fájlt: [Összetett erőforrások](../configurations/compositeConfigs.md) meghatározása a *séma* a egy "<ResourceName>. schema.psm1" fájlt egy [paraméterblokkban](/powershell/module/microsoft.powershell.core/about/about_functions?view=powershell-6#functions-with-parameters).
- **"\<Erőforrásnév\>.psm1"** fájlt: DSC-erőforrások alapján határozza meg az osztály a *séma* osztály definíciójában. Szintaktikai elemek osztály tulajdonságokként jelöli. További információkért lásd: [about_Classes](/powershell/module/psdesiredstateconfiguration/about/about_classes_and_dsc).

A szintaxist a DSC-erőforrás lekéréséhez használja a [Get-DSCResource](/powershell/module/PSDesiredStateConfiguration/Get-DscResource) parancsmagot a `-Syntax` paraméter. Ez hasonló a használata [Get-Command](/powershell/module/microsoft.powershell.core/get-command) az a `-Syntax` paraméter használatával beolvas parancsmag szintaxisát. A kimenetben láthatja az erőforráshoz, adja meg, hogy egy erőforrás vonatkozóan használt sablon jelennek meg.

```powershell
Get-DscResource -Syntax Service
```

A kimenetben láthatja hasonló lesz a kimenet az alábbi, ha az erőforrás funkcióbeállításainak szintaxis megváltozhatnak a jövőben. A parancsmag szintaxisát, például a *kulcsok* szögletes zárójelek között látható, nem kötelező. A típusok adja meg az adatok minden kulcs vár.

> [!NOTE]
> A **ellenőrizze, hogy** kulcsot nem kötelező megadni, mert alapértelmezés szerint az "E".

```output
Service [String] #ResourceName
{
    Name = [string]
    [BuiltInAccount = [string]{ LocalService | LocalSystem | NetworkService }]
    [Credential = [PSCredential]]
    [Dependencies = [string[]]]
    [DependsOn = [string[]]]
    [Description = [string]]
    [DisplayName = [string]]
    [Ensure = [string]{ Absent | Present }]
    [Path = [string]]
    [PsDscRunAsCredential = [PSCredential]]
    [StartupType = [string]{ Automatic | Disabled | Manual }]
    [State = [string]{ Running | Stopped }]
}
```

Belül a konfigurációt egy **szolgáltatás** erőforrás letiltása ehhez hasonló lehet a **ellenőrizze, hogy** a nyomtatásisor-kezelő szolgáltatást futtató.

> [!NOTE]
> Mielőtt erőforrás konfigurációban, importálnia kell a [Import-DSCResource](../configurations/import-dscresource.md).

```powershell
Configuration TestConfig
{
    # It is best practice to always directly import resources, even if the resource is a built-in resource.
    Import-DSCResource -Name Service
    Node localhost
    {
        # The name of this resource block, can be anything you choose, as long as it is of type [String] as indicated by the schema.
        Service "Spooler:Running"
        {
            Name = "Spooler"
            State = "Running"
        }
    }
}
```

Konfigurációk a azonos erőforrástípusok több példányának is tartalmazhat. Minden példányt egyedi névvel kell rendelkeznie. A következő példában egy második **szolgáltatás** erőforrás letiltása bekerül a "DHCP" szolgáltatás konfigurálásához.

```powershell
Configuration TestConfig
{
    # It is best practice to always directly import resources, even if the resource is a built-in resource.
    Import-DSCResource -Name Service
    Node localhost
    {
        # The name of this resource block, can be anything you choose, as long as it is of type [String] as indicated by the schema.
        Service "Spooler:Running"
        {
            Name = "Spooler"
            State = "Running"
        }

        # To configure a second service resource block, add another Service resource block and use a unique name.
        Service "DHCP:Running"
        {
            Name = "DHCP"
            State = "Running"
        }
    }
}
```

> [!NOTE]
> A PowerShell 5.0-es verziótól kezdve az intellisense lett hozzáadva a DSC. Ez az új funkció lehetővé teszi, hogy \<lapon\> és \<Ctrl + szóköz\> a kulcsnevek automatikus kiegészítés.

![Erőforrás kiegészítés](../media/resource-tabcompletion.png)

## <a name="built-in-resources"></a>Beépített erőforrások

Közösségi erőforrások kívül beépített erőforrások Windows, Linux-erőforrások és a csomópontok közötti függőségek erőforrásokat. A fenti lépések segítségével határozza meg a szintaxis ezeket az erőforrásokat és azok használatát. Ezek az erőforrások kiszolgálása a lapok alapján lettek archiválva **referencia**.

A Windows beépített erőforrásai

* [Archív erőforrás](../reference/resources/windows/archiveResource.md)
* [Környezeti erőforrás](../reference/resources/windows/environmentResource.md)
* [File erőforrás](../reference/resources/windows/fileResource.md)
* [Group erőforrás](../reference/resources/windows/groupResource.md)
* [GroupSet erőforrás](../reference/resources/windows/groupSetResource.md)
* [Log erőforrás](../reference/resources/windows/logResource.md)
* [Package erőforrás](../reference/resources/windows/packageResource.md)
* [ProcessSet erőforrás](../reference/resources/windows/ProcessSetResource.md)
* [Registry erőforrás](../reference/resources/windows/registryResource.md)
* [Script erőforrás](../reference/resources/windows/scriptResource.md)
* [Service erőforrás](../reference/resources/windows/serviceResource.md)
* [ServiceSet erőforrás](../reference/resources/windows/serviceSetResource.md)
* [User erőforrás](../reference/resources/windows/userResource.md)
* [WindowsFeature erőforrás](../reference/resources/windows/windowsFeatureResource.md)
* [WindowsFeatureSet erőforrás](../reference/resources/windows/windowsFeatureSetResource.md)
* [WindowsOptionalFeature erőforrás](../reference/resources/windows/windowsOptionalFeatureResource.md)
* [WindowsOptionalFeatureSet erőforrás](../reference/resources/windows/windowsOptionalFeatureSetResource.md)
* [WindowsPackageCabResource Resource](../reference/resources/windows/windowsPackageCabResource.md)
* [WindowsProcess erőforrás](../reference/resources/windows/windowsProcessResource.md)

[Csomópontok közötti függőségek](../configurations/crossNodeDependencies.md) erőforrások

* [WaitForAll erőforrás](../reference/resources/windows/waitForAllResource.md)
* [WaitForSome erőforrás](../reference/resources/windows/waitForSomeResource.md)
* [WaitForAny erőforrás](../reference/resources/windows/waitForAnyResource.md)

Package Management-erőforrásokkal

* [PackageManagement-erőforrás](../reference/resources/packagemanagement/PackageManagementDscResource.md)
* [PackageManagementSource erőforrás](../reference/resources/packagemanagement/PackageManagementSourceDscResource.md)

Linux-erőforrások

* [Linux archív erőforrás](../reference/resources/linux/lnxArchiveResource.md)
* [Linux környezeti erőforrás](../reference/resources/linux/lnxEnvironmentResource.md)
* [Linux FileLine erőforrás](../reference/resources/linux/lnxFileLineResource.md)
* [Linux-fájl erőforrás](../reference/resources/linux/lnxFileResource.md)
* [Linux-Group erőforrás](../reference/resources/linux/lnxGroupResource.md)
* [Linux-Package erőforrás](../reference/resources/linux/lnxPackageResource.md)
* [Linux-Script erőforrás](../reference/resources/linux/lnxScriptResource.md)
* [Linux-szolgáltatás-erőforrás](../reference/resources/linux/lnxServiceResource.md)
* [Linux SshAuthorizedKeys erőforrás](../reference/resources/linux/lnxSshAuthorizedKeysResource.md)
* [Linux felhasználói erőforrás](../reference/resources/linux/lnxUserResource.md)
