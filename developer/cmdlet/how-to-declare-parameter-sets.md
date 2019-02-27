---
title: Hogyan paraméterkészlettel deklarálnia |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 46905eb9-64d7-4c55-9c2a-7bc7bf04e14b
caps.latest.revision: 10
ms.openlocfilehash: 6c2e5891a8e3f24969c12a2e57dc5ae8caa68e41
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56849398"
---
# <a name="how-to-declare-parameter-sets"></a><span data-ttu-id="dba8f-102">Paraméterkészletek deklarálása</span><span class="sxs-lookup"><span data-stu-id="dba8f-102">How to Declare Parameter Sets</span></span>

<span data-ttu-id="dba8f-103">Ez a példa bemutatja, hogyan meghatározhatja a két paraméterkészlettel, amikor Ön kijelenti, hogy a parancsmag paramétereit.</span><span class="sxs-lookup"><span data-stu-id="dba8f-103">This example shows how to define two parameter sets when you declare the parameters for a cmdlet.</span></span> <span data-ttu-id="dba8f-104">Minden egyes paraméterkészletet egy egyedi paramétereket és a egy megosztott paraméter mindkét paraméterkészlettel által használt rendelkezik.</span><span class="sxs-lookup"><span data-stu-id="dba8f-104">Each parameter set has both a unique parameter and a shared parameter that is used by both parameter sets.</span></span> <span data-ttu-id="dba8f-105">Paraméterek beállítása, beleértve az alapértelmezett paraméter megadását, további információ: [parancsmag paraméterkészletek](./cmdlet-parameter-sets.md).</span><span class="sxs-lookup"><span data-stu-id="dba8f-105">For more information about parameters sets, including how to specify the default parameter set, see [Cmdlet Parameter Sets](./cmdlet-parameter-sets.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dba8f-106">Amikor csak lehetséges, adja meg az egyedi paramétereket egy kötelező paraméter beállítása paraméter.</span><span class="sxs-lookup"><span data-stu-id="dba8f-106">Whenever possible, define the unique parameter of a parameter set as a required parameter.</span></span> <span data-ttu-id="dba8f-107">Azonban ha azt szeretné, hogy a paraméterek megadása nélkül futtatja a parancsmagot, az egyedi paraméter lehet egy nem kötelező paraméter.</span><span class="sxs-lookup"><span data-stu-id="dba8f-107">However, if you want your cmdlet to run without specifying any parameters, the unique parameter can be an optional parameter.</span></span> <span data-ttu-id="dba8f-108">Például az egyedi paramétereket a `Get-Command` parancsmag nem kötelező.</span><span class="sxs-lookup"><span data-stu-id="dba8f-108">For example, the unique parameter of the `Get-Command` cmdlet is optional.</span></span>

## <a name="how-to-define-two-parameter-sets"></a><span data-ttu-id="dba8f-109">Két paraméterkészlettel definiálása</span><span class="sxs-lookup"><span data-stu-id="dba8f-109">How to Define Two Parameter Sets</span></span>

1. <span data-ttu-id="dba8f-110">Adja hozzá a `ParameterSet` kulcsszó használatával az első paraméter készlet egyedi paraméter paraméter attribútumát.</span><span class="sxs-lookup"><span data-stu-id="dba8f-110">Add the `ParameterSet` keyword to the Parameter attribute for the unique parameter of the first parameter set.</span></span>

   ```csharp
   [Parameter(Position = 0, Mandatory = true,
              ParameterSetName = "Test01")]
   public string UserName
   {
     get { return userName; }
     set { userName = value; }
   }
   private string userName;
   ```

2. <span data-ttu-id="dba8f-111">Adja hozzá a `ParameterSet` kulcsszó paraméter attribútumát a második paraméter beállított egyedi paraméter használatával.</span><span class="sxs-lookup"><span data-stu-id="dba8f-111">Add the `ParameterSet` keyword to the Parameter attribute for the unique parameter of the second parameter set.</span></span>

   ```csharp
   [Parameter(Position = 0, Mandatory = true,
              ParameterSetName = "Test02")]
   public string ComputerName
   {
     get { return computerName; }
     set { computerName = value; }
   }
   private string computerName;
   ```

3. <span data-ttu-id="dba8f-112">A paraméter, amely mindkét paraméterkészlettel tartozik, az egyes paraméter egy paraméter attribútum hozzáadása, és vegye fel a `ParameterSet` az egyes kulcsszót.</span><span class="sxs-lookup"><span data-stu-id="dba8f-112">For the parameter that belongs to both parameter sets, add a Parameter attribute for each parameter set and then add the `ParameterSet` keyword to each set.</span></span> <span data-ttu-id="dba8f-113">Az összes paraméter attribútumot megadhatja, hogyan arra a paraméterre van definiálva.</span><span class="sxs-lookup"><span data-stu-id="dba8f-113">In each Parameter attribute, you can specify how that parameter is defined.</span></span> <span data-ttu-id="dba8f-114">A paraméter lehet egy nem kötelező, és a egy másik kötelező.</span><span class="sxs-lookup"><span data-stu-id="dba8f-114">A parameter can be optional in one set and mandatory in another.</span></span>

   ```csharp
   [Parameter(Mandatory= true, ParameterSetName = "Test01")]
   [Parameter(ParameterSetName = "Test02")]
   public string SharedParam
   {
       get { return sharedParam; }
       set { sharedParam = value; }
   }
   private string sharedParam;
   ```

## <a name="see-also"></a><span data-ttu-id="dba8f-115">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="dba8f-115">See Also</span></span>

[<span data-ttu-id="dba8f-116">Parancsmag</span><span class="sxs-lookup"><span data-stu-id="dba8f-116">Cmdlet Parameter Sets</span></span>](./cmdlet-parameter-sets.md)

[<span data-ttu-id="dba8f-117">Egy Windows PowerShell-parancsmag írása</span><span class="sxs-lookup"><span data-stu-id="dba8f-117">Writing a Windows PowerShell Cmdlet</span></span>](./writing-a-windows-powershell-cmdlet.md)
