---
title: AccessDBProviderSample04 |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ee3a7e56-7331-4f71-9ecb-7a59b8021c68
caps.latest.revision: 10
ms.openlocfilehash: d9109e8d5b69a25ad52b90bcaff9628b01067211
ms.sourcegitcommit: caac7d098a448232304c9d6728e7340ec7517a71
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/16/2019
ms.locfileid: "58057620"
---
# <a name="accessdbprovidersample04"></a><span data-ttu-id="bc446-102">AccessDBProviderSample04</span><span class="sxs-lookup"><span data-stu-id="bc446-102">AccessDBProviderSample04</span></span>

<span data-ttu-id="bc446-103">Ez a példa bemutatja, hogyan tároló módszerek támogatásához a hívásokat írja felül a `Copy-Item`, `Get-ChildItem`, `New-Item`, és `Remove-Item` parancsmagok.</span><span class="sxs-lookup"><span data-stu-id="bc446-103">This sample shows how to overwrite container methods to support calls to the `Copy-Item`, `Get-ChildItem`, `New-Item`, and `Remove-Item` cmdlets.</span></span> <span data-ttu-id="bc446-104">Ezek a metódusok kell végrehajtani, ha az adattár tartalmaz, amelyek olyan tárolók elemek.</span><span class="sxs-lookup"><span data-stu-id="bc446-104">These methods should be implemented when the data store contains items that are containers.</span></span> <span data-ttu-id="bc446-105">A tároló egy olyan csoport gyermekelemek egy közös szülő elem alatt.</span><span class="sxs-lookup"><span data-stu-id="bc446-105">A container is a group of child items under a common parent item.</span></span> <span data-ttu-id="bc446-106">Ebben a példában a szolgáltató osztálya származik a [System.Management.Automation.Provider.Containercmdletprovider](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider) osztály.</span><span class="sxs-lookup"><span data-stu-id="bc446-106">The provider class in this sample derives from the [System.Management.Automation.Provider.Containercmdletprovider](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider) class.</span></span>

## <a name="demonstrates"></a><span data-ttu-id="bc446-107">Bemutatók</span><span class="sxs-lookup"><span data-stu-id="bc446-107">Demonstrates</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bc446-108">A szolgáltató osztálya nagy valószínűséggel lesz származtatva a [System.Management.Automation.Provider.Navigationcmdletprovider](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider)</span><span class="sxs-lookup"><span data-stu-id="bc446-108">Your provider class will most likely derive from the [System.Management.Automation.Provider.Navigationcmdletprovider](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider)</span></span>

<span data-ttu-id="bc446-109">Ez a minta bemutatja a következőket:</span><span class="sxs-lookup"><span data-stu-id="bc446-109">This sample demonstrates the following:</span></span>

- <span data-ttu-id="bc446-110">Deklaráló a `CmdletProvider` attribútum.</span><span class="sxs-lookup"><span data-stu-id="bc446-110">Declaring the `CmdletProvider` attribute.</span></span>

- <span data-ttu-id="bc446-111">A szolgáltató osztályt, amely a meghatározása a [System.Management.Automation.Provider.Containercmdletprovider](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider) osztály.</span><span class="sxs-lookup"><span data-stu-id="bc446-111">Defining a provider class that derives from the [System.Management.Automation.Provider.Containercmdletprovider](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider) class.</span></span>

- <span data-ttu-id="bc446-112">Írja felül a [System.Management.Automation.Provider.ContainerCmdletProvider.CopyItem](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.CopyItem) metódust változtathatja meg a `Copy-Item` parancsmag, mely lehetővé teszi, hogy a felhasználót, hogy elemek másolása egyik helyről egy másikra.</span><span class="sxs-lookup"><span data-stu-id="bc446-112">Overwriting the [System.Management.Automation.Provider.ContainerCmdletProvider.CopyItem](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.CopyItem) method to change the behavior of the `Copy-Item` cmdlet which allows the user to copy items from one location to another.</span></span> <span data-ttu-id="bc446-113">(Ez a minta nem jeleníti meg a dinamikus paraméterek hozzáadása a `Copy-Item` parancsmagot.)</span><span class="sxs-lookup"><span data-stu-id="bc446-113">(This sample does not show how to add dynamic parameters to the `Copy-Item` cmdlet.)</span></span>

- <span data-ttu-id="bc446-114">Írja felül a [System.Management.Automation.Provider.Containercmdletprovider.Getchilditems\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.GetChildItems) változtathatja meg a Get-ChildItems parancsmagot, amely lehetővé teszi, hogy a fölérendelt elemtől bejárásához a lekérdezni kívánt felhasználó metódus .</span><span class="sxs-lookup"><span data-stu-id="bc446-114">Overwriting the [System.Management.Automation.Provider.Containercmdletprovider.Getchilditems\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.GetChildItems) method to change the behavior of the Get-ChildItems cmdlet, which allows the user to retrieve the child items of the parent item.</span></span> <span data-ttu-id="bc446-115">(Ez a minta nem jeleníti meg a dinamikus paraméterek hozzáadása a Get-ChildItems parancsmagot.)</span><span class="sxs-lookup"><span data-stu-id="bc446-115">(This sample does not show how to add dynamic parameters to the Get-ChildItems cmdlet.)</span></span>

- <span data-ttu-id="bc446-116">Írja felül a [System.Management.Automation.Provider.Containercmdletprovider.Getchildnames\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.GetChildNames) változtathatja meg a Get-ChildItems parancsmag metódus során a `Name` a parancsmag paraméter meg van adva.</span><span class="sxs-lookup"><span data-stu-id="bc446-116">Overwriting the [System.Management.Automation.Provider.Containercmdletprovider.Getchildnames\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.GetChildNames) method to change the behavior of the Get-ChildItems cmdlet when the `Name` parameter of the cmdlet is specified.</span></span>

- <span data-ttu-id="bc446-117">Írja felül a [System.Management.Automation.Provider.Containercmdletprovider.Newitem\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.NewItem) metódust változtathatja meg a `New-Item` parancsmagot, amely lehetővé teszi a felhasználó elemek hozzáadása az adattár.</span><span class="sxs-lookup"><span data-stu-id="bc446-117">Overwriting the [System.Management.Automation.Provider.Containercmdletprovider.Newitem\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.NewItem) method to change the behavior of the `New-Item` cmdlet, which allows the user to add items to the data store.</span></span> <span data-ttu-id="bc446-118">(Ez a minta nem jeleníti meg a dinamikus paraméterek hozzáadása a `New-Item` parancsmagot.)</span><span class="sxs-lookup"><span data-stu-id="bc446-118">(This sample does not show how to add dynamic parameters to the `New-Item` cmdlet.)</span></span>

- <span data-ttu-id="bc446-119">Írja felül a [System.Management.Automation.Provider.Containercmdletprovider.Removeitem\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.RemoveItem) metódust változtathatja meg a `Remove-Item` parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="bc446-119">Overwriting the [System.Management.Automation.Provider.Containercmdletprovider.Removeitem\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.RemoveItem) method to change the behavior of the `Remove-Item` cmdlet.</span></span> <span data-ttu-id="bc446-120">(Ez a minta nem jeleníti meg a dinamikus paraméterek hozzáadása a `Remove-Item` parancsmagot.)</span><span class="sxs-lookup"><span data-stu-id="bc446-120">(This sample does not show how to add dynamic parameters to the `Remove-Item` cmdlet.)</span></span>

## <a name="example"></a><span data-ttu-id="bc446-121">Példa</span><span class="sxs-lookup"><span data-stu-id="bc446-121">Example</span></span>

<span data-ttu-id="bc446-122">Ez a példa bemutatja, hogyan felülírja a szükséges másolni, hozzon létre, majd távolítsa el az elemeket, valamint a gyermek és egy szülő cikk elemeinek beolvasása közben módszerei módszereket.</span><span class="sxs-lookup"><span data-stu-id="bc446-122">This sample shows how to overwrite the methods needed to copy, create, and remove items, as well as methods for getting the child items of a parent item.</span></span>

[!code-csharp[AccessDBProviderSample04.cs](../../powershell-sdk-samples/SDK-2.0/csharp/AccessDBProviderSample06/AccessDBProviderSample06.cs#L11-L1635 "AccessDBProviderSample04.cs")]

## <a name="see-also"></a><span data-ttu-id="bc446-123">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="bc446-123">See Also</span></span>

[<span data-ttu-id="bc446-124">System.Management.Automation.Provider.Itemcmdletprovider</span><span class="sxs-lookup"><span data-stu-id="bc446-124">System.Management.Automation.Provider.Itemcmdletprovider</span></span>](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider)

[<span data-ttu-id="bc446-125">System.Management.Automation.Provider.Containercmdletprovider</span><span class="sxs-lookup"><span data-stu-id="bc446-125">System.Management.Automation.Provider.Containercmdletprovider</span></span>](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider)

[<span data-ttu-id="bc446-126">System.Management.Automation.Provider.Navigationcmdletprovider</span><span class="sxs-lookup"><span data-stu-id="bc446-126">System.Management.Automation.Provider.Navigationcmdletprovider</span></span>](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider)

[<span data-ttu-id="bc446-127">A Windows PowerShell-szolgáltató tervezése</span><span class="sxs-lookup"><span data-stu-id="bc446-127">Designing Your Windows PowerShell Provider</span></span>](./provider-types.md)