---
ms.date: 12/12/2018
keywords: DSC, PowerShell, erőforrás, katalógus, beállítás
title: Paraméterek hozzáadása konfigurációkhoz
ms.openlocfilehash: 72e6c15593d11ed39d7fe8ea79f794089f410cf8
ms.sourcegitcommit: d1ba596f9e0d4df9565601a70687a126d535c917
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/05/2019
ms.locfileid: "70386317"
---
# <a name="add-parameters-to-a-configuration"></a>Paraméterek hozzáadása konfigurációkhoz

A függvényekhez hasonlóan a [konfigurációk](configurations.md) paraméterei is lehetővé teszik, hogy a felhasználók bevitele alapján több dinamikus konfigurációt engedélyezzen. A lépések hasonlóak a [függvények paraméterrel](/powershell/module/microsoft.powershell.core/about/about_functions)ismertetett műveletekhez.

Ez a példa egy alapszintű konfigurációval kezdődik, amely úgy konfigurálja a "sorkezelő" szolgáltatást, hogy "fut".

```powershell
Configuration TestConfig
{
    # It is best practice to explicitly import any required resources or modules.
    Import-DSCResource -Module PSDesiredStateConfiguration

    Node localhost
    {
        Service 'Spooler'
        {
            Name = 'Spooler'
            State = 'Running'
        }
    }
}
```

## <a name="built-in-configuration-parameters"></a>Beépített konfigurációs paraméterek

A függvényektől eltérően a [CmdletBinding](/powershell/module/microsoft.powershell.core/about/about_functions_cmdletbindingattribute) attribútum nem hoz létre funkciókat. A [gyakori paraméterek](/powershell/module/microsoft.powershell.core/about/about_commonparameters)mellett a konfigurációk a következő beépített paramétereket is használhatják, anélkül, hogy meg kellene határozni őket.

|Paraméter  |Leírás  |
|---------|---------|
|`-InstanceName`|[Összetett konfigurációk](compositeconfigs.md) definiálásakor használatos|
|`-DependsOn`|[Összetett konfigurációk](compositeconfigs.md) definiálásakor használatos|
|`-PSDSCRunAsCredential`|[Összetett konfigurációk](compositeconfigs.md) definiálásakor használatos|
|`-ConfigurationData`|A konfigurációban használható strukturált [konfigurációs adatbevitelre](configData.md) szolgál.|
|`-OutputPath`|Annak megadására szolgál,\<hogy\>a "számítógépnév. MOF" fájl hol lesz lefordítva|

## <a name="adding-your-own-parameters-to-configurations"></a>Saját paraméterek hozzáadása a konfigurációkhoz

A beépített paraméterek mellett saját paramétereket is hozzáadhat a konfigurációkhoz. A Block paraméter közvetlenül a konfigurációs deklarációban található, ugyanúgy, mint a függvény. A konfigurációs paraméterek blokkjának a **csomópont** deklarációján kívül kell lennie, és minden *importálási* utasítás felett kell lennie. Paraméterek hozzáadásával a konfigurációk robusztusabb és dinamikusak lehetnek.

```powershell
Configuration TestConfig
{
    param
    (

    )
```

### <a name="add-a-computername-parameter"></a>Számítógépnév-paraméter hozzáadása

Az első paraméter, amelyet hozzáadhat, egy `-Computername` paraméter, így dinamikusan lefordíthatja a ". MOF" fájlt `-Computername` a konfigurációba való átadáshoz. A függvényekhez hasonlóan megadhat egy alapértelmezett értéket is abban az esetben, ha a felhasználó nem ad át értéket a következőnek:`-ComputerName`

```powershell
param
(
    [String]
    $ComputerName="localhost"
)
```

A konfiguráción belül megadhatja a `-ComputerName` paramétert a csomópont-blokk definiálásakor.

```powershell
Node $ComputerName
{

}
```

### <a name="calling-your-configuration-with-parameters"></a>A konfiguráció meghívása paraméterekkel

Miután hozzáadta a paramétereket a konfigurációhoz, azokat ugyanúgy használhatja, mint a parancsmagot.

```powershell
TestConfig -ComputerName "server01"
```

### <a name="compiling-multiple-mof-files"></a>Több. MOF fájl fordítása

A csomópont-blokk is elfogadhatja a számítógépek neveinek vesszővel tagolt listáját, és mindegyikhez ". MOF" fájlokat fog készíteni. A következő példa futtatásával létrehozhat ". MOF" fájlokat a `-ComputerName` paraméternek átadott összes számítógép számára.

```powershell
Configuration TestConfig
{
    param
    (
        [String]
        $ComputerName="localhost"
    )

    # It is best practice to explicitly import any required resources or modules.
    Import-DSCResource -Module PSDesiredStateConfiguration

    Node $ComputerName
    {
        Service 'Spooler'
        {
            Name = 'Spooler'
            State = 'Running'
        }
    }
}

TestConfig -ComputerName "server01", "server02", "server03"
```

## <a name="advanced-parameters-in-configurations"></a>Speciális paraméterek a konfigurációkban

A `-ComputerName` paraméter mellett paramétereket is hozzáadhat a szolgáltatás nevéhez és állapotához. Az alábbi példa egy paraméterrel rendelkező `-ServiceName` paramétert ad hozzá, és a használatával dinamikusan meghatározza a **szolgáltatás** -erőforrás blokkot. Egy `-State` paraméter hozzáadásával dinamikusan definiálja az **állapotot** a **szolgáltatás** -erőforrás blokkban.

```powershell
Configuration TestConfig
{
    param
    (
        [String]
        $ServiceName,

        [String]
        $State,

        [String]
        $ComputerName="localhost"
    )

    # It is best practice to explicitly import any required resources or modules.
    Import-DSCResource -Module PSDesiredStateConfiguration

    Node $ComputerName
    {
        Service $ServiceName
        {
            Name = $ServiceName
            State = $State
        }
    }
}
```

> [!NOTE]
> További advacned forgatókönyvekben érdemes lehet a dinamikus adatok strukturált [konfigurációs adatokba](configData.md)való áthelyezésére.

A példában a konfiguráció dinamikusan `$ServiceName`zajlik, de ha nincs megadva, a rendszer hibát eredményez. Ehhez a példához hasonló alapértelmezett értéket adhat hozzá.

```powershell
[String]
$ServiceName="Spooler"
```

Ebben a példányban azonban több értelme van, hogy egyszerűen kényszerítse a felhasználót a `$ServiceName` paraméter értékének megadására. Az `parameter` attribútum lehetővé teszi további érvényesítési és folyamat-támogatás hozzáadását a konfiguráció paramétereinek eléréséhez.

A paraméterek deklarációja felett adja hozzá `parameter` az attribútum blokkot az alábbi példában látható módon.

```powershell
[parameter()]
[String]
$ServiceName
```

Az egyes `parameter` attribútumokhoz argumentumokat adhat meg a definiált paraméter szempontjainak szabályozásához. A következő példa a `$ServiceName` **kötelező** paramétert teszi lehetővé.

```powershell
[parameter(Mandatory)]
[String]
$ServiceName
```

A paraméter esetében meg szeretnénk akadályozni, hogy a felhasználó az előre definiált készleten kívül (például a futó, leállított) értéket `ValidationSet*`adja meg. az attribútum megakadályozza, hogy a felhasználó egy előre definiált készleten kívüli értékeket határozzon meg (például a futtatást, `$State` Leállítva). A következő példa hozzáadja az `ValidationSet` attribútumot a `$State` paraméterhez. Mivel a `$State` paramétert nem szeretnénk **kötelezővé**tenni, hozzá kell adnia egy alapértelmezett értéket.

```powershell
[ValidateSet("Running", "Stopped")]
[String]
$State="Running"
```

> [!NOTE]
> Attribútum használatakor nem kell `parameter` attribútumot megadnia. `validation`

További információt a [about_Functions_Advanced_Parameters](/powershell/module/microsoft.powershell.core/about/about_Functions_Advanced_Parameters)és az `parameter` érvényesítési attribútumokról a következő cikkekben olvashat:.

## <a name="fully-parameterized-configuration"></a>Teljes mértékben paraméteres konfiguráció

Most már van egy paraméteres konfiguráció, amely arra kényszeríti a felhasználót `-InstanceName`, `-ServiceName`hogy határozzon meg egy, `-State` és érvényesíti a paramétert.

```powershell
Configuration TestConfig
{
    param
    (
        [parameter(Mandatory)]
        [String]
        $ServiceName,

        [ValidateSet("Running","Stopped")]
        [String]
        $State="Running",

        [String]
        $ComputerName="localhost",
    )

    # It is best practice to explicitly import any required resources or modules.
    Import-DSCResource -Module PSDesiredStateConfiguration

    Node localhost
    {
        Service $ServiceName
        {
            Name = $ServiceName
            State = $State
        }
    }
}
```

## <a name="see-also"></a>Lásd még:

- [A DSC-konfigurációk írási súgója](configHelp.md)
- [Dinamikus konfigurációk](flow-control-in-configurations.md)
- [Konfigurációs adatai használata a konfigurációkban](configData.md)
- [Különálló konfigurációs és környezeti adatértékek](separatingEnvData.md)
