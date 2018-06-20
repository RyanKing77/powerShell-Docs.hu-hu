---
ms.date: 06/05/2017
keywords: PowerShell parancsmag
title: Grafikus dátumválasztó létrehozása
ms.assetid: c1cb722c-41e9-4baa-be83-59b4653222e9
ms.openlocfilehash: 3727c90c314a6fc1b3a338ec60e44259f153d954
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
ms.locfileid: "30954840"
---
# <a name="creating-a-graphical-date-picker"></a>Grafikus dátumválasztó létrehozása

Egy grafikus, naptár-stílusú Control, amely lehetővé teszi a felhasználóknak, válassza ki a hónap napját űrlapok létrehozásához használja a Windows PowerShell 3.0-s és újabb verziókban.

## <a name="create-a-graphical-date-picker-control"></a>Hozzon létre egy grafikus dátumválasztó-vezérlő

Másolja és illessze be a következő Windows PowerShell ISE-be, és mentse egy Windows PowerShell-parancsfájlt (.ps1).

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

A parancsfájl első lépése két .NET-keretrendszer osztály betöltése: **System.Drawing** és **System.Windows.Forms**. Majd indítsa el a .NET-keretrendszer osztály új példánya **Windows.Forms.Form**; biztosítja az üres űrlapból, vagy ablak, amelyhez elkezdhet szabályozza.

```powershell
$form = New-Object Windows.Forms.Form
```

Az űrlap osztály példányának létrehozása után értéket hozzárendelni az osztály három tulajdonságot.

- **Text.** Ez lesz az ablak címe.

- **Size.** Ez az az űrlap képpontban méretét. Az előző parancsfájl, amely 243 x széles 230 képpont magas űrlap hoz létre.

- **StartingPosition.** Ez nem kötelező tulajdonság értéke **CenterScreen** az előző parancsfájlban. Ez a tulajdonság nem ad hozzá, ha a Windows kiválaszt egy helyet, az űrlap megnyitásakor. Úgy, hogy a **StartingPosition** való **CenterScreen**, akkor program automatikusan jeleníti meg az űrlap közepén a képernyő minden alkalommal, amikor betölti a.

```powershell
$form.Text = 'Select a Date'
$form.Size = New-Object Drawing.Size @(243,230)
$form.StartPosition = 'CenterScreen'
```

Ezután hozzon létre, és adja hozzá a havinaptár-vezérlőben a képernyőn. Ebben a példában az aktuális nap nem a kijelölt vagy körben. Csak egy nap a naptár egy időben bejelölésével.

```powershell
$calendar = New-Object System.Windows.Forms.MonthCalendar
$calendar.ShowTodayCircle = $false
$calendar.MaxSelectionCount = 1
$form.Controls.Add($calendar)
```

Ezután hozzon létre egy **OK** gombra az űrlap. Adja meg a méretét és viselkedését a **OK** gombra. Ebben a példában a gomb pozíciója 165 a képernyő felső szélétől, és 38 képpontok bal szélétől. A gomb magassága 23 képpont, amíg a gomb hossza 75 képpontban megadva. A parancsfájl előre meghatározott Windows Forms-típusok gombra viselkedésmódját meghatározására használja.

```powershell
$OKButton = New-Object System.Windows.Forms.Button
$OKButton.Location = New-Object System.Drawing.Point(38,165)
$OKButton.Size = New-Object System.Drawing.Size(75,23)
$OKButton.Text = 'OK'
$OKButton.DialogResult = [System.Windows.Forms.DialogResult]::OK
$form.AcceptButton = $OKButton
$form.Controls.Add($OKButton)
```

Hasonlóképpen, létrehozhat egy **Mégse** gombra. A **Mégse** gomb, a lista elejéről 165 képpont, de az ablak bal szélétől 113 képpont.

```powershell
$CancelButton = New-Object System.Windows.Forms.Button
$CancelButton.Location = New-Object System.Drawing.Point(113,165)
$CancelButton.Size = New-Object System.Drawing.Size(75,23)
$CancelButton.Text = 'Cancel'
$CancelButton.DialogResult = [System.Windows.Forms.DialogResult]::Cancel
$form.CancelButton = $CancelButton
$form.Controls.Add($CancelButton)
```

Állítsa be a **Topmost** tulajdonságot **$true** azzal kényszerítheti a az ablak elveire más nyissa meg a windows és a párbeszédpanel megnyitásához.

```powershell
$form.Topmost = $true
```

Adja hozzá a következő kódsort a képernyőn megjelenő Windows.

```powershell
$result = $form.ShowDialog()
```

Végezetül, a kódot a **Ha** blokk utasítja Windows Mi a teendő az űrlapot, miután a felhasználók válasszon ki egy napot a naptárban, és kattintson a **OK** gombra vagy nyomja meg a **Enter** kulcs. A Windows PowerShell a felhasználók számára kijelölt dátumának megjelenítése.

```powershell
if ($result -eq [System.Windows.Forms.DialogResult]::OK)
{
    $date = $calendar.SelectionStart
    Write-Host "Date selected: $($date.ToShortDateString())"
}
```

## <a name="see-also"></a>Lásd még:

- [Hey Scripting Guy: Miért nem PowerShell grafikus felhasználói Felülettel példákban használhatók?](http://go.microsoft.com/fwlink/?LinkId=506644)
- [GitHub: Dave Wyatt WinFormsExampleUpdates](https://github.com/dlwyatt/WinFormsExampleUpdates)
- [A hét Windows PowerShell tipp: grafikus Dátumválasztó létrehozása](http://technet.microsoft.com/library/ff730942.aspx)