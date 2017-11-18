---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "Összetett erőforrásai erőforrásként a DSC-konfiguráció használata"
ms.openlocfilehash: d889384c8d9c0746200ad424c6ab448a0e41d66c
ms.sourcegitcommit: 60c6f9d8cf316e6d5b285854e6e5641ac7648f3f
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 11/17/2017
---
# <a name="composite-resources-using-a-dsc-configuration-as-a-resource"></a><span data-ttu-id="1535e-103">Összetett erőforrások: erőforrásként a DSC-konfiguráció használata</span><span class="sxs-lookup"><span data-stu-id="1535e-103">Composite resources: Using a DSC configuration as a resource</span></span>

> <span data-ttu-id="1535e-104">Vonatkozik: A Windows PowerShell 4.0-s verzióját, a Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="1535e-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="1535e-105">Valós helyzetekben konfigurációk válhat hosszú és összetett, számos különböző erőforrások hívja, és a Tulajdonságok túlnyomó számos beállítása.</span><span class="sxs-lookup"><span data-stu-id="1535e-105">In real-world situations, configurations can become long and complex, calling many different resources and setting a vast number of properties.</span></span> <span data-ttu-id="1535e-106">Az összetettség megoldása érdekében használhatja a Windows PowerShell kívánt állapot konfigurációs szolgáltatása (DSC) konfigurációs erőforrásként más konfigurációk.</span><span class="sxs-lookup"><span data-stu-id="1535e-106">To help address this complexity, you can use a Windows PowerShell Desired State Configuration (DSC) configuration as a resource for other configurations.</span></span> <span data-ttu-id="1535e-107">Ezt nevezik Ez egy összetett erőforrás.</span><span class="sxs-lookup"><span data-stu-id="1535e-107">We call this a composite resource.</span></span> <span data-ttu-id="1535e-108">Összetett erőforrás a DSC-konfiguráció, amely paraméterei.</span><span class="sxs-lookup"><span data-stu-id="1535e-108">A composite resource is a DSC configuration that takes parameters.</span></span> <span data-ttu-id="1535e-109">A konfigurációs paraméterei összekötőként az erőforrás tulajdonságait.</span><span class="sxs-lookup"><span data-stu-id="1535e-109">The parameters of the configuration act as the properties of the resource.</span></span> <span data-ttu-id="1535e-110">A konfigurációs fájlba mentett egy **. schema.psm1** bővítményt, és vesz egy tipikus DSC-erőforrás a parancsfájl a MOF-séma- és az erőforrás helye (DSC erőforrásokra vonatkozó további információkért lásd: [Windows PowerShell célállapot-konfiguráló erőforrások](resources.md).</span><span class="sxs-lookup"><span data-stu-id="1535e-110">The configuration is saved as a file with a **.schema.psm1** extension, and takes the place of both the MOF schema and the resource script in a typical DSC resource (for more information about DSC resources, see [Windows PowerShell Desired State Configuration Resources](resources.md).</span></span>

## <a name="creating-the-composite-resource"></a><span data-ttu-id="1535e-111">Az összetett erőforrás létrehozása</span><span class="sxs-lookup"><span data-stu-id="1535e-111">Creating the composite resource</span></span>

<span data-ttu-id="1535e-112">A fenti példában, amely hívja meg a virtuális gépeket konfigurálhatja a meglévő erőforrásokat számos-konfiguráció létrehozása azt.</span><span class="sxs-lookup"><span data-stu-id="1535e-112">In our example, we create a configuration that invokes a number of existing resources to configure virtual machines.</span></span> <span data-ttu-id="1535e-113">Helyett konfigurációs blokkokban kell beállítani a értékeket ad meg, a konfiguráció számos paramétert, majd a konfigurációs blokkok használt vesz igénybe.</span><span class="sxs-lookup"><span data-stu-id="1535e-113">Instead of specifying the values to be set in configuration blocks, the configuration takes a number of parameters that are then used in the configuration blocks.</span></span>

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

### <a name="saving-the-configuration-as-a-composite-resource"></a><span data-ttu-id="1535e-114">A konfiguráció mentése összetett erőforrásként</span><span class="sxs-lookup"><span data-stu-id="1535e-114">Saving the configuration as a composite resource</span></span>

<span data-ttu-id="1535e-115">DSC erőforrásként paraméteres konfigurációt használja, például, hogy bármely más MOF-alapú erőforrás könyvtárstruktúra mentheti, és nevezze el az olyan **. schema.psm1** bővítmény.</span><span class="sxs-lookup"><span data-stu-id="1535e-115">To use the parameterized configuration as a DSC resource, save it in a directory structure like that of any other MOF-based resource, and name it with a **.schema.psm1** extension.</span></span> <span data-ttu-id="1535e-116">Ez a példa azt fogja nevet a fájlnak **xVirtualMachine.schema.psm1**.</span><span class="sxs-lookup"><span data-stu-id="1535e-116">For this example, we’ll name the file **xVirtualMachine.schema.psm1**.</span></span> <span data-ttu-id="1535e-117">Szükség nevű jegyzékfájl létrehozása **xVirtualMachine.psd1** , amely tartalmazza a következő sort.</span><span class="sxs-lookup"><span data-stu-id="1535e-117">You also need to create a manifest named **xVirtualMachine.psd1** that contains the following line.</span></span> <span data-ttu-id="1535e-118">Vegye figyelembe, hogy ez kívül **MyDscResources.psd1**, tartozó összes erőforrást modul jegyzékfájljának a **MyDscResources** mappa.</span><span class="sxs-lookup"><span data-stu-id="1535e-118">Note that this is in addition to **MyDscResources.psd1**, the module manifest for all resources under the **MyDscResources** folder.</span></span>

```powershell
RootModule = 'xVirtualMachine.schema.psm1'
```

<span data-ttu-id="1535e-119">Amikor elkészült, a gyökérmappa-szerkezetében alábbinak kell lennie.</span><span class="sxs-lookup"><span data-stu-id="1535e-119">When you are done, the folder structure should be as follows.</span></span>

```
$env: psmodulepath
    |- MyDscResources
           MyDscResources.psd1
        |- DSCResources
            |- xVirtualMachine
                |- xVirtualMachine.psd1
                |- xVirtualMachine.schema.psm1
```

<span data-ttu-id="1535e-120">Az erőforrás most felderíthető a Get-DscResource parancsmag használatával, és a Tulajdonságok vagy parancsmagot vagy segítségével felderíthetők **Ctrl + szóköz** a Windows PowerShell ISE automatikusan hajthat végre.</span><span class="sxs-lookup"><span data-stu-id="1535e-120">The resource is now discoverable by using the Get-DscResource cmdlet, and its properties are discoverable by either that cmdlet or by using **Ctrl+Space** auto-complete in the Windows PowerShell ISE.</span></span>

## <a name="using-the-composite-resource"></a><span data-ttu-id="1535e-121">Az összetett erőforrás használata</span><span class="sxs-lookup"><span data-stu-id="1535e-121">Using the composite resource</span></span>

<span data-ttu-id="1535e-122">Ezután azt, amely behívja az összetett erőforrás-konfiguráció létrehozása.</span><span class="sxs-lookup"><span data-stu-id="1535e-122">Next we create a configuration that calls the composite resource.</span></span> <span data-ttu-id="1535e-123">Ez a konfiguráció meghívja a xVirtualMachine összetett erőforrás egy virtuális gép létrehozásához, és ekkor meghívja a **xComputer** erőforrást kell nevezni.</span><span class="sxs-lookup"><span data-stu-id="1535e-123">This configuration calls the xVirtualMachine composite resource to create a virtual machine, and then calls the **xComputer** resource to rename it.</span></span>

```powershell

configuration RenameVM
{

    Import-DscResource -Module TestCompositeResource
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

## <a name="supporting-psdscrunascredential"></a><span data-ttu-id="1535e-124">PsDscRunAsCredential támogatása</span><span class="sxs-lookup"><span data-stu-id="1535e-124">Supporting PsDscRunAsCredential</span></span>

><span data-ttu-id="1535e-125">**Megjegyzés:** **PsDscRunAsCredential** PowerShell 5.0-s vagy újabb támogatott.</span><span class="sxs-lookup"><span data-stu-id="1535e-125">**Note:** **PsDscRunAsCredential** is supported in PowerShell 5.0 and later.</span></span>

<span data-ttu-id="1535e-126">A **PsDscRunAsCredential** tulajdonság használható [a DSC-konfigurációk](configurations.md) erőforrás blokk adhatja meg, hogy az erőforrás verziója alatt kell futtatni a megadott hitelesítő adatok készletét.</span><span class="sxs-lookup"><span data-stu-id="1535e-126">The **PsDscRunAsCredential** property can be used in [DSC configurations](configurations.md) resource block to specify that the resource should be run under a specified set of credentials.</span></span>
<span data-ttu-id="1535e-127">További információkért lásd: [felhasználói hitelesítő adatokkal rendelkező futtató DSC](runAsUser.md).</span><span class="sxs-lookup"><span data-stu-id="1535e-127">For more information, see [Running DSC with user credentials](runAsUser.md).</span></span>

<span data-ttu-id="1535e-128">A felhasználói környezet belül egyéni erőforrás eléréséhez használhatja az automatikus változó `$PsDscContext`.</span><span class="sxs-lookup"><span data-stu-id="1535e-128">To access the user context from within a custom resource, you can use the automatic variable `$PsDscContext`.</span></span>

<span data-ttu-id="1535e-129">Például a következő kódot a felhasználói környezet, amely alatt az erőforrás fut, a részletes kimeneti adatfolyamba lesz írási:</span><span class="sxs-lookup"><span data-stu-id="1535e-129">For example the following code would write the user context under which the resource is running to the verbose output stream:</span></span>

```powershell
if (PsDscContext.RunAsUser) {
    Write-Verbose "User: $PsDscContext.RunAsUser";
}
```

## <a name="see-also"></a><span data-ttu-id="1535e-130">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="1535e-130">See Also</span></span>
### <a name="concepts"></a><span data-ttu-id="1535e-131">Fogalmak</span><span class="sxs-lookup"><span data-stu-id="1535e-131">Concepts</span></span>
* [<span data-ttu-id="1535e-132">Egyéni DSC-erőforrás MOF írása</span><span class="sxs-lookup"><span data-stu-id="1535e-132">Writing a custom DSC resource with MOF</span></span>](authoringResourceMOF.md)
* [<span data-ttu-id="1535e-133">Ismerkedés a Windows PowerShell célállapot-konfiguráció</span><span class="sxs-lookup"><span data-stu-id="1535e-133">Get Started with Windows PowerShell Desired State Configuration</span></span>](overview.md)

