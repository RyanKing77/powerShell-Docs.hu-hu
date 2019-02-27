---
title: Szolgáltató parancsmag-paraméterek |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: b3d09eaa-924f-4e2b-adfb-14bb729090dd
caps.latest.revision: 8
ms.openlocfilehash: d0fb81ee1ca1f80e216c021e1bd64771b8de4dc3
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56849692"
---
# <a name="provider-cmdlet-parameters"></a>Szolgáltatói parancsmag-paraméterek

Szolgáltató parancsmagjai a statikus paramétereket, amelyek támogatják a parancsmag minden szolgáltató számára elérhető, amikor a felhasználó adja meg a megadott érték bizonyos statikus paraméterek a szolgáltatói parancsmag adott, valamint a dinamikus paraméterek készletét kapható.

## <a name="provider-cmdlet-static-parameters"></a>Szolgáltató statikus parancsmag-paraméterek

Statikus paraméterek vannak meghatározva a Windows PowerShell. Ezek a paraméterek rengeteg konzisztencia biztosítson minden szolgáltató között, valamint egyszerűbb fejlesztési élmény érdekében a Windows PowerShell valósul meg. Ezek a paraméterek közé tartoznak a `literalPath`, `exclude`, és `include` paramétereit a `Get-Item` parancsmagot. Ezeket a paramétereket a kisebb sorozatát felülírható legyen a szolgáltató specifikus műveleteket biztosít. Ezek a paraméterek közé tartoznak a `Path` és `Value` paraméterében a `Set-Item` parancsmagot. Itt az, hogy felülírható legyen a szolgáltató parancsmagjai a paraméterek listája.

`Clear-Content` meghatározhatja, hogyan fogja használni a provider átadott értékek parancsmag a `Path` paraméterében a `Clear-Content` parancsmag alkalmazásával a [System.Management.Automation.Provider.Icontentcmdletprovider.Clearcontent*](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider.ClearContent)metódust.

`Clear-Item` meghatározhatja, hogyan fogja használni a provider átadott értékek parancsmag a `Path` paraméterében a `Clear-Item` parancsmag alkalmazásával a [System.Management.Automation.Provider.Itemcmdletprovider.Clearitem*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.ClearItem) a metódus.

`Clear-ItemProperty` meghatározhatja, hogyan fogja használni a provider átadott értékek parancsmag a `Path` és `Name` paramétereit a `Clear-ItemProperty` parancsmag alkalmazásával a [ System.Management.Automation.Provider.Ipropertycmdletprovider.Clearproperty*](/dotnet/api/System.Management.Automation.Provider.IPropertyCmdletProvider.ClearProperty) metódust.

`Copy-Item` meghatározhatja, hogyan fogja használni a provider átadott értékek parancsmag a `Path`, `Destination`, és `Recurse` paramétereit a `Copy-Item` parancsmag alkalmazásával a [ System.Management.Automation.Provider.Containercmdletprovider.Copyitem*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.CopyItem) metódust.

Get-ChildItems parancsmag meghatározhatja, hogyan fogja használni a provider átadott értékek a `Path` és `Recures` paramétereit a `Get-ChildItem` parancsmag alkalmazásával a [ System.Management.Automation.Provider.Containercmdletprovider.Getchilditems*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.GetChildItems) és [System.Management.Automation.Provider.Containercmdletprovider.Getchildnames*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.GetChildNames) módszereket.

`Get-Content` meghatározhatja, hogyan fogja használni a provider átadott értékek parancsmag a `Path` paraméterében a `Get-Content` parancsmag alkalmazásával a [System.Management.Automation.Provider.Icontentcmdletprovider.Getcontentreader*](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider.GetContentReader) metódust.

`Get-Item` meghatározhatja, hogyan fogja használni a provider átadott értékek parancsmag a `Path` paraméterében a `Get-Item` parancsmag alkalmazásával a [System.Management.Automation.Provider.Itemcmdletprovider.Getitem*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.GetItem) metódust.

`Get-ItemProperty` meghatározhatja, hogyan fogja használni a provider átadott értékek parancsmag a `Path` és `Name` paramétereit a `Get-ItemProperty` parancsmag alkalmazásával a [ System.Management.Automation.Provider.Ipropertycmdletprovider.Getproperty*](/dotnet/api/System.Management.Automation.Provider.IPropertyCmdletProvider.GetProperty) metódust.

`Invoke-Item` meghatározhatja, hogyan fogja használni a provider átadott értékek parancsmag a `Path` paraméterében a `Invoke-Item` parancsmag alkalmazásával a [System.Management.Automation.Provider.Itemcmdletprovider.Invokedefaultaction*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.InvokeDefaultAction)metódust.

`Move-Item` meghatározhatja, hogyan fogja használni a provider átadott értékek parancsmag a `Path` és `Destination` paramétereit a `Move-Item` parancsmag alkalmazásával a [ System.Management.Automation.Provider.Navigationcmdletprovider.Moveitem*](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.MoveItem) metódust.

`New-Item` meghatározhatja, hogyan fogja használni a provider átadott értékek parancsmag a `Path`, `ItemType`, és `Value` paramétereit a `New-Item` parancsmag alkalmazásával a [ System.Management.Automation.Provider.Containercmdletprovider.Newitem*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.NewItem) metódust.

`New-ItemProperty` meghatározhatja, hogyan fogja használni a provider átadott értékek parancsmag a `Path`, `Name`, `PropertyType`, és `Value` paramétereit a `New-ItemProperty` parancsmag alkalmazásával a [ Microsoft.Powershell.Commands.Registryprovider.Newproperty*](/dotnet/api/Microsoft.PowerShell.Commands.RegistryProvider.NewProperty) metódust.

`Remove-Item` Meghatározhatja, hogyan fogja használni a provider átadott értékek a `Path` és `Recurse` paramétereit a `Remove-Item` parancsmag alkalmazásával a [System.Management.Automation.Provider.Containercmdletprovider.Removeitem* ](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.RemoveItem) metódust.

`Remove-ItemProperty` Meghatározhatja, hogyan fogja használni a provider átadott értékek a `Path` és `Name` paramétereit a `Remove-ItemProperty` parancsmag alkalmazásával a [ System.Management.Automation.Provider.Idynamicpropertycmdletprovider.Removeproperty*](/dotnet/api/System.Management.Automation.Provider.IDynamicPropertyCmdletProvider.RemoveProperty) metódust.

`Rename-Item` meghatározhatja, hogyan fogja használni a provider átadott értékek parancsmag a `Path` és `NewName` paramétereit a `Rename-Item` parancsmag alkalmazásával a [ System.Management.Automation.Provider.Containercmdletprovider.Renameitem*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.RenameItem) metódust.

`Rename-ItemProperty` Meghatározhatja, hogyan fogja használni a provider átadott értékek a `Path`, `NewName`, és `Name` paramétereit a `Rename-ItemProperty` parancsmag alkalmazásával a [ System.Management.Automation.Provider.Idynamicpropertycmdletprovider.Renameproperty*](/dotnet/api/System.Management.Automation.Provider.IDynamicPropertyCmdletProvider.RenameProperty) metódust.

`Set-Content` meghatározhatja, hogyan fogja használni a provider átadott értékek parancsmag a `Path` paraméterében a `Set-Content` parancsmag alkalmazásával a [System.Management.Automation.Provider.Icontentcmdletprovider.Getcontentwriter*](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider.GetContentWriter) metódust.

`Set-Item` meghatározhatja, hogyan fogja használni a provider átadott értékek parancsmag a `Path` és `Value` paramétereit a `Set-Item` parancsmag alkalmazásával a [System.Management.Automation.Provider.Itemcmdletprovider.Setitem* ](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.SetItem) metódust.

`Set-ItemProperty` meghatározhatja, hogyan fogja használni a provider átadott értékek parancsmag a `Path` és `Value` paramétereit a `Set-Item` parancsmag alkalmazásával a [ System.Management.Automation.Provider.Ipropertycmdletprovider.Setproperty*](/dotnet/api/System.Management.Automation.Provider.IPropertyCmdletProvider.SetProperty) metódust.

`Test-Path` meghatározhatja, hogyan fogja használni a provider átadott értékek parancsmag a `Path` paraméterében a `Test-Path` parancsmag alkalmazásával a [System.Management.Automation.Provider.Itemcmdletprovider.Invokedefaultaction*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.InvokeDefaultAction)metódust.

Emellett nem adható meg ezeket a paramétereket, például a csatlakoznak-e opcionális vagy szükséges, jellemzőit és nem is, küldje el ezeket a paramétereket egy aliast, vagy adja meg a érvényesítési attribútumokat. Ezzel szemben a megadható paraméter jellemzők önálló parancsmagok attribútumok használatával a `Parameters` attribútum.

## <a name="provider-cmdlet-dynamic-parameters"></a>Szolgáltató parancsmag dinamikus paraméterek

A parancsmag szolgáltatók dinamikus paraméterek önálló parancsmagok dinamikus szolgáltatók hasonlóak. Mindkét esetben a paramétereket a parancsmagot, amikor a felhasználó adja meg egy adott értéket az egyik az alapértelmezett paraméterek, például a `path` paraméter. Azonban nem az összes statikus paraméterek segítségével dinamikus paraméterek hozzáadásával aktiválása. Dinamikus paraméterekkel kapcsolatos további információkért lásd: [szolgáltató parancsmag dinamikus paraméterek](./provider-cmdlet-dynamic-parameters.md).

## <a name="see-also"></a>Lásd még:

[Szolgáltató parancsmag dinamikus paraméterek](./provider-cmdlet-dynamic-parameters.md)

[A Windows PowerShell-szolgáltató írása](./writing-a-windows-powershell-provider.md)