---
title: A PSModulePath telepítési elérési út módosítása |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: dc5ce5a2-50e9-4c88-abf1-ac148a8a6b7b
caps.latest.revision: 15
ms.openlocfilehash: 639d3a28dd2af09fcc498caedc5fe74c1493445d
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56846507"
---
# <a name="modifying-the-psmodulepath-installation-path"></a>A PSModulePath telepítési útvonalának módosítása

A `PSModulePath` környezeti változó tárolja a lemezen telepített modulok helyeinek elérési útjára. Windows PowerShell modulok megkeresése, ha a felhasználó nem ad meg egy modul teljes elérési útja ezt a változót használja. Ezzel a változóval szereplő elérési utakat a keresés megjelenésük sorrendjében történik.

Ha a Windows PowerShell elindul, `PSModulePath` egy rendszerkörnyezeti változót a következő alapértelmezett értékkel jön létre: `$home\Documents\WindowsPowerShell\Modules; $pshome\Modules`.

## <a name="to-view-the-psmodulepath-variable"></a>A PSModulePath változó megtekintése

A megadott elérési utak megtekintéséhez a `PSModulePath` változó, írja be a következő parancsot:

`$env:PSModulePath`

## <a name="to-add-locations-to-the-psmodulepath-variable"></a>A helyek PSModulePath változó hozzáadása

Ezt a változót az elérési utak hozzáadásához használja a következő módszerek egyikét:

- Adjon hozzá egy ideiglenes érték, amely csak az aktuális munkamenet számára érhető el, a következő parancsot a parancssorban:

  `$env:PSModulePath = $env:PSModulePath + ";c:\ModulePath"`

- Adjon hozzá egy állandó értéket, amely a munkamenet megnyitásakor érhető el, adja hozzá a következő parancsot egy Windows PowerShell-profilhoz:

  `$env:PSModulePath = $env:PSModulePath + ";c:\ModulePath"`

  Profilokkal kapcsolatos további információkért lásd: [about_Profiles](/powershell/module/microsoft.powershell.core/about/about_profiles) a Microsoft TechNet-könyvtárban.

- Adja hozzá a beállításjegyzékhez egy állandó változó, hozzon létre egy új felhasználói nevű környezeti változót `PSModulePath` a a környezeti változók-szerkesztő használatával a **Rendszertulajdonságok** párbeszédpanel bezárásához.

- Állandó változó hozzáadása egy parancsfájl használatával, használja a **SetEnvironmentVariable** metódust a környezeti osztályt. Például a következő parancsfájl létrehozza a "C:\Program Files\Fabrikam\Module elérési útja a számítógépen a PSModulePath környezeti változó értékét. Az elérési út hozzáadása a felhasználói PSModulePath környezeti változót, állítsa be a cél "Felhasználó".

  ```powershell
  $CurrentValue = [Environment]::GetEnvironmentVariable("PSModulePath", "Machine")
  [Environment]::SetEnvironmentVariable("PSModulePath", $CurrentValue + ";C:\Program Files\Fabrikam\Modules", "Machine")

  ```

## <a name="to-remove-locations-from-the-psmodulepath"></a>Helyek eltávolításához a PSModulePath

Elérési utak távolíthatja el a változó hasonló módszerekkel: például `$env:PSModulePath = $env:PSModulePath -replace ";c:\\ModulePath"` eltávolítja a **c:\ModulePath** az aktuális munkamenet-ről.

## <a name="see-also"></a>Lásd még:

[Windows PowerShell-modul írása](./writing-a-windows-powershell-module.md)
