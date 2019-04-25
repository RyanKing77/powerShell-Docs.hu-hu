---
title: AccessDBProviderSample03 |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 9e576199-49c7-4355-9686-f9ed40c64a5f
caps.latest.revision: 10
ms.openlocfilehash: 57b6cfaa5f29300c60a5a745797111b6beba3133
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62081070"
---
# <a name="accessdbprovidersample03"></a><span data-ttu-id="54cd1-102">AccessDBProviderSample03</span><span class="sxs-lookup"><span data-stu-id="54cd1-102">AccessDBProviderSample03</span></span>

<span data-ttu-id="54cd1-103">Ez a példa bemutatja, hogyan felülírja a [System.Management.Automation.Provider.Itemcmdletprovider.Getitem\*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.GetItem) és [System.Management.Automation.Provider.Itemcmdletprovider.Setitem\*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.SetItem) módszereket támogatja a hívást a `Get-Item` és `Set-Item` parancsmagok.</span><span class="sxs-lookup"><span data-stu-id="54cd1-103">This sample shows how to overwrite the [System.Management.Automation.Provider.Itemcmdletprovider.Getitem\*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.GetItem) and [System.Management.Automation.Provider.Itemcmdletprovider.Setitem\*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.SetItem) methods to support calls to the `Get-Item` and `Set-Item` cmdlets.</span></span> <span data-ttu-id="54cd1-104">Ebben a példában a szolgáltató osztálya származik a [System.Management.Automation.Provider.Itemcmdletprovider](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider) osztály.</span><span class="sxs-lookup"><span data-stu-id="54cd1-104">The provider class in this sample derives from the [System.Management.Automation.Provider.Itemcmdletprovider](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider) class.</span></span>

## <a name="demonstrates"></a><span data-ttu-id="54cd1-105">Azt ismerteti</span><span class="sxs-lookup"><span data-stu-id="54cd1-105">Demonstrates</span></span>

> [!IMPORTANT]
> <span data-ttu-id="54cd1-106">A szolgáltató osztálya nagy valószínűséggel célosztályából származik a következő osztályok egyike, és a valószínűleg az egyéb szolgáltató felületek megvalósításához:</span><span class="sxs-lookup"><span data-stu-id="54cd1-106">Your provider class will most likely derive from one of the following classes and possibly implement other provider interfaces:</span></span>
>
> -   <span data-ttu-id="54cd1-107">[System.Management.Automation.Provider.Itemcmdletprovider](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider) class.</span><span class="sxs-lookup"><span data-stu-id="54cd1-107">[System.Management.Automation.Provider.Itemcmdletprovider](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider) class.</span></span>
> -   <span data-ttu-id="54cd1-108">[System.Management.Automation.Provider.Containercmdletprovider](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider) class.</span><span class="sxs-lookup"><span data-stu-id="54cd1-108">[System.Management.Automation.Provider.Containercmdletprovider](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider) class.</span></span> <span data-ttu-id="54cd1-109">Lásd: [AccessDBProviderSample04](./accessdbprovidersample04.md).</span><span class="sxs-lookup"><span data-stu-id="54cd1-109">See [AccessDBProviderSample04](./accessdbprovidersample04.md).</span></span>
> -   <span data-ttu-id="54cd1-110">[System.Management.Automation.Provider.Navigationcmdletprovider](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider) class.</span><span class="sxs-lookup"><span data-stu-id="54cd1-110">[System.Management.Automation.Provider.Navigationcmdletprovider](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider) class.</span></span> <span data-ttu-id="54cd1-111">Lásd: [AccessDBProviderSample05](./accessdbprovidersample05.md).</span><span class="sxs-lookup"><span data-stu-id="54cd1-111">See [AccessDBProviderSample05](./accessdbprovidersample05.md).</span></span>
>
> <span data-ttu-id="54cd1-112">Melyik szolgáltató osztálya alapján a szolgáltató funkciói célosztályából származik, lásd: kiválasztásával kapcsolatban további információt [tervezése a Windows PowerShell-szolgáltatóban](./provider-types.md).</span><span class="sxs-lookup"><span data-stu-id="54cd1-112">For more information about choosing which provider class to derive from based on provider features, see [Designing Your Windows PowerShell Provider](./provider-types.md).</span></span>

<span data-ttu-id="54cd1-113">Ez a minta bemutatja a következőket:</span><span class="sxs-lookup"><span data-stu-id="54cd1-113">This sample demonstrates the following:</span></span>

- <span data-ttu-id="54cd1-114">Deklaráló a `CmdletProvider` attribútum.</span><span class="sxs-lookup"><span data-stu-id="54cd1-114">Declaring the `CmdletProvider` attribute.</span></span>

- <span data-ttu-id="54cd1-115">A szolgáltató osztályt, amely a meghatározása a [System.Management.Automation.Provider.Itemcmdletprovider](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider) osztály.</span><span class="sxs-lookup"><span data-stu-id="54cd1-115">Defining a provider class that derives from the [System.Management.Automation.Provider.Itemcmdletprovider](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider) class.</span></span>

- <span data-ttu-id="54cd1-116">Írja felül a [System.Management.Automation.Provider.Drivecmdletprovider.Newdrive\*](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider.NewDrive) metódust változtathatja meg a `New-PSDrive` parancsmagot, a felhasználó létrehozása az új meghajtókat.</span><span class="sxs-lookup"><span data-stu-id="54cd1-116">Overwriting the [System.Management.Automation.Provider.Drivecmdletprovider.Newdrive\*](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider.NewDrive) method to change the behavior of the `New-PSDrive` cmdlet, allowing the user to create new drives.</span></span> <span data-ttu-id="54cd1-117">(Ez a minta nem jeleníti meg a dinamikus paraméterek hozzáadása a `New-PSDrive` parancsmagot.)</span><span class="sxs-lookup"><span data-stu-id="54cd1-117">(This sample does not show how to add dynamic parameters to the `New-PSDrive` cmdlet.)</span></span>

- <span data-ttu-id="54cd1-118">Írja felül a [System.Management.Automation.Provider.Drivecmdletprovider.Removedrive\*](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider.RemoveDrive) módszer eltávolítja a meglévő meghajtók támogatásához.</span><span class="sxs-lookup"><span data-stu-id="54cd1-118">Overwriting the [System.Management.Automation.Provider.Drivecmdletprovider.Removedrive\*](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider.RemoveDrive) method to support removing existing drives.</span></span>

- <span data-ttu-id="54cd1-119">Írja felül a [System.Management.Automation.Provider.Itemcmdletprovider.Getitem\*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.GetItem) metódust változtathatja meg a `Get-Item` parancsmagot, lehetővé téve a felhasználó az elemek lekéréséhez az adatokat az adattárból.</span><span class="sxs-lookup"><span data-stu-id="54cd1-119">Overwriting the [System.Management.Automation.Provider.Itemcmdletprovider.Getitem\*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.GetItem) method to change the behavior of the `Get-Item` cmdlet, allowing the user to retrieve items from the data store.</span></span> <span data-ttu-id="54cd1-120">(Ez a minta nem jeleníti meg a dinamikus paraméterek hozzáadása a `Get-Item` parancsmagot.)</span><span class="sxs-lookup"><span data-stu-id="54cd1-120">(This sample does not show how to add dynamic parameters to the `Get-Item` cmdlet.)</span></span>

- <span data-ttu-id="54cd1-121">Írja felül a [System.Management.Automation.Provider.Itemcmdletprovider.Setitem\*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.SetItem) metódust változtathatja meg a `Set-Item` parancsmagot, a felhasználók a cikkek az adattárban frissíteni.</span><span class="sxs-lookup"><span data-stu-id="54cd1-121">Overwriting the [System.Management.Automation.Provider.Itemcmdletprovider.Setitem\*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.SetItem) method to change the behavior of the `Set-Item` cmdlet, allowing the user to update the items in the data store.</span></span> <span data-ttu-id="54cd1-122">(Ez a minta nem jeleníti meg a dinamikus paraméterek hozzáadása a `Get-Item` parancsmagot.)</span><span class="sxs-lookup"><span data-stu-id="54cd1-122">(This sample does not show how to add dynamic parameters to the `Get-Item` cmdlet.)</span></span>

- <span data-ttu-id="54cd1-123">Írja felül a [System.Management.Automation.Provider.Itemcmdletprovider.Itemexists\*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.ItemExists) metódust változtathatja meg a `Test-Path` parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="54cd1-123">Overwriting the [System.Management.Automation.Provider.Itemcmdletprovider.Itemexists\*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.ItemExists) method to change the behavior of the `Test-Path` cmdlet.</span></span> <span data-ttu-id="54cd1-124">(Ez a minta nem jeleníti meg a dinamikus paraméterek hozzáadása a `Test-Path` parancsmagot.)</span><span class="sxs-lookup"><span data-stu-id="54cd1-124">(This sample does not show how to add dynamic parameters to the `Test-Path` cmdlet.)</span></span>

- <span data-ttu-id="54cd1-125">Írja felül a [System.Management.Automation.Provider.Itemcmdletprovider.Isvalidpath\*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.IsValidPath) módszer annak megállapításához, hogy a megadott elérési út érvényes.</span><span class="sxs-lookup"><span data-stu-id="54cd1-125">Overwriting the [System.Management.Automation.Provider.Itemcmdletprovider.Isvalidpath\*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.IsValidPath) method to determine if the provided path is valid.</span></span>

## <a name="example"></a><span data-ttu-id="54cd1-126">Példa</span><span class="sxs-lookup"><span data-stu-id="54cd1-126">Example</span></span>

<span data-ttu-id="54cd1-127">Ez a példa bemutatja, hogyan felülírja a lekéréséhez és a egy Microsoft Access-adatok elemek alap beállításához szükséges módszereket.</span><span class="sxs-lookup"><span data-stu-id="54cd1-127">This sample shows how to overwrite the methods needed to get and set items in a Microsoft Access data base.</span></span>

[!code-csharp[AccessDBProviderSample03.cs](../../powershell-sdk-samples/SDK-2.0/csharp/AccessDBProviderSample06/AccessDBProviderSample06.cs#L11-L976 "AccessDBProviderSample03.cs")]

## <a name="see-also"></a><span data-ttu-id="54cd1-128">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="54cd1-128">See Also</span></span>

[<span data-ttu-id="54cd1-129">System.Management.Automation.Provider.Itemcmdletprovider</span><span class="sxs-lookup"><span data-stu-id="54cd1-129">System.Management.Automation.Provider.Itemcmdletprovider</span></span>](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider)

[<span data-ttu-id="54cd1-130">System.Management.Automation.Provider.Containercmdletprovider</span><span class="sxs-lookup"><span data-stu-id="54cd1-130">System.Management.Automation.Provider.Containercmdletprovider</span></span>](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider)

[<span data-ttu-id="54cd1-131">System.Management.Automation.Provider.Navigationcmdletprovider</span><span class="sxs-lookup"><span data-stu-id="54cd1-131">System.Management.Automation.Provider.Navigationcmdletprovider</span></span>](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider)

[<span data-ttu-id="54cd1-132">A Windows PowerShell-szolgáltató tervezése</span><span class="sxs-lookup"><span data-stu-id="54cd1-132">Designing Your Windows PowerShell Provider</span></span>](./provider-types.md)