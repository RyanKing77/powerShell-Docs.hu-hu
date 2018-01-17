---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "Felhasználói hitelesítő adatokkal DSC fut"
ms.openlocfilehash: 7b57732679e4fb29112a3ca7fe64cba2bda67207
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 01/17/2018
---
# <a name="running-dsc-with-user-credentials"></a>Felhasználói hitelesítő adatokkal DSC fut 

> Vonatkozik: A Windows PowerShell 5.0, 5.1 Windows PowerShell

A DSC-erőforrásra a hitelesítő adatok egy megadott készlet automatikus futtathatja **PsDscRunAsCredential** tulajdonság a konfigurációban. Alapértelmezés szerint a DSC-ből az egyes erőforrások fiókként fut, a rendszer.
Vannak olyan helyzetek, amikor egy felhasználó szükség, például az MSI-csomagok telepítése egy adott felhasználó környezetében, a felhasználó beállításkulcsok, a felhasználó helyi könyvtárba való hozzáférés vagy a hálózathoz hozzáférő futó megosztani.

Minden DSC erőforrás rendelkezik egy **PsDscRunAsCredential** tulajdonság, amely a felhasználói hitelesítő adatok állítható be (egy [PSCredential](https://msdn.microsoft.com/en-us/library/ms572524(v=VS.85).aspx) objektum).
A hitelesítő adatokat is kódolt a konfigurációban a tulajdonság értékeként, vagy állíthat be az érték [Get-Credential](https://technet.microsoft.com/en-us/library/hh849815.aspx), amely fogja kérni a felhasználót a hitelesítő adatokat, ha a konfiguráció fordítása történik (További információ konfiguráció fordítása, lásd: [konfigurációk](configurations.md).

>**Megjegyzés:** PowerShell 5.0, használja a **PsDscRunAsCredential** összetett erőforrások hívása konfigurációk tulajdonság nem támogatott. 
>A PowerShell 5.1 a **PsDscRunAsCredential** tulajdonság támogatott konfigurációk összetett erőforrások hívja.

>**Megjegyzés:** a **PsDscRunAsCredential** tulajdonság nem érhető el a PowerShell 4.0-s verzióját.

A következő példában **Get-Credential** segítségével a felhasználók hitelesítő adatainak kéréséhez. A [beállításjegyzék](registryResource.md) erőforrás használatával módosíthatja a beállításkulcsot, amely meghatározza a Windows parancssori ablakban háttérszínét.

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

