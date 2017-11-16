---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "WMF, a powershell, a beállítása"
ms.openlocfilehash: c3645a6ba83081bd5ac31a13af0f67f6538db22a
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
# <a name="creating-and-connecting-to-a-jea-endpoint"></a><span data-ttu-id="9e056-102">Hoz létre és csatlakoztatja a JEA-végpont</span><span class="sxs-lookup"><span data-stu-id="9e056-102">Creating and Connecting to a JEA Endpoint</span></span>
<span data-ttu-id="9e056-103">JEA-végpont létrehozása kell létrehozni és regisztrálni egy kifejezetten konfigurált PowerShell munkamenet konfigurációs fájlt, amely a hozhatók létre a **New-PSSessionConfigurationFile** parancsmag.</span><span class="sxs-lookup"><span data-stu-id="9e056-103">To create a JEA endpoint, you need to create and register a specially-configured PowerShell Session Configuration file, which can be generated with the **New-PSSessionConfigurationFile** cmdlet.</span></span>

```powershell
New-PSSessionConfigurationFile -SessionType RestrictedRemoteServer -TranscriptDirectory "C:\ProgramData\JEATranscripts" -RunAsVirtualAccount -RoleDefinitions @{ 'CONTOSO\NonAdmin_Operators' = @{ RoleCapabilities = 'Maintenance' }} -Path "$env:ProgramData\JEAConfiguration\Demo.pssc" 
```

<span data-ttu-id="9e056-104">Ezzel létrehoz egy munkamenet-konfigurációs fájlt, amely a következőképpen néz ki:</span><span class="sxs-lookup"><span data-stu-id="9e056-104">This will create a session configuration file that looks like this:</span></span> 
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
RoleDefinitions = @{
    'CONTOSO\NonAdmin_Operators' = @{
        'RoleCapabilities' = 'Maintenance' } }

} 
```
<span data-ttu-id="9e056-105">A JEA-végpont létrehozása, ha a parancs (és a fájlban tartozó kulcsok) a következő paramétereket kell beállítani:</span><span class="sxs-lookup"><span data-stu-id="9e056-105">When creating a JEA endpoint, the following parameters of the command (and corresponding keys in the file) must be set:</span></span>
1.  <span data-ttu-id="9e056-106">A RestrictedRemoteServer SessionType</span><span class="sxs-lookup"><span data-stu-id="9e056-106">SessionType to RestrictedRemoteServer</span></span>
2.  <span data-ttu-id="9e056-107">A RunAsVirtualAccount **$true**</span><span class="sxs-lookup"><span data-stu-id="9e056-107">RunAsVirtualAccount to **$true**</span></span>
3.  <span data-ttu-id="9e056-108">A könyvtár "keresztül a képernyőre pillant" ki szeretné menteni után minden munkamenet TranscriptPath</span><span class="sxs-lookup"><span data-stu-id="9e056-108">TranscriptPath to the directory where “over the shoulder” transcripts will be saved after each session</span></span>
4.  <span data-ttu-id="9e056-109">RoleDefinitions való egy kivonattáblát, amely meghatározza, hogy mely csoportok rendelkezzenek hozzáféréssel a "Szerepkör képességeit."</span><span class="sxs-lookup"><span data-stu-id="9e056-109">RoleDefinitions to a hashtable that defines which groups have access to which “Role Capabilities.”</span></span>  <span data-ttu-id="9e056-110">Ez a mező határozza **ki** teheti **mi** ezen a végponton.</span><span class="sxs-lookup"><span data-stu-id="9e056-110">This field defines **who** can do **what** on this endpoint.</span></span>   <span data-ttu-id="9e056-111">Szerepkör képességek olyan különleges, amelyeket hamarosan részletesen.</span><span class="sxs-lookup"><span data-stu-id="9e056-111">Role Capabilities are special files that will be explained shortly.</span></span>


<span data-ttu-id="9e056-112">A RoleDefinitions mező határozza meg, hogy mely csoportok hozzáfért mely szerepkör-szolgáltatásait.</span><span class="sxs-lookup"><span data-stu-id="9e056-112">The RoleDefinitions field defines which groups had access to which Role Capabilities.</span></span>  <span data-ttu-id="9e056-113">Egy szerepkör, amely meghatározza, hogy elérhetővé tehető képességek egy készletét, csatlakozó felhasználók fájl.</span><span class="sxs-lookup"><span data-stu-id="9e056-113">A Role Capability is a file that defines a set of capabilities that will be exposed to connecting users.</span></span>  <span data-ttu-id="9e056-114">Szerepkör képességeket is létrehozhat a **New-PSRoleCapabilityFile** parancsot.</span><span class="sxs-lookup"><span data-stu-id="9e056-114">You can create Role Capabilities with the **New-PSRoleCapabilityFile** command.</span></span>

```powershell
New-PSRoleCapabilityFile -Path "$env:ProgramFiles\WindowsPowerShell\Modules\DemoModule\RoleCapabilities\Maintenance.psrc" 
```

<span data-ttu-id="9e056-115">Ezzel létrejön egy sablon szerepkör képesség, amely a következőképpen néz ki:</span><span class="sxs-lookup"><span data-stu-id="9e056-115">This will generate a template role capability that looks like this:</span></span>
```
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
<span data-ttu-id="9e056-116">A JEA munkamenet-konfiguráció által használandó szerepkör képességek kell menteni, egy érvényes PowerShell-modul egy "RoleCapabilities" nevű könyvtár.</span><span class="sxs-lookup"><span data-stu-id="9e056-116">To be used by a JEA session configuration, Role Capabilities must be saved as a valid PowerShell module in a directory named “RoleCapabilities”.</span></span> <span data-ttu-id="9e056-117">A modul rendelkezhet több szerepkör szolgáltatásfájlokban, ha szükséges.</span><span class="sxs-lookup"><span data-stu-id="9e056-117">A module may have multiple role capability files, if desired.</span></span>

<span data-ttu-id="9e056-118">Indul el, hogy mely parancsmagok, függvények, aliasok és a felhasználók elérhessék a JEA munkamenet való csatlakozáskor parancsfájlok konfigurálása, vegye fel saját szabályainak a szerepkör funkció fájlt a megjegyzésként sablonok ki.</span><span class="sxs-lookup"><span data-stu-id="9e056-118">To start configuring which cmdlets, functions, aliases, and scripts a user may access when connecting to a JEA session, add your own rules to the Role Capability file following the commented out templates.</span></span> <span data-ttu-id="9e056-119">A szerepkör képességek konfigurálásának mélyebb betekintést, tekintse meg a teljes [útmutató élmény](http://aka.ms/JEA).</span><span class="sxs-lookup"><span data-stu-id="9e056-119">For a deeper look into how you can configure Role Capabilities, check out the full [experience guide](http://aka.ms/JEA).</span></span>

<span data-ttu-id="9e056-120">Végül, miután befejezte a munkamenet-konfiguráció és a kapcsolódó szerepkör-képességek testreszabása, regisztrálja a munkamenet-konfiguráció és a végpont létrehozásához futtassa a **Register-PSSessionConfiguration**.</span><span class="sxs-lookup"><span data-stu-id="9e056-120">Finally, once you have finished customizing your session configuration and related Role Capabilities, register this session configuration and create the endpoint by running **Register-PSSessionConfiguration**.</span></span>

```powershell
Register-PSSessionConfiguration -Name Maintenance -Path "C:\ProgramData\JEAConfiguration\Demo.pssc" 
```

## <a name="connect-to-a-jea-endpoint"></a><span data-ttu-id="9e056-121">A JEA végponthoz kapcsolódni</span><span class="sxs-lookup"><span data-stu-id="9e056-121">Connect to a JEA Endpoint</span></span>
<span data-ttu-id="9e056-122">A JEA végpont csatlakozik működik, mint bármely más PowerShell végpont működik csatlakozik.</span><span class="sxs-lookup"><span data-stu-id="9e056-122">Connecting to a JEA Endpoint works the same way connecting to any other PowerShell endpoint works.</span></span>  <span data-ttu-id="9e056-123">Egyszerűen kell nevezze el a JEA végpont a "Konfiguráció" paraméterként **New-PSSession**, **Invoke-Command**, vagy **Enter-PSSession**.</span><span class="sxs-lookup"><span data-stu-id="9e056-123">You simply have to give your JEA endpoint name as the “ConfigurationName” parameter for **New-PSSession**, **Invoke-Command**, or **Enter-PSSession**.</span></span>

```powershell
Enter-PSSession -ConfigurationName Maintenance -ComputerName localhost
```
<span data-ttu-id="9e056-124">A JEA munkamenethez való csatlakozás után lesz korlátozva futó szerepkör funkciója, amelyek rendelkezik hozzáféréssel a parancsok szerepel az engedélyezési listán.</span><span class="sxs-lookup"><span data-stu-id="9e056-124">Once you have connected to the JEA session, you will be limited to running the commands whitelisted in the Role Capabilities that you have access to.</span></span> <span data-ttu-id="9e056-125">Ha a parancs nem engedélyezett az adott szerepkörhöz, akkor hibaüzenetet kap.</span><span class="sxs-lookup"><span data-stu-id="9e056-125">If you try to run any command not allowed for your role, you will encounter an error.</span></span>

