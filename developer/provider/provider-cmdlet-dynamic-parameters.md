---
title: Szolgáltató parancsmag dinamikus paraméterek |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 8f1069f7-8fa8-4622-9e2c-af29b0b961c2
caps.latest.revision: 6
ms.openlocfilehash: a50de014988336c473c565b506a73de1c864d7e0
ms.sourcegitcommit: caac7d098a448232304c9d6728e7340ec7517a71
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/16/2019
ms.locfileid: "58058232"
---
# <a name="provider-cmdlet-dynamic-parameters"></a>Szolgáltatói dinamikus parancsmag-paraméterek

Dinamikus paraméterek, amikor a felhasználó adja meg a statikus paraméterek, a parancsmag egy bizonyos értéket szolgáltató parancsmag hozzáadott szolgáltatók adhatja meg. Például egy szolgáltatót adhat hozzá másik dinamikus paraméterek alapján milyen elérési úton a felhasználó megadhatja, mikor hívják meg a `Get-Item` vagy `Set-Item` szolgáltató parancsmagjai.

## <a name="dynamic-parameter-methods"></a>Dinamikus paraméterek módszerek

Dinamikus paraméterek vannak meghatározva, a dinamikus paraméterek módszerekkel, például alkalmazásával a [System.Management.Automation.Provider.Itemcmdletprovider.Getitemdynamicparameters*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.GetItemDynamicParameters) és [ System.Management.Automation.Provider.Itemcmdletprovider.Setitemdynamicparameters*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.SetItemDynamicParameters)s módszereket. Ezek a metódusok nyilvános tulajdonságok vannak kitüntetett hasonlóak az önálló parancsmagok attribútumokkal rendelkező objektum visszaadása. Íme egy példa megvalósítását a [System.Management.Automation.Provider.Itemcmdletprovider.Getitemdynamicparameters*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.GetItemDynamicParameters) metódus a tanúsítványszolgáltató származnak:

```csharp
protected override object GetItemDynamicParameters(string path)
{
    return new CertificateProviderDynamicParameters();
}
```

Ellentétben a szolgáltató parancsmagjai statikus paraméterek adja meg ezeket a paramétereket jellemzőit ugyanolyan módon, hogy önálló parancsmagok paraméterek vannak meghatározva. Íme egy példa egy dinamikus paraméterek osztály a tanúsítványszolgáltató származnak:

```csharp
internal sealed class CertificateProviderDynamicParameters
{
  /// <summary>
  /// Dynamic parameter the controls whether we only return
  /// code signing certs.
  /// </summary>
  [Parameter()]
  public SwitchParameter CodeSigningCert
  {
    get
    {
      {
        return codeSigningCert;
      }
    }

    set
    {
      {
        codeSigningCert = value;
      }
    }
  }

    private SwitchParameter codeSigningCert = new SwitchParameter();
}
```

## <a name="dynamic-parameters"></a>Dinamikus paraméterek

Íme a statikus, dinamikus paraméterek hozzáadása használható paraméterek listáját.

`Clear-Content` a parancsmag a dinamikus paraméterek által aktivált meghatározhatja a `Path` a Törlés-Törlés parancsmag alkalmazásával a [System.Management.Automation.Provider.Icontentcmdletprovider.Clearcontentdynamicparameters* ](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider.ClearContentDynamicParameters) metódust.

`Clear-Item` a parancsmag a dinamikus paraméterek által aktivált meghatározhatja a `Path` paraméterében a `Clear-Item` parancsmag alkalmazásával a [System.Management.Automation.Provider.Itemcmdletprovider.Clearitemdynamicparameters*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.ClearItemDynamicParameters) metódust.

`Clear-ItemProperty` a parancsmag a dinamikus paraméterek által aktivált meghatározhatja a `Path` paraméterében a `Clear-ItemProperty` parancsmag alkalmazásával a [ System.Management.Automation.Provider.Ipropertycmdletprovider.Clearpropertydynamicparameters*](/dotnet/api/System.Management.Automation.Provider.IPropertyCmdletProvider.ClearPropertyDynamicParameters) metódust.

`Copy-Item` a parancsmag a dinamikus paraméterek által aktivált meghatározhatja a `Path`, `Destination`, és `Recurse` paraméterei a `Copy-Item` parancsmag alkalmazásával a [ System.Management.Automation.Provider.Containercmdletprovider.Copyitemdynamicparameters*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.CopyItemDynamicParameters) metódust.

Get-ChildItems parancsmag a dinamikus paraméterek által aktivált meghatározhatja a `Path` és `Recurse` paramétereit a `Get-ChildItem` parancsmag alkalmazásával a [ System.Management.Automation.Provider.Containercmdletprovider.Getchilditemsdynamicparameters*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.GetChildItemsDynamicParameters) és [System.Management.Automation.Provider.Containercmdletprovider.Getchildnamesdynamicparameters*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.GetChildNamesDynamicParameters) módszereket.

`Get-Content` a parancsmag a dinamikus paraméterek által aktivált meghatározhatja a `Path` paraméterében a `Get-Content` parancsmag alkalmazásával a [ System.Management.Automation.Provider.Icontentcmdletprovider.Getcontentreaderdynamicparameters*](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider.GetContentReaderDynamicParameters) metódust.

`Get-Item` a parancsmag a dinamikus paraméterek által aktivált meghatározhatja a `Path` paraméterében a `Get-Item` parancsmag alkalmazásával a [System.Management.Automation.Provider.Itemcmdletprovider.Getitemdynamicparameters*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.GetItemDynamicParameters) metódust.

`Get-ItemProperty` a parancsmag a dinamikus paraméterek által aktivált meghatározhatja a `Path` és `Name` paraméterei a `Get-ItemProperty` parancsmag alkalmazásával a [ System.Management.Automation.Provider.Ipropertycmdletprovider.Getpropertydynamicparameters*](/dotnet/api/System.Management.Automation.Provider.IPropertyCmdletProvider.GetPropertyDynamicParameters) metódust.

`Invoke-Item` a parancsmag a dinamikus paraméterek által aktivált meghatározhatja a `Path` paraméterében a `Invoke-Item` parancsmag alkalmazásával a [ System.Management.Automation.Provider.Itemcmdletprovider.Invokedefaultactiondynamicparameters*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.InvokeDefaultActionDynamicParameters) metódust.

`Move-Item` a parancsmag a dinamikus paraméterek által aktivált meghatározhatja a `Path` és `Destination` paraméterei a `Move-Item` parancsmag alkalmazásával a [ System.Management.Automation.Provider.Navigationcmdletprovider.Moveitemdynamicparameters*](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.MoveItemDynamicParameters) metódust.

`New-Item` a parancsmag a dinamikus paraméterek által aktivált meghatározhatja a `Path`, `ItemType`, és `Value` paraméterei a `New-Item` parancsmag alkalmazásával a [ System.Management.Automation.Provider.Containercmdletprovider.Newitemdynamicparameters*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.NewItemDynamicParameters) metódust.

`New-ItemProperty` a parancsmag a dinamikus paraméterek által aktivált meghatározhatja a `Path`, `Name`, `PropertyType`, és `Value` paraméterei a `New-ItemProperty` parancsmag alkalmazásával a [ System.Management.Automation.Provider.Idynamicpropertycmdletprovider.Newpropertydynamicparameters*](/dotnet/api/System.Management.Automation.Provider.IDynamicPropertyCmdletProvider.NewPropertyDynamicParameters) metódust.

`New-PSDrive` a parancsmag a dinamikus paraméterek által aktivált meghatározhatja a [System.Management.Automation.PSDriveinfo](/dotnet/api/System.Management.Automation.PSDriveInfo) által visszaadott objektum a `New-PSDrive` parancsmag alkalmazásával a [ System.Management.Automation.Provider.Drivecmdletprovider.Newdrivedynamicparameters*](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider.NewDriveDynamicParameters) metódust.

`Remove-Item` Dinamikus paraméterek által aktivált meghatározhatja a `Path` és `Recurse` paraméterei a `Remove-Item` parancsmag alkalmazásával a [ System.Management.Automation.Provider.Containercmdletprovider.Removeitemdynamicparameters*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.RemoveItemDynamicParameters) metódust.

`Remove-ItemProperty` Dinamikus paraméterek által aktivált meghatározhatja a `Path` és `Name` paraméterei a `Remove-ItemProperty` parancsmag alkalmazásával a [ System.Management.Automation.Provider.Idynamicpropertycmdletprovider.Removepropertydynamicparameters*](/dotnet/api/System.Management.Automation.Provider.IDynamicPropertyCmdletProvider.RemovePropertyDynamicParameters) metódust.

`Rename-Item` a parancsmag a dinamikus paraméterek által aktivált meghatározhatja a `Path` és `NewName` paraméterei a `Rename-Item` parancsmag alkalmazásával a [ System.Management.Automation.Provider.Containercmdletprovider.Renameitemdynamicparameters*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.RenameItemDynamicParameters) metódust.

`Rename-ItemProperty` Dinamikus paraméterek által aktivált meghatározhatja a `Path`, `Name`, és `NewName` paraméterei a `Rename-ItemProperty` parancsmag alkalmazásával a [ System.Management.Automation.Provider.Idynamicpropertycmdletprovider.Renamepropertydynamicparameters*](/dotnet/api/System.Management.Automation.Provider.IDynamicPropertyCmdletProvider.RenamePropertyDynamicParameters) metódust.

`Set-Content` a parancsmag a dinamikus paraméterek által aktivált meghatározhatja a `Path` paraméterében a `Set-Content` parancsmag alkalmazásával a [ System.Management.Automation.Provider.Icontentcmdletprovider.Getcontentwriterdynamicparameters*](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider.GetContentWriterDynamicParameters) metódust.

`Set-Item` a parancsmag a dinamikus paraméterek által aktivált meghatározhatja a `Path` és `Value` paraméterei a `Set-Item` parancsmag alkalmazásával a [ System.Management.Automation.Provider.Itemcmdletprovider.Setitemdynamicparameters*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.SetItemDynamicParameters) metódust.

`Set-ItemProperty` a parancsmag a dinamikus paraméterek által aktivált meghatározhatja a `Path` és `Value` paraméterei a `Set-Item` parancsmag alkalmazásával a [ System.Management.Automation.Provider.Ipropertycmdletprovider.Setpropertydynamicparameters*](/dotnet/api/System.Management.Automation.Provider.IPropertyCmdletProvider.SetPropertyDynamicParameters) metódust.

`Test-Path` a parancsmag a dinamikus paraméterek által aktivált meghatározhatja a `Path` paraméterében a `Test-Path` parancsmag alkalmazásával a [ System.Management.Automation.Provider.Itemcmdletprovider.Invokedefaultactiondynamicparameters*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.InvokeDefaultActionDynamicParameters) metódust.

## <a name="see-also"></a>Lásd még:

[A Windows PowerShell-szolgáltató írása](./writing-a-windows-powershell-provider.md)