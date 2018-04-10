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
---
# <a name="creating-a-custom-input-box"></a><span data-ttu-id="19db6-103">Egyéni beviteli mező létrehozása</span><span class="sxs-lookup"><span data-stu-id="19db6-103">Creating a Custom Input Box</span></span>

<span data-ttu-id="19db6-104">A parancsfájl egy grafikus egyéni beviteli mezőt a Microsoft .NET-keretrendszer űrlap-összeállító szolgáltatások a Windows PowerShell 3.0-s és újabb verziókban.</span><span class="sxs-lookup"><span data-stu-id="19db6-104">Script a graphical custom input box by using Microsoft .NET Framework form-building features in Windows PowerShell 3.0 and later releases.</span></span>

## <a name="create-a-custom-graphical-input-box"></a><span data-ttu-id="19db6-105">Hozzon létre egy egyéni, grafikus beviteli mezőbe</span><span class="sxs-lookup"><span data-stu-id="19db6-105">Create a custom, graphical input box</span></span>

<span data-ttu-id="19db6-106">Másolja és illessze be a következő Windows PowerShell ISE-be, és mentse egy Windows PowerShell-parancsfájlt (.ps1).</span><span class="sxs-lookup"><span data-stu-id="19db6-106">Copy and then paste the following into Windows PowerShell ISE, and then save it as a Windows PowerShell script (.ps1).</span></span>

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

<span data-ttu-id="19db6-107">A parancsfájl első lépése két .NET-keretrendszer osztály betöltése: **System.Drawing** és **System.Windows.Forms**.</span><span class="sxs-lookup"><span data-stu-id="19db6-107">The script begins by loading two .NET Framework classes: **System.Drawing** and **System.Windows.Forms**.</span></span> <span data-ttu-id="19db6-108">Majd indítsa el a .NET-keretrendszer osztály új példánya **: System.Windows.Forms.Form**; biztosítja az üres űrlapból, vagy ablak, amelyhez elkezdhet szabályozza.</span><span class="sxs-lookup"><span data-stu-id="19db6-108">You then start a new instance of the .NET Framework class **System.Windows.Forms.Form**; that provides a blank form or window to which you can start adding controls.</span></span>

```powershell
$form = New-Object System.Windows.Forms.Form
```

<span data-ttu-id="19db6-109">Az űrlap osztály példányának létrehozása után értéket hozzárendelni az osztály három tulajdonságot.</span><span class="sxs-lookup"><span data-stu-id="19db6-109">After you create an instance of the Form class, assign values to three properties of this class.</span></span>

- <span data-ttu-id="19db6-110">**Text.**</span><span class="sxs-lookup"><span data-stu-id="19db6-110">**Text.**</span></span> <span data-ttu-id="19db6-111">Ez lesz az ablak címe.</span><span class="sxs-lookup"><span data-stu-id="19db6-111">This becomes the title of the window.</span></span>

- <span data-ttu-id="19db6-112">**Size.**</span><span class="sxs-lookup"><span data-stu-id="19db6-112">**Size.**</span></span> <span data-ttu-id="19db6-113">Ez az az űrlap képpontban méretét.</span><span class="sxs-lookup"><span data-stu-id="19db6-113">This is the size of the form, in pixels.</span></span> <span data-ttu-id="19db6-114">A fenti parancsfájl űrlapot hoz létre, amely 300 x 200 magassága képpontban megadva.</span><span class="sxs-lookup"><span data-stu-id="19db6-114">The preceding script creates a form that’s 300 pixels wide by 200 pixels tall.</span></span>

- <span data-ttu-id="19db6-115">**StartingPosition.**</span><span class="sxs-lookup"><span data-stu-id="19db6-115">**StartingPosition.**</span></span> <span data-ttu-id="19db6-116">Ez nem kötelező tulajdonság értéke **CenterScreen** az előző parancsfájlban.</span><span class="sxs-lookup"><span data-stu-id="19db6-116">This optional property is set to **CenterScreen** in the preceding script.</span></span> <span data-ttu-id="19db6-117">Ez a tulajdonság nem ad hozzá, ha a Windows kiválaszt egy helyet, az űrlap megnyitásakor.</span><span class="sxs-lookup"><span data-stu-id="19db6-117">If you don’t add this property, Windows selects a location when the form is opened.</span></span> <span data-ttu-id="19db6-118">Úgy, hogy a **StartingPosition** való **CenterScreen**, akkor program automatikusan jeleníti meg az űrlap közepén a képernyő minden alkalommal, amikor betölti a.</span><span class="sxs-lookup"><span data-stu-id="19db6-118">By setting the **StartingPosition** to **CenterScreen**, you’re automatically displaying the form in the middle of the screen each time it loads.</span></span>

```powershell
$form.Text = 'Data Entry Form'
$form.Size = New-Object System.Drawing.Size(300,200)
$form.StartPosition = 'CenterScreen'
```

<span data-ttu-id="19db6-119">Ezután hozzon létre egy **OK** gombra az űrlap.</span><span class="sxs-lookup"><span data-stu-id="19db6-119">Next, create an **OK** button for your form.</span></span> <span data-ttu-id="19db6-120">Adja meg a méretét és viselkedését a **OK** gombra.</span><span class="sxs-lookup"><span data-stu-id="19db6-120">Specify the size and behavior of the **OK** button.</span></span> <span data-ttu-id="19db6-121">Ebben a példában a gomb pozíciója a képernyő felső szélétől 120 képpont, de 75 képpont bal szélétől.</span><span class="sxs-lookup"><span data-stu-id="19db6-121">In this example, the button position is 120 pixels from the form’s top edge, and 75 pixels from the left edge.</span></span> <span data-ttu-id="19db6-122">A gomb magassága 23 képpont, amíg a gomb hossza 75 képpontban megadva.</span><span class="sxs-lookup"><span data-stu-id="19db6-122">The button height is 23 pixels, while the button length is 75 pixels.</span></span> <span data-ttu-id="19db6-123">A parancsfájl előre meghatározott Windows Forms-típusok gombra viselkedésmódját meghatározására használja.</span><span class="sxs-lookup"><span data-stu-id="19db6-123">The script uses predefined Windows Forms types to determine the button behaviors.</span></span>

```powershell
$OKButton = New-Object System.Windows.Forms.Button
$OKButton.Location = New-Object System.Drawing.Point(75,120)
$OKButton.Size = New-Object System.Drawing.Size(75,23)
$OKButton.Text = 'OK'
$OKButton.DialogResult = [System.Windows.Forms.DialogResult]::OK
$form.AcceptButton = $OKButton
$form.Controls.Add($OKButton)
```

<span data-ttu-id="19db6-124">Hasonlóképpen, létrehozhat egy **Mégse** gombra.</span><span class="sxs-lookup"><span data-stu-id="19db6-124">Similarly, you create a **Cancel** button.</span></span> <span data-ttu-id="19db6-125">A **Mégse** gomb, a lista elejéről 120 képpont, de az ablak bal szélétől 150 képpont.</span><span class="sxs-lookup"><span data-stu-id="19db6-125">The **Cancel** button is 120 pixels from the top, but 150 pixels from the left edge of the window.</span></span>

```powershell
$CancelButton = New-Object System.Windows.Forms.Button
$CancelButton.Location = New-Object System.Drawing.Point(150,120)
$CancelButton.Size = New-Object System.Drawing.Size(75,23)
$CancelButton.Text = 'Cancel'
$CancelButton.DialogResult = [System.Windows.Forms.DialogResult]::Cancel
$form.CancelButton = $CancelButton
$form.Controls.Add($CancelButton)
```

<span data-ttu-id="19db6-126">A következő adja meg a címke szövegét, a ablakban adja meg a felhasználók a információkat.</span><span class="sxs-lookup"><span data-stu-id="19db6-126">Next, provide label text on your window that describes the information you want users to provide.</span></span>

```powershell
$label = New-Object System.Windows.Forms.Label
$label.Location = New-Object System.Drawing.Point(10,20)
$label.Size = New-Object System.Drawing.Size(280,20)
$label.Text = 'Please enter the information in the space below:'
$form.Controls.Add($label)
```

<span data-ttu-id="19db6-127">Adja hozzá a vezérlő (ebben az esetben a szövegmező), amely lehetővé teszi a felhasználóknak adja meg az adatokat, akkor már ismertetett a címke szövegét.</span><span class="sxs-lookup"><span data-stu-id="19db6-127">Add the control (in this case, a text box) that lets users provide the information you’ve described in your label text.</span></span> <span data-ttu-id="19db6-128">Nincsenek alkalmazhat szövegmezőkben; mellett sok más vezérlők További vezérlők, lásd: [System.Windows.Forms Namespace](http://msdn.microsoft.com/library/k50ex0x9(v=vs.110).aspx) az MSDN Webhelyén.</span><span class="sxs-lookup"><span data-stu-id="19db6-128">There are many other controls you can apply besides text boxes; for more controls, see [System.Windows.Forms Namespace](http://msdn.microsoft.com/library/k50ex0x9(v=vs.110).aspx) on MSDN.</span></span>

```powershell
$textBox = New-Object System.Windows.Forms.TextBox
$textBox.Location = New-Object System.Drawing.Point(10,40)
$textBox.Size = New-Object System.Drawing.Size(260,20)
$form.Controls.Add($textBox)
```

<span data-ttu-id="19db6-129">Állítsa be a **Topmost** tulajdonságot **$true** azzal kényszerítheti a az ablak elveire más nyissa meg a windows és a párbeszédpanel megnyitásához.</span><span class="sxs-lookup"><span data-stu-id="19db6-129">Set the **Topmost** property to **$true** to force the window to open atop other open windows and dialog boxes.</span></span>

```powershell
$form.Topmost = $true
```

<span data-ttu-id="19db6-130">Ezután adja hozzá a kódsort az űrlap aktiválásához, és a fókuszt a létrehozott szövegdobozba.</span><span class="sxs-lookup"><span data-stu-id="19db6-130">Next, add this line of code to activate the form, and set the focus to the text box that you created.</span></span>

```powershell
$form.Add_Shown({$textBox.Select()})
```

<span data-ttu-id="19db6-131">Adja hozzá a következő kódsort a képernyőn megjelenő Windows.</span><span class="sxs-lookup"><span data-stu-id="19db6-131">Add the following line of code to display the form in Windows.</span></span>

```powershell
$result = $form.ShowDialog()
```

<span data-ttu-id="19db6-132">Végezetül, a kódot a **Ha** blokk utasítja Windows Mi a teendő az űrlapot, miután a felhasználók szöveg a szövegmezőben adja meg, és kattintson a **OK** gombra vagy nyomja meg a **Enter** kulcs.</span><span class="sxs-lookup"><span data-stu-id="19db6-132">Finally, the code inside the **If** block instructs Windows what to do with the form after users provide text in the text box, and then click the **OK** button or press the **Enter** key.</span></span>

```powershell
if ($result -eq [System.Windows.Forms.DialogResult]::OK)
{
    $x = $textBox.Text
    $x
}
```

## <a name="see-also"></a><span data-ttu-id="19db6-133">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="19db6-133">See Also</span></span>

- [<span data-ttu-id="19db6-134">Hey Scripting Guy: Miért nem PowerShell grafikus felhasználói Felülettel példákban használhatók?</span><span class="sxs-lookup"><span data-stu-id="19db6-134">Hey Scripting Guy:  Why don’t these PowerShell GUI examples work?</span></span>](http://go.microsoft.com/fwlink/?LinkId=506644)
- [<span data-ttu-id="19db6-135">GitHub: Dave Wyatt WinFormsExampleUpdates</span><span class="sxs-lookup"><span data-stu-id="19db6-135">GitHub: Dave Wyatt's WinFormsExampleUpdates</span></span>](https://github.com/dlwyatt/WinFormsExampleUpdates)
- [<span data-ttu-id="19db6-136">A hét Windows PowerShell tipp: egyéni létrehozása beviteli mező</span><span class="sxs-lookup"><span data-stu-id="19db6-136">Windows PowerShell Tip of the Week:  Creating a Custom Input Box</span></span>](http://technet.microsoft.com/library/ff730941.aspx)