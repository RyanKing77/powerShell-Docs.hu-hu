---
title: Felhasználói üzenetek hozzáadása a parancsmaghoz |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- WriteWarning
- notifications, writing
- progress notification
- WriteVerbose
- Stop-Proc
- WriteProgress
- WriteDebug
- notifications, debug
- ProgressRecord
- samples, Stop-Proc cmdlet
- notifications, progress
- notifications, warning
- WriteObject
- WriteError
- verbose notification
- ProcessRecord
- notifications, verbose
- debug notification
- cmdlet, writing notifications
- warning
- code sample, user notifications
- user notifications
ms.assetid: 14c13acb-f0b7-4613-bc7d-c361d14da1a2
caps.latest.revision: 8
ms.openlocfilehash: 5b3a5f5d5d02c7d5a3c1d622ec1a3740739c694f
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62068776"
---
# <a name="adding-user-messages-to-your-cmdlet"></a>Felhasználói üzenetek hozzáadása a parancsmaghoz

Parancsmagok írhat a különböző típusú üzeneteket, amelyek a felhasználó által a Windows PowerShell-modul is megjelenik. Ezek az üzenetek közé tartozik a következők:

- Részletes üzeneteket, amelyek tartalmazzák az általános információkat.

- A hibakeresési információkat tartalmazó üzenetek.

- Figyelmeztető üzeneteket, amelyek tartalmaznak egy értesítés, hogy a parancsmag arra készül, hogy egy művelettel, amelyeken nem várt eredmények.

- Mennyi információkat tartalmazó üzenetek működik a parancsmag állapotjelentés befejeződött, amelyek hosszú ideig tart a művelet végrehajtása során.

Nincs korlátozva van, a parancsmag be írni képes üzenetek száma vagy a parancsmag írja az üzeneteket a típusát. Mindegyik üzenet íródik azáltal, hogy egy adott hívás a feldolgozási mód a parancsmag bemeneti adatban.

## <a name="the-stopproc-cmdlet"></a>A StopProc parancsmag

Ez a szakasz témakörei a következők:

- [A parancsmag meghatározása](#Defining-the-Cmdlet)

- [A rendszer módosítás paraméterek megadása](#Defining-Parameters-for-System-Modification)

- [Egy bemeneti metódus feldolgozási felülbírálása](#Overriding-an-Input-Processing-Method)

- [Részletes üzenet írásának](#Writing-a-Verbose-Message)

- [Hibakeresési üzenet írásának](#Writing-a-Debug-Message)

- [Egy figyelmeztető üzenet írása](#Writing-a-Warning-Message)

- [A folyamatállapot-üzenet írása](#Writing-a-Progress-Message)

- [Kódminta](#Code-Sample)

- [Objektumtípusok és formázása](#Define-Object-Types-and-Formatting)

- [A parancsmag készítése](#Building-the-Cmdlet)

- [A parancsmag tesztelése](#Testing-the-Cmdlet)

## <a name="defining-the-cmdlet"></a>A parancsmag meghatározása

Mindig a parancsmag elnevezési és a .NET-osztály, amely megvalósítja a parancsmag deklaráló parancsmag létrehozásának első lépése. Parancsmag rendezést felhasználói értesítések írhat a bemeneti feldolgozási módszerek; tehát általában nevet adhat a parancsmag minden olyan művelet, amely azt jelzi, hogy milyen system módosításokat végez a parancsmag használatával. A parancsmag jóváhagyott igék kapcsolatos további információkért lásd: [művelet neve](./approved-verbs-for-windows-powershell-commands.md).

A Stop-Proc parancsmag úgy tervezték, hogy a rendszer; módosítása ezért a [System.Management.Automation.CmdletAttribute](/dotnet/api/System.Management.Automation.CmdletAttribute) tartalmaznia kell a .NET deklarációjában a `SupportsShouldProcess` kulcsszó attribútumot, és állítható `true`.

A következő kódot a Stop-Proc parancsmag osztály definícióját. Ez a definíció kapcsolatos további információkért lásd: [létrehozása egy parancsmag, amely módosítja a rendszer](./creating-a-cmdlet-that-modifies-the-system.md).

```csharp
[Cmdlet(VerbsLifecycle.Stop, "proc",
        SupportsShouldProcess = true)]
public class StopProcCommand : Cmdlet
```

## <a name="defining-parameters-for-system-modification"></a>A rendszer módosítás paraméterek megadása

A Stop-Proc parancsmag meghatározása három paramétert: `Name`, `Force`, és `PassThru`. Ezek a paraméterek meghatározása kapcsolatos további információkért lásd: [létrehozása egy parancsmag, amely módosítja a rendszer](./creating-a-cmdlet-that-modifies-the-system.md).

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

A parancsmag felül kell írnia egy bemeneti metódus feldolgozása, leggyakrabban lesz [System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord). A Stop-Proc parancsmag felülbírálja a [System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) bemeneti metódusához feldolgozásra. Ez a megvalósítás a Stop-Proc parancsmag a hívások végrehajtott írási részletes üzeneteket, a hibakeresési üzeneteket és a figyelmeztető üzeneteket.

> [!NOTE]
> További információ a hogyan Ez a metódus meghívja a [System.Management.Automation.Cmdlet.ShouldProcess](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) és [System.Management.Automation.Cmdlet.ShouldContinue](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) módszereket, tekintse meg a [Létrehozása egy parancsmag, amely módosítja a rendszer](./creating-a-cmdlet-that-modifies-the-system.md).

## <a name="writing-a-verbose-message"></a>Részletes üzenet írásának

A [System.Management.Automation.Cmdlet.WriteVerbose](/dotnet/api/System.Management.Automation.Cmdlet.WriteVerbose) általános, nem kapcsolódó meghatározott hibafeltételek felhasználói szintű információkat írásához használt módszert. A rendszergazda folytatja a más parancsok feldolgozási felhasználhatja ezt az információt. Emellett ez a módszer használatával írt minden olyan információt kell kell honosított igény szerint.

A Stop-Proc parancsmag a következő kód bemutatja, két hívásainak a [System.Management.Automation.Cmdlet.WriteVerbose](/dotnet/api/System.Management.Automation.Cmdlet.WriteVerbose) metódus felülbírálását, a [System.Management.Automation.Cmdlet.ProcessRecord ](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) metódust.

```csharp
message = String.Format("Attempting to stop process \"{0}\".", name);
WriteVerbose(message);
```

```csharp
message = String.Format("Stopped process \"{0}\", pid {1}.",
                        processName, process.Id);

WriteVerbose(message);
```

## <a name="writing-a-debug-message"></a>Hibakeresési üzenet írásának

A [System.Management.Automation.Cmdlet.WriteDebug](/dotnet/api/System.Management.Automation.Cmdlet.WriteDebug) módszert a parancsmag működésének hibaelhárítására használható hibakeresési üzeneteket írni. A hívás érkezett egy bemeneti metódus feldolgozása.

> [!NOTE]
> Windows PowerShell is meghatároz egy `Debug` paraméter, amely egyaránt részletes mutat be, és a hibakeresési információkat. A parancsmag támogatja ezt a paramétert, ha nem kell meghívni [System.Management.Automation.Cmdlet.WriteDebug](/dotnet/api/System.Management.Automation.Cmdlet.WriteDebug) ugyanazt a kódot, amely meghívja a [System.Management.Automation.Cmdlet.WriteVerbose](/dotnet/api/System.Management.Automation.Cmdlet.WriteVerbose) .

A kód a minta Stop-Proc parancsmag a következő két szakasz hívásainak megjelenítéséhez a [System.Management.Automation.Cmdlet.WriteDebug](/dotnet/api/System.Management.Automation.Cmdlet.WriteDebug) metódus felülbírálását, a [ System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) metódust.

Hibakeresési üzenet írása előtt közvetlenül [System.Management.Automation.Cmdlet.ShouldProcess](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) nevezzük.

```csharp
message =
          String.Format("Acquired name for pid {0} : \"{1}\"",
                       process.Id, processName);
WriteDebug(message);
```

Hibakeresési üzenet írása előtt közvetlenül [System.Management.Automation.Cmdlet.WriteObject](/dotnet/api/System.Management.Automation.Cmdlet.WriteObject) nevezzük.

```csharp
message =
         String.Format("Writing process \"{0}\" to pipeline",
         processName);
WriteDebug(message);
WriteObject(process);
```

Windows PowerShell automatikusan átirányítja a bármely [System.Management.Automation.Cmdlet.WriteDebug](/dotnet/api/System.Management.Automation.Cmdlet.WriteDebug) hívásokat a nyomkövetés infrastruktúrát és a parancsmagok. Ez lehetővé teszi a metódust hívja, nem kell tennie minden olyan további fejlesztési munkálatok során, a parancsmag belül az üzemeltetési alkalmazás, egy fájl vagy egy hibakereső nyomon követését. A következő parancssori bejegyzés egy nyomkövetési művelet valósítja meg.

**PS > nyomkövetési-kifejezés stop-proc-fájl proc.log-paranccsal állítsa le a folyamaton Jegyzettömb**

## <a name="writing-a-warning-message"></a>Egy figyelmeztető üzenet írása

A [System.Management.Automation.Cmdlet.WriteWarning](/dotnet/api/System.Management.Automation.Cmdlet.WriteWarning) metódus írási egy figyelmeztetés, amikor a parancsmag arra készül, hogy előfordulhat, hogy nem várt eredményt, ha például egy csak olvasható fájlok felülírása művelet végrehajtására szolgál.

A következő kód a minta Stop-Proc parancsmag megjeleníti a hívást a [System.Management.Automation.Cmdlet.WriteWarning](/dotnet/api/System.Management.Automation.Cmdlet.WriteWarning) metódus felülbírálását, a [ System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) metódust.

```csharp
 if (criticalProcess)
 {
   message =
             String.Format("Stopping the critical process \"{0}\".",
                           processName);
   WriteWarning(message);
} // if (criticalProcess...
```

## <a name="writing-a-progress-message"></a>A folyamatállapot-üzenet írása

A [System.Management.Automation.Cmdlet.WriteProgress](/dotnet/api/System.Management.Automation.Cmdlet.WriteProgress) folyamatüzeneteket írhat, amikor a parancsmag operations igénybe egy kiterjesztett sok időt vesz igénybe. Hívás [System.Management.Automation.Cmdlet.WriteProgress](/dotnet/api/System.Management.Automation.Cmdlet.WriteProgress) átadja egy [System.Management.Automation.Progressrecord](/dotnet/api/System.Management.Automation.ProgressRecord) objektum, amely a renderelést a felhasználó számára a tároló alkalmazás érkezik.

> [!NOTE]
> A Stop-Proc parancsmag nem tartalmazza a hívást a [System.Management.Automation.Cmdlet.WriteProgress](/dotnet/api/System.Management.Automation.Cmdlet.WriteProgress) metódust.

A következő kódot a folyamatállapot-üzenet, amely megpróbálja elem másolása a parancsmag által írt példája.

```csharp
int myId = 0;
string myActivity = "Copy-item: Copying *.* to c:\abc";
string myStatus = "Copying file bar.txt";
ProgressRecord pr = new ProgressRecord(myId, myActivity, myStatus);
WriteProgress(pr);

pr.RecordType = ProgressRecordType.Completed;
WriteProgress(pr);
```

## <a name="code-sample"></a>Kódminta

A teljes C# mintakód, lásd: [StopProcessSample02 minta](./stopprocesssample02-sample.md).

## <a name="define-object-types-and-formatting"></a>Objektumtípusok és formázása

Windows PowerShell parancsmagok használatával a .NET-objektumokká közötti továbbítja. Ennek következtében a parancsmag előfordulhat, hogy meg kell határoznia a saját típusát, vagy a parancsmag előfordulhat, hogy ki kell terjesztenie egy másik parancsmag által biztosított meglévő típus. Új típusok meghatározása, vagy meglévő típusok bővítésével kapcsolatos további információkért lásd: [objektumtípusok kiterjesztése és formázás](http://msdn.microsoft.com/en-us/da976d91-a3d6-44e8-affa-466b1e2bd351).

## <a name="building-the-cmdlet"></a>A parancsmag készítése

Parancsmag-k megvalósítása után regisztrálni kell a Windows PowerShell-lel a Windows PowerShell beépülő modullal. Parancsmagok regisztrálásával kapcsolatos további információkért lásd: [parancsmagjainak regisztrálásához, a szolgáltatók és az alkalmazások üzemeltetése hogyan](http://msdn.microsoft.com/en-us/a41e9054-29c8-40ab-bf2b-8ce4e7ec1c8c).

## <a name="testing-the-cmdlet"></a>A parancsmag tesztelése

Ha a parancsmagot a Windows PowerShell-lel regisztrálva lett, azt a parancssorból való futtatásával tesztelheti. Most tesztelje a parancsmagra állítsa le a folyamaton. A parancssorból-parancsmagokkal kapcsolatos további információkért lásd: a [első lépések a Windows PowerShell-lel](/powershell/scripting/getting-started/getting-started-with-windows-powershell).

- A következő parancssori bejegyzés állítsa le a folyamaton használatával állítsa le a "JEGYZETTÖMB" nevű folyamatot, adja meg a részletes értesítések és a nyomtatási ladicí informace.

    ```powershell
    PS> stop-proc -Name notepad -Verbose -Debug
    ```

A következő eredmény jelenik meg.

    ```
    VERBOSE: Attempting to stop process " notepad ".
    DEBUG: Acquired name for pid 5584 : "notepad"

    Confirm
    Continue with this operation?
    [Y] Yes  [A] Yes to All  [H] Halt Command  [S] Suspend  [?] Help (default is "Y"): Y

    Confirm
    Are you sure you want to perform this action?
    Performing operation "stop-proc" on Target "notepad (5584)".
    [Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "Y"): Y
    VERBOSE: Stopped process "notepad", pid 5584.
    ```

## <a name="see-also"></a>Lásd még:

[Hozzon létre egy parancsmag, amely módosítja a rendszer](./creating-a-cmdlet-that-modifies-the-system.md)

[Hogyan hozhat létre egy Windows PowerShell-parancsmag](http://msdn.microsoft.com/en-us/0d721742-c849-4d0d-964f-78ddd9cd258c)

[Objektumtípusok kiterjesztése és formázása](http://msdn.microsoft.com/en-us/da976d91-a3d6-44e8-affa-466b1e2bd351)

[How to Register parancsmagok, a szolgáltatók és az alkalmazások üzemeltetéséhez](http://msdn.microsoft.com/en-us/a41e9054-29c8-40ab-bf2b-8ce4e7ec1c8c)

[Windows PowerShell SDK](../windows-powershell-reference.md)
