---
title: Szolgáltató parancsmagjai |} A Microsoft Docs
ms.custom: ''
ms.date: 09/12/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: d2465420-0970-4408-9ee5-260cf444cb67
caps.latest.revision: 8
ms.openlocfilehash: e6a0711cff6a550100f584fb64ae7f59f71a3cfb
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56845947"
---
# <a name="provider-cmdlets"></a>Szolgáltatói parancsmagok

A parancsmagok, amelyek a felhasználó futtathatja, kezelheti az adattár szolgáltató parancsmagjai nevezzük. Ezek a parancsmagok támogatják, írja felül az egyes módszerek határozzák meg az alap szolgáltató osztályok és kapcsolatok kell.

## <a name="provider-cmdlets"></a>Szolgáltató parancsmagjai

Az alábbiakban a szolgáltató parancsmagjai a által futtatható:

### <a name="psdrive-cmdlets"></a>PSDrive parancsmagok

- `Get-PSDrive`: Ez a parancsmag adja vissza, a Windows PowerShell-meghajtók az aktuális munkamenetben. Nem kell semmilyen metódus támogatja ezt a parancsmagot felülírása.

- `New-PSDrive`: Ez a parancsmag lehetővé teszi, hogy a felhasználó létrehozása a Windows PowerShell meghajtót az adattár eléréséhez. Ez a parancsmag támogatásához, felülírja a [System.Management.Automation.Provider.Drivecmdletprovider.Newdrive](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider.NewDrive) és [ System.Management.Automation.Provider.Drivecmdletprovider.Newdrivedynamicparameters](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider.NewDriveDynamicParameters) módszereket.

- `Remove-PSDrive`: Ez a parancsmag lehetővé teszi, hogy a felhasználót, hogy távolítsa el a Windows PowerShell-meghajtók, amely az adattár eléréséhez. Ez a parancsmag támogatásához, felülírja a [System.Management.Automation.Provider.Drivecmdletprovider.Removedrive](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider.RemoveDrive) metódust.

### <a name="item-cmdlets"></a>Item-parancsmagokkal

- `Clear-Item`: Ez a parancsmag lehetővé teszi, hogy a felhasználó eltávolítása egy elem értékét az adattárban. Ez a parancsmag támogatásához, felülírja a [System.Management.Automation.Provider.Itemcmdletprovider.Clearitem](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.ClearItem) és [ System.Management.Automation.Provider.Itemcmdletprovider.Clearitemdynamicparameters](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.ClearItemDynamicParameters) módszereket.

- `Copy-Item`: Ez a parancsmag lehetővé teszi, hogy a felhasználót, hogy az elem másolása egyik helyről egy másikra. Ez a parancsmag támogatásához, felülírja a [System.Management.Automation.Provider.Containercmdletprovider.Copyitem](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.CopyItem) és [ System.Management.Automation.Provider.Containercmdletprovider.Copyitemdynamicparameters](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.CopyItemDynamicParameters) módszereket.

- `Get-Item`: Ez a parancsmag lehetővé teszi, hogy a felhasználó be adatokat az adattárból. Ez a parancsmag támogatásához, felülírja a [System.Management.Automation.Provider.Itemcmdletprovider.Getitem](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.GetItem) és [System.Management.Automation.Provider.Itemcmdletprovider.Getitemdynamicparameters ](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.GetItemDynamicParameters) módszereket.

- `Get-ChildItem`: Ez a parancsmag lehetővé teszi, hogy a fölérendelt elemtől bejárásához a lekérdezni kívánt felhasználó. Ez a parancsmag támogatása érdekében írja felül a következő módszerek:

  - [System.Management.Automation.Provider.Containercmdletprovider.Getchilditems*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.GetChildItems)

  - [System.Management.Automation.Provider.Containercmdletprovider.Getchilditemsdynamicparameters*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.GetChildItemsDynamicParameters)

  - [System.Management.Automation.Provider.Containercmdletprovider.Getchildnames*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.GetChildNames)

  - [System.Management.Automation.Provider.Containercmdletprovider.Getchildnamesdynamicparameters*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.GetChildNamesDynamicParameters)

- `Invoke-Item`: Ez a parancsmag lehetővé teszi, hogy a felhasználó az elem által meghatározott alapértelmezett művelet végrehajtásához. Ez a parancsmag támogatásához, felülírja a [System.Management.Automation.Provider.Itemcmdletprovider.Invokedefaultaction](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.InvokeDefaultAction) és [ System.Management.Automation.Provider.Itemcmdletprovider.Invokedefaultaction](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.InvokeDefaultAction) módszereket.

- `Move-Item`: Ez a parancsmag lehetővé teszi, hogy a felhasználó az elem áthelyezése egyik helyről egy másik helyre. Ez a parancsmag támogatásához, felülírja a [System.Management.Automation.Provider.Navigationcmdletprovider.Moveitem](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.MoveItem) és [ System.Management.Automation.Provider.Navigationcmdletprovider.Moveitemdynamicparameters](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.MoveItemDynamicParameters)s módszereket.

- `New-ItemProperty`: Ez a parancsmag lehetővé teszi, hogy a felhasználó egy új elem létrehozására az adattárban.

- `Remove-Item`: Ez a parancsmag lehetővé teszi, hogy a felhasználót, hogy az adatokat az adattárból elemek eltávolítása. Ez a parancsmag támogatásához, felülírja a [System.Management.Automation.Provider.Containercmdletprovider.Removeitem](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.RemoveItem) és [ System.Management.Automation.Provider.Containercmdletprovider.Removeitemdynamicparameters](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.RemoveItemDynamicParameters) módszereket.

- `Rename-Item`: Ez a parancsmag lehetővé teszi, hogy a felhasználót, hogy nevezze át az adattár elemeit. Ez a parancsmag támogatásához, felülírja a [System.Management.Automation.Provider.Containercmdletprovider.Renameitem](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.RenameItem) és [ System.Management.Automation.Provider.Containercmdletprovider.Renameitemdynamicparameters](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.RenameItemDynamicParameters) módszereket.

- `Set-Item`: Ez a parancsmag lehetővé teszi, hogy a felhasználót, hogy frissítse a cikkek az adattárban. Ez a parancsmag támogatásához, felülírja a [System.Management.Automation.Provider.Itemcmdletprovider.Setitem](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.SetItem) és [System.Management.Automation.Provider.Itemcmdletprovider.Setitemdynamicparameters ](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.SetItemDynamicParameters) módszereket.

### <a name="item-content-cmdlets"></a>Item-parancsmagokkal

- `Add-Content`: Ez a parancsmag lehetővé teszi, hogy a tartalom hozzáadása egy elemet a felhasználó.

- `Clear-Content`: Ez a parancsmag lehetővé teszi, hogy a felhasználót, hogy törölje a tartalmat egy elemet a konfigurációelem törlése nélkül. Ez a parancsmag támogatásához, felülírja a [System.Management.Automation.Provider.Icontentcmdletprovider.Clearcontent](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider.ClearContent) és [ System.Management.Automation.Provider.Icontentcmdletprovider.Clearcontentdynamicparameters](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider.ClearContentDynamicParameters) módszereket.

- `Get-Content`: Ez a parancsmag lehetővé teszi, hogy a felhasználó lekérni a tartalmat egy elem. Ez a parancsmag támogatásához, felülírja a [System.Management.Automation.Provider.Icontentcmdletprovider.Getcontentreader](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider.GetContentReader) és [ System.Management.Automation.Provider.Icontentcmdletprovider.Getcontentreaderdynamicparameters](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider.GetContentReaderDynamicParameters) módszereket. A [System.Management.Automation.Provider.Icontentcmdletprovider.Getcontentreader*](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider.GetContentReader) metódus adja vissza egy [System.Management.Automation.Provider.Icontentreader](/dotnet/api/System.Management.Automation.Provider.IContentReader) , amely meghatározza a kapcsolat a metódusok a tartalmak olvasását.

- `Set-Content`: Ez a parancsmag lehetővé teszi, hogy a felhasználó frissítheti egy cikk tartalmát. Ez a parancsmag támogatásához, felülírja a [System.Management.Automation.Provider.Icontentcmdletprovider.Getcontentwriter](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider.GetContentWriter) és [ System.Management.Automation.Provider.Icontentcmdletprovider.Getcontentwriterdynamicparameters](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider.GetContentWriterDynamicParameters) módszereket. A [System.Management.Automation.Provider.Icontentcmdletprovider.Getcontentwriter*](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider.GetContentWriter) metódus adja vissza egy [System.Management.Automation.Provider.Icontentwriter](/dotnet/api/System.Management.Automation.Provider.IContentWriter) , amely meghatározza a kapcsolat a tartalmak írásához használt módszerek.

### <a name="item-property-cmdlets"></a>Vlastnost Item-parancsmagokkal

- `Clear-ItemProperty`: Ez a parancsmag lehetővé teszi, hogy a felhasználó törlése egy tulajdonság értéke. Ez a parancsmag támogatásához, felülírja a [System.Management.Automation.Provider.Ipropertycmdletprovider.Clearproperty](/dotnet/api/System.Management.Automation.Provider.IPropertyCmdletProvider.ClearProperty) és [ System.Management.Automation.Provider.Ipropertycmdletprovider.Clearpropertydynamicparameters](/dotnet/api/System.Management.Automation.Provider.IPropertyCmdletProvider.ClearPropertyDynamicParameters) módszereket.

- `Copy-ItemProperty`: Ez a parancsmag lehetővé teszi, hogy a felhasználó egy tulajdonságot, és annak értékét másolása egyik helyről egy másikra. Ez a parancsmag támogatásához, felülírja a [System.Management.Automation.Provider.Idynamicpropertycmdletprovider.Copyproperty](/dotnet/api/System.Management.Automation.Provider.IDynamicPropertyCmdletProvider.CopyProperty) és [ System.Management.Automation.Provider.Idynamicpropertycmdletprovider.Copypropertydynamicparameters](/dotnet/api/System.Management.Automation.Provider.IDynamicPropertyCmdletProvider.CopyPropertyDynamicParameters) módszereket.

- `Get-ItemProperty`: Ez a parancsmag egy elem tulajdonságait olvassa be. Ez a parancsmag támogatásához, felülírja a [System.Management.Automation.Provider.Ipropertycmdletprovider.Getproperty](/dotnet/api/System.Management.Automation.Provider.IPropertyCmdletProvider.GetProperty) és [ System.Management.Automation.Provider.Ipropertycmdletprovider.Getpropertydynamicparameters](/dotnet/api/System.Management.Automation.Provider.IPropertyCmdletProvider.GetPropertyDynamicParameters) módszereket.

- `Move-ItemProperty`: Ez a parancsmag lehetővé teszi, hogy a felhasználót, hogy egy tulajdonságot, és annak értékét áthelyezése egyik helyről egy másikra. Ez a parancsmag támogatásához, felülírja a [System.Management.Automation.Provider.Idynamicpropertycmdletprovider.Moveproperty](/dotnet/api/System.Management.Automation.Provider.IDynamicPropertyCmdletProvider.MoveProperty) és [ System.Management.Automation.Provider.Idynamicpropertycmdletprovider.Movepropertydynamicparameters](/dotnet/api/System.Management.Automation.Provider.IDynamicPropertyCmdletProvider.MovePropertyDynamicParameters) módszereket.

- `New-ItemProperty`: Ez a parancsmag lehetővé teszi, hogy a felhasználó számára hozzon létre egy új tulajdonságot, és állítsa az értékét. Ez a parancsmag támogatásához, felülírja a [System.Management.Automation.Provider.Idynamicpropertycmdletprovider.Newproperty](/dotnet/api/System.Management.Automation.Provider.IDynamicPropertyCmdletProvider.NewProperty) és [ System.Management.Automation.Provider.Idynamicpropertycmdletprovider.Newpropertydynamicparameters](/dotnet/api/System.Management.Automation.Provider.IDynamicPropertyCmdletProvider.NewPropertyDynamicParameters) módszereket.

- `Remove-ItemProperty`: Ez a parancsmag lehetővé teszi, hogy a felhasználót, hogy törölni egy tulajdonságot, és annak értékét. Ez a parancsmag támogatásához, felülírja a [System.Management.Automation.Provider.Idynamicpropertycmdletprovider.Removeproperty](/dotnet/api/System.Management.Automation.Provider.IDynamicPropertyCmdletProvider.RemoveProperty) és [ System.Management.Automation.Provider.Idynamicpropertycmdletprovider.Removepropertydynamicparameters](/dotnet/api/System.Management.Automation.Provider.IDynamicPropertyCmdletProvider.RemovePropertyDynamicParameters) módszereket.

- `Rename-ItemProperty`: Ez a parancsmag lehetővé teszi, hogy a felhasználó módosíthatja a tulajdonság nevét. Ez a parancsmag támogatásához, felülírja a [System.Management.Automation.Provider.Idynamicpropertycmdletprovider.Renameproperty](/dotnet/api/System.Management.Automation.Provider.IDynamicPropertyCmdletProvider.RenameProperty) és [ System.Management.Automation.Provider.Idynamicpropertycmdletprovider.Renamepropertydynamicparameters](/dotnet/api/System.Management.Automation.Provider.IDynamicPropertyCmdletProvider.RenamePropertyDynamicParameters) módszereket.

- `Set-ItemProperty`: Ez a parancsmag lehetővé teszi, hogy a felhasználót, hogy egy elem tulajdonságainak frissítéséhez. Ez a parancsmag támogatásához, felülírja a [System.Management.Automation.Provider.Ipropertycmdletprovider.Setproperty](/dotnet/api/System.Management.Automation.Provider.IPropertyCmdletProvider.SetProperty) és [ System.Management.Automation.Provider.Ipropertycmdletprovider.Setpropertydynamicparameters](/dotnet/api/System.Management.Automation.Provider.IPropertyCmdletProvider.SetPropertyDynamicParameters) módszereket.

### <a name="location-cmdlets"></a>Hely-parancsmagok

- `Get-Location`: A jelenlegi működő hely adatait kérdezi le. Nem kell semmilyen metódus támogatja ezt a parancsmagot felülírása.

- `Pop-Location`: Ez a parancsmag a legutóbb leküldve a veremben helyen az aktuális hely változik. Nem kell semmilyen metódus támogatja ezt a parancsmagot felülírása.

- `Push-Location`: Ez a parancsmag hozzáadja az aktuális hely felső részén (a "verem") helyek listáját. Nem kell semmilyen metódus támogatja ezt a parancsmagot felülírása.

- `Set-Location`: Ez a parancsmag az aktuális működő helye egy adott helyre állítja be. Nem kell semmilyen metódus támogatja ezt a parancsmagot felülírása.

### <a name="path-cmdlets"></a>Elérési út parancsmagok

- `Join-Path`: Ez a parancsmag lehetővé teszi, hogy a felhasználó úgy, hogy a szülő és gyermek részleges útvonalat provider – belső elérési utat hoz létre. Ez a parancsmag támogatásához, felülírja a [System.Management.Automation.Provider.Navigationcmdletprovider.Makepath](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.MakePath) metódust.

- `Convert-Path`: Ez a parancsmag egy Windows PowerShell útvonalról elérési alakítja egy Windows PowerShell szolgáltató elérési útjával.

- `Split-Path`: A megadott elérési utat részét adja vissza.

- `Resolve-Path`: Oldja fel a helyettesítő karakterek az elérési utat, és az elérési út tartalmát jeleníti meg.

- `Test-Path`: Ez a parancsmag határozza meg, hogy létezik-e minden eleme egy elérési utat. Ez a parancsmag támogatásához, felülírja a [System.Management.Automation.Provider.Itemcmdletprovider.Itemexists](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.ItemExists) és [ System.Management.Automation.Provider.Itemcmdletprovider.Itemexistsdynamicparameters](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.ItemExistsDynamicParameters) módszereket.

### <a name="psprovider-cmdlets"></a>PSProvider parancsmagok

- `Get-PSProvider`: Ez a parancsmag a szolgáltatók elérhetők a munkamenetben kapcsolatos információkat ad vissza. Nem kell semmilyen metódus támogatja ezt a parancsmagot felülírása.