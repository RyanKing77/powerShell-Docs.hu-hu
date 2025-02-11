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
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62081021"
---
# <a name="accessdbprovidersample04"></a>AccessDBProviderSample04

Ez a példa bemutatja, hogyan tároló módszerek támogatásához a hívásokat írja felül a `Copy-Item`, `Get-ChildItem`, `New-Item`, és `Remove-Item` parancsmagok. Ezek a metódusok kell végrehajtani, ha az adattár tartalmaz, amelyek olyan tárolók elemek. A tároló egy olyan csoport gyermekelemek egy közös szülő elem alatt. Ebben a példában a szolgáltató osztálya származik a [System.Management.Automation.Provider.Containercmdletprovider](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider) osztály.

## <a name="demonstrates"></a>Azt ismerteti

> [!IMPORTANT]
> A szolgáltató osztálya nagy valószínűséggel lesz származtatva a [System.Management.Automation.Provider.Navigationcmdletprovider](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider)

Ez a minta bemutatja a következőket:

- Deklaráló a `CmdletProvider` attribútum.

- A szolgáltató osztályt, amely a meghatározása a [System.Management.Automation.Provider.Containercmdletprovider](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider) osztály.

- Írja felül a [System.Management.Automation.Provider.ContainerCmdletProvider.CopyItem](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.CopyItem) metódust változtathatja meg a `Copy-Item` parancsmag, mely lehetővé teszi, hogy a felhasználót, hogy elemek másolása egyik helyről egy másikra. (Ez a minta nem jeleníti meg a dinamikus paraméterek hozzáadása a `Copy-Item` parancsmagot.)

- Írja felül a [System.Management.Automation.Provider.Containercmdletprovider.Getchilditems*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.GetChildItems) változtathatja meg a Get-ChildItems parancsmagot, amely lehetővé teszi, hogy a fölérendelt elemtől bejárásához a lekérdezni kívánt felhasználó metódus . (Ez a minta nem jeleníti meg a dinamikus paraméterek hozzáadása a Get-ChildItems parancsmagot.)

- Írja felül a [System.Management.Automation.Provider.Containercmdletprovider.Getchildnames*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.GetChildNames) változtathatja meg a Get-ChildItems parancsmag metódus során a `Name` a parancsmag paraméter meg van adva.

- Írja felül a [System.Management.Automation.Provider.Containercmdletprovider.Newitem*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.NewItem) metódust változtathatja meg a `New-Item` parancsmagot, amely lehetővé teszi a felhasználó elemek hozzáadása az adattár. (Ez a minta nem jeleníti meg a dinamikus paraméterek hozzáadása a `New-Item` parancsmagot.)

- Írja felül a [System.Management.Automation.Provider.Containercmdletprovider.Removeitem*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.RemoveItem) metódust változtathatja meg a `Remove-Item` parancsmagot. (Ez a minta nem jeleníti meg a dinamikus paraméterek hozzáadása a `Remove-Item` parancsmagot.)

## <a name="example"></a>Példa

Ez a példa bemutatja, hogyan felülírja a szükséges másolni, hozzon létre, majd távolítsa el az elemeket, valamint a gyermek és egy szülő cikk elemeinek beolvasása közben módszerei módszereket.

[!code-csharp[AccessDBProviderSample04.cs](../../powershell-sdk-samples/SDK-2.0/csharp/AccessDBProviderSample06/AccessDBProviderSample06.cs#L11-L1635 "AccessDBProviderSample04.cs")]

## <a name="see-also"></a>Lásd még:

[System.Management.Automation.Provider.Itemcmdletprovider](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider)

[System.Management.Automation.Provider.Containercmdletprovider](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider)

[System.Management.Automation.Provider.Navigationcmdletprovider](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider)

[A Windows PowerShell-szolgáltató tervezése](./provider-types.md)