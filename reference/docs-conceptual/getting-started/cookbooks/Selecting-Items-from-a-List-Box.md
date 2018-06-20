---
ms.date: 06/05/2017
keywords: PowerShell parancsmag
title: Elemek kiválasztása egy listából
ms.assetid: 327c7cc5-21d0-4ace-b151-aa1491d1d3c2
ms.openlocfilehash: 6ff6bff8f6ce4e9236d7877c4cca24a10932cbe0
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
ms.locfileid: "30951681"
---
# <a name="selecting-items-from-a-list-box"></a><span data-ttu-id="ce840-103">Elemek kiválasztása egy listából</span><span class="sxs-lookup"><span data-stu-id="ce840-103">Selecting Items from a List Box</span></span>

<span data-ttu-id="ce840-104">Egy párbeszédpanelt, amely lehetővé teszi, hogy a rendszergazdák kiválaszthatják az elemeket a lista vezérlőelemet létrehozásához használja a Windows PowerShell 3.0-s és újabb verziókban.</span><span class="sxs-lookup"><span data-stu-id="ce840-104">Use Windows PowerShell 3.0 and later releases to create a dialog box that lets users select items from a list box control.</span></span>

## <a name="create-a-list-box-control-and-select-items-from-it"></a><span data-ttu-id="ce840-105">Hozzon létre egy lista vezérlőelem, és válassza ki az elemeket</span><span class="sxs-lookup"><span data-stu-id="ce840-105">Create a list box control, and select items from it</span></span>

<span data-ttu-id="ce840-106">Másolja és illessze be a következő Windows PowerShell ISE-be, és mentse egy Windows PowerShell-parancsfájlt (.ps1).</span><span class="sxs-lookup"><span data-stu-id="ce840-106">Copy and then paste the following into Windows PowerShell ISE, and then save it as a Windows PowerShell script (.ps1).</span></span>

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

<span data-ttu-id="ce840-107">A parancsfájl első lépése két .NET-keretrendszer osztály betöltése: **System.Drawing** és **System.Windows.Forms**.</span><span class="sxs-lookup"><span data-stu-id="ce840-107">The script begins by loading two .NET Framework classes: **System.Drawing** and **System.Windows.Forms**.</span></span> <span data-ttu-id="ce840-108">Majd indítsa el a .NET-keretrendszer osztály új példánya **: System.Windows.Forms.Form**; biztosítja az üres űrlapból, vagy ablak, amelyhez elkezdhet szabályozza.</span><span class="sxs-lookup"><span data-stu-id="ce840-108">You then start a new instance of the .NET Framework class **System.Windows.Forms.Form**; that provides a blank form or window to which you can start adding controls.</span></span>

```powershell
Add-Type -AssemblyName System.Windows.Forms
Add-Type -AssemblyName System.Drawing
```

<span data-ttu-id="ce840-109">Az űrlap osztály példányának létrehozása után értéket hozzárendelni az osztály három tulajdonságot.</span><span class="sxs-lookup"><span data-stu-id="ce840-109">After you create an instance of the Form class, assign values to three properties of this class.</span></span>

- <span data-ttu-id="ce840-110">**Text.**</span><span class="sxs-lookup"><span data-stu-id="ce840-110">**Text.**</span></span> <span data-ttu-id="ce840-111">Ez lesz az ablak címe.</span><span class="sxs-lookup"><span data-stu-id="ce840-111">This becomes the title of the window.</span></span>

- <span data-ttu-id="ce840-112">**Size.**</span><span class="sxs-lookup"><span data-stu-id="ce840-112">**Size.**</span></span> <span data-ttu-id="ce840-113">Ez az az űrlap képpontban méretét.</span><span class="sxs-lookup"><span data-stu-id="ce840-113">This is the size of the form, in pixels.</span></span> <span data-ttu-id="ce840-114">A fenti parancsfájl űrlapot hoz létre, amely 300 x 200 magassága képpontban megadva.</span><span class="sxs-lookup"><span data-stu-id="ce840-114">The preceding script creates a form that’s 300 pixels wide by 200 pixels tall.</span></span>

- <span data-ttu-id="ce840-115">**StartingPosition.**</span><span class="sxs-lookup"><span data-stu-id="ce840-115">**StartingPosition.**</span></span> <span data-ttu-id="ce840-116">Ez nem kötelező tulajdonság értéke **CenterScreen** az előző parancsfájlban.</span><span class="sxs-lookup"><span data-stu-id="ce840-116">This optional property is set to **CenterScreen** in the preceding script.</span></span> <span data-ttu-id="ce840-117">Ez a tulajdonság nem ad hozzá, ha a Windows kiválaszt egy helyet, az űrlap megnyitásakor.</span><span class="sxs-lookup"><span data-stu-id="ce840-117">If you don’t add this property, Windows selects a location when the form is opened.</span></span> <span data-ttu-id="ce840-118">Úgy, hogy a **StartingPosition** való **CenterScreen**, akkor program automatikusan jeleníti meg az űrlap közepén a képernyő minden alkalommal, amikor betölti a.</span><span class="sxs-lookup"><span data-stu-id="ce840-118">By setting the **StartingPosition** to **CenterScreen**, you’re automatically displaying the form in the middle of the screen each time it loads.</span></span>

```powershell
$form.Text = 'Select a Computer'
$form.Size = New-Object System.Drawing.Size(300,200)
$form.StartPosition = 'CenterScreen'
```

<span data-ttu-id="ce840-119">Ezután hozzon létre egy **OK** gombra az űrlap.</span><span class="sxs-lookup"><span data-stu-id="ce840-119">Next, create an **OK** button for your form.</span></span> <span data-ttu-id="ce840-120">Adja meg a méretét és viselkedését a **OK** gombra.</span><span class="sxs-lookup"><span data-stu-id="ce840-120">Specify the size and behavior of the **OK** button.</span></span> <span data-ttu-id="ce840-121">Ebben a példában a gomb pozíciója a képernyő felső szélétől 120 képpont, de 75 képpont bal szélétől.</span><span class="sxs-lookup"><span data-stu-id="ce840-121">In this example, the button position is 120 pixels from the form’s top edge, and 75 pixels from the left edge.</span></span> <span data-ttu-id="ce840-122">A gomb magassága 23 képpont, amíg a gomb hossza 75 képpontban megadva.</span><span class="sxs-lookup"><span data-stu-id="ce840-122">The button height is 23 pixels, while the button length is 75 pixels.</span></span> <span data-ttu-id="ce840-123">A parancsfájl előre meghatározott Windows Forms-típusok gombra viselkedésmódját meghatározására használja.</span><span class="sxs-lookup"><span data-stu-id="ce840-123">The script uses predefined Windows Forms types to determine the button behaviors.</span></span>

```powershell
$OKButton = New-Object System.Windows.Forms.Button
$OKButton.Location = New-Object System.Drawing.Point(75,120)
$OKButton.Size = New-Object System.Drawing.Size(75,23)
$OKButton.Text = 'OK'
$OKButton.DialogResult = [System.Windows.Forms.DialogResult]::OK
$form.AcceptButton = $OKButton
$form.Controls.Add($OKButton)
```

<span data-ttu-id="ce840-124">Hasonlóképpen, létrehozhat egy **Mégse** gombra.</span><span class="sxs-lookup"><span data-stu-id="ce840-124">Similarly, you create a **Cancel** button.</span></span> <span data-ttu-id="ce840-125">A **Mégse** gomb, a lista elejéről 120 képpont, de az ablak bal szélétől 150 képpont.</span><span class="sxs-lookup"><span data-stu-id="ce840-125">The **Cancel** button is 120 pixels from the top, but 150 pixels from the left edge of the window.</span></span>

```powershell
$CancelButton = New-Object System.Windows.Forms.Button
$CancelButton.Location = New-Object System.Drawing.Point(150,120)
$CancelButton.Size = New-Object System.Drawing.Size(75,23)
$CancelButton.Text = 'Cancel'
$CancelButton.DialogResult = [System.Windows.Forms.DialogResult]::Cancel
$form.CancelButton = $CancelButton
$form.Controls.Add($CancelButton)
```

<span data-ttu-id="ce840-126">A következő adja meg a címke szövegét, a ablakban adja meg a felhasználók a információkat.</span><span class="sxs-lookup"><span data-stu-id="ce840-126">Next, provide label text on your window that describes the information you want users to provide.</span></span> <span data-ttu-id="ce840-127">Ebben az esetben érdemes a felhasználóknak, hogy a számítógép.</span><span class="sxs-lookup"><span data-stu-id="ce840-127">In this case, you want users to select a computer.</span></span>

```powershell
$label = New-Object System.Windows.Forms.Label
$label.Location = New-Object System.Drawing.Point(10,20)
$label.Size = New-Object System.Drawing.Size(280,20)
$label.Text = 'Please select a computer:'
$form.Controls.Add($label)
```

<span data-ttu-id="ce840-128">Adja hozzá a vezérlő (ebben az esetben egy lista), amely lehetővé teszi a felhasználóknak adja meg az adatokat, akkor már ismertetett a címke szövegét.</span><span class="sxs-lookup"><span data-stu-id="ce840-128">Add the control (in this case, a list box) that lets users provide the information you’ve described in your label text.</span></span> <span data-ttu-id="ce840-129">Nincsenek alkalmazhat listák; mellett sok más vezérlők További vezérlők, lásd: [System.Windows.Forms Namespace](http://msdn.microsoft.com/library/k50ex0x9(v=vs.110).aspx) az MSDN Webhelyén.</span><span class="sxs-lookup"><span data-stu-id="ce840-129">There are many other controls you can apply besides list boxes; for more controls, see [System.Windows.Forms Namespace](http://msdn.microsoft.com/library/k50ex0x9(v=vs.110).aspx) on MSDN.</span></span>

```powershell
$listBox = New-Object System.Windows.Forms.ListBox
$listBox.Location = New-Object System.Drawing.Point(10,40)
$listBox.Size = New-Object System.Drawing.Size(260,20)
$listBox.Height = 80
```

<span data-ttu-id="ce840-130">A következő szakaszban adja meg a felhasználók számára megjelenítendő a lista kívánt értékeket.</span><span class="sxs-lookup"><span data-stu-id="ce840-130">In the next section, you specify the values you want the list box to display to users.</span></span>

> [!NOTE]
> <span data-ttu-id="ce840-131">A lista hozta létre a parancsfájl a csak egy kiválasztását teszi lehetővé.</span><span class="sxs-lookup"><span data-stu-id="ce840-131">The list box created by this script allows only one selection.</span></span> <span data-ttu-id="ce840-132">Egy lista vezérlőelem, amely lehetővé teszi több kijelölés létrehozásához adjon meg értéket a **SelectionMode** tulajdonságot, hasonlóan a következő: `$listBox.SelectionMode = 'MultiExtended'`.</span><span class="sxs-lookup"><span data-stu-id="ce840-132">To create a list box control that allows multiple selections, specify a value for the **SelectionMode** property, similarly to the following:  `$listBox.SelectionMode = 'MultiExtended'`.</span></span> <span data-ttu-id="ce840-133">További információkért lásd: [többszörös kijelölés listák](Multiple-selection-List-Boxes.md).</span><span class="sxs-lookup"><span data-stu-id="ce840-133">For more information, see [Multiple-selection List Boxes](Multiple-selection-List-Boxes.md).</span></span>

```powershell
[void] $listBox.Items.Add('atl-dc-001')
[void] $listBox.Items.Add('atl-dc-002')
[void] $listBox.Items.Add('atl-dc-003')
[void] $listBox.Items.Add('atl-dc-004')
[void] $listBox.Items.Add('atl-dc-005')
[void] $listBox.Items.Add('atl-dc-006')
[void] $listBox.Items.Add('atl-dc-007')
```

<span data-ttu-id="ce840-134">A lista vezérlőelem vegye fel az űrlap, és kérje meg a Windows a képernyő elveire más windows és a párbeszédpanel megnyitásához, ha meg van nyitva.</span><span class="sxs-lookup"><span data-stu-id="ce840-134">Add the list box control to your form, and instruct Windows to open the form atop other windows and dialog boxes when it’s opened.</span></span>

```powershell
$form.Controls.Add($listBox)
$form.Topmost = $true
```

<span data-ttu-id="ce840-135">Adja hozzá a következő kódsort a képernyőn megjelenő Windows.</span><span class="sxs-lookup"><span data-stu-id="ce840-135">Add the following line of code to display the form in Windows.</span></span>

```powershell
$result = $form.ShowDialog()
```

<span data-ttu-id="ce840-136">Végezetül, a kódot a **Ha** blokk utasítja Windows Mi a teendő az űrlapot, miután a felhasználók jelöljön ki egy lehetőséget a legördülő listából, és kattintson a **OK** gombra vagy nyomja le az **Enter**kulcs.</span><span class="sxs-lookup"><span data-stu-id="ce840-136">Finally, the code inside the **If** block instructs Windows what to do with the form after users select an option from the list box, and then click the **OK** button or press the **Enter** key.</span></span>

```powershell
if ($result -eq [System.Windows.Forms.DialogResult]::OK)
{
    $x = $listBox.SelectedItem
    $x
}
```

## <a name="see-also"></a><span data-ttu-id="ce840-137">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="ce840-137">See Also</span></span>

- [<span data-ttu-id="ce840-138">Hey Scripting Guy: Miért nem PowerShell grafikus felhasználói Felülettel példákban használhatók?</span><span class="sxs-lookup"><span data-stu-id="ce840-138">Hey Scripting Guy:  Why don’t these PowerShell GUI examples work?</span></span>](http://go.microsoft.com/fwlink/?LinkId=506644)
- [<span data-ttu-id="ce840-139">GitHub: Dave Wyatt WinFormsExampleUpdates</span><span class="sxs-lookup"><span data-stu-id="ce840-139">GitHub: Dave Wyatt's WinFormsExampleUpdates</span></span>](https://github.com/dlwyatt/WinFormsExampleUpdates)
- [<span data-ttu-id="ce840-140">A hét Windows PowerShell tipp: lista elemek kijelölése</span><span class="sxs-lookup"><span data-stu-id="ce840-140">Windows PowerShell Tip of the Week:  Selecting Items from a List Box</span></span>](http://technet.microsoft.com/library/ff730949.aspx)