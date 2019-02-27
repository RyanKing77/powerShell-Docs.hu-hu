---
title: Paraméterek nélkül a parancsmag létrehozása |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- cmdlets [PowerShell Programmers Guide], creating
- cmdlets [PowerShell Programmers Guide], basic cmdlet
ms.assetid: 54236ef3-82db-45f8-9114-1ecb7ff65d3e
caps.latest.revision: 8
ms.openlocfilehash: 75a45e539b45b50714951f2b992d9ecf69de4664
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56850063"
---
# <a name="creating-a-cmdlet-without-parameters"></a>Paraméterek nélküli parancsmag létrehozása

Ez a szakasz ismerteti, hogyan hozhat létre olyan parancsmagot, amely adatait kérdezi le a helyi számítógépen, a paraméterek nélkül, és a folyamat ezután beírja az információkat. A parancsmag az itt leírtak szerint egy Get-Proc parancsmag, amely a folyamatok a helyi számítógép adatait kérdezi le, majd megjeleníti ezt az információt a parancssorból.

Ez a szakasz témakörei a következők:

- [A parancsmag elnevezése](#Naming-the-Cmdlet)

- [A parancsmag osztály meghatározása](#Defining-the-Cmdlet-Class)

- [Egy bemeneti metódus feldolgozási felülbírálása](#Overriding-an-Input-Processing-Method)

- [Kódminta](#Code-Sample)

- [Objektumtípusok definiálása és formázása](#Defining-Object-Types-and-Formatting)

- [A parancsmag készítése](#Building-the-Cmdlet)

- [A parancsmag tesztelése](#Testing-the-Cmdlet)

> [!NOTE]
> Vegye figyelembe, hogy parancsmagok írásakor, a Windows PowerShell® referenciaszerelvények letöltődnek lemezre (alapértelmezés szerint a C:\Program Files\Reference Assemblies\Microsoft\WindowsPowerShell\v1.0). A globális szerelvény gyorsítótárban (GAC) a telepítés nem.

## <a name="naming-the-cmdlet"></a>A parancsmag elnevezése

Egy parancsmag neve, amely jelzi, hogy a művelet a parancsmag lép igeként és főnév, amely azt jelzi, hogy az elemek, amelyek a parancsmagot a közvetítőtől áll. A Get-Proc parancsmagra folyamat objektumok kér le, mert használja a művelet "Get", határozzák meg a [System.Management.Automation.Verbscommon](/dotnet/api/System.Management.Automation.VerbsCommon) enumerálása, és a főnév jelzi, hogy működik-e a parancsmag folyamat elemeken a "Proc".

Parancsmagok elnevezésekor ne használja a következő karaktereket: #, () {} [] & - / \ $;: "" <> &#124; ? @ ` .

### <a name="choosing-a-noun"></a>Főnév kiválasztása

Egy adott főnév kell kiválasztani. A legcélszerűbb jedné főnév előtaggal van ellátva a termék neve akkor használhatja rövidített verzióját használja. Egy ilyen példa parancsmag neve "`Get-SQLServer`".

### <a name="choosing-a-verb"></a>Egy művelet kiválasztása

Jóváhagyott parancsmag művelet nevek a készletből egy műveletet kell használnia. A parancsmag jóváhagyott igék kapcsolatos további információkért lásd: [művelet neve](./approved-verbs-for-windows-powershell-commands.md).

## <a name="defining-the-cmdlet-class"></a>A parancsmag osztály meghatározása

Miután kiválasztotta a parancsmag neve, adja meg a parancsmag végrehajtása érdekében egy .NET-osztály. A Get-Proc parancsmagra osztály definícióját a következő:

```csharp
[Cmdlet(VerbsCommon.Get, "Proc")]
  public class GetProcCommand : Cmdlet
```

```vb
<Cmdlet(VerbsCommon.Get, "Proc")> _
Public Class GetProcCommand
    Inherits Cmdlet
```

Figyelje meg, hogy az osztály definícióját vissza a [System.Management.Automation.Cmdletattribute](/dotnet/api/System.Management.Automation.CmdletAttribute) attribútum szintaxissal `[Cmdlet(verb, noun, ...)]`, a parancsmag, ez az osztály azonosítására szolgál. Ez az egyetlen szükséges összes parancsmagjához, és lehetővé teszi a Windows PowerShell futtatási helyesen hívja meg őket. Attribútum az osztály tovább deklarálja, szükség esetén kulcsszavakkal állíthatja be. Vegye figyelembe, hogy a minta GetProcCommand osztály típusattribútum-deklaráció deklarálja csak főnevet és a művelet nevét a Get-Proc parancsmaghoz.

> [!NOTE]
> Minden Windows PowerShell attribútum osztály, amely lehet a kulcsszavak felelnek meg az attribútum az osztály tulajdonságait.

Az osztály a parancsmag elnevezésekor tanácsos tükrözik az osztály nevét a parancsmag neve. Ehhez használja az űrlap "VerbNounCommand" és "Művelet" és "Főnév" cserélje a ige és főnév, a parancsmag neve szerepel. Amint azt az előző osztálykiterjesztések definíciója, a Get-Proc parancsmagra meghatározása GetProcCommand, amely származó nevű osztály a [System.Management.Automation.Cmdlet](/dotnet/api/System.Management.Automation.Cmdlet) alaposztály.

> [!IMPORTANT]
> Ha szeretne meghatározni egy parancsmag, amely a Windows PowerShell-modul közvetlenül hozzáfér, a .NET-osztály típusból kell származtatni a [System.Management.Automation.Pscmdlet](/dotnet/api/System.Management.Automation.PSCmdlet) alaposztály. Ez az osztály kapcsolatos további információkért lásd: [létrehozása parancsmag adott meghatározása paraméterkészlettel](./adding-parameter-sets-to-a-cmdlet.md).

> [!NOTE]
> Az osztály a parancsmag fel kell tüntetni explicit módon is nyilvános. Nem jelölt nyilvános osztályok belső alapértelmezés szerint, és nem található a Windows PowerShell-modul által.

Használja a Windows PowerShell a [Microsoft.Powershell.Commands](/dotnet/api/Microsoft.PowerShell.Commands) parancsmag osztályt névterét. Javasoljuk, hogy a parancsmag osztályok helyezze az API-t névtér, például xxx.PS.Commands parancsok névtérben.

## <a name="overriding-an-input-processing-method"></a>Egy bemeneti metódus feldolgozási felülbírálása

A [System.Management.Automation.Cmdlet](/dotnet/api/System.Management.Automation.Cmdlet) osztály, amely legalább egy a parancsmag felül kell írnia, három bemeneti feldolgozás fő metódusokat biztosít. Hogyan dolgozza fel a Windows PowerShell a rekordok kapcsolatos további információkért lásd: [Windows PowerShell működése](https://msdn.microsoft.com/en-us/ced30e23-10af-4700-8933-49873bd84d58).

Bemeneti minden típusú, a Windows PowerShell-modult meghívja [System.Management.Automation.Cmdlet.Beginprocessing*](/dotnet/api/System.Management.Automation.Cmdlet.BeginProcessing) feldolgozási engedélyezéséhez. A parancsmag néhány előfeldolgozása vagy a telepítő kell végrehajtania, ha azt teheti ezt a módszert felülbírálja.

> [!NOTE]
> Windows PowerShell "rekord" kifejezés használatával ismertetik az megadásakor a parancsmag neve paraméterértékeket.

Ha a parancsmag elfogadja az adatcsatorna bemenetének, hogy felül kell írnia a [System.Management.Automation.Cmdlet.Processrecord*](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) metódust, és szükség esetén a [System.Management.Automation.Cmdlet.Endprocessing*](/dotnet/api/System.Management.Automation.Cmdlet.EndProcessing)metódust. Például a parancsmag felülírhatják a két módszert ha összes bemeneti használatával gyűjt [System.Management.Automation.Cmdlet.Processrecord*](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) , és ezután a bemenet egy elemet, hanem a teljes egyszerre, mint a `Sort-Object` a parancsmag hajtja végre.

Ha a parancsmag nem hozza a folyamat bemeneti, hogy felül kell írni a [System.Management.Automation.Cmdlet.Endprocessing*](/dotnet/api/System.Management.Automation.Cmdlet.EndProcessing) metódust. Vegye figyelembe, hogy ezt a módszert gyakran használt helyén [System.Management.Automation.Cmdlet.Beginprocessing*](/dotnet/api/System.Management.Automation.Cmdlet.BeginProcessing) amikor a parancsmag nem működik egy elem egyszerre, mint a rendezési parancsmag.

A Get-Proc parancsmagra adatcsatorna bemenetének kell kapnia, mert ez a beállítás felülbírálja a [System.Management.Automation.Cmdlet.Processrecord*](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) metódust, és használja az alapértelmezett megvalósítása esetében [ System.Management.Automation.Cmdlet.Beginprocessing*](/dotnet/api/System.Management.Automation.Cmdlet.BeginProcessing) és [System.Management.Automation.Cmdlet.Endprocessing*](/dotnet/api/System.Management.Automation.Cmdlet.EndProcessing). A [System.Management.Automation.Cmdlet.Processrecord*](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) felülbírálás kérdezi le a folyamatokat, és írja őket a parancssor használatával a [System.Management.Automation.Cmdlet.Writeobject*](/dotnet/api/System.Management.Automation.Cmdlet.WriteObject) a metódus.

```csharp
protected override void ProcessRecord()
{
  // Get the current processes
  Process[] processes = Process.GetProcesses();

  // Write the processes to the pipeline making them available
  // to the next cmdlet. The second parameter of this call tells
  // PowerShell to enumerate the array, and send one process at a
  // time to the pipeline.
  WriteObject(processes, true);
}
```

```vb
Protected Overrides Sub ProcessRecord()

    '/ Get the current processes.
    Dim processes As Process()
    processes = Process.GetProcesses()

    '/ Write the processes to the pipeline making them available
    '/ to the next cmdlet. The second parameter of this call tells
    '/ PowerShell to enumerate the array, and send one process at a
    '/ time to the pipeline.
    WriteObject(processes, True)

End Sub 'ProcessRecord
```

#### <a name="things-to-remember-about-input-processing"></a>Megjegyzendő tudnivalók kapcsolatos bemeneti feldolgozása

- A bemeneti alapértelmezett forrása a parancssorban a felhasználó által megadott explicit objektum (például egy karakterlánc). További információkért lásd: [létrehozásának folyamata parancssori bemeneti parancsmag](./adding-parameters-that-process-command-line-input.md).

- Egy bemeneti metódus feldolgozási is fogadhatnak bemenet a folyamathoz egy felsőbb rétegbeli parancsmag kimeneti objektumot. További információkért lásd: [létrehozásának folyamata folyamat bemeneti parancsmag](./adding-parameters-that-process-pipeline-input.md). Vegye figyelembe, hogy a parancsmag bemeneti fogadjon parancssori kombinációját, és folyamat adatforrásokat.

- Az alsóbb rétegbeli parancsmag előfordulhat, hogy nem ad vissza, hosszú ideje, vagy egyáltalán nem. Éppen ezért a feldolgozási mód a parancsmag a bemeneti kell tartalmaz a zárolások hívások során [System.Management.Automation.Cmdlet.Writeobject*](/dotnet/api/System.Management.Automation.Cmdlet.WriteObject), különösen a zárolásokat, amelyhez a hatókör túlnyúlik a parancsmag-példány.

> [!IMPORTANT]
> Parancsmagok soha nem kell hívnia [System.Console.Writeline*](/dotnet/api/System.Console.WriteLine) vagy azzal egyenértékű.

- Előfordulhat, hogy a parancsmag objektum változók végeztével karbantartása feldolgozása (például akkor, ha a fájlleíró megnyílik a [System.Management.Automation.Cmdlet.Beginprocessing*](/dotnet/api/System.Management.Automation.Cmdlet.BeginProcessing) metódust, és korlátlan ideig megőrzi a leíró használatra megnyitásához[ System.Management.Automation.Cmdlet.Processrecord*](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord)). Fontos megjegyezni, hogy a Windows PowerShell-modul nem mindig hívja a [System.Management.Automation.Cmdlet.Endprocessing*](/dotnet/api/System.Management.Automation.Cmdlet.EndProcessing) metódussal, amely végre kell hajtania objektum karbantartása.

Ha például [System.Management.Automation.Cmdlet.Endprocessing*](/dotnet/api/System.Management.Automation.Cmdlet.EndProcessing) előfordulhat, hogy nem hívható meg, ha a parancsmag midway megszakadt, vagy ha egy megszakítást okozó hiba jelenik meg a parancsmag bármely részén. Ezért egy objektum karbantartási igénylő parancsmag meg kell valósítania a teljes [System.Idisposable](/dotnet/api/System.IDisposable) minta, beleértve a befejezővel úgy, hogy a futtatókörnyezet is meghívhat [ System.Management.Automation.Cmdlet.Endprocessing*](/dotnet/api/System.Management.Automation.Cmdlet.EndProcessing) és [System.Idisposable.Dispose*](/dotnet/api/System.IDisposable.Dispose) feldolgozás végén.

## <a name="code-sample"></a>Kódminta

A teljes C# mintakód, lásd: [GetProcessSample01 minta](./getprocesssample01-sample.md).

## <a name="defining-object-types-and-formatting"></a>Objektumtípusok definiálása és formázása

Windows PowerShell parancsmagok használatával a .NET-objektumokká közötti továbbítja. Ennek következtében a parancsmag előfordulhat, hogy meg kell határoznia a saját típusát, vagy a parancsmag előfordulhat, hogy ki kell terjesztenie egy másik parancsmag által biztosított meglévő típus. Új típusok meghatározása, vagy meglévő típusok bővítésével kapcsolatos további információkért lásd: [objektumtípusok kiterjesztése és formázás](https://msdn.microsoft.com/en-us/da976d91-a3d6-44e8-affa-466b1e2bd351).

## <a name="building-the-cmdlet"></a>A parancsmag készítése

Parancsmag-k megvalósítása után regisztrálnia kell azt a Windows PowerShell-lel a Windows PowerShell beépülő modullal. Parancsmagok regisztrálásával kapcsolatos további információkért lásd: [parancsmagjainak regisztrálásához, a szolgáltatók és az alkalmazások üzemeltetése hogyan](https://msdn.microsoft.com/en-us/a41e9054-29c8-40ab-bf2b-8ce4e7ec1c8c).

## <a name="testing-the-cmdlet"></a>A parancsmag tesztelése

Ha a parancsmagot a Windows PowerShell-lel regisztrálva lett, azt a parancssorból való futtatásával tesztelheti. A kód a minta-Get-Proc parancsmag kis, de továbbra is használja a Windows PowerShell-modul és a egy meglévő .NET objektum, amely elegendő az, hogy hasznos. Most tesztelheti, hogy jobban megismerheti, mi mindent az Get-Proc, és hogyan használhatók a kimenetét. A parancssorból-parancsmagokkal kapcsolatos további információkért lásd: a [első lépések a Windows PowerShell-lel](/powershell/scripting/getting-started/getting-started-with-windows-powershell).

1. Indítsa el a Windows Powershellt, és az aktuális, a számítógépen futó folyamatok beolvasása.

    ```powershell
    get-proc
    ```

    A következő eredmény jelenik meg.

    ```output
    Handles  NPM(K)  PM(K)  WS(K)  VS(M)  CPU(s)  Id   ProcessName
    -------  ------  -----  -----  -----  ------  --   ----------
    254      7       7664   12048  66     173.75  1200  QCTRAY
    32       2       1372   2628   31       0.04  1860  DLG
    271      6       1216   3688   33       0.03  3816  lg
    27       2       560    1920   24       0.01  1768  TpScrex
    ...
    ```

2. Rendelje hozzá egy változót a parancsmag eredményei egyszerűbb kezelését.

    ```powershell
    $p=get-proc
    ```

3. A folyamatok számát beolvasása.

    ```powershell
    $p.length
    ```

    A következő eredmény jelenik meg.

    ```output
    63
    ```

4. Egy adott folyamat lekéréséhez.

    ```powershell
    $p[6]
    ```

    A következő eredmény jelenik meg.

    ```output
    Handles  NPM(K)  PM(K)  WS(K)  VS(M)  CPU(s)  Id    ProcessName
    -------  ------  -----  -----  -----  ------  --    -----------
    1033     3       2400   3336   35     0.53    1588  rundll32
    ```

5. Ez a folyamat kezdési idejét beolvasása.

    ```powershell
    $p[6].starttime
    ```

    A következő eredmény jelenik meg.

    ```output
    Tuesday, July 26, 2005 9:34:15 AM
    ```

    ```powershell
    $p[6].starttime.dayofyear
    ```

    ```output
    207
    ```

6. A folyamatok, amelynek az ablakleírók száma nagyobb, mint 500 beolvasása, és rendezze az eredmény.

    ```powershell
    $p | Where-Object {$_.HandleCount -gt 500 } | Sort-Object HandleCount
    ```

    A következő eredmény jelenik meg.

    ```output
    Handles  NPM(K)  PM(K)  WS(K)  VS(M)  CPU(s)  Id   ProcessName
    -------  ------  -----  -----  -----  ------  --   ----------
    568      14      2164   4972   39     5.55    824  svchost
    716       7      2080   5332   28    25.38    468  csrss
    761      21      33060  56608  440  393.56    3300 WINWORD
    791      71      7412   4540   59     3.31    492  winlogon
    ...
    ```

7. Használja a `Get-Member` parancsmagot, hogy minden egyes folyamat esetében elérhető tulajdonságok listája.

    ```powershell
    $p | Get-Member -MemberType property
    ```

    ```output
        TypeName: System.Diagnostics.Process
    ```

    A következő eredmény jelenik meg.

    ```output
    Name                     MemberType Definition
    ----                     ---------- ----------
    BasePriority             Property   System.Int32 BasePriority {get;}
    Container                Property   System.ComponentModel.IContainer Conta...
    EnableRaisingEvents      Property   System.Boolean EnableRaisingEvents {ge...
    ...
    ```

## <a name="see-also"></a>Lásd még:

[A parancsmag parancssori bemenet feldolgozása létrehozása](./adding-parameters-that-process-command-line-input.md)

[Adatcsatorna bemenetének feldolgozni a parancsmag létrehozása](./adding-parameters-that-process-pipeline-input.md)

[Hogyan hozhat létre egy Windows PowerShell-parancsmag](https://msdn.microsoft.com/en-us/0d721742-c849-4d0d-964f-78ddd9cd258c)

[Objektumtípusok kiterjesztése és formázása](https://msdn.microsoft.com/en-us/da976d91-a3d6-44e8-affa-466b1e2bd351)

[Hogyan működik a Windows PowerShell](https://msdn.microsoft.com/en-us/ced30e23-10af-4700-8933-49873bd84d58)

[How to Register parancsmagok, a szolgáltatók és az alkalmazások üzemeltetéséhez](https://msdn.microsoft.com/en-us/a41e9054-29c8-40ab-bf2b-8ce4e7ec1c8c)

[Windows PowerShell-referencia](../windows-powershell-reference.md)

[Parancsmag-minták](./cmdlet-samples.md)