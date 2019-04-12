---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: Grafikus dátumválasztó létrehozása
ms.assetid: c1cb722c-41e9-4baa-be83-59b4653222e9
ms.openlocfilehash: d3b24af935e781a8a36fc346a6108baaed37b6db
ms.sourcegitcommit: 3f6002e7109373eda31cc65fc84d2600447cb7e9
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/11/2019
ms.locfileid: "59506801"
---
# <a name="creating-a-graphical-date-picker"></a>Grafikus dátumválasztó létrehozása

A grafikus, naptár stílusú vezérlőelemmel, amely lehetővé teszi a felhasználóknak, válasszon ki egy napot a hónap egy űrlap létrehozásához használja a Windows PowerShell 3.0-s és újabb verziókban.

## <a name="create-a-graphical-date-picker-control"></a>Grafikus Dátumválasztó vezérlőelem létrehozása

Másolja, és ezután illessze be a következő Windows PowerShell ISE-ben, és mentse egy Windows PowerShell-parancsprogram (.ps1).

```powershell
Add-Type -AssemblyName System.Windows.Forms
Add-Type -AssemblyName System.Drawing

$form = New-Object Windows.Forms.Form -Property @{
    StartPosition = [Windows.Forms.FormStartPosition]::CenterScreen
    Size          = New-Object Drawing.Size 243, 230
    Text          = 'Select a Date'
    Topmost       = $true
}

$calendar = New-Object Windows.Forms.MonthCalendar -Property @{
    ShowTodayCircle   = $false
    MaxSelectionCount = 1
}
$form.Controls.Add($calendar)

$OKButton = New-Object Windows.Forms.Button -Property @{
    Location     = New-Object Drawing.Point 38, 165
    Size         = New-Object Drawing.Size 75, 23
    Text         = 'OK'
    DialogResult = [Windows.Forms.DialogResult]::OK
}
$form.AcceptButton = $OKButton
$form.Controls.Add($OKButton)

$CancelButton = New-Object Windows.Forms.Button -Property @{
    Location     = New-Object Drawing.Point 113, 165
    Size         = New-Object Drawing.Size 75, 23
    Text         = 'Cancel'
    DialogResult = [Windows.Forms.DialogResult]::Cancel
}
$form.CancelButton = $CancelButton
$form.Controls.Add($CancelButton)

$result = $form.ShowDialog()

if ($result -eq [Windows.Forms.DialogResult]::OK) {
    $date = $calendar.SelectionStart
    Write-Host "Date selected: $($date.ToShortDateString())"
}
```

A szkript első lépése betöltése két .NET-osztályok: **System.Drawing** és **System.Windows.Forms**.
Indítsa el a .NET-keretrendszer osztály egy új példányát **Windows.Forms.Form**; amely biztosítja, hogy egy üres űrlapot vagy ablakban, amelyhez elkezdhet szabályozza.

```powershell
$form = New-Object Windows.Forms.Form -Property @{
    StartPosition = [Windows.Forms.FormStartPosition]::CenterScreen
    Size          = New-Object Drawing.Size 243, 230
    Text          = 'Select a Date'
    Topmost       = $true
}
```

Ebben a példában ez az osztály tulajdonságait négy értékeket rendelő használatával a **tulajdonság** tulajdonság és a kivonattábla kulcsa.

1. **StartPosition**: Ha nem ezt a tulajdonságot, a Windows kiválaszt egy helyet, az űrlap megnyitásakor.
   Úgy, hogy ez a tulajdonság **CenterScreen**, akkor már automatikusan megjelenítése az űrlap a képernyő közepén minden alkalommal, amikor betölti.

2. **Méret**: Ez a méretét az űrlap (képpontban).
   A fenti szkript létrehoz egy képernyő, amely 243 képpont szélességű és 230 képpont magas.

3. **Szöveg**: Ez lesz az ablak címe.

4. **Legfelső**: Ez a tulajdonság beállításával `$true`, kényszerítheti az ablak megnyitásához nyissa meg a windows és a párbeszédpanelek interaktív irányítópultunkat.

Következő lépésként hozzon létre, és adja hozzá a Naptár vezérlőelem a képernyőn.
Ebben a példában az aktuális nap nem kiemelt vagy bekarikázott.
Felhasználók által választható csak egyetlen napon a naptárban egy időben.

```powershell
$calendar = New-Object Windows.Forms.MonthCalendar -Property @{
    ShowTodayCircle   = $false
    MaxSelectionCount = 1
}
$form.Controls.Add($calendar)
```

Ezután hozzon létre egy **OK** gombot az űrlapon.
Adja meg a méretét és viselkedését a **OK** gombra.
Ebben a példában a gomb pozice je 165 a képernyő felső széle, és 38 képpontok bal szélétől.
A gomb magassága 23 képpont, amíg a gomb hossza 75 képpont.
A szkript előre meghatározott Windows Forms-típusok a gomb viselkedés határozza meg.

```powershell
$OKButton = New-Object Windows.Forms.Button -Property @{
    Location     = New-Object Drawing.Point 38, 165
    Size         = New-Object Drawing.Size 75, 23
    Text         = 'OK'
    DialogResult = [Windows.Forms.DialogResult]::OK
}
$form.AcceptButton = $OKButton
$form.Controls.Add($OKButton)
```

Hasonlóképpen, létrehozhat egy **Mégse** gombra.
A **Mégse** gombot a felső 165 képpont, de az ablak bal szélétől 113 képpont.

```powershell
$CancelButton = New-Object Windows.Forms.Button -Property @{
    Location     = New-Object Drawing.Point 113, 165
    Size         = New-Object Drawing.Size 75, 23
    Text         = 'Cancel'
    DialogResult = [Windows.Forms.DialogResult]::Cancel
}
$form.CancelButton = $CancelButton
$form.Controls.Add($CancelButton)
```

Adja hozzá az alábbi kódsort az űrlap megjelenítésére a Windows.

```powershell
$result = $form.ShowDialog()
```

Végül a kód belül a `if` blokk arra utasítja a Windows Mi a teendő az űrlapot, miután a felhasználók válasszon ki egy napot a naptárban, és kattintson a **OK** gombra vagy nyomja le a **Enter** kulcs.
Windows PowerShell a választott dátum felhasználókat jeleníti meg.

```powershell
if ($result -eq [Windows.Forms.DialogResult]::OK) {
    $date = $calendar.SelectionStart
    Write-Host "Date selected: $($date.ToShortDateString())"
}
```

## <a name="see-also"></a>Lásd még:

- [Hey Scripting Guy:  Miért nem működnek a grafikus PowerShell-példákat?](https://go.microsoft.com/fwlink/?LinkId=506644)
- [GitHub: Dave Wyatt WinFormsExampleUpdates](https://github.com/dlwyatt/WinFormsExampleUpdates)
- [Windows PowerShell Tip of the Week:  Grafikus dátumválasztó létrehozása](https://technet.microsoft.com/library/ff730942.aspx)