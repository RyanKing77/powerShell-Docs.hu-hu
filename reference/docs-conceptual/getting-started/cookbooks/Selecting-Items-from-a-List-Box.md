---
ms.date: 2017-06-05
keywords: PowerShell parancsmag
title: "Lista elemek kijelölése"
ms.assetid: 327c7cc5-21d0-4ace-b151-aa1491d1d3c2
ms.openlocfilehash: 5b41ebfb193062a17abcc6ad6ddf1a2d9241a39e
ms.sourcegitcommit: d6ab9ab5909ed59cce4ce30e29457e0e75c7ac12
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/08/2017
---
# <a name="selecting-items-from-a-list-box"></a>Lista elemek kijelölése
Egy párbeszédpanelt, amely lehetővé teszi, hogy a rendszergazdák kiválaszthatják az elemeket a lista vezérlőelemet létrehozásához használja a Windows PowerShell 3.0-s és újabb verziókban.

## <a name="create-a-list-box-control-and-select-items-from-it"></a>Hozzon létre egy lista vezérlőelem, és válassza ki az elemeket
Másolja és illessze be a következő Windows PowerShell ISE-be, és mentse egy Windows PowerShell-parancsfájlt (.ps1).

```
Add-Type -AssemblyName System.Windows.Forms
Add-Type -AssemblyName System.Drawing

$form = New-Object System.Windows.Forms.Form 
$form.Text = "Select a Computer"
$form.Size = New-Object System.Drawing.Size(300,200) 
$form.StartPosition = "CenterScreen"

$OKButton = New-Object System.Windows.Forms.Button
$OKButton.Location = New-Object System.Drawing.Point(75,120)
$OKButton.Size = New-Object System.Drawing.Size(75,23)
$OKButton.Text = "OK"
$OKButton.DialogResult = [System.Windows.Forms.DialogResult]::OK
$form.AcceptButton = $OKButton
$form.Controls.Add($OKButton)

$CancelButton = New-Object System.Windows.Forms.Button
$CancelButton.Location = New-Object System.Drawing.Point(150,120)
$CancelButton.Size = New-Object System.Drawing.Size(75,23)
$CancelButton.Text = "Cancel"
$CancelButton.DialogResult = [System.Windows.Forms.DialogResult]::Cancel
$form.CancelButton = $CancelButton
$form.Controls.Add($CancelButton)

$label = New-Object System.Windows.Forms.Label
$label.Location = New-Object System.Drawing.Point(10,20) 
$label.Size = New-Object System.Drawing.Size(280,20) 
$label.Text = "Please select a computer:"
$form.Controls.Add($label) 

$listBox = New-Object System.Windows.Forms.ListBox 
$listBox.Location = New-Object System.Drawing.Point(10,40) 
$listBox.Size = New-Object System.Drawing.Size(260,20) 
$listBox.Height = 80

[void] $listBox.Items.Add("atl-dc-001")
[void] $listBox.Items.Add("atl-dc-002")
[void] $listBox.Items.Add("atl-dc-003")
[void] $listBox.Items.Add("atl-dc-004")
[void] $listBox.Items.Add("atl-dc-005")
[void] $listBox.Items.Add("atl-dc-006")
[void] $listBox.Items.Add("atl-dc-007")

$form.Controls.Add($listBox) 

$form.Topmost = $True

$result = $form.ShowDialog()

if ($result -eq [System.Windows.Forms.DialogResult]::OK)
{
    $x = $listBox.SelectedItem
    $x
}
```

A parancsfájl első lépése két .NET-keretrendszer osztály betöltése: **System.Drawing** és **System.Windows.Forms**. Majd indítsa el a .NET-keretrendszer osztály új példánya **: System.Windows.Forms.Form**; biztosítja az üres űrlapból, vagy ablak, amelyhez elkezdhet szabályozza.

```
Add-Type -AssemblyName System.Windows.Forms
Add-Type -AssemblyName System.Drawing
```

Az űrlap osztály példányának létrehozása után értéket hozzárendelni az osztály három tulajdonságot.

- **Szöveg.** Ez lesz az ablak címe.

- **Méret.** Ez az az űrlap képpontban méretét. A fenti parancsfájl űrlapot hoz létre, amely 300 x 200 magassága képpontban megadva.

- **StartingPosition.** Ez nem kötelező tulajdonság értéke **CenterScreen** az előző parancsfájlban. Ez a tulajdonság nem ad hozzá, ha a Windows kiválaszt egy helyet, az űrlap megnyitásakor. Úgy, hogy a **StartingPosition** való **CenterScreen**, akkor program automatikusan jeleníti meg az űrlap közepén a képernyő minden alkalommal, amikor betölti a.

```
$form.Text = "Select a Computer"
$form.Size = New-Object System.Drawing.Size(300,200) 
$form.StartPosition = "CenterScreen"
```

Ezután hozzon létre egy **OK** gombra az űrlap. Adja meg a méretét és viselkedését a **OK** gombra. Ebben a példában a gomb pozíciója a képernyő felső szélétől 120 képpont, de 75 képpont bal szélétől. A gomb magassága 23 képpont, amíg a gomb hossza 75 képpontban megadva. A parancsfájl előre meghatározott Windows Forms-típusok gombra viselkedésmódját meghatározására használja.

```
$OKButton = New-Object System.Windows.Forms.Button
$OKButton.Location = New-Object System.Drawing.Point(75,120)
$OKButton.Size = New-Object System.Drawing.Size(75,23)
$OKButton.Text = "OK"
$OKButton.DialogResult = [System.Windows.Forms.DialogResult]::OK
$form.AcceptButton = $OKButton
$form.Controls.Add($OKButton)
```

Hasonlóképpen, létrehozhat egy **Mégse** gombra. A **Mégse** gomb, a lista elejéről 120 képpont, de az ablak bal szélétől 150 képpont.

```
$CancelButton = New-Object System.Windows.Forms.Button
$CancelButton.Location = New-Object System.Drawing.Point(150,120)
$CancelButton.Size = New-Object System.Drawing.Size(75,23)
$CancelButton.Text = "Cancel"
$CancelButton.DialogResult = [System.Windows.Forms.DialogResult]::Cancel
$form.CancelButton = $CancelButton
$form.Controls.Add($CancelButton)
```

A következő adja meg a címke szövegét, a ablakban adja meg a felhasználók a információkat. Ebben az esetben érdemes a felhasználóknak, hogy a számítógép.

```
$label = New-Object System.Windows.Forms.Label
$label.Location = New-Object System.Drawing.Point(10,20) 
$label.Size = New-Object System.Drawing.Size(280,20) 
$label.Text = "Please select a computer:"
$form.Controls.Add($label)
```

Adja hozzá a vezérlő (ebben az esetben egy lista), amely lehetővé teszi a felhasználóknak adja meg az adatokat, akkor már ismertetett a címke szövegét. Nincsenek alkalmazhat listák; mellett sok más vezérlők További vezérlők, lásd: [System.Windows.Forms Namespace](http://msdn.microsoft.com/library/k50ex0x9(v=vs.110).aspx) az MSDN Webhelyén.

```
$listBox = New-Object System.Windows.Forms.ListBox 
$listBox.Location = New-Object System.Drawing.Point(10,40) 
$listBox.Size = New-Object System.Drawing.Size(260,20) 
$listBox.Height = 80
```

A következő szakaszban adja meg a felhasználók számára megjelenítendő a lista kívánt értékeket.

> [!NOTE]
> A lista hozta létre a parancsfájl a csak egy kiválasztását teszi lehetővé. Egy lista vezérlőelem, amely lehetővé teszi több kijelölés létrehozásához adjon meg értéket a **SelectionMode** tulajdonságot, hasonlóan a következő: `$listBox.SelectionMode = "MultiExtended"`. További információkért lásd: [többszörös kijelölés listák](Multiple-selection-List-Boxes.md).

```
[void] $listBox.Items.Add("atl-dc-001")
[void] $listBox.Items.Add("atl-dc-002")
[void] $listBox.Items.Add("atl-dc-003")
[void] $listBox.Items.Add("atl-dc-004")
[void] $listBox.Items.Add("atl-dc-005")
[void] $listBox.Items.Add("atl-dc-006")
[void] $listBox.Items.Add("atl-dc-007")
```

A lista vezérlőelem vegye fel az űrlap, és kérje meg a Windows a képernyő elveire más windows és a párbeszédpanel megnyitásához, ha meg van nyitva.

```
$form.Controls.Add($listBox) 
$form.Topmost = $True
```

Adja hozzá a következő kódsort a képernyőn megjelenő Windows.

```
$result = $form.ShowDialog()
```

Végezetül, a kódot a **Ha** blokk utasítja Windows Mi a teendő az űrlapot, miután a felhasználók jelöljön ki egy lehetőséget a legördülő listából, és kattintson a **OK** gombra vagy nyomja le az **Enter**kulcs.

```
if ($result -eq [System.Windows.Forms.DialogResult]::OK)
{
    $x = $listBox.SelectedItem
    $x
}
```

## <a name="see-also"></a>Lásd még:
- [Hey Scripting Guy: Miért nem PowerShell grafikus felhasználói Felülettel példákban használhatók?](http://go.microsoft.com/fwlink/?LinkId=506644)
- [GitHub: Dave Wyatt WinFormsExampleUpdates](https://github.com/dlwyatt/WinFormsExampleUpdates)
- [A hét Windows PowerShell tipp: lista elemek kijelölése](http://technet.microsoft.com/library/ff730949.aspx)

