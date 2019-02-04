---
ms.date: 12/12/2018
keywords: DSC, powershell, erőforrás, katalógus, beállítása
title: Paraméterek hozzáadása konfigurációkhoz
ms.openlocfilehash: 15213404f0cdd6416baf1f83af91b8f5279cc97f
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55685402"
---
# <a name="add-parameters-to-a-configuration"></a>Paraméterek hozzáadása konfigurációkhoz

Funkciók, például [konfigurációk](configurations.md) , hogy a felhasználói bemenet alapján több dinamikus konfigurációk rendelkeznek. A lépések hasonlóak leírt [függvényeket paraméterekkel](/powershell/module/microsoft.powershell.core/about/about_functions).

Ebben a példában a "Nyomtatásisor-kezelő" szolgáltatás "Fut" konfigurál alapkonfiguráció kezdődik.

```powershell
Configuration TestConfig
{
    # It is best practice to implicitly import any required resources or modules.
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

## <a name="built-in-configuration-parameters"></a>Beépített konfigurációs paraméterei

Egy függvény eltérően azonban a [CmdletBinding](/powershell/module/microsoft.powershell.core/about/about_functions_cmdletbindingattribute) attribútum nincs funkciókkal bővíti a. Mellett [általános paraméterek](/powershell/module/microsoft.powershell.core/about/about_commonparameters), konfigurációk is használhatja az alábbi paraméterek, beépített anélkül, hogy definiálja azokat.

|Paraméter  |Leírás  |
|---------|---------|
|`-InstanceName`|Határozza meg [összetett konfigurációk](compositeconfigs.md)|
|`-DependsOn`|Határozza meg [összetett konfigurációk](compositeconfigs.md)|
|`-PSDSCRunAsCredential`|Határozza meg [összetett konfigurációk](compositeconfigs.md)|
|`-ConfigurationData`|Amelyen a strukturált [konfigurációs adatok](configData.md) a konfigurációban való használat.|
|`-OutputPath`|Hol adható meg a "\<computername\>.mof" fájl le lesz fordítva|

## <a name="adding-your-own-parameters-to-configurations"></a>Konfigurációk a saját paraméterek hozzáadása

A beépített paraméterek mellett is adhat a saját paraméterek a konfigurációk. A paraméterblokkban közvetlenül a konfigurációs nyilatkozat, csakúgy, mint egy függvény belülre irányul. Egy konfigurációs paraméter blokk kívül bármely kell **csomópont** nyilatkozatok, és minden újabb *importálása* utasításokat. Paraméterek hozzáadásával a konfigurációk megbízhatóbb és dinamikus teheti meg.

```powershell
Configuration TestConfig
{
    param
    (

    )
```

### <a name="add-a-computername-parameter"></a>ComputerName paraméter hozzáadása

Az első paraméter lehetséges, hogy egy `-Computername` paramétert, így bármely dinamikusan állíthat össze egy ".mof" fájl `-Computername` adja át a konfigurációt. Funkciók, például megadhat egy alapértelmezett értéket, abban az esetben, ha a felhasználó nem felel meg egy értéket `-ComputerName`

```powershell
param
(
    [String]
    $ComputerName="localhost"
)
```

Belül a konfigurációját, majd megadhatja a `-ComputerName` paraméter a csomópont blokk meghatározásakor.

```powershell
Node $ComputerName
{

}
```

### <a name="calling-your-configuration-with-parameters"></a>A konfiguráció paraméterekkel hívása

Miután hozzáadta a paraméterek a konfigurációt, ugyanúgy, mint egy parancsmaggal használhatja őket.

```powershell
TestConfig -ComputerName "server01"
```

### <a name="compiling-multiple-mof-files"></a>Több .mof fájl fordítása

A csomópont blokk is fogadhat számítógépnevek vesszővel tagolt listája, és minden ".mof" fájlokat hoz létre. Az összes számítógép átadott ".mof" fájlok létrehozásához az alábbi példa futtatása a `-ComputerName` paraméter.

```powershell
Configuration TestConfig
{
    param
    (
        [String]
        $ComputerName="localhost"
    )

    # It is best practice to implicitly import any required resources or modules.
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

## <a name="advanced-parameters-in-configurations"></a>Speciális paraméterek konfigurációk

Mellett egy `-ComputerName` paramétert, hozzáadhatja a szolgáltatás nevét és állapotát paramétereit. Az alábbi példa hozzáad egy paraméter blokkot, egy `-ServiceName` paramétert, és használja, ezzel dinamikusan definiálva a **szolgáltatás** erőforrás letiltása. Hozzáadja a `-State` paraméter, ezzel dinamikusan definiálva a **állapot** a a **szolgáltatás** erőforrás letiltása.

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

    # It is best practice to implicitly import any required resources or modules.
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
> Más advacned forgatókönyvekben, akkor előfordulhat, hogy célszerűbb, a dinamikus adatokat áthelyezni egy strukturált [konfigurációs adatok](configData.md).

A példában most konfigurációs vesz igénybe egy dinamikus `$ServiceName`, de nincs megadva, ha fordítása hibát eredményez. Hozzáadhat például ebben a példában egy alapértelmezett értéket.

```powershell
[String]
$ServiceName="Spooler"
```

Ebben a példányban, logikus további egyszerűen kényszerítik a felhasználót adjon meg egy értéket a `$ServiceName` paraméter. A `parameter` attribútum lehetővé teszi, hogy további ellenőrzési és a folyamat a konfigurációs paramétereket támogatja.

Bármely paraméterdeklarációhoz felett adja hozzá a `parameter` attribútum letiltása az alábbi példában látható módon.

```powershell
[parameter()]
[String]
$ServiceName
```

A megadott argumentumok minden egyes `parameter` attribútum vezérlő aspektusainak paraméter van megadva. A következő példa a `$ServiceName` egy **kötelező** paraméter.

```powershell
[parameter(Mandatory)]
[String]
$ServiceName
```

Az a `$State` paramétert, szeretnénk, hogy a felhasználó kívül előre meghatározott értékeket (például a futó, a Leállítva) a `ValidationSet*`attribútum megakadályozná, hogy a felhasználó kívül (például a futó, előre meghatározott értékeket adjanak meg Leállítva). Az alábbi példa hozzáadja a `ValidationSet` attribútumot a `$State` paraméter. Mert szeretnénk, hogy nem a `$State` paraméter **kötelező**, hogy hozzá kell adnia egy alapértelmezett értéket.

```powershell
[ValidateSet("Running", "Stopped")]
[String]
$State="Running"
```

> [!NOTE]
> Nem kell megadnia egy `parameter` attribútum használata esetén egy `validation` attribútum.

További információ a `parameter` és az érvényesítési attribútumokat [about_Functions_Advanced_Parameters](/powershell/module/microsoft.powershell.core/about/about_Functions_Advanced_Parameters.md).

## <a name="fully-parameterized-configuration"></a>Teljes körűen paraméteres Configuration

Ezzel kapunk egy paraméteres Configuration, amely a felhasználó adja meg egy `-InstanceName`, `-ServiceName`, és érvényesíti a `-State` paraméter.

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

    # It is best practice to implicitly import any required resources or modules.
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

- [DSC-konfigurációk súgót írni](configHelp.md)
- [A dinamikus konfigurációk](flow-control-in-configurations.md)
- [Konfigurációs adatok használata a konfigurációk](configData.md)
- [Külön konfigurációs és környezeti adatok](separatingEnvData.md)
