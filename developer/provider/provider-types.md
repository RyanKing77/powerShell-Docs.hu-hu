---
title: Szolgáltatótípus |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: e523a8e1-42e4-4633-887f-fb74b3464561
caps.latest.revision: 12
ms.openlocfilehash: 25b604621c90f1aa88bc1eea365e47db66e98c3d
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56848495"
---
# <a name="provider-types"></a>Szolgáltatótípusok

Szolgáltatók azok alapvető funkciókat, a (Windows PowerShell által rendelkezésre bocsátott) szolgáltatói parancsmagok hogyan hajthat végre a műveleteket módosításával határozza meg. Például szolgáltatók alapértelmezett funkciójának használatához a `Get-Item` parancsmagot, vagy megváltoztathatja, hogyan működnek a parancsmagot, az adatokat az adattárból elemek beolvasása közben. A szolgáltatói funkciót ebben a témakörben ismertetett módszerek az adott szolgáltató alaposztályok és kapcsolódási felülírásával meghatározott funkciókat tartalmaz.

> [!NOTE]
> Szolgáltató funkciói Windows PowerShell által előre meghatározott, lásd: [szolgáltató képességei](http://msdn.microsoft.com/en-us/864e4807-554a-4016-80ea-bf643a090fc6).

## <a name="drive-enabled-providers"></a>Meghajtó engedélyezve szolgáltatók

Meghajtó engedélyezve szolgáltatók adja meg a felhasználó számára elérhető alapértelmezett meghajtókat, és engedélyezi a felhasználó hozzáadása vagy eltávolítása a meghajtók. A legtöbb esetben szolgáltatók meghajtó engedélyezett szolgáltatók azért, mert az adattár eléréséhez néhány alapértelmezett meghajtón van szükségük. Azonban a saját szolgáltató írás esetén előfordulhat, hogy vagy nem biztos, hogy a felhasználó létrehozásához, és távolítsa el a meghajtókat.

Meghajtó engedélyezve szolgáltató létrehozásához a szolgáltató osztályból kell származnia a [System.Management.Automation.Provider.Drivecmdletprovider](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider) vagy egy másik osztály, amely az adott osztályból származik. A [System.Management.Automation.Provider.Drivecmdletprovider](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider) osztály határozza meg a következő módszerek az alapértelmezett meghajtókat a szolgáltató és támogatásáért a `New-PSDrive` és `Remove-PSDrive` parancsmagok. A legtöbb esetben egy szolgáltató parancsmag támogatja, felül kell írnia a módszert, amelyet a Windows PowerShell meghívja a parancsmag meghívni például a `NewDrive` módszer a `New-PSDrive` parancsmagot, és opcionálisan egy második módszer, például felülírhatja`NewDriveDynamicParameters`, a dinamikus paraméterek hozzáadása a parancsmaghoz.

- A [System.Management.Automation.Provider.Drivecmdletprovider.Initializedefaultdrives*](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider.InitializeDefaultDrives) metódus határozza meg az alapértelmezett meghajtókat, amelyek a felhasználó számára elérhető, amikor a szolgáltató van használatban.

- A [System.Management.Automation.Provider.Drivecmdletprovider.Newdrive*](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider.NewDrive) és [System.Management.Automation.Provider.Drivecmdletprovider.Newdrivedynamicparameters*](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider.NewDriveDynamicParameters) módszerek Meghatározza, hogy a szolgáltató támogatja-e a `New-PSDrive` szolgáltató parancsmagot. Ez a parancsmag lehetővé teszi a felhasználóknak az adattár elérése.

- A [System.Management.Automation.Provider.Drivecmdletprovider.Removedrive*](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider.RemoveDrive) metódus határozza meg, hogy a szolgáltató támogatja-e a `Remove-PSDrive` szolgáltató parancsmagot. Ez a parancsmag lehetővé teszi, hogy a felhasználót, hogy a meghajtók eltávolítja az adatokat az adattárból.

## <a name="item-enabled-providers"></a>Elem engedélyezett szolgáltatók

Elem engedélyezett szolgáltatók engedélyezése a felhasználó lekérése, állítsa be vagy törölje az adattárban. Egy "elem" az adattár, amely a felhasználó érheti el és egymástól függetlenül kezelheti a eleme. Egy elem engedélyezett szolgáltató létrehozásához, a szolgáltató osztályból kell származnia a [System.Management.Automation.Provider.Itemcmdletprovider](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider) vagy egy másik osztály, amely az adott osztályból származik.

A [System.Management.Automation.Provider.Itemcmdletprovider](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider) osztály határozza meg az alábbi módszerek megvalósításának adott szolgáltató parancsmagjai. A legtöbb esetben egy szolgáltató parancsmag támogatja, felül kell írnia a módszert, amelyet a Windows PowerShell meghívja a parancsmag meghívni például a `ClearItem` módszer a `Clear-Item` parancsmagot, és opcionálisan egy második módszer, például felülírhatja`ClearItemDynamicParameters`, a dinamikus paraméterek hozzáadása a parancsmaghoz.

- A [System.Management.Automation.Provider.Itemcmdletprovider.Clearitem*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.ClearItem) és [System.Management.Automation.Provider.Itemcmdletprovider.Clearitemdynamicparameters*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.ClearItemDynamicParameters) módszerek határozza meg, hogy a szolgáltató támogatja-e a `Clear-Item` szolgáltató parancsmagot. Ez a parancsmag lehetővé teszi, hogy a felhasználó eltávolítja az érték egy elem szerepel az adattárban.

- A [System.Management.Automation.Provider.Itemcmdletprovider.Getitem*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.GetItem) és [System.Management.Automation.Provider.Itemcmdletprovider.Getitemdynamicparameters*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.GetItemDynamicParameters) módszerek meghatározása hogyan a szolgáltató támogatja a `Get-Item` szolgáltató parancsmagot. Ez a parancsmag lehetővé teszi, hogy a felhasználó be adatokat az adattárból.

- A [System.Management.Automation.Provider.Itemcmdletprovider.Setitem*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.SetItem) és [System.Management.Automation.Provider.Itemcmdletprovider.Setitemdynamicparameters*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.SetItemDynamicParameters) módszerek meghatározása hogyan a szolgáltató támogatja a `Set-Item` szolgáltató parancsmagot. Ez a parancsmag lehetővé teszi, hogy a felhasználót, hogy frissítse a cikkek az adattárban.

- A [System.Management.Automation.Provider.Itemcmdletprovider.Invokedefaultaction*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.InvokeDefaultAction) és [System.Management.Automation.Provider.Itemcmdletprovider.Invokedefaultaction*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.InvokeDefaultAction) módszerek határozza meg, hogy a szolgáltató támogatja-e a `Invoke-Item` szolgáltató parancsmagot. Ez a parancsmag lehetővé teszi, hogy a felhasználó az elem által meghatározott alapértelmezett művelet végrehajtásához.

- A [System.Management.Automation.Provider.Itemcmdletprovider.Itemexists*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.ItemExists) és [System.Management.Automation.Provider.Itemcmdletprovider.Itemexistsdynamicparameters*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.ItemExistsDynamicParameters) módszerek határozza meg, hogy a szolgáltató támogatja-e a `Test-Path` szolgáltató parancsmagot. Ez a parancsmag lehetővé teszi, hogy a felhasználó határozza meg, ha létezik-e a görbe összes elemét.

  A szolgáltató parancsmagok végrehajtásához használt módszerek mellett a [System.Management.Automation.Provider.Itemcmdletprovider](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider) osztály is határozza meg az alábbi módszerek:

- A [System.Management.Automation.Provider.Itemcmdletprovider.Expandpath*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.ExpandPath) módszer lehetővé teszi, hogy a felhasználó helyettesítő karaktereket használja, amikor a szolgáltató elérési útjának.

- A [System.Management.Automation.Provider.Itemcmdletprovider.Isvalidpath*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.IsValidPath) határozza meg, ha egy elérési út szintaktikailag és szemantikailag érvényes a szolgáltató.

## <a name="container-enabled-providers"></a>Tároló-kompatibilis szolgáltatók

Tároló-kompatibilis szolgáltatók engedélyezése a felhasználó számára, amelyek olyan tárolók elemek kezelése. A tároló egy olyan csoport gyermekelemek egy közös szülő elem alatt. Tároló-kompatibilis szolgáltató létrehozásához a szolgáltató osztályból kell származnia a [System.Management.Automation.Provider.Containercmdletprovider](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider) vagy egy másik osztály, amely az adott osztályból származik.

> [!IMPORTANT]
> Tároló-kompatibilis szolgáltatók nem fér hozzá a beágyazott tárolókat tartalmazó adattárakban. Ha egy adott tároló gyermekelem egy másik tárolóba, meg kell valósítani egy navigációs-kompatibilis szolgáltatót.

A [System.Management.Automation.Provider.Containercmdletprovider](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider) osztály határozza meg az alábbi módszerek megvalósításának adott szolgáltató parancsmagjai. A legtöbb esetben egy szolgáltató parancsmag támogatja, felül kell írnia a módszert, amelyet a Windows PowerShell meghívja a parancsmag meghívni például a `CopyItem` módszer a `Copy-Item` parancsmagot, és opcionálisan egy második módszer, például felülírhatja`CopyItemDynamicParameters`, a dinamikus paraméterek hozzáadása a parancsmaghoz.

- A [System.Management.Automation.Provider.Containercmdletprovider.Copyitem*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.CopyItem) és [System.Management.Automation.Provider.Containercmdletprovider.Copyitemdynamicparameters*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.CopyItemDynamicParameters) módszerek határozza meg, hogy a szolgáltató támogatja-e a `Copy-Item` szolgáltató parancsmagot. Ez a parancsmag lehetővé teszi, hogy a felhasználót, hogy az elem másolása egyik helyről egy másikra.

- A [System.Management.Automation.Provider.Containercmdletprovider.Getchilditems*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.GetChildItems) és [System.Management.Automation.Provider.Containercmdletprovider.Getchilditemsdynamicparameters*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.GetChildItemsDynamicParameters) módszerek határozza meg, hogy a szolgáltató támogatja-e a `Get-ChildItem` szolgáltató parancsmagot. Ez a parancsmag lehetővé teszi, hogy a fölérendelt elemtől bejárásához a lekérdezni kívánt felhasználó.

- A [System.Management.Automation.Provider.Containercmdletprovider.Getchildnames*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.GetChildNames) és [System.Management.Automation.Provider.Containercmdletprovider.Getchildnamesdynamicparameters*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.GetChildNamesDynamicParameters) módszerek határozza meg, hogy a szolgáltató támogatja-e a `Get-ChildItem` szolgáltató parancsmag ha annak `Name` paraméter meg van adva.

- A [System.Management.Automation.Provider.Containercmdletprovider.Newitem*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.NewItem) és [System.Management.Automation.Provider.Containercmdletprovider.Newitemdynamicparameters*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.NewItemDynamicParameters) módszerek határozza meg, hogy a szolgáltató támogatja-e a `New-Item` szolgáltató parancsmagot. Ez a parancsmag lehetővé teszi a felhasználóknak új elemek az adattárban.

- A [System.Management.Automation.Provider.Containercmdletprovider.Removeitem*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.RemoveItem) és [System.Management.Automation.Provider.Containercmdletprovider.Removeitemdynamicparameters*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.RemoveItemDynamicParameters) módszerek határozza meg, hogy a szolgáltató támogatja-e a `Remove-Item` szolgáltató parancsmagot. Ez a parancsmag lehetővé teszi, hogy a felhasználót, hogy az adatokat az adattárból elemek eltávolítása.

- A [System.Management.Automation.Provider.Containercmdletprovider.Renameitem*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.RenameItem) és [System.Management.Automation.Provider.Containercmdletprovider.Renameitemdynamicparameters*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.RenameItemDynamicParameters) módszerek határozza meg, hogy a szolgáltató támogatja-e a `Rename-Item` szolgáltató parancsmagot. Ez a parancsmag lehetővé teszi, hogy a felhasználót, hogy nevezze át az adattár elemeit.

  A szolgáltató parancsmagok végrehajtásához használt módszerek mellett a [System.Management.Automation.Provider.Containercmdletprovider](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider) osztály is határozza meg az alábbi módszerek:

- A [System.Management.Automation.Provider.Containercmdletprovider.Haschilditems*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.HasChildItems) módszer meghatározásához, hogy egy elem van-e a gyermekelemek használható a szolgáltató osztály alapján.

- A [System.Management.Automation.Provider.Containercmdletprovider.Convertpath*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.ConvertPath) módszer használható a szolgáltató osztály az új szolgáltatóhoz tartozó elérési út létrehozása a megadott elérési úton.

## <a name="navigation-enabled-providers"></a>Navigáció – engedélyezett szolgáltatók

Navigáció – engedélyezett szolgáltatók engedélyezése a felhasználó számára elemek áthelyezése az adattárban. Navigációs-kompatibilis szolgáltató létrehozásához a szolgáltató osztályból kell származnia a [System.Management.Automation.Provider.Navigationcmdletprovider](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider) osztály.

A [System.Management.Automation.Provider.Navigationcmdletprovider](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider) osztály határozza meg az alábbi módszerek megvalósításának adott szolgáltató parancsmagjai. A legtöbb esetben egy szolgáltató parancsmag támogatja, felül kell írnia a módszert, amelyet a Windows PowerShell meghívja a parancsmag meghívni például a `MoveItem` módszer a `Move-Item` parancsmagot, és opcionálisan egy második módszer, például felülírhatja`MoveItemDynamicParameters`, a dinamikus paraméterek hozzáadása a parancsmaghoz.

- A [System.Management.Automation.Provider.Navigationcmdletprovider.Moveitem*](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.MoveItem) és [System.Management.Automation.Provider.Navigationcmdletprovider.Moveitemdynamicparameters*](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.MoveItemDynamicParameters) módszerek határozza meg, hogy a szolgáltató támogatja-e a `Move-Item` szolgáltató parancsmagot. Ez a parancsmag lehetővé teszi, hogy a felhasználó az elem áthelyezése a tárolóban lévő egyik helyről egy másik helyre.

- A [System.Management.Automation.Provider.Navigationcmdletprovider.Makepath*](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.MakePath) metódus határozza meg, hogy a szolgáltató támogatja-e a `Join-Path` szolgáltató parancsmagot. Ez a parancsmag lehetővé teszi, hogy a felhasználó úgy, hogy a szülő és gyermek részleges útvonalat provider – belső elérési utat hoz létre.

  A szolgáltató parancsmagok végrehajtásához használt módszerek mellett a [System.Management.Automation.Provider.Navigationcmdletprovider](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider) osztály is határozza meg az alábbi módszerek:

- A [System.Management.Automation.Provider.Navigationcmdletprovider.Getchildname*](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.GetChildName) metódus kinyeri a gyermek csomópont egy elérési út neve.

- A [System.Management.Automation.Provider.Navigationcmdletprovider.Getparentpath*](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.GetParentPath) metódus kinyeri egy elérési utat a szülő részét.

- A [System.Management.Automation.Provider.Navigationcmdletprovider.Isitemcontainer*](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.IsItemContainer) metódus határozza meg, hogy az elem egy tároló elemet. Ebben a környezetben a tároló lehet egy közös szülő konfigurációelem a gyermekelemek csoportja.

- A [System.Management.Automation.Provider.Navigationcmdletprovider.Normalizerelativepath*](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.NormalizeRelativePath) metódus az elérési útként megadott alapútvonal viselkednek adja vissza.

## <a name="content-enabled-providers"></a>Tartalom engedélyezett szolgáltatók

Tartalom engedélyezett szolgáltatók engedélyezése a felhasználó törlése, beolvasása vagy beállítása cikkek tartalmának a tárolóban. Például a fájlrendszer-szolgáltatót lehetővé teszi, hogy törölje a jelet, lekérése és állítsa be a fájlok tartalmát a fájlrendszerben. Engedélyezve van a tartalomszolgáltatón létrehozásához, a szolgáltató osztály metódusain musí implementovat a [System.Management.Automation.Provider.Icontentcmdletprovider](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider) felületet.

A [System.Management.Automation.Provider.Icontentcmdletprovider](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider) az illesztő határozza meg az alábbi módszerek megvalósításának adott szolgáltató parancsmagjai. A legtöbb esetben egy szolgáltató parancsmag támogatja, felül kell írnia a módszert, amelyet a Windows PowerShell meghívja a parancsmag meghívni például a `ClearContent` módszer a `Clear-Content` parancsmagot, és opcionálisan egy második módszer, például felülírhatja`ClearContentDynamicParameters`, a dinamikus paraméterek hozzáadása a parancsmaghoz.

- A [System.Management.Automation.Provider.Icontentcmdletprovider.Clearcontent*](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider.ClearContent) és [System.Management.Automation.Provider.Icontentcmdletprovider.Clearcontentdynamicparameters*](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider.ClearContentDynamicParameters)módszerek határozza meg, hogy a szolgáltató támogatja-e a `Clear-Content` szolgáltató parancsmagot. Ez a parancsmag lehetővé teszi, hogy a felhasználót, hogy egy elem törlése az elem törlése nélkül.

- A [System.Management.Automation.Provider.Icontentcmdletprovider.Getcontentreader*](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider.GetContentReader) és [System.Management.Automation.Provider.Icontentcmdletprovider.Getcontentreaderdynamicparameters*](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider.GetContentReaderDynamicParameters) módszerek határozza meg, hogy a szolgáltató támogatja-e a `Get-Content` szolgáltató parancsmagot. Ez a parancsmag lehetővé teszi, hogy a felhasználó lekérni a tartalmat egy elem. A [System.Management.Automation.Provider.Icontentcmdletprovider.Getcontentreader*](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider.GetContentReader) metódus adja vissza egy [System.Management.Automation.Provider.Icontentreader](/dotnet/api/System.Management.Automation.Provider.IContentReader) , amely meghatározza a kapcsolat a metódusok a tartalmak olvasását.

- A [System.Management.Automation.Provider.Icontentcmdletprovider.Getcontentwriter*](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider.GetContentWriter) és [System.Management.Automation.Provider.Icontentcmdletprovider.Getcontentwriterdynamicparameters*](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider.GetContentWriterDynamicParameters) módszerek határozza meg, hogy a szolgáltató támogatja-e a `Set-Content` szolgáltató parancsmagot. Ez a parancsmag lehetővé teszi, hogy a felhasználó frissítheti egy cikk tartalmát. A [System.Management.Automation.Provider.Icontentcmdletprovider.Getcontentwriter*](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider.GetContentWriter) metódus adja vissza egy [System.Management.Automation.Provider.Icontentwriter](/dotnet/api/System.Management.Automation.Provider.IContentWriter) , amely meghatározza a kapcsolat a tartalmak írásához használt módszerek.

## <a name="property-enabled-providers"></a>Szolgáltatók tulajdonság engedélyezve

Tulajdonság engedélyezett szolgáltatók engedélyezése a felhasználó az adattárban található elemek tulajdonságainak kezeléséhez. Tulajdonság-kompatibilis szolgáltató létrehozásához a szolgáltató osztály metódusain musí implementovat a [System.Management.Automation.Provider.Ipropertycmdletprovider](/dotnet/api/System.Management.Automation.Provider.IPropertyCmdletProvider) és [ System.Management.Automation.Provider.Idynamicpropertycmdletprovider](/dotnet/api/System.Management.Automation.Provider.IDynamicPropertyCmdletProvider) felületek. A legtöbb esetben egy szolgáltató parancsmag támogatja, felül kell írnia a módszert, amelyet a Windows PowerShell meghívja a parancsmag meghívni például a `ClearProperty` metódus a Clear-tulajdonság parancsmagot, és opcionálisan egy második módszer, például felülírhatja`ClearPropertyDynamicParameters`, a dinamikus paraméterek hozzáadása a parancsmaghoz.

A [System.Management.Automation.Provider.Ipropertycmdletprovider](/dotnet/api/System.Management.Automation.Provider.IPropertyCmdletProvider) az illesztő határozza meg az alábbi módszerek adott szolgáltató parancsmagjai megvalósításához:

- A [System.Management.Automation.Provider.Ipropertycmdletprovider.Clearproperty*](/dotnet/api/System.Management.Automation.Provider.IPropertyCmdletProvider.ClearProperty) és [System.Management.Automation.Provider.Ipropertycmdletprovider.Clearpropertydynamicparameters*](/dotnet/api/System.Management.Automation.Provider.IPropertyCmdletProvider.ClearPropertyDynamicParameters) módszerek határozza meg, hogy a szolgáltató támogatja-e a `Clear-ItemProperty` szolgáltató parancsmagot. Ez a parancsmag lehetővé teszi, hogy a felhasználó törlése egy tulajdonság értéke.

- A [System.Management.Automation.Provider.Ipropertycmdletprovider.Getproperty*](/dotnet/api/System.Management.Automation.Provider.IPropertyCmdletProvider.GetProperty) és [System.Management.Automation.Provider.Ipropertycmdletprovider.Getpropertydynamicparameters*](/dotnet/api/System.Management.Automation.Provider.IPropertyCmdletProvider.GetPropertyDynamicParameters)módszerek határozza meg, hogy a szolgáltató támogatja-e a `Get-ItemProperty` szolgáltató parancsmagot. Ez a parancsmag lehetővé teszi, hogy a felhasználót, hogy a tulajdonság egy elem beolvasása.

- A [System.Management.Automation.Provider.Ipropertycmdletprovider.Setproperty*](/dotnet/api/System.Management.Automation.Provider.IPropertyCmdletProvider.SetProperty) és [System.Management.Automation.Provider.Ipropertycmdletprovider.Setpropertydynamicparameters*](/dotnet/api/System.Management.Automation.Provider.IPropertyCmdletProvider.SetPropertyDynamicParameters)módszerek határozza meg, hogy a szolgáltató támogatja-e a `Set-ItemProperty` szolgáltató parancsmagot. Ez a parancsmag lehetővé teszi, hogy a felhasználót, hogy egy elem tulajdonságainak frissítéséhez.

  A [System.Management.Automation.Provider.Idynamicpropertycmdletprovider](/dotnet/api/System.Management.Automation.Provider.IDynamicPropertyCmdletProvider) az illesztő határozza meg az alábbi módszerek adott szolgáltató parancsmagjai megvalósításához:

- A [System.Management.Automation.Provider.Idynamicpropertycmdletprovider.Copyproperty*](/dotnet/api/System.Management.Automation.Provider.IDynamicPropertyCmdletProvider.CopyProperty) és [ System.Management.Automation.Provider.Idynamicpropertycmdletprovider.Copypropertydynamicparameters*](/dotnet/api/System.Management.Automation.Provider.IDynamicPropertyCmdletProvider.CopyPropertyDynamicParameters) módszerek határozza meg, hogy a szolgáltató támogatja-e a `Copy-ItemProperty` szolgáltató parancsmagot. Ez a parancsmag lehetővé teszi, hogy a felhasználó egy tulajdonságot, és annak értékét másolása egyik helyről egy másikra.

- A [System.Management.Automation.Provider.Idynamicpropertycmdletprovider.Moveproperty*](/dotnet/api/System.Management.Automation.Provider.IDynamicPropertyCmdletProvider.MoveProperty) és [ System.Management.Automation.Provider.Idynamicpropertycmdletprovider.Movepropertydynamicparameters*](/dotnet/api/System.Management.Automation.Provider.IDynamicPropertyCmdletProvider.MovePropertyDynamicParameters) módszerek határozza meg, hogy a szolgáltató támogatja-e a `Move-ItemProperty` szolgáltató parancsmagot. Ez a parancsmag lehetővé teszi, hogy a felhasználót, hogy egy tulajdonságot, és annak értékét áthelyezése egyik helyről egy másikra.

- A [System.Management.Automation.Provider.Idynamicpropertycmdletprovider.Newproperty*](/dotnet/api/System.Management.Automation.Provider.IDynamicPropertyCmdletProvider.NewProperty) és [ System.Management.Automation.Provider.Idynamicpropertycmdletprovider.Newpropertydynamicparameters*](/dotnet/api/System.Management.Automation.Provider.IDynamicPropertyCmdletProvider.NewPropertyDynamicParameters) módszerek határozza meg, hogy a szolgáltató támogatja-e a `New-ItemProperty` szolgáltató parancsmagot. Ez a parancsmag lehetővé teszi, hogy a felhasználó számára hozzon létre egy új tulajdonságot, és állítsa az értékét.

- A [System.Management.Automation.Provider.Idynamicpropertycmdletprovider.Removeproperty*](/dotnet/api/System.Management.Automation.Provider.IDynamicPropertyCmdletProvider.RemoveProperty) és [ System.Management.Automation.Provider.Idynamicpropertycmdletprovider.Removepropertydynamicparameters*](/dotnet/api/System.Management.Automation.Provider.IDynamicPropertyCmdletProvider.RemovePropertyDynamicParameters) módszerek határozza meg, hogy a szolgáltató támogatja-e a `Remove-ItemProperty` parancsmagot. Ez a parancsmag lehetővé teszi, hogy a felhasználót, hogy törölni egy tulajdonságot, és annak értékét.

- A [System.Management.Automation.Provider.Idynamicpropertycmdletprovider.Renameproperty*](/dotnet/api/System.Management.Automation.Provider.IDynamicPropertyCmdletProvider.RenameProperty) és [ System.Management.Automation.Provider.Idynamicpropertycmdletprovider.Renamepropertydynamicparameters*](/dotnet/api/System.Management.Automation.Provider.IDynamicPropertyCmdletProvider.RenamePropertyDynamicParameters) módszerek határozza meg, hogy a szolgáltató támogatja-e a `Rename-ItemProperty` parancsmagot. Ez a parancsmag lehetővé teszi, hogy a felhasználó módosíthatja a tulajdonság nevét.

## <a name="see-also"></a>Lásd még:

[A Windows PowerShell-szolgáltató írása](./writing-a-windows-powershell-provider.md)