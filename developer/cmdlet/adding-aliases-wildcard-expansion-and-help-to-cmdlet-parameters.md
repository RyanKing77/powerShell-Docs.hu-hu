---
title: Aliasok, helyettesítő bővítése, hozzáadását és parancsmag-paraméterek segítségével |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 931ccace-c565-4a98-8dcc-df00f86394b1
caps.latest.revision: 8
ms.openlocfilehash: 946b71e4480a47ac6ccd6930be445d7efb4fb62d
ms.sourcegitcommit: 01b81317029b28dd9b61d167045fd31f1ec7bc06
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2019
ms.locfileid: "65854893"
---
# <a name="adding-aliases-wildcard-expansion-and-help-to-cmdlet-parameters"></a>Aliasok, helyettesítő bővítők és súgó hozzáadása a parancsmag-paraméterekhez

Ez a szakasz ismerteti, hogyan lehet aliasokat, helyettesítő bővítése, szeretne felvenni, és segítséget a Stop-Proc parancsmag paramétereinek üzenetek (ismertetett [létrehozása egy parancsmag, amely módosítja a rendszer](./creating-a-cmdlet-that-modifies-the-system.md)).

A Stop-Proc parancsmag megkísérli leállítani a folyamatokat, amelyek a Get-Proc parancsmaggal olvassa be (ismertetett [létrehozásához az első parancsmag](./creating-a-cmdlet-without-parameters.md)).

## <a name="defining-the-cmdlet"></a>A parancsmag meghatározása

Mindig a parancsmag elnevezési és a .NET-osztály, amely megvalósítja a parancsmag deklaráló parancsmag létrehozásának első lépése. Kell írnia egy parancsmaggal módosíthatja, a rendszer, mert ennek megfelelően kell elnevezni azt. Ez a parancsmag rendszerfolyamatok leáll, mert a által meghatározott műveletet "Stop", használja a [System.Management.Automation.Verbslifecycle](/dotnet/api/System.Management.Automation.VerbsLifeCycle) osztályt, a főnév "Proc" folyamatot jelzi. A parancsmag jóváhagyott igék kapcsolatos további információkért lásd: [művelet neve](./approved-verbs-for-windows-powershell-commands.md).

A következő kódot a Stop-Proc parancsmag osztálydefiníció.

```csharp
[Cmdlet(VerbsLifecycle.Stop, "proc",
        SupportsShouldProcess = true)]
public class StopProcCommand : Cmdlet
```

## <a name="defining-parameters-for-system-modification"></a>A rendszer módosítás paraméterek megadása

A parancsmag paramétereit, a támogatási rendszer módosítását és a felhasználói visszajelzések kell. A parancsmag meg kell határoznia egy `Name` paraméter vagy ezzel egyenértékű, hogy a parancsmag fogja tudni módosítani, a rendszer valamilyen azonosítója. Emellett a parancsmag meg kell határoznia a `Force` és `PassThru` paramétereket. További információ ezekről a paraméterekről: [létrehozása egy parancsmag, amely módosítja a rendszer](./creating-a-cmdlet-that-modifies-the-system.md).

## <a name="defining-a-parameter-alias"></a>A paraméter-Alias meghatározása

A paraméter-alias lehet egy másik nevet vagy egy jól definiált levelek 1 vagy 2 levelek rövid nevét egy parancsmag-paraméterben. Mindkét esetben az aliasok célja, hogy egyszerűsítse a parancssorból felhasználói bejegyzés. Windows PowerShell paraméter-aliasok keresztül támogatja a [System.Management.Automation.Aliasattribute](/dotnet/api/System.Management.Automation.AliasAttribute) attribútuma, amely a deklaráció szintaxisa [Alias()].

A következő kód bemutatja, hogyan alias adnak hozzá a `Name` paraméter.

```csharp
/// <summary>
/// Specify the mandatory Name parameter used to identify the
/// processes to be stopped.
/// </summary>
[Parameter(
           Position = 0,
           Mandatory = true,
           ValueFromPipeline = true,
           ValueFromPipelineByPropertyName = true,
           HelpMessage = "The name of one or more processes to stop. Wildcards are permitted."
)]
[Alias("ProcessName")]
public string[] Name
{
  get { return processNames; }
  set { processNames = value; }
}
private string[] processNames;
```

Használata mellett a [System.Management.Automation.Aliasattribute](/dotnet/api/System.Management.Automation.AliasAttribute) attribútum, a Windows PowerShell-futtatókörnyezet végzi a részleges névegyeztetés, még akkor is, ha nincsenek aliasok vannak megadva. Például, ha a parancsmag rendelkezik egy `FileName` és, hogy a csak paraméter kezdetű `F`, adja meg a felhasználó `Filename`, `Filenam`, `File`, `Fi`, vagy `F` és továbbra is ismeri fel a bejegyzést a `FileName` paraméter.

## <a name="creating-help-for-parameters"></a>Paraméterek súgóját létrehozása

Windows PowerShell parancsmag-paraméterek súgó létrehozása teszi lehetővé. Ehhez a rendszer módosítás- és felhasználói visszajelzési használt bármelyik paraméternél. Súgó támogatásához minden egyes paraméterhez beállíthat a `HelpMessage` kulcsszó az attribútum a [System.Management.Automation.Parameterattribute](/dotnet/api/System.Management.Automation.ParameterAttribute) deklarace attribútum. Ezt a kulcsszót a szöveg megjelenítése a felhasználónak, ha segítségre van szüksége a paraméter használatával határozza meg. Is beállíthat a `HelpMessageBaseName` kulcsszó egy erőforrást használja, az üzenet alapneveként azonosításához. Ha ezt a kulcsszót, is meg kell adni a `HelpMessageResourceId` kulcsszó használatával adja meg az erőforrás-azonosítója.

A következő kódot a Stop-Proc parancsmag az határozza meg a `HelpMessage` attribútum kulcsszó a `Name` paraméter.

```csharp
/// <summary>
/// Specify the mandatory Name parameter used to identify the
/// processes to be stopped.
/// </summary>
[Parameter(
           Position = 0,
           Mandatory = true,
           ValueFromPipeline = true,
           ValueFromPipelineByPropertyName = true,
           HelpMessage = "The name of one or more processes to stop. Wildcards are permitted."
)]
```

## <a name="overriding-an-input-processing-method"></a>Egy bemeneti metódus feldolgozási felülbírálása

A parancsmag felül kell írnia egy bemeneti metódus feldolgozása, a leggyakrabban ez lesz [System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord). Ha módosítja a rendszer, a parancsmag meg kell hívnia a [System.Management.Automation.Cmdlet.ShouldProcess](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) és [System.Management.Automation.Cmdlet.ShouldContinue](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) módszereket, hogy a felhasználó Ha visszajelzést előtt módosításakor. Ezek a metódusok kapcsolatos további információkért lásd: [létrehozása egy parancsmag, amely módosítja a rendszer](./creating-a-cmdlet-that-modifies-the-system.md).

## <a name="supporting-wildcard-expansion"></a>Helyettesítő karakteres bővítésének támogatása

Ahhoz, hogy a kijelölt objektumok több, a parancsmag használható a [System.Management.Automation.Wildcardpattern](/dotnet/api/System.Management.Automation.WildcardPattern) és [System.Management.Automation.Wildcardoptions](/dotnet/api/System.Management.Automation.WildcardOptions) biztosít osztályok bemeneti paraméter helyettesítő bővítésének támogatása. Helyettesítő karakterek mintái példák lsa * \*.txt és [a – c]\*. Akkor használják, karakteréhez escape-karakter a biztonsági idézőjelet ('), amikor a minta szó szerint használandó karaktert tartalmaz.

Fájl elérési útja és neve helyettesítő bővülésből példák gyakori forgatókönyvek, ahol lehetséges, hogy szeretné, a parancsmag is lehetővé teszik az elérési út bemenetek támogatása, ha több objektum kiválasztásának megadása kötelező. Gyakori eset a fájlrendszer, ahol a felhasználó szeretné látni a az aktuális mappában található összes fájl szerepel.

A testre szabott helyettesítő minta egyező megvalósítás csak ritkán kell. A parancsmag ebben az esetben támogatnia kell a teljes POSIX 1003.2, 3.13 specifikáció helyettesítő bővítés céljából, vagy a következő egyszerűsített részére:

- **A kérdőjel (?).** Egyeztet bármilyen karaktert, a megadott helyen.

- **Csillag (\*).** A megadott helyen indítása nulla vagy több karakterre illeszkedik.

- **Nyitó zárójel ([]).** Egy minta zárójel kifejezés, amely vagy egy karaktertartományt tartalmazhat mutatja be. Tartomány megadása kötelező, ha a kötőjelet (-) jelzi a tartomány szolgál.

- **Záró zárójel (]).** Egy minta zárójel kifejezés befejeződik.

- **Ajánlat vissza escape-karaktert (').** Azt jelzi, hogy a következő karaktert szó szerint kell tenni. Vegye figyelembe, hogy a biztonsági-idézőjelet (programozott módon megadása) szemben a parancssorból megadásakor a vissza-ajánlat escape-karakter meg kell adni kétszer.

> [!NOTE]
> Helyettesítő karakterek mintái kapcsolatos további információkért lásd: [helyettesítő karaktereket támogató parancsmag-paraméterek](./supporting-wildcard-characters-in-cmdlet-parameters.md).

A következő kód bemutatja, hogyan helyettesítő beállítások megadása és definiálása a helyettesítő karakterrel feloldásához használt a `Name` parancsmag paraméter.

```csharp
WildcardOptions options = WildcardOptions.IgnoreCase |
                          WildcardOptions.Compiled;
WildcardPattern wildcard = new WildcardPattern(name,options);
```

A következő kód bemutatja tesztelése, hogy a folyamat neve megegyezik-e a meghatározott helyettesítő karakterrel. Figyelje meg, hogy, ebben az esetben a folyamat neve nem egyezik meg a mintát, ha a parancsmag továbbra is a következő folyamat nevét.

```csharp
if (!wildcard.IsMatch(processName))
{
  continue;
}
```

## <a name="code-sample"></a>Kódminta

A teljes C# mintakód, lásd: [StopProcessSample03 minta](./stopprocesssample03-sample.md).

## <a name="define-object-types-and-formatting"></a>Objektumtípusok és formázása

Windows PowerShell parancsmagok használatával a .net-objektumokká közötti továbbítja. Ennek következtében a parancsmag előfordulhat, hogy meg kell határoznia a saját típusát, vagy a parancsmag előfordulhat, hogy ki kell terjesztenie egy másik parancsmag által biztosított meglévő típus. Új típusok meghatározása, vagy meglévő típusok bővítésével kapcsolatos további információkért lásd: [objektumtípusok kiterjesztése és formázás](https://msdn.microsoft.com/en-us/da976d91-a3d6-44e8-affa-466b1e2bd351).

## <a name="building-the-cmdlet"></a>A parancsmag készítése

Parancsmag-k megvalósítása után regisztrálni kell a Windows PowerShell-lel a Windows PowerShell beépülő modullal. Parancsmagok regisztrálásával kapcsolatos további információkért lásd: [parancsmagjainak regisztrálásához, a szolgáltatók és az alkalmazások üzemeltetése hogyan](https://msdn.microsoft.com/en-us/a41e9054-29c8-40ab-bf2b-8ce4e7ec1c8c).

## <a name="testing-the-cmdlet"></a>A parancsmag tesztelése

Ha a parancsmagot a Windows PowerShell-lel regisztrálva lett, azt a parancssorból való futtatásával tesztelheti. Most tesztelje a parancsmagra állítsa le a folyamaton. A parancssorból-parancsmagokkal kapcsolatos további információkért lásd: a [első lépések a Windows PowerShell-lel](/powershell/scripting/getting-started/getting-started-with-windows-powershell).

- Indítsa el a Windows Powershellt, és állítsa le a folyamaton segítségével egy folyamatot a Folyamatnév alias használatával állítsa le a `Name` paraméter.

    ```powershell
    PS> stop-proc -ProcessName notepad
    ```

A következő eredmény jelenik meg.

    ```
    Confirm
    Are you sure you want to perform this action?
    Performing operation "stop-proc" on Target "notepad (3496)".
    [Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "Y"): Y
    ```

- Győződjön meg a következő bejegyzést a parancssoron. A Name paraméter megadása kötelező, mivel azt kéri. Írja be "!" Megjeleníti a paraméter kapcsolódó súgószöveg.

    ```powershell
    PS> stop-proc
    ```

A következő eredmény jelenik meg.

    ```
    Cmdlet stop-proc at command pipeline position 1
    Supply values for the following parameters:
    (Type !? for Help.)
    Name[0]: !?
    The name of one or more processes to stop. Wildcards are permitted.
    Name[0]: notepad
    ```

- Most ellenőrizze az összes folyamat, amely megfelel a helyettesítő karakteres mintának leállítani a következő bejegyzés "* Megjegyzés\*". Minden egyes folyamat, amely megfelel a mintának leállítása előtt a rendszer kéri.

    ```powershell
    PS> stop-proc -Name *note*
    ```

A következő eredmény jelenik meg.

    ```
    Confirm
    Are you sure you want to perform this action?
    Performing operation "stop-proc" on Target "notepad (1112)".
    [Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "Y"): Y
    ```

A következő eredmény jelenik meg.

    ```
    Confirm
    Are you sure you want to perform this action?
    Performing operation "stop-proc" on Target "ONENOTEM (3712)".
    [Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "Y"): N
    ```

A következő eredmény jelenik meg.

    ```
    Confirm
    Are you sure you want to perform this action?
    Performing operation "stop-proc" on Target "ONENOTE (3592)".
    [Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "Y"): N
    ```

## <a name="see-also"></a>Lásd még:

[Hozzon létre egy parancsmag, amely módosítja a rendszer](./creating-a-cmdlet-that-modifies-the-system.md)

[Hogyan hozhat létre egy Windows PowerShell-parancsmag](https://msdn.microsoft.com/en-us/0d721742-c849-4d0d-964f-78ddd9cd258c)

[Objektumtípusok kiterjesztése és formázása](https://msdn.microsoft.com/en-us/da976d91-a3d6-44e8-affa-466b1e2bd351)

[How to Register parancsmagok, a szolgáltatók és az alkalmazások üzemeltetéséhez](https://msdn.microsoft.com/en-us/a41e9054-29c8-40ab-bf2b-8ce4e7ec1c8c)

[A helyettesítő karakterek támogató parancsmag-paraméterek](./supporting-wildcard-characters-in-cmdlet-parameters.md)

[Windows PowerShell SDK](../windows-powershell-reference.md)
