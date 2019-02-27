---
title: Windows PowerShell-gazdagépet a rövid útmutató |} A Microsoft Docs
ms.custom: ''
ms.date: 09/12/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 5a134b81-bd0c-4e1c-a2f0-9acbe852745a
caps.latest.revision: 9
ms.openlocfilehash: 2c6a4bca03ee7f62371cbc296f854464167e5a62
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56847788"
---
# <a name="windows-powershell-host-quickstart"></a><span data-ttu-id="b88cb-102">Windows PowerShell-gazda – Gyors üzembe helyezés</span><span class="sxs-lookup"><span data-stu-id="b88cb-102">Windows PowerShell Host Quickstart</span></span>

<span data-ttu-id="b88cb-103">Az alkalmazás futtatásához a Windows PowerShell, használja a [System.Management.Automation.PowerShell](/dotnet/api/System.Management.Automation.PowerShell) osztály.</span><span class="sxs-lookup"><span data-stu-id="b88cb-103">To host Windows PowerShell in your application, you use the [System.Management.Automation.PowerShell](/dotnet/api/System.Management.Automation.PowerShell) class.</span></span> <span data-ttu-id="b88cb-104">Ez az osztály metódusokat, hozzon létre egy folyamatot a parancsok, majd hajtsa végre ezeket a parancsokat egy futási teret biztosít.</span><span class="sxs-lookup"><span data-stu-id="b88cb-104">This class provides methods that create a pipeline of commands and then execute those commands in a runspace.</span></span> <span data-ttu-id="b88cb-105">Hozzon létre egy fogadó alkalmazás legegyszerűbb módja, hogy az alapértelmezett futási térből.</span><span class="sxs-lookup"><span data-stu-id="b88cb-105">The simplest way to create a host application is to use the default runspace.</span></span> <span data-ttu-id="b88cb-106">Az alapértelmezett futási térben összes az alapvető Windows PowerShell-parancsokat tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="b88cb-106">The default runspace contains all of the core Windows PowerShell commands.</span></span> <span data-ttu-id="b88cb-107">Ha azt szeretné, hogy az alkalmazás elérhetővé a Windows PowerShell-parancsokat csak egy részhalmazát, létre kell hoznia egy egyéni futási térből.</span><span class="sxs-lookup"><span data-stu-id="b88cb-107">If you want your application to expose only a subset of the Windows PowerShell commands, you must create a custom runspace.</span></span>

## <a name="using-the-default-runspace"></a><span data-ttu-id="b88cb-108">Az alapértelmezett futási teret használ</span><span class="sxs-lookup"><span data-stu-id="b88cb-108">Using the default runspace</span></span>

<span data-ttu-id="b88cb-109">Indítása, azt fogja alapértelmezett futási térben, majd a módszereket a [System.Management.Automation.PowerShell](/dotnet/api/System.Management.Automation.PowerShell) osztály parancsok, paraméterek, utasításokat és parancsfájlokat hozzáadni egy folyamatot.</span><span class="sxs-lookup"><span data-stu-id="b88cb-109">To start, we'll use the default runspace, and use the methods of the [System.Management.Automation.PowerShell](/dotnet/api/System.Management.Automation.PowerShell) class to add commands, parameters, statements, and scripts to a pipeline.</span></span>

### <a name="addcommand"></a><span data-ttu-id="b88cb-110">AddCommand</span><span class="sxs-lookup"><span data-stu-id="b88cb-110">AddCommand</span></span>

<span data-ttu-id="b88cb-111">Használja a [System.Management.Automation.Powershell.AddCommand\*](/dotnet/api/System.Management.Automation.PowerShell.AddCommand) módszere a [System.Management.Automation.PowerShell](/dotnet/api/System.Management.Automation.PowerShell) osztály parancsok hozzáadása a folyamatban.</span><span class="sxs-lookup"><span data-stu-id="b88cb-111">You use the [System.Management.Automation.Powershell.AddCommand\*](/dotnet/api/System.Management.Automation.PowerShell.AddCommand) method of the [System.Management.Automation.PowerShell](/dotnet/api/System.Management.Automation.PowerShell) class to add commands to the pipeline.</span></span> <span data-ttu-id="b88cb-112">Például tegyük fel, hogy a gépen futó folyamatok listájának beolvasása.</span><span class="sxs-lookup"><span data-stu-id="b88cb-112">For example, suppose you want to get the list of running processes on the machine.</span></span> <span data-ttu-id="b88cb-113">A módszer futtassa a következő parancsot a következőképpen történik.</span><span class="sxs-lookup"><span data-stu-id="b88cb-113">The way to run this command is as follows.</span></span>

1. <span data-ttu-id="b88cb-114">Hozzon létre egy [System.Management.Automation.PowerShell](/dotnet/api/System.Management.Automation.PowerShell) objektum.</span><span class="sxs-lookup"><span data-stu-id="b88cb-114">Create a [System.Management.Automation.PowerShell](/dotnet/api/System.Management.Automation.PowerShell) object.</span></span>

   ```csharp
   PowerShell ps = PowerShell.Create();
   ```

2. <span data-ttu-id="b88cb-115">Adja hozzá a végrehajtani kívánt parancsot.</span><span class="sxs-lookup"><span data-stu-id="b88cb-115">Add the command that you want to execute.</span></span>

   ```csharp
   ps.AddCommand("Get-Process");
   ```

3. <span data-ttu-id="b88cb-116">Hívja meg a parancsot.</span><span class="sxs-lookup"><span data-stu-id="b88cb-116">Invoke the command.</span></span>

   ```csharp
   ps.Invoke();
   ```

<span data-ttu-id="b88cb-117">Ha felhívja a [System.Management.Automation.Powershell.AddCommand\*](/dotnet/api/System.Management.Automation.PowerShell.AddCommand) metódus meghívása előtt egyszer további a [System.Management.Automation.Powershell.Invoke\*](/dotnet/api/System.Management.Automation.PowerShell.Invoke) metódus, eredményét a első parancs van irányíthatja át a második, és így tovább.</span><span class="sxs-lookup"><span data-stu-id="b88cb-117">If you call the [System.Management.Automation.Powershell.AddCommand\*](/dotnet/api/System.Management.Automation.PowerShell.AddCommand) method more than once before you call the [System.Management.Automation.Powershell.Invoke\*](/dotnet/api/System.Management.Automation.PowerShell.Invoke) method, the result of the first command is piped to the second, and so on.</span></span> <span data-ttu-id="b88cb-118">Ha nem szeretne egy parancsot az előző parancs eredménye kanálu, adja hozzá meghívásával a [System.Management.Automation.Powershell.AddStatement\*](/dotnet/api/System.Management.Automation.PowerShell.AddStatement) helyette.</span><span class="sxs-lookup"><span data-stu-id="b88cb-118">If you do not want to pipe the result of a previous command to a command, add it by calling the [System.Management.Automation.Powershell.AddStatement\*](/dotnet/api/System.Management.Automation.PowerShell.AddStatement) instead.</span></span>

### <a name="addparameter"></a><span data-ttu-id="b88cb-119">AddParameter</span><span class="sxs-lookup"><span data-stu-id="b88cb-119">AddParameter</span></span>

<span data-ttu-id="b88cb-120">Az előző példában egyetlen parancs paraméterek nélkül hajtja végre.</span><span class="sxs-lookup"><span data-stu-id="b88cb-120">The previous example executes a single command without any parameters.</span></span> <span data-ttu-id="b88cb-121">Használatával a parancshoz paramétereket is hozzáadhat a [System.Management.Automation.PSCommand.AddParameter\*](/dotnet/api/System.Management.Automation.PSCommand.AddParameter) metódus például az alábbi kód listáját kéri le összes nevű folyamat `PowerShell` fut a gép.</span><span class="sxs-lookup"><span data-stu-id="b88cb-121">You can add parameters to the command by using the [System.Management.Automation.PSCommand.AddParameter\*](/dotnet/api/System.Management.Automation.PSCommand.AddParameter) method For example, the following code gets a list of all of the processes that are named `PowerShell` running on the machine.</span></span>

```csharp
PowerShell.Create().AddCommand("Get-Process")
                   .AddParameter("Name", "PowerShell")
                   .Invoke();
```

<span data-ttu-id="b88cb-122">Hozzáadhat további paraméterek meghívásával [System.Management.Automation.PSCommand.AddParameter\*](/dotnet/api/System.Management.Automation.PSCommand.AddParameter) ismételten.</span><span class="sxs-lookup"><span data-stu-id="b88cb-122">You can add additional parameters by calling [System.Management.Automation.PSCommand.AddParameter\*](/dotnet/api/System.Management.Automation.PSCommand.AddParameter) repeatedly.</span></span>

```csharp
PowerShell.Create().AddCommand("Get-Process")
                   .AddParameter("Name", "PowerShell")
                   .AddParameter("Id", "12768")
                   .Invoke();
```

<span data-ttu-id="b88cb-123">Paraméterek és értékek tartalmazó meghívásával is hozzáadhat a [System.Management.Automation.PowerShell.AddParameters\*](/dotnet/api/System.Management.Automation.PowerShell.AddParameters) metódust.</span><span class="sxs-lookup"><span data-stu-id="b88cb-123">You can also add a dictionary of parameter names and values by calling the [System.Management.Automation.PowerShell.AddParameters\*](/dotnet/api/System.Management.Automation.PowerShell.AddParameters) method.</span></span>

```csharp
IDictionary parameters = new Dictionary<String, String>();
parameters.Add("Name", "PowerShell");

parameters.Add("Id", "12768");
PowerShell.Create().AddCommand("Get-Process")
   .AddParameters(parameters)
      .Invoke()

```

### <a name="addstatement"></a><span data-ttu-id="b88cb-124">AddStatement</span><span class="sxs-lookup"><span data-stu-id="b88cb-124">AddStatement</span></span>

<span data-ttu-id="b88cb-125">A kötegelés szimulálhatja a [System.Management.Automation.PowerShell.AddStatement\*](/dotnet/api/System.Management.Automation.PowerShell.AddStatement) metódussal, amely egy további utasítást ad hozzá a következő kódot a futó folyamatok nevű listáját kéri le a folyamat végén `PowerShell`, és majd a szolgáltatások listájának beolvasása.</span><span class="sxs-lookup"><span data-stu-id="b88cb-125">You can simulate batching by using the [System.Management.Automation.PowerShell.AddStatement\*](/dotnet/api/System.Management.Automation.PowerShell.AddStatement) method, which adds an additional statement to the end of the pipeline The following code gets a list of running processes with the name `PowerShell`, and then gets the list of running services.</span></span>

```csharp
PowerShell ps = PowerShell.Create();
ps.AddCommand("Get-Process").AddParameter("Name", "PowerShell");
ps.AddStatement().AddCommand("Get-Service");
ps.Invoke();
```

### <a name="addscript"></a><span data-ttu-id="b88cb-126">AddScript</span><span class="sxs-lookup"><span data-stu-id="b88cb-126">AddScript</span></span>

<span data-ttu-id="b88cb-127">Meglévő parancsfájl meghívásával futtathatja a [System.Management.Automation.PowerShell.AddScript\*](/dotnet/api/System.Management.Automation.PowerShell.AddScript) metódust.</span><span class="sxs-lookup"><span data-stu-id="b88cb-127">You can run an existing script by calling the [System.Management.Automation.PowerShell.AddScript\*](/dotnet/api/System.Management.Automation.PowerShell.AddScript) method.</span></span> <span data-ttu-id="b88cb-128">Az alábbi példa hozzáad egy parancsfájlt a folyamat, és futtatása.</span><span class="sxs-lookup"><span data-stu-id="b88cb-128">The following example adds a script to the pipeline and runs it.</span></span> <span data-ttu-id="b88cb-129">Ez a példa feltételezi, hogy már van egy nevű szkriptet `MyScript.ps1` nevű mappába `D:\PSScripts`.</span><span class="sxs-lookup"><span data-stu-id="b88cb-129">This example assumes there is already a script named `MyScript.ps1` in a folder named `D:\PSScripts`.</span></span>

```csharp
PowerShell ps = PowerShell.Create();
ps.AddScript("D:\PSScripts\MyScript.ps1").Invoke();
```

<span data-ttu-id="b88cb-130">Emellett van egy verziója a [System.Management.Automation.PowerShell.AddScript\*](/dotnet/api/System.Management.Automation.PowerShell.AddScript) metódus túlterhelését, amely egy nevű logikai paraméterrel `useLocalScope`.</span><span class="sxs-lookup"><span data-stu-id="b88cb-130">There is also a version of the [System.Management.Automation.PowerShell.AddScript\*](/dotnet/api/System.Management.Automation.PowerShell.AddScript) method that takes a boolean parameter named `useLocalScope`.</span></span> <span data-ttu-id="b88cb-131">Ha ez a paraméter értéke `true`, akkor a szkript futtatása helyi hatókörében.</span><span class="sxs-lookup"><span data-stu-id="b88cb-131">If this parameter is set to `true`, then the script is run in the local scope.</span></span> <span data-ttu-id="b88cb-132">A következő kódot fog futtassa a szkriptet a helyi hatókörében.</span><span class="sxs-lookup"><span data-stu-id="b88cb-132">The following code will run the script in the local scope.</span></span>

```csharp
PowerShell ps = PowerShell.Create();
ps.AddScript(@"D:\PSScripts\MyScript.ps1", true).Invoke();
```

## <a name="creating-a-custom-runspace"></a><span data-ttu-id="b88cb-133">Egy egyéni futási teret létrehozása</span><span class="sxs-lookup"><span data-stu-id="b88cb-133">Creating a custom runspace</span></span>

<span data-ttu-id="b88cb-134">Míg a korábbi példákban használt alapértelmezett futási térben alapvető Windows PowerShell-parancsok tölti be, egy egyéni futási teret, amely betölti az összes parancs csak egy meghatározott részhalmazát is létrehozhat.</span><span class="sxs-lookup"><span data-stu-id="b88cb-134">While the default runspace used in the previous examples loads all of the core Windows PowerShell commands, you can create a custom runspace that loads only a specified subset of all commands.</span></span> <span data-ttu-id="b88cb-135">Ennek a teljesítmény javítása érdekében érdemes (parancsok nagyobb számú betöltése a teljesítmény találat), vagy korlátozhatja a funkció a felhasználó a műveletek végrehajtásához.</span><span class="sxs-lookup"><span data-stu-id="b88cb-135">You might want to do this to improve performance (loading a larger number of commands is a performance hit), or to restrict the capability of the user to perform operations.</span></span> <span data-ttu-id="b88cb-136">A futási térrel, amely csak korlátozott számú parancsok egy korlátozott futási térrel nevezzük.</span><span class="sxs-lookup"><span data-stu-id="b88cb-136">A runspace that exposes only a limited number of commands is called a constrained runspace.</span></span> <span data-ttu-id="b88cb-137">Hozzon létre egy korlátozott futási térrel, használja a [System.Management.Automation.Runspaces.Runspace](/dotnet/api/System.Management.Automation.Runspaces.Runspace) és [System.Management.Automation.Runspaces.InitialSessionState](/dotnet/api/System.Management.Automation.Runspaces.InitialSessionState) osztályokat.</span><span class="sxs-lookup"><span data-stu-id="b88cb-137">To create a constrained runspace, you use the [System.Management.Automation.Runspaces.Runspace](/dotnet/api/System.Management.Automation.Runspaces.Runspace) and [System.Management.Automation.Runspaces.InitialSessionState](/dotnet/api/System.Management.Automation.Runspaces.InitialSessionState) classes.</span></span>

### <a name="creating-an-initialsessionstate-object"></a><span data-ttu-id="b88cb-138">Egy InitialSessionState objektum létrehozása</span><span class="sxs-lookup"><span data-stu-id="b88cb-138">Creating an InitialSessionState object</span></span>

<span data-ttu-id="b88cb-139">Hozzon létre egy egyéni futási teret, hogy először létre kell hozni egy [System.Management.Automation.Runspaces.InitialSessionState](/dotnet/api/System.Management.Automation.Runspaces.InitialSessionState) objektum.</span><span class="sxs-lookup"><span data-stu-id="b88cb-139">To create a custom runspace, you must first create an [System.Management.Automation.Runspaces.InitialSessionState](/dotnet/api/System.Management.Automation.Runspaces.InitialSessionState) object.</span></span> <span data-ttu-id="b88cb-140">A következő példában használunk a [System.Management.Automation.Runspaces.RunspaceFactory](/dotnet/api/System.Management.Automation.Runspaces.RunspaceFactory) egy ruspace létrehozni egy alapértelmezett létrehozása után [System.Management.Automation.Runspaces.InitialSessionState](/dotnet/api/System.Management.Automation.Runspaces.InitialSessionState) objektum.</span><span class="sxs-lookup"><span data-stu-id="b88cb-140">In the following example, we use the [System.Management.Automation.Runspaces.RunspaceFactory](/dotnet/api/System.Management.Automation.Runspaces.RunspaceFactory) to create a ruspace after creating a default [System.Management.Automation.Runspaces.InitialSessionState](/dotnet/api/System.Management.Automation.Runspaces.InitialSessionState) object.</span></span>

```csharp
InitialSessionState iss = InitialSessionState.CreateDefault();
Runspace rs = RunspaceFactory.CreateRunspace(iss);
rs.Open();
PowerShell ps = PowerShell.Create();
ps.Runspace = rs;
ps.AddCommand("Get-Command");
ps.Invoke();
```

### <a name="constraining-the-runspace"></a><span data-ttu-id="b88cb-141">A futási térben neve</span><span class="sxs-lookup"><span data-stu-id="b88cb-141">Constraining the runspace</span></span>

<span data-ttu-id="b88cb-142">Az előző példában létrehoztunk egy alapértelmezett [System.Management.Automation.Runspaces.InitialSessionState](/dotnet/api/System.Management.Automation.Runspaces.InitialSessionState) objektum, amely a beépített Windows PowerShell core tölti be.</span><span class="sxs-lookup"><span data-stu-id="b88cb-142">In the previous example, we created a default [System.Management.Automation.Runspaces.InitialSessionState](/dotnet/api/System.Management.Automation.Runspaces.InitialSessionState) object that loads all of the built-in core Windows PowerShell.</span></span> <span data-ttu-id="b88cb-143">Sikerült is rendelkezik felhívtuk a [System.Management.Automation.Runspaces.InitialSessionState.CreateDefault2\*](/dotnet/api/System.Management.Automation.Runspaces.InitialSessionState.CreateDefault2) módszer, amely csak a Mirosoft.PowerShell.Core szereplő parancsok szeretné betölteni InitialSessionState objektum létrehozása beépülő modul.</span><span class="sxs-lookup"><span data-stu-id="b88cb-143">We could also have called the [System.Management.Automation.Runspaces.InitialSessionState.CreateDefault2\*](/dotnet/api/System.Management.Automation.Runspaces.InitialSessionState.CreateDefault2) method to create an InitialSessionState object that would load only the commands in the Mirosoft.PowerShell.Core snapin.</span></span> <span data-ttu-id="b88cb-144">Hozzon létre egy több korlátozott futási térrel, létre kell hoznia egy üres [System.Management.Automation.Runspaces.InitialSessionState](/dotnet/api/System.Management.Automation.Runspaces.InitialSessionState) meghívásával objektum a [ System.Management.Automation.Runspaces.InitialSessionState.Create\*](/dotnet/api/System.Management.Automation.Runspaces.InitialSessionState.Create) módot, majd adja hozzá a InitialSessionState parancsokat.</span><span class="sxs-lookup"><span data-stu-id="b88cb-144">To create a more constrained runspace, you must create an empty [System.Management.Automation.Runspaces.InitialSessionState](/dotnet/api/System.Management.Automation.Runspaces.InitialSessionState) object by calling the [System.Management.Automation.Runspaces.InitialSessionState.Create\*](/dotnet/api/System.Management.Automation.Runspaces.InitialSessionState.Create) method, and then add commands to the InitialSessionState.</span></span>

<span data-ttu-id="b88cb-145">A futási térrel, amely betölti, csak az Ön által megadott parancsok használatával jelentősen nagyobb teljesítményt nyújt.</span><span class="sxs-lookup"><span data-stu-id="b88cb-145">Using a runspace that loads only the commands that you specify provides significantly improved performance.</span></span>

<span data-ttu-id="b88cb-146">A módszereket használ a [System.Management.Automation.Runspaces.SessionStateCmdletEntry](/dotnet/api/System.Management.Automation.Runspaces.SessionStateCmdletEntry) osztály-parancsmagok a kezdeti munkamenet-állapot meghatározásához.</span><span class="sxs-lookup"><span data-stu-id="b88cb-146">You use the methods of the [System.Management.Automation.Runspaces.SessionStateCmdletEntry](/dotnet/api/System.Management.Automation.Runspaces.SessionStateCmdletEntry) class to define cmdlets for the initial session state.</span></span> <span data-ttu-id="b88cb-147">Az alábbi példa létrehoz egy üres kezdeti munkamenet-állapot, majd határozza meg, és hozzáadja a `Get-Command` és `Import-Module` kezdeti munkamenet-állapot parancs.</span><span class="sxs-lookup"><span data-stu-id="b88cb-147">The following example creates an empty initial session state, then defines and adds the `Get-Command` and `Import-Module` commands to the initial session state.</span></span> <span data-ttu-id="b88cb-148">Hozunk majd létre egy adott kezdeti munkamenet-állapot által korlátozott futási térrel, és hajtsa végre a parancsokat, hogy futási térben található.</span><span class="sxs-lookup"><span data-stu-id="b88cb-148">We then create a runspace constrained by that initial session state, and execute the commands in that runspace.</span></span>

<span data-ttu-id="b88cb-149">Hozzon létre az első munkamenet-állapot.</span><span class="sxs-lookup"><span data-stu-id="b88cb-149">Create the initial session state.</span></span>

```csharp
InitialSessionState iss = InitialSessionState.Create();
```

<span data-ttu-id="b88cb-150">Parancsok hozzáadása az első munkamenet-állapot és megadása.</span><span class="sxs-lookup"><span data-stu-id="b88cb-150">Define and add commands to the initial session state.</span></span>

```csharp
SessionStateCmdletEntry getCommand = new SessionStateCmdletEntry(
        "Get-Command", typeof(Microsoft.PowerShell.Commands.GetCommandCommand), "");
SessionStateCmdletEntry importModule = new SessionStateCmdletEntry(
        "Import-Module", typeof(Microsoft.PowerShell.Commands.ImportModuleCommand), "");
iss.Commands.Add(getCommand);
iss.Commands.Add(importModule);
```

<span data-ttu-id="b88cb-151">Hozzon létre, és nyissa meg a futási térben.</span><span class="sxs-lookup"><span data-stu-id="b88cb-151">Create and open the runspace.</span></span>

```csharp
Runspace rs = RunspaceFactory.CreateRunspace(iss);
rs.Open();
```

<span data-ttu-id="b88cb-152">Hajtsa végre a parancsot, és az eredmény megjelenítése.</span><span class="sxs-lookup"><span data-stu-id="b88cb-152">Execute a command and show the result.</span></span>

```csharp
PowerShell ps = PowerShell.Create();
ps.Runspace = rs;
ps.AddCommand("Get-Command");
Collection<CommandInfo> result = ps.Invoke<CommandInfo>();
foreach (var entry in result)
{
       Console.WriteLine(entry.Name);
}
```

<span data-ttu-id="b88cb-153">A futtatásakor, ez a kód kimenete módon fog kinézni.</span><span class="sxs-lookup"><span data-stu-id="b88cb-153">When run, the output of this code will look as follows.</span></span>

```powershell
Get-Command
Import-Module
```
