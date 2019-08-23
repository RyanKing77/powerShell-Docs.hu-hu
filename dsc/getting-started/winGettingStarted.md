---
ms.date: 08/15/2019
keywords: DSC, PowerShell, konfigurálás, beállítás
title: Ismerkedés a Windowshoz készült kívánt állapot-konfigurációval (DSC)
ms.openlocfilehash: a4f9db481afda65fc4ac5e553230dbba3037ac9a
ms.sourcegitcommit: 5a004064f33acc0145ccd414535763e95f998c89
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/23/2019
ms.locfileid: "69988927"
---
# <a name="get-started-with-desired-state-configuration-dsc-for-windows"></a>Ismerkedés a Windowshoz készült kívánt állapot-konfigurációval (DSC)

Ez a témakör a PowerShell desired State Configuration (DSC) Windows rendszerhez való használatának első lépéseit ismerteti.
A DSC-vel kapcsolatos általános információkért lásd: Ismerkedés [a Windows PowerShell kívánt állapotának konfigurálásával](../overview/overview.md).

## <a name="supported-windows-operation-system-versions"></a>A Windows operációs rendszer támogatott verziói

A következő verziók támogatottak:

- A Windows Server 2019
- Windows Server 2016
- Windows Server 2012R2
- Windows Server 2012
- Windows Server 2008 R2 SP1
- Windows 10
- Windows 8.1
- Windows 7

A [Microsoft Hyper-V Server](/windows-server/virtualization/hyper-v/hyper-v-server-2016) önálló termék SKU nem tartalmazza a kívánt állapot konfigurációja megvalósítását, így nem felügyelhető a PowerShell DSC-vel vagy Azure Automation állapot-konfigurációval.

## <a name="installing-dsc"></a>A DSC telepítése

A PowerShell kívánt állapotának konfigurációját a Windows tartalmazza, és a Windows Management Framework frissíti.
A legújabb verzió a [Windows Management Framework 5,1](https://www.microsoft.com/en-us/download/details.aspx?id=54616).

> [!NOTE]
> A DSC-t használó gépek felügyeletéhez nincs szükség a Windows Server "DSC-Service" funkciójának engedélyezésére.
> Erre a szolgáltatásra csak Windows lekéréses kiszolgálópéldány létrehozásakor van szükség.

## <a name="using-dsc-for-windows"></a>A DSC használata Windows rendszeren

A következő szakasz ismerteti, hogyan hozhatók létre és futtathatók DSC-konfigurációk a Windows rendszerű számítógépeken.

### <a name="creating-a-configuration-mof-document"></a>Konfigurációs MOF-dokumentum létrehozása

A Windows PowerShell konfigurációs kulcsszava konfiguráció létrehozásához használható.
A következő lépések a konfigurációs dokumentumok Windows PowerShell használatával történő létrehozását ismertetik.

#### <a name="define-a-configuration-and-generate-the-configuration-document"></a>Konfiguráció definiálása és a konfigurációs dokumentum létrehozása:

```powershell
Configuration EnvironmentVariable_Path
{
    param ()

    Import-DscResource -ModuleName 'PSDscResources'

    Node localhost
    {
        Environment CreatePathEnvironmentVariable
        {
            Name = 'TestPathEnvironmentVariable'
            Value = 'TestValue'
            Ensure = 'Present'
            Path = $true
            Target = @('Process', 'Machine')
        }
    }
}

EnvironmentVariable_Path -OutputPath:"C:\EnvironmentVariable_Path"
```
#### <a name="install-a-module-containing-dsc-resources"></a>DSC-erőforrásokat tartalmazó modul telepítése

A Windows PowerShell kívánt állapotának konfigurálása a DSC-erőforrásokat tartalmazó beépített modulokat tartalmaz.
A PowerShellGet-parancsmagok használatával olyan külső forrásokból is betöltheti a modulokat, mint a PowerShell-galéria.

`Install-Module 'PSDscResources' -Verbose`

#### <a name="apply-the-configuration-to-the-machine"></a>A konfiguráció alkalmazása a gépre

A konfigurációs dokumentumok (MOF-fájlok) a [Start-DscConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration) parancsmag használatával alkalmazhatók a gépre.

`Start-DscConfiguration -Path 'C:\EnvironmentVariable_Path' -Wait -Verbose`

#### <a name="get-the-current-state-of-the-configuration"></a>A konfiguráció aktuális állapotának beolvasása

A [Get-DscConfiguration](/powershell/module/psdesiredstateconfiguration/get-dscconfiguration) parancsmag lekérdezi a gép aktuális állapotát, és visszaadja a konfiguráció aktuális értékeit.

`Get-DscConfiguration`

A [Get-DscLocalConfigurationManager](/powershell/module/psdesiredstateconfiguration/get-dscLocalConfigurationManager) parancsmag a gépen alkalmazott aktuális meta-konfigurációt adja vissza.

`Get-DscLocalConfigurationManager`

#### <a name="remove-the-current-configuration-from-a-machine"></a>A jelenlegi konfiguráció eltávolítása egy gépről

A [Remove-DscConfigurationDocument](/powershell/module/psdesiredstateconfiguration/remove-dscconfigurationdocument)

`Remove-DscConfigurationDocument -Stage Current -Verbose`

#### <a name="configure-settings-in-local-configuration-manager"></a>Beállítások konfigurálása a helyi Configuration Manager

A [set-DSCLocalConfigurationManager](/powershell/module/PSDesiredStateConfiguration/Set-DscLocalConfigurationManager) parancsmag használatával alkalmazzon egy meta Configuration MOF-fájlt a gépre.
A metaadat-konfiguráció MOF elérési útját igényli.

`Set-DSCLocalConfigurationManager -Path 'c:\metaconfig\localhost.meta.mof' -Verbose`

## <a name="windows-powershell-desired-state-configuration-log-files"></a>A Windows PowerShell kívánt állapotának konfigurációs naplófájljai

A DSC-naplókat a Windows eseménynaplóba írja a rendszer `Microsoft-Windows-Dsc/Operational`az elérési úton.
A hibakeresési célból további naplók is engedélyezhetők a [DSC](/powershell/dsc/troubleshooting/troubleshooting#where-are-dsc-event-logs)-eseménynaplók lépéseit követve.
