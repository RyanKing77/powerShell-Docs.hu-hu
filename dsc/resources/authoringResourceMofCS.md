---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: A DSC-erőforrás a szerzői műveletekC#
ms.openlocfilehash: 6f2bb4d411237f13e2735c2e5f630b4f40dc6842
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62076650"
---
# <a name="authoring-a-dsc-resource-in-c"></a>A DSC-erőforrás C nyelven készítése\#

> A következőkre vonatkozik: Windows PowerShell 4.0-s, a Windows PowerShell 5.0

Általában egy Windows PowerShell Desired State Configuration (DSC) egyéni erőforrás implementálva van a PowerShell-parancsfájlt. Azonban is alkalmazhat a DSC egyéni erőforrás funkcióit, ha a parancsmagokat C#. Parancsmagok írásáról bemutatását C#, lásd: [írása egy Windows PowerShell-parancsmag](/powershell/developer/windows-powershell).

Azokat a kivéve az erőforrásra a végrehajtási C# parancsmagok, mint a folyamat a MOF-séma létrehozása, a gyökérmappa-szerkezetében létrehozása, importálása és az egyéni DSC-erőforrás használatával ugyanazok, mint ismertetett [MOFazegyéniDSC-erőforrásírása](authoringResourceMOF.md).

## <a name="writing-a-cmdlet-based-resource"></a>Parancsmag-alapú-erőforrás írása
Ebben a példában egy egyszerű erőforrás, amely kezeli a szövegfájlba, és annak tartalma lesz megvalósítása.

### <a name="writing-the-mof-schema"></a>A MOF-séma írása

Az alábbiakban látható a MOF erőforrás-definícióban.

```
[ClassVersion("1.0.0"), FriendlyName("xDemoFile")]
class MSFT_XDemoFile : OMI_BaseResource
{
                [Key, Description("path")] String Path;
                [Write, Description("Should the file be present"), ValueMap{"Present","Absent"}, Values{"Present","Absent"}] String Ensure;
                [Write, Description("Contentof file.")] String Content;
};
```

### <a name="setting-up-the-visual-studio-project"></a>A Visual Studio-projekt beállítása
#### <a name="setting-up-a-cmdlet-project"></a>Egy parancsmag-projekt beállítása

1. Nyissa meg a Visual Studióban.
1. Hozzon létre egy C# projektre, és adja meg a nevét.
1. Válassza ki **osztálytár** a projekt rendelkezésre álló sablonok közül.
1. Kattintson a **Ok**.
1. A System.Automation.Management.dll postrádáte odkaz nA sestavení hozzáadása a projekthez.
1. Módosítsa az erőforrás neve megfelelő szerelvény nevét. Ebben az esetben a szerelvény neve lehet **MSFT_XDemoFile**.

### <a name="writing-the-cmdlet-code"></a>A parancsmag kód írása

A következő C# code valósítja meg a **Get-TargetResource**, **Set-TargetResource**, és **Test-TargetResource** parancsmagok.

```C#


namespace cSharpDSCResourceExample
{
    using System;
    using System.Collections.Generic;
    using System.IO;
    using System.Management.Automation;  // Windows PowerShell assembly.

    #region Get-TargetResource

    [OutputType(typeof(System.Collections.Hashtable))]
    [Cmdlet(VerbsCommon.Get, "TargetResource")]
    public class GetTargetResource : PSCmdlet
    {
        [Parameter(Mandatory = true)]
        public string Path { get; set; }

        /// <summary>
        /// Implement the logic to return the current state of the resource as a hashtable with keys being the resource properties
        /// and the values are the corresponding current value on the machine.
        /// </summary>
        protected override void ProcessRecord()
        {
            var currentResourceState = new Dictionary<string, string>();
            if (File.Exists(Path))
            {
                currentResourceState.Add("Ensure", "Present");

                // read current content
                string CurrentContent = "";
                using (var reader = new StreamReader(Path))
                {
                    CurrentContent = reader.ReadToEnd();
                }
                currentResourceState.Add("Content", CurrentContent);
            }
            else
            {
                currentResourceState.Add("Ensure", "Absent");
                currentResourceState.Add("Content", "");
            }
            // write the hashtable in the PS console.
            WriteObject(currentResourceState);
        }
    }

    # endregion

    #region Set-TargetResource
    [OutputType(typeof(void))]
    [Cmdlet(VerbsCommon.Set, "TargetResource")]
    public class SetTargetResource : PSCmdlet
    {
        [Parameter(Mandatory = true)]
        public string Path { get; set; }

        [Parameter(Mandatory = false)]

        [ValidateSet("Present", "Absent", IgnoreCase = true)]
        public string Ensure {
            get
            {
                // set the default to present.
               return (this._ensure ?? "Present") ;
            }
            set
            {
                this._ensure = value;
            }
        }

        [Parameter(Mandatory = false)]
        public string Content {
            get { return (string.IsNullOrEmpty(this._content) ? "" : this._content); }
            set { this._content = value; }
        }

        private string _ensure;
        private string _content;

        /// <summary>
        /// Implement the logic to set the state of the machine to the desired state.
        /// </summary>
        protected override void ProcessRecord()
        {
            WriteVerbose(string.Format("Running set with parameters {0}{1}{2}", Path, Ensure, Content));
            if (File.Exists(Path))
            {
                if (Ensure.Equals("absent", StringComparison.InvariantCultureIgnoreCase))
                {
                    File.Delete(Path);
                }
                else
                {
                    // file already exist and ensure "present" is specified. start writing the content to a file
                    if (!string.IsNullOrEmpty(Content))
                    {
                        string existingContent = null;
                        using (var reader = new StreamReader(Path))
                        {
                            existingContent = reader.ReadToEnd();
                        }
                        // check if the content of the file mathes the content passed
                        if (!existingContent.Equals(Content, StringComparison.InvariantCultureIgnoreCase))
                        {
                            WriteVerbose("Existing content did not match with desired content updating the content of the file");
                            using (var writer = new StreamWriter(Path))
                            {
                                writer.Write(Content);
                                writer.Flush();
                            }
                        }
                    }
                }

            }
            else
            {
                if (Ensure.Equals("present", StringComparison.InvariantCultureIgnoreCase))
                {
                    // if nothing is passed for content just write "" otherwise write the content passed.
                    using (var writer = new StreamWriter(Path))
                    {
                        WriteVerbose(string.Format("Creating a file under path {0} with content {1}", Path, Content));
                        writer.Write(Content);
                    }
                }

            }

            /* if you need to reboot the VM. please add the following two line of code.
            PSVariable DscMachineStatus = new PSVariable("DSCMachineStatus", 1, ScopedItemOptions.AllScope);
            this.SessionState.PSVariable.Set(DscMachineStatus);
             */

        }

    }

    # endregion

    #region Test-TargetResource

    [Cmdlet("Test", "TargetResource")]
    [OutputType(typeof(Boolean))]
    public class TestTargetResource : PSCmdlet
    {
        [Parameter(Mandatory = true)]
        public string Path { get; set; }

        [Parameter(Mandatory = false)]

        [ValidateSet("Present", "Absent", IgnoreCase = true)]
        public string Ensure
        {
            get
            {
                // set the default to present.
                return (this._ensure ?? "Present");
            }
            set
            {
                this._ensure = value;
            }
        }

        [Parameter(Mandatory = false)]
        public string Content
        {
            get { return (string.IsNullOrEmpty(this._content) ? "" : this._content); }
            set { this._content = value; }
        }

        private string _ensure;
        private string _content;

        /// <summary>
        /// Return a boolean value which indicates wheather the current machine is in desired state or not.
        /// </summary>
        protected override void ProcessRecord()
        {
            if (File.Exists(Path))
            {
                if( Ensure.Equals("absent", StringComparison.InvariantCultureIgnoreCase))
                {
                    WriteObject(false);
                }
                else
                {
                    // check if the content matches

                    string existingContent = null;
                    using (var stream = new StreamReader(Path))
                    {
                        existingContent = stream.ReadToEnd();
                    }

                    WriteObject(Content.Equals(existingContent, StringComparison.InvariantCultureIgnoreCase));
                }
            }
            else
            {
                WriteObject(Ensure.Equals("Absent", StringComparison.InvariantCultureIgnoreCase));
            }
        }
    }

    # endregion

}
```

### <a name="deploying-the-resource"></a>Az erőforrás üzembe helyezése

A lefordított dll-fájlt menteni a fájlt a parancsprogramfájlon alapuló erőforrás hasonló struktúrával. Az alábbiakban látható a gyökérmappa-szerkezetében ehhez az erőforráshoz.

```
$env: psmodulepath (folder)
    |- MyDscResources (folder)
        |- MyDscResources.psd1 (file, required)
        |- DSCResources (folder)
            |- MSFT_XDemoFile (folder)
                |- MSFT_XDemoFile.psd1 (file, optional)
                |- MSFT_XDemoFile.dll (file, required)
                |- MSFT_XDemoFile.schema.mof (file, required)
```

### <a name="see-also"></a>Lásd még:
#### <a name="concepts"></a>Fogalmak
[MOF-egyéni DSC-erőforrás írása](authoringResourceMOF.md)
#### <a name="other-resources"></a>Egyéb források
[Egy Windows PowerShell-parancsmag írása](/powershell/developer/windows-powershell)