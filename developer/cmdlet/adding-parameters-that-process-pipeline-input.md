---
title: Adatcsatorna bemenetének feldolgozott-paramétereket adunk hozzá |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- cmdlets [PowerShell Programmer's Guide], pipeline input
- parameters [PowerShell Programmer's Guide], pipeline input
ms.assetid: 09bf70a9-7c76-4ffe-b3f0-a1d5f10a0931
caps.latest.revision: 8
ms.openlocfilehash: bd52dc8aee7975d0899083a5c2f595b17690dc33
ms.sourcegitcommit: caac7d098a448232304c9d6728e7340ec7517a71
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/16/2019
ms.locfileid: "58054756"
---
# <a name="adding-parameters-that-process-pipeline-input"></a>Láncbemenetet feldolgozó paraméterek hozzáadása

A parancsmag bemenete egy forrása az objektumot, a folyamat, amely egy felsőbb rétegbeli parancsmag származik. Ez a szakasz ismerteti, hogyan lehet egy paraméter hozzáadása a Get-Proc parancsmag (ismertetett [létrehozásához az első parancsmag](./creating-a-cmdlet-without-parameters.md)), hogy a parancsmag folyamat objektumot tud feldolgozni.

A Get-Proc parancsmagot használja egy `Name` paraméter, amely egy folyamat objektumot a bemenetet elfogadja folyamat adatait kérdezi le a helyi számítógép megadott neve alapján, és ezután megjeleníti a folyamatok adatait a parancssorban.

Ez a szakasz témakörei a következők:

- [A parancsmag osztály meghatározása](#Defining-the-Cmdlet-Class)

- [A bemenetet a folyamat meghatározása](#Defining-Input-from-the-Pipeline)

- [Egy bemeneti metódus feldolgozási felülbírálása](#Overriding-an-Input-Processing-Method)

- [Kódminta](#Code-Sample)

- [Objektumtípusok definiálása és formázása](#Defining-Object-Types-and-Formatting)

- [A parancsmag készítése](#Building-the-Cmdlet)

- [A parancsmag tesztelése](#Testing-the-Cmdlet)

## <a name="defining-the-cmdlet-class"></a>A parancsmag osztály meghatározása

Mindig a parancsmag elnevezési és a .NET-osztály, amely megvalósítja a parancsmag deklaráló parancsmag létrehozásának első lépése. Ez a parancsmag folyamat adatait, kérdezi le, így az itt választott művelet neve "Get". (A szinte bármilyen rendezési parancsmag, amely képes adatok beolvasása a parancssori bemenet tud feldolgozni.) A parancsmag jóváhagyott igék kapcsolatos további információkért lásd: [művelet neve](./approved-verbs-for-windows-powershell-commands.md).

A Get-Proc parancsmag definícióját a következő: Ez a definíció részleteit [létrehozásához az első parancsmag](./creating-a-cmdlet-without-parameters.md).

```csharp
[Cmdlet(VerbsCommon.Get, "proc")]
public class GetProcCommand : Cmdlet
```

```vb
<Cmdlet(VerbsCommon.Get, "Proc")> _
Public Class GetProcCommand
    Inherits Cmdlet
```

## <a name="defining-input-from-the-pipeline"></a>A bemenetet a folyamat meghatározása

Ez a szakasz ismerteti, hogyan adhat meg a folyamat a parancsmag a bemenetet. A Get-Proc parancsmag képviselő tulajdonság határozza meg a `Name` paraméter leírtak szerint [a folyamat parancssori bemenet-paramétereket adunk hozzá](./adding-parameters-that-process-command-line-input.md). (Lásd a paraméterek deklaráló kapcsolatos általános információkat szakasza.)

Azonban parancsmag kell feldolgoznia az adatcsatorna bemenetének, amikor kell legyen kötve a Windows PowerShell-modul által bemeneti értékek paramétereit. Ehhez hozzá kell adnia a `ValueFromPipeline` kulcsszó, vagy adja hozzá a `ValueFromPipelineByProperty` kulcsszó használatával a [System.Management.Automation.Parameterattribute](/dotnet/api/System.Management.Automation.ParameterAttribute) deklarace attribútum. Adja meg a `ValueFromPipeline` kulcsszót, ha a parancsmag fér hozzá a teljes bemeneti objektum. Adja meg a `ValueFromPipelineByProperty` Ha a parancsmag csak az objektum osztályát fér hozzá.

Íme a paraméterdeklarációhoz a a `Name` a Get-Proc parancsmag, amely elfogadja a folyamat bemeneti paraméter.

[!code-csharp[GetProcessSample03.cs](../../powershell-sdk-samples/SDK-2.0/csharp/GetProcessSample03/GetProcessSample03.cs#L35-L44 "GetProcessSample03.cs")]

```vb
<Parameter(Position:=0, ValueFromPipeline:=True, _
ValueFromPipelineByPropertyName:=True), ValidateNotNullOrEmpty()> _
Public Property Name() As String()
    Get
        Return processNames
    End Get

    Set(ByVal value As String())
        processNames = value
    End Set

End Property
```

<!-- TODO!!!: review snippet reference  [!CODE [Msh_samplesgetproc03#GetProc03VBNameParameter](Msh_samplesgetproc03#GetProc03VBNameParameter)]  -->

Az előző deklarace készleteket a `ValueFromPipeline` kulcsszó használatával `true` úgy, hogy a Windows PowerShell-modul fog kötődni a paraméter a bejövő objektum, ha az objektum ugyanolyan típusú, mint a paramétert, vagy ha az azonos típusú is kényszeríthető. A `ValueFromPipelineByPropertyName` kulcsszó is értékre van állítva `true` úgy, hogy a Windows PowerShell-modul ellenőrzi a bejövő objektumot egy `Name` tulajdonság. A bejövő objektumnak a tulajdonságot, ha a futtatókörnyezet köti a `Name` paramétert a `Name` bejövő objektum tulajdonságának.

> [!NOTE]
> A beállítást, a `ValueFromPipeline` kulcsszó attribútum esetében egy paraméter elsőbbséget élvez a beállítása a `ValueFromPipelineByPropertyName` kulcsszót.

## <a name="overriding-an-input-processing-method"></a>Egy bemeneti metódus feldolgozási felülbírálása

Ha a parancsmagot, a folyamat bemeneti kezelni, kell a megfelelő bemenet feldolgozása metódusok felülbírálása. Az alapszintű bemeneti feldolgozási módszerek jelennek meg a [létrehozásához az első parancsmag](./creating-a-cmdlet-without-parameters.md).

A Get-Proc parancsmag felülbírálja a [System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) metódust a `Name` paraméter megadott információ a felhasználó vagy egy parancsfájlt. Ez a módszer a folyamatok minden kért Folyamatnév vagy az összes folyamat fog kapni, ha nincs név megadva. Figyelje meg, hogy belül [System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord), a hívást [System.Management.Automation.Cmdlet.WriteObject%28System.Object%2CSystem.Boolean%29](/dotnet/api/System.Management.Automation.Cmdlet.WriteObject%28System.Object%2CSystem.Boolean%29) a kimenete a folyamat küld kimeneti mechanizmus objektumokat. A második paraméter a hívás `enumerateCollection`, értékre van állítva `true` állapítható meg, hogy a Windows PowerShell modul enumerálása folyamat objektumok tömbje, és a egy folyamat egyszerre írni a parancssorból.

```csharp
protected override void ProcessRecord()
{
  // If no process names are passed to the cmdlet, get all processes.
  if (processNames == null)
  {
      // Write the processes to the pipeline making them available
      // to the next cmdlet. The second argument of this call tells
      // PowerShell to enumerate the array, and send one process at a
      // time to the pipeline.
      WriteObject(Process.GetProcesses(), true);
  }
  else
  {
    // If process names are passed to the cmdlet, get and write
    // the associated processes.
    foreach (string name in processNames)
    {
      WriteObject(Process.GetProcessesByName(name), true);
    } // End foreach (string name...).
  }
}
```

```vb
Protected Overrides Sub ProcessRecord()
    Dim processes As Process()

    '/ If no process names are passed to the cmdlet, get all processes.
    If processNames Is Nothing Then
        processes = Process.GetProcesses()
    Else

        '/ If process names are specified, write the processes to the
        '/ pipeline to display them or make them available to the next cmdlet.
        For Each name As String In processNames
            '/ The second parameter of this call tells PowerShell to enumerate the
            '/ array, and send one process at a time to the pipeline.
            WriteObject(Process.GetProcessesByName(name), True)
        Next
    End If

End Sub 'ProcessRecord
```

## <a name="code-sample"></a>Kódminta

A teljes C# mintakód, lásd: [GetProcessSample03 minta](./getprocesssample03-sample.md).

## <a name="defining-object-types-and-formatting"></a>Objektumtípusok definiálása és formázása

Windows PowerShell parancsmagok használatával a .net-objektumokká közötti továbbítja. Ennek következtében a parancsmag előfordulhat, hogy meg kell határoznia a saját típusát, vagy a parancsmag előfordulhat, hogy ki kell terjesztenie egy másik parancsmag által biztosított meglévő típus. Új típusok meghatározása, vagy meglévő típusok bővítésével kapcsolatos további információkért lásd: [objektumtípusok kiterjesztése és formázás](http://msdn.microsoft.com/en-us/da976d91-a3d6-44e8-affa-466b1e2bd351).

## <a name="building-the-cmdlet"></a>A parancsmag készítése

A parancsmag megvalósítása után regisztrálni kell a Windows PowerShell-lel a Windows PowerShell beépülő modullal. Parancsmagok regisztrálásával kapcsolatos további információkért lásd: [parancsmagjainak regisztrálásához, a szolgáltatók és az alkalmazások üzemeltetése hogyan](http://msdn.microsoft.com/en-us/a41e9054-29c8-40ab-bf2b-8ce4e7ec1c8c).

## <a name="testing-the-cmdlet"></a>A parancsmag tesztelése

Ha a parancsmagot a Windows PowerShell-lel regisztrálva lett, tesztelje azt a parancssorból való futtatásával. Például tesztelheti a kódját a minta parancsmagot. A parancssorból-parancsmagokkal kapcsolatos további információkért lásd: a [első lépések a Windows PowerShell-lel](/powershell/scripting/getting-started/getting-started-with-windows-powershell).

- A Windows PowerShell parancssorába a következő parancsokat a folyamat nevét a folyamat keretében lekéréséhez.

    ```powershell
    PS> type ProcessNames | get-proc
    ```

A következő eredmény jelenik meg.

    ```
    Handles  NPM(K)  PM(K)   WS(K)  VS(M)  CPU(s)    Id  ProcessName
    -------  ------  -----   ----- -----   ------    --  -----------
        809      21  40856    4448    147    9.50  2288  iexplore
        737      21  26036   16348    144   22.03  3860  iexplore
         39       2   1024     388     30    0.08  3396  notepad
       3927      62  71836   26984    467  195.19  1848  OUTLOOK
    ```

- Adja meg a következő sorokat a folyamat az objektumokat, amelyek rendelkeznek egy `Name` a folyamatok "IEXPLORE" nevű tulajdonságot. Ez a példa a `Get-Process` parancsmag (a Windows PowerShell által biztosított), egy fölérendelt parancs használatával kérje le a "IEXPLORE" folyamatokat.

    ```powershell
    PS> get-process iexplore | get-proc
    ```

A következő eredmény jelenik meg.

    ```
    Handles  NPM(K)  PM(K)   WS(K)  VS(M)  CPU(s)    Id  ProcessName
    -------  ------  -----      ----- -----   ------     -- -----------
        801      21  40720    6544    142    9.52  2288  iexplore
        726      21  25872   16652    138   22.09  3860  iexplore
        801      21  40720    6544    142    9.52  2288  iexplore
        726      21  25872   16652    138   22.09  3860  iexplore
    ```

## <a name="see-also"></a>Lásd még:

[Parancssori bemenet feldolgozása paraméterek hozzáadása](./adding-parameters-that-process-command-line-input.md)

[Az első parancsmag létrehozása](./creating-a-cmdlet-without-parameters.md)

[Objektumtípusok kiterjesztése és formázása](http://msdn.microsoft.com/en-us/da976d91-a3d6-44e8-affa-466b1e2bd351)

[How to Register parancsmagok, a szolgáltatók és az alkalmazások üzemeltetéséhez](http://msdn.microsoft.com/en-us/a41e9054-29c8-40ab-bf2b-8ce4e7ec1c8c)

[Windows PowerShell-referencia](../windows-powershell-reference.md)

[Parancsmag-minták](./cmdlet-samples.md)
