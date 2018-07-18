---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: e4910e95a417da61661aaddd98b2dc7da9f98a3d
ms.sourcegitcommit: 77f62a55cac8c13d69d51eef5fade18f71d66955
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/17/2018
ms.locfileid: "39093718"
---
# <a name="creating-and-connecting-to-a-jea-endpoint"></a>JEA-végpont létrehozása és csatlakozás a végponthoz
A JEA-végpont létrehozása, létrehozhat és regisztrálhat egy speciálisan konfigurált PowerShell-munkamenet konfigurációs fájlt, amely készíthet szeretne a **New-PSSessionConfigurationFile** parancsmagot.

```powershell
New-PSSessionConfigurationFile -SessionType RestrictedRemoteServer -TranscriptDirectory "C:\ProgramData\JEATranscripts" -RunAsVirtualAccount -RoleDefinitions @{ 'CONTOSO\NonAdmin_Operators' = @{ RoleCapabilities = 'Maintenance' }} -Path "$env:ProgramData\JEAConfiguration\Demo.pssc"
```

Ezzel létrehoz egy munkamenet-konfigurációs fájlt a következőhöz hasonló:
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
A JEA-végpont létrehozása, ha a parancs (és a fájlban a megfelelő kulcsok) a következő paramétereket kell beállítani:
1.  A RestrictedRemoteServer SessionType
2.  A RunAsVirtualAccount **$true**
3.  TranscriptPath arra a könyvtárra, ahol "keresztül a váll" átiratok menti a rendszer minden egyes munkamenetnél után
4.  RoleDefinitions, ez a szórótábla meghatározza, hogy mely csoportok kapjanak melyik "szerepkör lehetőségekhez."  Ez a mező határozza **akik** teheti **mi** ezen a végponton.   Szerepköri funkciók a speciális fájlok hamarosan részletesen.


A RoleDefinitions mező határozza meg, hogy mely csoportok rendelkezett hozzáféréssel, mely szerepkör-szolgáltatásait.  Egy szerepkör-szolgáltatás érhető el egy fájlt, amely meghatározza a felhasználók kapcsolódás képességeket, amelyek lesz közzétéve.  Szerepköri funkciók a hozhat létre a **New-PSRoleCapabilityFile** parancsot.

```powershell
New-PSRoleCapabilityFile -Path "$env:ProgramFiles\WindowsPowerShell\Modules\DemoModule\RoleCapabilities\Maintenance.psrc"
```

A művelet létrehoz egy sablon szerepkör képesség, a következőhöz hasonló:
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

A JEA munkamenet-konfiguráció által használandó szerepkörrel képességeket kell menteni, egy érvényes PowerShell-modul "RoleCapabilities" nevű címtárban. Modul rendelkezhet több szerepkör képesség fájlt, ha szükséges.

Konfigurálása, mely parancsmagok, függvények, aliasok és a felhasználók hozzáférhetnek a JEA-munkamenet való csatlakozáskor parancsfájlok először adja hozzá a saját szabályok a következő a megjegyzésekkel sablonjai szerepkör képesség fájlt. Szerepköri funkciók konfigurálásához be jobban meg, tekintse meg a teljes [útmutató élmény](http://aka.ms/JEA).

Végül, miután befejezte a munkamenet-konfigurációt és a kapcsolódó szerepköri funkciók testreszabása, a munkamenet-konfiguráció regisztrálása és a végpont létrehozásához futtassa **Register-PSSessionConfiguration**.

```powershell
Register-PSSessionConfiguration -Name Maintenance -Path "C:\ProgramData\JEAConfiguration\Demo.pssc"
```

## <a name="connect-to-a-jea-endpoint"></a>Csatlakozás a JEA-végpont

Csatlakozás a JEA végponthoz csatlakozik a bármely más PowerShell-végpont működik ugyanúgy működik.  Egyszerűen kell adni a JEA-végpont neve a "ConfigurationName" paraméterként **New-PSSession**, **Invoke-Command**, vagy **Enter-PSSession**.

```powershell
Enter-PSSession -ConfigurationName Maintenance -ComputerName localhost
```

A JEA-munkamenethez való csatlakozás után fog korlátozódni futó a szerepkörrel képességeket, amely hozzáfér a parancsok szerepel az engedélyezési listán. Ha bármely parancs nem engedélyezett az adott szerepkörhöz, hiba fog történni.