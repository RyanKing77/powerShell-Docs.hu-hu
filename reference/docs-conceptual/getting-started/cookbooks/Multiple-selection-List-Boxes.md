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
# <a name="multiple-selection-list-boxes"></a><span data-ttu-id="7ad05-103">Több kijelölési</span><span class="sxs-lookup"><span data-stu-id="7ad05-103">Multiple-selection List Boxes</span></span>

<span data-ttu-id="7ad05-104">Egyéni Windows űrlapon többszörös kijelölés lista vezérlőelemet létrehozásához használja a Windows PowerShell 3.0-s és újabb verziókban.</span><span class="sxs-lookup"><span data-stu-id="7ad05-104">Use Windows PowerShell 3.0 and later releases to create a multiple-selection list box control in a custom Windows Form.</span></span>

## <a name="create-list-box-controls-that-allow-multiple-selections"></a><span data-ttu-id="7ad05-105">Lista létrehozása, amelyek lehetővé teszik több kijelölés vezérlők</span><span class="sxs-lookup"><span data-stu-id="7ad05-105">Create list box controls that allow multiple selections</span></span>

<span data-ttu-id="7ad05-106">Másolja és illessze be a következő Windows PowerShell ISE-be, és mentse egy Windows PowerShell-parancsfájlt (.ps1).</span><span class="sxs-lookup"><span data-stu-id="7ad05-106">Copy and then paste the following into Windows PowerShell ISE, and then save it as a Windows PowerShell script (.ps1).</span></span>

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

<span data-ttu-id="7ad05-107">A parancsfájl első lépése két .NET-keretrendszer osztály betöltése: **System.Drawing** és **System.Windows.Forms**.</span><span class="sxs-lookup"><span data-stu-id="7ad05-107">The script begins by loading two .NET Framework classes: **System.Drawing** and **System.Windows.Forms**.</span></span> <span data-ttu-id="7ad05-108">Majd indítsa el a .NET-keretrendszer osztály új példánya **: System.Windows.Forms.Form**; biztosítja az üres űrlapból, vagy ablak, amelyhez elkezdhet szabályozza.</span><span class="sxs-lookup"><span data-stu-id="7ad05-108">You then start a new instance of the .NET Framework class **System.Windows.Forms.Form**; that provides a blank form or window to which you can start adding controls.</span></span>

```powershell
$form = New-Object System.Windows.Forms.Form
```

<span data-ttu-id="7ad05-109">Az űrlap osztály példányának létrehozása után értéket hozzárendelni az osztály három tulajdonságot.</span><span class="sxs-lookup"><span data-stu-id="7ad05-109">After you create an instance of the Form class, assign values to three properties of this class.</span></span>

- <span data-ttu-id="7ad05-110">**Text.**</span><span class="sxs-lookup"><span data-stu-id="7ad05-110">**Text.**</span></span> <span data-ttu-id="7ad05-111">Ez lesz az ablak címe.</span><span class="sxs-lookup"><span data-stu-id="7ad05-111">This becomes the title of the window.</span></span>

- <span data-ttu-id="7ad05-112">**Size.**</span><span class="sxs-lookup"><span data-stu-id="7ad05-112">**Size.**</span></span> <span data-ttu-id="7ad05-113">Ez az az űrlap képpontban méretét.</span><span class="sxs-lookup"><span data-stu-id="7ad05-113">This is the size of the form, in pixels.</span></span> <span data-ttu-id="7ad05-114">A fenti parancsfájl űrlapot hoz létre, amely 300 x 200 magassága képpontban megadva.</span><span class="sxs-lookup"><span data-stu-id="7ad05-114">The preceding script creates a form that’s 300 pixels wide by 200 pixels tall.</span></span>

- <span data-ttu-id="7ad05-115">**StartingPosition.**</span><span class="sxs-lookup"><span data-stu-id="7ad05-115">**StartingPosition.**</span></span> <span data-ttu-id="7ad05-116">Ez nem kötelező tulajdonság értéke **CenterScreen** az előző parancsfájlban.</span><span class="sxs-lookup"><span data-stu-id="7ad05-116">This optional property is set to **CenterScreen** in the preceding script.</span></span> <span data-ttu-id="7ad05-117">Ez a tulajdonság nem ad hozzá, ha a Windows kiválaszt egy helyet, az űrlap megnyitásakor.</span><span class="sxs-lookup"><span data-stu-id="7ad05-117">If you don’t add this property, Windows selects a location when the form is opened.</span></span> <span data-ttu-id="7ad05-118">Úgy, hogy a **StartingPosition** való **CenterScreen**, akkor program automatikusan jeleníti meg az űrlap közepén a képernyő minden alkalommal, amikor betölti a.</span><span class="sxs-lookup"><span data-stu-id="7ad05-118">By setting the **StartingPosition** to **CenterScreen**, you’re automatically displaying the form in the middle of the screen each time it loads.</span></span>

```powershell
$form.Text = 'Data Entry Form'
$form.Size = New-Object System.Drawing.Size(300,200)
$form.StartPosition = 'CenterScreen'
```

<span data-ttu-id="7ad05-119">Ezután hozzon létre egy **OK** gombra az űrlap.</span><span class="sxs-lookup"><span data-stu-id="7ad05-119">Next, create an **OK** button for your form.</span></span> <span data-ttu-id="7ad05-120">Adja meg a méretét és viselkedését a **OK** gombra.</span><span class="sxs-lookup"><span data-stu-id="7ad05-120">Specify the size and behavior of the **OK** button.</span></span> <span data-ttu-id="7ad05-121">Ebben a példában a gomb pozíciója a képernyő felső szélétől 120 képpont, de 75 képpont bal szélétől.</span><span class="sxs-lookup"><span data-stu-id="7ad05-121">In this example, the button position is 120 pixels from the form’s top edge, and 75 pixels from the left edge.</span></span> <span data-ttu-id="7ad05-122">A gomb magassága 23 képpont, amíg a gomb hossza 75 képpontban megadva.</span><span class="sxs-lookup"><span data-stu-id="7ad05-122">The button height is 23 pixels, while the button length is 75 pixels.</span></span> <span data-ttu-id="7ad05-123">A parancsfájl előre meghatározott Windows Forms-típusok gombra viselkedésmódját meghatározására használja.</span><span class="sxs-lookup"><span data-stu-id="7ad05-123">The script uses predefined Windows Forms types to determine the button behaviors.</span></span>

```powershell
$OKButton = New-Object System.Windows.Forms.Button
$OKButton.Location = New-Object System.Drawing.Size(75,120)
$OKButton.Size = New-Object System.Drawing.Size(75,23)
$OKButton.Text = 'OK'
$OKButton.DialogResult = [System.Windows.Forms.DialogResult]::OK
$form.AcceptButton = $OKButton
$form.Controls.Add($OKButton)
```

<span data-ttu-id="7ad05-124">Hasonlóképpen, létrehozhat egy **Mégse** gombra.</span><span class="sxs-lookup"><span data-stu-id="7ad05-124">Similarly, you create a **Cancel** button.</span></span> <span data-ttu-id="7ad05-125">A **Mégse** gomb, a lista elejéről 120 képpont, de az ablak bal szélétől 150 képpont.</span><span class="sxs-lookup"><span data-stu-id="7ad05-125">The **Cancel** button is 120 pixels from the top, but 150 pixels from the left edge of the window.</span></span>

```powershell
$CancelButton = New-Object System.Windows.Forms.Button
$CancelButton.Location = New-Object System.Drawing.Point(150,120)
$CancelButton.Size = New-Object System.Drawing.Size(75,23)
$CancelButton.Text = 'Cancel'
$CancelButton.DialogResult = [System.Windows.Forms.DialogResult]::Cancel
$form.CancelButton = $CancelButton
$form.Controls.Add($CancelButton)
```

<span data-ttu-id="7ad05-126">A következő adja meg a címke szövegét, a ablakban adja meg a felhasználók a információkat.</span><span class="sxs-lookup"><span data-stu-id="7ad05-126">Next, provide label text on your window that describes the information you want users to provide.</span></span>

```powershell
$label = New-Object System.Windows.Forms.Label
$label.Location = New-Object System.Drawing.Point(10,20)
$label.Size = New-Object System.Drawing.Size(280,20)
$label.Text = 'Please make a selection from the list below:'
$form.Controls.Add($label)
```

<span data-ttu-id="7ad05-127">Adja hozzá a vezérlő (ebben az esetben egy lista), amely lehetővé teszi a felhasználóknak adja meg az adatokat, akkor már ismertetett a címke szövegét.</span><span class="sxs-lookup"><span data-stu-id="7ad05-127">Add the control (in this case, a list box) that lets users provide the information you’ve described in your label text.</span></span> <span data-ttu-id="7ad05-128">Nincsenek alkalmazhat szövegmezőkben; mellett sok más vezérlők További vezérlők, lásd: [System.Windows.Forms Namespace](http://msdn.microsoft.com/library/k50ex0x9(v=vs.110).aspx) az MSDN Webhelyén.</span><span class="sxs-lookup"><span data-stu-id="7ad05-128">There are many other controls you can apply besides text boxes; for more controls, see [System.Windows.Forms Namespace](http://msdn.microsoft.com/library/k50ex0x9(v=vs.110).aspx) on MSDN.</span></span>

```powershell
$listBox = New-Object System.Windows.Forms.Listbox
$listBox.Location = New-Object System.Drawing.Point(10,40)
$listBox.Size = New-Object System.Drawing.Size(260,20)
```

<span data-ttu-id="7ad05-129">Itt látható, hogyan adhatja meg, hogy szeretné-e a felhasználók megadhatják több értéket a listából.</span><span class="sxs-lookup"><span data-stu-id="7ad05-129">Here’s how you specify that you want to allow users to select multiple values from the list.</span></span>

```powershell
$listBox.SelectionMode = 'MultiExtended'
```

<span data-ttu-id="7ad05-130">A következő szakaszban adja meg a felhasználók számára megjelenítendő a lista kívánt értékeket.</span><span class="sxs-lookup"><span data-stu-id="7ad05-130">In the next section, you specify the values you want the list box to display to users.</span></span>

```powershell
[void] $listBox.Items.Add('Item 1')
[void] $listBox.Items.Add('Item 2')
[void] $listBox.Items.Add('Item 3')
[void] $listBox.Items.Add('Item 4')
[void] $listBox.Items.Add('Item 5')
```

<span data-ttu-id="7ad05-131">Adja meg a lista vezérlőelem maximális magasságát.</span><span class="sxs-lookup"><span data-stu-id="7ad05-131">Specify the maximum height of the list box control.</span></span>

```powershell
$listBox.Height = 70
```

<span data-ttu-id="7ad05-132">A lista vezérlőelem vegye fel az űrlap, és kérje meg a Windows a képernyő elveire más windows és a párbeszédpanel megnyitásához, ha meg van nyitva.</span><span class="sxs-lookup"><span data-stu-id="7ad05-132">Add the list box control to your form, and instruct Windows to open the form atop other windows and dialog boxes when it’s opened.</span></span>

```powershell
$form.Controls.Add($listBox)
$form.Topmost = $true
```

<span data-ttu-id="7ad05-133">Adja hozzá a következő kódsort a képernyőn megjelenő Windows.</span><span class="sxs-lookup"><span data-stu-id="7ad05-133">Add the following line of code to display the form in Windows.</span></span>

```powershell
$result = $form.ShowDialog()
```

<span data-ttu-id="7ad05-134">Végezetül, a kódot a **Ha** blokk utasítja Windows Mi a teendő az űrlapot, miután a felhasználók egy vagy több lehetőséget válassza a legördülő listából, és kattintson a **OK** gombra vagy nyomja meg a **Enter**  kulcs.</span><span class="sxs-lookup"><span data-stu-id="7ad05-134">Finally, the code inside the **If** block instructs Windows what to do with the form after users select one or more options from the list box, and then click the **OK** button or press the **Enter** key.</span></span>

```powershell
if ($result -eq [System.Windows.Forms.DialogResult]::OK)
{
    $x = $listBox.SelectedItems
    $x
}
```

## <a name="see-also"></a><span data-ttu-id="7ad05-135">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="7ad05-135">See Also</span></span>

- [<span data-ttu-id="7ad05-136">Hey Scripting Guy: Miért nem PowerShell grafikus felhasználói Felülettel példákban használhatók?</span><span class="sxs-lookup"><span data-stu-id="7ad05-136">Hey Scripting Guy:  Why don’t these PowerShell GUI examples work?</span></span>](http://go.microsoft.com/fwlink/?LinkId=506644)
- [<span data-ttu-id="7ad05-137">GitHub: Dave Wyatt WinFormsExampleUpdates</span><span class="sxs-lookup"><span data-stu-id="7ad05-137">GitHub: Dave Wyatt's WinFormsExampleUpdates</span></span>](https://github.com/dlwyatt/WinFormsExampleUpdates)
- [<span data-ttu-id="7ad05-138">A hét Windows PowerShell tipp: Jelölje ki a listában be - és egyéb!</span><span class="sxs-lookup"><span data-stu-id="7ad05-138">Windows PowerShell Tip of the Week:  Multi-Select List Boxes - And More!</span></span>](http://technet.microsoft.com/library/ff730950.aspx)