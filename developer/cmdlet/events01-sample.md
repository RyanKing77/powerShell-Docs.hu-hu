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
# <a name="events01-sample"></a>Events01 – minta

Ez a példa bemutatja, hogyan hozhat létre olyan parancsmagot, amely lehetővé teszi, hogy a felhasználó regisztrálhatja által előállított eseményeket [System.IO.Filesystemwatcher](/dotnet/api/System.IO.FileSystemWatcher). Ezzel a parancsmaggal a felhasználók regisztrálhatnak egy művelet hajtható végre, ha létrejön egy fájl egy adott könyvtárban. Ez a minta származik a [Microsoft.PowerShell.Commands.Objecteventregistrationbase](/dotnet/api/Microsoft.PowerShell.Commands.ObjectEventRegistrationBase) alaposztály.

## <a name="how-to-build-the-sample-by-using-visual-studio"></a>Hogyan hozhat létre a mintát a Visual Studio használatával.

1. A Windows PowerShell 2.0 SDK telepítve van, és keresse meg a Events01 mappát. Az alapértelmezett hely a C:\Program Files (x86) \Microsoft SDKs\Windows\v7.0\Samples\sysmgmt\WindowsPowerShell\csharp\Events01.

2. A megoldásfájlt (.sln) ikonra. Ekkor megnyílik a mintaprojektet a Microsoft Visual Studio.

3. Az a **összeállítása** menüjében válassza **megoldás fordítása**.

    A könyvtárban, a minta az alapértelmezett \bin vagy \bin\debug mappákat a lesz felépítve.

### <a name="how-to-run-the-sample"></a>A minta futtatása

1. Hozza létre a következő modul mappát:

    `[user]/documents/windowspowershell/modules/events01`

2. A minta a könyvtárfájl a modul mappába másolja.

3. Indítsa el a Windows PowerShellt.

4. Futtassa a parancsmagot betöltése a Windows PowerShell a következő parancsot:

    ```powershell
    import-module events01
    ```

5. Használja a Register-FileSystemEvent parancsmagot egy műveletet, amely egy üzenetet fog kiírni, amikor létrejön egy fájl a TEMP könyvtár alá regisztrálni.

    ```powershell
    Register-FileSystemEvent $env:temp Created -filter "*.txt" -action { Write-Host "A file was created in the TEMP directory" }
    ```

6. Hozzon létre egy fájlt a TEMP könyvtár alá, és vegye figyelembe, hogy végrehajtja-e a művelet (az üzenet jelenik meg).

Ez a kimenet az eredmények az alábbi lépéseket.

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

## <a name="requirements"></a>Követelmények

Ez a minta Windows PowerShell 2.0 szükséges.

## <a name="demonstrates"></a>Bemutatók

Ez a minta bemutatja a következő.

- Hogyan írható-eseményregisztráció parancsmag. A parancsmag származik a [Microsoft.PowerShell.Commands.Objecteventregistrationbase](/dotnet/api/Microsoft.PowerShell.Commands.ObjectEventRegistrationBase) osztály, amely támogatja a gyakori paraméterek a Register-* esemény parancsmagok. Parancsmagok származó [Microsoft.PowerShell.Commands.Objecteventregistrationbase](/dotnet/api/Microsoft.PowerShell.Commands.ObjectEventRegistrationBase) csak definiálnia kell a adott paramétereikről bírálja felül a `GetSourceObject` és `GetSourceObjectEventName` módszerek absztrakt.

## <a name="example"></a>Példa

Ez a példa bemutatja, hogyan regisztrálhat az események által kiváltott [System.IO.FileSystemWatcher](https://msdn.microsoft.com/en-us/library/system.io.filesystemwatcher\(v=vs.110\).aspx).

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

## <a name="see-also"></a>Lásd még:

[Egy Windows PowerShell-parancsmag írása](./writing-a-windows-powershell-cmdlet.md)