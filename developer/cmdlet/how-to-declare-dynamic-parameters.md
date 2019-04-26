---
title: Deklarálja a dinamikus paraméterek hogyan |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: db04f1df-def5-4456-8869-336024cda723
caps.latest.revision: 8
ms.openlocfilehash: a9c530cdc66302eb6b3d9d2b284eeb486c3b2ba9
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62067922"
---
# <a name="how-to-declare-dynamic-parameters"></a><span data-ttu-id="43e81-102">Dinamikus paraméterek deklarálása</span><span class="sxs-lookup"><span data-stu-id="43e81-102">How to Declare Dynamic Parameters</span></span>

<span data-ttu-id="43e81-103">Ez a példa bemutatja, hogyan futásidőben a parancsmag adott dinamikus paraméterek meghatározására.</span><span class="sxs-lookup"><span data-stu-id="43e81-103">This example shows how to define dynamic parameters that are added to the cmdlet at runtime.</span></span> <span data-ttu-id="43e81-104">Ebben a példában a `Department` paramétert a parancsmaghoz egészül ki, amikor a felhasználó adja meg a `Employee` paraméter váltani.</span><span class="sxs-lookup"><span data-stu-id="43e81-104">In this example, the `Department` parameter is added to the cmdlet whenever the user specifies the `Employee` switch parameter.</span></span> <span data-ttu-id="43e81-105">Dinamikus paraméterekkel kapcsolatos további információkért lásd: [dinamikus parancsmag-paraméterek](./cmdlet-dynamic-parameters.md).</span><span class="sxs-lookup"><span data-stu-id="43e81-105">For more information about dynamic parameters, see [Cmdlet Dynamic Parameters](./cmdlet-dynamic-parameters.md).</span></span>

## <a name="to-define-dynamic-parameters"></a><span data-ttu-id="43e81-106">Dinamikus paraméterek megadásához</span><span class="sxs-lookup"><span data-stu-id="43e81-106">To define dynamic parameters</span></span>

1. <span data-ttu-id="43e81-107">A parancsmag osztálydeklaráció adja hozzá a [System.Management.Automation.Idynamicparameters](/dotnet/api/System.Management.Automation.IDynamicParameters) csatoló látható módon.</span><span class="sxs-lookup"><span data-stu-id="43e81-107">In the cmdlet class declaration, add the [System.Management.Automation.Idynamicparameters](/dotnet/api/System.Management.Automation.IDynamicParameters) interface as shown.</span></span>

   ```csharp
   public class SendGreetingCommand : Cmdlet, IDynamicParameters
   ```

2. <span data-ttu-id="43e81-108">Hívja a [System.Management.Automation.Idynamicparameters.Getdynamicparameters\*](/dotnet/api/System.Management.Automation.IDynamicParameters.GetDynamicParameters) metódussal, amely visszaadja az objektum, amely a dinamikus paraméterek vannak meghatározva.</span><span class="sxs-lookup"><span data-stu-id="43e81-108">Call the [System.Management.Automation.Idynamicparameters.Getdynamicparameters\*](/dotnet/api/System.Management.Automation.IDynamicParameters.GetDynamicParameters) method, which returns the object in which the dynamic parameters are defined.</span></span> <span data-ttu-id="43e81-109">Ebben a példában a metódus nevezzük, amikor a `Employee` paraméter meg van adva.</span><span class="sxs-lookup"><span data-stu-id="43e81-109">In this example, the method is called when the `Employee` parameter is specified.</span></span>

   ```csharp
   public object GetDynamicParameters()
   {
       if (employee)
       {
         context= new SendGreetingCommandDynamicParameters();
         return context;
       }
       return null;
   }
   private SendGreetingCommandDynamicParameters context;
   ```

3. <span data-ttu-id="43e81-110">Egy osztály, amely meghatározza a dinamikus paraméterek hozzá kell deklarálni.</span><span class="sxs-lookup"><span data-stu-id="43e81-110">Declare a class that defines the dynamic parameters to be added.</span></span> <span data-ttu-id="43e81-111">Használhatja az attribútumokat, amelyek a statikus parancsmag-paraméterek, a dinamikus paraméterek deklarálnia deklarálásához használt.</span><span class="sxs-lookup"><span data-stu-id="43e81-111">You can use the attributes that you used to declare the static cmdlet parameters to declare the dynamic parameters.</span></span>

   ```csharp
   public class SendGreetingCommandDynamicParameters
   {
     [Parameter]
     [ValidateSet ("Marketing", "Sales", "Development")]
     public string Department
     {
       get { return department; }
       set { department = value; }
     }
     private string department;
   }
   ```

## <a name="example"></a><span data-ttu-id="43e81-112">Példa</span><span class="sxs-lookup"><span data-stu-id="43e81-112">Example</span></span>

<span data-ttu-id="43e81-113">Ebben a példában a `Department` paraméter kerül, amikor a felhasználó adja meg a `Employee` paraméter.</span><span class="sxs-lookup"><span data-stu-id="43e81-113">In this example, the `Department` parameter is added whenever the user specifies the `Employee` parameter.</span></span> <span data-ttu-id="43e81-114">A `Department` paraméter nem kötelező paraméter, és a ValidateSet attribútum az engedélyezett argumentumok meghatározására szolgál.</span><span class="sxs-lookup"><span data-stu-id="43e81-114">The `Department` parameter is an optional parameter, and the ValidateSet attribute is used to specify the allowed arguments.</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Management.Automation;     // PowerShell assembly.

namespace SendGreeting
{
  // Declare the cmdlet class that supports the
  // IDynamicParameters interface.
  [Cmdlet(VerbsCommunications.Send, "Greeting")]
  public class SendGreetingCommand : Cmdlet, IDynamicParameters
  {
    // Declare the parameters for the cmdlet.
    [Parameter(Mandatory = true)]
    public string Name
    {
      get { return name; }
      set { name = value; }
    }
    private string name;

    [Parameter]
    [Alias ("FTE")]
    public SwitchParameter Employee
    {
      get { return employee; }
      set { employee = value; }
    }
    private Boolean employee;

    // Implement GetDynamicParameters to
    // retrieve the dynamic parameter.
    public object GetDynamicParameters()
    {
      if (employee)
      {
        context= new SendGreetingCommandDynamicParameters();
        return context;
      }
      return null;
   }
   private SendGreetingCommandDynamicParameters context;

    // Overide the ProcessRecord method to process the
    // supplied user name and write out a greeting to
    // the user by calling the WriteObject method.
    protected override void ProcessRecord()
    {
      WriteObject("Hello " + name + "! ");
      if (employee)
      {
        WriteObject("Department: " + context.Department);
      }
    }
  }

  // Define the dynamic parameters to be added
  public class SendGreetingCommandDynamicParameters
  {
    [Parameter]
    [ValidateSet ("Marketing", "Sales", "Development")]
    public string Department
    {
      get { return department; }
      set { department = value; }
    }
    private string department;
  }
}
```

## <a name="see-also"></a><span data-ttu-id="43e81-115">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="43e81-115">See Also</span></span>

[<span data-ttu-id="43e81-116">System.Management.Automation.Runtimedefinedparameterdictionary</span><span class="sxs-lookup"><span data-stu-id="43e81-116">System.Management.Automation.Runtimedefinedparameterdictionary</span></span>](/dotnet/api/System.Management.Automation.RuntimeDefinedParameterDictionary)

[<span data-ttu-id="43e81-117">System.Management.Automation.Idynamicparameters.Getdynamicparameters\*</span><span class="sxs-lookup"><span data-stu-id="43e81-117">System.Management.Automation.Idynamicparameters.Getdynamicparameters\*</span></span>](/dotnet/api/System.Management.Automation.IDynamicParameters.GetDynamicParameters)

[<span data-ttu-id="43e81-118">A parancsmag dinamikus paraméterek</span><span class="sxs-lookup"><span data-stu-id="43e81-118">Cmdlet Dynamic Parameters</span></span>](./cmdlet-dynamic-parameters.md)

[<span data-ttu-id="43e81-119">Windows PowerShell SDK</span><span class="sxs-lookup"><span data-stu-id="43e81-119">Windows PowerShell SDK</span></span>](../windows-powershell-reference.md)