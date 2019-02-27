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
ms.openlocfilehash: a9204ca7b28fc5792ef9bd18f6b0b24964de7386
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56849293"
---
# <a name="public-resource-schema"></a><span data-ttu-id="ad2fa-102">Nyilvános erőforrások sémája</span><span class="sxs-lookup"><span data-stu-id="ad2fa-102">Public Resource Schema</span></span>

<span data-ttu-id="ad2fa-103">Felügyeleti OData MOF segítségével meghatározhatja az erőforrásokat és azok tulajdonságait.</span><span class="sxs-lookup"><span data-stu-id="ad2fa-103">Management OData uses MOF to define resources and their properties.</span></span> <span data-ttu-id="ad2fa-104">Felügyeleti OData entitás tulajdonságait közvetlenül felelnek meg a felügyelt típus az alapul szolgáló parancsmag által visszaadott tulajdonságait.</span><span class="sxs-lookup"><span data-stu-id="ad2fa-104">The properties of a Management OData entity correspond directly to the properties of the managed type returned by the underlying cmdlet.</span></span>

## <a name="defining-a-resource"></a><span data-ttu-id="ad2fa-105">Egy erőforrás meghatározása</span><span class="sxs-lookup"><span data-stu-id="ad2fa-105">Defining a resource</span></span>

<span data-ttu-id="ad2fa-106">Az egyes erőforrások felel meg egy Windows PowerShell-parancsmag által visszaadott objektum.</span><span class="sxs-lookup"><span data-stu-id="ad2fa-106">Each resource corresponds to an object returned by a Windows PowerShell cmdlet.</span></span> <span data-ttu-id="ad2fa-107">A publc erőforrás MOF-fájlt adja meg egy erőforrást egy osztály deklarálásával.</span><span class="sxs-lookup"><span data-stu-id="ad2fa-107">In the publc resource MOF file, you define a resource by declaring a class.</span></span> <span data-ttu-id="ad2fa-108">Az osztály az objektum tulajdonságainak tulajdonságok áll.</span><span class="sxs-lookup"><span data-stu-id="ad2fa-108">The class consists of properties that correspond to the properties of the object.</span></span> <span data-ttu-id="ad2fa-109">Például az alábbi példában a [System.Diagnostics.Process](/dotnet/api/System.Diagnostics.Process) osztályt a következő MOF képviseli.</span><span class="sxs-lookup"><span data-stu-id="ad2fa-109">For example, in the following example, the [System.Diagnostics.Process](/dotnet/api/System.Diagnostics.Process) class is represented by the following MOF.</span></span>

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

<span data-ttu-id="ad2fa-110">Minden tulajdonságnévnek adattípust előzi meg.</span><span class="sxs-lookup"><span data-stu-id="ad2fa-110">Each property name is preceded by a data type.</span></span> <span data-ttu-id="ad2fa-111">Ebben a példában szereplő adattípusoknak felel meg a .NET-keretrendszert az CLR-beli adatok egyszerű típusok, de a Tulajdonságok lehet más erőforrások és a komplex típusok, mindkettő leírt később mutató hivatkozásokat is.</span><span class="sxs-lookup"><span data-stu-id="ad2fa-111">The data types in this example correspond to primitive CLR data types in the .NET Frameworks, but properties can also be references to other resources or complex types, which are both described later.</span></span>

<span data-ttu-id="ad2fa-112">A `Key` minősítő azt jelzi, hogy egy tulajdonságot egy erőforrás-példány egyedi azonosítására szolgál.</span><span class="sxs-lookup"><span data-stu-id="ad2fa-112">The `Key` qualifier indicates that a property is used to uniquely identify a resource instance.</span></span> <span data-ttu-id="ad2fa-113">Egy erőforrás egynél több kulcs is van.</span><span class="sxs-lookup"><span data-stu-id="ad2fa-113">A resource can have more than one key.</span></span>

<span data-ttu-id="ad2fa-114">A `Required` minősítő azt jelzi, hogy a tulajdonságot kötelező megadni.</span><span class="sxs-lookup"><span data-stu-id="ad2fa-114">The `Required` qualifier indicates that the property is required.</span></span> <span data-ttu-id="ad2fa-115">Ha egy tulajdonság célállapotba a `Key` minősítő, akkor minősül szükséges, és a `Required` minősítő már nem szükséges.</span><span class="sxs-lookup"><span data-stu-id="ad2fa-115">If a property is labeled with the `Key` qualifier, it is considered to be required, and the `Required` qualifier is not necessary.</span></span>

### <a name="complex-data-types"></a><span data-ttu-id="ad2fa-116">Összetett adattípusok</span><span class="sxs-lookup"><span data-stu-id="ad2fa-116">Complex data types</span></span>

<span data-ttu-id="ad2fa-117">Entitások tulajdonságainak összetett adattípusok is rendelkezhet.</span><span class="sxs-lookup"><span data-stu-id="ad2fa-117">Properties of entities can have complex data types.</span></span> <span data-ttu-id="ad2fa-118">Összetett adattípusok olyan, más típusú, C programozási nyelven struktúrák hasonló épülnek fel.</span><span class="sxs-lookup"><span data-stu-id="ad2fa-118">Complex data types are types that are made up of other types, similar to structs in the C programming language.</span></span> <span data-ttu-id="ad2fa-119">Egy összetett típus van deklarálva a MOF-fájlban található egy osztályt, a `ComplexType` minősítő, az alábbi példában látható módon.</span><span class="sxs-lookup"><span data-stu-id="ad2fa-119">A complex type is declared in the MOF file as a class with the `ComplexType` qualifier, as in the following example.</span></span>

```csharp
[ComplexType]
class PswsTest_ProcessModule
{
    String ModuleName;
    String FileName;
};
```

<span data-ttu-id="ad2fa-120">Egy összetett típus az entitástulajdonság deklarálnia, deklarálhatja, mint egy `string` típusú a `EmbeddedInstance` minősítő, beleértve a komplex típus nevét.</span><span class="sxs-lookup"><span data-stu-id="ad2fa-120">To declare an entity property as a complex type, you declare it as a `string` type with the `EmbeddedInstance` qualifier, including the name of the complex type.</span></span> <span data-ttu-id="ad2fa-121">A következő példa hshows tulajdonság a nyilatkozat, a `PswsTest_ProcessModule` típus deklarálva az előző példában.</span><span class="sxs-lookup"><span data-stu-id="ad2fa-121">The following example hshows the declaration of a property of the `PswsTest_ProcessModule` type declared in the previous example.</span></span>

```csharp
[Required, EmbeddedInstance("PswsTest_ProcessModule")] String Modules[];
```

### <a name="associating-entities"></a><span data-ttu-id="ad2fa-122">Entitások társítása</span><span class="sxs-lookup"><span data-stu-id="ad2fa-122">Associating entities</span></span>

<span data-ttu-id="ad2fa-123">A társítás és AssocationClass minősítők használatával társíthatja a két entitás.</span><span class="sxs-lookup"><span data-stu-id="ad2fa-123">You can associate two entities by using the Association and AssocationClass qualifiers.</span></span> <span data-ttu-id="ad2fa-124">További információkért lásd: [társítása Management OData entitások](./associating-management-odata-entities.md).</span><span class="sxs-lookup"><span data-stu-id="ad2fa-124">For more information, see [Associating Management OData Entities](./associating-management-odata-entities.md).</span></span>

### <a name="derived-types"></a><span data-ttu-id="ad2fa-125">Származtatott típusokkal</span><span class="sxs-lookup"><span data-stu-id="ad2fa-125">Derived types</span></span>

<span data-ttu-id="ad2fa-126">Egy másik a típus származtathatók.</span><span class="sxs-lookup"><span data-stu-id="ad2fa-126">You can derive a type from another type.</span></span> <span data-ttu-id="ad2fa-127">A származtatott típusban örökli az összes, amelyről osztályból származtatott explicit módon tulajdonságokat mellett a típus tulajdonságait.</span><span class="sxs-lookup"><span data-stu-id="ad2fa-127">The derived type inherits all of the properties of the type from which it derives in addition to any properties explicitly derived.</span></span> <span data-ttu-id="ad2fa-128">Az alábbi példa bemutatja a típusa határozza meg, majd határozza meg, hogy típusból származtatott két típusa.</span><span class="sxs-lookup"><span data-stu-id="ad2fa-128">The following example shows a type declaration and then a declaration of two types derived from that type.</span></span>

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