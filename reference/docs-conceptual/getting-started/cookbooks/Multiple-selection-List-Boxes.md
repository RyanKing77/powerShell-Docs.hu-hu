---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: Többszörös kijelölésű listák
ms.assetid: f74cd5d9-da57-4802-b614-0b194a7bc8f8
ms.openlocfilehash: a762145dc197ec7e1424b2fbdcef5e7380d13803
ms.sourcegitcommit: 221b7daab7f597f8b2e4864cf9b5d9dda9b9879b
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 11/27/2018
ms.locfileid: "52320975"
---
# <a name="multiple-selection-list-boxes"></a><span data-ttu-id="2f4cc-103">Többszörös kijelölési lista</span><span class="sxs-lookup"><span data-stu-id="2f4cc-103">Multiple-selection List Boxes</span></span>

<span data-ttu-id="2f4cc-104">Windows PowerShell 3.0-s és újabb kiadásaiban segítségével egy többszörös kijelölési lista vezérlőelem hozzon létre egy egyéni Windows-űrlapon.</span><span class="sxs-lookup"><span data-stu-id="2f4cc-104">Use Windows PowerShell 3.0 and later releases to create a multiple-selection list box control in a custom Windows Form.</span></span>

## <a name="create-list-box-controls-that-allow-multiple-selections"></a><span data-ttu-id="2f4cc-105">Lista létrehozása, amely több elem is választható vezérlők</span><span class="sxs-lookup"><span data-stu-id="2f4cc-105">Create list box controls that allow multiple selections</span></span>

<span data-ttu-id="2f4cc-106">Másolja, és ezután illessze be a következő Windows PowerShell ISE-ben, és mentse egy Windows PowerShell-parancsprogram (.ps1).</span><span class="sxs-lookup"><span data-stu-id="2f4cc-106">Copy and then paste the following into Windows PowerShell ISE, and then save it as a Windows PowerShell script (.ps1).</span></span>

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

<span data-ttu-id="2f4cc-107">A szkript első lépése két .NET-keretrendszer osztály betöltésekor: **System.Drawing** és **System.Windows.Forms**.</span><span class="sxs-lookup"><span data-stu-id="2f4cc-107">The script begins by loading two .NET Framework classes: **System.Drawing** and **System.Windows.Forms**.</span></span> <span data-ttu-id="2f4cc-108">Indítsa el a .NET-keretrendszer osztály egy új példányát **System.Windows.Forms.Form**; amely biztosítja, hogy egy üres űrlapot vagy ablakban, amelyhez elkezdhet szabályozza.</span><span class="sxs-lookup"><span data-stu-id="2f4cc-108">You then start a new instance of the .NET Framework class **System.Windows.Forms.Form**; that provides a blank form or window to which you can start adding controls.</span></span>

```powershell
$form = New-Object System.Windows.Forms.Form
```

<span data-ttu-id="2f4cc-109">Miután létrehozta az űrlap osztály egy példányát, értéket rendelni az osztály három tulajdonságot.</span><span class="sxs-lookup"><span data-stu-id="2f4cc-109">After you create an instance of the Form class, assign values to three properties of this class.</span></span>

- <span data-ttu-id="2f4cc-110">**Szöveg.**</span><span class="sxs-lookup"><span data-stu-id="2f4cc-110">**Text.**</span></span> <span data-ttu-id="2f4cc-111">Ez lesz az ablak címe.</span><span class="sxs-lookup"><span data-stu-id="2f4cc-111">This becomes the title of the window.</span></span>

- <span data-ttu-id="2f4cc-112">**Velikost.**</span><span class="sxs-lookup"><span data-stu-id="2f4cc-112">**Size.**</span></span> <span data-ttu-id="2f4cc-113">Ez a méretét az űrlap (képpontban).</span><span class="sxs-lookup"><span data-stu-id="2f4cc-113">This is the size of the form, in pixels.</span></span> <span data-ttu-id="2f4cc-114">A fenti szkript létrehoz egy képernyő, amely 300 képpont széles és 200 képpont magas.</span><span class="sxs-lookup"><span data-stu-id="2f4cc-114">The preceding script creates a form that’s 300 pixels wide by 200 pixels tall.</span></span>

- <span data-ttu-id="2f4cc-115">**Kezdőpozíció.**</span><span class="sxs-lookup"><span data-stu-id="2f4cc-115">**StartingPosition.**</span></span> <span data-ttu-id="2f4cc-116">Ez nem kötelező tulajdonsága **CenterScreen** az előző szkriptben.</span><span class="sxs-lookup"><span data-stu-id="2f4cc-116">This optional property is set to **CenterScreen** in the preceding script.</span></span> <span data-ttu-id="2f4cc-117">Ha nem ezt a tulajdonságot, a Windows kiválaszt egy helyet, az űrlap megnyitásakor.</span><span class="sxs-lookup"><span data-stu-id="2f4cc-117">If you don’t add this property, Windows selects a location when the form is opened.</span></span> <span data-ttu-id="2f4cc-118">Beállításával a **kezdőpozíció** való **CenterScreen**, akkor már automatikusan megjelenítése az űrlap a képernyő közepén minden alkalommal, amikor betölti.</span><span class="sxs-lookup"><span data-stu-id="2f4cc-118">By setting the **StartingPosition** to **CenterScreen**, you’re automatically displaying the form in the middle of the screen each time it loads.</span></span>

```powershell
$form.Text = 'Data Entry Form'
$form.Size = New-Object System.Drawing.Size(300,200)
$form.StartPosition = 'CenterScreen'
```

<span data-ttu-id="2f4cc-119">Ezután hozzon létre egy **OK** gombot az űrlapon.</span><span class="sxs-lookup"><span data-stu-id="2f4cc-119">Next, create an **OK** button for your form.</span></span> <span data-ttu-id="2f4cc-120">Adja meg a méretét és viselkedését a **OK** gombra.</span><span class="sxs-lookup"><span data-stu-id="2f4cc-120">Specify the size and behavior of the **OK** button.</span></span> <span data-ttu-id="2f4cc-121">Ebben a példában a gomb elhelyezése, a képernyő felső széle 120 képpont 75 képpont bal szélétől.</span><span class="sxs-lookup"><span data-stu-id="2f4cc-121">In this example, the button position is 120 pixels from the form’s top edge, and 75 pixels from the left edge.</span></span> <span data-ttu-id="2f4cc-122">A gomb magassága 23 képpont, amíg a gomb hossza 75 képpont.</span><span class="sxs-lookup"><span data-stu-id="2f4cc-122">The button height is 23 pixels, while the button length is 75 pixels.</span></span> <span data-ttu-id="2f4cc-123">A szkript előre meghatározott Windows Forms-típusok a gomb viselkedés határozza meg.</span><span class="sxs-lookup"><span data-stu-id="2f4cc-123">The script uses predefined Windows Forms types to determine the button behaviors.</span></span>

```powershell
$OKButton = New-Object System.Windows.Forms.Button
$OKButton.Location = New-Object System.Drawing.Size(75,120)
$OKButton.Size = New-Object System.Drawing.Size(75,23)
$OKButton.Text = 'OK'
$OKButton.DialogResult = [System.Windows.Forms.DialogResult]::OK
$form.AcceptButton = $OKButton
$form.Controls.Add($OKButton)
```

<span data-ttu-id="2f4cc-124">Hasonlóképpen, létrehozhat egy **Mégse** gombra.</span><span class="sxs-lookup"><span data-stu-id="2f4cc-124">Similarly, you create a **Cancel** button.</span></span> <span data-ttu-id="2f4cc-125">A **Mégse** gombot a felső 120 képpont, de az ablak bal szélétől 150 pixeles.</span><span class="sxs-lookup"><span data-stu-id="2f4cc-125">The **Cancel** button is 120 pixels from the top, but 150 pixels from the left edge of the window.</span></span>

```powershell
$CancelButton = New-Object System.Windows.Forms.Button
$CancelButton.Location = New-Object System.Drawing.Point(150,120)
$CancelButton.Size = New-Object System.Drawing.Size(75,23)
$CancelButton.Text = 'Cancel'
$CancelButton.DialogResult = [System.Windows.Forms.DialogResult]::Cancel
$form.CancelButton = $CancelButton
$form.Controls.Add($CancelButton)
```

<span data-ttu-id="2f4cc-126">Következő lépésként adja meg az ablak, amely leírja az adatokat, adja meg a felhasználók a felirat szövege.</span><span class="sxs-lookup"><span data-stu-id="2f4cc-126">Next, provide label text on your window that describes the information you want users to provide.</span></span>

```powershell
$label = New-Object System.Windows.Forms.Label
$label.Location = New-Object System.Drawing.Point(10,20)
$label.Size = New-Object System.Drawing.Size(280,20)
$label.Text = 'Please make a selection from the list below:'
$form.Controls.Add($label)
```

<span data-ttu-id="2f4cc-127">Adja hozzá a vezérlő (ebben az esetben egy lista), amely lehetővé teszi a felhasználóknak adja meg az adatokat, akkor már ismertetett a felirat szövege.</span><span class="sxs-lookup"><span data-stu-id="2f4cc-127">Add the control (in this case, a list box) that lets users provide the information you’ve described in your label text.</span></span> <span data-ttu-id="2f4cc-128">Nincsenek alkalmazhat szövegmezők; mellett számos más vezérlők További vezérlők, lásd: [System.Windows.Forms Namespace](https://msdn.microsoft.com/library/k50ex0x9(v=vs.110).aspx) az MSDN Webhelyén.</span><span class="sxs-lookup"><span data-stu-id="2f4cc-128">There are many other controls you can apply besides text boxes; for more controls, see [System.Windows.Forms Namespace](https://msdn.microsoft.com/library/k50ex0x9(v=vs.110).aspx) on MSDN.</span></span>

```powershell
$listBox = New-Object System.Windows.Forms.Listbox
$listBox.Location = New-Object System.Drawing.Point(10,40)
$listBox.Size = New-Object System.Drawing.Size(260,20)
```

<span data-ttu-id="2f4cc-129">Itt adhatja meg, hogy szeretné-e engedélyezése a felhasználók számára kijelölhet a listában több érték van.</span><span class="sxs-lookup"><span data-stu-id="2f4cc-129">Here’s how you specify that you want to allow users to select multiple values from the list.</span></span>

```powershell
$listBox.SelectionMode = 'MultiExtended'
```

<span data-ttu-id="2f4cc-130">A következő szakaszban adja meg a kívánt értékeket, a felhasználók számára megjelenítendő legördülő listából.</span><span class="sxs-lookup"><span data-stu-id="2f4cc-130">In the next section, you specify the values you want the list box to display to users.</span></span>

```powershell
[void] $listBox.Items.Add('Item 1')
[void] $listBox.Items.Add('Item 2')
[void] $listBox.Items.Add('Item 3')
[void] $listBox.Items.Add('Item 4')
[void] $listBox.Items.Add('Item 5')
```

<span data-ttu-id="2f4cc-131">Adja meg a lista vezérlőelem maximális magasságát.</span><span class="sxs-lookup"><span data-stu-id="2f4cc-131">Specify the maximum height of the list box control.</span></span>

```powershell
$listBox.Height = 70
```

<span data-ttu-id="2f4cc-132">A lista vezérlőelem felvétele az űrlapot, és kérje meg a Windows más windows és a párbeszédpanelek interaktív irányítópultunkat képernyő megnyitásához, ha meg van nyitva.</span><span class="sxs-lookup"><span data-stu-id="2f4cc-132">Add the list box control to your form, and instruct Windows to open the form atop other windows and dialog boxes when it’s opened.</span></span>

```powershell
$form.Controls.Add($listBox)
$form.Topmost = $true
```

<span data-ttu-id="2f4cc-133">Adja hozzá az alábbi kódsort az űrlap megjelenítésére a Windows.</span><span class="sxs-lookup"><span data-stu-id="2f4cc-133">Add the following line of code to display the form in Windows.</span></span>

```powershell
$result = $form.ShowDialog()
```

<span data-ttu-id="2f4cc-134">Végül a kód belül a **Ha** blokk arra utasítja a Windows Mi a teendő az űrlapot, miután a felhasználók egy vagy több lehetőség kiválasztása a listából, és kattintson a **OK** gombra vagy nyomja le a **Enter**  kulcsot.</span><span class="sxs-lookup"><span data-stu-id="2f4cc-134">Finally, the code inside the **If** block instructs Windows what to do with the form after users select one or more options from the list box, and then click the **OK** button or press the **Enter** key.</span></span>

```powershell
if ($result -eq [System.Windows.Forms.DialogResult]::OK)
{
    $x = $listBox.SelectedItems
    $x
}
```

## <a name="see-also"></a><span data-ttu-id="2f4cc-135">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="2f4cc-135">See Also</span></span>

- [<span data-ttu-id="2f4cc-136">Hey Scripting Guy: Miért nem a grafikus PowerShell-példákat működnek?</span><span class="sxs-lookup"><span data-stu-id="2f4cc-136">Hey Scripting Guy:  Why don’t these PowerShell GUI examples work?</span></span>](https://go.microsoft.com/fwlink/?LinkId=506644)
- [<span data-ttu-id="2f4cc-137">GitHub: Dave Wyatt WinFormsExampleUpdates</span><span class="sxs-lookup"><span data-stu-id="2f4cc-137">GitHub: Dave Wyatt's WinFormsExampleUpdates</span></span>](https://github.com/dlwyatt/WinFormsExampleUpdates)
- [<span data-ttu-id="2f4cc-138">Windows PowerShell Tip of the Week: többszörös kijelöléssel sorolja be - és egyéb!</span><span class="sxs-lookup"><span data-stu-id="2f4cc-138">Windows PowerShell Tip of the Week:  Multi-Select List Boxes - And More!</span></span>](https://technet.microsoft.com/library/ff730950.aspx)