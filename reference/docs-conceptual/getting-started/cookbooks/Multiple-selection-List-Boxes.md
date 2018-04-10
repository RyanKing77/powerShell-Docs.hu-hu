---
ms.date: 06/05/2017
keywords: PowerShell parancsmag
title: Többszörös kijelölésű listák
ms.assetid: f74cd5d9-da57-4802-b614-0b194a7bc8f8
ms.openlocfilehash: 81708fd5d7204fb7d136e9d8e808303f4d3f4c30
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="multiple-selection-list-boxes"></a>Több kijelölési

Egyéni Windows űrlapon többszörös kijelölés lista vezérlőelemet létrehozásához használja a Windows PowerShell 3.0-s és újabb verziókban.

## <a name="create-list-box-controls-that-allow-multiple-selections"></a>Lista létrehozása, amelyek lehetővé teszik több kijelölés vezérlők

Másolja és illessze be a következő Windows PowerShell ISE-be, és mentse egy Windows PowerShell-parancsfájlt (.ps1).

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

A parancsfájl első lépése két .NET-keretrendszer osztály betöltése: **System.Drawing** és **System.Windows.Forms**. Majd indítsa el a .NET-keretrendszer osztály új példánya **: System.Windows.Forms.Form**; biztosítja az üres űrlapból, vagy ablak, amelyhez elkezdhet szabályozza.

```powershell
$form = New-Object System.Windows.Forms.Form
```

Az űrlap osztály példányának létrehozása után értéket hozzárendelni az osztály három tulajdonságot.

- **Text.** Ez lesz az ablak címe.

- **Size.** Ez az az űrlap képpontban méretét. A fenti parancsfájl űrlapot hoz létre, amely 300 x 200 magassága képpontban megadva.

- **StartingPosition.** Ez nem kötelező tulajdonság értéke **CenterScreen** az előző parancsfájlban. Ez a tulajdonság nem ad hozzá, ha a Windows kiválaszt egy helyet, az űrlap megnyitásakor. Úgy, hogy a **StartingPosition** való **CenterScreen**, akkor program automatikusan jeleníti meg az űrlap közepén a képernyő minden alkalommal, amikor betölti a.

```powershell
$form.Text = 'Data Entry Form'
$form.Size = New-Object System.Drawing.Size(300,200)
$form.StartPosition = 'CenterScreen'
```

Ezután hozzon létre egy **OK** gombra az űrlap. Adja meg a méretét és viselkedését a **OK** gombra. Ebben a példában a gomb pozíciója a képernyő felső szélétől 120 képpont, de 75 képpont bal szélétől. A gomb magassága 23 képpont, amíg a gomb hossza 75 képpontban megadva. A parancsfájl előre meghatározott Windows Forms-típusok gombra viselkedésmódját meghatározására használja.

```powershell
$OKButton = New-Object System.Windows.Forms.Button
$OKButton.Location = New-Object System.Drawing.Size(75,120)
$OKButton.Size = New-Object System.Drawing.Size(75,23)
$OKButton.Text = 'OK'
$OKButton.DialogResult = [System.Windows.Forms.DialogResult]::OK
$form.AcceptButton = $OKButton
$form.Controls.Add($OKButton)
```

Hasonlóképpen, létrehozhat egy **Mégse** gombra. A **Mégse** gomb, a lista elejéről 120 képpont, de az ablak bal szélétől 150 képpont.

```powershell
$CancelButton = New-Object System.Windows.Forms.Button
$CancelButton.Location = New-Object System.Drawing.Point(150,120)
$CancelButton.Size = New-Object System.Drawing.Size(75,23)
$CancelButton.Text = 'Cancel'
$CancelButton.DialogResult = [System.Windows.Forms.DialogResult]::Cancel
$form.CancelButton = $CancelButton
$form.Controls.Add($CancelButton)
```

A következő adja meg a címke szövegét, a ablakban adja meg a felhasználók a információkat.

```powershell
$label = New-Object System.Windows.Forms.Label
$label.Location = New-Object System.Drawing.Point(10,20)
$label.Size = New-Object System.Drawing.Size(280,20)
$label.Text = 'Please make a selection from the list below:'
$form.Controls.Add($label)
```

Adja hozzá a vezérlő (ebben az esetben egy lista), amely lehetővé teszi a felhasználóknak adja meg az adatokat, akkor már ismertetett a címke szövegét. Nincsenek alkalmazhat szövegmezőkben; mellett sok más vezérlők További vezérlők, lásd: [System.Windows.Forms Namespace](http://msdn.microsoft.com/library/k50ex0x9(v=vs.110).aspx) az MSDN Webhelyén.

```powershell
$listBox = New-Object System.Windows.Forms.Listbox
$listBox.Location = New-Object System.Drawing.Point(10,40)
$listBox.Size = New-Object System.Drawing.Size(260,20)
```

Itt látható, hogyan adhatja meg, hogy szeretné-e a felhasználók megadhatják több értéket a listából.

```powershell
$listBox.SelectionMode = 'MultiExtended'
```

A következő szakaszban adja meg a felhasználók számára megjelenítendő a lista kívánt értékeket.

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

A lista vezérlőelem vegye fel az űrlap, és kérje meg a Windows a képernyő elveire más windows és a párbeszédpanel megnyitásához, ha meg van nyitva.

```powershell
$form.Controls.Add($listBox)
$form.Topmost = $true
```

Adja hozzá a következő kódsort a képernyőn megjelenő Windows.

```powershell
$result = $form.ShowDialog()
```

Végezetül, a kódot a **Ha** blokk utasítja Windows Mi a teendő az űrlapot, miután a felhasználók egy vagy több lehetőséget válassza a legördülő listából, és kattintson a **OK** gombra vagy nyomja meg a **Enter**  kulcs.

```powershell
if ($result -eq [System.Windows.Forms.DialogResult]::OK)
{
    $x = $listBox.SelectedItems
    $x
}
```

## <a name="see-also"></a>Lásd még:

- [Hey Scripting Guy: Miért nem PowerShell grafikus felhasználói Felülettel példákban használhatók?](http://go.microsoft.com/fwlink/?LinkId=506644)
- [GitHub: Dave Wyatt WinFormsExampleUpdates](https://github.com/dlwyatt/WinFormsExampleUpdates)
- [A hét Windows PowerShell tipp: Jelölje ki a listában be - és egyéb!](http://technet.microsoft.com/library/ff730950.aspx)