---
title: Paraméter hozzáadása a parancsmag beállítja |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- parameter sets [PowerShell Programmer's Guide]
ms.assetid: a6131db4-fd6e-45f1-bd47-17e7174afd56
caps.latest.revision: 8
ms.openlocfilehash: f0bff11618c18bf53b9c2a185445795a17306fa3
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62068837"
---
# <a name="adding-parameter-sets-to-a-cmdlet"></a>Paraméterkészletek hozzáadása parancsmagokhoz

Ez a szakasz ismerteti a Stop-Proc parancsmaghoz paraméterkészletek hozzáadása (ismertetett [létrehozása egy parancsmag, amely módosítja a rendszer](./creating-a-cmdlet-that-modifies-the-system.md)). Hasonló a Stop-Proc más parancsmagoknak a programozói útmutatóban leírt, ez a parancsmag megkísérli leállítani folyamatokat, amelyek a Get-Proc parancsmaggal olvassa be (ismertetett [létrehozásához az első parancsmag](./creating-a-cmdlet-without-parameters.md)).

Ez a szakasz témakörei a következők:

- [Tudnivaló paraméterkészlettel kapcsolatban](#Adding-Parameter-Sets-to-a-Cmdlet)

- [A parancsmag osztály deklaráló](#Declaring-the-Cmdlet-Class)

- [A parancsmag paramétereit deklaráló](#Declaring-the-Parameters-of-the-Cmdlet)

- [Egy bemeneti metódus feldolgozási felülbírálása](#Overriding-an-Input-Processing-Method)

- [Kódminta](#Declaring-the-Parameters-of-the-Cmdlet)

- [Objektumtípusok definiálása és formázása](#Defining-Object-Types-and-Formatting)

- [A parancsmag készítése](#Building-the-Cmdlet)

- [A parancsmag tesztelése](#Testing-the-Cmdlet)

## <a name="things-to-know-about-parameter-sets"></a>Tudnivaló paraméterkészlettel kapcsolatban

Windows PowerShell-paramétert olyan paramétereket, működjön együtt határozza meg. -Okat a parancsmag paramétereit, hozzon létre egy egyetlen parancsmag, amely alapján a csoport milyen paraméterek a felhasználó adja meg a működését is módosíthatja.

Például olyan parancsmagot, amely két paraméterkészlettel használ a különböző funkciók meghatározására a `Get-EventLog` parancsmag Windows PowerShell által biztosított. Ez a parancsmag különböző információkat ad vissza, ha a felhasználó adja meg a `List` vagy `LogName` paraméter. Ha a `LogName` paraméter meg van adva, a parancsmag visszaadja a eseményekkel kapcsolatos információkat lévő adott eseménynaplóból. Ha a `List` paraméter meg van adva, a parancsmag visszaadja a napló információ fájlok magukat (nem az események adatait tartalmazzák). Ebben az esetben a `List` és `LogName` paraméterek két külön paraméterkészlettel azonosításához.

Tudnivalók paraméterkészlettel két fontos dolog, hogy a Windows PowerShell-modul egy adott bevitel beállítása csak egyetlen paramétert használ, és, hogy minden egyes paraméterkészletet rendelkeznie kell legalább egy paramétert, amely egyedi az adott paraméterkészletet.

A legutóbbi pont mutatja be, a Stop-Proc parancsmag három paraméterkészlettel használ: `ProcessName`, `ProcessId`, és `InputObject`. Ezek paraméterkészlettel mindegyike rendelkezik, amely nem szerepel a többi paraméterkészlettel egy paramétert. A paraméterkészlettel megoszthat más paramétereket, de a parancsmag az egyedi paramétereket használja `ProcessName`, `ProcessId`, és `InputObject` azonosításához, mely a Windows PowerShell-modul használandó paraméterek készletével.

## <a name="declaring-the-cmdlet-class"></a>A parancsmag osztály deklaráló

Mindig a parancsmag elnevezési és a .NET-osztály, amely megvalósítja a parancsmag deklaráló parancsmag létrehozásának első lépése. A parancsmag az életciklus-művelet "Stop" használatos, mert a parancsmag rendszerfolyamatok leáll. A főnév neve "Proc" használata a parancsmag a folyamatok működik. Az alábbi nyilatkozatot jegyezze fel, hogy a parancsmag ige és főnév neve jelennek-e be a parancsmag az osztály nevét.

> [!NOTE]
> További információ a jóváhagyott művelet neve: [művelet neve](./approved-verbs-for-windows-powershell-commands.md).

A következő kódot a Stop-Proc parancsmag osztálydefiníció.

```csharp
[Cmdlet(VerbsLifecycle.Stop, "Proc",
        DefaultParameterSetName = "ProcessId",
        SupportsShouldProcess = true)]
public class StopProcCommand : PSCmdlet
```

```vb
<Cmdlet(VerbsLifecycle.Stop, "Proc", DefaultParameterSetName:="ProcessId", _
SupportsShouldProcess:=True)> _
Public Class StopProcCommand
    Inherits PSCmdlet
```

## <a name="declaring-the-parameters-of-the-cmdlet"></a>A parancsmag paramétereit deklaráló

Ez a parancsmag három paraméter szükséges a parancsmag (ezeket a paramétereket is megadhatja a paraméterkészlettel), majd határozza meg, valamint egy `Force` paraméter, amely kezeli a parancsmag funkciója és a egy `PassThru` paraméter, amely meghatározza, hogy küld-e a parancsmag egy a folyamat keretében kimeneti objektumot. Alapértelmezés szerint ez a parancsmag nem felel meg a folyamat használatával egy objektumot. Ezen utolsó két paraméterekkel kapcsolatos további információkért lásd: [létrehozása egy parancsmag, amely módosítja a rendszer](./creating-a-cmdlet-that-modifies-the-system.md).

### <a name="declaring-the-name-parameter"></a>A Name paraméter deklaráló

A bemeneti paraméter lehetővé teszi, hogy a felhasználó számára le kell állítani a folyamatok nevét adja meg. Vegye figyelembe, hogy a `ParameterSetName` kulcsszó az attribútum a [System.Management.Automation.Parameterattribute](/dotnet/api/System.Management.Automation.ParameterAttribute) attribútum meghatározza, hogy a `ProcessName` paraméterkészlet ehhez a paraméterhez.

[!code-csharp[StopProcessSample04.cs](../../powershell-sdk-samples/SDK-2.0/csharp/StopProcessSample04/StopProcessSample04.cs#L44-L58 "StopProcessSample04.cs")]

```vb
<Parameter(Position:=0, ParameterSetName:="ProcessName", _
Mandatory:=True, _
ValueFromPipeline:=True, ValueFromPipelineByPropertyName:=True, _
HelpMessage:="The name of one or more processes to stop. " & _
    "Wildcards are permitted."), [Alias]("ProcessName")> _
Public Property Name() As String()
    Get
        Return processNames
    End Get
    Set(ByVal value As String())
        processNames = value
    End Set
End Property

Private processNames() As String
```

Fontos megjegyezni, hogy az alias "ProcessName" a paraméter van megadva.

### <a name="declaring-the-id-parameter"></a>Az Id paraméter deklaráló

A bemeneti paraméter lehetővé teszi, hogy a felhasználó számára le kell állítani a folyamatok azonosítóját adja meg. Vegye figyelembe, hogy a `ParameterSetName` kulcsszó az attribútum a [System.Management.Automation.Parameterattribute](/dotnet/api/System.Management.Automation.ParameterAttribute) attribútum meghatározza, hogy a `ProcessId` paraméterkészletet.

```csharp
[Parameter(
           ParameterSetName = "ProcessId",
           Mandatory = true,
           ValueFromPipelineByPropertyName = true,
           ValueFromPipeline = true
)]
[Alias("ProcessId")]
public int[] Id
{
  get { return processIds; }
  set { processIds = value; }
}
private int[] processIds;
```

```vb
<Parameter(ParameterSetName:="ProcessId", _
Mandatory:=True, _
ValueFromPipelineByPropertyName:=True, _
ValueFromPipeline:=True), [Alias]("ProcessId")> _
Public Property Id() As Integer()
    Get
        Return processIds
    End Get
    Set(ByVal value As Integer())
        processIds = value
    End Set
End Property
Private processIds() As Integer
```

Fontos megjegyezni, hogy az alias "Folyamatazonosító" a paraméter van megadva.

### <a name="declaring-the-inputobject-parameter"></a>Deklaráló InputObject paraméter

A bemeneti paraméter lehetővé teszi, hogy a felhasználó megadhatja a bemeneti objektum, amely le kell állítani a folyamatokkal kapcsolatos információkat tartalmazza. Vegye figyelembe, hogy a `ParameterSetName` kulcsszó az attribútum a [System.Management.Automation.Parameterattribute](/dotnet/api/System.Management.Automation.ParameterAttribute) attribútum meghatározza, hogy a `InputObject` paraméterkészlet ehhez a paraméterhez.

```csharp
[Parameter(
           ParameterSetName = "InputObject",
           Mandatory = true,
           ValueFromPipeline = true)]
public Process[] InputObject
{
  get { return inputObject; }
  set { inputObject = value; }
}
private Process[] inputObject;
```

```vb
<Parameter(ParameterSetName:="InputObject", _
Mandatory:=True, ValueFromPipeline:=True)> _
Public Property InputObject() As Process()
    Get
        Return myInputObject
    End Get
    Set(ByVal value As Process())
        myInputObject = value
    End Set
End Property
Private myInputObject() As Process
```

Ne feledje is, hogy ez a paraméter nincs aliasneve.

### <a name="declaring-parameters-in-multiple-parameter-sets"></a>Paramétereket a több paraméterkészlettel deklaráló

Bár az egyes paraméternek egyedi paraméternek kell lennie, paraméterek egynél több paraméterkészlettel is tartozhat. Ezekben az esetekben adja meg a megosztott paraméter egy [System.Management.Automation.Parameterattribute](/dotnet/api/System.Management.Automation.ParameterAttribute) típusattribútum-deklaráció egyes beállítása mely, amely a paraméter tartozik. Ha egy paraméter paraméterkészlettel minden, akkor csak egyszer deklarálja a paraméter-attribútumhoz kell, és nem kell megadnia a paraméterkészlet neve.

## <a name="overriding-an-input-processing-method"></a>Egy bemeneti metódus feldolgozási felülbírálása

Minden parancsmagot felül kell írnia egy bemeneti metódus feldolgozása, a leggyakrabban ez lesz a [System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) metódust. Ebben a parancsmagban a [System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) úgy, hogy a parancsmag képes feldolgozni a folyamatok tetszőleges számú módszert felülbírálja. Tartalmaz egy kiválasztási utasítás, amely meghívja a melyik paraméterkészlet alapján más módszert a felhasználó adta meg.

```csharp
protected override void ProcessRecord()
{
  switch (ParameterSetName)
  {
    case "ProcessName":
         ProcessByName();
         break;

    case "ProcessId":
         ProcessById();
         break;

    case "InputObject":
         foreach (Process process in inputObject)
         {
           SafeStopProcess(process);
         }
         break;

    default:
         throw new ArgumentException("Bad ParameterSet Name");
  } // switch (ParameterSetName...
} // ProcessRecord
```

```vb
Protected Overrides Sub ProcessRecord()
    Select Case ParameterSetName
        Case "ProcessName"
            ProcessByName()

        Case "ProcessId"
            ProcessById()

        Case "InputObject"
            Dim process As Process
            For Each process In myInputObject
                SafeStopProcess(process)
            Next process

        Case Else
            Throw New ArgumentException("Bad ParameterSet Name")
    End Select

End Sub 'ProcessRecord ' ProcessRecord
```

Az a Select-utasítás által meghívott segédmetódusokat nem ebben a témakörben találhatók, de megtekintheti a teljes kódmintát a következő szakaszban a végrehajtásuk.

## <a name="code-sample"></a>Kódminta

A teljes C# mintakód, lásd: [StopProcessSample04 minta](./stopprocesssample04-sample.md).

## <a name="defining-object-types-and-formatting"></a>Objektumtípusok definiálása és formázása

Windows PowerShell parancsmagok használatával a .NET-objektumokká közötti továbbítja. Ennek következtében a parancsmag előfordulhat, hogy meg kell határoznia a saját típusát, vagy a parancsmag előfordulhat, hogy ki kell terjesztenie egy másik parancsmag által biztosított meglévő típus. Új típusok meghatározása, vagy meglévő típusok bővítésével kapcsolatos további információkért lásd: [objektumtípusok kiterjesztése és formázás](http://msdn.microsoft.com/en-us/da976d91-a3d6-44e8-affa-466b1e2bd351).

## <a name="building-the-cmdlet"></a>A parancsmag készítése

Parancsmag-k megvalósítása után regisztrálnia kell azt a Windows PowerShell-lel a Windows PowerShell beépülő modullal. Parancsmagok regisztrálásával kapcsolatos további információkért lásd: [parancsmagjainak regisztrálásához, a szolgáltatók és az alkalmazások üzemeltetése hogyan](http://msdn.microsoft.com/en-us/a41e9054-29c8-40ab-bf2b-8ce4e7ec1c8c).

## <a name="testing-the-cmdlet"></a>A parancsmag tesztelése

Ha a parancsmagot a Windows PowerShell-lel regisztrálva lett, tesztelje azt a parancssorból való futtatásával. Az alábbiakban néhány tesztek azt mutatják be, hogyan a `ProcessId` és `InputObject` paraméterek azok paraméterkészlettel leállítani a folyamat teszteléséhez használhatók.

- A Windows PowerShell-lel elindult, futtassa a Stop-Proc parancsmagot a `ProcessId` paraméter beállítása annak azonosítója alapján a folyamat leállítása. Ebben az esetben a parancsmagot használja a `ProcessId` paraméterkészlet a folyamat leállítása érdekében.

    ```
    PS> stop-proc -Id 444
    Confirm
    Are you sure you want to perform this action?
    Performing operation "stop-proc" on Target "notepad (444)".
    [Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "Y"): Y
    ```

- A Windows PowerShell-lel elindult, futtassa a Stop-Proc parancsmagot a `InputObject` paraméterkészlet folyamatok leállítani a Jegyzettömb objektum által beolvasott a `Get-Process` parancsot.

    ```
    PS> get-process notepad | stop-proc
    Confirm
    Are you sure you want to perform this action?
    Performing operation "stop-proc" on Target "notepad (444)".
    [Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "Y"): N
    ```

## <a name="see-also"></a>Lásd még:

[A parancsmag létrehozása, amely módosítja a rendszer](./creating-a-cmdlet-that-modifies-the-system.md)

[Hogyan hozhat létre egy Windows PowerShell-parancsmag](http://msdn.microsoft.com/en-us/0d721742-c849-4d0d-964f-78ddd9cd258c)

[Objektumtípusok kiterjesztése és formázása](http://msdn.microsoft.com/en-us/da976d91-a3d6-44e8-affa-466b1e2bd351)

[How to Register parancsmagok, a szolgáltatók és az alkalmazások üzemeltetéséhez](http://msdn.microsoft.com/en-us/a41e9054-29c8-40ab-bf2b-8ce4e7ec1c8c)

[Windows PowerShell SDK](../windows-powershell-reference.md)
