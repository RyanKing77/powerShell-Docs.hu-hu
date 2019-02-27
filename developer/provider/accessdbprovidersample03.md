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
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56849195"
---
# <a name="accessdbprovidersample03"></a>AccessDBProviderSample03

Ez a példa bemutatja, hogyan felülírja a [System.Management.Automation.Provider.Itemcmdletprovider.Getitem*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.GetItem) és [System.Management.Automation.Provider.Itemcmdletprovider.Setitem*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.SetItem) módszereket támogatja a hívást a `Get-Item` és `Set-Item` parancsmagok. Ebben a példában a szolgáltató osztálya származik a [System.Management.Automation.Provider.Itemcmdletprovider](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider) osztály.

## <a name="demonstrates"></a>Bemutatók

> [!IMPORTANT]
> A szolgáltató osztálya nagy valószínűséggel célosztályából származik a következő osztályok egyike, és a valószínűleg az egyéb szolgáltató felületek megvalósításához:
>
> -   [System.Management.Automation.Provider.Itemcmdletprovider](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider) class.
> -   [System.Management.Automation.Provider.Containercmdletprovider](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider) class. Lásd: [AccessDBProviderSample04](./accessdbprovidersample04.md).
> -   [System.Management.Automation.Provider.Navigationcmdletprovider](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider) class. Lásd: [AccessDBProviderSample05](./accessdbprovidersample05.md).
>
> Melyik szolgáltató osztálya alapján a szolgáltató funkciói célosztályából származik, lásd: kiválasztásával kapcsolatban további információt [tervezése a Windows PowerShell-szolgáltatóban](./provider-types.md).

Ez a minta bemutatja a következőket:

- Deklaráló a `CmdletProvider` attribútum.

- A szolgáltató osztályt, amely a meghatározása a [System.Management.Automation.Provider.Itemcmdletprovider](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider) osztály.

- Írja felül a [System.Management.Automation.Provider.Drivecmdletprovider.Newdrive*](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider.NewDrive) metódust változtathatja meg a `New-PSDrive` parancsmagot, a felhasználó létrehozása az új meghajtókat. (Ez a minta nem jeleníti meg a dinamikus paraméterek hozzáadása a `New-PSDrive` parancsmagot.)

- Írja felül a [System.Management.Automation.Provider.Drivecmdletprovider.Removedrive*](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider.RemoveDrive) módszer eltávolítja a meglévő meghajtók támogatásához.

- Írja felül a [System.Management.Automation.Provider.Itemcmdletprovider.Getitem*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.GetItem) metódust változtathatja meg a `Get-Item` parancsmagot, lehetővé téve a felhasználó az elemek lekéréséhez az adatokat az adattárból. (Ez a minta nem jeleníti meg a dinamikus paraméterek hozzáadása a `Get-Item` parancsmagot.)

- Írja felül a [System.Management.Automation.Provider.Itemcmdletprovider.Setitem*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.SetItem) metódust változtathatja meg a `Set-Item` parancsmagot, a felhasználók a cikkek az adattárban frissíteni. (Ez a minta nem jeleníti meg a dinamikus paraméterek hozzáadása a `Get-Item` parancsmagot.)

- Írja felül a [System.Management.Automation.Provider.Itemcmdletprovider.Itemexists*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.ItemExists) metódust változtathatja meg a `Test-Path` parancsmagot. (Ez a minta nem jeleníti meg a dinamikus paraméterek hozzáadása a `Test-Path` parancsmagot.)

- Írja felül a [System.Management.Automation.Provider.Itemcmdletprovider.Isvalidpath*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.IsValidPath) módszer annak megállapításához, hogy a megadott elérési út érvényes.

## <a name="example"></a>Példa

Ez a példa bemutatja, hogyan felülírja a lekéréséhez és a egy Microsoft Access-adatok elemek alap beállításához szükséges módszereket.

[!code-csharp[AccessDBProviderSample03.cs](../../powershell-sdk-samples/SDK-2.0/csharp/AccessDBProviderSample06/AccessDBProviderSample06.cs#L11-L976 "AccessDBProviderSample03.cs")]

## <a name="see-also"></a>Lásd még:

[System.Management.Automation.Provider.Itemcmdletprovider](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider)

[System.Management.Automation.Provider.Containercmdletprovider](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider)

[System.Management.Automation.Provider.Navigationcmdletprovider](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider)

[A Windows PowerShell-szolgáltató tervezése](./provider-types.md)