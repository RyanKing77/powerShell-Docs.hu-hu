---
title: Egy munkafolyamat-tevékenységet hoz létre egy Windows PowerShell-parancsmag |} A Microsoft Docs
ms.custom: ''
ms.date: 09/12/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 4174e84f-d516-4aca-b418-273047dcfb07
caps.latest.revision: 7
ms.openlocfilehash: 5761ed2168a46d6ed9a2e50554d459f5b93223ee
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56848579"
---
# <a name="creating-a-workflow-activity-from-a-windows-powershell-cmdlet"></a>Munkafolyamat-tevékenységek létrehozása egy Windows PowerShell-parancsmagban

Bármely Windows PowerShell-modul és parancsmag csomagolható, aktivita pracovního Postupu módszerek használatával a [Microsoft.Powershell.Activities.Activitygenerator](/dotnet/api/Microsoft.PowerShell.Activities.ActivityGenerator) osztály. Használja a [Microsoft.Powershell.Activities.Activitygenerator.Generatefrommoduleinfo*](/dotnet/api/Microsoft.PowerShell.Activities.ActivityGenerator.GenerateFromModuleInfo), [Microsoft.Powershell.Activities.Activitygenerator.Generatefromcommandinfo*](/dotnet/api/Microsoft.PowerShell.Activities.ActivityGenerator.GenerateFromCommandInfo), és [Microsoft.Powershell.Activities.Activitygenerator.Generatefromname*](/dotnet/api/Microsoft.PowerShell.Activities.ActivityGenerator.GenerateFromName) módszerek a [Microsoft.Powershell.Activities.Activitygenerator](/dotnet/api/Microsoft.PowerShell.Activities.ActivityGenerator) osztály létrehozása C# -kód egy tevékenység jelöli. Ezután feldolgozhatjuk a létrejövő C# szerelvény lehet hozzáadni a tevékenységként projekt kódot.

Ezután feldolgozhatjuk a létrejövő C# szerelvény lehet hozzáadni egy projektet egy tevékenységként egy parancssorból a következő képernyőn a kódot.

**CSC/nologo /out:AssemblyName /target:library /reference:System.Activities.Activity /reference:Microsoft.PowerShell.Activities codefile.cs**

## <a name="example"></a>Példa

Az alábbi példa bemutatja, hogyan hozhat létre C# egy Windows PowerShell-modul tevékenységét kódját.

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.IO;
using System.Management.Automation;
using System.Collections.ObjectModel;
using Microsoft.PowerShell.Activities;

namespace MakeActivity
{
    class Program
    {
        static void Main(string[] args)

        {
            StreamWriter CodeFile = new StreamWriter("c:\\\\testmodule\\codefile.cs");
            Collection<PSModuleInfo> ModuleInfos = new Collection<PSModuleInfo> { };
            PSModuleInfo ModuleInfo;
            string ActivityCode = "";
            string ModulePath = "";
            Console.Write("Type the full path and filename of the module to process:");
            ModulePath = Console.ReadLine();

            PowerShell ps = PowerShell.Create();

            ps.AddCommand("Import-Module").AddArgument(ModulePath);
            ps.AddParameter("PassThru");
            ModuleInfos = ps.Invoke<PSModuleInfo>();

            ModuleInfo = (PSModuleInfo)ModuleInfos[0];

            ActivityCode = ActivityGenerator.GenerateFromModuleInfo(ModuleInfo, "MyNamespace").First<String>();

           CodeFile.Write(ActivityCode);
            Console.ReadLine();

        }
    }
}

```

## <a name="example"></a>Példa

Az alábbi példa bemutatja, hogyan hozhat létre C# egy Windows PowerShell-parancsmag tevékenységét kódját.

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.IO;
using System.Management.Automation;
using System.Collections.ObjectModel;
using Microsoft.PowerShell.Activities;

namespace MakeActivity
{
    class Program
    {
        static void Main(string[] args)

        {
            StreamWriter CodeFile = new StreamWriter("c:\\\\testmodule\\codefile.cs");
            Collection<PSModuleInfo> ModuleInfos = new Collection<PSModuleInfo> { };
            PSModuleInfo ModuleInfo;
            Collection<CommandInfo> CommandInfos = new Collection<CommandInfo> { };
            CommandInfo MyCommand;
            string ActivityCode = "";
            string ModulePath = "";
            Console.Write("Type the full path and filename of the module to process:");
            ModulePath = Console.ReadLine();

            PowerShell ps = PowerShell.Create();

            ps.AddCommand("Import-Module").AddArgument(ModulePath);
            ps.AddParameter("PassThru");
            ModuleInfos = ps.Invoke<PSModuleInfo>();

            ModuleInfo = (PSModuleInfo)ModuleInfos[0];

            ps.AddCommand("Get-Command").AddArgument(ModuleInfo);
            CommandInfos = ps.Invoke<CommandInfo>();

            MyCommand = CommandInfos[0];

            ActivityCode = ActivityGenerator.GenerateFromCommandInfo(MyCommand, "MyNamespace");

           CodeFile.Write(ActivityCode);
            Console.ReadLine();

        }
    }
}

```