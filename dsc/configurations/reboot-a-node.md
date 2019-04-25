---
ms.date: 1/17/2019
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Csomópont újraindítása
ms.openlocfilehash: 015b82a32caefc420973651c72e272fd85baf880
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62080118"
---
# <a name="reboot-a-node"></a>Csomópont újraindítása

> [!NOTE]
> Ez a témakör ismerteti hogyan lehet egy csomópont újraindítását. Ahhoz, hogy az újraindítás, a sikeres a **ActionAfterReboot** és **RebootNodeIfNeeded** LCM beállításainak megfelelően konfigurálni kell.
> Című témakörben olvashat a helyi Configuration Manager-beállítások, [a Local Configuration Manager konfigurálása](../managing-nodes/metaConfig.md), vagy [konfigurálása a Local Configuration Manager (v4)](../managing-nodes/metaConfig4.md).

Csomópontok is újra kell indítani a belül egy erőforrást, az a `$global:DSCMachineStatus` jelzőt. Jelzőbit `1` a a `Set-TargetResource` függvény kényszeríti az LCM kell újraindítani a csomópontot közvetlenül után a **beállítása** metódus az aktuális erőforrás. Ez a jelző használatával a **xPendingReboot** erőforrás észleli, ha újraindítás függőben lévő DSC-en kívül.

A [konfigurációk](configurations.md) előfordulhat, hogy hajtsa végre a lépéseket, a csomópont újraindítását igénylő. Ez sikerült közé tartozik többek között például:

- Windows-frissítések
- Szoftver telepítése
- Fájl átnevezése
- Számítógép átnevezése

A **xPendingReboot** erőforrás ellenőrzi a megadott számítógép helyek annak megállapításához, hogy újraindítás függőben. Ha a csomópontot újra kell indítani, DSC-en kívül a **xPendingReboot** erőforrás-csoportok a `$global:DSCMachineStatus` jelzőt `1` kényszerített újraindítás felismerését és feloldását, a függőben lévő feltétel.

> [!NOTE]
> Bármely DSC-erőforrás, a csomópont újraindítása, ha ez a jelző tulajdonságban az LCM utasíthatja a `Set-TargetResource` függvény. További információkért lásd: [MOF-egyéni DSC-erőforrás írása](../resources/authoringResourceMOF.md).

## <a name="syntax"></a>Szintaxis

```
xPendingReboot [String] #ResourceName
{
    Name = [string]
    [DependsOn = [string[]]]
    [PsDscRunAsCredential = [PSCredential]]
    [SkipCcmClientSDK = [bool]]
    [SkipComponentBasedServicing = [bool]]
    [SkipPendingComputerRename = [bool]]
    [SkipPendingFileRename = [bool]]
    [SkipWindowsUpdate = [bool]]
}
```

## <a name="properties"></a>Tulajdonságok

| Tulajdonság | Leírás |
| --- | --- |
| Név| Kötelező paraméter, amely példányonként az erőforrás egy konfigurációs belül egyedinek kell lennie.|
| SkipComponentBasedServicing | Az összetevő-alapú kiszolgálás összetevő által aktivált kihagyása újraindítások. |
| SkipWindowsUpdate | Windows Update által aktivált kihagyása újraindítások.|
| SkipPendingFileRename | Függőben lévő fájlok kihagyása nevezze át az újraindítások. |
| SkipCcmClientSDK | A ConfigMgr-ügyfél által aktivált kihagyása újraindítások. |
| SkipComputerRename | Számítógép által aktivált kihagyása újraindítások nevez át. |
| PSDSCRunAsCredential | A 5-ös verzióját támogatja. Az erőforrás végrehajtja a megadott felhasználó. |
| DependsOn | Azt jelzi, hogy a konfigurációt egy másik erőforrás futtatnia kell, mielőtt az erőforrás konfigurálva van. Például, ha az erőforrás-konfiguráció azonosítója letiltása, a futtatni kívánt parancsfájl először van **ResourceName** és a típusa **ResourceType**, ez a tulajdonság használata esetén `DependsOn = "[ResourceType]ResourceName"`. További információkért lásd: [DependsOn használatával](resource-depends-on.md)|

## <a name="example"></a>Példa

A következő példa telepíti a Microsoft Exchange segítségével a [xExchange](https://github.com/PowerShell/xExchange) erőforrás.
A telepítés során a **xPendingReboot** erőforrás szolgál újraindíthatja a csomópontot.

> [!NOTE]
> Ebben a példában a szükséges Exchange-kiszolgáló hozzáadása az erdő jogosultságokkal rendelkező fiók hitelesítő adatait. A DSC-hitelesítőadatokkal további információkért lásd: [hitelesítő adatok kezelése a DSC](../configurations/configDataCredentials.md)

```powershell
$ConfigurationData = @{
    AllNodes = @(
        @{
            NodeName                    = '*'
            PSDSCAllowPlainTextPassword = $true
        },
        @{
            NodeName = 'DSCPULL-1'
        }
    )
}

Configuration Example
{
    param
    (
        [Parameter(Mandatory = $true)]
        [System.Management.Automation.PSCredential]
        $ExchangeAdminCredential
    )

    Import-DscResource -Module xExchange
    Import-DscResource -Module xPendingReboot

    Node $AllNodes.NodeName
    {
        # Copy the Exchange setup files locally
        File ExchangeBinaries
        {
            Ensure          = 'Present'
            Type            = 'Directory'
            Recurse         = $true
            SourcePath      = '\\rras-1\Binaries\E15CU6'
            DestinationPath = 'C:\Binaries\E15CU6'
        }

        # Check if a reboot is needed before installing Exchange
        xPendingReboot BeforeExchangeInstall
        {
            Name       = 'BeforeExchangeInstall'
            DependsOn  = '[File]ExchangeBinaries'
        }

        # Do the Exchange install
        xExchInstall InstallExchange
        {
            Path       = 'C:\Binaries\E15CU6\Setup.exe'
            Arguments  = '/mode:Install /role:Mailbox /Iacceptexchangeserverlicenseterms'
            Credential = $ExchangeAdminCredential
            DependsOn  = '[xPendingReboot]BeforeExchangeInstall'
        }

        # See if a reboot is required after installing Exchange
        xPendingReboot AfterExchangeInstall
        {
            Name      = 'AfterExchangeInstall'
            DependsOn = '[xExchInstall]InstallExchange'
        }
    }
}
```

> [!NOTE]
> Ez a példa feltételezi, hogy konfigurálta a Local Configuration Manager újraindítások engedélyezéséhez, és továbbra is az újraindítás után a konfigurációt.

## <a name="where-to-download"></a>Letöltési helyét

Ebben a témakörben az alábbi helyeken, vagy a PowerShell-galériából által használt erőforrások töltheti le.

- [xPendingReboot](https://github.com/PowerShell/xPendingReboot)
- [xExchange](https://github.com/PowerShell/xExchange)
