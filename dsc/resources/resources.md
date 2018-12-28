---
ms.date: 12/12/2018
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC-erőforrások
ms.openlocfilehash: 542a210ab47c650eac625108a78e76bc2cd55572
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404190"
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

![Erőforrás kiegészítés](/media/resource-tabcompletion.png)
