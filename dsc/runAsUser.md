---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: A DSC futtatása felhasználói hitelesítő adatokkal
ms.openlocfilehash: 4a6c3d8b561cd0a27be07a68f1b577f7bf764254
ms.sourcegitcommit: 8b076ebde7ef971d7465bab834a3c2a32471ef6f
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/06/2018
ms.locfileid: "37893909"
---
# <a name="running-dsc-with-user-credentials"></a>A DSC futtatása felhasználói hitelesítő adatokkal

> A következőkre vonatkozik: Windows PowerShell 5.0, 5.1 Windows PowerShell

Az automatikus használatával futtathatja egy meghatározott hitelesítő adatokat a DSC erőforrás **PsDscRunAsCredential** tulajdonság a konfigurációban.
Alapértelmezés szerint DSC fut az egyes erőforrások a system fiók.
Vannak olyan helyzetek, amikor egy felhasználó szükség, például az MSI-csomagok telepítése egy adott felhasználó környezetében, a felhasználó beállításkulcsokat, egy felhasználó adott helyi könyvtár eléréséhez vagy hálózat elérése futó megosztása.

Minden DSC-erőforrás rendelkezik egy **PsDscRunAsCredential** tulajdonságot, amely értékre lehet beállítani a felhasználói hitelesítő adatokat (a [PSCredential](/dotnet/api/system.management.automation.pscredential) objektumot).
A hitelesítő adat lehet, változtatható a konfigurációban a tulajdonság értékét, vagy és megadható az érték [Get-Credential](/powershell/module/Microsoft.PowerShell.Security/Get-Credential), amely fogja kérni a felhasználót a hitelesítő adatait, ha a konfiguráció fordítása (További információ konfiguráció fordítása, lásd: [konfigurációk](configurations.md).

> [!NOTE] 
> A PowerShell 5.0-s használata a **PsDscRunAsCredential** összetett erőforrások hívása konfigurációkban tulajdonság nem támogatott.
> A PowerShell 5.1-es a **PsDscRunAsCredential** tulajdonság támogatott konfigurációk összetett erőforrások hívásakor.
> A **PsDscRunAsCredential** tulajdonság nem érhető el a PowerShell 4.0-s verzióját.

A következő példában `Get-Credential` kéri a felhasználótól a hitelesítő adatok segítségével.
A [beállításjegyzék](registryResource.md) erőforrás segítségével módosíthatja a beállításkulcsot, amely meghatározza a Windows parancssori ablakban háttérszíne.

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
> Ez a példa feltételezi, hogy rendelkezik-e egy érvényes tanúsítványt, `C:\publicKeys\targetNode.cer`, és hogy a tanúsítvány ujjlenyomatának érték.
> További információ a DSC-konfiguráció MOF-fájlok a hitelesítő adatok titkosítása: [a MOF-fájl biztonságossá tétele](secureMOF.md).
