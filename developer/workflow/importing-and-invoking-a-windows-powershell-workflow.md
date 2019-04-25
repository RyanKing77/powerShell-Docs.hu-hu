---
title: Importálás és a egy Windows PowerShell-munkafolyamat meghívása |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 50e6f9b1-2678-4f53-9250-7c48843a9549
caps.latest.revision: 5
ms.openlocfilehash: 1113c0d1cd68bb97d2f96b529f755b62137d1f40
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62080339"
---
# <a name="importing-and-invoking-a-windows-powershell-workflow"></a>Windows PowerShell munkafolyamat importálása és meghívása

Windows PowerShell 3, importálása és vyvolat pracovní postup, mint egy Windows PowerShell-modul csomagolt teszi lehetővé. További információ a Windows PowerShell-modulokat: [Windows PowerShell-modul írása](../module/writing-a-windows-powershell-module.md).

A [System.Management.Automation.Psjobproxy](/dotnet/api/System.Management.Automation.PSJobProxy)osztály ügyfél oldalán proxyként szolgál a munkafolyamat-objektumok a kiszolgálón. Az alábbi eljárás ismerteti, hogyan egy [System.Management.Automation.Psjobproxy](/dotnet/api/System.Management.Automation.PSJobProxy)objektum vyvolat pracovní postup.

### <a name="creating-a-psjobproxy-object-to-execute-workflow-commands-on-a-remote-server"></a>Egy munkafolyamat-parancsok egy távoli kiszolgálón végrehajtandó PSJobProxy objektum létrehozásához.

1. Hozzon létre egy [System.Management.Automation.Runspaces.Wsmanconnectioninfo](/dotnet/api/System.Management.Automation.Runspaces.WSManConnectionInfo)objektumot hozzon létre egy kapcsolatot egy távoli futási térből.

2. Állítsa be a [System.Management.Automation.Runspaces.Wsmanconnectioninfo.Shelluri*](/dotnet/api/System.Management.Automation.Runspaces.WSManConnectionInfo.ShellUri) tulajdonságát a [System.Management.Automation.Runspaces.Wsmanconnectioninfo](/dotnet/api/System.Management.Automation.Runspaces.WSManConnectionInfo)az objektum `Microsoft.PowerShell.Workflow` , Adjon meg egy Windows PowerShell-végpontot.

3. Hozzon létre egy futási teret, amely a; Ehhez hajtsa végre az előző lépésekben létrehozott kapcsolatot használ.

4. Hozzon létre egy [System.Management.Automation.Powershell](/dotnet/api/System.Management.Automation.PowerShell)objektumra, és állítsa be a [System.Management.Automation.Powershell.Runspace*](/dotnet/api/System.Management.Automation.PowerShell.Runspace) az előző lépésben létrehozott futási térben tulajdonságot.

5. Importálja a munkafolyamat-modul, és azokat a parancsokat a [System.Management.Automation.Powershell](/dotnet/api/System.Management.Automation.PowerShell).

6. Hozzon létre egy [System.Management.Automation.Psjobproxy](/dotnet/api/System.Management.Automation.PSJobProxy) objektumra, és a távoli kiszolgálón végrehajtandó munkafolyamat-parancsok használatával.

## <a name="example"></a>Példa

Az alábbi példakód bemutatja, hogyan vyvolat pracovní postup Windows PowerShell-lel való.

Ebben a példában a Windows PowerShell 3 van szükség.

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Management.Automation;
using System.Management.Automation.Runspaces;

namespace WorkflowHostTest
{

class Program
    {
        static void Main(string[] args)
        {
            if (args.Length == 0)
            {
                Console.WriteLine("Specify path to Workflow module");
                return;
            }

            string moduleFile = args[0];

            Console.Write("Creating Remote runspace connection...");
            WSManConnectionInfo connectionInfo = new WSManConnectionInfo();

            //Set the shellURI to workflow endpoint Microsoft.PowerShell.Workflow
            connectionInfo.ShellUri = "Microsoft.PowerShell.Workflow";

            //Create and open a runspace.
            Runspace runspace = RunspaceFactory.CreateRunspace(connectionInfo);
            runspace.Open();
            Console.WriteLine("done");

            PowerShell powershell = PowerShell.Create();
            powershell.Runspace = runspace;
            Console.Write("Setting $VerbosePreference=\"Continue\"...");
            powershell.AddScript("$VerbosePreference=\"Continue\"");
            powershell.Invoke();
            Console.WriteLine("done");

            Console.Write("Importing Workflow module...");
            powershell.Commands.Clear();

            //Import the module in to the PowerShell runspace. A XAML file could also be imported directly by using Import-Module.
            powershell.AddCommand("Import-Module").AddArgument(moduleFile);
            powershell.Invoke();
            Console.WriteLine("done");

            Console.Write("Creating job proxy...");
            powershell.Commands.Clear();
            powershell.AddCommand("Get-Proc").AddArgument("*");
            PSJobProxy job = powershell.AsJobProxy();
            Console.WriteLine("done");

                Console.WriteLine();
                Console.WriteLine("Using job proxy and performing operations...");
                Console.WriteLine("State of Job :" + job.JobStateInfo.State.ToString());
                Console.WriteLine("Starting job...");
                job.StartJob();
                Console.WriteLine("State of Job :" + job.JobStateInfo.State.ToString());

                // use blocking enumerator to wait for objects until job finishes
                job.Output.BlockingEnumerator = true;
                foreach (PSObject o in job.Output)
                {
                    Console.WriteLine(o.Properties["ProcessName"].Value.ToString());
                }

                // wait for a random time before attempting to stop job
                Random random = new Random();
                int time = random.Next(1, 10);
                Console.Write("Sleeping for {0} seconds when job is running on another thread...", time);
                System.Threading.Thread.Sleep(time * 1000);
                Console.WriteLine("done");
                Console.WriteLine("Stopping job...");
                job.StopJob();
                Console.WriteLine("State of Job :" + job.JobStateInfo.State.ToString());
                Console.WriteLine();
                job.Finished.WaitOne();
                Console.WriteLine("Output from job");
                Console.WriteLine("---------------");

                foreach (PSObject o in job.Output)
                {
                    Console.WriteLine(o.Properties["ProcessName"].Value.ToString());
                }

                Console.WriteLine();
                Console.WriteLine("Verbose messages from job");
                Console.WriteLine("-------------------------");
                foreach (VerboseRecord v in job.Verbose)
                {
                    Console.WriteLine(v.Message);
                }

            runspace.Close();
        }
    }
}

```