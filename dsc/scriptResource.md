---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "A DSC-parancsfájl-erőforrás"
ms.openlocfilehash: 81718de0b0c8463189e33e565dc9ff39692dbe8b
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
# <a name="dsc-script-resource"></a><span data-ttu-id="254ba-103">A DSC-parancsfájl-erőforrás</span><span class="sxs-lookup"><span data-stu-id="254ba-103">DSC Script Resource</span></span>

 
> <span data-ttu-id="254ba-104">Vonatkozik: A Windows PowerShell 4.0-s verzióját, a Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="254ba-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="254ba-105">A **parancsfájl** erőforrás a Windows PowerShell szükséges konfiguráló (DSC) lehetővé teszi a Windows PowerShell parancsfájl-blokkokban futtathatnak célcsomópontokat.</span><span class="sxs-lookup"><span data-stu-id="254ba-105">The **Script** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to run Windows PowerShell script blocks on target nodes.</span></span> <span data-ttu-id="254ba-106">A `Script` erőforrás `GetScript`, `SetScript`, és `TestScript` tulajdonságok.</span><span class="sxs-lookup"><span data-stu-id="254ba-106">The `Script` resource has `GetScript`, `SetScript`, and `TestScript` properties.</span></span> <span data-ttu-id="254ba-107">Ezeket a tulajdonságokat meg kell minden egyes cél csomóponton futó parancsfájl-blokkokban.</span><span class="sxs-lookup"><span data-stu-id="254ba-107">These properties should be set to script blocks that will run on each target node.</span></span> 

<span data-ttu-id="254ba-108">A `GetScript` parancsprogram-blokkot kell visszaadnia egy kivonattáblát az aktuális csomópont állapotát jelző.</span><span class="sxs-lookup"><span data-stu-id="254ba-108">The `GetScript` script block should return a hashtable representing the state of the current node.</span></span> <span data-ttu-id="254ba-109">A hashtable csak tartalmaznia kell egy key `Result` és az érték típusúnak kell lennie `String`.</span><span class="sxs-lookup"><span data-stu-id="254ba-109">The hashtable must only contain one key `Result` and the value must be of type `String`.</span></span> <span data-ttu-id="254ba-110">Visszaadandó semmit nem szükséges.</span><span class="sxs-lookup"><span data-stu-id="254ba-110">It is not required to return anything.</span></span> <span data-ttu-id="254ba-111">A DSC-ből nem minden kimenetét a script blokkból.</span><span class="sxs-lookup"><span data-stu-id="254ba-111">DSC doesn't do anything with the output of this script block.</span></span>

<span data-ttu-id="254ba-112">A `TestScript` parancsprogram-blokkot kell meghatározni, hogy az aktuális csomópont módosítani kell-e.</span><span class="sxs-lookup"><span data-stu-id="254ba-112">The `TestScript` script block should determine if the current node needs to be modified.</span></span> <span data-ttu-id="254ba-113">Az kell visszaadnia `$true` Ha a csomópont naprakész.</span><span class="sxs-lookup"><span data-stu-id="254ba-113">It should return `$true` if the node is up-to-date.</span></span> <span data-ttu-id="254ba-114">Az kell visszaadnia `$false` Ha a csomópont-konfiguráció elavult, és amelyet frissíteni kell a `SetScript` parancsprogram-blokkot tartalmazzon.</span><span class="sxs-lookup"><span data-stu-id="254ba-114">It should return `$false` if the node's configuration is out-of-date and should be updated by the `SetScript` script block.</span></span> <span data-ttu-id="254ba-115">A `TestScript` DSC hívja parancsprogram-blokkot tartalmazzon.</span><span class="sxs-lookup"><span data-stu-id="254ba-115">The `TestScript` script block is called by DSC.</span></span>

<span data-ttu-id="254ba-116">A `SetScript` parancsprogram-blokkot kell módosítani a csomópont.</span><span class="sxs-lookup"><span data-stu-id="254ba-116">The `SetScript` script block should modify the node.</span></span> <span data-ttu-id="254ba-117">Azt nevezzük DSC által, ha a `TestScript` visszatérési blokkolása `$false`.</span><span class="sxs-lookup"><span data-stu-id="254ba-117">It is called by DSC if the `TestScript` block return `$false`.</span></span>

<span data-ttu-id="254ba-118">Ha szeretné-e a konfigurációs parancsprogram a változók használata a `GetScript`, `TestScript`, vagy `SetScript` parancsfájl-blokkokban, használja a `$using:` hatókör (lásd lent példát).</span><span class="sxs-lookup"><span data-stu-id="254ba-118">If you need to use variables from your configuration script in the `GetScript`, `TestScript`, or `SetScript` script blocks, use the `$using:` scope (see below for an example).</span></span>


## <a name="syntax"></a><span data-ttu-id="254ba-119">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="254ba-119">Syntax</span></span>

```
Script [string] #ResourceName
{
    GetScript = [string]
    SetScript = [string]
    TestScript = [string]
    [ Credential = [PSCredential] ]
    [ DependsOn = [string[]] ]
}
```

## <a name="properties"></a><span data-ttu-id="254ba-120">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="254ba-120">Properties</span></span>

|  <span data-ttu-id="254ba-121">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="254ba-121">Property</span></span>  |  <span data-ttu-id="254ba-122">Leírás</span><span class="sxs-lookup"><span data-stu-id="254ba-122">Description</span></span>   | 
|---|---| 
| <span data-ttu-id="254ba-123">GetScript</span><span class="sxs-lookup"><span data-stu-id="254ba-123">GetScript</span></span>| <span data-ttu-id="254ba-124">Biztosít egy adatblokk indításakor futó Windows PowerShell-parancsfájl a [Get-DscConfiguration](https://technet.microsoft.com/en-us/library/dn407379.aspx) parancsmag.</span><span class="sxs-lookup"><span data-stu-id="254ba-124">Provides a block of Windows PowerShell script that runs when you invoke the [Get-DscConfiguration](https://technet.microsoft.com/en-us/library/dn407379.aspx) cmdlet.</span></span> <span data-ttu-id="254ba-125">Ez a blokk egy kivonattáblát kell visszaadnia.</span><span class="sxs-lookup"><span data-stu-id="254ba-125">This block must return a hashtable.</span></span> <span data-ttu-id="254ba-126">A hashtable csak tartalmaznia kell egy key **eredmény** és az érték típusúnak kell lennie **karakterlánc**.</span><span class="sxs-lookup"><span data-stu-id="254ba-126">The hashtable must only contain one key **Result** and the value must be of type **String**.</span></span>| 
| <span data-ttu-id="254ba-127">SetScript</span><span class="sxs-lookup"><span data-stu-id="254ba-127">SetScript</span></span>| <span data-ttu-id="254ba-128">A Windows PowerShell-parancsfájl adatblokk biztosít.</span><span class="sxs-lookup"><span data-stu-id="254ba-128">Provides a block of Windows PowerShell script.</span></span> <span data-ttu-id="254ba-129">Ha meghívása a [Start-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx) parancsmag, a **TestScript** blokk első futtatja.</span><span class="sxs-lookup"><span data-stu-id="254ba-129">When you invoke the [Start-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx) cmdlet, the **TestScript** block runs first.</span></span> <span data-ttu-id="254ba-130">Ha a **TestScript** értéket ad vissza blokkolása **$false**, a **SetScript** blokk fog futni.</span><span class="sxs-lookup"><span data-stu-id="254ba-130">If the **TestScript** block returns **$false**, the **SetScript** block will run.</span></span> <span data-ttu-id="254ba-131">Ha a **TestScript** értéket ad vissza blokkolása **$true**, a **SetScript** blokk nem fog futni.</span><span class="sxs-lookup"><span data-stu-id="254ba-131">If the **TestScript** block returns **$true**, the **SetScript** block will not run.</span></span>| 
| <span data-ttu-id="254ba-132">TestScript</span><span class="sxs-lookup"><span data-stu-id="254ba-132">TestScript</span></span>| <span data-ttu-id="254ba-133">A Windows PowerShell-parancsfájl adatblokk biztosít.</span><span class="sxs-lookup"><span data-stu-id="254ba-133">Provides a block of Windows PowerShell script.</span></span> <span data-ttu-id="254ba-134">Ha meghívása a [Start-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx) parancsmag, ez a blokk futtatásakor.</span><span class="sxs-lookup"><span data-stu-id="254ba-134">When you invoke the [Start-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx) cmdlet, this block runs.</span></span> <span data-ttu-id="254ba-135">Ha a visszaadott érték **$false**, a SetScript blokk fog futni.</span><span class="sxs-lookup"><span data-stu-id="254ba-135">If it returns **$false**, the SetScript block will run.</span></span> <span data-ttu-id="254ba-136">Ha a visszaadott érték **$true**, SetScript blokk lesz, nem futnak.</span><span class="sxs-lookup"><span data-stu-id="254ba-136">If it returns **$true**, the SetScript block will not run.</span></span> <span data-ttu-id="254ba-137">A **TestScript** blokk is fut, indításakor a [teszt-DscConfiguration](https://technet.microsoft.com/en-us/library/dn407382.aspx) parancsmag.</span><span class="sxs-lookup"><span data-stu-id="254ba-137">The **TestScript** block also runs when you invoke the [Test-DscConfiguration](https://technet.microsoft.com/en-us/library/dn407382.aspx) cmdlet.</span></span> <span data-ttu-id="254ba-138">Azonban ebben az esetben az a **SetScript** blokk nem fogja futtatni, függetlenül attól, milyen értéket a TestScript blokkolása értéket ad vissza.</span><span class="sxs-lookup"><span data-stu-id="254ba-138">However, in this case, the **SetScript** block will not run, no matter what value the TestScript block returns.</span></span> <span data-ttu-id="254ba-139">A **TestScript** blokkot kell visszaadnia igaz, ha a tényleges konfigurációs megegyezik a jelenlegi kívánt állapot konfigurációs, és hamis értéket, ha nem felel meg.</span><span class="sxs-lookup"><span data-stu-id="254ba-139">The **TestScript** block must return True if the actual configuration matches the current desired state configuration, and False if it does not match.</span></span> <span data-ttu-id="254ba-140">(Az aktuális kívánt állapot az utolsó konfigurációját a csomópont által használt DSC helyeztek.)</span><span class="sxs-lookup"><span data-stu-id="254ba-140">(The current desired state configuration is the last configuration enacted on the node that is using DSC.)</span></span>| 
| <span data-ttu-id="254ba-141">hitelesítő adatok</span><span class="sxs-lookup"><span data-stu-id="254ba-141">Credential</span></span>| <span data-ttu-id="254ba-142">Azt jelzi, ha a hitelesítő adatok szükségesek a parancsfájl futtatásához használandó hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="254ba-142">Indicates the credentials to use for running this script, if credentials are required.</span></span>| 
| <span data-ttu-id="254ba-143">dependsOn</span><span class="sxs-lookup"><span data-stu-id="254ba-143">DependsOn</span></span>| <span data-ttu-id="254ba-144">Azt jelzi, hogy egy másik erőforrás konfigurációjának kell futtatni, mielőtt ehhez az erőforráshoz van konfigurálva.</span><span class="sxs-lookup"><span data-stu-id="254ba-144">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="254ba-145">Például, ha az erőforrás-konfiguráció azonosítója blokk futtatni kívánt parancsfájl első az **ResourceName** és annak típusa **ResourceType**, az e tulajdonság használatával szintaxisa a következő `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="254ba-145">For example, if the ID of the resource configuration script block that you want to run first is **ResourceName** and its type is **ResourceType**, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>

## <a name="example-1"></a><span data-ttu-id="254ba-146">1. példa</span><span class="sxs-lookup"><span data-stu-id="254ba-146">Example 1</span></span>
```powershell
$version = Get-Content 'version.txt'

Configuration ScriptTest
{
    Import-DscResource –ModuleName 'PSDesiredStateConfiguration'

    Script ScriptExample
    {
        SetScript = 
        { 
            $sw = New-Object System.IO.StreamWriter("C:\TempFolder\TestFile.txt")
            $sw.WriteLine("Some sample string")
            $sw.Close()
        }
        TestScript = { Test-Path "C:\TempFolder\TestFile.txt" }
        GetScript = { @{ Result = (Get-Content C:\TempFolder\TestFile.txt) } }          
    }
}
```

## <a name="example-2"></a><span data-ttu-id="254ba-147">2. példa</span><span class="sxs-lookup"><span data-stu-id="254ba-147">Example 2</span></span>
```powershell
$version = Get-Content 'version.txt'

Configuration ScriptTest
{
    Import-DscResource –ModuleName 'PSDesiredStateConfiguration'

    Script UpdateConfigurationVersion
    {
        GetScript = { 
            $currentVersion = Get-Content (Join-Path -Path $env:SYSTEMDRIVE -ChildPath 'version.txt')
            return @{ 'Version' = "$currentVersion" }
        }          
        TestScript = { 
            $state = $GetScript
            if( $state['Version'] -eq $using:version )
            {
                Write-Verbose -Message ('{0} -eq {1}' -f $state['Version'],$using:version)
                return $true
            }
            Write-Verbose -Message ('Version up-to-date: {0}' -f $using:version)
            return $false
        }
        SetScript = { 
            $using:version | Set-Content -Path (Join-Path -Path $env:SYSTEMDRIVE -ChildPath 'version.txt')
        }
    }
}
```

<span data-ttu-id="254ba-148">Ehhez az erőforráshoz a konfigurációs verzió ír egy szövegfájlba.</span><span class="sxs-lookup"><span data-stu-id="254ba-148">This resource is writing the configuration's version to a text file.</span></span> <span data-ttu-id="254ba-149">Ebben a verzióban érhető el az ügyfélszámítógépen, de nem a csomópontok egyikén, ezért az egyes átadni rendelkezik a `Script` a PowerShell parancsfájl-blokkokban erőforrás `using` hatókör.</span><span class="sxs-lookup"><span data-stu-id="254ba-149">This version is available on the client computer, but isn't on any of the nodes, so it has to be passed to each of the `Script` resource's script blocks with PowerShell's `using` scope.</span></span> <span data-ttu-id="254ba-150">Amikor a csomópont MOF létrehozása a fájl, értékét a `$version` változó olvasható ki egy szövegfájlból, az ügyfélszámítógépen.</span><span class="sxs-lookup"><span data-stu-id="254ba-150">When generating the node's MOF file, the value of the `$version` variable is read from a text file on the client computer.</span></span> <span data-ttu-id="254ba-151">A DSC cserél a `$using:version` minden parancsprogram változók értékét letiltása a `$version` változó.</span><span class="sxs-lookup"><span data-stu-id="254ba-151">DSC replaces the `$using:version` variables in each script block with the value of the `$version` variable.</span></span>

