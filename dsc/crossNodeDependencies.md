---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "Kereszt-csomópont függőségeinek megadása"
ms.openlocfilehash: f4411161d819d96803f57600646409d5bfe827b9
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 01/17/2018
---
# <a name="specifying-cross-node-dependencies"></a>Kereszt-csomópont függőségeinek megadása

> Vonatkozik: A Windows PowerShell 5.0

A DSC különleges forrásanyagokat biztosít az **WaitForAll**, **WaitForAny**, és **WaitForSome** , amely használható a konfigurációk függőségek határozza meg az egyéb konfigurációk csomópontok. Ezeket az erőforrásokat viselkedése a következőképpen történik:

* **WaitForAll**: sikeres lesz, ha a megadott erőforrás definiált összes cél csomóponton megfelelő állapotban a **csomópontnév** tulajdonság.
* **WaitForAny**: sikeres lesz, ha a megadott erőforrás a célcsomópontokat definiált legalább egyikének megfelelő állapotban a **csomópontnév** tulajdonság.
* **WaitForSome**: Adja meg a **NodeCount** kívül tulajdonságának egy **csomópontnév** tulajdonság. Az erőforrás sikeres lesz, ha az erőforrás a megfelelő állapotban a csomópontok minimális száma (által megadott **NodeCount**) határozzák meg a **csomópontnév** tulajdonság. 

## <a name="using-waitforxxxx-resources"></a>WaitForXXXX erőforrások használata

Használatához a **WaitForXXXX** erőforrások, létrehozhat egy erőforrás adatblokk, amelyben a DSC-erőforrás és a csomópontokon történő várakozás az erőforrás típusát. Ezután a **DependsOn** bármely egyéb erőforrásokat a tulajdonság a konfigurációját, és várja meg a megadott feltételek tárolt metaadatblokkok a **WaitForXXXX** sikeres csomópont.

Például a következő konfiguráció célcsomóponton arra vár, hogy a **xADDomain** erőforrás a befejezéséhez a **MyDC** legfeljebb 30-csomópont újrapróbálkozik, 15 másodperces időközönként, mielőtt a célcsomóponttal csatlakozhat a tartományhoz.

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

>**Megjegyzés:** a WaitForXXX alapértelmezés szerint erőforrások próbálja egyszer, és akkor sikertelen. Bár nem kötelező, általában célszerű a újrapróbálkozási időköz és számának megadása.

## <a name="see-also"></a>Lásd még:
* [A DSC-konfigurációk](configurations.md)
* [A DSC-erőforrások](resources.md)
* [A helyi Configuration Manager konfigurálása](metaConfig.md)

