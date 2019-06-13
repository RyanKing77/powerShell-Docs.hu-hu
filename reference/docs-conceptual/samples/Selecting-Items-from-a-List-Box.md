---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: Elemek kiválasztása egy listából
ms.openlocfilehash: 55bc9409b0e330a2080781bfd4c586109896258f
ms.sourcegitcommit: a6f13c16a535acea279c0ddeca72f1f0d8a8ce4c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2019
ms.locfileid: "67030826"
---
# <a name="selecting-items-from-a-list-box"></a>Elemek kiválasztása egy listából

Egy párbeszédpanel, amely lehetővé teszi az elemek kiválasztása egy lista vezérlőelem a felhasználók létrehozásához használja a Windows PowerShell 3.0-s és újabb verziókban.

## <a name="create-a-list-box-control-and-select-items-from-it"></a>Hozzon létre egy lista vezérlőelem és elemeket választhat

Másolja, és ezután illessze be a következő Windows PowerShell ISE-ben, és mentse egy Windows PowerShell-parancsprogram (.ps1).

```powershell
Add-Type -AssemblyName System.Windows.Forms
Add-Type -AssemblyName System.Drawing

$form = New-Object System.Windows.Forms.Form
$form.Text = 'Select a Computer'
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
$label.Text = 'Please select a computer:'
$form.Controls.Add($label)

$listBox = New-Object System.Windows.Forms.ListBox
$listBox.Location = New-Object System.Drawing.Point(10,40)
$listBox.Size = New-Object System.Drawing.Size(260,20)
$listBox.Height = 80

[void] $listBox.Items.Add('atl-dc-001')
[void] $listBox.Items.Add('atl-dc-002')
[void] $listBox.Items.Add('atl-dc-003')
[void] $listBox.Items.Add('atl-dc-004')
[void] $listBox.Items.Add('atl-dc-005')
[void] $listBox.Items.Add('atl-dc-006')
[void] $listBox.Items.Add('atl-dc-007')

$form.Controls.Add($listBox)

$form.Topmost = $true

$result = $form.ShowDialog()

if ($result -eq [System.Windows.Forms.DialogResult]::OK)
{
    $x = $listBox.SelectedItem
    $x
}
```

A szkript első lépése betöltése két .NET-osztályok: **System.Drawing** és **System.Windows.Forms**. Indítsa el a .NET-keretrendszer osztály egy új példányát **System.Windows.Forms.Form**; amely biztosítja, hogy egy üres űrlapot vagy ablakban, amelyhez elkezdhet szabályozza.

```powershell
Add-Type -AssemblyName System.Windows.Forms
Add-Type -AssemblyName System.Drawing
```

Miután létrehozta az űrlap osztály egy példányát, értéket rendelni az osztály három tulajdonságot.

- **Szöveg.** Ez lesz az ablak címe.

- **Velikost.** Ez a méretét az űrlap (képpontban). A fenti szkript létrehoz egy képernyő, amely 300 képpont széles és 200 képpont magas.

- **Kezdőpozíció.** Ez nem kötelező tulajdonsága **CenterScreen** az előző szkriptben. Ha nem ezt a tulajdonságot, a Windows kiválaszt egy helyet, az űrlap megnyitásakor. Beállításával a **kezdőpozíció** való **CenterScreen**, akkor már automatikusan megjelenítése az űrlap a képernyő közepén minden alkalommal, amikor betölti.

```powershell
$form.Text = 'Select a Computer'
$form.Size = New-Object System.Drawing.Size(300,200)
$form.StartPosition = 'CenterScreen'
```

Ezután hozzon létre egy **OK** gombot az űrlapon. Adja meg a méretét és viselkedését a **OK** gombra. Ebben a példában a gomb elhelyezése, a képernyő felső széle 120 képpont 75 képpont bal szélétől. A gomb magassága 23 képpont, amíg a gomb hossza 75 képpont. A szkript előre meghatározott Windows Forms-típusok a gomb viselkedés határozza meg.

```powershell
$OKButton = New-Object System.Windows.Forms.Button
$OKButton.Location = New-Object System.Drawing.Point(75,120)
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

Következő lépésként adja meg az ablak, amely leírja az adatokat, adja meg a felhasználók a felirat szövege. Ebben az esetben érdemes a felhasználók számára, válasszon ki egy számítógépet.

```powershell
$label = New-Object System.Windows.Forms.Label
$label.Location = New-Object System.Drawing.Point(10,20)
$label.Size = New-Object System.Drawing.Size(280,20)
$label.Text = 'Please select a computer:'
$form.Controls.Add($label)
```

Adja hozzá a vezérlő (ebben az esetben egy lista), amely lehetővé teszi a felhasználóknak adja meg az adatokat, akkor már ismertetett a felirat szövege. Nincsenek alkalmazhat listák; mellett számos más vezérlők További vezérlők, lásd: [System.Windows.Forms Namespace](https://msdn.microsoft.com/library/k50ex0x9(v=vs.110).aspx) az MSDN Webhelyén.

```powershell
$listBox = New-Object System.Windows.Forms.ListBox
$listBox.Location = New-Object System.Drawing.Point(10,40)
$listBox.Size = New-Object System.Drawing.Size(260,20)
$listBox.Height = 80
```

A következő szakaszban adja meg a kívánt értékeket, a felhasználók számára megjelenítendő legördülő listából.

> [!NOTE]
> A legördülő listából a szkript által létrehozott csak egy kiválasztását teszi lehetővé. A lista vezérlőelem, amely lehetővé teszi, hogy több elem is választható létrehozásához adjon meg értéket a **SelectionMode** tulajdonságát, hasonlóan a következő: `$listBox.SelectionMode = 'MultiExtended'`. További információkért lásd: [többszörös kijelölési lista](Multiple-selection-List-Boxes.md).

```powershell
[void] $listBox.Items.Add('atl-dc-001')
[void] $listBox.Items.Add('atl-dc-002')
[void] $listBox.Items.Add('atl-dc-003')
[void] $listBox.Items.Add('atl-dc-004')
[void] $listBox.Items.Add('atl-dc-005')
[void] $listBox.Items.Add('atl-dc-006')
[void] $listBox.Items.Add('atl-dc-007')
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

Végül a kód belül a **Ha** blokk arra utasítja a Windows Mi a teendő az űrlapot, miután a felhasználók jelöljön ki egy lehetőséget a legördülő listából, és kattintson a **OK** gombra vagy nyomja le a **Enter**kulcsot.

```powershell
if ($result -eq [System.Windows.Forms.DialogResult]::OK)
{
    $x = $listBox.SelectedItem
    $x
}
```

## <a name="see-also"></a>Lásd még:

- [Hey Scripting Guy:  Miért nem működnek a grafikus PowerShell-példákat?](https://go.microsoft.com/fwlink/?LinkId=506644)
- [GitHub: Dave Wyatt WinFormsExampleUpdates](https://github.com/dlwyatt/WinFormsExampleUpdates)
- [Windows PowerShell Tip of the Week:  Elemek kiválasztása egy listából](https://technet.microsoft.com/library/ff730949.aspx)
