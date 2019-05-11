---
title: Egy PowerShell-modul telepítése |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: fb82827e-fdb7-4cbf-b3d4-093e72b3ff0e
caps.latest.revision: 28
ms.openlocfilehash: 60ac4bf9089232a9fa879e835e32da53422489fd
ms.sourcegitcommit: 58fb23c854f5a8b40ad1f952d3323aeeccac7a24
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/07/2019
ms.locfileid: "65229447"
---
# <a name="installing-a-powershell-module"></a>PowerShell-modul telepítése

Miután létrehozta a PowerShell-modult, valószínűleg érdemes a modul telepítése a rendszerben, hogy Ön vagy mások által a előfordulhat, hogy használhassák. Általánosan fogalmazva ez áll a modul fájlok másolása (ie, a .psm1 vagy bináris szerelvény, a moduljegyzékben és a kapcsolódó fájlokat) egy könyvtárat a számítógépen. Nagyon kis projekthez másolása és beillesztése a fájlokat egy távoli számítógépen; a Windows Explorer egyszerűen lehet azonban nagyobb megoldások, előfordulhat, hogy szeretne használni egy bonyolultabb telepítési folyamatot. Függetlenül attól, hogyan juthat a modul be a rendszerbe a PowerShell használhatja módszer, amely lehetővé teszi a felhasználók kereséséhez és a modulok használatához. Ezért a telepítés fő probléma annak ellenőrzése, hogy a modul talált lesz-e a PowerShell. További információkért lásd: [egy PowerShell-modul importálása](./importing-a-powershell-module.md).

## <a name="rules-for-installing-modules"></a>Modulok telepítésére vonatkozó szabályok

A következő információkat az összes modult, hogy hoz létre a saját használja, a modulok von le más felektől származó és a modulok hozzá mások vonatkozik.

### <a name="install-modules-in-psmodulepath"></a>A PSModulePath modulok telepítése

Amikor csak lehetséges, az összes modulok telepítéséhez az elérési utat, amely szerepel a **PSModulePath** környezeti változót, vagy adja hozzá a modul elérési útja a **PSModulePath** környezeti változó értékét.

A **PSModulePath** környezeti változót ($Env: PSModulePath) a Windows PowerShell-modulok helyeket tartalmaz. Parancsmagok támaszkodnak található modulok a környezeti változó értékét.

Alapértelmezés szerint a **PSModulePath** környezeti változó értékét a következő rendszert és a felhasználói modul könyvtárakat tartalmazza, de a hozzá, és szerkessze a értéket.

- `$PSHome\Modules` (%Windir%\System32\WindowsPowerShell\v1.0\Modules)

  > [!WARNING]
  > Ez a hely modulok, a Windows számára van fenntartva. Ne telepítse a modulok ezen a helyen.

- `$Home\Documents\WindowsPowerShell\Modules` (% UserProfile%\Documents\WindowsPowerShell\Modules)

- `$Env:ProgramFiles\WindowsPowerShell\Modules` (%ProgramFiles%\WindowsPowerShell\Modules)

  Értékének beolvasásához a **PSModulePath** környezeti változót, használja a következő parancsok egyikét.

  ```powershell
  $Env:PSModulePath
  [Environment]::GetEnvironmentVariable("PSModulePath")
  ```

  Vegye fel a modul elérési utat értékét a **PSModulePath** környezeti változó értékét, használja a következő parancs formátuma. Ezt a formátumot használja a **SetEnvironmentVariable** módszere a **System.Environment** munkamenet független módosítást az osztály a **PSModulePath** környezet a változó.

  ```powershell
  #Save the current value in the $p variable.
  $p = [Environment]::GetEnvironmentVariable("PSModulePath")

  #Add the new path to the $p variable. Begin with a semi-colon separator.
  $p += ";C:\Program Files (x86)\MyCompany\Modules\"

  #Add the paths in $p to the PSModulePath value.
  [Environment]::SetEnvironmentVariable("PSModulePath",$p)

  ```

  > [!IMPORTANT]
  > Miután hozzáadta az elérési útját **PSModulePath**, meg kell szórási egy környezet üzenet-változásról. Teszi közzé a módosítás lehetővé teszi, hogy más alkalmazások, például a rendszerhéj, a módosítás átvételéhez. Küldi el a módosítást, hogy rendelkezik a termék telepítési kód küldése egy **WM_SETTINGCHANGE** üzenet `lParam` állítsa be a "Környezet" karakterláncot. Ügyeljen arra, hogy az üzenet elküldése után a modul telepítési kód frissített **PSModulePath**.

### <a name="use-the-correct-module-directory-name"></a>Használja a megfelelő modul könyvtár neve

Egy megfelelően formázott modul az a modul, amely rendelkezik legalább egy fájlt a modulkönyvtárat alapneveként megegyező nevű címtárban tárolt. Ha egy modul nem megfelelően formázott, Windows PowerShell nem ismeri fel modulként.

A "base"fájl nevéhez, az a név nélkül a fájlnévkiterjesztést. Egy megfelelően formázott modulban neve a modul fájlokat tartalmazó könyvtárba egyeznie kell legalább egy fájlt a modul alapneveként.

Például a minta a Fabrikam modul, a modul fájlt tartalmazó könyvtár neve a "Fabrikam", legalább egy fájlt a "Fabrikam" alap neve. Ebben az esetben Fabrikam.psd1 és Fabrikam.dll is rendelkezik a "Fabrikam" alapnévvel.

```
C:\Program Files
  Fabrikam Technologies
    Fabrikam Manager
      Modules
        Fabrikam
          Fabrikam.psd1 (module manifest)
          Fabrikam.dll (module assembly)

```

### <a name="effect-of-incorrect-installation"></a>Helytelen telepítés hatása

Ha a modul nem megfelelően formázott és a hely értékét nem szerepel a **PSModulePath** nem működnek a környezeti változót, például a következő Windows PowerShell-lel, alapvető felderítési funkcióit.

- A modul automatikus telepítési szolgáltatás nem tudja automatikusan importálja a modult.

- A `ListAvailable` paraméterében a [Get-Module](/powershell/module/Microsoft.PowerShell.Core/Get-Module) parancsmag a modul nem található.

- A [Import-Module](/powershell/module/Microsoft.PowerShell.Core/Import-Module) parancsmag a modul nem található. Importálja a modult, meg kell adnia a legfelső szintű modul fájl vagy a modul Alkalmazásjegyzék-fájl teljes elérési útja.

  Egyéb hasznos segédanyaghoz, például a következő, nem működnek, ha a modul importálása a munkamenetbe. A megfelelően formázott modulok a **PSModulePath** környezeti változót, ezek a szolgáltatások munkahelyi akkor is, ha a modul nincs importálva a munkamenetbe.

- A [Get-Command](/powershell/module/Microsoft.PowerShell.Core/Get-Command) parancsmag parancsok a modul nem található.

- A [Update-Help](/powershell/module/Microsoft.PowerShell.Core/Update-Help) és [Save-Help](/powershell/module/Microsoft.PowerShell.Core/Save-Help) parancsmagok nem frissíthető, és mentse a modul súgójában.

- A [Show-parancs](/powershell/module/Microsoft.PowerShell.Utility/Show-Command) parancsmag nem található, és megjeleníti a parancsok a modulban.

  A parancsok a modul hiányoznak a `Show-Command` a Windows PowerShell integrált parancsfájlkezelési környezet (ISE) ablak.

## <a name="where-to-install-modules"></a>Hol-modulok telepítése

Ez a szakasz azt ismerteti, hol a fájlrendszer, a Windows PowerShell-modulok telepítéséhez. A hely attól függ, a modul használatáról.

### <a name="installing-modules-for-a-specific-user"></a>Egy adott felhasználó modulok telepítése

Hozzon létre saját modult, vagy a modul le egy másik entitás, például a Windows PowerShell-Közösség webhelyén, és azt szeretné, hogy a modul csak a felhasználói fiókjához elérhető legyen, ha a modul telepítése a felhasználó-specifikus modulokat címtárban.

`$home\Documents\WindowsPowerShell\Modules\<Module Folder>\<Module Files>`

A felhasználó-specifikus modulokat könyvtár értéke kerül a **PSModulePath** alapértelmezés szerint a környezeti változót.

### <a name="installing-modules-for-all-users-in-program-files"></a>Az összes felhasználó számára a Program Files modulok telepítése

Ha azt szeretné, hogy a számítógép minden felhasználója számára elérhetővé válnak a modul, a modul a Program Files helyre fogja telepíteni.

`$Env:ProgramFiles\WindowsPowerShell\Modules\<Module Folder>\<Module Files>`

> [!NOTE]
> A Windows PowerShell 4.0-s és újabb verziók alapértelmezés szerint a Program Files helyen a PSModulePath környezeti változó értéke kerül. Windows PowerShell korábbi verziói esetén manuálisan létrehozhat a Program Files helyen ((%ProgramFiles%\WindowsPowerShell\Modules) és az elérési út hozzáadása a PSModulePath környezeti változót a fent leírtak szerint.

### <a name="installing-modules-in-a-product-directory"></a>Egy termék könyvtárban modulok telepítése

Ha a modul más felek terjeszti, használja az alapértelmezett Program Files helyet a fent leírt, vagy saját a vállalatra jellemző vagy a termékspecifikus alkönyvtára a % ProgramFiles % könyvtár létrehozása.

A Fabrikam technológiák, egy fiktív vállalat, például egy Windows PowerShell-modul Fabrikam Manager termékük van szállítási. A modul telepítője modulok alkönyvtárban a Fabrikam Manager termék alkönyvtár hoz létre.

```
C:\Program Files
  Fabrikam Technologies
    Fabrikam Manager
      Modules
        Fabrikam
          Fabrikam.psd1 (module manifest)
          Fabrikam.dll (module assembly)

```

Ahhoz, hogy a Windows PowerShell modul felderítési szolgáltatások a Fabrikam modul található, a modul Fabrikam telepítője ad hozzá a modul hely értékét a **PSModulePath** környezeti változót.

```powershell
$p = [Environment]::GetEnvironmentVariable("PSModulePath")
$p += ";C:\Program Files\Fabrikam Technologies\Fabrikam Manager\Modules\"
[Environment]::SetEnvironmentVariable("PSModulePath",$p)
```

### <a name="installing-modules-in-the-common-files-directory"></a>A közös fájlok címtárban modulok telepítése

Ha egy modul több összetevőből egy termék vagy egy termék több verzióját használja, a modul telepítése egy modul-specifikus alkönyvtár %ProgramFiles%\Common Files\Modules alkönyvtár.

A következő példában a Fabrikam modul Fabrikam alkönyvtára települ a `%ProgramFiles%\Common Files\Modules` alkönyvtárat. Vegye figyelembe, hogy mindegyik modul saját alkönyvtárában található cikkre hivatkozik, a modulok alkönyvtárban található.

```
C:\Program Files
  Common Files
    Modules
      Fabrikam
        Fabrikam.psd1 (module manifest)
        Fabrikam.dll (module assembly)
```

Ezt követően a telepítő biztosítja a értékét a **PSModulePath** környezeti változó tartalmazza a közös fájlok modulok alkönyvtár elérési útját.

```powershell
$m = $env:ProgramFiles + '\Common Files\Modules'
$p = [Environment]::GetEnvironmentVariable("PSModulePath")
$q = $p -split ';'
if ($q -notContains $m) {
    $q += ";$m"
}
$p = $q -join ';'
[Environment]::SetEnvironmentVariable("PSModulePath", $p)
```

## <a name="installing-multiple-versions-of-a-module"></a>Egy modul több verziójának telepítése

Az alábbi eljárással ugyanazon modul több verziójának telepítéséhez.

1. Hozzon létre egy könyvtárat a modul minden egyes verzióját. Vegye fel a verziószámot a könyvtár nevét.
2. Hozzon létre egy moduljegyzék a modul minden egyes verziójához. Az értékét a **ModuleVersion** a jegyzékfájlban kulcsban, adja meg a modul verziószámát. Mentse a jegyzékfájlt (.psd1) a modul verzióspecifikus könyvtárában.
3. A modul gyökérmappa elérési útja hozzá értékét a **PSModulePath** környezeti változót, a következő példákban szemléltetett módon.

A modul egy adott verziót importált, a végfelhasználó használható a `MinimumVersion` vagy `RequiredVersion` paramétereit a [Import-Module](/powershell/module/Microsoft.PowerShell.Core/Import-Module) parancsmagot.

Ha például a Fabrikam modul 8.0-s és 9.0-s verzióban érhető el, ha a Fabrikam modul könyvtárstruktúrát előfordulhat, hogy az alábbihoz hasonló lesz.

 ```
C:\Program Files
Fabrikam Manager
  Fabrikam8
    Fabrikam
      Fabrikam.psd1 (module manifest: ModuleVersion = "8.0")
      Fabrikam.dll (module assembly)
  Fabrikam9
    Fabrikam
      Fabrikam.psd1 (module manifest: ModuleVersion = "9.0")
      Fabrikam.dll (module assembly)
```

A telepítő felveszi mindkét modul elérési útja a **PSModulePath** környezeti változó értékét.

```powershell
$p = [Environment]::GetEnvironmentVariable("PSModulePath")
$p += ";C:\Program Files\Fabrikam\Fabrikam8;C:\Program Files\Fabrikam\Fabrikam9"
[Environment]::SetEnvironmentVariable("PSModulePath",$p)
```

Amikor végzett, ezeket a lépéseket a **ListAvailable** paraméterében a [Get-Module](/powershell/module/Microsoft.PowerShell.Core/Get-Module) parancsmag Előhozza a Fabrikam modulok mindkét. Egy adott modul importálásához használja a `MinimumVersion` vagy `RequiredVersion` paramétereit a [Import-Module](/powershell/module/Microsoft.PowerShell.Core/Import-Module) parancsmagot.

Ha mindkét rendszer importálja a parancsmagmodulokat a ugyanazon munkamenet, és a modulok ugyanazokat a neveket a parancsmagokat tartalmaznak, a parancsmagok utolsó importált hatékonyak a munkamenetben.

## <a name="handling-command-name-conflicts"></a>A parancs névütközések kezelése

A parancs neve ütközik akkor fordulhat elő, ha a parancsokat egy modul által a neve megegyezik a parancsok a felhasználói munkamenetben.

Ha egy munkamenetben két azonos nevű parancsok tartalmaz, a Windows PowerShell futtatja a parancs típusa, amely élvez elsőbbséget. Ha egy munkamenetben két ugyanazzal a névvel és típussal rendelkező parancsok tartalmaz, a Windows PowerShell a munkamenethez legutoljára hozzáadott parancs futtatja. Szeretne futtatni egy parancsot, amely alapértelmezés szerint nem fut, a felhasználók megszerezheti a parancs neve a modul nevét.

Például, ha a munkamenet tartalmaz egy `Get-Date` függvény és a `Get-Date` Windows PowerShell-parancsmagot futtatja a függvény alapértelmezés szerint. A parancsmag futtatásához kiírja a parancsot a modul neve, mint például:

```powershell
Microsoft.PowerShell.Utility\Get-Date
```

Név ütközések elkerülése érdekében, a modul szerzők használhatja a **DefaultCommandPrefix** modulból exportált kulcsot, adja meg az összes parancsra vonatkozó főnévi előtagot a moduljegyzékben.

A felhasználók használhatják a **előtag** paraméterében a `Import-Module` parancsmagot, hogy egy másik előtagot használja. Értékét a **előtag** paraméter elsőbbséget élvez az értékét a **DefaultCommandPrefix** kulcsot.

## <a name="see-also"></a>Lásd még:

[about_Command_Precedence](/powershell/module/microsoft.powershell.core/about/about_command_precedence)

[Windows PowerShell-modul írása](./writing-a-windows-powershell-module.md)
