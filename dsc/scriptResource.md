---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "A DSC-parancsfájl-erőforrás"
ms.openlocfilehash: 22213b74986b45b3a8205f1584b3b0d89a92f211
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 01/17/2018
---
# <a name="dsc-script-resource"></a>A DSC-parancsfájl-erőforrás

 
> Vonatkozik: A Windows PowerShell 4.0-s verzióját, a Windows PowerShell 5.0

A **parancsfájl** erőforrás a Windows PowerShell szükséges konfiguráló (DSC) lehetővé teszi a Windows PowerShell parancsfájl-blokkokban futtathatnak célcsomópontokat. A `Script` erőforrás `GetScript`, `SetScript`, és `TestScript` tulajdonságok. Ezeket a tulajdonságokat meg kell minden egyes cél csomóponton futó parancsfájl-blokkokban. 

A `GetScript` parancsprogram-blokkot kell visszaadnia egy kivonattáblát az aktuális csomópont állapotát jelző. A hashtable csak tartalmaznia kell egy key `Result` és az érték típusúnak kell lennie `String`. Visszaadandó semmit nem szükséges. A DSC-ből nem minden kimenetét a script blokkból.

A `TestScript` parancsprogram-blokkot kell meghatározni, hogy az aktuális csomópont módosítani kell-e. Az kell visszaadnia `$true` Ha a csomópont naprakész. Az kell visszaadnia `$false` Ha a csomópont-konfiguráció elavult, és amelyet frissíteni kell a `SetScript` parancsprogram-blokkot tartalmazzon. A `TestScript` DSC hívja parancsprogram-blokkot tartalmazzon.

A `SetScript` parancsprogram-blokkot kell módosítani a csomópont. Azt nevezzük DSC által, ha a `TestScript` visszatérési blokkolása `$false`.

Ha szeretné-e a konfigurációs parancsprogram a változók használata a `GetScript`, `TestScript`, vagy `SetScript` parancsfájl-blokkokban, használja a `$using:` hatókör (lásd lent példát).


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

## <a name="properties"></a>Tulajdonságok

|  Tulajdonság  |  Leírás   | 
|---|---| 
| GetScript| Biztosít egy adatblokk indításakor futó Windows PowerShell-parancsfájl a [Get-DscConfiguration](https://technet.microsoft.com/en-us/library/dn407379.aspx) parancsmag. Ez a blokk egy kivonattáblát kell visszaadnia. A hashtable csak tartalmaznia kell egy key **eredmény** és az érték típusúnak kell lennie **karakterlánc**.| 
| SetScript| A Windows PowerShell-parancsfájl adatblokk biztosít. Ha meghívása a [Start-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx) parancsmag, a **TestScript** blokk első futtatja. Ha a **TestScript** értéket ad vissza blokkolása **$false**, a **SetScript** blokk fog futni. Ha a **TestScript** értéket ad vissza blokkolása **$true**, a **SetScript** blokk nem fog futni.| 
| TestScript| A Windows PowerShell-parancsfájl adatblokk biztosít. Ha meghívása a [Start-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx) parancsmag, ez a blokk futtatásakor. Ha a visszaadott érték **$false**, a SetScript blokk fog futni. Ha a visszaadott érték **$true**, SetScript blokk lesz, nem futnak. A **TestScript** blokk is fut, indításakor a [teszt-DscConfiguration](https://technet.microsoft.com/en-us/library/dn407382.aspx) parancsmag. Azonban ebben az esetben az a **SetScript** blokk nem fogja futtatni, függetlenül attól, milyen értéket a TestScript blokkolása értéket ad vissza. A **TestScript** blokkot kell visszaadnia igaz, ha a tényleges konfigurációs megegyezik a jelenlegi kívánt állapot konfigurációs, és hamis értéket, ha nem felel meg. (Az aktuális kívánt állapot az utolsó konfigurációját a csomópont által használt DSC helyeztek.)| 
| hitelesítő adatok| Azt jelzi, ha a hitelesítő adatok szükségesek a parancsfájl futtatásához használandó hitelesítő adatok.| 
| dependsOn| Azt jelzi, hogy egy másik erőforrás konfigurációjának kell futtatni, mielőtt ehhez az erőforráshoz van konfigurálva. Például, ha az erőforrás-konfiguráció azonosítója blokk futtatni kívánt parancsfájl első az **ResourceName** és annak típusa **ResourceType**, az e tulajdonság használatával szintaxisa a következő `DependsOn = "[ResourceType]ResourceName"`.

## <a name="example-1"></a>1. példa
```powershell
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

## <a name="example-2"></a>2. példa
```powershell
$version = Get-Content 'version.txt'

Configuration ScriptTest
{
    Import-DscResource –ModuleName 'PSDesiredStateConfiguration'

    Script UpdateConfigurationVersion
    {
        GetScript = { 
            $currentVersion = Get-Content (Join-Path -Path $env:SYSTEMDRIVE -ChildPath 'version.txt')
            return @{ 'Result' = "$currentVersion" }
        }          
        TestScript = { 
            $state = $GetScript
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
```

Ehhez az erőforráshoz a konfigurációs verzió ír egy szövegfájlba. Ebben a verzióban érhető el az ügyfélszámítógépen, de nem a csomópontok egyikén, ezért az egyes átadni rendelkezik a `Script` a PowerShell parancsfájl-blokkokban erőforrás `using` hatókör. Amikor a csomópont MOF létrehozása a fájl, értékét a `$version` változó olvasható ki egy szövegfájlból, az ügyfélszámítógépen. A DSC cserél a `$using:version` minden parancsprogram változók értékét letiltása a `$version` változó.

