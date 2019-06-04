---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Hitelesítő adatok használata DSC-erőforrásokkal
ms.openlocfilehash: fea2e3cad8d081c17853e127203f1d40d98c5de2
ms.sourcegitcommit: bc42c9166857147a1ecf9924b718d4a48eb901e3
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/03/2019
ms.locfileid: "66470763"
---
# <a name="use-credentials-with-dsc-resources"></a>Hitelesítő adatok használata DSC-erőforrásokkal

> Érvényes: Windows PowerShell 5.0, 5.1 Windows PowerShell

Az automatikus használatával futtathatja egy meghatározott hitelesítő adatokat a DSC erőforrás **PsDscRunAsCredential** tulajdonság a konfigurációban. Alapértelmezés szerint DSC fut az egyes erőforrások a system fiók. Vannak olyan helyzetek, amikor egy felhasználó szükség, például az MSI-csomagok telepítése egy adott felhasználó környezetében, a felhasználó beállításkulcsokat, egy felhasználó adott helyi könyvtár eléréséhez vagy hálózat elérése futó megosztása. A **SeInteractiveLogonRight** szükséges, a célgépen, adja meg, hogy minden olyan fiók **PSDSCRunAsCredential**. További információkért lásd: [fiók jogokat állandók](/windows/desktop/secauthz/account-rights-constants).

Minden DSC-erőforrás rendelkezik egy **PsDscRunAsCredential** tulajdonságot, amely értékre lehet beállítani a felhasználói hitelesítő adatokat (a [PSCredential](/dotnet/api/system.management.automation.pscredential) objektumot). A hitelesítő adat lehet, változtatható a konfigurációban a tulajdonság értékét, vagy és megadható az érték [Get-Credential](/powershell/module/Microsoft.PowerShell.Security/Get-Credential), amely fogja kérni a felhasználót a hitelesítő adatait, ha a konfiguráció fordítása (További információ konfiguráció fordítása, lásd: [konfigurációk](configurations.md).

> [!NOTE]
> A PowerShell 5.0-s használata a **PsDscRunAsCredential** összetett erőforrások hívása konfigurációkban tulajdonság nem támogatott. A PowerShell 5.1-es a **PsDscRunAsCredential** tulajdonság támogatott konfigurációk összetett erőforrások hívásakor. A **PsDscRunAsCredential** tulajdonság nem érhető el a PowerShell 4.0-s verzióját.

A következő példában `Get-Credential` kéri a felhasználótól a hitelesítő adatok segítségével. A **beállításjegyzék** erőforrás segítségével módosíthatja a beállításkulcsot, amely meghatározza a Windows parancssori ablakban háttérszíne.

```powershell
Configuration ChangeCmdBackGroundColor
{
    Import-DscResource -ModuleName PSDesiredStateConfiguration

    Node $AllNodes.NodeName
    {
        Registry CmdPath
        {
            Key                  = 'HKEY_CURRENT_USER\SOFTWARE\Microsoft\Command Processor'
            ValueName            = 'DefaultColor'
            ValueData            = '1F'
            ValueType            = 'DWORD'
            Ensure               = 'Present'
            Force                = $true
            Hex                  = $true
            PsDscRunAsCredential = Get-Credential
        }
    }
}

$configData = @{
    AllNodes = @(
        @{
            NodeName             = 'localhost';
            PSDscAllowDomainUser = $true
            CertificateFile      = 'C:\publicKeys\targetNode.cer'
            Thumbprint           = '7ee7f09d-4be0-41aa-a47f-96b9e3bdec25'
        }
    )
}

ChangeCmdBackGroundColor -ConfigurationData $configData
```

> [!NOTE]
> Ez a példa feltételezi, hogy rendelkezik-e egy érvényes tanúsítványt, `C:\publicKeys\targetNode.cer`, és hogy a tanúsítvány ujjlenyomatának érték. További információ a DSC-konfiguráció MOF-fájlok a hitelesítő adatok titkosítása: [a MOF-fájl biztonságossá tétele](../pull-server/secureMOF.md).
