---
title: Events01 minta |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 27d0ee5e-2589-4530-92ef-c09996b80994
caps.latest.revision: 10
ms.openlocfilehash: c9963819f1842d1245735dabc487babaa566c160
ms.sourcegitcommit: caac7d098a448232304c9d6728e7340ec7517a71
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/16/2019
ms.locfileid: "58057161"
---
# <a name="events01-sample"></a><span data-ttu-id="b1fc2-102">Events01 – minta</span><span class="sxs-lookup"><span data-stu-id="b1fc2-102">Events01 Sample</span></span>

<span data-ttu-id="b1fc2-103">Ez a példa bemutatja, hogyan hozhat létre olyan parancsmagot, amely lehetővé teszi, hogy a felhasználó regisztrálhatja által előállított eseményeket [System.IO.Filesystemwatcher](/dotnet/api/System.IO.FileSystemWatcher).</span><span class="sxs-lookup"><span data-stu-id="b1fc2-103">This sample shows how to create a cmdlet that allows the user to register for events that are raised by [System.IO.Filesystemwatcher](/dotnet/api/System.IO.FileSystemWatcher).</span></span> <span data-ttu-id="b1fc2-104">Ezzel a parancsmaggal a felhasználók regisztrálhatnak egy művelet hajtható végre, ha létrejön egy fájl egy adott könyvtárban.</span><span class="sxs-lookup"><span data-stu-id="b1fc2-104">With this cmdlet, users can register an action to execute when a file is created under a specific directory.</span></span> <span data-ttu-id="b1fc2-105">Ez a minta származik a [Microsoft.PowerShell.Commands.Objecteventregistrationbase](/dotnet/api/Microsoft.PowerShell.Commands.ObjectEventRegistrationBase) alaposztály.</span><span class="sxs-lookup"><span data-stu-id="b1fc2-105">This sample derives from the [Microsoft.PowerShell.Commands.Objecteventregistrationbase](/dotnet/api/Microsoft.PowerShell.Commands.ObjectEventRegistrationBase) base class.</span></span>

## <a name="how-to-build-the-sample-by-using-visual-studio"></a><span data-ttu-id="b1fc2-106">Hogyan hozhat létre a mintát a Visual Studio használatával.</span><span class="sxs-lookup"><span data-stu-id="b1fc2-106">How to build the sample by using Visual Studio.</span></span>

1. <span data-ttu-id="b1fc2-107">A Windows PowerShell 2.0 SDK telepítve van, és keresse meg a Events01 mappát.</span><span class="sxs-lookup"><span data-stu-id="b1fc2-107">With the Windows PowerShell 2.0 SDK installed, navigate to the Events01 folder.</span></span> <span data-ttu-id="b1fc2-108">Az alapértelmezett hely a C:\Program Files (x86) \Microsoft SDKs\Windows\v7.0\Samples\sysmgmt\WindowsPowerShell\csharp\Events01.</span><span class="sxs-lookup"><span data-stu-id="b1fc2-108">The default location is C:\Program Files (x86)\Microsoft SDKs\Windows\v7.0\Samples\sysmgmt\WindowsPowerShell\csharp\Events01.</span></span>

2. <span data-ttu-id="b1fc2-109">A megoldásfájlt (.sln) ikonra.</span><span class="sxs-lookup"><span data-stu-id="b1fc2-109">Double-click the icon for the solution (.sln) file.</span></span> <span data-ttu-id="b1fc2-110">Ekkor megnyílik a mintaprojektet a Microsoft Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b1fc2-110">This opens the sample project in Microsoft Visual Studio.</span></span>

3. <span data-ttu-id="b1fc2-111">Az a **összeállítása** menüjében válassza **megoldás fordítása**.</span><span class="sxs-lookup"><span data-stu-id="b1fc2-111">In the **Build** menu, select **Build Solution**.</span></span>

    <span data-ttu-id="b1fc2-112">A könyvtárban, a minta az alapértelmezett \bin vagy \bin\debug mappákat a lesz felépítve.</span><span class="sxs-lookup"><span data-stu-id="b1fc2-112">The library for the sample will be built in the default \bin or \bin\debug folders.</span></span>

### <a name="how-to-run-the-sample"></a><span data-ttu-id="b1fc2-113">A minta futtatása</span><span class="sxs-lookup"><span data-stu-id="b1fc2-113">How to run the sample</span></span>

1. <span data-ttu-id="b1fc2-114">Hozza létre a következő modul mappát:</span><span class="sxs-lookup"><span data-stu-id="b1fc2-114">Create the following module folder:</span></span>

    `[user]/documents/windowspowershell/modules/events01`

2. <span data-ttu-id="b1fc2-115">A minta a könyvtárfájl a modul mappába másolja.</span><span class="sxs-lookup"><span data-stu-id="b1fc2-115">Copy the library file for the sample to the module folder.</span></span>

3. <span data-ttu-id="b1fc2-116">Indítsa el a Windows PowerShellt.</span><span class="sxs-lookup"><span data-stu-id="b1fc2-116">Start Windows PowerShell.</span></span>

4. <span data-ttu-id="b1fc2-117">Futtassa a parancsmagot betöltése a Windows PowerShell a következő parancsot:</span><span class="sxs-lookup"><span data-stu-id="b1fc2-117">Run the following command to load the cmdlet into Windows PowerShell:</span></span>

    ```powershell
    import-module events01
    ```

5. <span data-ttu-id="b1fc2-118">Használja a Register-FileSystemEvent parancsmagot egy műveletet, amely egy üzenetet fog kiírni, amikor létrejön egy fájl a TEMP könyvtár alá regisztrálni.</span><span class="sxs-lookup"><span data-stu-id="b1fc2-118">Use the Register-FileSystemEvent cmdlet to register an action that will write a message when a file is created under the TEMP directory.</span></span>

    ```powershell
    Register-FileSystemEvent $env:temp Created -filter "*.txt" -action { Write-Host "A file was created in the TEMP directory" }
    ```

6. <span data-ttu-id="b1fc2-119">Hozzon létre egy fájlt a TEMP könyvtár alá, és vegye figyelembe, hogy végrehajtja-e a művelet (az üzenet jelenik meg).</span><span class="sxs-lookup"><span data-stu-id="b1fc2-119">Create a file under the TEMP directory and note that the action is executed (the message is displayed).</span></span>

<span data-ttu-id="b1fc2-120">Ez a kimenet az eredmények az alábbi lépéseket.</span><span class="sxs-lookup"><span data-stu-id="b1fc2-120">This is a sample output that results by following these steps.</span></span>

```output
Id              Name            State      HasMoreData     Location             Command
--              ----            -----      -----------     --------             -------
1               26932870-d3b... NotStarted False                                 Write-Host "A f...

```

```powershell
Set-Content $env:temp\test.txt "This is a test file"
```

```output
A file was created in the TEMP directory
```

## <a name="requirements"></a><span data-ttu-id="b1fc2-121">Követelmények</span><span class="sxs-lookup"><span data-stu-id="b1fc2-121">Requirements</span></span>

<span data-ttu-id="b1fc2-122">Ez a minta Windows PowerShell 2.0 szükséges.</span><span class="sxs-lookup"><span data-stu-id="b1fc2-122">This sample requires Windows PowerShell 2.0.</span></span>

## <a name="demonstrates"></a><span data-ttu-id="b1fc2-123">Bemutatók</span><span class="sxs-lookup"><span data-stu-id="b1fc2-123">Demonstrates</span></span>

<span data-ttu-id="b1fc2-124">Ez a minta bemutatja a következő.</span><span class="sxs-lookup"><span data-stu-id="b1fc2-124">This sample demonstrates the following.</span></span>

- <span data-ttu-id="b1fc2-125">Hogyan írható-eseményregisztráció parancsmag.</span><span class="sxs-lookup"><span data-stu-id="b1fc2-125">How to write a cmdlet for event registration.</span></span> <span data-ttu-id="b1fc2-126">A parancsmag származik a [Microsoft.PowerShell.Commands.Objecteventregistrationbase](/dotnet/api/Microsoft.PowerShell.Commands.ObjectEventRegistrationBase) osztály, amely támogatja a gyakori paraméterek a Register-\* esemény parancsmagok.</span><span class="sxs-lookup"><span data-stu-id="b1fc2-126">The cmdlet derives from the [Microsoft.PowerShell.Commands.Objecteventregistrationbase](/dotnet/api/Microsoft.PowerShell.Commands.ObjectEventRegistrationBase) class, which provides support for parameters common to the Register-\*Event cmdlets.</span></span> <span data-ttu-id="b1fc2-127">Parancsmagok származó [Microsoft.PowerShell.Commands.Objecteventregistrationbase](/dotnet/api/Microsoft.PowerShell.Commands.ObjectEventRegistrationBase) csak definiálnia kell a adott paramétereikről bírálja felül a `GetSourceObject` és `GetSourceObjectEventName` módszerek absztrakt.</span><span class="sxs-lookup"><span data-stu-id="b1fc2-127">Cmdlets that are derived from [Microsoft.PowerShell.Commands.Objecteventregistrationbase](/dotnet/api/Microsoft.PowerShell.Commands.ObjectEventRegistrationBase) need only to define their particular parameters and override the `GetSourceObject` and `GetSourceObjectEventName` abstract methods.</span></span>

## <a name="example"></a><span data-ttu-id="b1fc2-128">Példa</span><span class="sxs-lookup"><span data-stu-id="b1fc2-128">Example</span></span>

<span data-ttu-id="b1fc2-129">Ez a példa bemutatja, hogyan regisztrálhat az események által kiváltott [System.IO.FileSystemWatcher](https://msdn.microsoft.com/en-us/library/system.io.filesystemwatcher\(v=vs.110\).aspx).</span><span class="sxs-lookup"><span data-stu-id="b1fc2-129">This sample shows how to register for events raised by [System.IO.FileSystemWatcher](https://msdn.microsoft.com/en-us/library/system.io.filesystemwatcher\(v=vs.110\).aspx).</span></span>

```csharp
namespace Sample
{
    using System;
    using System.IO;
    using System.Management.Automation;
    using System.Management.Automation.Runspaces;
    using Microsoft.PowerShell.Commands;

    [Cmdlet(VerbsLifecycle.Register, "FileSystemEvent")]
    public class RegisterObjectEventCommand : ObjectEventRegistrationBase
    {
        /// <summary>The FileSystemWatcher that exposes the events.</summary>
        private FileSystemWatcher fileSystemWatcher = new FileSystemWatcher();

        /// <summary>Name of the event to which the cmdlet registers.</summary>
        private string eventName = null;

        /// <summary>
        /// Gets or sets the path that will be monitored by the FileSystemWatcher.
        /// </summary>
        [Parameter(Mandatory = true, Position = 0)]
        public string Path
        {
            get
            {
                return this.fileSystemWatcher.Path;
            }

            set
            {
                this.fileSystemWatcher.Path = value;
            }
        }

        /// <summary>
        /// Gets or sets the name of the event to which the cmdlet registers.
        /// <para>
        /// Currently System.IO.FileSystemWatcher exposes 6 events: Changed, Created,
        /// Deleted, Disposed, Error, and Renamed. Check the MSDN documentation of
        /// FileSystemWatcher for details on each event.
        /// </para>
        /// </summary>
        [Parameter(Mandatory = true, Position = 1)]
        public string EventName
        {
            get
            {
                return this.eventName;
            }

            set
            {
                this.eventName = value;
            }
        }

        /// <summary>
        /// Gets or sets the filter that will be user by the FileSystemWatcher.
        /// </summary>
        [Parameter(Mandatory = false)]
        public string Filter
        {
            get
            {
                return this.fileSystemWatcher.Filter;
            }

            set
            {
                this.fileSystemWatcher.Filter = value;
            }
        }

        /// <summary>
        /// Derived classes must implement this method to return the object that generates
        /// the events to be monitored.
        /// </summary>
        /// <returns> This sample returns an instance of System.IO.FileSystemWatcher</returns>
        protected override object GetSourceObject()
        {
            return this.fileSystemWatcher;
        }

        /// <summary>
        /// Derived classes must implement this method to return the name of the event to
        /// be monitored. This event must be exposed by the input object.
        /// </summary>
        /// <returns> This sample returns the event specified by the user with the -EventName parameter.</returns>
        protected override string GetSourceObjectEventName()
        {
            return this.eventName;
        }
    }
}
```

## <a name="see-also"></a><span data-ttu-id="b1fc2-130">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="b1fc2-130">See Also</span></span>

[<span data-ttu-id="b1fc2-131">Egy Windows PowerShell-parancsmag írása</span><span class="sxs-lookup"><span data-stu-id="b1fc2-131">Writing a Windows PowerShell Cmdlet</span></span>](./writing-a-windows-powershell-cmdlet.md)