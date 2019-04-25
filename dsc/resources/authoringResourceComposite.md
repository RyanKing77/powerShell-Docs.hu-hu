---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Összetett erőforrások – erőforrásként a DSC-konfiguráció használata
ms.openlocfilehash: 2823d05e0c8feb2933ca691f9ab5149ace2f7ee3
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62076684"
---
# <a name="composite-resources-using-a-dsc-configuration-as-a-resource"></a><span data-ttu-id="c8d58-103">Összetett erőforrások: A DSC-konfiguráció használata erőforrásként</span><span class="sxs-lookup"><span data-stu-id="c8d58-103">Composite resources: Using a DSC configuration as a resource</span></span>

> <span data-ttu-id="c8d58-104">A következőkre vonatkozik: Windows PowerShell 4.0-s, a Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="c8d58-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="c8d58-105">A való életből vett helyzetekben a konfigurációk válhat a hosszú és összetett, számos különböző erőforrás hívása és a egy hatalmas tulajdonságainak beállítása.</span><span class="sxs-lookup"><span data-stu-id="c8d58-105">In real-world situations, configurations can become long and complex, calling many different resources and setting a vast number of properties.</span></span> <span data-ttu-id="c8d58-106">Annak érdekében, oldja meg ezt a komplexitást, egy Windows PowerShell Desired State Configuration (DSC) konfigurációt használhatja erőforrásként más konfigurációk esetén.</span><span class="sxs-lookup"><span data-stu-id="c8d58-106">To help address this complexity, you can use a Windows PowerShell Desired State Configuration (DSC) configuration as a resource for other configurations.</span></span> <span data-ttu-id="c8d58-107">Ezt nevezzük egy összetett erőforrást.</span><span class="sxs-lookup"><span data-stu-id="c8d58-107">We call this a composite resource.</span></span> <span data-ttu-id="c8d58-108">Egy összetett erőforrás egy DSC-konfiguráció, amely a paramétereket.</span><span class="sxs-lookup"><span data-stu-id="c8d58-108">A composite resource is a DSC configuration that takes parameters.</span></span> <span data-ttu-id="c8d58-109">A konfiguráció paraméterei az erőforrás tulajdonságainak szerepét.</span><span class="sxs-lookup"><span data-stu-id="c8d58-109">The parameters of the configuration act as the properties of the resource.</span></span> <span data-ttu-id="c8d58-110">A konfigurációs fájlba mentett egy **. schema.psm1** bővítményt, és vesz igénybe egy jellemző DSC-erőforrás szkriptet a MOF-séma- és az erőforráscsoport helye (DSC-erőforrások kapcsolatos további információkért lásd: [Windows PowerShell Desired State Configuration erőforrások](resources.md).</span><span class="sxs-lookup"><span data-stu-id="c8d58-110">The configuration is saved as a file with a **.schema.psm1** extension, and takes the place of both the MOF schema and the resource script in a typical DSC resource (for more information about DSC resources, see [Windows PowerShell Desired State Configuration Resources](resources.md).</span></span>

## <a name="creating-the-composite-resource"></a><span data-ttu-id="c8d58-111">Az összetett erőforrás létrehozása</span><span class="sxs-lookup"><span data-stu-id="c8d58-111">Creating the composite resource</span></span>

<span data-ttu-id="c8d58-112">Ebben a példában létrehozunk egy konfigurációt, amely meghív egy meglévő erőforrások konfigurálása a virtuális gépek száma.</span><span class="sxs-lookup"><span data-stu-id="c8d58-112">In our example, we create a configuration that invokes a number of existing resources to configure virtual machines.</span></span> <span data-ttu-id="c8d58-113">Ahelyett, hogy a konfigurációs blokk kell beállítani az értékek megadásával, a konfigurációs paramétereket, majd a konfigurációs egységekben több vesz igénybe.</span><span class="sxs-lookup"><span data-stu-id="c8d58-113">Instead of specifying the values to be set in configuration blocks, the configuration takes a number of parameters that are then used in the configuration blocks.</span></span>

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

### <a name="saving-the-configuration-as-a-composite-resource"></a><span data-ttu-id="c8d58-114">Összetett erőforrásként konfigurációjának mentése</span><span class="sxs-lookup"><span data-stu-id="c8d58-114">Saving the configuration as a composite resource</span></span>

<span data-ttu-id="c8d58-115">A paraméteres configuration adatokként a DSC-erőforrás, mentse azt egy könyvtárstruktúrát, mint bármely más MOF-alapú erőforrás, amely, és adja neki a egy **. schema.psm1** bővítmény.</span><span class="sxs-lookup"><span data-stu-id="c8d58-115">To use the parameterized configuration as a DSC resource, save it in a directory structure like that of any other MOF-based resource, and name it with a **.schema.psm1** extension.</span></span> <span data-ttu-id="c8d58-116">Ebben a példában azt fogja nevet a fájlnak **xVirtualMachine.schema.psm1**.</span><span class="sxs-lookup"><span data-stu-id="c8d58-116">For this example, we’ll name the file **xVirtualMachine.schema.psm1**.</span></span> <span data-ttu-id="c8d58-117">Hozzon létre egy jegyzéket nevű kell **xVirtualMachine.psd1** , amely tartalmazza a következő sort.</span><span class="sxs-lookup"><span data-stu-id="c8d58-117">You also need to create a manifest named **xVirtualMachine.psd1** that contains the following line.</span></span> <span data-ttu-id="c8d58-118">Vegye figyelembe, hogy ez kiegészítésként szolgál **MyDscResources.psd1**, a modul jegyzékfájljának tartozó összes erőforrást a **MyDscResources** mappát.</span><span class="sxs-lookup"><span data-stu-id="c8d58-118">Note that this is in addition to **MyDscResources.psd1**, the module manifest for all resources under the **MyDscResources** folder.</span></span>

```powershell
RootModule = 'xVirtualMachine.schema.psm1'
```

<span data-ttu-id="c8d58-119">Amikor elkészült, a gyökérmappa-szerkezetében alábbinak kell lennie.</span><span class="sxs-lookup"><span data-stu-id="c8d58-119">When you are done, the folder structure should be as follows.</span></span>

```
$env: psmodulepath
    |- MyDscResources
           MyDscResources.psd1
        |- DSCResources
            |- xVirtualMachine
                |- xVirtualMachine.psd1
                |- xVirtualMachine.schema.psm1
```

<span data-ttu-id="c8d58-120">Az erőforrás már felderíthetők a Get-DscResource parancsmag használatával, és a tulajdonságai nem észlelhető, vagy a parancsmagot vagy a **Ctrl + szóköz** automatikus kiegészítés a Windows PowerShell ISE-ben.</span><span class="sxs-lookup"><span data-stu-id="c8d58-120">The resource is now discoverable by using the Get-DscResource cmdlet, and its properties are discoverable by either that cmdlet or by using **Ctrl+Space** auto-complete in the Windows PowerShell ISE.</span></span>

## <a name="using-the-composite-resource"></a><span data-ttu-id="c8d58-121">Az összetett erőforrás használata</span><span class="sxs-lookup"><span data-stu-id="c8d58-121">Using the composite resource</span></span>

<span data-ttu-id="c8d58-122">Ezután létrehozunk egy konfigurációt, amely meghívja ezt az összetett erőforrást.</span><span class="sxs-lookup"><span data-stu-id="c8d58-122">Next we create a configuration that calls the composite resource.</span></span> <span data-ttu-id="c8d58-123">Ez a konfiguráció meghívja a xVirtualMachine összetett erőforrás hozhat létre egy virtuális gépet, és ekkor meghívja a **xComputer** nevezze át az erőforrást.</span><span class="sxs-lookup"><span data-stu-id="c8d58-123">This configuration calls the xVirtualMachine composite resource to create a virtual machine, and then calls the **xComputer** resource to rename it.</span></span>

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

## <a name="supporting-psdscrunascredential"></a><span data-ttu-id="c8d58-124">PsDscRunAsCredential támogatása</span><span class="sxs-lookup"><span data-stu-id="c8d58-124">Supporting PsDscRunAsCredential</span></span>

><span data-ttu-id="c8d58-125">**Megjegyzés:** **PsDscRunAsCredential** a PowerShell 5.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="c8d58-125">**Note:** **PsDscRunAsCredential** is supported in PowerShell 5.0 and later.</span></span>

<span data-ttu-id="c8d58-126">A **PsDscRunAsCredential** tulajdonság használható [DSC-konfigurációk](../configurations/configurations.md) erőforrás letiltása, hogy az erőforrás alatt kell futtatni. egy meghatározott hitelesítő adatok megadásához.</span><span class="sxs-lookup"><span data-stu-id="c8d58-126">The **PsDscRunAsCredential** property can be used in [DSC configurations](../configurations/configurations.md) resource block to specify that the resource should be run under a specified set of credentials.</span></span>
<span data-ttu-id="c8d58-127">További információkért lásd: [DSC futtatása felhasználói hitelesítő adatokkal](../configurations/runAsUser.md).</span><span class="sxs-lookup"><span data-stu-id="c8d58-127">For more information, see [Running DSC with user credentials](../configurations/runAsUser.md).</span></span>

<span data-ttu-id="c8d58-128">A felhasználói környezet belül egy egyéni erőforrás elérésére, használhatja az automatikus változót `$PsDscContext`.</span><span class="sxs-lookup"><span data-stu-id="c8d58-128">To access the user context from within a custom resource, you can use the automatic variable `$PsDscContext`.</span></span>

<span data-ttu-id="c8d58-129">Például a következő kódot a felhasználói környezet, amelyben az erőforrás fut. a részletes kimeneti adatfolyamba volna írni:</span><span class="sxs-lookup"><span data-stu-id="c8d58-129">For example the following code would write the user context under which the resource is running to the verbose output stream:</span></span>

```powershell
if ($PsDscContext.RunAsUser) {
    Write-Verbose "User: $PsDscContext.RunAsUser";
}
```

## <a name="see-also"></a><span data-ttu-id="c8d58-130">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="c8d58-130">See Also</span></span>
### <a name="concepts"></a><span data-ttu-id="c8d58-131">Fogalmak</span><span class="sxs-lookup"><span data-stu-id="c8d58-131">Concepts</span></span>
* [<span data-ttu-id="c8d58-132">MOF-egyéni DSC-erőforrás írása</span><span class="sxs-lookup"><span data-stu-id="c8d58-132">Writing a custom DSC resource with MOF</span></span>](authoringResourceMOF.md)
* [<span data-ttu-id="c8d58-133">Ismerkedés a Windows PowerShell Desired State Configuration</span><span class="sxs-lookup"><span data-stu-id="c8d58-133">Get Started with Windows PowerShell Desired State Configuration</span></span>](../overview/overview.md)