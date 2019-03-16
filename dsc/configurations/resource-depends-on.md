---
ms.date: 12/12/2018
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Erőforrás-függőségek DependsOn használatával
ms.openlocfilehash: 5ea08c76c203188f41513ad0cc1f4571579b4172
ms.sourcegitcommit: caac7d098a448232304c9d6728e7340ec7517a71
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/16/2019
ms.locfileid: "58055699"
---
# <a name="resource-dependencies-using-dependson"></a>Erőforrás-függőségek DependsOn használatával

Amikor ír [konfigurációk](configurations.md), hozzáadhat [erőforrás blokkok](../resources/resources.md) konfigurálása egy cél csomópont aspektusait. Adja hozzá az erőforrás-blokkok továbbra is, mint a konfigurációk növelhető, elég nagy és kezelése nehézkes. Az egyik ilyen kihívás abban az erőforrás-blokkok alkalmazott sorrendben. Erőforrások általában a sorrendben vannak definiálva a konfigurációs belül érvényesek. Növekedésével a konfiguráció nagyobb és összetettebb, használhatja a `DependsOn` kulcs megadásával az erőforrások, amelyek egy erőforrást egy másik erőforrás függ a alkalmazott sorrendjének módosításához.

A `DependsOn` kulcs használható bármilyen erőforrás letiltása. A többi erőforrás kulcsainak azonos mechanizmusnak a kulcs/érték-van definiálva. A `DependsOn` kulcs vár a következő szintaxissal karakterláncok tömbje.

```
DependsOn = '[<Resource Type>]<Resource Name>', '[<Resource Type>]<Resource Name'
```

Az alábbi példa egy tűzfalszabály engedélyezése és a nyilvános profil konfigurálása után konfigurálja.

```powershell
# Install the NetworkingDSC module to configure firewall rules and profiles.
Install-Module -Name NetworkingDSC

Configuration ConfigureFirewall
{
    Import-DSCResource -Name Firewall, FirewallProfile
    Node localhost
    {
        Firewall Firewall
        {
            Name                  = 'IIS-WebServerRole-HTTP-In-TCP'
            Ensure                = 'Present'
            Enabled               = 'True'
            DependsOn             = '[FirewallProfile]FirewallProfilePublic'
        }

        FirewallProfile FirewallProfilePublic
        {
            Name = 'Public'
            Enabled = 'True'
            DefaultInboundAction = 'Block'
            DefaultOutboundAction = 'Allow'
            AllowInboundRules = 'True'
            AllowLocalFirewallRules = 'False'
            AllowLocalIPsecRules = 'False'
            NotifyOnListen = 'True'
            LogFileName = '%systemroot%\system32\LogFiles\Firewall\pfirewall.log'
            LogMaxSizeKilobytes = 16384
            LogAllowed = 'False'
            LogBlocked = 'True'
            LogIgnored = 'NotConfigured'
        }
    }
}

ConfigureFirewall -OutputPath C:\Temp\
```

Amikor alkalmazza a konfigurációt, a tűzfal profil mindig konfigurálja a rendszer először függetlenül attól, milyen sorrendben az erőforrás-blokkok vannak definiálva. Ha a konfigurációt alkalmaz, mindenképpen vegye figyelembe a meglévő konfiguráció, így szükség esetén visszaállíthatja célcsomópontokat.

```
PS> Start-DSCConfiguration -Verbose -Wait -Path C:\Temp\ -ComputerName localhost

VERBOSE: Perform operation 'Invoke CimMethod' with following parameters, ''methodName' = SendConfigurationApply,'className' = MSFT_DSCLocalConfigurationManager,'namespaceName' = root/Microsoft/Windows/DesiredStateConfiguration'.
VERBOSE: An LCM method call arrived from computer SERVER01 with user sid S-1-5-21-181338-0189125723-1543119021-1282804.
VERBOSE: [SERVER01]: LCM:  [ Start  Set      ]
VERBOSE: [SERVER01]:                            [DSCEngine] Importing the module C:\Program Files\WindowsPowerShell\Modules\NetworkingDsc\6.1.0.0\DscResources\MSFT_Firewall\MSFT_Firewall.psm1 in force mode.
VERBOSE: [SERVER01]:                            [DSCEngine] Importing the module C:\Program Files\WindowsPowerShell\Modules\NetworkingDsc\6.1.0.0\DscResources\MSFT_FirewallProfile\MSFT_FirewallProfile.psm1 in force mode.
VERBOSE: [SERVER01]: LCM:  [ Start  Resource ]  [[FirewallProfile]FirewallProfilePublic]
VERBOSE: [SERVER01]: LCM:  [ Start  Test     ]  [[FirewallProfile]FirewallProfilePublic]
VERBOSE: [SERVER01]:                            [[FirewallProfile]FirewallProfilePublic] Importing the module MSFT_FirewallProfile in force mode.
VERBOSE: [SERVER01]:                            [[FirewallProfile]FirewallProfilePublic] Test-TargetResource: Testing Firewall Public Profile.
VERBOSE: [SERVER01]:                            [[FirewallProfile]FirewallProfilePublic] Test-TargetResource: Firewall Public Profile "AllowInboundRules" is "NotConfigured" but should be "True". Change required.
VERBOSE: [SERVER01]:                            [[FirewallProfile]FirewallProfilePublic] Test-TargetResource: Firewall Public Profile "AllowLocalFirewallRules" is "NotConfigured" but should be "False". Change required.
VERBOSE: [SERVER01]:                            [[FirewallProfile]FirewallProfilePublic] Test-TargetResource: Firewall Public Profile "AllowLocalIPsecRules" is "NotConfigured" but should be "False". Change required.
VERBOSE: [SERVER01]:                            [[FirewallProfile]FirewallProfilePublic] Test-TargetResource: Firewall Public Profile "DefaultOutboundAction" is "NotConfigured" but should be "Allow". Change required.
VERBOSE: [SERVER01]:                            [[FirewallProfile]FirewallProfilePublic] Test-TargetResource: Firewall Public Profile "LogBlocked" is "False" but should be "True". Change required.
VERBOSE: [SERVER01]:                            [[FirewallProfile]FirewallProfilePublic] Test-TargetResource: Firewall Public Profile "LogMaxSizeKilobytes" is "4096" but should be "16384". Change required.
VERBOSE: [SERVER01]: LCM:  [ End    Test     ]  [[FirewallProfile]FirewallProfilePublic]  in 1.6890 seconds.
VERBOSE: [SERVER01]: LCM:  [ Start  Set      ]  [[FirewallProfile]FirewallProfilePublic]
VERBOSE: [SERVER01]:                            [[FirewallProfile]FirewallProfilePublic] Importing the module MSFT_FirewallProfile in force mode.
VERBOSE: [SERVER01]:                            [[FirewallProfile]FirewallProfilePublic] Set-TargetResource: Setting Firewall Public Profile.
VERBOSE: [SERVER01]:                            [[FirewallProfile]FirewallProfilePublic] Set-TargetResource: Setting Firewall Public Profile parameter AllowInboundRules to "AllowInboundRules".
VERBOSE: [SERVER01]:                            [[FirewallProfile]FirewallProfilePublic] Set-TargetResource: Setting Firewall Public Profile parameter AllowLocalFirewallRules to "AllowLocalFirewallRules".
VERBOSE: [SERVER01]:                            [[FirewallProfile]FirewallProfilePublic] Set-TargetResource: Setting Firewall Public Profile parameter AllowLocalIPsecRules to "AllowLocalIPsecRules".
VERBOSE: [SERVER01]:                            [[FirewallProfile]FirewallProfilePublic] Set-TargetResource: Setting Firewall Public Profile parameter DefaultOutboundAction to "DefaultOutboundAction".
VERBOSE: [SERVER01]:                            [[FirewallProfile]FirewallProfilePublic] Set-TargetResource: Setting Firewall Public Profile parameter LogBlocked to "LogBlocked".
VERBOSE: [SERVER01]:                            [[FirewallProfile]FirewallProfilePublic] Set-TargetResource: Setting Firewall Public Profile parameter LogMaxSizeKilobytes to "LogMaxSizeKilobytes".
VERBOSE: [SERVER01]:                            [[FirewallProfile]FirewallProfilePublic] Set-TargetResource: Setting Firewall Public Profile updated.
VERBOSE: [SERVER01]: LCM:  [ End    Set      ]  [[FirewallProfile]FirewallProfilePublic]  in 10.0360 seconds.
VERBOSE: [SERVER01]: LCM:  [ End    Resource ]  [[FirewallProfile]FirewallProfilePublic]
VERBOSE: [SERVER01]: LCM:  [ Start  Resource ]  [[Firewall]Firewall]
VERBOSE: [SERVER01]: LCM:  [ Start  Test     ]  [[Firewall]Firewall]
VERBOSE: [SERVER01]:                            [[Firewall]Firewall] Importing the module MSFT_Firewall in force mode.
VERBOSE: [SERVER01]:                            [[Firewall]Firewall] Test-TargetResource: Checking settings for firewall rule with Name 'IIS-WebServerRole-HTTP-In-TCP'.
VERBOSE: [SERVER01]:                            [[Firewall]Firewall] Test-TargetResource: Find firewall rule with Name 'IIS-WebServerRole-HTTP-In-TCP'.
VERBOSE: [SERVER01]:                            [[Firewall]Firewall] Get-FirewallRule: No Firewall Rule found with Name 'IIS-WebServerRole-HTTP-In-TCP'.
VERBOSE: [SERVER01]:                            [[Firewall]Firewall] Test-TargetResource: Firewall rule with Name 'IIS-WebServerRole-HTTP-In-TCP' does not exist.
VERBOSE: [SERVER01]:                            [[Firewall]Firewall] Test-TargetResource: Check Firewall rule with Name 'IIS-WebServerRole-HTTP-In-TCP' returning False.
VERBOSE: [SERVER01]: LCM:  [ End    Test     ]  [[Firewall]Firewall]  in 1.1780 seconds.
VERBOSE: [SERVER01]: LCM:  [ Start  Set      ]  [[Firewall]Firewall]
VERBOSE: [SERVER01]:                            [[Firewall]Firewall] Importing the module MSFT_Firewall in force mode.
VERBOSE: [SERVER01]:                            [[Firewall]Firewall] Set-TargetResource: Applying settings for firewall rule with Name 'IIS-WebServerRole-HTTP-In-TCP'.
VERBOSE: [SERVER01]:                            [[Firewall]Firewall] Set-TargetResource: Find firewall rule with Name 'IIS-WebServerRole-HTTP-In-TCP'.
VERBOSE: [SERVER01]:                            [[Firewall]Firewall] Get-FirewallRule: No Firewall Rule found with Name 'IIS-WebServerRole-HTTP-In-TCP'.
VERBOSE: [SERVER01]:                            [[Firewall]Firewall] Set-TargetResource: We want the firewall rule with Name 'IIS-WebServerRole-HTTP-In-TCP' to exist since Ensure is set to Present.
VERBOSE: [SERVER01]:                            [[Firewall]Firewall] Set-TargetResource: We want the firewall rule with Name 'IIS-WebServerRole-HTTP-In-TCP' to exist, but it does not.
VERBOSE: [SERVER01]:                            [[Firewall]Firewall] New-NetFirewallRule DisplayName: IIS-WebServerRole-HTTP-In-TCP
VERBOSE: [SERVER01]: LCM:  [ End    Set      ]  [[Firewall]Firewall]  in 1.0850 seconds.
VERBOSE: [SERVER01]: LCM:  [ End    Resource ]  [[Firewall]Firewall]
VERBOSE: [SERVER01]: LCM:  [ End    Set      ]
VERBOSE: [SERVER01]: LCM:  [ End    Set      ]    in  15.2880 seconds.
VERBOSE: Operation 'Invoke CimMethod' complete.
VERBOSE: Time taken for configuration job to complete is 15.385 seconds
```

Ez biztosítja, hogy ha a **FirewallProfile** erőforrás bármilyen okból nem sikerül a **tűzfal** letiltása nem hajtja végre, annak ellenére, hogy először van definiálva. A `DependsOn` kulcs lehetővé teszi, hogy a nagyobb rugalmasság a csoportosítási erőforrás-címblokkokat, és annak biztosítására, hogy függőségek megoldott erőforrás végrehajtása előtt.

Speciális konfigurációk esetében is használhatja [csomópont közötti függőségi](crossNodeDependencies.md) , hogy még pontosabb szabályozást (például annak biztosítása, a tartományvezérlő előtt az ügyfél csatlakoztatása a tartományhoz van konfigurálva).

## <a name="cleaning-up"></a>Karbantartása

Ha a fenti konfigurációs telepítette, megfordíthatja kulcsokat végrehajtott esetleges módosításokat visszavonni. A fenti példában, a beállítás a **engedélyezve** hamis kulcs letiltja a tűzfalszabályt, és a profil. A példában a cél csomópont előző konfigurált állapota megfelelő igény szerint kell módosítania.

```powershell
        Firewall Firewall
        {
            Name                  = 'IIS-WebServerRole-HTTP-In-TCP'
            Enabled               = 'False'
            DependsOn             = '[FirewallProfile]FirewallProfilePublic'
        }

        FirewallProfile FirewallProfilePublic
        {
            Name = 'Public'
            Enabled = 'False'
        }
```

## <a name="see-also"></a>Lásd még:

- [A csomópontok közötti függőségek használata](./crossNodeDependencies.md)
