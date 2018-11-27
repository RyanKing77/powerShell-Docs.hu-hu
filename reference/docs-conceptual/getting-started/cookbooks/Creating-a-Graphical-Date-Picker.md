---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: Grafikus dátumválasztó létrehozása
ms.assetid: c1cb722c-41e9-4baa-be83-59b4653222e9
ms.openlocfilehash: 6dd43a3b1f4c67633ad1755de3db88eb8c6772c8
ms.sourcegitcommit: 221b7daab7f597f8b2e4864cf9b5d9dda9b9879b
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 11/27/2018
ms.locfileid: "52320329"
---
# <a name="creating-a-graphical-date-picker"></a>Grafikus dátumválasztó létrehozása

A grafikus, naptár stílusú vezérlőelemmel, amely lehetővé teszi a felhasználóknak, válasszon ki egy napot a hónap egy űrlap létrehozásához használja a Windows PowerShell 3.0-s és újabb verziókban.

## <a name="create-a-graphical-date-picker-control"></a>Grafikus Dátumválasztó vezérlőelem létrehozása

Másolja, és ezután illessze be a következő Windows PowerShell ISE-ben, és mentse egy Windows PowerShell-parancsprogram (.ps1).

```powershell
Add-Type -AssemblyName System.Windows.Forms
Add-Type -AssemblyName System.Drawing

$form = New-Object Windows.Forms.Form

$form.Text = 'Select a Date'
$form.Size = New-Object Drawing.Size @(243,230)
$form.StartPosition = 'CenterScreen'

$calendar = New-Object System.Windows.Forms.MonthCalendar
$calendar.ShowTodayCircle = $false
$calendar.MaxSelectionCount = 1
$form.Controls.Add($calendar)

$OKButton = New-Object System.Windows.Forms.Button
$OKButton.Location = New-Object System.Drawing.Point(38,165)
$OKButton.Size = New-Object System.Drawing.Size(75,23)
$OKButton.Text = 'OK'
$OKButton.DialogResult = [System.Windows.Forms.DialogResult]::OK
$form.AcceptButton = $OKButton
$form.Controls.Add($OKButton)

$CancelButton = New-Object System.Windows.Forms.Button
$CancelButton.Location = New-Object System.Drawing.Point(113,165)
$CancelButton.Size = New-Object System.Drawing.Size(75,23)
$CancelButton.Text = 'Cancel'
$CancelButton.DialogResult = [System.Windows.Forms.DialogResult]::Cancel
$form.CancelButton = $CancelButton
$form.Controls.Add($CancelButton)

$form.Topmost = $true

$result = $form.ShowDialog()

if ($result -eq [System.Windows.Forms.DialogResult]::OK)
{
    $date = $calendar.SelectionStart
    Write-Host "Date selected: $($date.ToShortDateString())"
}
```

A szkript első lépése két .NET-keretrendszer osztály betöltésekor: **System.Drawing** és **System.Windows.Forms**. Indítsa el a .NET-keretrendszer osztály egy új példányát **Windows.Forms.Form**; amely biztosítja, hogy egy üres űrlapot vagy ablakban, amelyhez elkezdhet szabályozza.

```powershell
$form = New-Object Windows.Forms.Form
```

Miután létrehozta az űrlap osztály egy példányát, értéket rendelni az osztály három tulajdonságot.

- **Szöveg.** Ez lesz az ablak címe.

- **Velikost.** Ez a méretét az űrlap (képpontban). A fenti szkript létrehoz egy képernyő, amely 243 képpont szélességű és 230 képpont magas.

- **Kezdőpozíció.** Ez nem kötelező tulajdonsága **CenterScreen** az előző szkriptben. Ha nem ezt a tulajdonságot, a Windows kiválaszt egy helyet, az űrlap megnyitásakor. Beállításával a **kezdőpozíció** való **CenterScreen**, akkor már automatikusan megjelenítése az űrlap a képernyő közepén minden alkalommal, amikor betölti.

```powershell
$form.Text = 'Select a Date'
$form.Size = New-Object Drawing.Size @(243,230)
$form.StartPosition = 'CenterScreen'
```

Következő lépésként hozzon létre, és adja hozzá a Naptár vezérlőelem a képernyőn. Ebben a példában az aktuális nap nem kiemelt vagy bekarikázott. Felhasználók által választható csak egyetlen napon a naptárban egy időben.

```powershell
$calendar = New-Object System.Windows.Forms.MonthCalendar
$calendar.ShowTodayCircle = $false
$calendar.MaxSelectionCount = 1
$form.Controls.Add($calendar)
```

Ezután hozzon létre egy **OK** gombot az űrlapon. Adja meg a méretét és viselkedését a **OK** gombra. Ebben a példában a gomb pozice je 165 a képernyő felső széle, és 38 képpontok bal szélétől. A gomb magassága 23 képpont, amíg a gomb hossza 75 képpont. A szkript előre meghatározott Windows Forms-típusok a gomb viselkedés határozza meg.

```powershell
$OKButton = New-Object System.Windows.Forms.Button
$OKButton.Location = New-Object System.Drawing.Point(38,165)
$OKButton.Size = New-Object System.Drawing.Size(75,23)
$OKButton.Text = 'OK'
$OKButton.DialogResult = [System.Windows.Forms.DialogResult]::OK
$form.AcceptButton = $OKButton
$form.Controls.Add($OKButton)
```

Hasonlóképpen, létrehozhat egy **Mégse** gombra. A **Mégse** gombot a felső 165 képpont, de az ablak bal szélétől 113 képpont.

```powershell
$CancelButton = New-Object System.Windows.Forms.Button
$CancelButton.Location = New-Object System.Drawing.Point(113,165)
$CancelButton.Size = New-Object System.Drawing.Size(75,23)
$CancelButton.Text = 'Cancel'
$CancelButton.DialogResult = [System.Windows.Forms.DialogResult]::Cancel
$form.CancelButton = $CancelButton
$form.Controls.Add($CancelButton)
```

Állítsa be a **Topmost** tulajdonságot **$true** kényszerítése az ablak megnyitásához nyissa meg a windows és a párbeszédpanelek interaktív irányítópultunkat.

```powershell
$form.Topmost = $true
```

Adja hozzá az alábbi kódsort az űrlap megjelenítésére a Windows.

```powershell
$result = $form.ShowDialog()
```

Végül a kód belül a **Ha** blokk arra utasítja a Windows Mi a teendő az űrlapot, miután a felhasználók válasszon ki egy napot a naptárban, és kattintson a **OK** gombra vagy nyomja le a **Enter** kulcs. Windows PowerShell a választott dátum felhasználókat jeleníti meg.

```powershell
if ($result -eq [System.Windows.Forms.DialogResult]::OK)
{
    $date = $calendar.SelectionStart
    Write-Host "Date selected: $($date.ToShortDateString())"
}
```

## <a name="see-also"></a>Lásd még:

- [Hey Scripting Guy: Miért nem a grafikus PowerShell-példákat működnek?](https://go.microsoft.com/fwlink/?LinkId=506644)
- [GitHub: Dave Wyatt WinFormsExampleUpdates](https://github.com/dlwyatt/WinFormsExampleUpdates)
- [Windows PowerShell Tip of the Week: grafikus Dátumválasztó létrehozása](https://technet.microsoft.com/library/ff730942.aspx)