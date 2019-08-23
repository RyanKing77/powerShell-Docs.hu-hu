---
title: Szolgáltatói típusok | Microsoft Docs
ms.custom: ''
ms.date: 08/21/2019
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: e523a8e1-42e4-4633-887f-fb74b3464561
caps.latest.revision: 12
ms.openlocfilehash: 0a9bfe5dd0978ffce66db1b18ef4d82be6c1a7f2
ms.sourcegitcommit: 5a004064f33acc0145ccd414535763e95f998c89
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/23/2019
ms.locfileid: "69986650"
---
# <a name="provider-types"></a>Szolgáltatótípusok

A szolgáltatók az alapfunkciókat úgy határozzák meg, hogy megváltoztatják a PowerShell által biztosított szolgáltatói parancsmagok működését, és végrehajtják a műveleteiket. A szolgáltatók például használhatják a `Get-Item` parancsmag alapértelmezett funkcióit, vagy megváltoztathatják, hogy a parancsmag hogyan működjön az elemek adattárból való beolvasása során. A jelen dokumentumban ismertetett szolgáltatói funkciók olyan funkciókat foglalnak magukban, amelyek az egyes szolgáltatói alaposztályokból és felületekből származó metódusok felülírásával rendelkeznek.

> [!NOTE]
> A PowerShell által előre definiált szolgáltatói funkciókért lásd: [szolgáltatói képességek](/previous-versions//ee126189(v=vs.85)).

## <a name="drive-enabled-providers"></a>Meghajtó-kompatibilis szolgáltatók

A meghajtóval kompatibilis szolgáltatók határozzák meg a felhasználó számára elérhető alapértelmezett meghajtókat, és lehetővé teszik a felhasználók számára meghajtók hozzáadását vagy eltávolítását. A legtöbb esetben a szolgáltatók meghajtó-kompatibilis szolgáltatók, mert az adattárban való hozzáféréshez szükségük van egy alapértelmezett meghajtóra. A saját szolgáltatójának írásakor azonban előfordulhat, hogy nem szeretné engedélyezni a felhasználó számára a meghajtók létrehozását és eltávolítását.

A meghajtókat támogató szolgáltató létrehozásához a szolgáltatói osztálynak a [System. Management. Automation. Provider. DriveCmdletProvider](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider) osztályból vagy egy másik, ebből az osztályból származtatott osztályból kell származnia. A **System. Management. Automation. Provider. DriveCmdletProvider** osztály a következő módszereket határozza meg a szolgáltató alapértelmezett meghajtóinak megvalósításához és a és `New-PSDrive` `Remove-PSDrive` a parancsmagok támogatásához. A legtöbb esetben a szolgáltatói parancsmag támogatásához felül kell írnia azt a metódust, amelyet a PowerShell-motor a parancsmag meghívására hív meg `New-PSDrive` , például `NewDrive` a parancsmag metódusát, és opcionálisan felülírhatja a `NewDriveDynamicParameters` második metódust is, például: dinamikus paraméterek a parancsmaghoz való hozzáadásához.

- A [System. Management. Automation. Provider. DriveCmdletProvider. InitializeDefaultDrives](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider.InitializeDefaultDrives) metódus határozza meg a felhasználó számára elérhető alapértelmezett meghajtókat, amikor a szolgáltató használatban van.

- A [System. Management. Automation. Provider. DriveCmdletProvider. NewDrive](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider.NewDrive) és [System. Management. Automation. Provider. DriveCmdletProvider. NewDriveDynamicParameters](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider.NewDriveDynamicParameters) módszerek határozzák meg, hogy a szolgáltató hogyan támogatja a `New-PSDrive`szolgáltatói parancsmag. Ez a parancsmag lehetővé teszi, hogy a felhasználó meghajtót hozzon létre az adattár eléréséhez.

- A [System. Management. Automation. Provider. DriveCmdletProvider. RemoveDrive](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider.RemoveDrive) metódus határozza meg, hogyan támogatja a `Remove-PSDrive` szolgáltató a Provider parancsmagot. Ez a parancsmag lehetővé teszi, hogy a felhasználó eltávolítsa a meghajtókat az adattárból.

## <a name="item-enabled-providers"></a>Elemmel kompatibilis szolgáltatók

Az elemek használatát engedélyező szolgáltatók lehetővé teszik a felhasználó számára az adattárban lévő elemek beolvasását, beállítását vagy törlését. Az "Item" az adattár olyan eleme, amelyet a felhasználó egymástól függetlenül elérhet vagy kezelhet. Egy elemmel kompatibilis szolgáltató létrehozásához a szolgáltatói osztálynak a [System. Management. Automation. Provider. ItemCmdletProvider](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider) osztályból vagy egy másik, ebből az osztályból származtatott osztályból kell származnia.

A **System. Management. Automation. Provider. ItemCmdletProvider** osztály a következő metódusokat határozza meg bizonyos szolgáltatói parancsmagok megvalósításához. A legtöbb esetben a szolgáltatói parancsmag támogatásához felül kell írnia azt a metódust, amelyet a PowerShell-motor a parancsmag meghívására hív meg `Clear-Item` , például `ClearItem` a parancsmag metódusát, és opcionálisan felülírhatja a `ClearItemDynamicParameters` második metódust is, például: dinamikus paraméterek a parancsmaghoz való hozzáadásához.

- A [System. Management. Automation. Provider. ItemCmdletProvider. ClearItem](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.ClearItem) és [System. Management. Automation. Provider. ItemCmdletProvider. ClearItemDynamicParameters](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.ClearItemDynamicParameters) módszerek határozzák meg, hogy a szolgáltató hogyan támogatja a `Clear-Item`szolgáltatói parancsmag. Ez a parancsmag lehetővé teszi a felhasználó számára az adattárban lévő elemek értékének eltávolítását.

- A [System. Management. Automation. Provider. ItemCmdletProvider. GetItem](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.GetItem) és [System. Management. Automation. Provider. ItemCmdletProvider. GetItemDynamicParameters](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.GetItemDynamicParameters) módszerek határozzák meg, hogy a `Get-Item` szolgáltató hogyan támogatja a szolgáltatói parancsmag. Ez a parancsmag lehetővé teszi, hogy a felhasználó beolvassa az adatait az adattárból.

- A [System. Management. Automation. Provider. ItemCmdletProvider. SetItem](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.SetItem) és [System. Management. Automation. Provider. ItemCmdletProvider. SetItemDynamicParameters](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.SetItemDynamicParameters) módszerek határozzák meg, hogy a `Set-Item` szolgáltató hogyan támogatja a szolgáltatói parancsmag. Ez a parancsmag lehetővé teszi, hogy a felhasználó frissítse az adattárban lévő elemek értékeit.

- A [System. Management. Automation. Provider. Itemcmdletprovider. InvokeDefaultAction](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.InvokeDefaultAction) és [System. Management. Automation. Provider. Itemcmdletprovider. InvokeDefaultActionDynamicParameters](/dotnet/api/system.management.automation.provider.itemcmdletprovider.invokedefaultactiondynamicparameters) metódusok határozzák meg a szolgáltatót támogatja a `Invoke-Item` Provider parancsmagot. Ez a parancsmag lehetővé teszi, hogy a felhasználó végrehajtsa az adott elemmel megadott alapértelmezett műveletet.

- A [System. Management. Automation. Provider. ItemCmdletProvider. ItemExists](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.ItemExists) és [System. Management. Automation. Provider. ItemCmdletProvider. ItemExistsDynamicParameters](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.ItemExistsDynamicParameters) módszerek határozzák meg, hogy a szolgáltató hogyan támogatja a `Test-Path`szolgáltatói parancsmag. Ez a parancsmag lehetővé teszi a felhasználó számára annak meghatározását, hogy létezik-e egy elérési út összes eleme.

A szolgáltatói parancsmagok megvalósításához használt módszerek mellett a **System. Management. Automation. Provider. ItemCmdletProvider** osztály a következő módszereket is meghatározza:

- A [System. Management. Automation. Provider. ItemCmdletProvider. ExpandPath](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.ExpandPath) metódus lehetővé teszi, hogy a felhasználó helyettesítő karaktereket használjon a szolgáltató elérési útjának megadásakor.

- A [System. Management. Automation. Provider. ItemCmdletProvider. IsValidPath](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.IsValidPath) segítségével megállapítható, hogy az elérési út szintaktikai és szemantikailag érvényes-e a szolgáltató számára.

## <a name="container-enabled-providers"></a>Tárolók számára engedélyezett szolgáltatók

A tárolók számára engedélyezett szolgáltatók lehetővé teszik, hogy a felhasználó kezelje a tárolók elemeit. A tárolók egy közös fölérendelt elem alatti alárendelt elemek csoportja. Egy tárolót engedélyező szolgáltató létrehozásához a szolgáltatói osztálynak a [System. Management. Automation. Provider. ContainerCmdletProvider](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider) osztályból vagy egy másik, ebből az osztályból származtatott osztályból kell származnia.

> [!IMPORTANT]
> A tárolók számára engedélyezett szolgáltatók nem férnek hozzá a beágyazott tárolókat tartalmazó adattárakhoz. Ha egy tároló alárendelt eleme egy másik tároló, be kell vezetnie egy navigációs képességgel rendelkező szolgáltatót.

A **System. Management. Automation. Provider. ContainerCmdletProvider** osztály a következő metódusokat határozza meg bizonyos szolgáltatói parancsmagok megvalósításához. A legtöbb esetben a szolgáltatói parancsmag támogatásához felül kell írnia azt a metódust, amelyet a PowerShell-motor a parancsmag meghívására hív meg `Copy-Item` , például `CopyItem` a parancsmag metódusát, és opcionálisan felülírhatja a `CopyItemDynamicParameters` második metódust is, például: dinamikus paraméterek a parancsmaghoz való hozzáadásához.

- A [System. Management. Automation. Provider. ContainerCmdletProvider. CopyItem](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.CopyItem) és [System. Management. Automation. Provider. ContainerCmdletProvider. CopyItemDynamicParameters](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.CopyItemDynamicParameters) módszerek határozzák meg, hogy a szolgáltató hogyan támogatja a `Copy-Item` szolgáltatói parancsmag. Ez a parancsmag lehetővé teszi, hogy a felhasználó az egyik helyről egy másikra másoljon egy elemet.

- A [System. Management. Automation. Provider. ContainerCmdletProvider. GetChildItems](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.GetChildItems) és [System. Management. Automation. Provider. ContainerCmdletProvider. GetChildItemsDynamicParameters](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.GetChildItemsDynamicParameters) metódusok határozzák meg a szolgáltatót támogatja a `Get-ChildItem` Provider parancsmagot. Ez a parancsmag lehetővé teszi a felhasználó számára, hogy lekérje a fölérendelt elem alárendelt elemeit.

- A [System. Management. Automation. Provider. ContainerCmdletProvider. GetChildNames](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.GetChildNames) és [System. Management. Automation. Provider. ContainerCmdletProvider. GetChildNamesDynamicParameters](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.GetChildNamesDynamicParameters) metódusok határozzák meg a szolgáltatót a `Get-ChildItem` szolgáltatói parancsmagot támogatja `Name` , ha a paraméter meg van adva.

- A [System. Management. Automation. Provider. ContainerCmdletProvider. NewItem](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.NewItem) és [System. Management. Automation. Provider. ContainerCmdletProvider. NewItemDynamicParameters](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.NewItemDynamicParameters) módszerek határozzák meg, hogy a szolgáltató hogyan támogatja a `New-Item` szolgáltatói parancsmag. Ez a parancsmag lehetővé teszi, hogy a felhasználó új elemeket hozzon létre az adattárban.

- A [System. Management. Automation. Provider. ContainerCmdletProvider. RemoveItem](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.RemoveItem) és [System. Management. Automation. Provider. ContainerCmdletProvider. RemoveItemDynamicParameters](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.RemoveItemDynamicParameters) módszerek határozzák meg, hogy a szolgáltató hogyan támogatja a `Remove-Item` szolgáltatói parancsmag. Ez a parancsmag lehetővé teszi, hogy a felhasználó eltávolítsa az elemeket az adattárból.

- A [System. Management. Automation. Provider. ContainerCmdletProvider. RenameItem](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.RenameItem) és [System. Management. Automation. Provider. ContainerCmdletProvider. RenameItemDynamicParameters](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.RenameItemDynamicParameters) módszerek határozzák meg, hogy a szolgáltató hogyan támogatja a `Rename-Item` szolgáltatói parancsmag. Ez a parancsmag lehetővé teszi a felhasználó számára az adattárban lévő elemek átnevezését.

A szolgáltatói parancsmagok megvalósításához használt módszerek mellett a **System. Management. Automation. Provider. ContainerCmdletProvider** osztály a következő módszereket is meghatározza:

- A [System. Management. Automation. Provider. ContainerCmdletProvider. HasChildItems](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.HasChildItems) metódust a szolgáltató osztály használhatja annak megállapítására, hogy egy elem rendelkezik-e alárendelt elemekkel.

- A [System. Management. Automation. Provider. ContainerCmdletProvider. ConvertPath](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.ConvertPath) metódust a Provider osztály használhatja arra, hogy egy adott elérési útról származó új szolgáltatói útvonalat hozzon létre.

## <a name="navigation-enabled-providers"></a>Navigációs képességgel rendelkező szolgáltatók

A navigációs képességgel rendelkező szolgáltatók lehetővé teszik, hogy a felhasználó áthelyezze az elemeket az adattárba. A navigációs képességgel rendelkező szolgáltatók létrehozásához a szolgáltatói osztálynak a [System. Management. Automation. Provider. NavigationCmdletProvider](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider) osztályból kell származnia.

A **System. Management. Automation. Provider. NavigationCmdletProvider** osztály a következő metódusokat határozza meg bizonyos szolgáltatói parancsmagok megvalósításához. A legtöbb esetben a szolgáltatói parancsmag támogatásához felül kell írnia azt a metódust, amelyet a PowerShell-motor a parancsmag meghívására hív meg `Move-Item` , például `MoveItem` a parancsmag metódusát, és opcionálisan felülírhatja a `MoveItemDynamicParameters` második metódust is, például: dinamikus paraméterek a parancsmaghoz való hozzáadásához.

- A [System. Management. Automation. Provider. NavigationCmdletProvider. MoveItem](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.MoveItem) és [System. Management. Automation. Provider. NavigationCmdletProvider. MoveItemDynamicParameters](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.MoveItemDynamicParameters) módszerek határozzák meg, hogy a szolgáltató hogyan támogatja a `Move-Item` szolgáltatói parancsmag. Ez a parancsmag lehetővé teszi, hogy a felhasználó egy elemet a tároló egyik helyéről egy másik helyre helyezzen át.

- A [System. Management. Automation. Provider. NavigationCmdletProvider. MakePath](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.MakePath) metódus határozza meg, hogyan támogatja a `Join-Path` szolgáltató a Provider parancsmagot. Ez a parancsmag lehetővé teszi, hogy a felhasználó egyesítse a szülő és gyermek elérésiút-szegmenst a szolgáltató belső elérési útjának létrehozásához.

A szolgáltatói parancsmagok megvalósításához használt módszerek mellett a **System. Management. Automation. Provider. NavigationCmdletProvider** osztály a következő módszereket is meghatározza:

- A [System. Management. Automation. Provider. NavigationCmdletProvider. GetChildName](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.GetChildName) metódus kibontja egy elérési út alárendelt csomópontjának nevét.

- A [System. Management. Automation. Provider. NavigationCmdletProvider. GetParentPath](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.GetParentPath) metódus kibontja az elérési út szülő részét.

- A [System. Management. Automation. Provider. NavigationCmdletProvider. IsItemContainer](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.IsItemContainer) metódus határozza meg, hogy az elem egy tároló elem-e. Ebben a kontextusban a tároló az alárendelt elemek egy csoportját jelöli egy közös fölérendelt elem alatt.

- A [System. Management. Automation. Provider. NavigationCmdletProvider. NormalizeRelativePath](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.NormalizeRelativePath) metódus visszaadja a megadott alapútvonalhoz viszonyított elem elérési útját.

## <a name="content-enabled-providers"></a>Content-kompatibilis szolgáltatók

A tartalom-kompatibilis szolgáltatók lehetővé teszik a felhasználó számára az adattárban lévő elemek tartalmának törlését, beolvasását vagy beállítását.
A fájlrendszer-szolgáltató például lehetővé teszi a fájlrendszerben lévő fájlok tartalmának törlését, beolvasását és beállítását. A tartalom-kompatibilis szolgáltató létrehozásához a szolgáltatói osztálynak meg kell valósítania a [System. Management. Automation. Provider. IContentCmdletProvider](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider) interfész metódusait.

A **System. Management. Automation. Provider. IContentCmdletProvider** felülete a következő metódusokat határozza meg bizonyos szolgáltatói parancsmagok megvalósításához. A legtöbb esetben a szolgáltatói parancsmag támogatásához felül kell írnia azt a metódust, amelyet a PowerShell-motor a parancsmag meghívására hív meg `Clear-Content` , például `ClearContent` a parancsmag metódusát, és opcionálisan felülírhatja a `ClearContentDynamicParameters` második metódust is, például: dinamikus paraméterek a parancsmaghoz való hozzáadásához.

- A [System. Management. Automation. Provider. IContentCmdletProvider. ClearContent](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider.ClearContent) és [System. Management. Automation. Provider. IContentCmdletProvider. ClearContentDynamicParameters](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider.ClearContentDynamicParameters) metódusok határozzák meg, hogyan támogatja a szolgáltató a `Clear-Content` Provider parancsmag. Ez a parancsmag lehetővé teszi a felhasználó számára az elemek tartalmának törlését az elemek törlése nélkül.

- A [System. Management. Automation. Provider. IContentCmdletProvider. GetContentReader](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider.GetContentReader) és [System. Management. Automation. Provider. IContentCmdletProvider. GetContentReaderDynamicParameters](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider.GetContentReaderDynamicParameters) metódusok határozzák meg a szolgáltatót támogatja a `Get-Content` Provider parancsmagot. Ez a parancsmag lehetővé teszi a felhasználó számára egy adott tétel tartalmának lekérését. A `System.Management.Automation.Provider.IContentCmdletProvider.GetContentReader` metódus egy [System. Management. Automation. Provider. IContentReader](/dotnet/api/System.Management.Automation.Provider.IContentReader) felületet ad vissza, amely meghatározza a tartalom olvasásához használt metódusokat.

- A [System. Management. Automation. Provider. IContentCmdletProvider. GetContentWriter](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider.GetContentWriter) és [System. Management. Automation. Provider. IContentCmdletProvider. GetContentWriterDynamicParameters](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider.GetContentWriterDynamicParameters) metódusok határozzák meg a szolgáltatót támogatja a `Set-Content` Provider parancsmagot. Ez a parancsmag lehetővé teszi a felhasználó számára egy adott tétel tartalmának frissítését. A `System.Management.Automation.Provider.IContentCmdletProvider.GetContentWriter` metódus egy [System. Management. Automation. Provider. IContentWriter](/dotnet/api/System.Management.Automation.Provider.IContentWriter) felületet ad vissza, amely meghatározza a tartalom írásához használt módszereket.

## <a name="property-enabled-providers"></a>Tulajdonsággal rendelkező szolgáltatók

A tulajdonságot engedélyező szolgáltatók lehetővé teszik, hogy a felhasználó kezelje az adattár elemeinek tulajdonságait.
A tulajdonságot támogató szolgáltató létrehozásához a szolgáltatói osztálynak meg kell valósítania a [System. Management. Automation. Provider. IPropertyCmdletProvider](/dotnet/api/System.Management.Automation.Provider.IPropertyCmdletProvider) és [System. Management. Automation. Provider. IDynamicPropertyCmdletProvider metódusait. ](/dotnet/api/System.Management.Automation.Provider.IDynamicPropertyCmdletProvider)felületek. A legtöbb esetben a szolgáltatói parancsmag támogatásához felül kell írnia azt a metódust, amelyet a PowerShell-motor hív a parancsmag meghívásához, `ClearProperty` például a Clear-Property parancsmag metódusát, és opcionálisan felül is írhatja a második metódust, `ClearPropertyDynamicParameters` például: dinamikus paraméterek a parancsmaghoz való hozzáadásához.

A **System. Management. Automation. Provider. IPropertyCmdletProvider** felülete a következő metódusokat határozza meg a megadott szolgáltatói parancsmagok megvalósításához:

- A [System. Management. Automation. Provider. IPropertyCmdletProvider. ClearProperty](/dotnet/api/System.Management.Automation.Provider.IPropertyCmdletProvider.ClearProperty) és [System. Management. Automation. Provider. IPropertyCmdletProvider. ClearPropertyDynamicParameters](/dotnet/api/System.Management.Automation.Provider.IPropertyCmdletProvider.ClearPropertyDynamicParameters) metódusok határozzák meg a szolgáltatót támogatja a `Clear-ItemProperty` Provider parancsmagot. Ez a parancsmag lehetővé teszi a felhasználó számára egy tulajdonság értékének törlését.

- A [System. Management. Automation. Provider. IPropertyCmdletProvider. GetProperty](/dotnet/api/System.Management.Automation.Provider.IPropertyCmdletProvider.GetProperty) és [System. Management. Automation. Provider. IPropertyCmdletProvider. GetPropertyDynamicParameters](/dotnet/api/System.Management.Automation.Provider.IPropertyCmdletProvider.GetPropertyDynamicParameters) metódusok határozzák meg, hogyan támogatja a szolgáltató a `Get-ItemProperty` Provider parancsmag. Ez a parancsmag lehetővé teszi a felhasználó számára egy adott tétel tulajdonságának lekérését.

- A [System. Management. Automation. Provider. IPropertyCmdletProvider. SetProperty](/dotnet/api/System.Management.Automation.Provider.IPropertyCmdletProvider.SetProperty) és [System. Management. Automation. Provider. IPropertyCmdletProvider. SetPropertyDynamicParameters](/dotnet/api/System.Management.Automation.Provider.IPropertyCmdletProvider.SetPropertyDynamicParameters) metódusok határozzák meg, hogyan támogatja a szolgáltató a `Set-ItemProperty` Provider parancsmag. Ez a parancsmag lehetővé teszi, hogy a felhasználó frissítse az elemek tulajdonságait.

  A **System. Management. Automation. Provider. IDynamicPropertyCmdletProvider** felülete a következő metódusokat határozza meg a megadott szolgáltatói parancsmagok megvalósításához:

- A [System. Management. Automation. Provider. IDynamicPropertyCmdletProvider. CopyProperty](/dotnet/api/System.Management.Automation.Provider.IDynamicPropertyCmdletProvider.CopyProperty) és [System. Management. Automation. Provider. IDynamicPropertyCmdletProvider. CopyPropertyDynamicParameters](/dotnet/api/System.Management.Automation.Provider.IDynamicPropertyCmdletProvider.CopyPropertyDynamicParameters) metódusok határozzák meg, hogyan a szolgáltató támogatja `Copy-ItemProperty` a Provider parancsmagot. Ez a parancsmag lehetővé teszi, hogy a felhasználó egy tulajdonságot és annak értékét egy helyről egy másikra másolja.

- A [System. Management. Automation. Provider. IDynamicPropertyCmdletProvider. MoveProperty](/dotnet/api/System.Management.Automation.Provider.IDynamicPropertyCmdletProvider.MoveProperty) és [System. Management. Automation. Provider. IDynamicPropertyCmdletProvider. MovePropertyDynamicParameters](/dotnet/api/System.Management.Automation.Provider.IDynamicPropertyCmdletProvider.MovePropertyDynamicParameters) metódusok határozzák meg, hogyan a szolgáltató támogatja `Move-ItemProperty` a Provider parancsmagot. Ez a parancsmag lehetővé teszi, hogy a felhasználó áthelyezze a tulajdonságot és annak értékét egyik helyről a másikra.

- A [System. Management. Automation. Provider. IDynamicPropertyCmdletProvider. NewProperty](/dotnet/api/System.Management.Automation.Provider.IDynamicPropertyCmdletProvider.NewProperty) és [System. Management. Automation. Provider. IDynamicPropertyCmdletProvider. NewPropertyDynamicParameters](/dotnet/api/System.Management.Automation.Provider.IDynamicPropertyCmdletProvider.NewPropertyDynamicParameters) metódusok határozzák meg, hogyan a szolgáltató támogatja `New-ItemProperty` a Provider parancsmagot. Ez a parancsmag lehetővé teszi, hogy a felhasználó új tulajdonságot hozzon létre, és beállítsa annak értékét.

- A [System. Management. Automation. Provider. IDynamicPropertyCmdletProvider. RemoveProperty](/dotnet/api/System.Management.Automation.Provider.IDynamicPropertyCmdletProvider.RemoveProperty) és [System. Management. Automation. Provider. IDynamicPropertyCmdletProvider. RemovePropertyDynamicParameters](/dotnet/api/System.Management.Automation.Provider.IDynamicPropertyCmdletProvider.RemovePropertyDynamicParameters) metódusok határozzák meg, hogyan a szolgáltató támogatja a `Remove-ItemProperty` parancsmagot. Ez a parancsmag lehetővé teszi, hogy a felhasználó törölje a tulajdonságot és annak értékét.

- A [System. Management. Automation. Provider. IDynamicPropertyCmdletProvider. RenameProperty](/dotnet/api/System.Management.Automation.Provider.IDynamicPropertyCmdletProvider.RenameProperty) és [System. Management. Automation. Provider. IDynamicPropertyCmdletProvider. RenamePropertyDynamicParameters](/dotnet/api/System.Management.Automation.Provider.IDynamicPropertyCmdletProvider.RenamePropertyDynamicParameters) metódusok határozzák meg, hogyan a szolgáltató támogatja a `Rename-ItemProperty` parancsmagot. Ez a parancsmag lehetővé teszi, hogy a felhasználó módosítsa a tulajdonság nevét.

## <a name="see-also"></a>Lásd még:

[about_Providers](/powershell/module/microsoft.powershell.core/about/about_providers)

[Windows PowerShell-szolgáltató írása](./writing-a-windows-powershell-provider.md)
