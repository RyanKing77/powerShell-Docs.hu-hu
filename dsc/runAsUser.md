---
ms.date: 06/12/2017
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: A DSC futtatása felhasználói hitelesítő adatokkal
ms.openlocfilehash: b2992ad562dea375aba980611312c7b96a23189c
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/16/2018
ms.locfileid: "34189703"
---
# <a name="running-dsc-with-user-credentials"></a><span data-ttu-id="cf4c0-103">A DSC futtatása felhasználói hitelesítő adatokkal</span><span class="sxs-lookup"><span data-stu-id="cf4c0-103">Running DSC with user credentials</span></span>

> <span data-ttu-id="cf4c0-104">Vonatkozik: A Windows PowerShell 5.0, 5.1 Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="cf4c0-104">Applies To: Windows PowerShell 5.0, Windows PowerShell 5.1</span></span>

<span data-ttu-id="cf4c0-105">A DSC-erőforrásra a hitelesítő adatok egy megadott készlet automatikus futtathatja **PsDscRunAsCredential** tulajdonság a konfigurációban.</span><span class="sxs-lookup"><span data-stu-id="cf4c0-105">You can run a DSC resource under a specified set of credentials by using the automatic **PsDscRunAsCredential** property in the configuration.</span></span>
<span data-ttu-id="cf4c0-106">Alapértelmezés szerint a DSC-ből az egyes erőforrások fiókként fut, a rendszer.</span><span class="sxs-lookup"><span data-stu-id="cf4c0-106">By default, DSC runs each resource as the system account.</span></span>
<span data-ttu-id="cf4c0-107">Vannak olyan helyzetek, amikor egy felhasználó szükség, például az MSI-csomagok telepítése egy adott felhasználó környezetében, a felhasználó beállításkulcsok, a felhasználó helyi könyvtárba való hozzáférés vagy a hálózathoz hozzáférő futó megosztani.</span><span class="sxs-lookup"><span data-stu-id="cf4c0-107">There are times when running as a user is necessary, such as installing MSI packages in a specific user context, setting a user's registry keys, accessing a user's specific local directory, or accessing a network share.</span></span>

<span data-ttu-id="cf4c0-108">Minden DSC erőforrás rendelkezik egy **PsDscRunAsCredential** tulajdonság, amely a felhasználói hitelesítő adatok állítható be (egy [PSCredential](https://msdn.microsoft.com/library/ms572524(v=VS.85).aspx) objektum).</span><span class="sxs-lookup"><span data-stu-id="cf4c0-108">Every DSC resource has a **PsDscRunAsCredential** property that can be set to any user credentials (a [PSCredential](https://msdn.microsoft.com/library/ms572524(v=VS.85).aspx) object).</span></span>
<span data-ttu-id="cf4c0-109">A hitelesítő adatokat is kódolt a konfigurációban a tulajdonság értékeként, vagy állíthat be az érték [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx), amely fogja kérni a felhasználót a hitelesítő adatokat, ha a konfiguráció fordítása történik (További információ konfiguráció fordítása, lásd: [konfigurációk](configurations.md).</span><span class="sxs-lookup"><span data-stu-id="cf4c0-109">The credential can be hard-coded as the value of the property in the configuration, or you can set the value to [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx), which will prompt the user for a credential when the configuration is compiled (for information about compiling configurations, see [Configurations](configurations.md).</span></span>

><span data-ttu-id="cf4c0-110">**Megjegyzés:** PowerShell 5.0, használja a **PsDscRunAsCredential** összetett erőforrások hívása konfigurációk tulajdonság nem támogatott.</span><span class="sxs-lookup"><span data-stu-id="cf4c0-110">**Note:** In PowerShell 5.0, using the **PsDscRunAsCredential** property in configurations calling composite resources was not supported.</span></span>
><span data-ttu-id="cf4c0-111">A PowerShell 5.1 a **PsDscRunAsCredential** tulajdonság támogatott konfigurációk összetett erőforrások hívja.</span><span class="sxs-lookup"><span data-stu-id="cf4c0-111">In PowerShell 5.1, the **PsDscRunAsCredential** property is supported in configurations calling composite resources.</span></span>

><span data-ttu-id="cf4c0-112">**Megjegyzés:** a **PsDscRunAsCredential** tulajdonság nem érhető el a PowerShell 4.0-s verzióját.</span><span class="sxs-lookup"><span data-stu-id="cf4c0-112">**Note:** The **PsDscRunAsCredential** property is not available in PowerShell 4.0.</span></span>

<span data-ttu-id="cf4c0-113">A következő példában **Get-Credential** segítségével a felhasználók hitelesítő adatainak kéréséhez.</span><span class="sxs-lookup"><span data-stu-id="cf4c0-113">In the following example, **Get-Credential** is used to prompt the user for credentials.</span></span>
<span data-ttu-id="cf4c0-114">A [beállításjegyzék](registryResource.md) erőforrás használatával módosíthatja a beállításkulcsot, amely meghatározza a Windows parancssori ablakban háttérszínét.</span><span class="sxs-lookup"><span data-stu-id="cf4c0-114">The [Registry](registryResource.md) resource is used to change the registry key that specifies the background color for the Windows command prompt window.</span></span>

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
><span data-ttu-id="cf4c0-115">**Megjegyzés:** Ez a példa feltételezi, hogy rendelkezik-e egy érvényes tanúsítványt, `C:\publicKeys\targetNode.cer`, és hogy a tanúsítvány ujjlenyomatát érték.</span><span class="sxs-lookup"><span data-stu-id="cf4c0-115">**Note:** This example assumes that you have a valid certificate at `C:\publicKeys\targetNode.cer`, and that the thumbprint of that certificate is the value shown.</span></span>
><span data-ttu-id="cf4c0-116">További információ a DSC-konfiguráció MOF-fájlok a hitelesítő adatok titkosítása: [biztonságossá tétele a MOF-fájlt](secureMOF.md).</span><span class="sxs-lookup"><span data-stu-id="cf4c0-116">For information about encrypting credentials in DSC configuration MOF files, see [Securing the MOF file](secureMOF.md).</span></span>