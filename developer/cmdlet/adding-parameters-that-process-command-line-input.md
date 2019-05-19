---
title: Parancssori bemenet feldolgozása-paramétereket adunk hozzá |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- cmdlets [PowerShell Programmer's Guide], parameters
- Get-Proc cmdlet [PowerShell Programmer's Guide]
- cmdlets [PowerShell Programmer's Guide], command line input
- command line input [PowerShell Programmer's Guide]
- parameters [PowerShell Programmer's Guide]
- cmdlets [PowerShell Programmer's Guide], creating
ms.assetid: da0b32f8-7b51-440e-a061-3177b5759e0e
caps.latest.revision: 9
ms.openlocfilehash: c9ad84c5bcb6826fcf51db9a1f1a578a65a1f275
ms.sourcegitcommit: 01b81317029b28dd9b61d167045fd31f1ec7bc06
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2019
ms.locfileid: "65854948"
---
# <a name="adding-parameters-that-process-command-line-input"></a>Parancssori bemenetet feldolgozó paraméterek hozzáadása

A parancsmag bemenete egy forrása a parancssorból. Ez a témakör ismerteti, hogyan adhat hozzá egy paramétert a **Get-Proc** parancsmag (amely leírt [létrehozásához az első parancsmag](./creating-a-cmdlet-without-parameters.md)), hogy a parancsmag bemeneti a helyi számítógépről explicit alapján tud feldolgozni. a parancsmagnak átadott objektum. A **Get-Proc** leírt parancsmag itt lekéri a nevük alapján folyamatok, majd megjeleníti a a folyamatokra vonatkozó parancsot a parancssorba.

## <a name="defining-the-cmdlet-class"></a>A parancsmag osztály meghatározása

A parancsmag létrehozásának első lépése elnevezési parancsmag és a .NET-keretrendszer osztály, amely megvalósítja a parancsmag a nyilatkozat. Ez a parancsmag folyamat adatait, kérdezi le, így az itt választott művelet neve "Get". (A szinte bármilyen rendezési parancsmag, amely képes adatok beolvasása a parancssori bemenet tud feldolgozni.) A parancsmag jóváhagyott igék kapcsolatos további információkért lásd: [művelet neve](./approved-verbs-for-windows-powershell-commands.md).

Íme az osztálydeklaráció számára a **Get-Proc** parancsmagot. Ez a definíció kapcsolatos részletes információkat [létrehozásához az első parancsmag](./creating-a-cmdlet-without-parameters.md).

```csharp
[Cmdlet(VerbsCommon.Get, "proc")]
public class GetProcCommand: Cmdlet
```

```vb
<Cmdlet(VerbsCommon.Get, "Proc")> _
Public Class GetProcCommand
    Inherits Cmdlet
```

## <a name="declaring-parameters"></a>Paraméterek deklaráló

Egy parancsmag-paraméterben lehetővé teszi, hogy a felhasználó számára információk megadása a parancsmaghoz. A következő példában **Get-Proc** és `Get-Member` átadott parancsmagok nevei és `MemberType` egy paraméter a `Get-Member` parancsmagot. A paraméter argumentuma a "property".

**PS > get-proc; `get-member` - membertype tulajdonság**

Deklarálja a parancsmag paraméterei, először meg kell határoznia a tulajdonságokat, amelyek a paramétereket. Az a **Get-Proc** , a parancsmag csak paraméter `Name`, amely ebben az esetben a .NET-keretrendszer folyamat lekérni kívánt objektum nevét jelöli. Ezért a parancsmag osztály nevének tömbjét fogadására karakterlánc típusú tulajdonsága határozza meg.

Íme a paraméterdeklarációhoz a a `Name` paraméterében a **Get-Proc** parancsmagot.

```csharp
/// <summary>
/// Specify the cmdlet Name parameter.
/// </summary>
  [Parameter(Position = 0)]
  [ValidateNotNullOrEmpty]
  public string[] Name
  {
    get { return processNames; }
    set { processNames = value; }
  }
  private string[] processNames;

  #endregion Parameters
```

```vb
<Parameter(Position:=0), ValidateNotNullOrEmpty()> _
Public Property Name() As String()
    Get
        Return processNames
    End Get

    Set(ByVal value As String())
        processNames = value
    End Set

End Property
```

A Windows PowerShell-modult, amely Ez a tulajdonság tájékoztatja a `Name` paramétert, egy [System.Management.Automation.Parameterattribute](/dotnet/api/System.Management.Automation.ParameterAttribute) attribútummal egészül ki a tulajdonság meghatározása. Alapszintű szintaxis miatt ez az attribútum `[Parameter()]`.

> [!NOTE]
> Egy paraméter fel kell tüntetni explicit módon is nyilvános. Nem nyilvános, belső alapértelmezett vannak megjelölve, és a Windows PowerShell-modul nem találhatók paraméterek.

Ezt a parancsmagot használja a karakterláncok a `Name` paraméter. Ha lehetséges a parancsmaghoz is meg kell határozniuk paraméter egy tömb, mert ez lehetővé teszi a parancsmagot, amely egynél több elem fogadja el.

#### <a name="things-to-remember-about-parameter-definitions"></a>Megjegyzendő Paraméterdefiníciókra kapcsolatos tudnivalók

- Előre meghatározott Windows PowerShell paraméter nevükkel és adattípusukkal kell annak biztosításához, hogy a parancsmag kompatibilis a Windows PowerShell-parancsmagok, a lehetséges használható újra. Például, ha az összes parancsmagot használja az előre definiált `Id` paraméternév egy erőforrást, a felhasználó fog könnyedén azonosíthatja a paramétert, függetlenül attól, milyen parancsmagot használják szerinti ismertetése. Paraméterek nevei alapvetően ugyanazokat a szabályokat használ a közös nyelvi futtatókörnyezet (CLR) a változók nevében hajtsa végre. A paraméter elnevezésével kapcsolatos további információkért lásd: [parancsmag-paraméterek nevei](https://msdn.microsoft.com/en-us/c4500737-0a05-4d01-911b-394424c65bfb).

- Windows PowerShell fenntart egy egységes felhasználói élmény érdekében néhány paraméterek nevei. Ne használja a következő paraméter neve: `WhatIf`, `Confirm`, `Verbose`, `Debug`, `Warn`, `ErrorAction`, `ErrorVariable`, `OutVariable`, és `OutBuffer`. Ezenkívül ezek a paraméterek nevei a következő aliasok vannak fenntartva: `vb`, `db`, `ea`, `ev`, `ov`, és `ob`.

- `Name` van egy egyszerű és közös paraméter neve, a parancsmagok használata ajánlott. Célszerűbb válassza ki a paraméter neve, mint egy összetett nevét, amely egy adott parancsmag egyedi, és nehéz megjegyezni ehhez hasonló.

- Paramétereket is kis-és a Windows PowerShellben, noha alapértelmezés szerint a rendszerhéj megőrzi az esetet. Kisbetű/nagybetű megkülönböztetése argumentum attól függ, hogy a parancsmag a műveletet. Megadott parancssori argumentumot továbbítson a paramétert.

- Más paraméter deklarációinak példákért lásd [parancsmag-paraméterek](./cmdlet-parameters.md).

## <a name="declaring-parameters-as-positional-or-named"></a>A Helyzetbeállító vagy elnevezett paraméterek deklaráló

A parancsmag be kell állítania minden paraméter, vagy egy csak pozíciórekord vagy elnevezett paraméter. Mindkét típusú paramétereket fogadja el az egyetlen argumentumot, vesszővel válassza el egymástól, és logikai beállítások elválasztva több argumentumot. Egy logikai paramétert, más néven egy *váltson*, csak a logikai beállítások kezeli. A kapcsoló a paraméter meglétének szolgál. Az ajánlott alapértelmezett érték `false`.

A minta **Get-Proc** parancsmag határozza meg a `Name` paraméter 0 pozíciója a Helyzetbeállító paraméterként. Ez azt jelenti, hogy a rendszer automatikusan beszúrja az első argumentum a parancssorban a felhasználó megadja ezt a paramétert. Ha szeretne meghatározni egy elnevezett paraméterhez, amelyhez a felhasználónak meg kell adnia a paraméternév megadásához, a parancssorból, ne módosítsa a `Position` kulcsszó a típusattribútum-deklaráció kívül.

> [!NOTE]
> Paraméterek névvel kell rendelkeznie, hacsak azt javasoljuk, hogy a leggyakrabban használt paraméterek csak pozíciórekord, hogy a felhasználóknak nem kell írja be a paraméter neve.

## <a name="declaring-parameters-as-mandatory-or-optional"></a>Kötelező vagy választható paramétereket deklaráló

A parancsmag be kell állítania minden paraméter egy választható vagy egy kötelező paraméter. A minta **Get-Proc** parancsmagot, a `Name` paraméter nem kötelező megadni, mert a `Mandatory` kulcsszó a típusattribútum-deklaráció nem állítható.

## <a name="supporting-parameter-validation"></a>Támogató paraméter ellenőrzése

A minta **Get-Proc** parancsmag hozzáadja egy bemenet-ellenőrzés attribútum [System.Management.Automation.Validatenotnulloremptyattribute](/dotnet/api/System.Management.Automation.ValidateNotNullOrEmptyAttribute), az a `Name` érvényesítéséhez paraméter, amely a bemeneti adat sem `null` , se nem üres. Ez az attribútum a Windows PowerShell által biztosított több ellenőrzési attribútumok egyike. Egyéb ellenőrzési attribútumok példákért lásd [paraméter bemeneti ellenőrzése](./validating-parameter-input.md).

```
[Parameter(Position = 0)]
[ValidateNotNullOrEmpty]
public string[] Name
```

## <a name="overriding-an-input-processing-method"></a>Egy bemeneti metódus feldolgozási felülbírálása

A parancsmagot, a parancssori bemenet kezelésére, ha azt a megfelelő bemeneti feldolgozási módszerek felül kell írnia. Az alapszintű bemeneti feldolgozási módszerek jelennek meg a [létrehozásához az első parancsmag](./creating-a-cmdlet-without-parameters.md).

A **Get-Proc** parancsmag felülbírálja a [System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) metódust a `Name` paraméter megadott információ a felhasználó vagy egy parancsfájlt. Ez a módszer beolvassa a folyamatok minden kért Folyamatnév, és az összes folyamat, ha nincs név megadva. Figyelje meg, hogy a [System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord), a hívást [System.Management.Automation.Cmdlet.WriteObject%28System.Object%2CSystem.Boolean%29](/dotnet/api/system.management.automation.cmdlet.writeobject?view=powershellsdk-1.1.0#System_Management_Automation_Cmdlet_WriteObject_System_Object_System_Boolean_) a kimenete a folyamat küld kimeneti mechanizmus objektumokat. A második paraméter a hívás `enumerateCollection`, értékre van állítva `true` tájékoztatja a Windows PowerShell-futtatókörnyezet, a kimeneti tömbben folyamat objektumok számbavétele és a egy folyamat egyszerre írni a parancssorból.

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
    }
  }
}
```

```vb
Protected Overrides Sub ProcessRecord()

    '/ If no process names are passed to the cmdlet, get all processes.
    If processNames Is Nothing Then
        Dim processes As Process()
        processes = Process.GetProcesses()
    End If

    '/ If process names are specified, write the processes to the
    '/ pipeline to display them or make them available to the next cmdlet.

    For Each name As String In processNames
        '/ The second parameter of this call tells PowerShell to enumerate the
        '/ array, and send one process at a time to the pipeline.
        WriteObject(Process.GetProcessesByName(name), True)
    Next

End Sub 'ProcessRecord
```

## <a name="code-sample"></a>Kódminta

A teljes C# mintakód, lásd: [GetProcessSample02 minta](./getprocesssample02-sample.md).

## <a name="defining-object-types-and-formatting"></a>Objektumtípusok definiálása és formázása

Windows PowerShell parancsmagok használatával a .NET-keretrendszer objektumok közötti továbbítja. Ennek következtében a parancsmag előfordulhat, hogy meg kell határoznia a saját típusát, vagy parancsmag előfordulhat, hogy ki kell terjesztenie egy másik parancsmag által biztosított meglévő típus. Új típusok meghatározása, vagy meglévő típusok bővítésével kapcsolatos további információkért lásd: [objektumtípusok kiterjesztése és formázás](http://msdn.microsoft.com/en-us/da976d91-a3d6-44e8-affa-466b1e2bd351).

## <a name="building-the-cmdlet"></a>A parancsmag készítése

A parancsmag megvalósítása, után regisztrálnia kell azt a Windows PowerShell-lel a Windows PowerShell beépülő modul használatával. Parancsmagok regisztrálásával kapcsolatos további információkért lásd: [parancsmagjainak regisztrálásához, a szolgáltatók és az alkalmazások üzemeltetése hogyan](http://msdn.microsoft.com/en-us/a41e9054-29c8-40ab-bf2b-8ce4e7ec1c8c).

## <a name="testing-the-cmdlet"></a>A parancsmag tesztelése

Amikor a parancsmag a Windows PowerShell használatával regisztrál, azt a parancssorból való futtatásával tesztelheti. Itt két módon a minta parancsmagot a kódja tesztelésére. A parancssorból-parancsmagokkal kapcsolatos további információkért lásd: [első lépések a Windows PowerShell-lel](/powershell/scripting/getting-started/getting-started-with-windows-powershell).

- A Windows PowerShell parancssorába a következő paranccsal listázhatja az Internet Explorer folyamat, amely a neve "IEXPLORE."

    ```powershell
    PS> get-proc -name iexplore
    ```

A következő eredmény jelenik meg.

    ```
    Handles  NPM(K)  PM(K)   WS(K)  VS(M)  CPU(s)   Id   ProcessName
    -------  ------  -----   -----  -----   ------ --   -----------
        354      11  10036   18992    85   0.67   3284   iexplore
    ```

- A listán az Internet Explorer, az Outlook és a Jegyzettömb folyamatok "IEXPLORE" nevű, "OUTLOOK" és "A JEGYZETTÖMB," a következő paranccsal. Ha több folyamatot, ezek mindegyike jelennek meg.

    ```powershell
    PS> get-proc -name iexplore, outlook, notepad
    ```

A következő eredmény jelenik meg.

    ```
    Handles  NPM(K)  PM(K)   WS(K)  VS(M)  CPU(s)   Id   ProcessName
    -------  ------  -----   -----  -----  ------   --    -----------
        732      21  24696    5000    138   2.25  2288   iexplore
        715      19  20556   14116    136   1.78  3860   iexplore
       3917      62  74096   58112    468 191.56  1848   OUTLOOK
         39       2   1024    3280     30   0.09  1444   notepad
         39       2   1024     356     30   0.08  3396   notepad
    ```

## <a name="see-also"></a>Lásd még:

[Folyamat folyamat bemeneti paraméterek hozzáadása](./adding-parameters-that-process-pipeline-input.md)

[Az első parancsmag létrehozása](./creating-a-cmdlet-without-parameters.md)

[Objektumtípusok kiterjesztése és formázása](http://msdn.microsoft.com/en-us/da976d91-a3d6-44e8-affa-466b1e2bd351)

[How to Register parancsmagok, a szolgáltatók és az alkalmazások üzemeltetéséhez](http://msdn.microsoft.com/en-us/a41e9054-29c8-40ab-bf2b-8ce4e7ec1c8c)

[Windows PowerShell-referencia](../windows-powershell-reference.md)

[Parancsmag-minták](./cmdlet-samples.md)
