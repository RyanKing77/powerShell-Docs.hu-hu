---
title: Parancsmag létrehozása adattár eléréséhez
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.openlocfilehash: 7acccbd48dcfb654b11e448a1f24835ad3668fae
ms.sourcegitcommit: a02ccbeaa17c0e513d6c4a21b877c88ac7725458
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/28/2019
ms.locfileid: "70104468"
---
# <a name="creating-a-cmdlet-to-access-a-data-store"></a>Parancsmag létrehozása adattár eléréséhez

Ez a szakasz azt ismerteti, hogyan hozható létre olyan parancsmag, amely egy Windows PowerShell-szolgáltató segítségével fér hozzá a tárolt adatmennyiségekhez. Ez a típusú parancsmag a Windows PowerShell futtatókörnyezet Windows PowerShell-szolgáltatói infrastruktúráját használja, ezért a parancsmag osztálynak a [System. Management. Automation. PSCmdlet](/dotnet/api/System.Management.Automation.PSCmdlet) alaposztályból kell származnia.

Az itt leírt Select-Str parancsmag megkeresheti és kiválaszthatja a karakterláncokat egy fájlban vagy objektumban. A karakterlánc azonosítására szolgáló mintázatok explicit módon megadhatók a parancsmag `Path` paraméterén keresztül, vagy implicit módon a `Script` paraméterrel.

A parancsmagot úgy tervezték, hogy bármely, a [System. Management. Automation. Provider. Icontentcmdletprovider](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider)származtatott Windows PowerShell-szolgáltatót használja. A parancsmag például megadhatja a fájlrendszer-szolgáltatót vagy a Windows PowerShell által biztosított változó szolgáltatót. További információ a PowerShell-szolgáltatók aboutWindows: [a Windows PowerShell-szolgáltató](../prog-guide/designing-your-windows-powershell-provider.md)megtervezése.

## <a name="defining-the-cmdlet-class"></a>A parancsmag osztályának meghatározása

A parancsmag létrehozásának első lépése mindig a parancsmag elnevezése, és a parancsmagot implementáló .NET-osztály deklarálása. Ez a parancsmag bizonyos karakterláncokat észlel, így az itt választott művelet neve a [System. Management. Automation. Verbscommon](/dotnet/api/System.Management.Automation.VerbsCommon) osztály által definiált "Select". A rendszer a "Str" főnévi nevet használja, mert a parancsmag karakterláncokat használ. Az alábbi deklarációban vegye figyelembe, hogy a parancsmag-utasítás és a főnév neve a parancsmag osztályának nevében jelenik meg. További információ a jóváhagyott parancsmag-műveletekről: [parancsmag-műveletek nevei](./approved-verbs-for-windows-powershell-commands.md).

Az ehhez a parancsmaghoz tartozó .NET-osztálynak a [System. Management. Automation. PSCmdlet](/dotnet/api/System.Management.Automation.PSCmdlet) alaposztályból kell származnia, mivel a Windows PowerShell-futtatókörnyezet számára szükséges támogatást biztosít a Windows PowerShell-szolgáltatói infrastruktúra elérhetővé tétele érdekében. Vegye figyelembe, hogy ez a parancsmag a .NET-keretrendszer reguláris kifejezéseit is használja, például a [System. Text. RegularExpressions. regex](/dotnet/api/System.Text.RegularExpressions.Regex)osztályt.

Az alábbi kód a Select-Str parancsmag osztályának definíciója.

```csharp
[Cmdlet(VerbsCommon.Select, "Str", DefaultParameterSetName="PatternParameterSet")]
public class SelectStringCommand : PSCmdlet
```

Ez a parancsmag egy alapértelmezett paramétert határoz meg úgy `DefaultParameterSetName` , hogy hozzáadja az attribútum kulcsszót az osztály deklarációjában. Ha a `PatternParameterSet` `Script` paraméter nincs megadva, a rendszer az alapértelmezett paramétert használja. A paraméterrel kapcsolatos további információkért tekintse meg a `Pattern` és `Script` a paramétert a következő szakaszban.

## <a name="defining-parameters-for-data-access"></a>Paraméterek definiálása adateléréshez

Ez a parancsmag számos olyan paramétert definiál, amely lehetővé teszi a felhasználó számára a tárolt adatok elérését és vizsgálatát. Ezek a paraméterek egy `Path` olyan paramétert tartalmaznak, amely megadja az adattár helyét, `Pattern` egy paramétert, amely meghatározza a keresésben használandó mintát, és számos más paramétert, amelyek támogatják a keresés végrehajtását.

> [!NOTE]
> További információ a paraméterek definiálásának alapjairól: [Paraméterek hozzáadása a parancssori bemenet feldolgozásához](./adding-parameters-that-process-command-line-input.md).

### <a name="declaring-the-path-parameter"></a>A Path paraméter deklarálása

Az adattár megkereséséhez a parancsmagnak egy Windows PowerShell-elérési utat kell használnia az adattár elérésére tervezett Windows PowerShell-szolgáltató azonosításához. Ezért egy `Path` String Array típusú paramétert határoz meg a szolgáltató helyének jelzéséhez.

```csharp
[Parameter(
           Position = 0,
           ParameterSetName = "ScriptParameterSet",
           Mandatory = true)]
[Parameter(
           Position = 0,
           ParameterSetName = "PatternParameterSet",
           ValueFromPipeline = true,
           Mandatory = true)]
           [Alias("PSPath")]
public string[] Path
{
  get { return paths; }
  set { paths = value; }
}
private string[] paths;
```

Vegye figyelembe, hogy ez a paraméter két különböző paraméterhez tartozik, és aliassal rendelkezik.

Két [System. Management. Automation. Parameterattribute](/dotnet/api/System.Management.Automation.ParameterAttribute) attribútum deklarálja, hogy `Path` a paraméter a `ScriptParameterSet` és a `PatternParameterSet`közé tartozik. További információ a paraméterekről: [Paraméterek beállítása parancsmaghoz](./adding-parameter-sets-to-a-cmdlet.md).

A [System. Management. Automation. Aliasattribute](/dotnet/api/System.Management.Automation.AliasAttribute) attribútum deklarálja `PSPath` a `Path` paraméter aliasát. Az alias deklarálása kifejezetten ajánlott a Windows PowerShell-szolgáltatókat elérő más parancsmagokkal való konzisztencia érdekében. A PowerShell elérési útjaival kapcsolatos további információkért tekintse meg a [Windows PowerShell működése](/previous-versions//ms714658(v=vs.85))a PowerShell-aboutWindows című témakört.

### <a name="declaring-the-pattern-parameter"></a>A minta paraméter deklarálása

A keresendő mintázatok megadásához a parancsmag olyan `Pattern` paramétert deklarál, amely karakterláncok tömbje. A rendszer pozitív eredményt ad vissza, ha bármelyik minta megtalálható az adattárban. Vegye figyelembe, hogy ezek a minták lefordított reguláris kifejezéseket tartalmazó tömbbe vagy literális keresésekhez használt helyettesítő mintázatokból állnak.

```csharp
[Parameter(
           Position = 1,
           ParameterSetName = "PatternParameterSet",
           Mandatory = true)]
public string[] Pattern
{
  get { return patterns; }
  set { patterns = value; }
}
private string[] patterns;
private Regex[] regexPattern;
private WildcardPattern[] wildcardPattern;
```

Ha ez a paraméter meg `PatternParameterSet`van adva, a parancsmag az alapértelmezett paramétert használja. Ebben az esetben a parancsmag az itt megadott mintákat használja a karakterláncok kiválasztásához. Ezzel szemben a `Script` paramétert a mintákat tartalmazó parancsfájl megadására is felhasználhatja. A `Script` és`Pattern` a paraméterek két külön paramétert határoznak meg, így kölcsönösen kizárják egymást.

### <a name="declaring-search-support-parameters"></a>Keresési támogatási paraméterek deklarálása

Ez a parancsmag az alábbi támogatási paramétereket határozza meg, amelyek segítségével módosíthatja a parancsmag keresési képességeit.

A `Script` paraméter egy parancsfájl-blokkot határoz meg, amely a parancsmag alternatív keresési mechanizmusának biztosítására használható. A szkriptnek tartalmaznia kell a megfeleltetéshez használt mintákat, és vissza kell adni a [System. Management. Automation. PSObject](/dotnet/api/System.Management.Automation.PSObject) objektumot. Vegye figyelembe, hogy ez a paraméter a beállított `ScriptParameterSet` paramétert azonosító egyedi paraméter is. Ha a Windows PowerShell-futtatókörnyezet ezt a paramétert látja, csak a `ScriptParameterSet` beállított paraméterekhez tartozó paramétereket használja.

```csharp
[Parameter(
           Position = 1,
           ParameterSetName = "ScriptParameterSet",
           Mandatory = true)]
public ScriptBlock Script
{
  set { script = value; }
  get { return script; }
}
ScriptBlock script;
```

A `SimpleMatch` paraméter egy switch paraméter, amely azt jelzi, hogy a parancsmag explicit módon egyezik-e a megadott mintákkal. Ha a felhasználó megadja a paramétert a parancssorban (`true`), a parancsmag a megadott mintákat használja. Ha a paraméter nincs megadva (`false`), a parancsmag reguláris kifejezéseket használ. A paraméter alapértelmezett értéke `false`a következő:.

```csharp
[Parameter]
public SwitchParameter SimpleMatch
{
  get { return simpleMatch; }
  set { simpleMatch = value; }
}
private bool simpleMatch;
```

A `CaseSensitive` paraméter egy switch paraméter, amely jelzi, hogy a rendszer megkülönbözteti-e a kis-és nagybetűket. Ha a felhasználó megadja a paramétert a parancssorban (`true`), a parancsmag a minták összehasonlításakor a karakterek kis-és nagybetűjét is ellenőrzi. Ha a paraméter nincs megadva (`false`), a parancsmag nem különbözteti meg a kis-és nagybetűket. Például a "sajat" és a "sajat" is pozitív találatként lesz visszaadva. A paraméter alapértelmezett értéke `false`a következő:.

```csharp
[Parameter]
public SwitchParameter CaseSensitive
{
  get { return caseSensitive; }
  set { caseSensitive = value; }
}
private bool caseSensitive;
```

A `Exclude` és`Include` paraméterek azonosítják azokat az elemeket, amelyeket kifejezetten kizárnak a keresésből vagy azokból. Alapértelmezés szerint a parancsmag az adattár összes elemét keresi. A parancsmag által végrehajtott keresés korlátozásához azonban ezek a paraméterek használhatók a keresésbe foglalandó vagy kihagyott elemek explicit jelzésére.

```csharp
[Parameter]
public SwitchParameter CaseSensitive
{
  get { return caseSensitive; }
  set { caseSensitive = value; }
}
private bool caseSensitive;
```

```csharp
[Parameter]
[ValidateNotNullOrEmpty]
public string[] Include
{
  get
  {
    return includeStrings;
  }
  set
  {
    includeStrings = value;

    this.include = new WildcardPattern[includeStrings.Length];
    for (int i = 0; i < includeStrings.Length; i++)
    {
      this.include[i] = new WildcardPattern(includeStrings[i], WildcardOptions.IgnoreCase);
    }
  }
}

internal string[] includeStrings = null;
internal WildcardPattern[] include = null;
```

### <a name="declaring-parameter-sets"></a>Paraméter-készletek deklarálása

Ez a parancsmag két paraméter-készletet `PatternParameterSet`használ (`ScriptParameterSet` és ez az alapértelmezett beállítás), amely az adatelérés során használt két paraméterérték neve. `PatternParameterSet`az alapértelmezett paraméter van beállítva, és a `Pattern` paraméter megadásakor használatos. `ScriptParameterSet`akkor használható, ha a felhasználó egy másik keresési mechanizmust ad `Script` meg a paraméter használatával. További információ a paraméterekről: [Paraméterek beállítása parancsmaghoz](./adding-parameter-sets-to-a-cmdlet.md).

## <a name="overriding-input-processing-methods"></a>Bemeneti feldolgozási módszerek felülbírálása

A parancsmagoknak felül kell bírálni a [System. Management. Automation. PSCmdlet](/dotnet/api/System.Management.Automation.PSCmdlet) osztály egy vagy több bemeneti feldolgozási módszerét. További információ a bemeneti feldolgozási módszerekről: [az első parancsmag létrehozása](./creating-a-cmdlet-without-parameters.md).

Ez a parancsmag felülbírálja a [System. Management. Automation. parancsmag. BeginProcessing](/dotnet/api/System.Management.Automation.Cmdlet.BeginProcessing) metódust, amely lefordított reguláris kifejezések tömbjét hozza létre indításkor. Ez növeli a teljesítményt a nem egyszerű egyezést nem használó keresések során.

```csharp
protected override void BeginProcessing()
{
  WriteDebug("Validating patterns.");
  if (patterns != null)
  {
    foreach(string pattern in patterns)
    {
      if (pattern == null)
      ThrowTerminatingError(new ErrorRecord(
                            new ArgumentNullException(
                            "Search pattern cannot be null."),
                            "NullSearchPattern",
                            ErrorCategory.InvalidArgument,
                            pattern)
                            );
    }

    WriteVerbose("Search pattern(s) are valid.");

    // If a simple match is not specified, then
    // compile the regular expressions once.
    if (!simpleMatch)
    {
      WriteDebug("Compiling search regular expressions.");

      RegexOptions regexOptions = RegexOptions.Compiled;
      if (!caseSensitive)
         regexOptions |= RegexOptions.Compiled;
      regexPattern = new Regex[patterns.Length];

      for (int i = 0; i < patterns.Length; i++)
      {
        try
        {
          regexPattern[i] = new Regex(patterns[i], regexOptions);
        }
        catch (ArgumentException ex)
        {
          ThrowTerminatingError(new ErrorRecord(
                        ex,
                        "InvalidRegularExpression",
                        ErrorCategory.InvalidArgument,
                        patterns[i]
                     ));
        }
      } //Loop through patterns to create RegEx objects.

      WriteVerbose("Pattern(s) compiled into regular expressions.");
    }// If not a simple match.

    // If a simple match is specified, then compile the
    // wildcard patterns once.
    else
    {
      WriteDebug("Compiling search wildcards.");

      WildcardOptions wildcardOptions = WildcardOptions.Compiled;

      if (!caseSensitive)
      {
        wildcardOptions |= WildcardOptions.IgnoreCase;
      }

      wildcardPattern = new WildcardPattern[patterns.Length];
      for (int i = 0; i < patterns.Length; i++)
      {
        wildcardPattern[i] =
                     new WildcardPattern(patterns[i], wildcardOptions);
      }

      WriteVerbose("Pattern(s) compiled into wildcard expressions.");
    }// If match is a simple match.
  }// If valid patterns are available.
}// End of function BeginProcessing().
```

Ez a parancsmag felülbírálja a [System. Management. Automation. parancsmag. ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) metódust is, amellyel feldolgozhatja azokat a karakterlánc-beállításokat, amelyeket a felhasználó a parancssorban végrehajt. A karakterlánc-kijelölés eredményét egyéni objektum formájában írja le egy privát **MatchString** metódus meghívásával.

```csharp
protected override void ProcessRecord()
{
  UInt64 lineNumber = 0;
  MatchInfo result;
  ArrayList nonMatches = new ArrayList();

  // Walk the list of paths and search the contents for
  // any of the specified patterns.
  foreach (string psPath in paths)
  {
    // Once the filepaths are expanded, we may have more than one
    // path, so process all referenced paths.
    foreach(PathInfo path in
            SessionState.Path.GetResolvedPSPathFromPSPath(psPath)
           )
    {
      WriteVerbose("Processing path " + path.Path);

      // Check if the path represents one of the items to be
      // excluded. If so, continue to next path.
      if (!MeetsIncludeExcludeCriteria(path.ProviderPath))
         continue;

      // Get the content reader for the item(s) at the
      // specified path.
      Collection<IContentReader> readerCollection = null;
      try
      {
        readerCollection =
                    this.InvokeProvider.Content.GetReader(path.Path);
      }
      catch (PSNotSupportedException ex)
      {
        WriteError(new ErrorRecord(ex,
                   "ContentAccessNotSupported",
                    ErrorCategory.NotImplemented,
                    path.Path)
                   );
        return;
      }

      foreach(IContentReader reader in readerCollection)
      {
        // Reset the line number for this path.
        lineNumber = 0;

        // Read in a single block (line in case of a file)
        // from the object.
        IList items = reader.Read(1);

        // Read and process one block(line) at a time until
        // no more blocks(lines) exist.
        while (items != null && items.Count == 1)
        {
          // Increment the line number each time a line is
          // processed.
          lineNumber++;

          String message = String.Format("Testing line {0} : {1}",
                                        lineNumber, items[0]);

          WriteDebug(message);

          result = SelectString(items[0]);

          if (result != null)
          {
            result.Path = path.Path;
            result.LineNumber = lineNumber;

            WriteObject(result);
          }
          else
          {
            // Add the block(line) that did not match to the
            // collection of non matches , which will be stored
            // in the SessionState variable $NonMatches
            nonMatches.Add(items[0]);
          }

          // Get the next line from the object.
          items = reader.Read(1);

        }// While loop for reading one line at a time.
      }// Foreach loop for reader collection.
    }// Foreach loop for processing referenced paths.
  }// Foreach loop for walking of path list.

  // Store the list of non-matches in the
  // session state variable $NonMatches.
  try
  {
    this.SessionState.PSVariable.Set("NonMatches", nonMatches);
  }
  catch (SessionStateUnauthorizedAccessException ex)
  {
    WriteError(new ErrorRecord(ex,
               "CannotWriteVariableNonMatches",
               ErrorCategory.InvalidOperation,
               nonMatches)
              );
  }

}// End of protected override void ProcessRecord().
```

## <a name="accessing-content"></a>Tartalom elérése

A parancsmagnak meg kell nyitnia a Windows PowerShell elérési útja által jelzett szolgáltatót, hogy hozzáférhessen az adataihoz. A RunSpace [System. Management. Automation. sessionstate](/dotnet/api/System.Management.Automation.SessionState) objektuma a szolgáltatóhoz való hozzáféréshez használatos, míg a (z) parancsmag [System. Management. Automation. PSCmdlet. Invokeprovider *](/dotnet/api/System.Management.Automation.PSCmdlet.InvokeProvider) tulajdonsága a szolgáltató megnyitására szolgál. A tartalomhoz való hozzáférést a [System. Management. Automation. Providerintrinsics](/dotnet/api/System.Management.Automation.ProviderIntrinsics) objektum lekérésével lehet megnyitva a szolgáltató számára.

Ez a minta Select-Str parancsmag a [System. Management. Automation. Providerintrinsics. Content *](/dotnet/api/System.Management.Automation.ProviderIntrinsics.Content) tulajdonság használatával teszi elérhetővé a tartalmat a vizsgálathoz. Ezután meghívhatja a [System. Management. Automation. Contentcmdletproviderintrinsics. Getreader *](/dotnet/api/System.Management.Automation.ContentCmdletProviderIntrinsics.GetReader) metódust, átadva a szükséges Windows PowerShell-elérési utat.

## <a name="code-sample"></a>Mintakód

A következő kód a Select-Str parancsmag ezen verziójának megvalósítását mutatja be. Vegye figyelembe, hogy ez a kód tartalmazza a parancsmag osztályt, a parancsmag által használt privát metódusokat, valamint a parancsmag regisztrálásához használt Windows PowerShell beépülő modul kódját. A parancsmag regisztrálásával kapcsolatos további információkért lásd: [a parancsmag felépítése](#defining-the-cmdlet-class).

```csharp
//
// Copyright (c) 2006 Microsoft Corporation. All rights reserved.
//
// THIS CODE AND INFORMATION IS PROVIDED "AS IS" WITHOUT WARRANTY OF
// ANY KIND, EITHER EXPRESSED OR IMPLIED, INCLUDING BUT NOT LIMITED TO
// THE IMPLIED WARRANTIES OF MERCHANTABILITY AND/OR FITNESS FOR A
// PARTICULAR PURPOSE.
//
using System;
using System.Text.RegularExpressions;
using System.Collections;
using System.Collections.ObjectModel;
using System.Management.Automation;
using System.Management.Automation.Provider;
using System.ComponentModel;

namespace Microsoft.Samples.PowerShell.Commands
{
  #region SelectStringCommand
  /// <summary>
  /// This cmdlet searches through PSObjects for particular patterns.
  /// </summary>
  /// <remarks>
  /// This cmdlet can be used to search any object, such as a file or a
  /// variable, whose provider exposes methods for reading and writing
  /// content.
  /// </remarks>
  [Cmdlet(VerbsCommon.Select, "Str", DefaultParameterSetName="PatternParameterSet")]
  public class SelectStringCommand : PSCmdlet
  {
    #region Parameters
    /// <summary>
    /// Declare a Path parameter that specifies where the data is stored.
    /// This parameter must specify a PowerShell that indicates the
    /// PowerShell provider that is used to access the objects to be
    /// searched for matching patterns. This parameter should also have
    /// a PSPath alias to provide consistency with other cmdlets that use
    /// PowerShell providers.
    /// </summary>
    /// <value>Path of the object(s) to search.</value>
    [Parameter(
               Position = 0,
               ParameterSetName = "ScriptParameterSet",
               Mandatory = true)]
    [Parameter(
               Position = 0,
               ParameterSetName = "PatternParameterSet",
               ValueFromPipeline = true,
               Mandatory = true)]
               [Alias("PSPath")]
    public string[] Path
    {
      get { return paths; }
      set { paths = value; }
    }
    private string[] paths;

    /// <summary>
    /// Declare a Pattern parameter that specifies the pattern(s)
    /// used to find matching patterns in the string representation
    /// of the objects. A positive result will be returned
    /// if any of the patterns are found in the objects.
    /// </summary>
    /// <remarks>
    /// The patterns will be compiled into an array of wildcard
    /// patterns for a simple match (literal string matching),
    /// or the patterns will be converted into an array of compiled
    /// regular expressions.
    /// </remarks>
    /// <value>Array of patterns to search.</value>
    [Parameter(
               Position = 1,
               ParameterSetName = "PatternParameterSet",
               Mandatory = true)]
    public string[] Pattern
    {
      get { return patterns; }
      set { patterns = value; }
    }
    private string[] patterns;
    private Regex[] regexPattern;
    private WildcardPattern[] wildcardPattern;

    /// <summary>
    /// Declare a Script parameter that specifies a script block
    /// that is called to perform the matching operations
    /// instead of the matching performed by the cmdlet.
    /// </summary>
    /// <value>Script block that will be called for matching</value>
    [Parameter(
               Position = 1,
               ParameterSetName = "ScriptParameterSet",
               Mandatory = true)]
    public ScriptBlock Script
    {
      set { script = value; }
      get { return script; }
    }
    ScriptBlock script;

    /// <summary>
    /// Declare a switch parameter that specifies if the pattern(s) are used
    /// literally. If not (default), searching is
    /// done using regular expressions.
    /// </summary>
    /// <value>If True, a literal pattern is used.</value>
    [Parameter]
    public SwitchParameter SimpleMatch
    {
      get { return simpleMatch; }
      set { simpleMatch = value; }
    }
    private bool simpleMatch;

    /// <summary>
    /// Declare a switch parameter that specifies if a case-sensitive
    /// search is performed.  If not (default), a case-insensitive search
    /// is performed.
    /// </summary>
    /// <value>If True, a case-sensitive search is made.</value>
    [Parameter]
    public SwitchParameter CaseSensitive
    {
      get { return caseSensitive; }
      set { caseSensitive = value; }
    }
    private bool caseSensitive;

    /// <summary>
    /// Declare an Include parameter that species which
    /// specific items are searched.  When this parameter
    /// is used, items that are not listed here are omitted
    /// from the search.
    /// </summary>
    [Parameter]
    [ValidateNotNullOrEmpty]
    public string[] Include
    {
      get
      {
        return includeStrings;
      }
      set
      {
        includeStrings = value;

        this.include = new WildcardPattern[includeStrings.Length];
        for (int i = 0; i < includeStrings.Length; i++)
        {
          this.include[i] = new WildcardPattern(includeStrings[i], WildcardOptions.IgnoreCase);
        }
      }
    }

    internal string[] includeStrings = null;
    internal WildcardPattern[] include = null;

    /// <summary>
    /// Declare an Exclude parameter that species which
    /// specific items are omitted from the search.
    /// </summary>
    ///
    [Parameter]
    [ValidateNotNullOrEmpty]
    public string[] Exclude
    {
      get
      {
        return excludeStrings;
      }
      set
      {
        excludeStrings = value;

        this.exclude = new WildcardPattern[excludeStrings.Length];
        for (int i = 0; i < excludeStrings.Length; i++)
        {
          this.exclude[i] = new WildcardPattern(excludeStrings[i], WildcardOptions.IgnoreCase);
        }
      }
    }
    internal string[] excludeStrings;
    internal WildcardPattern[] exclude;

    #endregion Parameters

    #region Overrides
    /// <summary>
    /// If regular expressions are used for pattern matching,
    /// then build an array of compiled regular expressions
    /// at startup. This increases performance during scanning
    /// operations when simple matching is not used.
    /// </summary>
    protected override void BeginProcessing()
    {
      WriteDebug("Validating patterns.");
      if (patterns != null)
      {
        foreach(string pattern in patterns)
        {
          if (pattern == null)
          ThrowTerminatingError(new ErrorRecord(
                                new ArgumentNullException(
                                "Search pattern cannot be null."),
                                "NullSearchPattern",
                                ErrorCategory.InvalidArgument,
                                pattern)
                                );
        }

        WriteVerbose("Search pattern(s) are valid.");

        // If a simple match is not specified, then
        // compile the regular expressions once.
        if (!simpleMatch)
        {
          WriteDebug("Compiling search regular expressions.");

          RegexOptions regexOptions = RegexOptions.Compiled;
          if (!caseSensitive)
             regexOptions |= RegexOptions.Compiled;
          regexPattern = new Regex[patterns.Length];

          for (int i = 0; i < patterns.Length; i++)
          {
            try
            {
              regexPattern[i] = new Regex(patterns[i], regexOptions);
            }
            catch (ArgumentException ex)
            {
              ThrowTerminatingError(new ErrorRecord(
                            ex,
                            "InvalidRegularExpression",
                            ErrorCategory.InvalidArgument,
                            patterns[i]
                         ));
            }
          } //Loop through patterns to create RegEx objects.

          WriteVerbose("Pattern(s) compiled into regular expressions.");
        }// If not a simple match.

        // If a simple match is specified, then compile the
        // wildcard patterns once.
        else
        {
          WriteDebug("Compiling search wildcards.");

          WildcardOptions wildcardOptions = WildcardOptions.Compiled;

          if (!caseSensitive)
          {
            wildcardOptions |= WildcardOptions.IgnoreCase;
          }

          wildcardPattern = new WildcardPattern[patterns.Length];
          for (int i = 0; i < patterns.Length; i++)
          {
            wildcardPattern[i] =
                         new WildcardPattern(patterns[i], wildcardOptions);
          }

          WriteVerbose("Pattern(s) compiled into wildcard expressions.");
        }// If match is a simple match.
      }// If valid patterns are available.
    }// End of function BeginProcessing().

    /// <summary>
    /// Process the input and search for the specified patterns.
    /// </summary>
    protected override void ProcessRecord()
    {
      UInt64 lineNumber = 0;
      MatchInfo result;
      ArrayList nonMatches = new ArrayList();

      // Walk the list of paths and search the contents for
      // any of the specified patterns.
      foreach (string psPath in paths)
      {
        // Once the filepaths are expanded, we may have more than one
        // path, so process all referenced paths.
        foreach(PathInfo path in
                SessionState.Path.GetResolvedPSPathFromPSPath(psPath)
               )
        {
          WriteVerbose("Processing path " + path.Path);

          // Check if the path represents one of the items to be
          // excluded. If so, continue to next path.
          if (!MeetsIncludeExcludeCriteria(path.ProviderPath))
             continue;

          // Get the content reader for the item(s) at the
          // specified path.
          Collection<IContentReader> readerCollection = null;
          try
          {
            readerCollection =
                        this.InvokeProvider.Content.GetReader(path.Path);
          }
          catch (PSNotSupportedException ex)
          {
            WriteError(new ErrorRecord(ex,
                       "ContentAccessNotSupported",
                        ErrorCategory.NotImplemented,
                        path.Path)
                       );
            return;
          }

          foreach(IContentReader reader in readerCollection)
          {
            // Reset the line number for this path.
            lineNumber = 0;

            // Read in a single block (line in case of a file)
            // from the object.
            IList items = reader.Read(1);

            // Read and process one block(line) at a time until
            // no more blocks(lines) exist.
            while (items != null && items.Count == 1)
            {
              // Increment the line number each time a line is
              // processed.
              lineNumber++;

              String message = String.Format("Testing line {0} : {1}",
                                            lineNumber, items[0]);

              WriteDebug(message);

              result = SelectString(items[0]);

              if (result != null)
              {
                result.Path = path.Path;
                result.LineNumber = lineNumber;

                WriteObject(result);
              }
              else
              {
                // Add the block(line) that did not match to the
                // collection of non matches , which will be stored
                // in the SessionState variable $NonMatches
                nonMatches.Add(items[0]);
              }

              // Get the next line from the object.
              items = reader.Read(1);

            }// While loop for reading one line at a time.
          }// Foreach loop for reader collection.
        }// Foreach loop for processing referenced paths.
      }// Foreach loop for walking of path list.

      // Store the list of non-matches in the
      // session state variable $NonMatches.
      try
      {
        this.SessionState.PSVariable.Set("NonMatches", nonMatches);
      }
      catch (SessionStateUnauthorizedAccessException ex)
      {
        WriteError(new ErrorRecord(ex,
                   "CannotWriteVariableNonMatches",
                   ErrorCategory.InvalidOperation,
                   nonMatches)
                  );
      }

    }// End of protected override void ProcessRecord().
    #endregion Overrides

    #region PrivateMethods
    /// <summary>
    /// Check for a match using the input string and the pattern(s)
    /// specified.
    /// </summary>
    /// <param name="input">The string to test.</param>
    /// <returns>MatchInfo object containing information about
    /// result of a match</returns>
    private MatchInfo SelectString(object input)
    {
      string line = null;

      try
      {
        // Convert the object to a string type
        // safely using language support methods
        line = (string)LanguagePrimitives.ConvertTo(
                                                    input,
                                                    typeof(string)
                                                    );
        line = line.Trim(' ','\t');
      }
      catch (PSInvalidCastException ex)
      {
        WriteError(new ErrorRecord(
                   ex,
                   "CannotCastObjectToString",
                   ErrorCategory.InvalidOperation,
                   input)
                   );

        return null;
      }

      MatchInfo result = null;

      // If a scriptblock has been specified, call it
      // with the path for processing.  It will return
      // one object.
      if (script != null)
      {
        WriteDebug("Executing script block.");

        Collection<PSObject> psObjects =
                             script.Invoke(
                                           line,
                                           simpleMatch,
                                           caseSensitive
                                          );

        foreach (PSObject psObject in psObjects)
        {
          if (LanguagePrimitives.IsTrue(psObject))
          {
            result = new MatchInfo();
            result.Line = line;
            result.IgnoreCase = !caseSensitive;

            break;
          } //End of If.
        } //End ForEach loop.
      } // End of If if script exists.

      // If script block exists, see if this line matches any
      // of the match patterns.
      else
      {
        int patternIndex = 0;

        while (patternIndex < patterns.Length)
        {
          if ((simpleMatch &&
              wildcardPattern[patternIndex].IsMatch(line))
              || (regexPattern != null
              && regexPattern[patternIndex].IsMatch(line))
             )
          {
            result = new MatchInfo();
            result.IgnoreCase = !caseSensitive;
            result.Line = line;
            result.Pattern = patterns[patternIndex];

            break;
          }

          patternIndex++;

        }// While loop through patterns.
      }// Else for no script block specified.

      return result;

    }// End of SelectString

    /// <summary>
    /// Check whether the supplied name meets the include/exclude criteria.
    /// That is - it's on the include list if the include list was
    /// specified, and not on the exclude list if the exclude list was specified.
    /// </summary>
    /// <param name="path">path to validate</param>
    /// <returns>True if the path is acceptable.</returns>
    private bool MeetsIncludeExcludeCriteria(string path)
    {
      bool ok = false;

      // See if the file is on the include list.
      if (this.include != null)
      {
        foreach (WildcardPattern patternItem in this.include)
        {
          if (patternItem.IsMatch(path))
          {
            ok = true;
            break;
          }
        }
      }
      else
      {
        ok = true;
      }

      if (!ok)
         return false;

      // See if the file is on the exclude list.
      if (this.exclude != null)
      {
        foreach (WildcardPattern patternItem in this.exclude)
        {
          if (patternItem.IsMatch(path))
          {
            ok = false;
            break;
          }
        }
      }

      return ok;
    } //MeetsIncludeExcludeCriteria
    #endregion Private Methods

  }// class SelectStringCommand

  #endregion SelectStringCommand

  #region MatchInfo

  /// <summary>
  /// Class representing the result of a pattern/literal match
  /// that is passed through the pipeline by the Select-Str cmdlet.
  /// </summary>
  public class MatchInfo
  {
    /// <summary>
    /// Indicates if the match was done ignoring case.
    /// </summary>
    /// <value>True if case was ignored.</value>
    public bool IgnoreCase
    {
      get { return ignoreCase; }
      set { ignoreCase = value; }
    }
    private bool ignoreCase;

    /// <summary>
    /// Specifies the number of the matching line.
    /// </summary>
    /// <value>The number of the matching line.</value>
    public UInt64 LineNumber
    {
      get { return lineNumber; }
      set { lineNumber = value; }
    }
    private UInt64 lineNumber;

    /// <summary>
    /// Specifies the text of the matching line.
    /// </summary>
    /// <value>The text of the matching line.</value>
    public string Line
    {
      get { return line; }
      set { line = value; }
    }
    private string line;

    /// <summary>
    /// Specifies the full path of the object(file) containing the
    /// matching line.
    /// </summary>
    /// <remarks>
    /// It will be "inputStream" if the object came from the input
    /// stream.
    /// </remarks>
    /// <value>The path name</value>
    public string Path
    {
      get { return path; }
      set
      {
        pathSet = true;
        path = value;
      }
    }
    private string path;
    private bool pathSet;

    /// <summary>
    /// Specifies the pattern that was used in the match.
    /// </summary>
    /// <value>The pattern string</value>
    public string Pattern
    {
      get { return pattern; }
      set { pattern = value; }
    }
    private string pattern;

    private const string MatchFormat = "{0}:{1}:{2}";

    /// <summary>
    /// Returns the string representation of this object. The format
    /// depends on whether a path has been set for this object or
    /// not.
    /// </summary>
    /// <remarks>
    /// If the path component is set, as would be the case when
    /// matching in a file, ToString() returns the path, line
    /// number and line text.  If path is not set, then just the
    /// line text is presented.
    /// </remarks>
    /// <returns>The string representation of the match object.</returns>
    public override string ToString()
    {
      if (pathSet)
         return String.Format(
         System.Threading.Thread.CurrentThread.CurrentCulture,
         MatchFormat,
         this.path,
         this.lineNumber,
         this.line
         );
      else
         return this.line;
    }
  }// End class MatchInfo

  #endregion

  #region PowerShell snap-in

  /// <summary>
  /// Create a PowerShell snap-in for the Select-Str cmdlet.
  /// </summary>
  [RunInstaller(true)]
  public class SelectStringPSSnapIn : PSSnapIn
  {
    /// <summary>
    /// Create an instance of the SelectStrPSSnapin class.
    /// </summary>
    public SelectStringPSSnapIn()
           : base()
    {
    }

    /// <summary>
    /// Specify the name of the PowerShell snap-in.
    /// </summary>
    public override string Name
    {
      get
      {
        return "SelectStrPSSnapIn";
      }
    }

    /// <summary>
    /// Specify the vendor of the PowerShell snap-in.
    /// </summary>
    public override string Vendor
    {
      get
      {
        return "Microsoft";
      }
    }

    /// <summary>
    /// Specify the localization resource information for the vendor.
    /// Use the format: SnapinName,VendorName.
    /// </summary>
    public override string VendorResource
    {
      get
      {
        return "SelectStrSnapIn,Microsoft";
      }
    }

    /// <summary>
    /// Specify the description of the PowerShell snap-in.
    /// </summary>
    public override string Description
    {
      get
        {
          return "This is a PowerShell snap-in for the Select-Str cmdlet.";
        }
    }

    /// <summary>
    /// Specify the localization resource information for the description.
    /// Use the format: SnapinName,Description.

    /// </summary>
    public override string DescriptionResource
    {
      get
      {
          return "SelectStrSnapIn,This is a PowerShell snap-in for the Select-Str cmdlet.";
      }
    }
  }
  #endregion PowerShell snap-in

} //namespace Microsoft.Samples.PowerShell.Commands;
```

## <a name="building-the-cmdlet"></a>A parancsmag felépítése

A parancsmag implementálása után regisztrálnia kell a Windows PowerShell-lel egy Windows PowerShell beépülő modullal. A parancsmagok regisztrálásával kapcsolatos további információkért lásd: [parancsmagok, szolgáltatók és gazdagép-alkalmazások regisztrálása](/previous-versions//ms714644(v=vs.85)).

## <a name="testing-the-cmdlet"></a>A parancsmag tesztelése

Ha a parancsmag regisztrálva van a Windows PowerShellben, tesztelheti azt a parancssorban futtatva. A következő eljárással ellenőrizheti a minta Select-Str parancsmagot.

1. Indítsa el a Windows PowerShellt, és keresse meg a megjegyzések fájlt a ".NET" kifejezéssel rendelkező sorok előfordulásainak kereséséhez. Vegye figyelembe, hogy az útvonal neve körüli idézőjelek csak akkor szükségesek, ha az elérési út egynél több szóból áll.

    ```powershell
    select-str -Path "notes" -Pattern ".NET" -SimpleMatch=$false
    ```

    A következő kimenet jelenik meg.

    ```output
    IgnoreCase   : True
    LineNumber   : 8
    Line         : Because Windows PowerShell works directly with .NET objects, there is often a .NET object
    Path         : C:\PowerShell-Progs\workspace\Samples\SelectStr\notes
    Pattern      : .NET
    IgnoreCase   : True
    LineNumber   : 21
    Line         : You should normally define the class for a cmdlet in a .NET namespace
    Path         : C:\PowerShell-Progs\workspace\Samples\SelectStr\notes
    Pattern      : .NET
    ```

2. Keresse meg a megjegyzések fájljában a "over" szót tartalmazó sorok előfordulásait, majd a többi szöveget. A `SimpleMatch` paraméter az alapértelmezett `false`értéket használja. A keresés megkülönbözteti a kis-és `CaseSensitive` `false`nagybetűket, mert a paraméter értéke a következő:.

    ```powershell
    select-str -Path notes -Pattern "over*" -SimpleMatch -CaseSensitive:$false
    ```

    A következő kimenet jelenik meg.

    ```output
    IgnoreCase   : True
    LineNumber   : 45
    Line         : Override StopProcessing
    Path         : C:\PowerShell-Progs\workspace\Samples\SelectStr\notes
    Pattern      : over*
    IgnoreCase   : True
    LineNumber   : 49
    Line         : overriding the StopProcessing method
    Path         : C:\PowerShell-Progs\workspace\Samples\SelectStr\notes
    Pattern      : over*
    ```

3. A Notes-fájlban reguláris kifejezéssel keresheti meg a mintát. A parancsmag a betűket és az üres szóközöket keresi zárójelek közé.

    ```powershell
    select-str -Path notes -Pattern "\([A-Za-z:blank:]" -SimpleMatch:$false
    ```

    A következő kimenet jelenik meg.

    ```output
    IgnoreCase   : True
    LineNumber   : 1
    Line         : Advisory Guidelines (Consider Following)
    Path         : C:\PowerShell-Progs\workspace\Samples\SelectStr\notes
    Pattern      : \([A-Za-z:blank:]
    IgnoreCase   : True
    LineNumber   : 53
    Line         : If your cmdlet has objects that are not disposed of (written to the pipeline)
    Path         : C:\PowerShell-Progs\workspace\Samples\SelectStr\notes
    Pattern      : \([A-Za-z:blank:]
    ```

4. A megjegyzések fájljának kis-és nagybetűket megkülönböztető keresését hajtsa végre a "paraméter" szó előfordulása esetén.

    ```powershell
    select-str -Path notes -Pattern Parameter -CaseSensitive
    ```

    A következő kimenet jelenik meg.

    ```output
    IgnoreCase   : False
    LineNumber   : 6
    Line         : Support an InputObject Parameter
    Path         : C:\PowerShell-Progs\workspace\Samples\SelectStr\notes
    Pattern      : Parameter
    IgnoreCase   : False
    LineNumber   : 30
    Line         : Support Force Parameter
    Path         : C:\PowerShell-Progs\workspace\Samples\SelectStr\notes
    Pattern      : Parameter
    ```

5. A 0 és 9 közötti numerikus értékkel rendelkező változóknál keresse meg a Windows PowerShell által szállított változót.

    ```powershell
    select-str -Path * -Pattern "[0-9]"
    ```

    A következő kimenet jelenik meg.

    ```output
    IgnoreCase   : True
    LineNumber   : 1
    Line         : 64
    Path         : Variable:\MaximumHistoryCount
    Pattern      : [0-9]
    ```

6. Egy parancsfájl-blokk használatával keresse meg a "POS" karakterlánc SelectStrCommandSample.cs. A parancsfájl **cmatch** funkciója kis-és nagybetűket nem megkülönböztető mintázatot hajt végre.

    ```powershell
    select-str -Path "SelectStrCommandSample.cs" -Script { if ($args[0] -cmatch "Pos"){ return $true } return $false }
    ```

    A következő kimenet jelenik meg.

    ```output
    IgnoreCase   : True
    LineNumber   : 37
    Line         :    Position = 0.
    Path         : C:\PowerShell-Progs\workspace\Samples\SelectStr\SelectStrCommandSample.cs
    Pattern      :
    ```

## <a name="see-also"></a>Lásd még:

[Windows PowerShell-parancsmag létrehozása](/powershell/developer/cmdlet/writing-a-windows-powershell-cmdlet)

[Az első parancsmag létrehozása](./creating-a-cmdlet-without-parameters.md)

[A rendszer módosítását módosító parancsmag létrehozása](./creating-a-cmdlet-that-modifies-the-system.md)

[A Windows PowerShell-szolgáltató megtervezése](../prog-guide/designing-your-windows-powershell-provider.md)

[A Windows PowerShell működése](/previous-versions//ms714658(v=vs.85))

[Parancsmagok, szolgáltatók és gazdagép-alkalmazások regisztrálása](/previous-versions//ms714644(v=vs.85))

[Windows PowerShell SDK](../windows-powershell-reference.md)
