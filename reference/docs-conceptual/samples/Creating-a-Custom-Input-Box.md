---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: Egyéni beviteli mező létrehozása
ms.assetid: 0b12e56c-299f-40ee-afbf-d30d23ed2565
ms.openlocfilehash: 2d04ad6df65cdb4ff13d136dea47bbba6a01f3a2
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404153"
---
# <a name="creating-a-custom-input-box"></a>Egyéni beviteli mező létrehozása

A Microsoft .NET-keretrendszer űrlap-összeállító szolgáltatások a Windows PowerShell 3.0-s és újabb kiadásaiban a grafikus egyéni beviteli mező-szkript.

## <a name="create-a-custom-graphical-input-box"></a>Egy egyéni, grafikus beviteli mező létrehozása

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

Következő lépésként adja meg az ablak, amely leírja az adatokat, adja meg a felhasználók a felirat szövege.

```powershell
$label = New-Object System.Windows.Forms.Label
$label.Location = New-Object System.Drawing.Point(10,20)
$label.Size = New-Object System.Drawing.Size(280,20)
$label.Text = 'Please enter the information in the space below:'
$form.Controls.Add($label)
```

Adja hozzá a vezérlő (ebben az esetben a szövegmezőbe), amely lehetővé teszi a felhasználóknak adja meg az adatokat, akkor már ismertetett a felirat szövege. Nincsenek alkalmazhat szövegmezők; mellett számos más vezérlők További vezérlők, lásd: [System.Windows.Forms Namespace](https://msdn.microsoft.com/library/k50ex0x9(v=vs.110).aspx) az MSDN Webhelyén.

```powershell
$textBox = New-Object System.Windows.Forms.TextBox
$textBox.Location = New-Object System.Drawing.Point(10,40)
$textBox.Size = New-Object System.Drawing.Size(260,20)
$form.Controls.Add($textBox)
```

Állítsa be a **Topmost** tulajdonságot **$true** kényszerítése az ablak megnyitásához nyissa meg a windows és a párbeszédpanelek interaktív irányítópultunkat.

```powershell
$form.Topmost = $true
```

Ezután adja hozzá a kódsort az űrlap aktiválásához, és a fókuszt a szövegdobozba, amelyet Ön hozott létre.

```powershell
$form.Add_Shown({$textBox.Select()})
```

Adja hozzá az alábbi kódsort az űrlap megjelenítésére a Windows.

```powershell
$result = $form.ShowDialog()
```

Végül a kód belül a **Ha** blokk arra utasítja a Windows Mi a teendő az űrlapot, miután a felhasználók adjon meg szöveget a szövegmezőbe, és kattintson a **OK** gombra vagy nyomja le a **Enter** kulcs.

```powershell
if ($result -eq [System.Windows.Forms.DialogResult]::OK)
{
    $x = $textBox.Text
    $x
}
```

## <a name="see-also"></a>Lásd még:

- [Hey Scripting Guy:  Miért nem működnek a grafikus PowerShell-példákat?](https://go.microsoft.com/fwlink/?LinkId=506644)
- [GitHub: Dave Wyatt WinFormsExampleUpdates](https://github.com/dlwyatt/WinFormsExampleUpdates)
- [Windows PowerShell Tip of the Week:  Egyéni beviteli mező létrehozása](https://technet.microsoft.com/library/ff730941.aspx)