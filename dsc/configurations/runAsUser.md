---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC-erőforrások hitelesítő adatok használata
ms.openlocfilehash: af54c286ce744cd7db0b0e2d05087f60cdf1a33c
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404351"
---
# <a name="use-credentials-with-dsc-resources"></a><span data-ttu-id="d563e-103">DSC-erőforrások hitelesítő adatok használata</span><span class="sxs-lookup"><span data-stu-id="d563e-103">Use Credentials with DSC Resources</span></span>

> <span data-ttu-id="d563e-104">Érvényes: Windows PowerShell 5.0, 5.1 Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="d563e-104">Applies To: Windows PowerShell 5.0, Windows PowerShell 5.1</span></span>

<span data-ttu-id="d563e-105">Az automatikus használatával futtathatja egy meghatározott hitelesítő adatokat a DSC erőforrás **PsDscRunAsCredential** tulajdonság a konfigurációban.</span><span class="sxs-lookup"><span data-stu-id="d563e-105">You can run a DSC resource under a specified set of credentials by using the automatic **PsDscRunAsCredential** property in the configuration.</span></span>
<span data-ttu-id="d563e-106">Alapértelmezés szerint DSC fut az egyes erőforrások a system fiók.</span><span class="sxs-lookup"><span data-stu-id="d563e-106">By default, DSC runs each resource as the system account.</span></span>
<span data-ttu-id="d563e-107">Vannak olyan helyzetek, amikor egy felhasználó szükség, például az MSI-csomagok telepítése egy adott felhasználó környezetében, a felhasználó beállításkulcsokat, egy felhasználó adott helyi könyvtár eléréséhez vagy hálózat elérése futó megosztása.</span><span class="sxs-lookup"><span data-stu-id="d563e-107">There are times when running as a user is necessary, such as installing MSI packages in a specific user context, setting a user's registry keys, accessing a user's specific local directory, or accessing a network share.</span></span>

<span data-ttu-id="d563e-108">Minden DSC-erőforrás rendelkezik egy **PsDscRunAsCredential** tulajdonságot, amely értékre lehet beállítani a felhasználói hitelesítő adatokat (a [PSCredential](/dotnet/api/system.management.automation.pscredential) objektumot).</span><span class="sxs-lookup"><span data-stu-id="d563e-108">Every DSC resource has a **PsDscRunAsCredential** property that can be set to any user credentials (a [PSCredential](/dotnet/api/system.management.automation.pscredential) object).</span></span>
<span data-ttu-id="d563e-109">A hitelesítő adat lehet, változtatható a konfigurációban a tulajdonság értékét, vagy és megadható az érték [Get-Credential](/powershell/module/Microsoft.PowerShell.Security/Get-Credential), amely fogja kérni a felhasználót a hitelesítő adatait, ha a konfiguráció fordítása (További információ konfiguráció fordítása, lásd: [konfigurációk](configurations.md).</span><span class="sxs-lookup"><span data-stu-id="d563e-109">The credential can be hard-coded as the value of the property in the configuration, or you can set the value to [Get-Credential](/powershell/module/Microsoft.PowerShell.Security/Get-Credential), which will prompt the user for a credential when the configuration is compiled (for information about compiling configurations, see [Configurations](configurations.md).</span></span>

> [!NOTE]
> <span data-ttu-id="d563e-110">A PowerShell 5.0-s használata a **PsDscRunAsCredential** összetett erőforrások hívása konfigurációkban tulajdonság nem támogatott.</span><span class="sxs-lookup"><span data-stu-id="d563e-110">In PowerShell 5.0, using the **PsDscRunAsCredential** property in configurations calling composite resources was not supported.</span></span>
> <span data-ttu-id="d563e-111">A PowerShell 5.1-es a **PsDscRunAsCredential** tulajdonság támogatott konfigurációk összetett erőforrások hívásakor.</span><span class="sxs-lookup"><span data-stu-id="d563e-111">In PowerShell 5.1, the **PsDscRunAsCredential** property is supported in configurations calling composite resources.</span></span>
> <span data-ttu-id="d563e-112">A **PsDscRunAsCredential** tulajdonság nem érhető el a PowerShell 4.0-s verzióját.</span><span class="sxs-lookup"><span data-stu-id="d563e-112">The **PsDscRunAsCredential** property is not available in PowerShell 4.0.</span></span>

<span data-ttu-id="d563e-113">A következő példában `Get-Credential` kéri a felhasználótól a hitelesítő adatok segítségével.</span><span class="sxs-lookup"><span data-stu-id="d563e-113">In the following example, `Get-Credential` is used to prompt the user for credentials.</span></span>
<span data-ttu-id="d563e-114">A **beállításjegyzék** erőforrás segítségével módosíthatja a beállításkulcsot, amely meghatározza a Windows parancssori ablakban háttérszíne.</span><span class="sxs-lookup"><span data-stu-id="d563e-114">The **Registry** resource is used to change the registry key that specifies the background color for the Windows command prompt window.</span></span>

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
> <span data-ttu-id="d563e-115">Ez a példa feltételezi, hogy rendelkezik-e egy érvényes tanúsítványt, `C:\publicKeys\targetNode.cer`, és hogy a tanúsítvány ujjlenyomatának érték.</span><span class="sxs-lookup"><span data-stu-id="d563e-115">This example assumes that you have a valid certificate at `C:\publicKeys\targetNode.cer`, and that the thumbprint of that certificate is the value shown.</span></span>
> <span data-ttu-id="d563e-116">További információ a DSC-konfiguráció MOF-fájlok a hitelesítő adatok titkosítása: [a MOF-fájl biztonságossá tétele](../pull-server/secureMOF.md).</span><span class="sxs-lookup"><span data-stu-id="d563e-116">For information about encrypting credentials in DSC configuration MOF files, see [Securing the MOF file](../pull-server/secureMOF.md).</span></span>
