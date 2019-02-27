---
title: Szolgáltató minták |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: c4933dad-fec9-4337-a1a9-9dc16ee87cc3
caps.latest.revision: 9
ms.openlocfilehash: 1e7aeb5bcb6bd5a2845648c3327e2245e6c428ba
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56844799"
---
# <a name="provider-samples"></a>Szolgáltatói minták

Ez a szakasz tartalmazza a minta-szolgáltató, amely egy Microsoft Access-adatbázis eléréséhez. Ezek a minták alap szolgáltató osztályokat származtatást szolgáltató osztályokat tartalmazza.

## <a name="in-this-section"></a>A szakasz tartalma

Ez a témakör az alábbi részekből áll:

[AccessDBProviderSample01 minta](./accessdbprovidersample01.md) Ez a példa bemutatja, hogyan deklarálja a szolgáltató osztályt, amely közvetlenül a [System.Management.Automation.Provider.Cmdletprovider](/dotnet/api/System.Management.Automation.Provider.CmdletProvider) osztály. Része Itt csak a teljesség.

[AccessDBProviderSample02](./accessdbprovidersample02.md) Ez a példa bemutatja, hogyan felülírja a [System.Management.Automation.Provider.Drivecmdletprovider.Newdrive*](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider.NewDrive) és [ System.Management.Automation.Provider.Drivecmdletprovider.Removedrive*](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider.RemoveDrive) módszereket támogatja a hívást a `New-PSDrive` és `Remove-PSDrive` parancsmagok. Ebben a példában a szolgáltató osztálya származik a [System.Management.Automation.Provider.Drivecmdletprovider](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider) osztály.

[AccessDBProviderSample03](./accessdbprovidersample03.md) Ez a példa bemutatja, hogyan felülírja a [System.Management.Automation.Provider.Itemcmdletprovider.Getitem*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.GetItem) és [ System.Management.Automation.Provider.Itemcmdletprovider.Setitem*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.SetItem) módszereket támogatja a hívást a `Get-Item` és `Set-Item` parancsmagok. Ebben a példában a szolgáltató osztálya származik a [System.Management.Automation.Provider.Itemcmdletprovider](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider) osztály.

[AccessDBProviderSample04](./accessdbprovidersample04.md) Ez a példa bemutatja, hogyan tároló módszerek támogatásához a hívásokat írja felül a `Copy-Item`, `Get-ChildItem`, `New-Item`, és `Remove-Item` parancsmagok. Ezek a metódusok kell végrehajtani, ha az adattár tartalmaz, amelyek olyan tárolók elemek. A tároló egy olyan csoport gyermekelemek egy közös szülő elem alatt. Ebben a példában a szolgáltató osztálya származik a [System.Management.Automation.Provider.Containercmdletprovider](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider) osztály.

[AccessDBProviderSample05](./accessdbprovidersample05.md) Ez a példa bemutatja, hogyan tároló módszerek támogatásához a hívásokat írja felül a `Move-Item` és `Join-Path` parancsmagok. Ezek a metódusok kell végrehajtani, amikor a felhasználónak szüksége van a tárolóban lévő elemek áthelyezése, és ha az adattár tartalmaz beágyazott tárolók. Ebben a példában a szolgáltató osztálya származik a [System.Management.Automation.Provider.Navigationcmdletprovider](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider) osztály.

[AccessDBProviderSample06](./accessdbprovidersample06.md) Ez a példa bemutatja, hogyan tartalom módszerek támogatásához a hívásokat írja felül a `Clear-Content`, `Get-Content`, és `Set-Content` parancsmagok. Ezek a metódusok kell végrehajtani, amikor a felhasználó az adattárban lévő cikkek a tartalom kezelésére kell. Ebben a példában a szolgáltató osztálya származik a [System.Management.Automation.Provider.Navigationcmdletprovider](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider) osztály, és implementálja a [ System.Management.Automation.Provider.Icontentcmdletprovider](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider) felületet.

## <a name="see-also"></a>Lásd még:

[A Windows PowerShell-szolgáltató írása](./writing-a-windows-powershell-provider.md)