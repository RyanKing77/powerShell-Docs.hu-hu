---
ms.date: 12/12/2018
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Csomópontok közötti függőségek megadása
ms.openlocfilehash: 1bdfbd9f8a94809d6bf410eff525e1c877fb6aad
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62080203"
---
# <a name="specifying-cross-node-dependencies"></a>Csomópontok közötti függőségek megadása

> A következőkre vonatkozik: Windows PowerShell 5.0

DSC biztosít speciális erőforrások **WaitForAll**, **WaitForAny**, és **WaitForSome** , amely használható a konfigurációkban függőségeinek megadása a további beállításai csomópontok. Ezek az erőforrások viselkedését a következőképpen történik:

- **WaitForAll**: Sikeres lesz, ha az adott erőforrás az összes, meghatározott cél csomóponton a kívánt állapotban van a **csomópontnév** tulajdonság.
- **WaitForAny**: Sikeres lesz, ha a megadott erőforrás legalább az egyik a célcsomópontokat, meghatározott a kívánt állapotban van a **csomópontnév** tulajdonság.
- **WaitForSome**: Megadja egy **NodeCount** tulajdonság mellett egy **csomópontnév** tulajdonság. Az erőforrás sikeres lesz, ha az erőforrás a kívánt állapotban lévő csomópontok minimális száma (által megadott **NodeCount**) által meghatározott a **csomópontnév** tulajdonság.

## <a name="syntax"></a>Szintaxis

A **WaitForAll** és **WaitForAny** erőforrások megosztása ugyanazt a szintaxist. Cserélje le \<ResourceType\> -t az alábbi példában **WaitForAny** vagy **WaitForAll**.
Például a **DependsOn** kulcsszó, szüksége lesz a nevet a következőként: "[ResourceType] ResourceName" formátumban. Ha az erőforrás tartozik egy külön [konfigurációs](configurations.md), például a **ConfigurationName** a formázott karakterlánc "[ResourceType] ResourceName:: [ConfigurationName]:: [ConfigurationName]". A **csomópontnév** a számítógép vagy a csomópont, amelyen az aktuális erőforrás várnia kell.

```
<ResourceType> [string] #ResourceName
{
    ResourceName = [string]
    NodeName = [string]
    [ DependsOn = [string[]] ]
    [ PsDscRunAsCredential = [PSCredential]]
    [ RetryCount = [Uint32] ]
    [ RetryIntervalSec = [Uint64] ]
    [ ThrottleLimit = [Uint32]]
}
```

A **WaitForSome** erőforrás a fenti példában egy hasonló szintaxissal rendelkezik, de hozzáadja a **NodeCount** kulcsot. A **NodeCount** azt jelzi, hogy a várjon az aktuális erőforrás hány csomóponttal.

```
WaitForSome [String] #ResourceName
{
    NodeCount = [UInt32]
    NodeName = [string[]]
    ResourceName = [string]
    [DependsOn = [string[]]]
    [PsDscRunAsCredential = [PSCredential]]
    [RetryCount = [UInt32]]
    [RetryIntervalSec = [UInt64]]
    [ThrottleLimit = [UInt32]]
}
```

Az összes **WaitForXXXX** az alábbi szintaxissal kulcsok megoszthatja.

|  Vlastnost |}  Leírás || RetryIntervalSec |} Mielőtt újra próbálkozna másodpercek számát. Minimum: 1. |} | RetryCount |} Az újrapróbálkozások maximális számát. |} | ThrottleLimit |} Egyidejű csatlakozás gépek száma. Alapértelmezett érték a `New-CimSession` alapértelmezett. |} |} DependsOn |} Azt jelzi, hogy a konfigurációt egy másik erőforrás futtatnia kell, mielőtt az erőforrás konfigurálva van. További információkért lásd: [DependsOn](resource-depends-on.md)|| PsDscRunAsCredential |} Lásd: [DSC használata a felhasználói hitelesítő adatok](./runAsUser.md) |


## <a name="using-waitforxxxx-resources"></a>WaitForXXXX erőforrások használata

Minden egyes **WaitForXXXX** erőforrás megvárja, amíg befejeződik a megadott csomópont a megadott erőforrások. Ugyanazt a konfigurációt más erőforrások is majd *függenek* a **WaitForXXXX** erőforrást a **DependsOn** kulcsot.

Például a következő konfigurációban a célcsomópont várakozik a **xADDomain** erőforrás a befejezéséhez a **MyDC** legfeljebb 30-csomópont újrapróbálkozik, 15 másodperces intervallumon előtt a Célcsomópont csatlakozhat a tartományhoz.

```powershell
Configuration JoinDomain
{
    Import-DscResource -Module xComputerManagement, xActiveDirectory

    Node myDC
    {
        WindowsFeature InstallAD
        {
            Ensure = 'Present'
            Name = 'AD-Domain-Services'
        }

        xADDomain NewDomain
        {
            DomainName = 'Contoso.com'
            DomainAdministratorCredential = (Get-Credential)
            SafemodeAdministratorPassword = (Get-Credential)
            DatabasePath = "C:\Windows\NTDS"
            LogPath = "C:\Windows\NTDS"
            SysvolPath = "C:\Windows\Sysvol"
        }
    }

    Node myDomainJoinedServer
    {
        WaitForAll DC
        {
            ResourceName      = '[xADDomain]NewDomain'
            NodeName          = 'MyDC'
            RetryIntervalSec  = 15
            RetryCount        = 30
        }

        xComputer JoinDomain
        {
            Name             = 'myPC'
            DomainName       = 'Contoso.com'
            Credential       = (Get-Credential)
            DependsOn        ='[WaitForAll]DC'
        }
    }
}
```

Konfiguráció fordítása, amikor két ".mof" fájlok jönnek létre. ".Mof" fájlok egyaránt vonatkozik a célcsomópontokat, használja a [Start-DSCConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration) parancsmag

>**Megjegyzés:** A WaitForXXX alapértelmezés szerint az erőforrások próbálja meg egyszer, és akkor sikertelen. Bár ez nem szükséges, általában célszerű adjon meg egy **RetryCount** és **RetryIntervalSec**.

## <a name="see-also"></a>Lásd még:

- [DSC-konfigurációk](configurations.md)
- [Erőforrás-függőségek használatára](resource-depends-on.md)
- [DSC-erőforrások](../resources/resources.md)
- [A helyi Configuration Manager](../managing-nodes/metaConfig.md)
