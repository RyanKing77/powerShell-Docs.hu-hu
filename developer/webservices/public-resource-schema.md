---
title: Nyilvános séma |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: e67298ee-a773-4402-8afb-d97ad0e030e5
caps.latest.revision: 4
ms.openlocfilehash: c7e20ff0f36e8cab2d414ff2e5924b3359ad9c60
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62080577"
---
# <a name="public-resource-schema"></a>Nyilvános erőforrások sémája

Felügyeleti OData MOF segítségével meghatározhatja az erőforrásokat és azok tulajdonságait. Felügyeleti OData entitás tulajdonságait közvetlenül felelnek meg a felügyelt típus az alapul szolgáló parancsmag által visszaadott tulajdonságait.

## <a name="defining-a-resource"></a>Egy erőforrás meghatározása

Az egyes erőforrások felel meg egy Windows PowerShell-parancsmag által visszaadott objektum. A nyilvános erőforrás MOF-fájlt adja meg egy erőforrást egy osztály deklarálásával. Az osztály az objektum tulajdonságainak tulajdonságok áll. Például az alábbi példában a [System.Diagnostics.Process](/dotnet/api/System.Diagnostics.Process) osztályt a következő MOF képviseli.

```csharp
class PswsTest_Process
{
    [Key] SInt32 Id;
    [Required] SInt32 BasePriority;
    [Required] SInt32 HandleCount;
    [Required] string MachineName;
    [Required] SInt32 MainWindowHandle;

    ...
};
```

Minden tulajdonságnévnek adattípust előzi meg. Ebben a példában szereplő adattípusoknak felel meg a .NET-keretrendszert az CLR-beli adatok egyszerű típusok, de a Tulajdonságok lehet más erőforrások és a komplex típusok, mindkettő leírt később mutató hivatkozásokat is.

A `Key` minősítő azt jelzi, hogy egy tulajdonságot egy erőforrás-példány egyedi azonosítására szolgál. Egy erőforrás egynél több kulcs is van.

A `Required` minősítő azt jelzi, hogy a tulajdonságot kötelező megadni. Ha egy tulajdonság célállapotba a `Key` minősítő, akkor minősül szükséges, és a `Required` minősítő már nem szükséges.

### <a name="complex-data-types"></a>Összetett adattípusok

Entitások tulajdonságainak összetett adattípusok is rendelkezhet. Összetett adattípusok olyan, más típusú, C programozási nyelven struktúrák hasonló épülnek fel. Egy összetett típus van deklarálva a MOF-fájlban található egy osztályt, a `ComplexType` minősítő, az alábbi példában látható módon.

```csharp
[ComplexType]
class PswsTest_ProcessModule
{
    String ModuleName;
    String FileName;
};
```

Egy összetett típus az entitástulajdonság deklarálnia, deklarálhatja, mint egy `string` típusú a `EmbeddedInstance` minősítő, beleértve a komplex típus nevét. Az alábbi példa bemutatja egy tulajdonságának a nyilatkozat az `PswsTest_ProcessModule` típus deklarálva az előző példában.

```csharp
[Required, EmbeddedInstance("PswsTest_ProcessModule")] String Modules[];
```

### <a name="associating-entities"></a>Entitások társítása

A társítás és AssociationClass minősítők használatával társíthatja a két entitás. További információkért lásd: [társítása Management OData entitások](./associating-management-odata-entities.md).

### <a name="derived-types"></a>Származtatott típusokkal

Egy másik a típus származtathatók. A származtatott típusban örökli az összes, amelyről osztályból származtatott explicit módon tulajdonságokat mellett a típus tulajdonságait. Az alábbi példa bemutatja a típusa határozza meg, majd határozza meg, hogy típusból származtatott két típusa.

```csharp
Class Product {

    [Key] String ProductName;

};

Class DairyProduct : Product {

    Uint16 PercentFat;
};
Class POPProduct : Product {

    Boolean IsCarbonated;
};
```