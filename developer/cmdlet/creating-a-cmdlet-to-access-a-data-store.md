---
title: A parancsmag egy Data Store eléréséhez létrehozása |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ea15e00e-20dc-4209-9e97-9ffd763e5d97
caps.latest.revision: 8
ms.openlocfilehash: 8d7ba9d122e90b80f6009b6dc8e8e3bb07331e4a
ms.sourcegitcommit: 01b81317029b28dd9b61d167045fd31f1ec7bc06
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2019
ms.locfileid: "65854856"
---
# <a name="creating-a-cmdlet-to-access-a-data-store"></a>Parancsmag létrehozása adattár eléréséhez

Ez a szakasz ismerteti, hogyan hozhat létre olyan parancsmagot, amely hozzáfér a tárolt adatokat, de a Windows PowerShell-szolgáltatóban. Az ilyen típusú parancsmagot használja a Windows PowerShell-modul a Windows PowerShell szolgáltató infrastruktúra, és ezért a parancsmag osztályból kell származnia a [System.Management.Automation.PSCmdlet](/dotnet/api/System.Management.Automation.PSCmdlet) alaposztály.

A Select-Str parancsmag, az itt leírtak szerint is keresse meg és válassza ki a karakterláncok egy fájl vagy az objektum. A karakterlánc azonosításához használt minták keresztül explicit módon adható meg a `Path` paramétert a parancsmag vagy implicit módon keresztül a `Script` paraméter.

A parancsmag úgy tervezték, hogy bármely Windows PowerShell-szolgáltatóval származó [System.Management.Automation.Provider.Icontentcmdletprovider](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider). A parancsmag megadhatja például, a fájlrendszer-szolgáltatót, vagy a Windows PowerShell által biztosított változó szolgáltató. További információk aboutWindows PowerShell-szolgáltatók, lásd: [tervezése a Windows PowerShell-szolgáltatóban](../prog-guide/designing-your-windows-powershell-provider.md).

## <a name="defining-the-cmdlet-class"></a>A parancsmag osztály meghatározása

Mindig a parancsmag elnevezési és a .NET-osztály, amely megvalósítja a parancsmag deklaráló parancsmag létrehozásának első lépése. Ez a parancsmag észleli a "Kiválasztás", tehát a művelet nevét itt választott által meghatározott egyes karakterláncok a [System.Management.Automation.Verbscommon](/dotnet/api/System.Management.Automation.VerbsCommon) osztály. A főnév neve "Str" használata a parancsmag közvetítőtől karakterláncokat. Az alábbi nyilatkozatot jegyezze fel, hogy a parancsmag ige és főnév neve jelennek-e be a parancsmag az osztály nevét. A parancsmag jóváhagyott igék kapcsolatos további információkért lásd: [művelet neve](./approved-verbs-for-windows-powershell-commands.md).

Ez a parancsmag a .NET-osztály származhat a [System.Management.Automation.PSCmdlet](/dotnet/api/System.Management.Automation.PSCmdlet) alaposztály, mert a Windows PowerShell-modul által közzé kellett tenni a Windows PowerShell-szolgáltató támogatja infrastruktúra. Vegye figyelembe, hogy ez a parancsmag emellett lehetővé teszi például használja a .NET-keretrendszer reguláris kifejezések osztályok [System.Text.Regularexpressions.Regex](/dotnet/api/System.Text.RegularExpressions.Regex).

A következő kódot a Select-Str parancsmag osztálydefiníció.

```csharp
[Cmdlet(VerbsCommon.Select, "Str", DefaultParameterSetName="PatternParameterSet")]
public class SelectStringCommand : PSCmdlet
```

Ez a parancsmag határozza meg az alapértelmezett paraméterek hozzáadásával állítsa be a `DefaultParameterSetName` az osztálydeklaráció kulcsszó attribútumot. Az alapértelmezett paraméterkészletet `PatternParameterSet` mikor szolgál a `Script` paraméter nincs megadva. Ez a paraméter beállítása kapcsolatos további információkért lásd: a `Pattern` és `Script` paraméter vitafórum a következő szakaszban.

## <a name="defining-parameters-for-data-access"></a>Az adatok eléréséhez a paraméterek megadása

Ez a parancsmag, amely engedélyezi a felhasználó elérheti, és vizsgálja meg a tárolt adatok számos paraméter határozza meg. Ezek a paraméterek közé tartozik egy `Path` paraméter, amely azt jelzi, hogy a hely az adattár egy `Pattern` paraméter, amely a mintát használni a Keresés és számos más paramétereket, amelyek támogatják a hogyan megy végbe a keresést.

> [!NOTE]
> A paraméterek meghatározása az alapokat kapcsolatos további információkért lásd: [a folyamat parancssori bemenet-paramétereket adunk hozzá](./adding-parameters-that-process-command-line-input.md).

### <a name="declaring-the-path-parameter"></a>Az elérési út paraméter deklaráló

Keresse meg az adattár, ezt a parancsmagot kell használnia a egy Windows PowerShell-elérési út azonosíthatja a Windows PowerShell-szolgáltatóban, amelyek célja, hogy az adattár eléréséhez. Azt határozza meg, ezért egy `Path` paraméterében helyének megadására a szolgáltató típusú karakterlánc-tömbben.

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

Vegye figyelembe, hogy ez a paraméter két különböző paraméterkészlettel tartozik, és arról, hogy vannak-e egy aliast.

Két [System.Management.Automation.Parameterattribute](/dotnet/api/System.Management.Automation.ParameterAttribute) attribútumok deklarálja, hogy a `Path` paraméter tartozik a `ScriptParameterSet` és a `PatternParameterSet`. Paraméterkészlettel kapcsolatos további információkért lásd: [hozzáadása paraméterkészletek parancsmag](./adding-parameter-sets-to-a-cmdlet.md).

A [System.Management.Automation.Aliasattribute](/dotnet/api/System.Management.Automation.AliasAttribute) attribútum deklarálja a `PSPath` aliasa a `Path` paraméter. Ezt az aliast deklaráló erősen ajánlott a konzisztencia, a többi parancsmag, amely a Windows PowerShell-szolgáltató elérésére. További információk aboutWindows PowerShell elérési utak, lásd: "PowerShell-elérési út fogalmak" a [Windows PowerShell működése](https://msdn.microsoft.com/en-us/ced30e23-10af-4700-8933-49873bd84d58).

### <a name="declaring-the-pattern-parameter"></a>A minta paraméterét deklaráló

Annak megadásához, keresse meg a mintákat, ez a parancsmag deklarálja a `Pattern` paraméter, amely egy karakterláncokból álló tömbre van. Egy pozitív eredményt adja vissza, ha bármelyik mintát az adattárban találhatók. Vegye figyelembe, hogy ezek a minták állíthatók össze egy tömböt a lefordított reguláris kifejezéseket, vagy helyettesítő mintákat a konstans-keresésekhez tömbjét.

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

Ha ez a paraméter meg van adva, a parancsmag használja az alapértelmezett paraméterkészletet `PatternParameterSet`. Ebben az esetben a parancsmagot használja, a karakterláncok jelölje be az itt megadott minták. Ezzel szemben a `Script` paraméter is használható, adja meg a mintákat tartalmazó parancsfájl. A `Script` és `Pattern` paraméterek megadása két külön paraméterkészlettel, így ezek kölcsönösen kizárják egymást.

### <a name="declaring-search-support-parameters"></a>Jelentést készítő keresési támogatási paraméterek

Ez a parancsmag a következő támogatási paramétereket, hogy módosítsa a keresési funkciókat, a parancsmag segítségével határozza meg.

A `Script` paraméter adja meg a parancsmag egy másik keresési mechanizmust biztosít használható parancsprogram-blokkot. A parancsfájl kell tartalmaznia a megfelelő használt minták, és adja vissza egy [System.Management.Automation.PSObject](/dotnet/api/System.Management.Automation.PSObject) objektum. Vegye figyelembe, hogy ezt a paramétert is az egyedi paraméter, amely azonosítja a `ScriptParameterSet` paraméterkészletet. Amikor a Windows PowerShell-modul látja ezt a paramétert, akkor használja, csak a tartoznak paraméterek a `ScriptParameterSet` paraméterkészletet.

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

A `SimpleMatch` egy kapcsoló paraméter, amely azt jelzi, hogy a parancsmag az explicit módon felel meg a mintákat, ezek végzik. Amikor a felhasználó adja meg a paraméter a parancssorban (`true`), a parancsmag használja a mintákat, ezek végzik. Ha a paraméter nincs megadva (`false`), a parancsmag reguláris kifejezéseket használ. Ez a paraméter alapértelmezett értéke `false`.

```csharp
[Parameter]
public SwitchParameter SimpleMatch
{
  get { return simpleMatch; }
  set { simpleMatch = value; }
}
private bool simpleMatch;
```

A `CaseSensitive` egy kapcsoló paraméter, amely azt jelzi, hogy történik-e a kis-és nagybetűket keresési. Amikor a felhasználó adja meg a paraméter a parancssorban (`true`), a parancsmag ellenőrzi a nagybetűs és kisbetűs karakterek összehasonlításakor mintáit. Ha a paraméter nincs megadva (`false`), a parancsmag nem tesz különbséget a kis- és nagybetűk között. Például "MyFile" és "myfile" mindkettő rendszer visszaadna, pozitív találatok. Ez a paraméter alapértelmezett értéke `false`.

```csharp
[Parameter]
public SwitchParameter CaseSensitive
{
  get { return caseSensitive; }
  set { caseSensitive = value; }
}
private bool caseSensitive;
```

A `Exclude` és `Include` paraméterek azonosítják, amelyek kifejezetten zárva vagy a keresés szereplő elemek. Alapértelmezés szerint a parancsmag fog minden elem szerepel az adattárban. Azonban korlátozhatja a keresést, a parancsmag által végrehajtott, ezeket a paramétereket lehet explicit módon jelezni a keresés foglalandó elemek vagy nincs megadva.

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

### <a name="declaring-parameter-sets"></a>Jelentést készítő paraméterkészlettel

Ez a parancsmag két paraméterkészlettel használ (`ScriptParameterSet` és `PatternParameterSet`, az alapértelmezett), az adatok elérésére használt két paraméterkészlettel nevei. `PatternParameterSet` az alapértelmezett paraméterkészletet, és ha használható a `Pattern` paraméter meg van adva. `ScriptParameterSet` használatos, amikor a felhasználó egy másik keresési mechanizmussal adja meg a `Script` paraméter. Paraméterkészlettel kapcsolatos további információkért lásd: [hozzáadása paraméterkészletek parancsmag](./adding-parameter-sets-to-a-cmdlet.md).

## <a name="overriding-input-processing-methods"></a>Bemeneti feldolgozási módszerek felülbírálása

Parancsmagok egy vagy több módszert feldolgozása a bemeneti felül kell írnia a [System.Management.Automation.PSCmdlet](/dotnet/api/System.Management.Automation.PSCmdlet) osztály. A bemeneti feldolgozási módszerekkel kapcsolatos további információkért lásd: [létrehozásához az első parancsmag](./creating-a-cmdlet-without-parameters.md).

Ez a parancsmag felülbírálja a [System.Management.Automation.Cmdlet.BeginProcessing](/dotnet/api/System.Management.Automation.Cmdlet.BeginProcessing) hozhat létre egy tömbjét metódus lefordított indításkor reguláris kifejezéseket. Ez növeli a teljesítményt, hogy ne használjon egyszerű megfelelő keresések során.

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

Ez a parancsmag emellett felülbírálja a [System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) metódus feldolgozása a karakterlánc-beállításokat a felhasználó által a parancssoron. Karakterlánc kijelölés eredményét egy egyéni objektum formájában privát meghívásával ír **MatchString** metódust.

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

A parancsmag meg kell nyitnia a szolgáltató, a Windows PowerShell-elérési útját jelzi, hogy hozzá tudjon férni az adatokat. A [System.Management.Automation.Sessionstate](/dotnet/api/System.Management.Automation.SessionState) objektum esetében a Providert a futási teret használ, miközben a [System.Management.Automation.PSCmdlet.Invokeprovider*](/dotnet/api/System.Management.Automation.PSCmdlet.InvokeProvider) tulajdonságát a a parancsmag segítségével nyissa meg a szolgáltatót. Az adatszolgáltató által biztosított tartalmakhoz való hozzáférést a [System.Management.Automation.Providerintrinsics](/dotnet/api/System.Management.Automation.ProviderIntrinsics) megnyitni a szolgáltató objektumot.

Ez a minta kiválasztása – Str parancsmag használja a [System.Management.Automation.Providerintrinsics.Content*](/dotnet/api/System.Management.Automation.ProviderIntrinsics.Content) megvizsgálja a tartalom elérhetővé tulajdonság. Ezt követően meghívhatja a [System.Management.Automation.Contentcmdletproviderintrinsics.Getreader*](/dotnet/api/System.Management.Automation.ContentCmdletProviderIntrinsics.GetReader) módszer, átadja a szükséges Windows PowerShell-útvonal.

## <a name="code-sample"></a>Kódminta

A következő kód bemutatja ennek a verziónak a kiválasztása – Str parancsmag végrehajtására. Vegye figyelembe, hogy ez a kód tartalmazza a parancsmag osztály, a parancsmag által használt titkos módszerek és a Windows PowerShell beépülő modul kódot a parancsmag regisztrálásához használt. A parancsmag nyilvántartására vonatkozó további információkért lásd: [létrehozásához a parancsmag](#building-the-cmdlet).

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

## <a name="building-the-cmdlet"></a>A parancsmag készítése

Parancsmag-k megvalósítása után regisztrálnia kell azt a Windows PowerShell-lel a Windows PowerShell beépülő modullal. Parancsmagok regisztrálásával kapcsolatos további információkért lásd: [parancsmagjainak regisztrálásához, a szolgáltatók és az alkalmazások üzemeltetése hogyan](https://msdn.microsoft.com/en-us/a41e9054-29c8-40ab-bf2b-8ce4e7ec1c8c).

## <a name="testing-the-cmdlet"></a>A parancsmag tesztelése

Ha a parancsmagot a Windows PowerShell-lel regisztrálva lett, azt a parancssorból való futtatásával tesztelheti. A következő eljárás használható a Select-Str parancsmagra teszteléséhez.

1. Indítsa el a Windows Powershellt, és keresse meg a ".NET" kifejezést tartalmazó sorok előfordulását a megjegyzések fájlban. Vegye figyelembe, hogy az elérési út nevét tegye idézőjelbe szükségesek, csak akkor, ha az elérési út egynél több szóból áll.

    ```powershell
    select-str -Path "notes" -Pattern ".NET" -SimpleMatch=$false
    ```

    A következő eredmény jelenik meg.

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

2. Keresse meg a megjegyzések fájlban szót tartalmazó sorok előfordulását "keresztül", bármely más szöveg követ. A `SimpleMatch` paraméter alapértelmezett értékét használja `false`. A keresés megkülönbözteti a kis-és mivel a `CaseSensitive` paraméter értéke `false`.

    ```powershell
    select-str -Path notes -Pattern "over*" -SimpleMatch -CaseSensitive:$false
    ```

    A következő eredmény jelenik meg.

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

3. Keresse meg a megjegyzések fájlban, a minta egy reguláris kifejezést használ. A parancsmag rákeres a alfabetikus karaktereket és szóközöket zárójelek között.

    ```powershell
    select-str -Path notes -Pattern "\([A-Za-z:blank:]" -SimpleMatch:$false
    ```

    A következő eredmény jelenik meg.

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

4. A megjegyzések fájl kis-és nagybetűket keresést végrehajtani az előfordulások "Paraméter" szó.

    ```powershell
    select-str -Path notes -Pattern Parameter -CaseSensitive
    ```

    A következő eredmény jelenik meg.

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

5. Keresés a változó szolgáltató Önnek a Windows PowerShell-lel változók, amelyek rendelkeznek a 0 – 9 numerikus értékeket.

    ```powershell
    select-str -Path * -Pattern "[0-9]"
    ```

    A következő eredmény jelenik meg.

    ```output
    IgnoreCase   : True
    LineNumber   : 1
    Line         : 64
    Path         : Variable:\MaximumHistoryCount
    Pattern      : [0-9]
    ```

6. Parancsprogram-blokkot használatával keresse meg a fájlban SelectStrCommandSample.cs "Pos" karakterláncnak. A **cmatch** függvény esetében a szkript hajt végre egy kis-és névminta egyeztetésével.

    ```powershell
    select-str -Path "SelectStrCommandSample.cs" -Script { if ($args[0] -cmatch "Pos"){ return $true } return $false }
    ```

    A következő eredmény jelenik meg.

    ```output
    IgnoreCase   : True
    LineNumber   : 37
    Line         :    Position = 0.
    Path         : C:\PowerShell-Progs\workspace\Samples\SelectStr\SelectStrCommandSample.cs
    Pattern      :
    ```

## <a name="see-also"></a>Lásd még:

[Hogyan hozhat létre egy Windows PowerShell-parancsmag](https://msdn.microsoft.com/en-us/0d721742-c849-4d0d-964f-78ddd9cd258c)

[Az első parancsmag létrehozása](./creating-a-cmdlet-without-parameters.md)

[A parancsmag létrehozása, amely módosítja a rendszer](./creating-a-cmdlet-that-modifies-the-system.md)

[A Windows PowerShell-szolgáltató tervezése](../prog-guide/designing-your-windows-powershell-provider.md)

[Hogyan működik a Windows PowerShell](https://msdn.microsoft.com/en-us/ced30e23-10af-4700-8933-49873bd84d58)

[How to Register parancsmagok, a szolgáltatók és az alkalmazások üzemeltetéséhez](https://msdn.microsoft.com/en-us/a41e9054-29c8-40ab-bf2b-8ce4e7ec1c8c)

[Windows PowerShell SDK](../windows-powershell-reference.md)
