---
ms.date: 08/24/2018
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC-Script erőforrás
ms.openlocfilehash: 4eee5625add4d96ade7ababf7f534f597a26712d
ms.sourcegitcommit: f4bd4e116e22c8b5bfcb61680a7c42e58b4da93e
ms.translationtype: HT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/22/2019
ms.locfileid: "59984289"
---
# <a name="dsc-script-resource"></a>DSC-Script erőforrás

> A következőkre vonatkozik: Windows PowerShell 4.0-s, a Windows PowerShell 5.x

A **parancsfájl** erőforrás a Windows PowerShell Desired State Configuration (DSC) csomópontokon való futtatáshoz Windows PowerShell parancsfájl-blokkokban cél mechanizmust biztosít. A **parancsfájl** erőforrás-felhasználási `GetScript`, `SetScript`, és `TestScript` való hajtsa végre a megfelelő DSC parancsfájl-blokkokban tartalmazó tulajdonságok állapot műveleteket.

## <a name="syntax"></a>Szintaxis

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
> A `GetScript`, `TestScript`, és `SetScript` karakterláncok blokkok tárolni.

## <a name="properties"></a>Tulajdonságok

|Tulajdonság|Leírás|
|--------|-----------|
|GetScript|Parancsprogram-blokkot, amely a csomópont aktuális állapotát adja vissza.|
|SetScript|Parancsprogram-blokkot DSC használó, kényszerítse a megfelelőséget, amikor a csomópont nem a kívánt állapotban van.|
|TestScript|Parancsprogram-blokkot, amely meghatározza, hogy a csomópont a kívánt állapotban van.|
|Hitelesítő adatok| Azt jelzi, ha a hitelesítő adatok szükségesek a szkript futtatásához használandó hitelesítő adatok.|
|DependsOn| Azt jelzi, hogy a konfigurációt egy másik erőforrás futtatnia kell, mielőtt az erőforrás konfigurálva van. Például, ha az erőforrás-konfiguráció azonosítója letiltása, a futtatni kívánt parancsfájl először van **ResourceName** és a típusa **ResourceType**, ez a tulajdonság használata esetén `DependsOn = "[ResourceType]ResourceName"`.

### <a name="getscript"></a>GetScript

DSC nem használja a kimenetét `GetScript`. A [Get-DscConfiguration](/powershell/module/PSDesiredStateConfiguration/Get-DscConfiguration) parancsmag végrehajtja a `GetScript` a csomópont aktuális állapotának beolvasására tett. Visszatérési értéket nem kötelező a `GetScript`. Ha megad egy visszatérési értéket, kell lennie egy `hashtable` tartalmazó egy **eredmény** kulcsot, amelynek az értéke egy `String`.

### <a name="testscript"></a>TestScript

A `TestScript` határozza meg, hogy DSC által végrehajtott a `SetScript` kell futtatni. Ha a `TestScript` adja vissza `$false`, DSC végrehajtja a `SetScript` ahhoz, hogy a csomópont a kívánt állapotra. Kell visszaadnia egy `boolean` értéket. Eredménye `$true` azt jelzi, hogy a csomópont megfelelő és `SetScript` nem kell végrehajtani.

A [a Test-DscConfiguration](/powershell/module/PSDesiredStateConfiguration/Test-DscConfiguration) parancsmag végrehajtja a `TestScript` csomópontok megfelelnek-e lekérni a **parancsfájl** erőforrásokat. Azonban ebben az esetben az a `SetScript` nem fut, függetlenül attól, hogy mi a `TestScript` letiltása értéket ad vissza.

> [!NOTE]
> Minden kimenetének a `TestScript` része, a visszaadott érték. PowerShell unsuppressed kimeneti adatok nullától eltérő, ami azt jelenti, amely értelmezi a `TestScript` adja vissza `$true` függetlenül a csomópont állapota.
> Ez kiszámíthatatlan következményekkel járhat, téves, eredményez, és nehézséget okoz a hibaelhárítás során.

### <a name="setscript"></a>SetScript

A `SetScript` módosítja a csomópont a kívánt állapotban kényszerítésére. Azt nevezzük DSC szerint, ha a `TestScript` parancsfájl-blokk értéket ad vissza `$false`. A `SetScript` kell nem tartozik visszaadott érték.

## <a name="examples"></a>Példák

### <a name="example-1-write-sample-text-using-a-script-resource"></a>1. példa: Szövegminta használatával egy parancsfájl-erőforrás írása

Ebben a példában megvizsgálja, hogy létezik-e `C:\TempFolder\TestFile.txt` minden egyes csomóponton. Ha még nem létezik, akkor használatával létrehozza a `SetScript`. A `GetScript` nem használatos a fájlt, és a visszaadott érték tartalmát adja vissza.

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

### <a name="example-2-compare-version-information-using-a-script-resource"></a>2. példa: Script erőforrás használatával fájlverzió-információkat összehasonlítása

Ez a példa lekéri a *megfelelő* fájlverzió-információkat a szerzői műveletekhez részben számítógépen szöveges fájlból, és tárolja azokat az a `$version` változó. A csomópont MOF-fájl létrehozása, DSC helyettesíti a `$using:version` változók minden parancsprogram a következő értékkel: blokkolja a `$version` változó. A futtatás során a *megfelelő* verzió minden csomóponton egy szöveges fájlban és képest, és az azt követő végrehajtások frissített.

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
