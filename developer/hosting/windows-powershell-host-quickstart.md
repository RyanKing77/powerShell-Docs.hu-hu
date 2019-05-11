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
ms.openlocfilehash: 9a080b6db7416ae6bf65a1b0353e9f17a56cc6c5
ms.sourcegitcommit: 00cf9a99972ce40db7c25b9a3fc6152dec6bddb6
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/28/2019
ms.locfileid: "64530619"
---
# <a name="windows-powershell-host-quickstart"></a>Windows PowerShell-gazda – Gyors üzembe helyezés

Az alkalmazás futtatásához a Windows PowerShell, használja a [System.Management.Automation.PowerShell](/dotnet/api/System.Management.Automation.PowerShell) osztály.
Ez az osztály metódusokat, hozzon létre egy folyamatot a parancsok, majd hajtsa végre ezeket a parancsokat egy futási teret biztosít.
Hozzon létre egy fogadó alkalmazás legegyszerűbb módja, hogy az alapértelmezett futási térből.
Az alapértelmezett futási térben összes az alapvető Windows PowerShell-parancsokat tartalmazza.
Ha azt szeretné, hogy az alkalmazás elérhetővé a Windows PowerShell-parancsokat csak egy részhalmazát, létre kell hoznia egy egyéni futási térből.

## <a name="using-the-default-runspace"></a>Az alapértelmezett futási teret használ

Indítása, azt fogja alapértelmezett futási térben, majd a módszereket a [System.Management.Automation.PowerShell](/dotnet/api/System.Management.Automation.PowerShell) osztály parancsok, paraméterek, utasításokat és parancsfájlokat hozzáadni egy folyamatot.

### <a name="addcommand"></a>AddCommand

Használja a [System.Management.Automation.Powershell.AddCommand](/dotnet/api/System.Management.Automation.PowerShell.AddCommand) metódus parancsok hozzáadása a folyamatban.
Például tegyük fel, hogy a gépen futó folyamatok listájának beolvasása.
A módszer futtassa a következő parancsot a következőképpen történik.

1. Hozzon létre egy [System.Management.Automation.PowerShell](/dotnet/api/System.Management.Automation.PowerShell) objektum.

   ```csharp
   PowerShell ps = PowerShell.Create();
   ```

2. Adja hozzá a végrehajtani kívánt parancsot.

   ```csharp
   ps.AddCommand("Get-Process");
   ```

3. Hívja meg a parancsot.

   ```csharp
   ps.Invoke();
   ```

Ha a AddCommand metódus hívása előtt többször hívás a [System.Management.Automation.Powershell.Invoke](/dotnet/api/System.Management.Automation.PowerShell.Invoke) módot, az első parancs eredménye van irányíthatja át a második, és így tovább.
Ha nem szeretne egy parancsot az előző parancs eredménye kanálu, adja hozzá meghívásával a [System.Management.Automation.Powershell.AddStatement](/dotnet/api/System.Management.Automation.PowerShell.AddStatement) helyette.

### <a name="addparameter"></a>AddParameter

Az előző példában egyetlen parancs paraméterek nélkül hajtja végre.
Használatával a parancshoz paramétereket is hozzáadhat a [System.Management.Automation.PSCommand.AddParameter](/dotnet/api/System.Management.Automation.PSCommand.AddParameter) metódust.
Például a következő kódot az összes folyamat, amely a nevesített listájának lekérése `PowerShell` fut a gépen.

```csharp
PowerShell.Create().AddCommand("Get-Process")
                   .AddParameter("Name", "PowerShell")
                   .Invoke();
```

További paraméterek AddParameter metódus meghívásának többször is hozzáadhat.

```csharp
PowerShell.Create().AddCommand("Get-Process")
                   .AddParameter("Name", "PowerShell")
                   .AddParameter("Id", "12768")
                   .Invoke();
```

Paraméterek és értékek tartalmazó meghívásával is hozzáadhat a [System.Management.Automation.PowerShell.AddParameters](/dotnet/api/System.Management.Automation.PowerShell.AddParameters) metódust.

```csharp
IDictionary parameters = new Dictionary<String, String>();
parameters.Add("Name", "PowerShell");

parameters.Add("Id", "12768");
PowerShell.Create().AddCommand("Get-Process")
   .AddParameters(parameters)
      .Invoke()

```

### <a name="addstatement"></a>AddStatement

A kötegelés szimulálhatja a [System.Management.Automation.PowerShell.AddStatement](/dotnet/api/System.Management.Automation.PowerShell.AddStatement) metódussal, amely egy további utasítást ad hozzá a folyamat végén.
A következő kódot a futó folyamatok nevű listáját kéri le `PowerShell`, és majd a szolgáltatások listájának beolvasása.

```csharp
PowerShell ps = PowerShell.Create();
ps.AddCommand("Get-Process").AddParameter("Name", "PowerShell");
ps.AddStatement().AddCommand("Get-Service");
ps.Invoke();
```

### <a name="addscript"></a>AddScript

Meglévő parancsfájl meghívásával futtathatja a [System.Management.Automation.PowerShell.AddScript](/dotnet/api/System.Management.Automation.PowerShell.AddScript) metódust.
Az alábbi példa hozzáad egy parancsfájlt a folyamat, és futtatása.
Ez a példa feltételezi, hogy már van egy nevű szkriptet `MyScript.ps1` nevű mappába `D:\PSScripts`.

```csharp
PowerShell ps = PowerShell.Create();
ps.AddScript("D:\PSScripts\MyScript.ps1").Invoke();
```

Is van, amely egy logikai paramétert nevű AddScript metódus verzió `useLocalScope`.
Ha ez a paraméter értéke `true`, akkor a szkript futtatása helyi hatókörében.
A következő kódot fog futtassa a szkriptet a helyi hatókörében.

```csharp
PowerShell ps = PowerShell.Create();
ps.AddScript(@"D:\PSScripts\MyScript.ps1", true).Invoke();
```

## <a name="creating-a-custom-runspace"></a>Egy egyéni futási teret létrehozása

Míg a korábbi példákban használt alapértelmezett futási térben alapvető Windows PowerShell-parancsok tölti be, egy egyéni futási teret, amely betölti az összes parancs csak egy meghatározott részhalmazát is létrehozhat.
Ennek a teljesítmény javítása érdekében érdemes (parancsok nagyobb számú betöltése a teljesítmény találat), vagy korlátozhatja a funkció a felhasználó a műveletek végrehajtásához.
A futási térrel, amely csak korlátozott számú parancsok egy korlátozott futási térrel nevezzük.
Hozzon létre egy korlátozott futási térrel, használja a [System.Management.Automation.Runspaces.Runspace](/dotnet/api/System.Management.Automation.Runspaces.Runspace) és [System.Management.Automation.Runspaces.InitialSessionState](/dotnet/api/System.Management.Automation.Runspaces.InitialSessionState) osztályokat.

### <a name="creating-an-initialsessionstate-object"></a>Egy InitialSessionState objektum létrehozása

Hozzon létre egy egyéni futási teret, hogy először létre kell hozni egy [System.Management.Automation.Runspaces.InitialSessionState](/dotnet/api/System.Management.Automation.Runspaces.InitialSessionState) objektum.
A következő példában használunk a [System.Management.Automation.Runspaces.RunspaceFactory](/dotnet/api/System.Management.Automation.Runspaces.RunspaceFactory) egy futási teret létrehozni egy alapértelmezett InitialSessionState objektum létrehozása után.

```csharp
InitialSessionState iss = InitialSessionState.CreateDefault();
Runspace rs = RunspaceFactory.CreateRunspace(iss);
rs.Open();
PowerShell ps = PowerShell.Create();
ps.Runspace = rs;
ps.AddCommand("Get-Command");
ps.Invoke();
```

### <a name="constraining-the-runspace"></a>A futási térben neve

Az előző példában létrehoztunk egy alapértelmezett [System.Management.Automation.Runspaces.InitialSessionState](/dotnet/api/System.Management.Automation.Runspaces.InitialSessionState) objektum, amely a beépített Windows PowerShell core tölti be.
Sikerült is rendelkezik felhívtuk a [System.Management.Automation.Runspaces.InitialSessionState.CreateDefault2](/dotnet/api/System.Management.Automation.Runspaces.InitialSessionState.CreateDefault2) módszer, amely csak a Microsoft.PowerShell.Core szereplő parancsok szeretné betölteni InitialSessionState objektum létrehozása beépülő modul.
Hozzon létre egy több korlátozott futási térrel, létre kell hoznia egy üres InitialSessionState objektum meghívásával a [System.Management.Automation.Runspaces.InitialSessionState.Create](/dotnet/api/System.Management.Automation.Runspaces.InitialSessionState.Create) módot, majd adja hozzá a parancsokat a InitialSessionState.

A futási térrel, amely betölti, csak az Ön által megadott parancsok használatával jelentősen nagyobb teljesítményt nyújt.

A módszereket használ a [System.Management.Automation.Runspaces.SessionStateCmdletEntry](/dotnet/api/System.Management.Automation.Runspaces.SessionStateCmdletEntry) osztály-parancsmagok a kezdeti munkamenet-állapot meghatározásához.
Az alábbi példa létrehoz egy üres kezdeti munkamenet-állapot, majd határozza meg, és hozzáadja a `Get-Command` és `Import-Module` kezdeti munkamenet-állapot parancs.
Hozunk majd létre egy adott kezdeti munkamenet-állapot által korlátozott futási térrel, és hajtsa végre a parancsokat, hogy futási térben található.

Hozzon létre az első munkamenet-állapot.

```csharp
InitialSessionState iss = InitialSessionState.Create();
```

Parancsok hozzáadása az első munkamenet-állapot és megadása.

```csharp
SessionStateCmdletEntry getCommand = new SessionStateCmdletEntry(
        "Get-Command", typeof(Microsoft.PowerShell.Commands.GetCommandCommand), "");
SessionStateCmdletEntry importModule = new SessionStateCmdletEntry(
        "Import-Module", typeof(Microsoft.PowerShell.Commands.ImportModuleCommand), "");
iss.Commands.Add(getCommand);
iss.Commands.Add(importModule);
```

Hozzon létre, és nyissa meg a futási térben.

```csharp
Runspace rs = RunspaceFactory.CreateRunspace(iss);
rs.Open();
```

Hajtsa végre a parancsot, és az eredmény megjelenítése.

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

A futtatásakor, ez a kód kimenete módon fog kinézni.

```powershell
Get-Command
Import-Module
```
