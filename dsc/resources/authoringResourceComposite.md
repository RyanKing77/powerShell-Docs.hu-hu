---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Összetett erőforrások – erőforrásként a DSC-konfiguráció használata
ms.openlocfilehash: 2823d05e0c8feb2933ca691f9ab5149ace2f7ee3
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55684044"
---
# <a name="composite-resources-using-a-dsc-configuration-as-a-resource"></a>Összetett erőforrások: A DSC-konfiguráció használata erőforrásként

> Érvényes: Windows PowerShell 4.0-s, a Windows PowerShell 5.0

A való életből vett helyzetekben a konfigurációk válhat a hosszú és összetett, számos különböző erőforrás hívása és a egy hatalmas tulajdonságainak beállítása. Annak érdekében, oldja meg ezt a komplexitást, egy Windows PowerShell Desired State Configuration (DSC) konfigurációt használhatja erőforrásként más konfigurációk esetén. Ezt nevezzük egy összetett erőforrást. Egy összetett erőforrás egy DSC-konfiguráció, amely a paramétereket. A konfiguráció paraméterei az erőforrás tulajdonságainak szerepét. A konfigurációs fájlba mentett egy **. schema.psm1** bővítményt, és vesz igénybe egy jellemző DSC-erőforrás szkriptet a MOF-séma- és az erőforráscsoport helye (DSC-erőforrások kapcsolatos további információkért lásd: [Windows PowerShell Desired State Configuration erőforrások](resources.md).

## <a name="creating-the-composite-resource"></a>Az összetett erőforrás létrehozása

Ebben a példában létrehozunk egy konfigurációt, amely meghív egy meglévő erőforrások konfigurálása a virtuális gépek száma. Ahelyett, hogy a konfigurációs blokk kell beállítani az értékek megadásával, a konfigurációs paramétereket, majd a konfigurációs egységekben több vesz igénybe.

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

### <a name="saving-the-configuration-as-a-composite-resource"></a>Összetett erőforrásként konfigurációjának mentése

A paraméteres configuration adatokként a DSC-erőforrás, mentse azt egy könyvtárstruktúrát, mint bármely más MOF-alapú erőforrás, amely, és adja neki a egy **. schema.psm1** bővítmény. Ebben a példában azt fogja nevet a fájlnak **xVirtualMachine.schema.psm1**. Hozzon létre egy jegyzéket nevű kell **xVirtualMachine.psd1** , amely tartalmazza a következő sort. Vegye figyelembe, hogy ez kiegészítésként szolgál **MyDscResources.psd1**, a modul jegyzékfájljának tartozó összes erőforrást a **MyDscResources** mappát.

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

Az erőforrás már felderíthetők a Get-DscResource parancsmag használatával, és a tulajdonságai nem észlelhető, vagy a parancsmagot vagy a **Ctrl + szóköz** automatikus kiegészítés a Windows PowerShell ISE-ben.

## <a name="using-the-composite-resource"></a>Az összetett erőforrás használata

Ezután létrehozunk egy konfigurációt, amely meghívja ezt az összetett erőforrást. Ez a konfiguráció meghívja a xVirtualMachine összetett erőforrás hozhat létre egy virtuális gépet, és ekkor meghívja a **xComputer** nevezze át az erőforrást.

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

>**Megjegyzés:** **PsDscRunAsCredential** a PowerShell 5.0-s és újabb verzióiban támogatott.

A **PsDscRunAsCredential** tulajdonság használható [DSC-konfigurációk](../configurations/configurations.md) erőforrás letiltása, hogy az erőforrás alatt kell futtatni. egy meghatározott hitelesítő adatok megadásához.
További információkért lásd: [DSC futtatása felhasználói hitelesítő adatokkal](../configurations/runAsUser.md).

A felhasználói környezet belül egy egyéni erőforrás elérésére, használhatja az automatikus változót `$PsDscContext`.

Például a következő kódot a felhasználói környezet, amelyben az erőforrás fut. a részletes kimeneti adatfolyamba volna írni:

```powershell
if ($PsDscContext.RunAsUser) {
    Write-Verbose "User: $PsDscContext.RunAsUser";
}
```

## <a name="see-also"></a>Lásd még:
### <a name="concepts"></a>Fogalmak
* [MOF-egyéni DSC-erőforrás írása](authoringResourceMOF.md)
* [Ismerkedés a Windows PowerShell Desired State Configuration](../overview/overview.md)