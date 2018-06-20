---
ms.date: 06/05/2017
keywords: PowerShell parancsmag
title: Egyéni beviteli mező létrehozása
ms.assetid: 0b12e56c-299f-40ee-afbf-d30d23ed2565
ms.openlocfilehash: 681a75a28a8fb03eb4442d5e20b32b25a337d540
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
ms.locfileid: "30954755"
---
# <a name="creating-a-custom-input-box"></a>Egyéni beviteli mező létrehozása

A parancsfájl egy grafikus egyéni beviteli mezőt a Microsoft .NET-keretrendszer űrlap-összeállító szolgáltatások a Windows PowerShell 3.0-s és újabb verziókban.

## <a name="create-a-custom-graphical-input-box"></a>Hozzon létre egy egyéni, grafikus beviteli mezőbe

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
$label.Text = 'Please enter the information in the space below:'
$form.Controls.Add($label)

$textBox = New-Object System.Windows.Forms.TextBox
$textBox.Location = New-Object System.Drawing.Point(10,40)
$textBox.Size = New-Object System.Drawing.Size(260,20)
$form.Controls.Add($textBox)

$form.Topmost = $true

$form.Add_Shown({$textBox.Select()})
$result = $form.ShowDialog()

if ($result -eq [System.Windows.Forms.DialogResult]::OK)
{
    $x = $textBox.Text
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
$OKButton.Location = New-Object System.Drawing.Point(75,120)
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
$label.Text = 'Please enter the information in the space below:'
$form.Controls.Add($label)
```

Adja hozzá a vezérlő (ebben az esetben a szövegmező), amely lehetővé teszi a felhasználóknak adja meg az adatokat, akkor már ismertetett a címke szövegét. Nincsenek alkalmazhat szövegmezőkben; mellett sok más vezérlők További vezérlők, lásd: [System.Windows.Forms Namespace](http://msdn.microsoft.com/library/k50ex0x9(v=vs.110).aspx) az MSDN Webhelyén.

```powershell
$textBox = New-Object System.Windows.Forms.TextBox
$textBox.Location = New-Object System.Drawing.Point(10,40)
$textBox.Size = New-Object System.Drawing.Size(260,20)
$form.Controls.Add($textBox)
```

Állítsa be a **Topmost** tulajdonságot **$true** azzal kényszerítheti a az ablak elveire más nyissa meg a windows és a párbeszédpanel megnyitásához.

```powershell
$form.Topmost = $true
```

Ezután adja hozzá a kódsort az űrlap aktiválásához, és a fókuszt a létrehozott szövegdobozba.

```powershell
$form.Add_Shown({$textBox.Select()})
```

Adja hozzá a következő kódsort a képernyőn megjelenő Windows.

```powershell
$result = $form.ShowDialog()
```

Végezetül, a kódot a **Ha** blokk utasítja Windows Mi a teendő az űrlapot, miután a felhasználók szöveg a szövegmezőben adja meg, és kattintson a **OK** gombra vagy nyomja meg a **Enter** kulcs.

```powershell
if ($result -eq [System.Windows.Forms.DialogResult]::OK)
{
    $x = $textBox.Text
    $x
}
```

## <a name="see-also"></a>Lásd még:

- [Hey Scripting Guy: Miért nem PowerShell grafikus felhasználói Felülettel példákban használhatók?](http://go.microsoft.com/fwlink/?LinkId=506644)
- [GitHub: Dave Wyatt WinFormsExampleUpdates](https://github.com/dlwyatt/WinFormsExampleUpdates)
- [A hét Windows PowerShell tipp: egyéni létrehozása beviteli mező](http://technet.microsoft.com/library/ff730941.aspx)