---
title: Parancsmag dinamikus paramétereinek | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 8ae2196d-d6c8-4101-8805-4190d293af51
caps.latest.revision: 13
ms.openlocfilehash: 19d31f6b619dff23e7e35bb53d2397f4f41eb728
ms.sourcegitcommit: 5a004064f33acc0145ccd414535763e95f998c89
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/23/2019
ms.locfileid: "69986252"
---
# <a name="cmdlet-dynamic-parameters"></a><span data-ttu-id="835a6-102">Parancsmag dinamikus paraméterei</span><span class="sxs-lookup"><span data-stu-id="835a6-102">Cmdlet dynamic parameters</span></span>

<span data-ttu-id="835a6-103">A parancsmagok meghatározhatják azokat a paramétereket, amelyek a felhasználó számára speciális feltételek mellett érhetők el, például ha egy másik paraméter argumentuma egy adott érték.</span><span class="sxs-lookup"><span data-stu-id="835a6-103">Cmdlets can define parameters that are available to the user under special conditions, such as when the argument of another parameter is a specific value.</span></span> <span data-ttu-id="835a6-104">Ezeket a paramétereket a rendszer futásidőben adja hozzá, és dinamikus paramétereknek nevezzük, mivel ezek csak szükség esetén lesznek hozzáadva.</span><span class="sxs-lookup"><span data-stu-id="835a6-104">These parameters are added at runtime and are referred to as dynamic parameters because they're only added when needed.</span></span> <span data-ttu-id="835a6-105">Tervezhet például olyan parancsmagot, amely több paramétert ad meg, ha meg van adva egy adott kapcsoló paraméter.</span><span class="sxs-lookup"><span data-stu-id="835a6-105">For example, you can design a cmdlet that adds several parameters only when a specific switch parameter is specified.</span></span>

> [!NOTE]
> <span data-ttu-id="835a6-106">A szolgáltatók és a PowerShell-függvények dinamikus paramétereket is meghatározhatnak.</span><span class="sxs-lookup"><span data-stu-id="835a6-106">Providers and PowerShell functions can also define dynamic parameters.</span></span>

## <a name="dynamic-parameters-in-powershell-cmdlets"></a><span data-ttu-id="835a6-107">Dinamikus paraméterek a PowerShell-parancsmagokban</span><span class="sxs-lookup"><span data-stu-id="835a6-107">Dynamic parameters in PowerShell cmdlets</span></span>

<span data-ttu-id="835a6-108">A PowerShell dinamikus paramétereket használ számos szolgáltatói parancsmagban.</span><span class="sxs-lookup"><span data-stu-id="835a6-108">PowerShell uses dynamic parameters in several of its provider cmdlets.</span></span> <span data-ttu-id="835a6-109">A és `Get-Item` `Get-ChildItem` a parancsmag például a **CodeSigningCert** paramétert adja hozzá futásidőben, ha a **path** paraméter megadja a **hitelesítésszolgáltató** elérési útját.</span><span class="sxs-lookup"><span data-stu-id="835a6-109">For example, the `Get-Item` and `Get-ChildItem` cmdlets add a **CodeSigningCert** parameter at runtime when the **Path** parameter specifies the **Certificate** provider path.</span></span> <span data-ttu-id="835a6-110">Ha a **path** paraméter egy másik szolgáltató elérési útját határozza meg, a **CodeSigningCert** paraméter nem érhető el.</span><span class="sxs-lookup"><span data-stu-id="835a6-110">If the **Path** parameter specifies a path for a different provider, the **CodeSigningCert** parameter isn't available.</span></span>

<span data-ttu-id="835a6-111">Az alábbi példák `Get-Item` azt mutatják be, hogy a **CodeSigningCert** paraméter Hogyan vehető fel futásidőben a futtatáskor.</span><span class="sxs-lookup"><span data-stu-id="835a6-111">The following examples show how the **CodeSigningCert** parameter is added at runtime when `Get-Item` is run.</span></span>

<span data-ttu-id="835a6-112">Ebben a példában a PowerShell-futtatókörnyezet hozzáadta a paramétert, és a parancsmag sikeres.</span><span class="sxs-lookup"><span data-stu-id="835a6-112">In this example, the PowerShell runtime has added the parameter and the cmdlet is successful.</span></span>

```powershell
Get-Item -Path cert:\CurrentUser -CodeSigningCert
```

```Output
Location   : CurrentUser
StoreNames : {SmartCardRoot, UserDS, AuthRoot, CA...}
```

<span data-ttu-id="835a6-113">Ebben a példában egy **fájlrendszer** -meghajtó van megadva, és a rendszer hibát ad vissza.</span><span class="sxs-lookup"><span data-stu-id="835a6-113">In this example, a **FileSystem** drive is specified and an error is returned.</span></span> <span data-ttu-id="835a6-114">A hibaüzenet azt jelzi, hogy a **CodeSigningCert** paraméter nem található.</span><span class="sxs-lookup"><span data-stu-id="835a6-114">The error message indicates that the **CodeSigningCert** parameter can't be found.</span></span>

```powershell
Get-Item -Path C:\ -CodeSigningCert
```

```Output
Get-Item : A parameter cannot be found that matches parameter name 'codesigningcert'.
At line:1 char:37
+  get-item -path C:\ -codesigningcert <<<<
--------
    CategoryInfo          : InvalidArgument: (:) [Get-Item], ParameterBindingException
    FullyQualifiedErrorId : NamedParameterNotFound,Microsoft.PowerShell.Commands.GetItemCommand
```

## <a name="support-for-dynamic-parameters"></a><span data-ttu-id="835a6-115">Dinamikus paraméterek támogatása</span><span class="sxs-lookup"><span data-stu-id="835a6-115">Support for dynamic parameters</span></span>

<span data-ttu-id="835a6-116">A dinamikus paraméterek támogatásához a következő elemeknek szerepelniük kell a parancsmag kódjában.</span><span class="sxs-lookup"><span data-stu-id="835a6-116">To support dynamic parameters, the following elements must be included in the cmdlet code.</span></span>

### <a name="interface"></a><span data-ttu-id="835a6-117">Interfész</span><span class="sxs-lookup"><span data-stu-id="835a6-117">Interface</span></span>

<span data-ttu-id="835a6-118">[System. Management. Automation. IDynamicParameters](/dotnet/api/System.Management.Automation.IDynamicParameters).</span><span class="sxs-lookup"><span data-stu-id="835a6-118">[System.Management.Automation.IDynamicParameters](/dotnet/api/System.Management.Automation.IDynamicParameters).</span></span>
<span data-ttu-id="835a6-119">Ez az interfész biztosítja a dinamikus paraméterek lekérésére szolgáló metódust.</span><span class="sxs-lookup"><span data-stu-id="835a6-119">This interface provides the method that retrieves the dynamic parameters.</span></span>

<span data-ttu-id="835a6-120">Például:</span><span class="sxs-lookup"><span data-stu-id="835a6-120">For example:</span></span>

`public class SendGreetingCommand : Cmdlet, IDynamicParameters`

### <a name="method"></a><span data-ttu-id="835a6-121">Módszer</span><span class="sxs-lookup"><span data-stu-id="835a6-121">Method</span></span>

<span data-ttu-id="835a6-122">[System. Management. Automation. IDynamicParameters. GetDynamicParameters](/dotnet/api/System.Management.Automation.IDynamicParameters.GetDynamicParameters).</span><span class="sxs-lookup"><span data-stu-id="835a6-122">[System.Management.Automation.IDynamicParameters.GetDynamicParameters](/dotnet/api/System.Management.Automation.IDynamicParameters.GetDynamicParameters).</span></span>
<span data-ttu-id="835a6-123">Ez a metódus lekéri a dinamikus paraméterek definícióit tartalmazó objektumot.</span><span class="sxs-lookup"><span data-stu-id="835a6-123">This method retrieves the object that contains the dynamic parameter definitions.</span></span>

<span data-ttu-id="835a6-124">Például:</span><span class="sxs-lookup"><span data-stu-id="835a6-124">For example:</span></span>

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

### <a name="class"></a><span data-ttu-id="835a6-125">Osztály</span><span class="sxs-lookup"><span data-stu-id="835a6-125">Class</span></span>

<span data-ttu-id="835a6-126">Egy osztály, amely meghatározza a hozzáadandó dinamikus paramétereket.</span><span class="sxs-lookup"><span data-stu-id="835a6-126">A class that defines the dynamic parameters to be added.</span></span> <span data-ttu-id="835a6-127">Ennek az osztálynak tartalmaznia kell egy **paraméter** -attribútumot az egyes paraméterekhez, valamint a parancsmaghoz szükséges nem kötelező **aliasokat** és **érvényesítési** attribútumokat.</span><span class="sxs-lookup"><span data-stu-id="835a6-127">This class must include a **Parameter** attribute for each parameter and any optional **Alias** and **Validation** attributes that are needed by the cmdlet.</span></span>

<span data-ttu-id="835a6-128">Például:</span><span class="sxs-lookup"><span data-stu-id="835a6-128">For example:</span></span>

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

<span data-ttu-id="835a6-129">A dinamikus paramétereket támogató parancsmagok teljes példáját a [dinamikus paraméterek deklarálása](./how-to-declare-dynamic-parameters.md)című témakörben tekintheti meg.</span><span class="sxs-lookup"><span data-stu-id="835a6-129">For a complete example of a cmdlet that supports dynamic parameters, see [How to Declare Dynamic Parameters](./how-to-declare-dynamic-parameters.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="835a6-130">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="835a6-130">See also</span></span>

[<span data-ttu-id="835a6-131">System. Management. Automation. IDynamicParameters</span><span class="sxs-lookup"><span data-stu-id="835a6-131">System.Management.Automation.IDynamicParameters</span></span>](/dotnet/api/System.Management.Automation.IDynamicParameters)

[<span data-ttu-id="835a6-132">System. Management. Automation. IDynamicParameters. GetDynamicParameters</span><span class="sxs-lookup"><span data-stu-id="835a6-132">System.Management.Automation.IDynamicParameters.GetDynamicParameters</span></span>](/dotnet/api/System.Management.Automation.IDynamicParameters.GetDynamicParameters)

[<span data-ttu-id="835a6-133">Dinamikus paraméterek deklarálása</span><span class="sxs-lookup"><span data-stu-id="835a6-133">How to Declare Dynamic Parameters</span></span>](./how-to-declare-dynamic-parameters.md)

[<span data-ttu-id="835a6-134">Windows PowerShell-parancsmag írása</span><span class="sxs-lookup"><span data-stu-id="835a6-134">Writing a Windows PowerShell Cmdlet</span></span>](./writing-a-windows-powershell-cmdlet.md)
