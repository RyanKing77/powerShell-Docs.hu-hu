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
ms.openlocfilehash: f020f023f9a379ff8a610edb7d5dcfe207170394
ms.sourcegitcommit: caac7d098a448232304c9d6728e7340ec7517a71
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/16/2019
ms.locfileid: "58055546"
---
# <a name="accessdbprovidersample06"></a>AccessDBProviderSample06

Ez a példa bemutatja, hogyan tartalom módszerek támogatásához a hívásokat írja felül a `Clear-Content`, `Get-Content`, és `Set-Content` parancsmagok. Ezek a metódusok kell végrehajtani, amikor a felhasználó az adattárban lévő cikkek a tartalom kezelésére kell. Ebben a példában a szolgáltató osztálya származik a [System.Management.Automation.Provider.Navigationcmdletprovider](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider) osztály, és implementálja a [ System.Management.Automation.Provider.Icontentcmdletprovider](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider) felületet.

## <a name="demonstrates"></a>Bemutatók

> [!IMPORTANT]
> A szolgáltató osztálya nagy valószínűséggel célosztályából származik a következő osztályok egyike, és a valószínűleg az egyéb szolgáltató felületek megvalósításához:
>
> -   [System.Management.Automation.Provider.Itemcmdletprovider](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider) class. Lásd: [AccessDBProviderSample03](./accessdbprovidersample03.md).
> -   [System.Management.Automation.Provider.Containercmdletprovider](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider) class. Lásd: [AccessDBProviderSample04](./accessdbprovidersample04.md).
> -   [System.Management.Automation.Provider.Navigationcmdletprovider](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider) class.
>
> Melyik szolgáltató osztálya alapján a szolgáltató funkciói célosztályából származik, lásd: kiválasztásával kapcsolatban további információt [tervezése a Windows PowerShell-szolgáltatóban](./provider-types.md).

Ez a minta bemutatja a következőket:

- Deklaráló a `CmdletProvider` attribútum.

- A szolgáltató osztályt, amely a meghatározása a [System.Management.Automation.Provider.Navigationcmdletprovider](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider) deklarálja class, és hogy a [ System.Management.Automation.Provider.Icontentcmdletprovider](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider) felületet.

- Írja felül a [System.Management.Automation.Provider.Icontentcmdletprovider.Clearcontent*](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider.ClearContent) metódust változtathatja meg a `Clear-Content` parancsmagot, a felhasználó a tartalom eltávolítása egy elemet. (Ez a minta nem jeleníti meg a dinamikus paraméterek hozzáadása a `Clear-Content` parancsmagot.)

- Írja felül a [System.Management.Automation.Provider.Icontentcmdletprovider.Getcontentreader*](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider.GetContentReader) metódust változtathatja meg a `Get-Content` parancsmagot, lehetővé téve a felhasználó lekérni a tartalmat egy elem. (Ez a minta nem jeleníti meg a dinamikus paraméterek hozzáadása a `Get-Content` parancsmagot.).

- Írja felül a [Microsoft.PowerShell.Commands.Filesystemprovider.Getcontentwriter*](/dotnet/api/Microsoft.PowerShell.Commands.FileSystemProvider.GetContentWriter) metódust változtathatja meg a `Set-Content` parancsmagot, a felhasználók egy elem a tartalom frissítéséhez. (Ez a minta nem jeleníti meg a dinamikus paraméterek hozzáadása a `Set-Content` parancsmagot.)

## <a name="example"></a>Példa

Ez a példa bemutatja, hogyan felülírja a módszereket, törlése, beolvasása, és egy Microsoft Access-adatok cikkek tartalmának base beállítása szükséges.

[!code-csharp[AccessDBProviderSample06.cs](../../powershell-sdk-samples/SDK-2.0/csharp/AccessDBProviderSample06/AccessDBProviderSample06.cs#L11-L2399 "AccessDBProviderSample06.cs")]

## <a name="see-also"></a>Lásd még:

[System.Management.Automation.Provider.Itemcmdletprovider](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider)

[System.Management.Automation.Provider.Containercmdletprovider](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider)

[System.Management.Automation.Provider.Navigationcmdletprovider](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider)

[A Windows PowerShell-szolgáltató tervezése](./provider-types.md)