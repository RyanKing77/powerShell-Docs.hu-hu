---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: A DSC futtatása felhasználói hitelesítő adatokkal
ms.openlocfilehash: 37e6ff64c9c6d3960653d417e22a6c93c653230c
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="running-dsc-with-user-credentials"></a>A DSC futtatása felhasználói hitelesítő adatokkal

> Vonatkozik: A Windows PowerShell 5.0, 5.1 Windows PowerShell

A DSC-erőforrásra a hitelesítő adatok egy megadott készlet automatikus futtathatja **PsDscRunAsCredential** tulajdonság a konfigurációban.
Alapértelmezés szerint a DSC-ből az egyes erőforrások fiókként fut, a rendszer.
Vannak olyan helyzetek, amikor egy felhasználó szükség, például az MSI-csomagok telepítése egy adott felhasználó környezetében, a felhasználó beállításkulcsok, a felhasználó helyi könyvtárba való hozzáférés vagy a hálózathoz hozzáférő futó megosztani.

Minden DSC erőforrás rendelkezik egy **PsDscRunAsCredential** tulajdonság, amely a felhasználói hitelesítő adatok állítható be (egy [PSCredential](https://msdn.microsoft.com/library/ms572524(v=VS.85).aspx) objektum).
A hitelesítő adatokat is kódolt a konfigurációban a tulajdonság értékeként, vagy állíthat be az érték [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx), amely fogja kérni a felhasználót a hitelesítő adatokat, ha a konfiguráció fordítása történik (További információ konfiguráció fordítása, lásd: [konfigurációk](configurations.md).

>**Megjegyzés:** PowerShell 5.0, használja a **PsDscRunAsCredential** összetett erőforrások hívása konfigurációk tulajdonság nem támogatott.
>A PowerShell 5.1 a **PsDscRunAsCredential** tulajdonság támogatott konfigurációk összetett erőforrások hívja.

>**Megjegyzés:** a **PsDscRunAsCredential** tulajdonság nem érhető el a PowerShell 4.0-s verzióját.

A következő példában **Get-Credential** segítségével a felhasználók hitelesítő adatainak kéréséhez.
A [beállításjegyzék](registryResource.md) erőforrás használatával módosíthatja a beállításkulcsot, amely meghatározza a Windows parancssori ablakban háttérszínét.

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
>**Megjegyzés:** Ez a példa feltételezi, hogy rendelkezik-e egy érvényes tanúsítványt, `C:\publicKeys\targetNode.cer`, és hogy a tanúsítvány ujjlenyomatát érték.
>További információ a DSC-konfiguráció MOF-fájlok a hitelesítő adatok titkosítása: [biztonságossá tétele a MOF-fájlt](secureMOF.md).