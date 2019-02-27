---
title: Megszakítást nem a parancsmaghoz a hibajelentés hozzáadása |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f2a1531a-a92a-4606-9d54-c5df80d34f33
caps.latest.revision: 8
ms.openlocfilehash: 2f3bb481722363557c93ebbc5e6df62baeff2555
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56851015"
---
# <a name="adding-non-terminating-error-reporting-to-your-cmdlet"></a>Megszakítást nem okozó hibajelentések hozzáadása a parancsmaghoz

Parancsmagok meghívásával nonterminating hibák jelentheti a [System.Management.Automation.Cmdlet.Writeerror*](/dotnet/api/System.Management.Automation.Cmdlet.WriteError) módszer továbbra is megfelelően működjenek, az aktuális bemeneti objektumon, vagy további bejövő és folyamat-objektumok. Ez a szakasz ismerteti, hogyan hozhat létre olyan parancsmagot, amely a bemeneti feldolgozási módszerei a nonterminating hibát jelez.

Nonterminating hibák (csakúgy, mint a hibák megszakítást), a parancsmag át kell adnia egy [System.Management.Automation.Errorrecord](/dotnet/api/System.Management.Automation.ErrorRecord) objektum a hiba azonosítása. Minden egyes hibarekord azonosíthatók egy egyedi karakterlánccá, úgynevezett "hiba azonosítója." Az azonosító mellett minden egyes hibához kategóriáját állandók határozzák meg által meghatározott egy [System.Management.Automation.Errorcategory](/dotnet/api/System.Management.Automation.ErrorCategory) enumerálása. A felhasználó megtekintheti a hibákat azok kategória alapján beállításával a `$ErrorView` "CategoryView" változó.

Hiba a rekordok kapcsolatos további információkért lásd: [Windows PowerShell Hibarekordjainak](./windows-powershell-error-records.md).

Ez a szakasz témakörei a következők:

- [A parancsmag meghatározása](#Defining-the-Cmdlet)

- [Paraméterek megadása](#Defining-Parameters)

- [Bemeneti feldolgozási módszerek felülbírálása](#Overriding-Input-Processing-Methods)

- [Nonterminating hibát jelentett](#Reporting-Nonterminating-Errors)

- [Kódminta](#Code-Sample)

- [Objektumtípusok definiálása és formázása](#Define-Object-Types-and-Formatting)

- [A parancsmag készítése](#Building-the-Cmdlet)

- [A parancsmag tesztelése](#Testing-the-Cmdlet)

## <a name="defining-the-cmdlet"></a>A parancsmag meghatározása

Mindig a parancsmag elnevezési és a .NET-osztály, amely megvalósítja a parancsmag deklaráló parancsmag létrehozásának első lépése. Ez a parancsmag folyamat adatait, kérdezi le, így az itt választott művelet neve "Get". (A szinte bármilyen rendezési parancsmag, amely képes adatok beolvasása a parancssori bemenet tud feldolgozni.) A parancsmag jóváhagyott igék kapcsolatos további információkért lásd: [művelet neve](./approved-verbs-for-windows-powershell-commands.md).

A Get-Proc parancsmag definícióját a következő: Ez a definíció részleteit [létrehozásához az első parancsmag](./creating-a-cmdlet-without-parameters.md).

```csharp
[Cmdlet(VerbsCommon.Get, "proc")]
public class GetProcCommand: Cmdlet
```

```vb
<Cmdlet(VerbsCommon.Get, "Proc")> _
Public Class GetProcCommand
    Inherits Cmdlet
```

## <a name="defining-parameters"></a>Paraméterek megadása

Ha szükséges, a parancsmag meg kell határoznia a feldolgozása a bemeneti paraméterek. Meghatározza a Get-Proc parancsmag egy `Name` paraméter leírtak szerint [a folyamat parancssori bemenet-paramétereket adunk hozzá](./adding-parameters-that-process-command-line-input.md).

Íme a paraméterdeklarációhoz a a `Name` paramétert a Get-Proc parancsmag.

```csharp
[Parameter(
           Position = 0,
           ValueFromPipeline = true,
           ValueFromPipelineByPropertyName = true
)]
[ValidateNotNullOrEmpty]
public string[] Name
{
  get { return processNames; }
  set { processNames = value; }
}
private string[] processNames;
```

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

## <a name="overriding-input-processing-methods"></a>Bemeneti feldolgozási módszerek felülbírálása

Minden parancsmag felül kell írnia a bemeneti feldolgozási által biztosított módszerek közül legalább az [System.Management.Automation.Cmdlet](/dotnet/api/System.Management.Automation.Cmdlet) osztály. Ezek a metódusok tárgyalja [létrehozásához az első parancsmag](./creating-a-cmdlet-without-parameters.md).

> [!NOTE]
> A parancsmag minden rekord lehető egymástól függetlenül kell kezelni.

A Get-Proc parancsmag felülbírálja a [System.Management.Automation.Cmdlet.Processrecord*](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) metódust a `Name` paramétere a felhasználó vagy egy parancsfájl által megadott bemenetet. Ez a módszer a folyamatok minden kért Folyamatnév vagy az összes folyamat fog kapni, ha nincs név megadva. Ez a felülbírálás részleteit [létrehozásához az első parancsmag](./creating-a-cmdlet-without-parameters.md).

#### <a name="things-to-remember-when-reporting-errors"></a>Megjegyzendő tudnivalók jelentése hiba esetén

A [System.Management.Automation.Errorrecord](/dotnet/api/System.Management.Automation.ErrorRecord) objektumot, hogy a parancsmag továbbítja, ha maga kivétel hiba írása szükséges. Kövesse a .NET használata a kivétel meghatározásakor. Alapvetően Ha a hiba szemantikailag ugyanaz, mint a meglévő kivételt, a parancsmag kell használni vagy származtassa. a kivétel. Ellenkező esetben a kell származtatni egy új kivétel vagy közvetlenül a kivétel hierarchia a [System.Exception](/dotnet/api/System.Exception) osztály.

(FullyQualifiedErrorId osztály tulajdonságához tartozó a ErrorRecord keresztül érhetők el) hiba azonosítók létrehozása során vegye figyelembe a következőket.

- Megcélzott diagnosztikai céllal, hogy amikor a teljes azonosítót vizsgálatával megadhatja, hogy milyen a hiba van, és ahol a hiba érkezett karakterláncok használatát.

- Egy megfelelően formázott abszolút hiba azonosítója a következő lehet.

`CommandNotFoundException,Micrososft.PowerShell.Commands.GetCommanddCommand.`

Figyelje meg, hogy az előző példában a hiba azonosítója (az első token) jelöl ki a hibát, és a fennmaradó rész azt jelzi, hogy a hiba, honnan származnak.

- Az összetettebb esetekhez ponttal elválasztott jogkivonat, amely képes elemezni az ellenőrzési hiba azonosítója lehet. Ez lehetővé teszi, hogy hiba azonosítóját, valamint az azonosítóját, valamint a hiba hibakategória részeit túl ágban.

A parancsmag adott hiba általános jelentését azonosítók kell rendelni különböző kódhoz tartozó elérési út. Hozzárendelés hiba azonosítók szem előtt tartani a következő információkat:

- Hiba azonosítója a parancsmag életciklusa során állandó kell maradnia. Ne módosítsa a parancsmag-verziók közötti hiba azonosítója szemantikáját.

- Egy hiba azonosító, termékről a jelentett hiba szövege használja. Ne használjon szóközöket vagy absztrakt.

- A parancsmag csak az olyan hiba azonosítók, amelyek reprodukálható készítése rendelkezik. Ez például nem hozhat létre egy azonosítót, amely egy folyamat azonosítóját tartalmazza. Hiba azonosítók hasznosak a felhasználó, csak akkor, ha azok megegyeznek-azonosítók, amelyeket más azonos problémát tapasztalt felhasználók által is látható.

Nem kezelt kivételek nem észlelt Windows PowerShell a következő feltételek esetében alkalmazhatja:

- Parancsmag hoz létre egy új hozzászóláslánc és futó abban, hogy a szál nem kezelt kivételt jelez, ha a Windows PowerShell nem képes a hibát, és a folyamat leáll.

- Ha egy objektum nem kezelt kivételt okozó kód destruktoru vagy Dispose függvényhez módszereket, a Windows PowerShell nem képes a hibát, és a folyamat leáll.

## <a name="reporting-nonterminating-errors"></a>Nonterminating hibát jelentett

A bemeneti feldolgozási módszerek közül is tud jelentéseket nonterminating hiba a kimeneti adatfolyamhoz a a [System.Management.Automation.Cmdlet.Writeerror*](/dotnet/api/System.Management.Automation.Cmdlet.WriteError) metódust. Íme egy példa a Get-Proc parancsmag, amely bemutatja a hívást a [System.Management.Automation.Cmdlet.Writeerror*](/dotnet/api/System.Management.Automation.Cmdlet.WriteError) a felülbírálását belül a [ System.Management.Automation.Cmdlet.Processrecord*](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) metódust. Ebben az esetben a rendszer hívást kezdeményez, ha a parancsmag egy folyamatot egy adott folyamat azonosítója nem található.

```csharp
protected override void ProcessRecord()
{
  // If no name parameter passed to cmdlet, get all processes.
  if (processNames == null)
  {
    WriteObject(Process.GetProcesses(), true);
  }
    else
    {
      // If a name parameter is passed to cmdlet, get and write
      // the associated processes.
      // Write a nonterminating error for failure to retrieve
      // a process.
      foreach (string name in processNames)
      {
        Process[] processes;

        try
        {
          processes = Process.GetProcessesByName(name);
        }
        catch (InvalidOperationException ex)
        {
          WriteError(new ErrorRecord(
                     ex,
                     "NameNotFound",
                     ErrorCategory.InvalidOperation,
                     name));
          continue;
        }

        WriteObject(processes, true);
      } // foreach (...
    } // else
  }
```

#### <a name="things-to-remember-about-writing-nonterminating-errors"></a>Megjegyzendő tudnivalók Nonterminating hibák írása

Nonterminating hiba esetén a parancsmag kell létrehoznia egy adott hiba minden egyes megadott bemeneti objektum azonosítója.

A parancsmag gyakran van szükség, a Windows PowerShell-művelet nonterminating hiba által előállított módosításához. Ez ehhez meghatározása a `ErrorAction` és `ErrorVariable` paramétereket. Ha az határozza meg a `ErrorAction` paramétert, a parancsmag megjeleníti a felhasználói beállítások [System.Management.Automation.Actionpreference](/dotnet/api/system.management.automation.actionpreference), beállításával közvetlenül is befolyásolhatja a művelet a `$ErrorActionPreference` változó.

A parancsmag nonterminating hibák mentheti egy változó használatával a `ErrorVariable` paramétert, amely nem befolyásolja a beállítását `ErrorAction`. Hibák fűzhető egy létező hiba változó plusz jelre (+) hozzáadásával az előtérben, a változó nevét.

## <a name="code-sample"></a>Kódminta

A teljes C# mintakód, lásd: [GetProcessSample04 minta](./getprocesssample04-sample.md).

## <a name="define-object-types-and-formatting"></a>Objektumtípusok és formázása

Windows PowerShell parancsmagok használatával a .NET-objektumokká közötti továbbítja. Ennek következtében a parancsmag előfordulhat, hogy meg kell határoznia a saját típusát, vagy a parancsmag előfordulhat, hogy ki kell terjesztenie egy másik parancsmag által biztosított meglévő típus. Új típusok meghatározása, vagy meglévő típusok bővítésével kapcsolatos további információkért lásd: [objektumtípusok kiterjesztése és formázás](http://msdn.microsoft.com/en-us/da976d91-a3d6-44e8-affa-466b1e2bd351).

## <a name="building-the-cmdlet"></a>A parancsmag készítése

Parancsmag-k megvalósítása után regisztrálnia kell azt a Windows PowerShell-lel a Windows PowerShell beépülő modullal. Parancsmagok regisztrálásával kapcsolatos további információkért lásd: [parancsmagjainak regisztrálásához, a szolgáltatók és az alkalmazások üzemeltetése hogyan](http://msdn.microsoft.com/en-us/a41e9054-29c8-40ab-bf2b-8ce4e7ec1c8c).

## <a name="testing-the-cmdlet"></a>A parancsmag tesztelése

Ha a parancsmagot a Windows PowerShell-lel regisztrálva lett, azt a parancssorból való futtatásával tesztelheti. Most tesztelheti a minta Get-Proc parancsmaggal ellenőrizheti, hogy hibát jelez:

- Indítsa el a Windows Powershellt, és a Get-Proc parancsmag használatával lekérheti az a "Teszt" nevű folyamatokat.

    ```powershell
    PS> get-proc -name test
    ```

A következő eredmény jelenik meg.

    ```
    get-proc : Operation is not valid due to the current state of the object.
    At line:1 char:9
    + get-proc  <<<< -name test
    ```

## <a name="see-also"></a>Lásd még:

[Folyamat folyamat bemeneti paraméterek hozzáadása](./adding-parameters-that-process-pipeline-input.md)

[Parancssori bemenet feldolgozása paraméterek hozzáadása](./adding-parameters-that-process-command-line-input.md)

[Az első parancsmag létrehozása](./creating-a-cmdlet-without-parameters.md)

[Objektumtípusok kiterjesztése és formázása](http://msdn.microsoft.com/en-us/da976d91-a3d6-44e8-affa-466b1e2bd351)

[How to Register parancsmagok, a szolgáltatók és az alkalmazások üzemeltetéséhez](http://msdn.microsoft.com/en-us/a41e9054-29c8-40ab-bf2b-8ce4e7ec1c8c)

[Windows PowerShell-referencia](../windows-powershell-reference.md)

[Parancsmag-minták](./cmdlet-samples.md)
