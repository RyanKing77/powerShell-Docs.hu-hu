---
ms.date: 08/24/2018
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC-Script erőforrás
ms.openlocfilehash: 4eee5625add4d96ade7ababf7f534f597a26712d
ms.sourcegitcommit: 0ca836d1044e46d3a7dcbc69fa93d84f74848559
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/04/2019
ms.locfileid: "58920356"
---
# <a name="dsc-script-resource"></a><span data-ttu-id="9709d-103">DSC-Script erőforrás</span><span class="sxs-lookup"><span data-stu-id="9709d-103">DSC Script Resource</span></span>

> <span data-ttu-id="9709d-104">Érvényes: Windows PowerShell 4.0-s, a Windows PowerShell 5.x</span><span class="sxs-lookup"><span data-stu-id="9709d-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.x</span></span>

<span data-ttu-id="9709d-105">A **parancsfájl** erőforrás a Windows PowerShell Desired State Configuration (DSC) csomópontokon való futtatáshoz Windows PowerShell parancsfájl-blokkokban cél mechanizmust biztosít.</span><span class="sxs-lookup"><span data-stu-id="9709d-105">The **Script** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to run Windows PowerShell script blocks on target nodes.</span></span> <span data-ttu-id="9709d-106">A **parancsfájl** erőforrás-felhasználási `GetScript`, `SetScript`, és `TestScript` való hajtsa végre a megfelelő DSC parancsfájl-blokkokban tartalmazó tulajdonságok állapot műveleteket.</span><span class="sxs-lookup"><span data-stu-id="9709d-106">The **Script** resource uses `GetScript`, `SetScript`, and `TestScript` properties that contain script blocks you define to perform the corresponding DSC state operations.</span></span>

## <a name="syntax"></a><span data-ttu-id="9709d-107">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="9709d-107">Syntax</span></span>

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

> [!NOTE]
> <span data-ttu-id="9709d-108">A `GetScript`, `TestScript`, és `SetScript` karakterláncok blokkok tárolni.</span><span class="sxs-lookup"><span data-stu-id="9709d-108">The `GetScript`, `TestScript`, and `SetScript` blocks are stored as strings.</span></span>

## <a name="properties"></a><span data-ttu-id="9709d-109">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="9709d-109">Properties</span></span>

|<span data-ttu-id="9709d-110">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="9709d-110">Property</span></span>|<span data-ttu-id="9709d-111">Leírás</span><span class="sxs-lookup"><span data-stu-id="9709d-111">Description</span></span>|
|--------|-----------|
|<span data-ttu-id="9709d-112">GetScript</span><span class="sxs-lookup"><span data-stu-id="9709d-112">GetScript</span></span>|<span data-ttu-id="9709d-113">Parancsprogram-blokkot, amely a csomópont aktuális állapotát adja vissza.</span><span class="sxs-lookup"><span data-stu-id="9709d-113">A script block that returns the current state of the Node.</span></span>|
|<span data-ttu-id="9709d-114">SetScript</span><span class="sxs-lookup"><span data-stu-id="9709d-114">SetScript</span></span>|<span data-ttu-id="9709d-115">Parancsprogram-blokkot DSC használó, kényszerítse a megfelelőséget, amikor a csomópont nem a kívánt állapotban van.</span><span class="sxs-lookup"><span data-stu-id="9709d-115">A script block that DSC uses to enforce compliance when the Node is not in the desired state.</span></span>|
|<span data-ttu-id="9709d-116">TestScript</span><span class="sxs-lookup"><span data-stu-id="9709d-116">TestScript</span></span>|<span data-ttu-id="9709d-117">Parancsprogram-blokkot, amely meghatározza, hogy a csomópont a kívánt állapotban van.</span><span class="sxs-lookup"><span data-stu-id="9709d-117">A script block that determines if the Node is in the desired state.</span></span>|
|<span data-ttu-id="9709d-118">Hitelesítő adatok</span><span class="sxs-lookup"><span data-stu-id="9709d-118">Credential</span></span>| <span data-ttu-id="9709d-119">Azt jelzi, ha a hitelesítő adatok szükségesek a szkript futtatásához használandó hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="9709d-119">Indicates the credentials to use for running this script, if credentials are required.</span></span>|
|<span data-ttu-id="9709d-120">DependsOn</span><span class="sxs-lookup"><span data-stu-id="9709d-120">DependsOn</span></span>| <span data-ttu-id="9709d-121">Azt jelzi, hogy a konfigurációt egy másik erőforrás futtatnia kell, mielőtt az erőforrás konfigurálva van.</span><span class="sxs-lookup"><span data-stu-id="9709d-121">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="9709d-122">Például, ha az erőforrás-konfiguráció azonosítója letiltása, a futtatni kívánt parancsfájl először van **ResourceName** és a típusa **ResourceType**, ez a tulajdonság használata esetén `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="9709d-122">For example, if the ID of the resource configuration script block that you want to run first is **ResourceName** and its type is **ResourceType**, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>

### <a name="getscript"></a><span data-ttu-id="9709d-123">GetScript</span><span class="sxs-lookup"><span data-stu-id="9709d-123">GetScript</span></span>

<span data-ttu-id="9709d-124">DSC nem használja a kimenetét `GetScript`.</span><span class="sxs-lookup"><span data-stu-id="9709d-124">DSC does not use the output from `GetScript`.</span></span> <span data-ttu-id="9709d-125">A [Get-DscConfiguration](/powershell/module/PSDesiredStateConfiguration/Get-DscConfiguration) parancsmag végrehajtja a `GetScript` a csomópont aktuális állapotának beolvasására tett.</span><span class="sxs-lookup"><span data-stu-id="9709d-125">The [Get-DscConfiguration](/powershell/module/PSDesiredStateConfiguration/Get-DscConfiguration) cmdlet executes the `GetScript` to retrieve a node's current state.</span></span> <span data-ttu-id="9709d-126">Visszatérési értéket nem kötelező a `GetScript`.</span><span class="sxs-lookup"><span data-stu-id="9709d-126">A return value is not required from `GetScript`.</span></span> <span data-ttu-id="9709d-127">Ha megad egy visszatérési értéket, kell lennie egy `hashtable` tartalmazó egy **eredmény** kulcsot, amelynek az értéke egy `String`.</span><span class="sxs-lookup"><span data-stu-id="9709d-127">If you specify a return value, it must be a `hashtable` containing a **Result** key whose value is a `String`.</span></span>

### <a name="testscript"></a><span data-ttu-id="9709d-128">TestScript</span><span class="sxs-lookup"><span data-stu-id="9709d-128">TestScript</span></span>

<span data-ttu-id="9709d-129">A `TestScript` határozza meg, hogy DSC által végrehajtott a `SetScript` kell futtatni.</span><span class="sxs-lookup"><span data-stu-id="9709d-129">The `TestScript` is executed by DSC to determine if the `SetScript` should be run.</span></span> <span data-ttu-id="9709d-130">Ha a `TestScript` adja vissza `$false`, DSC végrehajtja a `SetScript` ahhoz, hogy a csomópont a kívánt állapotra.</span><span class="sxs-lookup"><span data-stu-id="9709d-130">If the `TestScript` returns `$false`, DSC executes the `SetScript` to bring the node back to the desired state.</span></span> <span data-ttu-id="9709d-131">Kell visszaadnia egy `boolean` értéket.</span><span class="sxs-lookup"><span data-stu-id="9709d-131">It must return a `boolean` value.</span></span> <span data-ttu-id="9709d-132">Eredménye `$true` azt jelzi, hogy a csomópont megfelelő és `SetScript` nem kell végrehajtani.</span><span class="sxs-lookup"><span data-stu-id="9709d-132">A result of `$true` indicates that the node is compliant and `SetScript` should not executed.</span></span>

<span data-ttu-id="9709d-133">A [a Test-DscConfiguration](/powershell/module/PSDesiredStateConfiguration/Test-DscConfiguration) parancsmag végrehajtja a `TestScript` csomópontok megfelelnek-e lekérni a **parancsfájl** erőforrásokat.</span><span class="sxs-lookup"><span data-stu-id="9709d-133">The [Test-DscConfiguration](/powershell/module/PSDesiredStateConfiguration/Test-DscConfiguration) cmdlet, executes the `TestScript` to retrieve the nodes compliance with the  **Script** resources.</span></span> <span data-ttu-id="9709d-134">Azonban ebben az esetben az a `SetScript` nem fut, függetlenül attól, hogy mi a `TestScript` letiltása értéket ad vissza.</span><span class="sxs-lookup"><span data-stu-id="9709d-134">However, in this case, the `SetScript` does not run, no matter what the `TestScript` block returns.</span></span>

> [!NOTE]
> <span data-ttu-id="9709d-135">Minden kimenetének a `TestScript` része, a visszaadott érték.</span><span class="sxs-lookup"><span data-stu-id="9709d-135">All output from your `TestScript` is part of its return value.</span></span> <span data-ttu-id="9709d-136">PowerShell unsuppressed kimeneti adatok nullától eltérő, ami azt jelenti, amely értelmezi a `TestScript` adja vissza `$true` függetlenül a csomópont állapota.</span><span class="sxs-lookup"><span data-stu-id="9709d-136">PowerShell interprets unsuppressed output as non-zero, which means that your `TestScript` will return `$true` regardless of your node's state.</span></span>
> <span data-ttu-id="9709d-137">Ez kiszámíthatatlan következményekkel járhat, téves, eredményez, és nehézséget okoz a hibaelhárítás során.</span><span class="sxs-lookup"><span data-stu-id="9709d-137">This results in unpredictable results, false positives, and causes difficulty during troubleshooting.</span></span>

### <a name="setscript"></a><span data-ttu-id="9709d-138">SetScript</span><span class="sxs-lookup"><span data-stu-id="9709d-138">SetScript</span></span>

<span data-ttu-id="9709d-139">A `SetScript` módosítja a csomópont a kívánt állapotban kényszerítésére.</span><span class="sxs-lookup"><span data-stu-id="9709d-139">The `SetScript` modifies the node to enforce the desired state.</span></span> <span data-ttu-id="9709d-140">Azt nevezzük DSC szerint, ha a `TestScript` parancsfájl-blokk értéket ad vissza `$false`.</span><span class="sxs-lookup"><span data-stu-id="9709d-140">It is called by DSC if the `TestScript` script block returns `$false`.</span></span> <span data-ttu-id="9709d-141">A `SetScript` kell nem tartozik visszaadott érték.</span><span class="sxs-lookup"><span data-stu-id="9709d-141">The `SetScript` should have no return value.</span></span>

## <a name="examples"></a><span data-ttu-id="9709d-142">Példák</span><span class="sxs-lookup"><span data-stu-id="9709d-142">Examples</span></span>

### <a name="example-1-write-sample-text-using-a-script-resource"></a><span data-ttu-id="9709d-143">1. példa: Szövegminta használatával egy parancsfájl-erőforrás írása</span><span class="sxs-lookup"><span data-stu-id="9709d-143">Example 1: Write sample text using a Script resource</span></span>

<span data-ttu-id="9709d-144">Ebben a példában megvizsgálja, hogy létezik-e `C:\TempFolder\TestFile.txt` minden egyes csomóponton.</span><span class="sxs-lookup"><span data-stu-id="9709d-144">This example tests for the existence of `C:\TempFolder\TestFile.txt` on each node.</span></span> <span data-ttu-id="9709d-145">Ha még nem létezik, akkor használatával létrehozza a `SetScript`.</span><span class="sxs-lookup"><span data-stu-id="9709d-145">If it does not exist, it creates it using the `SetScript`.</span></span> <span data-ttu-id="9709d-146">A `GetScript` nem használatos a fájlt, és a visszaadott érték tartalmát adja vissza.</span><span class="sxs-lookup"><span data-stu-id="9709d-146">The `GetScript` returns the contents of the file, and its return value is not used.</span></span>

```powershell
Configuration ScriptTest
{
    Import-DscResource -ModuleName 'PSDesiredStateConfiguration'

    Node localhost
    {
        Script ScriptExample
        {
            SetScript = {
                $sw = New-Object System.IO.StreamWriter("C:\TempFolder\TestFile.txt")
                $sw.WriteLine("Some sample string")
                $sw.Close()
            }
            TestScript = { Test-Path "C:\TempFolder\TestFile.txt" }
            GetScript = { @{ Result = (Get-Content C:\TempFolder\TestFile.txt) } }
        }
    }
}
```

### <a name="example-2-compare-version-information-using-a-script-resource"></a><span data-ttu-id="9709d-147">2. példa: Script erőforrás használatával fájlverzió-információkat összehasonlítása</span><span class="sxs-lookup"><span data-stu-id="9709d-147">Example 2: Compare version information using a Script resource</span></span>

<span data-ttu-id="9709d-148">Ez a példa lekéri a *megfelelő* fájlverzió-információkat a szerzői műveletekhez részben számítógépen szöveges fájlból, és tárolja azokat az a `$version` változó.</span><span class="sxs-lookup"><span data-stu-id="9709d-148">This example retrieves the *compliant* version information from a text file on the authoring computer and stores it in the `$version` variable.</span></span> <span data-ttu-id="9709d-149">A csomópont MOF-fájl létrehozása, DSC helyettesíti a `$using:version` változók minden parancsprogram a következő értékkel: blokkolja a `$version` változó.</span><span class="sxs-lookup"><span data-stu-id="9709d-149">When generating the node's MOF file, DSC replaces the `$using:version` variables in each script block with the value of the `$version` variable.</span></span> <span data-ttu-id="9709d-150">A futtatás során a *megfelelő* verzió minden csomóponton egy szöveges fájlban és képest, és az azt követő végrehajtások frissített.</span><span class="sxs-lookup"><span data-stu-id="9709d-150">During execution, the *compliant* version is stored in a text file on each Node and compared and updated on subsequent executions.</span></span>

```powershell
$version = Get-Content 'version.txt'

Configuration ScriptTest
{
    Import-DscResource -ModuleName 'PSDesiredStateConfiguration'

    Node localhost
    {
        Script UpdateConfigurationVersion
        {
            GetScript = {
                $currentVersion = Get-Content (Join-Path -Path $env:SYSTEMDRIVE -ChildPath 'version.txt')
                return @{ 'Result' = "$currentVersion" }
            }
            TestScript = {
                # Create and invoke a scriptblock using the $GetScript automatic variable, which contains a string representation of the GetScript.
                $state = [scriptblock]::Create($GetScript).Invoke()

                if( $state['Result'] -eq $using:version )
                {
                    Write-Verbose -Message ('{0} -eq {1}' -f $state['Result'],$using:version)
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
}
```
