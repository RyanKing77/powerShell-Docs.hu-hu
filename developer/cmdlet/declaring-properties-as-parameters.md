---
title: Tulajdonságok paraméterekként deklaráló |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f71ea35d-cff5-4e44-a5c6-3a747ed4c4d9
caps.latest.revision: 9
ms.openlocfilehash: 6f6640afb15b3608669538f9b5f53d7a8a5c380d
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62068266"
---
# <a name="declaring-properties-as-parameters"></a><span data-ttu-id="a83c8-102">Tulajdonságok deklarálása paraméterekként</span><span class="sxs-lookup"><span data-stu-id="a83c8-102">Declaring Properties as Parameters</span></span>

<span data-ttu-id="a83c8-103">Ez a témakör alapvető információkat látnia kell, mielőtt azt deklarálja, hogy a parancsmag paramétereit.</span><span class="sxs-lookup"><span data-stu-id="a83c8-103">This topic provides basic information you must understand before you declare the parameters of a cmdlet.</span></span>

<span data-ttu-id="a83c8-104">Deklarálja a parancsmag osztályon belül a parancsmag paramétereit, a nyilvános tulajdonságok, amelyek az egyes paraméterek megadása, és hozzáadhatja egy vagy több paraméter-attribútumok minden egyes tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="a83c8-104">To declare the parameters of a cmdlet within your cmdlet class, define the public properties that represent each parameter, and then add one or more Parameter attributes to each property.</span></span> <span data-ttu-id="a83c8-105">A Windows PowerShell-modul a parancsmag-paraméterként tulajdonság azonosítására használ a paraméter-attribútumok.</span><span class="sxs-lookup"><span data-stu-id="a83c8-105">The Windows PowerShell runtime uses the Parameter attributes to identify the property as a cmdlet parameter.</span></span> <span data-ttu-id="a83c8-106">Alapszintű a paraméter-attribútumhoz deklaráló szintaxisa a következő `[Parameter()]`.</span><span class="sxs-lookup"><span data-stu-id="a83c8-106">The basic syntax for declaring the Parameter attribute is `[Parameter()]`.</span></span>

<span data-ttu-id="a83c8-107">Íme egy példa egy kötelező paraméterként meghatározott tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="a83c8-107">Here is an example of a property defined as a required parameter.</span></span>

```csharp
[Parameter(Position = 0, Mandatory = true)]
public string UserName
{
  get { return userName; }
  set { userName = value; }
}
private string userName;
```

<span data-ttu-id="a83c8-108">Néhány dolog paraméterekkel kapcsolatos tudnivalók.</span><span class="sxs-lookup"><span data-stu-id="a83c8-108">Here are some things to remember about parameters.</span></span>

- <span data-ttu-id="a83c8-109">Egy paraméter fel kell tüntetni explicit módon is nyilvános.</span><span class="sxs-lookup"><span data-stu-id="a83c8-109">A parameter must be explicitly marked as public.</span></span> <span data-ttu-id="a83c8-110">Nem nyilvános, belső alapértelmezett vannak megjelölve, és nem található a Windows PowerShell-modul által paraméterek.</span><span class="sxs-lookup"><span data-stu-id="a83c8-110">Parameters that are not marked as public default to internal and will not be found by the Windows PowerShell runtime.</span></span>

- <span data-ttu-id="a83c8-111">Paraméterek jobb paraméter ellenőrzése biztosít a Microsoft .NET-keretrendszer típusú lehet definiálni.</span><span class="sxs-lookup"><span data-stu-id="a83c8-111">Parameters should be defined as Microsoft .NET Framework types to provide better parameter validation.</span></span> <span data-ttu-id="a83c8-112">Például csak egy érték a tartományon kívül egy értékhalmazt paramétereket enumerálási típusát, meg kell határozni.</span><span class="sxs-lookup"><span data-stu-id="a83c8-112">For example, parameters that are restricted to one value out of a set of values should be defined as an enumeration type.</span></span> <span data-ttu-id="a83c8-113">Paraméterek, amelyek egy egységes erőforrás-azonosító (URI) érték típusúnak kell lennie [System.Uri](/dotnet/api/System.Uri).</span><span class="sxs-lookup"><span data-stu-id="a83c8-113">Parameters that take a Uniform Resource Identifier (URI) value should be of type [System.Uri](/dotnet/api/System.Uri).</span></span>

- <span data-ttu-id="a83c8-114">Kerülje el az összes, de szabad formátumú szöveges tulajdonságainak alapszintű karakterlánc paraméterei.</span><span class="sxs-lookup"><span data-stu-id="a83c8-114">Avoid basic string parameters for all but free-form text properties.</span></span>

- <span data-ttu-id="a83c8-115">Egy paraméter paraméterkészlettel tetszőleges számú is hozzáadhat.</span><span class="sxs-lookup"><span data-stu-id="a83c8-115">You can add a parameter to any number of parameter sets.</span></span> <span data-ttu-id="a83c8-116">Paraméterkészlettel kapcsolatos további információkért lásd: [parancsmag paraméterkészletek](./cmdlet-parameter-sets.md).</span><span class="sxs-lookup"><span data-stu-id="a83c8-116">For more information about parameter sets, see [Cmdlet Parameter Sets](./cmdlet-parameter-sets.md).</span></span>

<span data-ttu-id="a83c8-117">Windows PowerShell parancsmagok automatikusan elérhető általános paraméterek készletét is biztosít.</span><span class="sxs-lookup"><span data-stu-id="a83c8-117">Windows PowerShell also provides a set of common parameters that are automatically available to every cmdlet.</span></span> <span data-ttu-id="a83c8-118">Ezeket a paramétereket, és az aliasokat kapcsolatos további információkért lásd: [parancsmag-paraméterek általános](./common-parameter-names.md).</span><span class="sxs-lookup"><span data-stu-id="a83c8-118">For more information about these parameters and their aliases, see [Cmdlet Common Parameters](./common-parameter-names.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="a83c8-119">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="a83c8-119">See Also</span></span>

[<span data-ttu-id="a83c8-120">A parancsmag közös paraméterek</span><span class="sxs-lookup"><span data-stu-id="a83c8-120">Cmdlet Common Parameters</span></span>](./common-parameter-names.md)

[<span data-ttu-id="a83c8-121">A parancsmag a paraméter típusa</span><span class="sxs-lookup"><span data-stu-id="a83c8-121">Types of Cmdlet Parameter</span></span>](./types-of-cmdlet-parameters.md)

[<span data-ttu-id="a83c8-122">Egy Windows PowerShell-parancsmag írása</span><span class="sxs-lookup"><span data-stu-id="a83c8-122">Writing a Windows PowerShell Cmdlet</span></span>](./writing-a-windows-powershell-cmdlet.md)
