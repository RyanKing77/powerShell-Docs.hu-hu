---
title: A parancsmag dinamikus paraméterek |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 8ae2196d-d6c8-4101-8805-4190d293af51
caps.latest.revision: 13
ms.openlocfilehash: 2fc73b6ef5a862fafb7a3c8fe3da19ac71bafc05
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62068538"
---
# <a name="cmdlet-dynamic-parameters"></a><span data-ttu-id="978a4-102">Parancsmagok dinamikus paraméterei</span><span class="sxs-lookup"><span data-stu-id="978a4-102">Cmdlet Dynamic Parameters</span></span>

<span data-ttu-id="978a4-103">Parancsmagok speciális körülmények, például ha egy másik paraméter argumentuma egy adott érték a felhasználó számára elérhető paramétereket adhatja meg.</span><span class="sxs-lookup"><span data-stu-id="978a4-103">Cmdlets can define parameters that are available to the user under special conditions, such as when the argument of another parameter is a specific value.</span></span> <span data-ttu-id="978a4-104">Ezek a paraméterek futásidőben kerülnek, és nevezzük *dinamikus paraméterek* mert csak szükség esetén kerül.</span><span class="sxs-lookup"><span data-stu-id="978a4-104">These parameters are added at runtime and are referred to as *dynamic parameters* because they are added only when they are needed.</span></span> <span data-ttu-id="978a4-105">Például, amely hozzáad számos paraméter csak akkor, ha egy adott kapcsoló paraméter meg van adva a parancsmag is tervezhet.</span><span class="sxs-lookup"><span data-stu-id="978a4-105">For example, you can design a cmdlet that adds several parameters only when a specific switch parameter is specified.</span></span>

> [!NOTE]
> <span data-ttu-id="978a4-106">A szolgáltatók és a Windows PowerShell-funkciók is megadhatók a dinamikus paraméterek.</span><span class="sxs-lookup"><span data-stu-id="978a4-106">Providers and Windows PowerShell functions can also define dynamic parameters.</span></span>

## <a name="dynamic-parameters-in-windows-powershell-cmdlets"></a><span data-ttu-id="978a4-107">Dinamikus paraméterek a Windows PowerShell-parancsmagok</span><span class="sxs-lookup"><span data-stu-id="978a4-107">Dynamic Parameters in Windows PowerShell Cmdlets</span></span>

<span data-ttu-id="978a4-108">Windows PowerShell számos, a szolgáltató parancsmagjai a dinamikus paramétereket használja.</span><span class="sxs-lookup"><span data-stu-id="978a4-108">Windows PowerShell uses dynamic parameters in several of its provider cmdlets.</span></span> <span data-ttu-id="978a4-109">Például a `Get-Item` és `Get-ChildItem` parancsmagok hozzáadása egy `CodeSigningCert` futásidőben paraméter során a `Path` a parancsmag tanúsítvány szolgáltató elérési útját adja meg.</span><span class="sxs-lookup"><span data-stu-id="978a4-109">For example, the `Get-Item` and `Get-ChildItem` cmdlets add a `CodeSigningCert` parameter at runtime when the `Path` parameter of the cmdlet specifies the Certificate provider path.</span></span> <span data-ttu-id="978a4-110">Ha a `Path` a parancsmag elérési útja a másik szolgáltatóhoz, a `CodeSigningCert` paraméter nem érhető el.</span><span class="sxs-lookup"><span data-stu-id="978a4-110">If the `Path` parameter of the cmdlet specifies a path for a different provider, the `CodeSigningCert` parameter is not available.</span></span>

<span data-ttu-id="978a4-111">Az alábbi példák mutatják a `CodeSigningCert` paraméter futásidőben kerül során a `Get-Item` parancsmagot futtatja.</span><span class="sxs-lookup"><span data-stu-id="978a4-111">The following examples show how the `CodeSigningCert` parameter is added at runtime when the `Get-Item` cmdlet is run.</span></span>

<span data-ttu-id="978a4-112">Az első példában a Windows PowerShell-modul hozzá van adva a paramétert, és a parancsmag sikeres.</span><span class="sxs-lookup"><span data-stu-id="978a4-112">In the first example, the Windows PowerShell runtime has added the parameter, and the cmdlet is successful.</span></span>

```powershell
Get-Item -Path cert:\CurrentUser -codesigningcert
```

```output
Location   : CurrentUser
StoreNames : {SmartCardRoot, UserDS, AuthRoot, CA...}
```

<span data-ttu-id="978a4-113">A második példában egy fájlrendszer meghajtón van megadva, és hibát ad vissza.</span><span class="sxs-lookup"><span data-stu-id="978a4-113">In the second example, a FileSystem drive is specified, and an error is returned.</span></span> <span data-ttu-id="978a4-114">A hibaüzenet azt jelzi, hogy a `CodeSigningCert` paraméter nem található.</span><span class="sxs-lookup"><span data-stu-id="978a4-114">The error message indicates that the `CodeSigningCert` parameter cannot be found.</span></span>

```powershell
Get-Item -Path C:\ -codesigningcert
```

```output
Get-Item : A parameter cannot be found that matches parameter name 'codesigningcert'.
At line:1 char:37
+  get-item -path C:\ -codesigningcert <<<<
--------
    CategoryInfo          : InvalidArgument: (:) [Get-Item], ParameterBindingException
    FullyQualifiedErrorId : NamedParameterNotFound,Microsoft.PowerShell.Commands.GetItemCommand
```

## <a name="support-for-dynamic-parameters"></a><span data-ttu-id="978a4-115">Dinamikus paraméterek támogatása</span><span class="sxs-lookup"><span data-stu-id="978a4-115">Support for Dynamic Parameters</span></span>

<span data-ttu-id="978a4-116">Támogatja a dinamikus paraméterek, a parancsmag kódot a következő elemeket kell tartalmaznia.</span><span class="sxs-lookup"><span data-stu-id="978a4-116">To support dynamic parameters, the cmdlet code must include the following elements.</span></span>

<span data-ttu-id="978a4-117">[System.Management.Automation.Idynamicparameters](/dotnet/api/System.Management.Automation.IDynamicParameters) Ez az interfész biztosít a módszert, amelyet a dinamikus paraméterek kérdezi le.</span><span class="sxs-lookup"><span data-stu-id="978a4-117">[System.Management.Automation.Idynamicparameters](/dotnet/api/System.Management.Automation.IDynamicParameters) This interface provides the method that retrieves the dynamic parameters.</span></span>

<span data-ttu-id="978a4-118">Példa:</span><span class="sxs-lookup"><span data-stu-id="978a4-118">Example:</span></span>

`public class SendGreetingCommand : Cmdlet, IDynamicParameters`

<span data-ttu-id="978a4-119">[System.Management.Automation.Idynamicparameters.Getdynamicparameters\*](/dotnet/api/System.Management.Automation.IDynamicParameters.GetDynamicParameters) a metódus lekér az objektum, amely a dinamikus paraméterek kapcsolatos definíciókat tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="978a4-119">[System.Management.Automation.Idynamicparameters.Getdynamicparameters\*](/dotnet/api/System.Management.Automation.IDynamicParameters.GetDynamicParameters) This method retrieves the object that contains the dynamic parameter definitions.</span></span>

<span data-ttu-id="978a4-120">Példa:</span><span class="sxs-lookup"><span data-stu-id="978a4-120">Example:</span></span>

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

<span data-ttu-id="978a4-121">Dinamikus paraméter osztály Ez az osztály a paraméterek hozzáadandó határozza meg.</span><span class="sxs-lookup"><span data-stu-id="978a4-121">Dynamic Parameter class This class defines the parameters to be added.</span></span> <span data-ttu-id="978a4-122">Ez az osztály egyes paramétereket és a nem kötelező Alias és az érvényesítési attribútumokat, amelyek szükségesek a parancsmag egy paraméter attribútum tartalmaznia kell.</span><span class="sxs-lookup"><span data-stu-id="978a4-122">This class must include a Parameter attribute for each parameter and any optional Alias and Validation attributes that are needed by the cmdlet.</span></span>

<span data-ttu-id="978a4-123">Példa:</span><span class="sxs-lookup"><span data-stu-id="978a4-123">Example:</span></span>

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

<span data-ttu-id="978a4-124">Egy parancsmag, amely támogatja a dinamikus paraméterek egy teljes példa: [deklarálja a dinamikus paraméterek hogyan](./how-to-declare-dynamic-parameters.md).</span><span class="sxs-lookup"><span data-stu-id="978a4-124">For a complete example of a cmdlet that supports dynamic parameters, see [How to Declare Dynamic Parameters](./how-to-declare-dynamic-parameters.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="978a4-125">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="978a4-125">See Also</span></span>

[<span data-ttu-id="978a4-126">System.Management.Automation.Idynamicparameters</span><span class="sxs-lookup"><span data-stu-id="978a4-126">System.Management.Automation.Idynamicparameters</span></span>](/dotnet/api/System.Management.Automation.IDynamicParameters)

[<span data-ttu-id="978a4-127">System.Management.Automation.Idynamicparameters.Getdynamicparameters\*</span><span class="sxs-lookup"><span data-stu-id="978a4-127">System.Management.Automation.Idynamicparameters.Getdynamicparameters\*</span></span>](/dotnet/api/System.Management.Automation.IDynamicParameters.GetDynamicParameters)

[<span data-ttu-id="978a4-128">Hogyan deklarálja a dinamikus paraméterek</span><span class="sxs-lookup"><span data-stu-id="978a4-128">How to Declare Dynamic Parameters</span></span>](./how-to-declare-dynamic-parameters.md)

[<span data-ttu-id="978a4-129">Egy Windows PowerShell-parancsmag írása</span><span class="sxs-lookup"><span data-stu-id="978a4-129">Writing a Windows PowerShell Cmdlet</span></span>](./writing-a-windows-powershell-cmdlet.md)
