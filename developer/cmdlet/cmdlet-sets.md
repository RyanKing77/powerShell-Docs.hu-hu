---
title: A parancsmag csoportok |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: bcf0739e-920e-4dd8-afca-2c6d6927bc2a
caps.latest.revision: 10
ms.openlocfilehash: e9c59474b7e2bbc07166df8a8b4fa8099edd360f
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56849048"
---
# <a name="cmdlet-sets"></a><span data-ttu-id="04e7e-102">Parancsmagkészletek</span><span class="sxs-lookup"><span data-stu-id="04e7e-102">Cmdlet Sets</span></span>

<span data-ttu-id="04e7e-103">A parancsmagok tervezésekor esetekben kell bizonyos műveletek végrehajtását az adott adatok a merülhetnek fel.</span><span class="sxs-lookup"><span data-stu-id="04e7e-103">When you design your cmdlets, you might encounter cases in which you need to perform several actions on the same piece of data.</span></span> <span data-ttu-id="04e7e-104">Szüksége lehet például beolvasása és adatok vagy elindításához és a folyamat leállítása.</span><span class="sxs-lookup"><span data-stu-id="04e7e-104">For example, you might need to get and set data or start and stop a process.</span></span> <span data-ttu-id="04e7e-105">Annak ellenére, hozhat létre külön parancsmagok minden művelet végrehajtására, a parancsmag megtervezésekor osztály, amely az egyes parancsmagok osztályok származnak.</span><span class="sxs-lookup"><span data-stu-id="04e7e-105">Although you will need to create separate cmdlets to perform each action, your cmdlet design should include a base class from which the classes for the individual cmdlets are derived.</span></span>

<span data-ttu-id="04e7e-106">Vegye figyelembe az alábbiakat, osztály végrehajtása során.</span><span class="sxs-lookup"><span data-stu-id="04e7e-106">Keep the following things in mind when implementing a base class.</span></span>

- <span data-ttu-id="04e7e-107">Deklarálja a származtatott parancsmagok az alaposztályban által használt bármilyen általános paramétert.</span><span class="sxs-lookup"><span data-stu-id="04e7e-107">Declare any common parameters used by all the derived cmdlets in the base class.</span></span>

- <span data-ttu-id="04e7e-108">Parancsmag-specifikus paramétereket adhat hozzá a megfelelő parancsmag osztályhoz.</span><span class="sxs-lookup"><span data-stu-id="04e7e-108">Add cmdlet-specific parameters to the appropriate cmdlet class.</span></span>

- <span data-ttu-id="04e7e-109">Bírálja felül a megfelelő bemeneti metódus az alaposztály feldolgozása.</span><span class="sxs-lookup"><span data-stu-id="04e7e-109">Override the appropriate input processing method in the base class.</span></span>

- <span data-ttu-id="04e7e-110">Deklarálja a [System.Management.Automation.Cmdletattribute](/dotnet/api/System.Management.Automation.CmdletAttribute) lévő összes parancsmag osztály attribútumot, de nem deklarálja a az alaposztály alaposztályát.</span><span class="sxs-lookup"><span data-stu-id="04e7e-110">Declare the [System.Management.Automation.Cmdletattribute](/dotnet/api/System.Management.Automation.CmdletAttribute) attribute on all cmdlet classes, but do not declare it on the base class.</span></span>

- <span data-ttu-id="04e7e-111">Alkalmazzon egy [System.Management.Automation.Pssnapin](/dotnet/api/System.Management.Automation.PSSnapIn) vagy [System.Management.Automation.Custompssnapin](/dotnet/api/System.Management.Automation.CustomPSSnapIn) osztályt, amelynek a neve és leírása parancsmagok készletét tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="04e7e-111">Implement a [System.Management.Automation.Pssnapin](/dotnet/api/System.Management.Automation.PSSnapIn) or [System.Management.Automation.Custompssnapin](/dotnet/api/System.Management.Automation.CustomPSSnapIn) class whose name and description reflects the set of cmdlets.</span></span>

## <a name="example"></a><span data-ttu-id="04e7e-112">Példa</span><span class="sxs-lookup"><span data-stu-id="04e7e-112">Example</span></span>

<span data-ttu-id="04e7e-113">Az alábbi példa egy alaposztály, amelyet a Get-Proc és Stop-Proc parancsmag alaposztályból származik az azonos megvalósítását mutatja be.</span><span class="sxs-lookup"><span data-stu-id="04e7e-113">The following example shows the implementation of a base class that is used by Get-Proc and Stop-Proc cmdlet that derive from the same base class.</span></span>

```csharp
using System;
using System.Diagnostics;
using System.Management.Automation;             //Windows PowerShell namespace.

namespace Microsoft.Samples.PowerShell.Commands
{

  #region ProccessCommands

  /// <summary>
  /// This class implements a Stop-Proc cmdlet. The parameters
  /// for this cmdlet are defined by the BaseProcCommand class.
  /// </summary>
  [Cmdlet(VerbsLifecycle.Stop, "Proc", SupportsShouldProcess = true)]
  public class StopProcCommand : BaseProcCommand
  {
    public override void ProcessObject(Process process)
    {
      if (ShouldProcess(process.ProcessName, "Stop-Proc"))
      {
        process.Kill();
      }
    }
  }

  /// <summary>
  /// This class implements a Get-Proc cmdlet. The parameters
  /// for this cmdlet are defined by the BaseProcCommand class.
  /// </summary>

  [Cmdlet(VerbsCommon.Get, "Proc")]
  public class GetProcCommand : BaseProcCommand
  {
    public override void ProcessObject(Process process)
    {
      WriteObject(process);
    }
  }

  /// <summary>
  /// This class is the base class that defines the common
  /// functionality used by the Get-Proc and Stop-Proc
  /// cmdlets.
  /// </summary>
  public class BaseProcCommand : Cmdlet
  {
    #region Parameters

    // Defines the Name parameter that is used to
    // specify a process by its name.
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

    // Defines the Exclude parameter that is used to
    // specify which processes should be excluded when
    // the cmdlet performs its action.
    [Parameter()]
    public string[] Exclude
    {
      get { return excludeNames; }
      set { excludeNames = value; }
    }
    private string[] excludeNames = new string[0];
    #endregion Parameters

    public virtual void ProcessObject(Process process)
    {
      throw new NotImplementedException("This method should be overridden.");
    }

    #region Cmdlet Overrides
    // <summary>
    // For each of the requested process names, retrieve and write
    // the associated processes.
    // </summary>
    protected override void ProcessRecord()
    {
      // Set up the wildcard chracters used in resolving
      // the process names.
      WildcardOptions options = WildcardOptions.IgnoreCase |
                                WildcardOptions.Compiled;

      WildcardPattern[] include = new WildcardPattern[Name.Length];
      for (int i = 0; i < Name.Length; i++)
      {
        include[i] = new WildcardPattern(Name[i], options);
      }

      WildcardPattern[] exclude = new WildcardPattern[Exclude.Length];
      for (int i = 0; i < Exclude.Length; i++)
      {
        exclude[i] = new WildcardPattern(Exclude[i], options);
      }

      foreach (Process p in Process.GetProcesses())
      {
        foreach (WildcardPattern wIn in include)
        {
          if (wIn.IsMatch(p.ProcessName))
          {
            bool processThisOne = true;
            foreach (WildcardPattern wOut in exclude)
            {
              if (wOut.IsMatch(p.ProcessName))
              {
                processThisOne = false;
                break;
              }
            }
            if (processThisOne)
            {
              ProcessObject(p);
            }
            break;
          }
        }
      }
    }
    #endregion Cmdlet Overrides
  }
    #endregion ProcessCommands
}
```

## <a name="see-also"></a><span data-ttu-id="04e7e-114">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="04e7e-114">See Also</span></span>

[<span data-ttu-id="04e7e-115">Egy Windows PowerShell-parancsmag írása</span><span class="sxs-lookup"><span data-stu-id="04e7e-115">Writing a Windows PowerShell Cmdlet</span></span>](./writing-a-windows-powershell-cmdlet.md)
