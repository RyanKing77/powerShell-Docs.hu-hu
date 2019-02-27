---
title: AccessDBProviderSample06 |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 46dc0657-110f-4367-8bb6-a95dca2c5016
caps.latest.revision: 8
ms.openlocfilehash: 59832ed8a4fad3b07a171946bff28fb3e1dbe442
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56845870"
---
# <a name="accessdbprovidersample06"></a><span data-ttu-id="bb52a-102">AccessDBProviderSample06</span><span class="sxs-lookup"><span data-stu-id="bb52a-102">AccessDBProviderSample06</span></span>

<span data-ttu-id="bb52a-103">Ez a példa bemutatja, hogyan tartalom módszerek támogatásához a hívásokat írja felül a `Clear-Content`, `Get-Content`, és `Set-Content` parancsmagok.</span><span class="sxs-lookup"><span data-stu-id="bb52a-103">This sample shows how to overwrite content methods to support calls to the `Clear-Content`, `Get-Content`, and `Set-Content` cmdlets.</span></span> <span data-ttu-id="bb52a-104">Ezek a metódusok kell végrehajtani, amikor a felhasználó az adattárban lévő cikkek a tartalom kezelésére kell.</span><span class="sxs-lookup"><span data-stu-id="bb52a-104">These methods should be implemented when the user needs to manage the content of the items in the data store.</span></span> <span data-ttu-id="bb52a-105">Ebben a példában a szolgáltató osztálya származik a [System.Management.Automation.Provider.Navigationcmdletprovider](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider) osztály, és implementálja a [ System.Management.Automation.Provider.Icontentcmdletprovider](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider) felületet.</span><span class="sxs-lookup"><span data-stu-id="bb52a-105">The provider class in this sample derives from the [System.Management.Automation.Provider.Navigationcmdletprovider](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider) class, and it implements the [System.Management.Automation.Provider.Icontentcmdletprovider](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider) interface.</span></span>

## <a name="demonstrates"></a><span data-ttu-id="bb52a-106">Bemutatók</span><span class="sxs-lookup"><span data-stu-id="bb52a-106">Demonstrates</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bb52a-107">A szolgáltató osztálya nagy valószínűséggel célosztályából származik a következő osztályok egyike, és a valószínűleg az egyéb szolgáltató felületek megvalósításához:</span><span class="sxs-lookup"><span data-stu-id="bb52a-107">Your provider class will most likely derive from one of the following classes and possibly implement other provider interfaces:</span></span>
>
> -   <span data-ttu-id="bb52a-108">[System.Management.Automation.Provider.Itemcmdletprovider](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider) class.</span><span class="sxs-lookup"><span data-stu-id="bb52a-108">[System.Management.Automation.Provider.Itemcmdletprovider](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider) class.</span></span> <span data-ttu-id="bb52a-109">Lásd: [AccessDBProviderSample03](./accessdbprovidersample03.md).</span><span class="sxs-lookup"><span data-stu-id="bb52a-109">See [AccessDBProviderSample03](./accessdbprovidersample03.md).</span></span>
> -   <span data-ttu-id="bb52a-110">[System.Management.Automation.Provider.Containercmdletprovider](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider) class.</span><span class="sxs-lookup"><span data-stu-id="bb52a-110">[System.Management.Automation.Provider.Containercmdletprovider](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider) class.</span></span> <span data-ttu-id="bb52a-111">Lásd: [AccessDBProviderSample04](./accessdbprovidersample04.md).</span><span class="sxs-lookup"><span data-stu-id="bb52a-111">See [AccessDBProviderSample04](./accessdbprovidersample04.md).</span></span>
> -   <span data-ttu-id="bb52a-112">[System.Management.Automation.Provider.Navigationcmdletprovider](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider) class.</span><span class="sxs-lookup"><span data-stu-id="bb52a-112">[System.Management.Automation.Provider.Navigationcmdletprovider](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider) class.</span></span>
>
> <span data-ttu-id="bb52a-113">Melyik szolgáltató osztálya alapján a szolgáltató funkciói célosztályából származik, lásd: kiválasztásával kapcsolatban további információt [tervezése a Windows PowerShell-szolgáltatóban](./provider-types.md).</span><span class="sxs-lookup"><span data-stu-id="bb52a-113">For more information about choosing which provider class to derive from based on provider features, see [Designing Your Windows PowerShell Provider](./provider-types.md).</span></span>

<span data-ttu-id="bb52a-114">Ez a minta bemutatja a következőket:</span><span class="sxs-lookup"><span data-stu-id="bb52a-114">This sample demonstrates the following:</span></span>

- <span data-ttu-id="bb52a-115">Deklaráló a `CmdletProvider` attribútum.</span><span class="sxs-lookup"><span data-stu-id="bb52a-115">Declaring the `CmdletProvider` attribute.</span></span>

- <span data-ttu-id="bb52a-116">A szolgáltató osztályt, amely a meghatározása a [System.Management.Automation.Provider.Navigationcmdletprovider](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider) deklarálja class, és hogy a [ System.Management.Automation.Provider.Icontentcmdletprovider](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider) felületet.</span><span class="sxs-lookup"><span data-stu-id="bb52a-116">Defining a provider class that derives from the [System.Management.Automation.Provider.Navigationcmdletprovider](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider) class and that declares the [System.Management.Automation.Provider.Icontentcmdletprovider](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider) interface.</span></span>

- <span data-ttu-id="bb52a-117">Írja felül a [System.Management.Automation.Provider.Icontentcmdletprovider.Clearcontent\*](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider.ClearContent) metódust változtathatja meg a `Clear-Content` parancsmagot, a felhasználó a tartalom eltávolítása egy elemet.</span><span class="sxs-lookup"><span data-stu-id="bb52a-117">Overwriting the [System.Management.Automation.Provider.Icontentcmdletprovider.Clearcontent\*](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider.ClearContent) method to change the behavior of the `Clear-Content` cmdlet, allowing the user to remove the content from an item.</span></span> <span data-ttu-id="bb52a-118">(Ez a minta nem jeleníti meg a dinamikus paraméterek hozzáadása a `Clear-Content` parancsmagot.)</span><span class="sxs-lookup"><span data-stu-id="bb52a-118">(This sample does not show how to add dynamic parameters to the `Clear-Content` cmdlet.)</span></span>

- <span data-ttu-id="bb52a-119">Írja felül a [System.Management.Automation.Provider.Icontentcmdletprovider.Getcontentreader\*](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider.GetContentReader) metódust változtathatja meg a `Get-Content` parancsmagot, lehetővé téve a felhasználó lekérni a tartalmat egy elem.</span><span class="sxs-lookup"><span data-stu-id="bb52a-119">Overwriting the [System.Management.Automation.Provider.Icontentcmdletprovider.Getcontentreader\*](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider.GetContentReader) method to change the behavior of the `Get-Content` cmdlet, allowing the user to retrieve the content of an item.</span></span> <span data-ttu-id="bb52a-120">(Ez a minta nem jeleníti meg a dinamikus paraméterek hozzáadása a `Get-Content` parancsmagot.).</span><span class="sxs-lookup"><span data-stu-id="bb52a-120">(This sample does not show how to add dynamic parameters to the `Get-Content` cmdlet.).</span></span>

- <span data-ttu-id="bb52a-121">Írja felül a [Microsoft.Powershell.Commands.Filesystemprovider.Getcontentwriter\*](/dotnet/api/Microsoft.PowerShell.Commands.FileSystemProvider.GetContentWriter) metódust változtathatja meg a `Set-Content` parancsmagot, a felhasználók egy elem a tartalom frissítéséhez.</span><span class="sxs-lookup"><span data-stu-id="bb52a-121">Overwriting the [Microsoft.Powershell.Commands.Filesystemprovider.Getcontentwriter\*](/dotnet/api/Microsoft.PowerShell.Commands.FileSystemProvider.GetContentWriter) method to change the behavior of the `Set-Content` cmdlet, allowing the user to update the content of an item.</span></span> <span data-ttu-id="bb52a-122">(Ez a minta nem jeleníti meg a dinamikus paraméterek hozzáadása a `Set-Content` parancsmagot.)</span><span class="sxs-lookup"><span data-stu-id="bb52a-122">(This sample does not show how to add dynamic parameters to the `Set-Content` cmdlet.)</span></span>

## <a name="example"></a><span data-ttu-id="bb52a-123">Példa</span><span class="sxs-lookup"><span data-stu-id="bb52a-123">Example</span></span>

<span data-ttu-id="bb52a-124">Ez a példa bemutatja, hogyan felülírja a módszereket, törlése, beolvasása, és egy Microsoft Access-adatok cikkek tartalmának base beállítása szükséges.</span><span class="sxs-lookup"><span data-stu-id="bb52a-124">This sample shows how to overwrite the methods needed to clear, get, and set the content of items in a Microsoft Access data base.</span></span>

[!code-csharp[AccessDBProviderSample06.cs](../../powershell-sdk-samples/SDK-2.0/csharp/AccessDBProviderSample06/AccessDBProviderSample06.cs#L11-L2399 "AccessDBProviderSample06.cs")]

## <a name="see-also"></a><span data-ttu-id="bb52a-125">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="bb52a-125">See Also</span></span>

[<span data-ttu-id="bb52a-126">System.Management.Automation.Provider.Itemcmdletprovider</span><span class="sxs-lookup"><span data-stu-id="bb52a-126">System.Management.Automation.Provider.Itemcmdletprovider</span></span>](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider)

[<span data-ttu-id="bb52a-127">System.Management.Automation.Provider.Containercmdletprovider</span><span class="sxs-lookup"><span data-stu-id="bb52a-127">System.Management.Automation.Provider.Containercmdletprovider</span></span>](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider)

[<span data-ttu-id="bb52a-128">System.Management.Automation.Provider.Navigationcmdletprovider</span><span class="sxs-lookup"><span data-stu-id="bb52a-128">System.Management.Automation.Provider.Navigationcmdletprovider</span></span>](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider)

[<span data-ttu-id="bb52a-129">A Windows PowerShell-szolgáltató tervezése</span><span class="sxs-lookup"><span data-stu-id="bb52a-129">Designing Your Windows PowerShell Provider</span></span>](./provider-types.md)