---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 3acd266a75bc61ffe4bce467cfb804ac7865c629
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62057247"
---
# <a name="creating-and-connecting-to-a-jea-endpoint"></a><span data-ttu-id="d6fb5-102">JEA-végpont létrehozása és csatlakozás a végponthoz</span><span class="sxs-lookup"><span data-stu-id="d6fb5-102">Creating and Connecting to a JEA Endpoint</span></span>

<span data-ttu-id="d6fb5-103">A JEA-végpont létrehozása, létrehozhat és regisztrálhat egy speciálisan konfigurált PowerShell-munkamenet konfigurációs fájlt, amely készíthet szeretne a **New-PSSessionConfigurationFile** parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="d6fb5-103">To create a JEA endpoint, you need to create and register a specially-configured PowerShell Session Configuration file, which can be generated with the **New-PSSessionConfigurationFile** cmdlet.</span></span>

```powershell
New-PSSessionConfigurationFile -SessionType RestrictedRemoteServer -TranscriptDirectory "C:\ProgramData\JEATranscripts" -RunAsVirtualAccount -RoleDefinitions @{ 'CONTOSO\NonAdmin_Operators' = @{ RoleCapabilities = 'Maintenance' }} -Path "$env:ProgramData\JEAConfiguration\Demo.pssc"
```

<span data-ttu-id="d6fb5-104">Ezzel létrehoz egy munkamenet-konfigurációs fájlt a következőhöz hasonló:</span><span class="sxs-lookup"><span data-stu-id="d6fb5-104">This will create a session configuration file that looks like this:</span></span>

```powershell
@{

    # Version number of the schema used for this document
    SchemaVersion = '2.0.0.0'

    # ID used to uniquely identify this document
    GUID = 'a384fdd3-5830-4a2c-ac86-cdd1822c3afd'

    # Author of this document
    Author = 'Administrator'

    # Description of the functionality provided by these settings
    # Description = ''

    # Session type defaults to apply for this session configuration. Can be 'RestrictedRemoteServer' (recommended), 'Empty', or 'Default'
    SessionType = 'RestrictedRemoteServer'

    # Directory to place session transcripts for this session configuration
    TranscriptDirectory = 'C:\ProgramData\JEATranscripts'

    # Whether to run this session configuration as the machine's (virtual) administrator account
    RunAsVirtualAccount = $true

    # Groups associated with machine's (virtual) administrator account
    # RunAsVirtualAccountGroups = 'Remote Desktop Users', 'Remote Management Users'

    # Scripts to run when applied to a session
    # ScriptsToProcess = 'C:\ConfigData\InitScript1.ps1', 'C:\ConfigData\InitScript2.ps1'

    # User roles (security groups), and the Role Capabilities that should be applied to them when applied to a session
    RoleDefinitions = @{ 'CONTOSO\NonAdmin_Operators' = @{ 'RoleCapabilities' = 'Maintenance' } }
}
```

<span data-ttu-id="d6fb5-105">A JEA-végpont létrehozása, ha a parancs (és a fájlban a megfelelő kulcsok) a következő paramétereket kell beállítani:</span><span class="sxs-lookup"><span data-stu-id="d6fb5-105">When creating a JEA endpoint, the following parameters of the command (and corresponding keys in the file) must be set:</span></span>

1. <span data-ttu-id="d6fb5-106">SessionType to RestrictedRemoteServer</span><span class="sxs-lookup"><span data-stu-id="d6fb5-106">SessionType to RestrictedRemoteServer</span></span>
2. <span data-ttu-id="d6fb5-107">A RunAsVirtualAccount **$true**</span><span class="sxs-lookup"><span data-stu-id="d6fb5-107">RunAsVirtualAccount to **$true**</span></span>
3. <span data-ttu-id="d6fb5-108">TranscriptPath arra a könyvtárra, ahol "keresztül a váll" átiratok menti a rendszer minden egyes munkamenetnél után</span><span class="sxs-lookup"><span data-stu-id="d6fb5-108">TranscriptPath to the directory where "over the shoulder" transcripts will be saved after each session</span></span>
4. <span data-ttu-id="d6fb5-109">RoleDefinitions, ez a szórótábla meghatározza, hogy mely csoportok kapjanak melyik "szerepkör lehetőségekhez."</span><span class="sxs-lookup"><span data-stu-id="d6fb5-109">RoleDefinitions to a hashtable that defines which groups have access to which "Role Capabilities."</span></span> <span data-ttu-id="d6fb5-110">Ez a mező határozza **akik** teheti **mi** ezen a végponton.</span><span class="sxs-lookup"><span data-stu-id="d6fb5-110">This field defines **who** can do **what** on this endpoint.</span></span> <span data-ttu-id="d6fb5-111">Szerepköri funkciók a speciális fájlok hamarosan részletesen.</span><span class="sxs-lookup"><span data-stu-id="d6fb5-111">Role Capabilities are special files that will be explained shortly.</span></span>

<span data-ttu-id="d6fb5-112">A RoleDefinitions mező határozza meg, hogy mely csoportok rendelkezett hozzáféréssel, mely szerepkör-szolgáltatásait.</span><span class="sxs-lookup"><span data-stu-id="d6fb5-112">The RoleDefinitions field defines which groups had access to which Role Capabilities.</span></span> <span data-ttu-id="d6fb5-113">Egy szerepkör-szolgáltatás érhető el egy fájlt, amely meghatározza a felhasználók kapcsolódás képességeket, amelyek lesz közzétéve.</span><span class="sxs-lookup"><span data-stu-id="d6fb5-113">A Role Capability is a file that defines a set of capabilities that will be exposed to connecting users.</span></span>
<span data-ttu-id="d6fb5-114">Szerepköri funkciók a hozhat létre a **New-PSRoleCapabilityFile** parancsot.</span><span class="sxs-lookup"><span data-stu-id="d6fb5-114">You can create Role Capabilities with the **New-PSRoleCapabilityFile** command.</span></span>

```powershell
New-PSRoleCapabilityFile -Path "$env:ProgramFiles\WindowsPowerShell\Modules\DemoModule\RoleCapabilities\Maintenance.psrc"
```

<span data-ttu-id="d6fb5-115">A művelet létrehoz egy sablon szerepkör képesség, a következőhöz hasonló:</span><span class="sxs-lookup"><span data-stu-id="d6fb5-115">This will generate a template role capability that looks like this:</span></span>

```powershell
@{
    # ID used to uniquely identify this document
    GUID = '9287a34f-3f0e-4fbe-9dd7-f1361ba9fd65'

    # Author of this document
    Author = 'Administrator'

    # Description of the functionality provided by these settings
    # Description = ''

    # Company associated with this document
    CompanyName = 'Unknown'

    # Copyright statement for this document
    Copyright = '(c) 2015 Administrator. All rights reserved.'

    # Modules to import when applied to a session
    # ModulesToImport = 'MyCustomModule', @{ ModuleName = 'MyCustomModule'; ModuleVersion = '1.0.0.0'; GUID = '4d30d5f0-cb16-4898-812d-f20a6c596bdf' }

    # Aliases to make visible when applied to a session
    # VisibleAliases = 'Item1', 'Item2'

    # Cmdlets to make visible when applied to a session
    # VisibleCmdlets = 'Invoke-Cmdlet1', @{ Name = 'Invoke-Cmdlet2'; Parameters = @{ Name = 'Parameter1'; ValidateSet = 'Item1', 'Item2' }, @{ Name = 'Parameter2'; ValidatePattern = 'L*' } }

    # Functions to make visible when applied to a session
    # VisibleFunctions = 'Invoke-Function1', @{ Name = 'Invoke-Function2'; Parameters = @{ Name = 'Parameter1'; ValidateSet = 'Item1', 'Item2' }, @{ Name = 'Parameter2'; ValidatePattern = 'L*' } }

    # External commands (scripts and applications) to make visible when applied to a session
    # VisibleExternalCommands = 'Item1', 'Item2'

    # Providers to make visible when applied to a session
    # VisibleProviders = 'Item1', 'Item2'

    # Scripts to run when applied to a session
    # ScriptsToProcess = 'C:\ConfigData\InitScript1.ps1', 'C:\ConfigData\InitScript2.ps1'

    # Aliases to be defined when applied to a session
    # AliasDefinitions = @{ Name = 'Alias1'; Value = 'Invoke-Alias1'}, @{ Name = 'Alias2'; Value = 'Invoke-Alias2'}

    # Functions to define when applied to a session
    # FunctionDefinitions = @{ Name = 'MyFunction'; ScriptBlock = { param($MyInput) $MyInput } }

    # Variables to define when applied to a session
    # VariableDefinitions = @{ Name = 'Variable1'; Value = { 'Dynamic' + 'InitialValue' } }, @{ Name = 'Variable2'; Value = 'StaticInitialValue' }

    # Environment variables to define when applied to a session
    # EnvironmentVariables = @{ Variable1 = 'Value1'; Variable2 = 'Value2' }

    # Type files (.ps1xml) to load when applied to a session
    # TypesToProcess = 'C:\ConfigData\MyTypes.ps1xml', 'C:\ConfigData\OtherTypes.ps1xml'

    # Format files (.ps1xml) to load when applied to a session
    # FormatsToProcess = 'C:\ConfigData\MyFormats.ps1xml', 'C:\ConfigData\OtherFormats.ps1xml'

    # Assemblies to load when applied to a session
    # AssembliesToLoad = 'System.Web', 'System.OtherAssembly, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a'

}
```

<span data-ttu-id="d6fb5-116">A JEA munkamenet-konfiguráció által használandó szerepkörrel képességeket kell menteni, egy érvényes PowerShell-modul "RoleCapabilities" nevű címtárban.</span><span class="sxs-lookup"><span data-stu-id="d6fb5-116">To be used by a JEA session configuration, Role Capabilities must be saved as a valid PowerShell module in a directory named "RoleCapabilities".</span></span> <span data-ttu-id="d6fb5-117">Modul rendelkezhet több szerepkör képesség fájlt, ha szükséges.</span><span class="sxs-lookup"><span data-stu-id="d6fb5-117">A module may have multiple role capability files, if desired.</span></span>

<span data-ttu-id="d6fb5-118">Konfigurálása, mely parancsmagok, függvények, aliasok és a felhasználók hozzáférhetnek a JEA-munkamenet való csatlakozáskor parancsfájlok először adja hozzá a saját szabályok a következő a megjegyzésekkel sablonjai szerepkör képesség fájlt.</span><span class="sxs-lookup"><span data-stu-id="d6fb5-118">To start configuring which cmdlets, functions, aliases, and scripts a user may access when connecting to a JEA session, add your own rules to the Role Capability file following the commented out templates.</span></span> <span data-ttu-id="d6fb5-119">Szerepköri funkciók konfigurálásához be jobban meg, tekintse meg a teljes [útmutató élmény](http://aka.ms/JEA).</span><span class="sxs-lookup"><span data-stu-id="d6fb5-119">For a deeper look into how you can configure Role Capabilities, check out the full [experience guide](http://aka.ms/JEA).</span></span>

<span data-ttu-id="d6fb5-120">Végül, miután befejezte a munkamenet-konfigurációt és a kapcsolódó szerepköri funkciók testreszabása, a munkamenet-konfiguráció regisztrálása és a végpont létrehozásához futtassa `Register-PSSessionConfiguration`.</span><span class="sxs-lookup"><span data-stu-id="d6fb5-120">Finally, once you have finished customizing your session configuration and related Role Capabilities, register this session configuration and create the endpoint by running `Register-PSSessionConfiguration`.</span></span>

```powershell
Register-PSSessionConfiguration -Name Maintenance -Path "C:\ProgramData\JEAConfiguration\Demo.pssc"
```

## <a name="connect-to-a-jea-endpoint"></a><span data-ttu-id="d6fb5-121">Csatlakozás a JEA-végpont</span><span class="sxs-lookup"><span data-stu-id="d6fb5-121">Connect to a JEA Endpoint</span></span>

<span data-ttu-id="d6fb5-122">Csatlakozás a JEA végponthoz csatlakozik a bármely más PowerShell-végpont működik ugyanúgy működik.</span><span class="sxs-lookup"><span data-stu-id="d6fb5-122">Connecting to a JEA Endpoint works the same way connecting to any other PowerShell endpoint works.</span></span>
<span data-ttu-id="d6fb5-123">Egyszerűen kell adni a JEA-végpont neve a "ConfigurationName" paraméterként **New-PSSession**, **Invoke-Command**, vagy **Enter-PSSession**.</span><span class="sxs-lookup"><span data-stu-id="d6fb5-123">You simply have to give your JEA endpoint name as the "ConfigurationName" parameter for **New-PSSession**, **Invoke-Command**, or **Enter-PSSession**.</span></span>

```powershell
Enter-PSSession -ConfigurationName Maintenance -ComputerName localhost
```

<span data-ttu-id="d6fb5-124">A JEA-munkamenethez való csatlakozás után fog korlátozódni futó a szerepkörrel képességeket, amely hozzáfér a parancsok szerepel az engedélyezési listán.</span><span class="sxs-lookup"><span data-stu-id="d6fb5-124">Once you have connected to the JEA session, you will be limited to running the commands whitelisted in the Role Capabilities that you have access to.</span></span> <span data-ttu-id="d6fb5-125">Ha bármely parancs nem engedélyezett az adott szerepkörhöz, hiba fog történni.</span><span class="sxs-lookup"><span data-stu-id="d6fb5-125">If you try to run any command not allowed for your role, you will encounter an error.</span></span>