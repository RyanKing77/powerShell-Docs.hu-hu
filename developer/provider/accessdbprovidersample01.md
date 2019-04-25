---
title: AccessDBProviderSample01 |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 853b7e5d-76c1-490e-8269-0ef31ba2ff13
caps.latest.revision: 10
ms.openlocfilehash: dc1ae92af8a57d6197b595db8e098256ac444b78
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62081121"
---
# <a name="accessdbprovidersample01"></a><span data-ttu-id="9bc41-102">AccessDBProviderSample01</span><span class="sxs-lookup"><span data-stu-id="9bc41-102">AccessDBProviderSample01</span></span>

<span data-ttu-id="9bc41-103">Ez a példa bemutatja, hogyan deklaráljon egy szolgáltató osztályt, amely közvetlenül a [System.Management.Automation.Provider.Cmdletprovider](/dotnet/api/System.Management.Automation.Provider.CmdletProvider) osztály.</span><span class="sxs-lookup"><span data-stu-id="9bc41-103">This sample shows how to declare a provider class that derives directly from the [System.Management.Automation.Provider.Cmdletprovider](/dotnet/api/System.Management.Automation.Provider.CmdletProvider) class.</span></span> <span data-ttu-id="9bc41-104">Része Itt csak a teljesség.</span><span class="sxs-lookup"><span data-stu-id="9bc41-104">It is included here only for completeness.</span></span>

## <a name="demonstrates"></a><span data-ttu-id="9bc41-105">Azt ismerteti</span><span class="sxs-lookup"><span data-stu-id="9bc41-105">Demonstrates</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9bc41-106">A szolgáltató osztálya nagy valószínűséggel célosztályából származik a következő osztályok egyike, és a valószínűleg az egyéb szolgáltató felületek megvalósításához:</span><span class="sxs-lookup"><span data-stu-id="9bc41-106">Your provider class will most likely derive from one of the following classes and possibly implement other provider interfaces:</span></span>
>
> -   <span data-ttu-id="9bc41-107">[System.Management.Automation.Provider.Itemcmdletprovider](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider) class.</span><span class="sxs-lookup"><span data-stu-id="9bc41-107">[System.Management.Automation.Provider.Itemcmdletprovider](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider) class.</span></span> <span data-ttu-id="9bc41-108">Lásd: [AccessDBProviderSample03](./accessdbprovidersample03.md).</span><span class="sxs-lookup"><span data-stu-id="9bc41-108">See [AccessDBProviderSample03](./accessdbprovidersample03.md).</span></span>
> -   <span data-ttu-id="9bc41-109">[System.Management.Automation.Provider.Containercmdletprovider](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider) class.</span><span class="sxs-lookup"><span data-stu-id="9bc41-109">[System.Management.Automation.Provider.Containercmdletprovider](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider) class.</span></span> <span data-ttu-id="9bc41-110">Lásd: [AccessDBProviderSample04](./accessdbprovidersample04.md).</span><span class="sxs-lookup"><span data-stu-id="9bc41-110">See [AccessDBProviderSample04](./accessdbprovidersample04.md).</span></span>
> -   <span data-ttu-id="9bc41-111">[System.Management.Automation.Provider.Navigationcmdletprovider](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider) class.</span><span class="sxs-lookup"><span data-stu-id="9bc41-111">[System.Management.Automation.Provider.Navigationcmdletprovider](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider) class.</span></span> <span data-ttu-id="9bc41-112">Lásd: [AccessDBProviderSample05](./accessdbprovidersample05.md).</span><span class="sxs-lookup"><span data-stu-id="9bc41-112">See [AccessDBProviderSample05](./accessdbprovidersample05.md).</span></span>
>
> <span data-ttu-id="9bc41-113">Melyik szolgáltató osztálya alapján a szolgáltató funkciói célosztályából származik, lásd: kiválasztásával kapcsolatban további információt [tervezése a Windows PowerShell-szolgáltatóban](./provider-types.md).</span><span class="sxs-lookup"><span data-stu-id="9bc41-113">For more information about choosing which provider class to derive from based on provider features, see [Designing Your Windows PowerShell Provider](./provider-types.md).</span></span>

<span data-ttu-id="9bc41-114">Ez a minta bemutatja a következőket:</span><span class="sxs-lookup"><span data-stu-id="9bc41-114">This sample demonstrates the following:</span></span>

- <span data-ttu-id="9bc41-115">Deklaráló a `CmdletProvider` attribútum.</span><span class="sxs-lookup"><span data-stu-id="9bc41-115">Declaring the `CmdletProvider` attribute.</span></span>

- <span data-ttu-id="9bc41-116">A szolgáltató osztályt, amely közvetlenül a meghatározása a [System.Management.Automation.Provider.Cmdletprovider](/dotnet/api/System.Management.Automation.Provider.CmdletProvider) osztály.</span><span class="sxs-lookup"><span data-stu-id="9bc41-116">Defining a provider class that derives directly from the [System.Management.Automation.Provider.Cmdletprovider](/dotnet/api/System.Management.Automation.Provider.CmdletProvider) class.</span></span>

## <a name="example"></a><span data-ttu-id="9bc41-117">Példa</span><span class="sxs-lookup"><span data-stu-id="9bc41-117">Example</span></span>

<span data-ttu-id="9bc41-118">Ez a példa bemutatja, egy szolgáltató osztálya definiálása és hogyan deklarálja a `CmdletProvider` attribútum.</span><span class="sxs-lookup"><span data-stu-id="9bc41-118">This sample shows how to define a provider class and how to declare the `CmdletProvider` attribute.</span></span>

```csharp
namespace Microsoft.Samples.PowerShell.Providers
{
  using System.Management.Automation;
  using System.Management.Automation.Provider;

  /// <summary>
  /// This sample shows how to declare a provider class and how to
  /// declare the CmdletProvider attribute.
  /// </summary>
  [CmdletProvider("AccessDB", ProviderCapabilities.None)]
  public class AccessDBProvider : CmdletProvider
  {
    // Add provider logic here.
  }
}
```

## <a name="see-also"></a><span data-ttu-id="9bc41-119">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="9bc41-119">See Also</span></span>

[<span data-ttu-id="9bc41-120">System.Management.Automation.Provider.Itemcmdletprovider</span><span class="sxs-lookup"><span data-stu-id="9bc41-120">System.Management.Automation.Provider.Itemcmdletprovider</span></span>](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider)

[<span data-ttu-id="9bc41-121">System.Management.Automation.Provider.Containercmdletprovider</span><span class="sxs-lookup"><span data-stu-id="9bc41-121">System.Management.Automation.Provider.Containercmdletprovider</span></span>](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider)

[<span data-ttu-id="9bc41-122">System.Management.Automation.Provider.Navigationcmdletprovider</span><span class="sxs-lookup"><span data-stu-id="9bc41-122">System.Management.Automation.Provider.Navigationcmdletprovider</span></span>](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider)

[<span data-ttu-id="9bc41-123">A Windows PowerShell-szolgáltató tervezése</span><span class="sxs-lookup"><span data-stu-id="9bc41-123">Designing Your Windows PowerShell Provider</span></span>](./provider-types.md)