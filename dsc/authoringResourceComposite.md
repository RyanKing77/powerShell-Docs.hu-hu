---
ms.date: 06/12/2017
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: Összetett erőforrásai erőforrásként a DSC-konfiguráció használata
ms.openlocfilehash: 246cab3b437546490d650e45be263a43fd0c84c3
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/16/2018
---
# <a name="composite-resources-using-a-dsc-configuration-as-a-resource"></a>Összetett erőforrások: erőforrásként a DSC-konfiguráció használata

> Vonatkozik: A Windows PowerShell 4.0-s verzióját, a Windows PowerShell 5.0

Valós helyzetekben konfigurációk válhat hosszú és összetett, számos különböző erőforrások hívja, és a Tulajdonságok túlnyomó számos beállítása. Az összetettség megoldása érdekében használhatja a Windows PowerShell kívánt állapot konfigurációs szolgáltatása (DSC) konfigurációs erőforrásként más konfigurációk. Ezt nevezik Ez egy összetett erőforrás. Összetett erőforrás a DSC-konfiguráció, amely paraméterei. A konfigurációs paraméterei összekötőként az erőforrás tulajdonságait. A konfigurációs fájlba mentett egy **. schema.psm1** bővítményt, és vesz egy tipikus DSC-erőforrás a parancsfájl a MOF-séma- és az erőforrás helye (DSC erőforrásokra vonatkozó további információkért lásd: [Windows PowerShell célállapot-konfiguráló erőforrások](resources.md).

## <a name="creating-the-composite-resource"></a>Az összetett erőforrás létrehozása

A fenti példában, amely hívja meg a virtuális gépeket konfigurálhatja a meglévő erőforrásokat számos-konfiguráció létrehozása azt. Helyett konfigurációs blokkokban kell beállítani a értékeket ad meg, a konfiguráció számos paramétert, majd a konfigurációs blokkok használt vesz igénybe.

```powershell
Configuration xVirtualMachine
{
    param
    (
        # Name of VMs
        [Parameter(Mandatory)]
        [ValidateNotNullOrEmpty()]
        [String[]] $VMName,

        # Name of Switch to create
        [Parameter(Mandatory)]
        [ValidateNotNullOrEmpty()]
        [String] $SwitchName,

        # Type of Switch to create
        [Parameter(Mandatory)]
        [ValidateNotNullOrEmpty()]
        [String] $SwitchType,

        # Source Path for VHD
        [Parameter(Mandatory)]
        [ValidateNotNullOrEmpty()]
        [String] $VHDParentPath,

        # Destination path for diff VHD
        [Parameter(Mandatory)]
        [ValidateNotNullOrEmpty()]
        [String] $VHDPath,

        # Startup Memory for VM
        [Parameter(Mandatory)]
        [ValidateNotNullOrEmpty()]
        [String] $VMStartupMemory,

        # State of the VM
        [Parameter(Mandatory)]
        [ValidateNotNullOrEmpty()]
        [String] $VMState
    )

    # Import the module that defines custom resources
    Import-DscResource -Module xComputerManagement,xHyper-V

    # Install the Hyper-V role
    WindowsFeature HyperV
    {
        Ensure = "Present"
        Name = "Hyper-V"
    }

    # Create the virtual switch
    xVMSwitch $SwitchName
    {
        Ensure = "Present"
        Name = $SwitchName
        Type = $SwitchType
        DependsOn = "[WindowsFeature]HyperV"
    }

    # Check for Parent VHD file
    File ParentVHDFile
    {
        Ensure = "Present"
        DestinationPath = $VHDParentPath
        Type = "File"
        DependsOn = "[WindowsFeature]HyperV"
    }

    # Check the destination VHD folder
    File VHDFolder
    {
        Ensure = "Present"
        DestinationPath = $VHDPath
        Type = "Directory"
        DependsOn = "[File]ParentVHDFile"
    }

    # Create VM specific diff VHD
    foreach ($Name in $VMName)
    {
        xVHD "VHD$Name"
        {
            Ensure = "Present"
            Name = $Name
            Path = $VHDPath
            ParentPath = $VHDParentPath
            DependsOn = @("[WindowsFeature]HyperV",
                          "[File]VHDFolder")
        }
    }

    # Create VM using the above VHD
    foreach($Name in $VMName)
    {
        xVMHyperV "VMachine$Name"
        {
            Ensure = "Present"
            Name = $Name
            VhDPath = (Join-Path -Path $VHDPath -ChildPath $Name)
            SwitchName = $SwitchName
            StartupMemory = $VMStartupMemory
            State = $VMState
            MACAddress = $MACAddress
            WaitForIP = $true
            DependsOn = @("[WindowsFeature]HyperV",
                          "[xVHD]VHD$Name")
        }
    }
}
```

### <a name="saving-the-configuration-as-a-composite-resource"></a>A konfiguráció mentése összetett erőforrásként

DSC erőforrásként paraméteres konfigurációt használja, például, hogy bármely más MOF-alapú erőforrás könyvtárstruktúra mentheti, és nevezze el az olyan **. schema.psm1** bővítmény. Ez a példa azt fogja nevet a fájlnak **xVirtualMachine.schema.psm1**. Szükség nevű jegyzékfájl létrehozása **xVirtualMachine.psd1** , amely tartalmazza a következő sort. Vegye figyelembe, hogy ez kívül **MyDscResources.psd1**, tartozó összes erőforrást modul jegyzékfájljának a **MyDscResources** mappa.

```powershell
RootModule = 'xVirtualMachine.schema.psm1'
```

Amikor elkészült, a gyökérmappa-szerkezetében alábbinak kell lennie.

```
$env: psmodulepath
    |- MyDscResources
           MyDscResources.psd1
        |- DSCResources
            |- xVirtualMachine
                |- xVirtualMachine.psd1
                |- xVirtualMachine.schema.psm1
```

Az erőforrás most felderíthető a Get-DscResource parancsmag használatával, és a Tulajdonságok vagy parancsmagot vagy segítségével felderíthetők **Ctrl + szóköz** a Windows PowerShell ISE automatikusan hajthat végre.

## <a name="using-the-composite-resource"></a>Az összetett erőforrás használata

Ezután azt, amely behívja az összetett erőforrás-konfiguráció létrehozása. Ez a konfiguráció meghívja a xVirtualMachine összetett erőforrás egy virtuális gép létrehozásához, és ekkor meghívja a **xComputer** erőforrást kell nevezni.

```powershell

configuration RenameVM
{

    Import-DscResource -Module xVirtualMachine
    Node localhost
    {
        xVirtualMachine VM
        {
            VMName = "Test"
            SwitchName = "Internal"
            SwitchType = "Internal"
            VhdParentPath = "C:\Demo\VHD\RTM.vhd"
            VHDPath = "C:\Demo\VHD"
            VMStartupMemory = 1024MB
            VMState = "Running"
        }
    }

    Node "192.168.10.1"
    {
        xComputer Name
        {
            Name = "SQL01"
            DomainName = "fourthcoffee.com"
        }
    }
}
```

## <a name="supporting-psdscrunascredential"></a>PsDscRunAsCredential támogatása

>**Megjegyzés:** **PsDscRunAsCredential** PowerShell 5.0-s vagy újabb támogatott.

A **PsDscRunAsCredential** tulajdonság használható [a DSC-konfigurációk](configurations.md) erőforrás blokk adhatja meg, hogy az erőforrás verziója alatt kell futtatni a megadott hitelesítő adatok készletét.
További információkért lásd: [felhasználói hitelesítő adatokkal rendelkező futtató DSC](runAsUser.md).

A felhasználói környezet belül egyéni erőforrás eléréséhez használhatja az automatikus változó `$PsDscContext`.

Például a következő kódot a felhasználói környezet, amely alatt az erőforrás fut, a részletes kimeneti adatfolyamba lesz írási:

```powershell
if ($PsDscContext.RunAsUser) {
    Write-Verbose "User: $PsDscContext.RunAsUser";
}
```

## <a name="see-also"></a>Lásd még:
### <a name="concepts"></a>Fogalmak
* [Egyéni DSC-erőforrás MOF írása](authoringResourceMOF.md)
* [Ismerkedés a Windows PowerShell célállapot-konfiguráció](overview.md)