---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: Többszörös kijelölésű listák
ms.openlocfilehash: dcfa43ac8e7cc4ba6147f71791edbf7989af3583
ms.sourcegitcommit: a6f13c16a535acea279c0ddeca72f1f0d8a8ce4c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2019
ms.locfileid: "67030094"
---
# <a name="multiple-selection-list-boxes"></a>Többszörös kijelölési lista

Windows PowerShell 3.0-s és újabb kiadásaiban segítségével egy többszörös kijelölési lista vezérlőelem hozzon létre egy egyéni Windows-űrlapon.

## <a name="create-list-box-controls-that-allow-multiple-selections"></a>Lista létrehozása, amely több elem is választható vezérlők

Másolja, és ezután illessze be a következő Windows PowerShell ISE-ben, és mentse egy Windows PowerShell-parancsprogram (.ps1).

```powershell
Add-Type -AssemblyName System.Windows.Forms
Add-Type -AssemblyName System.Drawing

$form = New-Object System.Windows.Forms.Form
$form.Text = 'Data Entry Form'
$form.Size = New-Object System.Drawing.Size(300,200)
$form.StartPosition = 'CenterScreen'

$OKButton = New-Object System.Windows.Forms.Button
$OKButton.Location = New-Object System.Drawing.Point(75,120)
$OKButton.Size = New-Object System.Drawing.Size(75,23)
$OKButton.Text = 'OK'
$OKButton.DialogResult = [System.Windows.Forms.DialogResult]::OK
$form.AcceptButton = $OKButton
$form.Controls.Add($OKButton)

$CancelButton = New-Object System.Windows.Forms.Button
$CancelButton.Location = New-Object System.Drawing.Point(150,120)
$CancelButton.Size = New-Object System.Drawing.Size(75,23)
$CancelButton.Text = 'Cancel'
$CancelButton.DialogResult = [System.Windows.Forms.DialogResult]::Cancel
$form.CancelButton = $CancelButton
$form.Controls.Add($CancelButton)

$label = New-Object System.Windows.Forms.Label
$label.Location = New-Object System.Drawing.Point(10,20)
$label.Size = New-Object System.Drawing.Size(280,20)
$label.Text = 'Please make a selection from the list below:'
$form.Controls.Add($label)

$listBox = New-Object System.Windows.Forms.Listbox
$listBox.Location = New-Object System.Drawing.Point(10,40)
$listBox.Size = New-Object System.Drawing.Size(260,20)

$listBox.SelectionMode = 'MultiExtended'

[void] $listBox.Items.Add('Item 1')
[void] $listBox.Items.Add('Item 2')
[void] $listBox.Items.Add('Item 3')
[void] $listBox.Items.Add('Item 4')
[void] $listBox.Items.Add('Item 5')

$listBox.Height = 70
$form.Controls.Add($listBox)
$form.Topmost = $true

$result = $form.ShowDialog()

if ($result -eq [System.Windows.Forms.DialogResult]::OK)
{
    $x = $listBox.SelectedItems
    $x
}
```

A szkript első lépése betöltése két .NET-osztályok: **System.Drawing** és **System.Windows.Forms**. Indítsa el a .NET-keretrendszer osztály egy új példányát **System.Windows.Forms.Form**; amely biztosítja, hogy egy üres űrlapot vagy ablakban, amelyhez elkezdhet szabályozza.

```powershell
$form = New-Object System.Windows.Forms.Form
```

Miután létrehozta az űrlap osztály egy példányát, értéket rendelni az osztály három tulajdonságot.

- **Szöveg.** Ez lesz az ablak címe.

- **Velikost.** Ez a méretét az űrlap (képpontban). A fenti szkript létrehoz egy képernyő, amely 300 képpont széles és 200 képpont magas.

- **Kezdőpozíció.** Ez nem kötelező tulajdonsága **CenterScreen** az előző szkriptben. Ha nem ezt a tulajdonságot, a Windows kiválaszt egy helyet, az űrlap megnyitásakor. Beállításával a **kezdőpozíció** való **CenterScreen**, akkor már automatikusan megjelenítése az űrlap a képernyő közepén minden alkalommal, amikor betölti.

```powershell
$form.Text = 'Data Entry Form'
$form.Size = New-Object System.Drawing.Size(300,200)
$form.StartPosition = 'CenterScreen'
```

Ezután hozzon létre egy **OK** gombot az űrlapon. Adja meg a méretét és viselkedését a **OK** gombra. Ebben a példában a gomb elhelyezése, a képernyő felső széle 120 képpont 75 képpont bal szélétől. A gomb magassága 23 képpont, amíg a gomb hossza 75 képpont. A szkript előre meghatározott Windows Forms-típusok a gomb viselkedés határozza meg.

```powershell
$OKButton = New-Object System.Windows.Forms.Button
$OKButton.Location = New-Object System.Drawing.Size(75,120)
$OKButton.Size = New-Object System.Drawing.Size(75,23)
$OKButton.Text = 'OK'
$OKButton.DialogResult = [System.Windows.Forms.DialogResult]::OK
$form.AcceptButton = $OKButton
$form.Controls.Add($OKButton)
```

Hasonlóképpen, létrehozhat egy **Mégse** gombra. A **Mégse** gombot a felső 120 képpont, de az ablak bal szélétől 150 pixeles.

```powershell
$CancelButton = New-Object System.Windows.Forms.Button
$CancelButton.Location = New-Object System.Drawing.Point(150,120)
$CancelButton.Size = New-Object System.Drawing.Size(75,23)
$CancelButton.Text = 'Cancel'
$CancelButton.DialogResult = [System.Windows.Forms.DialogResult]::Cancel
$form.CancelButton = $CancelButton
$form.Controls.Add($CancelButton)
```

Következő lépésként adja meg az ablak, amely leírja az adatokat, adja meg a felhasználók a felirat szövege.

```powershell
$label = New-Object System.Windows.Forms.Label
$label.Location = New-Object System.Drawing.Point(10,20)
$label.Size = New-Object System.Drawing.Size(280,20)
$label.Text = 'Please make a selection from the list below:'
$form.Controls.Add($label)
```

Adja hozzá a vezérlő (ebben az esetben egy lista), amely lehetővé teszi a felhasználóknak adja meg az adatokat, akkor már ismertetett a felirat szövege. Nincsenek alkalmazhat szövegmezők; mellett számos más vezérlők További vezérlők, lásd: [System.Windows.Forms Namespace](https://msdn.microsoft.com/library/k50ex0x9(v=vs.110).aspx) az MSDN Webhelyén.

```powershell
$listBox = New-Object System.Windows.Forms.Listbox
$listBox.Location = New-Object System.Drawing.Point(10,40)
$listBox.Size = New-Object System.Drawing.Size(260,20)
```

Itt adhatja meg, hogy szeretné-e engedélyezése a felhasználók számára kijelölhet a listában több érték van.

```powershell
$listBox.SelectionMode = 'MultiExtended'
```

A következő szakaszban adja meg a kívánt értékeket, a felhasználók számára megjelenítendő legördülő listából.

```powershell
[void] $listBox.Items.Add('Item 1')
[void] $listBox.Items.Add('Item 2')
[void] $listBox.Items.Add('Item 3')
[void] $listBox.Items.Add('Item 4')
[void] $listBox.Items.Add('Item 5')
```

Adja meg a lista vezérlőelem maximális magasságát.

```powershell
$listBox.Height = 70
```

A lista vezérlőelem felvétele az űrlapot, és kérje meg a Windows más windows és a párbeszédpanelek interaktív irányítópultunkat képernyő megnyitásához, ha meg van nyitva.

```powershell
$form.Controls.Add($listBox)
$form.Topmost = $true
```

Adja hozzá az alábbi kódsort az űrlap megjelenítésére a Windows.

```powershell
$result = $form.ShowDialog()
```

Végül a kód belül a **Ha** blokk arra utasítja a Windows Mi a teendő az űrlapot, miután a felhasználók egy vagy több lehetőség kiválasztása a listából, és kattintson a **OK** gombra vagy nyomja le a **Enter**  kulcsot.

```powershell
if ($result -eq [System.Windows.Forms.DialogResult]::OK)
{
    $x = $listBox.SelectedItems
    $x
}
```

## <a name="see-also"></a>Lásd még:

- [Hey Scripting Guy:  Miért nem működnek a grafikus PowerShell-példákat?](https://go.microsoft.com/fwlink/?LinkId=506644)
- [GitHub: Dave Wyatt WinFormsExampleUpdates](https://github.com/dlwyatt/WinFormsExampleUpdates)
- [Windows PowerShell Tip of the Week:  Többszörös kijelölési lista - és a további!](https://technet.microsoft.com/library/ff730950.aspx)
