---
title: A parancsmag létrehozása, amely módosítja a rendszer |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- should process [PowerShell Programmer's Guide]
- should continue [PowerShell Programmer's Guide]
- user feedback [PowerShell Programmer's Guide]
- confirm impact [PowerShell Programmer's Guide]
ms.assetid: 59be4120-1700-4d92-a308-ef4a32ccf11a
caps.latest.revision: 8
ms.openlocfilehash: bbe9f0213754d1cc47e0fd9a7a898bde916c0636
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62068439"
---
# <a name="creating-a-cmdlet-that-modifies-the-system"></a>Rendszermódosító parancsmag létrehozása

A parancsmag néha módosítani kell a futó állapotot a rendszer, nem csak a Windows PowerShell-modul állapotát. Ezekben az esetekben a parancsmag engedélyezi a felhasználó egy alkalommal-e a módosítás megerősítéséhez.

A parancsmag megerősítést támogatásához két dolgot kell tennie.

- Deklarálja, hogy a parancsmag megerősítést támogatja a megadása esetén a [System.Management.Automation.CmdletAttribute](/dotnet/api/System.Management.Automation.CmdletAttribute) úgy, hogy kulcsszó Cmdletbinding attribútum `true`.

- Hívás [System.Management.Automation.Cmdlet.ShouldProcess](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) (ahogyan az az alábbi példában látható) a parancsmag végrehajtása közben.

Megerősítő támogatásával parancsmag tesz elérhetővé a `Confirm` és `WhatIf` paraméterek, amelyeket a Windows PowerShell által biztosított, és megfelel a fejlesztési irányelveket a parancsmagok (parancsmag fejlesztési irányelvek kapcsolatos további információkért lásd: [ A parancsmag fejlesztési irányelvek](./cmdlet-development-guidelines.md).).

## <a name="changing-the-system"></a>A rendszer módosítása

A művelet, "módosítása a rendszer", amely potenciálisan a Windows PowerShell kívül a rendszer állapotának módosítása minden parancsmag hivatkozik. Ha például leállítása folyamatban van egy folyamat, engedélyezése vagy letiltása egy felhasználói fiókot, vagy egy sort egy adatbázistábla soraihoz való is meg kell erősíteni a rendszer az összes változtatás hozzáadása. Ezzel szemben az operatív adatok olvasása vagy átmeneti kapcsolatokat hozhat létre ne módosítsa a rendszer, és általában nem kell megerősítést. Megerősítő is nem szükséges műveleteket, amelynek érvénybe korlátozódik belül a Windows PowerShell-futtatókörnyezet, mint például a `set-variable`. Parancsmagok, amelyek vagy előfordulhat, hogy nem módosítsa egy állandó deklarálnia kell `SupportsShouldProcess` hívja [System.Management.Automation.Cmdlet.ShouldProcess](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) csak akkor, ha azok készül, hogy módosítsa egy állandó.

> [!NOTE]
> ShouldProcess megerősítő csak parancsmagok vonatkozik. Ha egy parancs vagy parancsfájl módosítja a futó állapotot a rendszer közvetlenül meghívásával a .NET-metódusokat és tulajdonságokat, vagy a hívó alkalmazások, kívül a Windows PowerShell, az ilyen típusú megerősítő nem lesz elérhető.

## <a name="the-stopproc-cmdlet"></a>A StopProc parancsmag

Ez a témakör ismerteti, amely megpróbálja leállítani a folyamatokat, amelyek a Get-Proc parancsmaggal olvassa be a Stop-Proc parancsmag (ismertetett [létrehozásához az első parancsmag](./creating-a-cmdlet-without-parameters.md)).

Ez a szakasz témakörei a következők:

- [A parancsmag meghatározása](#Defining-the-Cmdlet)

- [A rendszer módosítás paraméterek megadása](#Defining-Parameters-for-System-Modification)

- [Egy bemeneti metódus feldolgozási felülbírálása](#Overriding-an-Input-Processing-Method)

- [A ShouldProcess metódus hívása](#Calling-the-ShouldProcess-Method)

- [A ShouldContinue metódus hívása](#Calling-the-ShouldContinue-Method)

- [A bemeneti feldolgozó leállítása](#Stopping-Input-Processing)

- [Kódminta](#Code-Sample)

- [Objektumtípusok definiálása és formázása](#Defining-Object-Types-and-Formatting)

- [A parancsmag készítése](#Building-the-Cmdlet)

- [A parancsmag tesztelése](#Testing-the-Cmdlet)

## <a name="defining-the-cmdlet"></a>A parancsmag meghatározása

Mindig a parancsmag elnevezési és a .NET-osztály, amely megvalósítja a parancsmag deklaráló parancsmag létrehozásának első lépése. Kell írnia egy parancsmaggal módosíthatja, a rendszer, mert ennek megfelelően kell elnevezni azt. A parancsmag leáll rendszer folyamataihoz, így az itt választott művelet neve "Stop" határozzák meg a [System.Management.Automation.Verbslifecycle](/dotnet/api/System.Management.Automation.VerbsLifeCycle) osztályt, a főnév "Proc" jelzi, hogy a parancsmag leállítja a folyamatot. A parancsmag jóváhagyott igék kapcsolatos további információkért lásd: [művelet neve](./approved-verbs-for-windows-powershell-commands.md).

A Stop-Proc parancsmag osztály definícióját a következő:

```csharp
[Cmdlet(VerbsLifecycle.Stop, "Proc",
        SupportsShouldProcess = true)]
public class StopProcCommand : Cmdlet
```

Vegye figyelembe, hogy a [System.Management.Automation.CmdletAttribute](/dotnet/api/System.Management.Automation.CmdletAttribute) nyilatkozat, a `SupportsShouldProcess` kulcsszó attribútum értéke `true` engedélyezéséhez a parancsmag való meghíváshoz [ System.Management.Automation.Cmdlet.ShouldProcess](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) és [System.Management.Automation.Cmdlet.ShouldContinue](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue). A kulcsszó beállítása nélkül a `Confirm` és `WhatIf` paraméterek nem lesz elérhető, a felhasználó számára.

### <a name="extremely-destructive-actions"></a>Rendkívül felülíró művelet

Egyes műveletek károsak rendkívül, például egy aktív merevlemez-partíciók újraformázást. Ezekben az esetekben a parancsmag kell beállítania `ConfirmImpact`  =  `ConfirmImpact.High` deklarálásakor a [System.Management.Automation.CmdletAttribute](/dotnet/api/System.Management.Automation.CmdletAttribute) attribútum. Ez a beállítás kényszeríti a parancsmag kérelem felhasználói jóváhagyás, akkor is, ha a felhasználó nem adta meg a `Confirm` paraméter. Azonban a parancsmag a fejlesztők kerülendő túlzott mértékű használata `ConfirmImpact` műveletek, amelyek csak potenciálisan ártalmas, például a felhasználói fiók törlése. Ne feledje, hogy `ConfirmImpact` értékre van állítva [System.Management.Automation.Confirmimpact.High](/dotnet/api/System.Management.Automation.ConfirmImpact.High).

Egyes műveletekre hasonló módon, nagy valószínűséggel nem romboló, Bár elméletben módosíthatják kívül a Windows PowerShell rendszert a futó állapotot. Az ilyen parancsmagok állíthatja `ConfirmImpact` való [System.Management.Automation.Confirmimpact.Low](/dotnet/api/system.management.automation.confirmimpact?view=powershellsdk-1.1.0). Ez fog kerülni eseménymegerősítési kéréseknek, ahol a felhasználó erősítse meg a csak a közepes hatású és a nagy hatású műveletek kérte.

## <a name="defining-parameters-for-system-modification"></a>A rendszer módosítás paraméterek megadása

Ez a szakasz ismerteti, hogyan adhat meg a parancsmag paramétereit, beleértve azokat is, a támogatási rendszerben módosítás van szükség. Lásd: [a folyamat CommandLine bemeneti paramétereket adunk hozzá](./adding-parameters-that-process-command-line-input.md) Ha paramétereket meghatározó kapcsolatos általános információra van szüksége.

A Stop-Proc parancsmag meghatározása három paramétert: `Name`, `Force`, és `PassThru`.

A `Name` paraméter felel meg a `Name` a folyamat bemeneti objektum tulajdonságát. Vegye figyelembe, hogy a `Name` ebben a példában paramétert kötelező, mivel a parancsmag sikertelen lesz, ha nem rendelkezik egy névvel ellátott folyamat leállítása.

A `Force` paraméter lehetővé teszi, hogy a felhasználó felülbírálhatja a hívások [System.Management.Automation.Cmdlet.ShouldContinue](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue). Tulajdonképpen bármely parancsmag, amely meghívja a [System.Management.Automation.Cmdlet.ShouldContinue](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) rendelkeznie kell egy `Force` paramétert, hogy amikor `Force` van megadva, a parancsmag meghívása kihagyja [ System.Management.Automation.Cmdlet.ShouldContinue](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) és folytatja a műveletet. Vegye figyelembe, hogy ez nincs hatással a hívások [System.Management.Automation.Cmdlet.ShouldProcess](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess).

A `PassThru` paraméter lehetővé teszi, hogy a felhasználó-e a parancsmag adja át a kimeneti objektum keresztül, ebben az esetben egy folyamat Leállítás utáni jelzi. Vegye figyelembe, hogy ezt a paramétert a parancsmaghoz saját maga helyett egy tulajdonság a bemeneti objektum van kötve.

Íme a Stop-Proc parancsmagok a paraméterdeklarációhoz.

```csharp
[Parameter(
           Position = 0,
           Mandatory = true,
           ValueFromPipeline = true,
           ValueFromPipelineByPropertyName = true
)]
public string[] Name
{
  get { return processNames; }
  set { processNames = value; }
}
private string[] processNames;

/// <summary>
/// Specify the Force parameter that allows the user to override
/// the ShouldContinue call to force the stop operation. This
/// parameter should always be used with caution.
/// </summary>
[Parameter]
public SwitchParameter Force
{
  get { return force; }
  set { force = value; }
}
private bool force;

/// <summary>
/// Specify the PassThru parameter that allows the user to specify
/// that the cmdlet should pass the process object down the pipeline
/// after the process has been stopped.
/// </summary>
[Parameter]
public SwitchParameter PassThru
{
  get { return passThru; }
  set { passThru = value; }
}
private bool passThru;
```

## <a name="overriding-an-input-processing-method"></a>Egy bemeneti metódus feldolgozási felülbírálása

A parancsmag felül kell írnia egy bemeneti metódus feldolgozása. Az alábbi kód bemutatja a [System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) használja a Stop-Proc parancsmagra felülbírálás. Az egyes kért Folyamatnév, ez a módszer biztosítja, hogy a folyamat nem egy külön folyamat, megkísérli leállítani a folyamatot, és ezután elküldi a kimeneti objektum, ha a `PassThru` paraméter meg van adva.

```csharp
protected override void ProcessRecord()
{
  foreach (string name in processNames)
  {
    // For every process name passed to the cmdlet, get the associated
    // process(es). For failures, write a non-terminating error
    Process[] processes;

    try
    {
      processes = Process.GetProcessesByName(name);
    }
    catch (InvalidOperationException ioe)
    {
      WriteError(new ErrorRecord(ioe,"Unable to access the target process by name",
                 ErrorCategory.InvalidOperation, name));
      continue;
    }

    // Try to stop the process(es) that have been retrieved for a name
    foreach (Process process in processes)
    {
      string processName;

      try
      {
        processName = process.ProcessName;
      }

      catch (Win32Exception e)
        {
          WriteError(new ErrorRecord(e, "ProcessNameNotFound",
                     ErrorCategory.ReadError, process));
          continue;
        }

        // Call Should Process to confirm the operation first.
        // This is always false if WhatIf is set.
        if (!ShouldProcess(string.Format("{0} ({1})", processName,
                           process.Id)))
        {
          continue;
        }
        // Call ShouldContinue to make sure the user really does want
        // to stop a critical process that could possibly stop the computer.
        bool criticalProcess =
             criticalProcessNames.Contains(processName.ToLower());

        if (criticalProcess &&!force)
        {
          string message = String.Format
                ("The process \"{0}\" is a critical process and should not be stopped. Are you sure you wish to stop the process?",
                processName);

          // It is possible that ProcessRecord is called multiple times
          // when the Name parameter receives objects as input from the
          // pipeline. So to retain YesToAll and NoToAll input that the
          // user may enter across multiple calls to ProcessRecord, this
          // information is stored as private members of the cmdlet.
          if (!ShouldContinue(message, "Warning!",
                              ref yesToAll,
                              ref noToAll))
          {
            continue;
          }
        } // if (criticalProcess...
        // Stop the named process.
        try
        {
          process.Kill();
        }
        catch (Exception e)
        {
          if ((e is Win32Exception) || (e is SystemException) ||
              (e is InvalidOperationException))
          {
            // This process could not be stopped so write
            // a non-terminating error.
            string message = String.Format("{0} {1} {2}",
                             "Could not stop process \"", processName,
                             "\".");
            WriteError(new ErrorRecord(e, message,
                       ErrorCategory.CloseError, process));
                       continue;
          } // if ((e is...
          else throw;
        } // catch

        // If the PassThru parameter argument is
        // True, pass the terminated process on.
        if (passThru)
        {
          WriteObject(process);
        }
    } // foreach (Process...
  } // foreach (string...
} // ProcessRecord
```

## <a name="calling-the-shouldprocess-method"></a>A ShouldProcess metódus hívása

A feldolgozási mód a parancsmag bemeneti meg kell hívnia a [System.Management.Automation.Cmdlet.ShouldProcess](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) metódust (például törlése fájlok) módosításakor a működőképes állapotba előtt, győződjön meg arról, hogy egy művelet végrehajtása a rendszer. Ez lehetővé teszi a Windows PowerShell modul megadnia a rendszerhéjból a megfelelő "WhatIf" és "Confirm" viselkedését.

> [!NOTE]
> Ha a parancsmag kijelenti, hogy támogatja a kell dolgoznia, és győződjön meg arról, hogy nem sikerül a [System.Management.Automation.Cmdlet.ShouldProcess](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) hívja, a felhasználó váratlanul előfordulhat, hogy módosítsa a rendszer.

A hívás [System.Management.Automation.Cmdlet.ShouldProcess](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) küld a felhasználó a Windows PowerShell-futtatókörnyezetben, figyelembe véve parancssori beállítást vagy preferenciaváltozók módosítani az erőforrás neve a meghatározása, mi megjelenjenek a felhasználó számára.

Az alábbi példa bemutatja a hívást [System.Management.Automation.Cmdlet.ShouldProcess](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) a felülbírálását a [System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) metódusban a minta Állítsa le a folyamaton parancsmagot.

```csharp
if (!ShouldProcess(string.Format("{0} ({1})", processName,
                   process.Id)))
{
  continue;
}
```

## <a name="calling-the-shouldcontinue-method"></a>A ShouldContinue metódus hívása

A hívást a [System.Management.Automation.Cmdlet.ShouldContinue](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) metódus elküld egy másodlagos üzenetet a felhasználónak. A kérés érkezett hívása után [System.Management.Automation.Cmdlet.ShouldProcess](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) adja vissza `true` , és ha a `Force` paraméter nem volt beállítva `true`. A felhasználó ezután visszajelzést küldhet a tegyük fel, hogy a művelet folytatni kell. A parancsmag hívásokat [System.Management.Automation.Cmdlet.ShouldContinue](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) , egy további ellenőrzési potenciálisan veszélyes rendszermódosítások, vagy ha szeretné, hogy a felhasználó igen-mindig és nem mindig beállításokat biztosítson.

Az alábbi példa bemutatja a hívást [System.Management.Automation.Cmdlet.ShouldContinue](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) a felülbírálását a [System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) metódusban a minta Állítsa le a folyamaton parancsmagot.

```csharp
if (criticalProcess &&!force)
{
  string message = String.Format
        ("The process \"{0}\" is a critical process and should not be stopped. Are you sure you wish to stop the process?",
        processName);

  // It is possible that ProcessRecord is called multiple times
  // when the Name parameter receives objects as input from the
  // pipeline. So to retain YesToAll and NoToAll input that the
  // user may enter across multiple calls to ProcessRecord, this
  // information is stored as private members of the cmdlet.
  if (!ShouldContinue(message, "Warning!",
                      ref yesToAll,
                      ref noToAll))
  {
    continue;
  }
} // if (criticalProcess...
```

## <a name="stopping-input-processing"></a>A bemeneti feldolgozó leállítása

A bemenet feldolgozásának leállítása lehetőséget kell biztosítani a metódus egy parancsmag, amellyel a rendszer a módosítások feldolgozása a bemeneti. A Stop-Proc parancsmag esetében a kérés érkezett a [System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) metódust a [System.Diagnostics.Process.Kill*](/dotnet/api/System.Diagnostics.Process.Kill) metódust. Mivel a `PassThru` paraméter értéke `true`, [System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) is meghívja [System.Management.Automation.Cmdlet.WriteObject](/dotnet/api/System.Management.Automation.Cmdlet.WriteObject) küldése a folyamat objektumról a folyamathoz.

## <a name="code-sample"></a>Kódminta

A teljes C# mintakód, lásd: [StopProcessSample01 minta](./stopprocesssample01-sample.md).

## <a name="defining-object-types-and-formatting"></a>Objektumtípusok definiálása és formázása

Windows PowerShell parancsmagok használatával a .net-objektumokká közötti továbbítja. Ennek következtében a parancsmag előfordulhat, hogy meg kell határoznia a saját típusát, vagy a parancsmag előfordulhat, hogy ki kell terjesztenie egy másik parancsmag által biztosított meglévő típus. Új típusok meghatározása, vagy meglévő típusok bővítésével kapcsolatos további információkért lásd: [objektumtípusok kiterjesztése és formázás](https://msdn.microsoft.com/en-us/da976d91-a3d6-44e8-affa-466b1e2bd351).

## <a name="building-the-cmdlet"></a>A parancsmag készítése

Parancsmag-k megvalósítása után regisztrálni kell a Windows PowerShell-lel a Windows PowerShell beépülő modullal. Parancsmagok regisztrálásával kapcsolatos további információkért lásd: [parancsmagjainak regisztrálásához, a szolgáltatók és az alkalmazások üzemeltetése hogyan](https://msdn.microsoft.com/en-us/a41e9054-29c8-40ab-bf2b-8ce4e7ec1c8c).

## <a name="testing-the-cmdlet"></a>A parancsmag tesztelése

Ha a parancsmagot a Windows PowerShell-lel regisztrálva lett, azt a parancssorból való futtatásával tesztelheti. Az alábbiakban számos tesztet, amely a Stop-Proc parancsmag teszteléséhez. A parancssorból-parancsmagokkal kapcsolatos további információkért lásd: a [első lépések a Windows PowerShell-lel](/powershell/scripting/getting-started/getting-started-with-windows-powershell).

- Indítsa el a Windows Powershellt, és leállítja a feldolgozást, ahogy az alábbi a Stop-Proc parancsmag használatával. Mivel a parancsmag a határozza meg a `Name` , kötelező paraméter, a parancsmag-lekérdezések a paraméterhez.

    ```powershell
    PS> stop-proc
    ```

A következő eredmény jelenik meg.

    ```
    Cmdlet stop-proc at command pipeline position 1
    Supply values for the following parameters:
    Name[0]:
    ```

- Most pedig a parancsmag használatával állítsa le a "JEGYZETTÖMB" nevű folyamatot. A parancsmag kéri, hogy erősítse meg a műveletet.

    ```powershell
    PS> stop-proc -Name notepad
    ```

A következő eredmény jelenik meg.

    ```
    Confirm
    Are you sure you want to perform this action?
    Performing operation "stop-proc" on Target "notepad (4996)".
    [Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "Y"): Y
    ```

- Használatával állítsa le a folyamaton látható módon állítsa le a kritikus fontosságú "WINLOGON" folyamatot. Ön kéri, és a művelet végrehajtása, mert ennek az operációs rendszer újraindítását kapcsolatos figyelmeztetést kap.

    ```powershell
    PS> stop-proc -Name Winlogon
    ```

A következő eredmény jelenik meg.

    ```output
    Confirm
    Are you sure you want to perform this action?
    Performing operation "stop-proc" on Target "winlogon (656)".
    [Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "Y"): Y
    Warning!
    The process " winlogon " is a critical process and should not be stopped. Are you sure you wish to stop the process?
    [Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "Y"): N
    ```

- Most próbáljon nélkül figyelmeztetést kap a WINLOGON folyamat leállítása érdekében. Vegye figyelembe, hogy használja-e ez a parancs a bejegyzés a `Force` paraméter a figyelmeztetés felülbírálása.

    ```powershell
    PS> stop-proc -Name winlogon -Force
    ```

A következő eredmény jelenik meg.

    ```output
    Confirm
    Are you sure you want to perform this action?
    Performing operation "stop-proc" on Target "winlogon (656)".
    [Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "Y"): N
    ```

## <a name="see-also"></a>Lásd még:

[Parancssori bemenet feldolgozása paraméterek hozzáadása](./adding-parameters-that-process-command-line-input.md)

[Objektumtípusok kiterjesztése és formázása](https://msdn.microsoft.com/en-us/da976d91-a3d6-44e8-affa-466b1e2bd351)

[How to Register parancsmagok, a szolgáltatók és az alkalmazások üzemeltetéséhez](https://msdn.microsoft.com/en-us/a41e9054-29c8-40ab-bf2b-8ce4e7ec1c8c)

[Windows PowerShell SDK](../windows-powershell-reference.md)

[Parancsmag-minták](./cmdlet-samples.md)