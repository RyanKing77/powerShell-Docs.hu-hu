---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "A DSC-erőforrás a C# készítése"
ms.openlocfilehash: 2fc6b8c127bca29e8f66fc7bd8d2828fdfe39f3c
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 01/17/2018
---
# <a name="authoring-a-dsc-resource-in-c"></a><span data-ttu-id="e8ff9-103">A DSC-erőforrás a C# készítése</span><span class="sxs-lookup"><span data-stu-id="e8ff9-103">Authoring a DSC resource in C#</span></span>

> <span data-ttu-id="e8ff9-104">Vonatkozik: A Windows PowerShell 4.0-s verzióját, a Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="e8ff9-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="e8ff9-105">Általában a Windows PowerShell kívánt állapot konfigurációs szolgáltatása (DSC) egyéni erőforrás vezettek be egy PowerShell-parancsfájlt.</span><span class="sxs-lookup"><span data-stu-id="e8ff9-105">Typically, a Windows PowerShell Desired State Configuration (DSC) custom resource is implemented in a PowerShell script.</span></span> <span data-ttu-id="e8ff9-106">Azonban is valósíthatja meg egyéni DSC-erőforrás funkcióinak parancsmagok írása C# nyelven íródtak.</span><span class="sxs-lookup"><span data-stu-id="e8ff9-106">However, you can also implement the functionality of a DSC custom resource by writing cmdlets in C#.</span></span> <span data-ttu-id="e8ff9-107">Témakörben megismerkedhet a parancsmagok írása C# nyelven íródtak, [írása egy Windows PowerShell-parancsmag](https://technet.microsoft.com/en-us/library/dd878294.aspx).</span><span class="sxs-lookup"><span data-stu-id="e8ff9-107">For an introduction on writing cmdlets in C#, see [Writing a Windows PowerShell Cmdlet](https://technet.microsoft.com/en-us/library/dd878294.aspx).</span></span>

<span data-ttu-id="e8ff9-108">Vezérelt végrehajtási az erőforrás a C#, parancsmagok, a folyamat a MOF-séma létrehozása, a gyökérmappa-szerkezetében létrehozása, importálása és az egyéni DSC erőforrás használatával megegyeznek a [MOFegyéniDSCerőforrásírása](authoringResourceMOF.md).</span><span class="sxs-lookup"><span data-stu-id="e8ff9-108">Aside from implementing the resource in C# as cmdlets, the process of creating the MOF schema, creating the folder structure, importing and using your custom DSC resource are the same as described in [Writing a custom DSC resource with MOF](authoringResourceMOF.md).</span></span>

## <a name="writing-a-cmdlet-based-resource"></a><span data-ttu-id="e8ff9-109">Egy parancsmag-alapú erőforrás írása</span><span class="sxs-lookup"><span data-stu-id="e8ff9-109">Writing a cmdlet-based resource</span></span>
<span data-ttu-id="e8ff9-110">Ehhez a példához fog megvalósítása egyszerű erőforrás kezelő szövegfájlba és annak tartalmát.</span><span class="sxs-lookup"><span data-stu-id="e8ff9-110">For this example, we will implement a simple resource that manages a text file and its contents.</span></span>

### <a name="writing-the-mof-schema"></a><span data-ttu-id="e8ff9-111">A MOF-séma írása</span><span class="sxs-lookup"><span data-stu-id="e8ff9-111">Writing the MOF schema</span></span>

<span data-ttu-id="e8ff9-112">Az alábbiakban áttekintjük a MOF erőforrás-definícióban.</span><span class="sxs-lookup"><span data-stu-id="e8ff9-112">The following is the MOF resource definition.</span></span>

```
[ClassVersion("1.0.0"), FriendlyName("xDemoFile")]
class MSFT_XDemoFile : OMI_BaseResource
{
                [Key, Description("path")] String Path;
                [Write, Description("Should the file be present"), ValueMap{"Present","Absent"}, Values{"Present","Absent"}] String Ensure;
                [Write, Description("Contentof file.")] String Content;                   
};
```

### <a name="setting-up-the-visual-studio-project"></a><span data-ttu-id="e8ff9-113">A Visual Studio-projekt létrehozása</span><span class="sxs-lookup"><span data-stu-id="e8ff9-113">Setting up the Visual Studio project</span></span>
#### <a name="setting-up-a-cmdlet-project"></a><span data-ttu-id="e8ff9-114">Egy parancsmag-projekt létrehozása</span><span class="sxs-lookup"><span data-stu-id="e8ff9-114">Setting up a cmdlet project</span></span>

1. <span data-ttu-id="e8ff9-115">Nyissa meg a Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e8ff9-115">Open Visual Studio.</span></span>
1. <span data-ttu-id="e8ff9-116">Hozzon létre egy C#-projektet, és adja meg a nevét.</span><span class="sxs-lookup"><span data-stu-id="e8ff9-116">Create a C# project and provide the name.</span></span>
1. <span data-ttu-id="e8ff9-117">Válassza ki **Class Library** az elérhető sablonok alapján.</span><span class="sxs-lookup"><span data-stu-id="e8ff9-117">Select **Class Library** from the available project templates.</span></span>
1. <span data-ttu-id="e8ff9-118">Kattintson a **Ok**.</span><span class="sxs-lookup"><span data-stu-id="e8ff9-118">Click **Ok**.</span></span>
1. <span data-ttu-id="e8ff9-119">A System.Automation.Management.dll egy szerelvényre mutató hivatkozás hozzáadása a projekthez.</span><span class="sxs-lookup"><span data-stu-id="e8ff9-119">Add an assembly reference to System.Automation.Management.dll to your project.</span></span>
1. <span data-ttu-id="e8ff9-120">Módosítsa az erőforrás-névre a szerelvény nevét.</span><span class="sxs-lookup"><span data-stu-id="e8ff9-120">Change the assembly name to match the resource name.</span></span> <span data-ttu-id="e8ff9-121">Ebben az esetben a szerelvény neve lehet **MSFT_XDemoFile**.</span><span class="sxs-lookup"><span data-stu-id="e8ff9-121">In this case, the assembly should be named **MSFT_XDemoFile**.</span></span>

### <a name="writing-the-cmdlet-code"></a><span data-ttu-id="e8ff9-122">A parancsmag programozás</span><span class="sxs-lookup"><span data-stu-id="e8ff9-122">Writing the cmdlet code</span></span>

<span data-ttu-id="e8ff9-123">A következő C#-kódban valósítja meg a **Get-TargetResource**, **Set-TargetResource**, és **teszt-TargetResource** parancsmagok.</span><span class="sxs-lookup"><span data-stu-id="e8ff9-123">The following C# code implements the **Get-TargetResource**, **Set-TargetResource**, and **Test-TargetResource** cmdlets.</span></span>

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

### <a name="deploying-the-resource"></a><span data-ttu-id="e8ff9-124">Az erőforrás üzembe helyezése</span><span class="sxs-lookup"><span data-stu-id="e8ff9-124">Deploying the resource</span></span>

<span data-ttu-id="e8ff9-125">A lefordított dll-fájl mentéséhez egy parancsprogram-alapú erőforrás hasonló fájlstruktúrájával.</span><span class="sxs-lookup"><span data-stu-id="e8ff9-125">The compiled dll file should be saved in a file structure similar to a script-based resource.</span></span> <span data-ttu-id="e8ff9-126">Ehhez az erőforráshoz a mappastruktúra a következő:</span><span class="sxs-lookup"><span data-stu-id="e8ff9-126">The following is the folder structure for this resource.</span></span>

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

### <a name="see-also"></a><span data-ttu-id="e8ff9-127">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="e8ff9-127">See Also</span></span>
#### <a name="concepts"></a><span data-ttu-id="e8ff9-128">Fogalmak</span><span class="sxs-lookup"><span data-stu-id="e8ff9-128">Concepts</span></span>
[<span data-ttu-id="e8ff9-129">Egyéni DSC-erőforrás MOF írása</span><span class="sxs-lookup"><span data-stu-id="e8ff9-129">Writing a custom DSC resource with MOF</span></span>](authoringResourceMOF.md)
#### <a name="other-resources"></a><span data-ttu-id="e8ff9-130">Egyéb források</span><span class="sxs-lookup"><span data-stu-id="e8ff9-130">Other Resources</span></span>
[<span data-ttu-id="e8ff9-131">Egy Windows PowerShell-parancsmag írása</span><span class="sxs-lookup"><span data-stu-id="e8ff9-131">Writing a Windows PowerShell Cmdlet</span></span>](https://msdn.microsoft.com/en-us/library/dd878294.aspx)

