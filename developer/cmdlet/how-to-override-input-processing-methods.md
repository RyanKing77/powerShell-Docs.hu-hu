---
title: Bemeneti feldolgozási módszerek felülbírálása |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 1a1ad921-5816-4937-acf1-ed4760fae740
caps.latest.revision: 8
ms.openlocfilehash: cfee55576518cf9ce38501192872ce94054f5213
ms.sourcegitcommit: caac7d098a448232304c9d6728e7340ec7517a71
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/16/2019
ms.locfileid: "58056396"
---
# <a name="how-to-override-input-processing-methods"></a>Bemeneti feldolgozási módszerek felülbírálása

Ezek a példák bemutatják, hogyan írja felül a bemeneti feldolgozási belül egy parancsmag módszerek. Ezek a módszerek használhatók a következő műveletek végrehajtásához:

- A [System.Management.Automation.Cmdlet.BeginProcessing](/dotnet/api/System.Management.Automation.Cmdlet.BeginProcessing) módszert az összes olyan objektum, a parancsmag által feldolgozott érvényes egyszeri indítási műveletek végrehajtásához. A Windows PowerShell-modul csak egyszer meghívja ezt a metódust.

- A [System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) metódus az objektumot a parancsmagnak átadott feldolgozására szolgál. A Windows PowerShell-modul minden egyes objektumot a parancsmagnak átadott ezt a módszert igényel.

- A [System.Management.Automation.Cmdlet.EndProcessing](/dotnet/api/System.Management.Automation.Cmdlet.EndProcessing) metódus egyszeri utáni feldolgozási műveletek végrehajtására szolgál. A Windows PowerShell-modul csak egyszer meghívja ezt a metódust.

## <a name="to-override-the-beginprocessing-method"></a>A BeginProcessing metódus felülbírálására

- Egy védett felülbírálását deklarálja a [System.Management.Automation.Cmdlet.BeginProcessing](/dotnet/api/System.Management.Automation.Cmdlet.BeginProcessing) metódust.

A következő osztály egy minta üzenetet jelenít meg. Szeretné használni ezt az osztályt, módosítsa a ige és főnév, a parancsmag attribútum, módosítsa a nevet, hogy tükrözzék az új ige és főnév az osztály és majd a felülbírálást, adja hozzá a funkciókra van szüksége a [System.Management.Automation.Cmdlet.BeginProcessing ](/dotnet/api/System.Management.Automation.Cmdlet.BeginProcessing) metódust.

```csharp
[Cmdlet(VerbsDiagnostic.Test, "BeginProcessingClass")]
public class TestBeginProcessingClassTemplate : Cmdlet
{
  // Override the BeginProcessing method to add preprocessing
  //operations to the cmdlet.
  protected override void BeginProcessing()
  {
    // Replace the WriteObject method with the logic required
    // by your cmdlet. It is used here to generate the following
    // output:
    // "This is a test of the BeginProcessing template."
    WriteObject("This is a test of the BeginProcessing template.");
  }
}
```

## <a name="to-override-the-processrecord-method"></a>A ProcessRecord metódus felülbírálására

- Egy védett felülbírálását deklarálja a [System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) metódust.

A következő osztály egy minta üzenetet jelenít meg. Szeretné használni ezt az osztályt, módosítsa a ige és főnév, a parancsmag attribútum, módosítsa a nevet, hogy tükrözzék az új ige és főnév az osztály és majd a felülbírálást, adja hozzá a funkciókra van szüksége a [System.Management.Automation.Cmdlet.ProcessRecord ](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) metódust.

```csharp
[Cmdlet(VerbsDiagnostic.Test, "ProcessRecordClass")]
public class TestProcessRecordClassTemplate : Cmdlet
{
    // Override the ProcessRecord method to add processing
    //operations to the cmdlet.
    protected override void ProcessRecord()
    {
        // Replace the WriteObject method with the logic required
        // by your cmdlet. It is used here to generate the following
        // output:
        // "This is a test of the ProcessRecord template."
        WriteObject("This is a test of the ProcessRecord template.");
    }
}

```

## <a name="to-override-the-endprocessing-method"></a>A EndProcessing metódus felülbírálására

- Egy védett felülbírálását deklarálja a [System.Management.Automation.Cmdlet.EndProcessing](/dotnet/api/System.Management.Automation.Cmdlet.EndProcessing) metódust.

A következő osztály egy mintát jelenít meg. Szeretné használni ezt az osztályt, módosítsa a ige és főnév, a parancsmag attribútum, módosítsa a nevet, hogy tükrözzék az új ige és főnév az osztály és majd a felülbírálást, adja hozzá a funkciókra van szüksége a [System.Management.Automation.Cmdlet.EndProcessing ](/dotnet/api/System.Management.Automation.Cmdlet.EndProcessing) metódust.

```csharp
[Cmdlet(VerbsDiagnostic.Test, "EndProcessingClass")]
public class TestEndProcessingClassTemplate : Cmdlet
{
  // Override the EndProcessing method to add postprocessing
  //operations to the cmdlet.
  protected override void EndProcessing()
  {
    // Replace the WriteObject method with the logic required
    // by your cmdlet. It is used here to generate the following
    // output:
    // "This is a test of the BeginProcessing template."
    WriteObject("This is a test of the EndProcessing template.");
  }
}
```

## <a name="see-also"></a>Lásd még:

[System.Management.Automation.Cmdlet.BeginProcessing](/dotnet/api/System.Management.Automation.Cmdlet.BeginProcessing)

[System.Management.Automation.Cmdlet.EndProcessing](/dotnet/api/System.Management.Automation.Cmdlet.EndProcessing)

[System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord)

[Egy Windows PowerShell-parancsmag írása](./writing-a-windows-powershell-cmdlet.md)
