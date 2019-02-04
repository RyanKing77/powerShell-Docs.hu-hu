---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: Elemek kiválasztása egy listából
ms.assetid: 327c7cc5-21d0-4ace-b151-aa1491d1d3c2
ms.openlocfilehash: e3d52839409a2fd58fbdc924a2b92d96fbecee53
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55688496"
---
# <a name="selecting-items-from-a-list-box"></a><span data-ttu-id="c32ff-103">Elemek kiválasztása egy listából</span><span class="sxs-lookup"><span data-stu-id="c32ff-103">Selecting Items from a List Box</span></span>

<span data-ttu-id="c32ff-104">Egy párbeszédpanel, amely lehetővé teszi az elemek kiválasztása egy lista vezérlőelem a felhasználók létrehozásához használja a Windows PowerShell 3.0-s és újabb verziókban.</span><span class="sxs-lookup"><span data-stu-id="c32ff-104">Use Windows PowerShell 3.0 and later releases to create a dialog box that lets users select items from a list box control.</span></span>

## <a name="create-a-list-box-control-and-select-items-from-it"></a><span data-ttu-id="c32ff-105">Hozzon létre egy lista vezérlőelem és elemeket választhat</span><span class="sxs-lookup"><span data-stu-id="c32ff-105">Create a list box control, and select items from it</span></span>

<span data-ttu-id="c32ff-106">Másolja, és ezután illessze be a következő Windows PowerShell ISE-ben, és mentse egy Windows PowerShell-parancsprogram (.ps1).</span><span class="sxs-lookup"><span data-stu-id="c32ff-106">Copy and then paste the following into Windows PowerShell ISE, and then save it as a Windows PowerShell script (.ps1).</span></span>

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

<span data-ttu-id="c32ff-107">A szkript első lépése betöltése két .NET-osztályok: **System.Drawing** és **System.Windows.Forms**.</span><span class="sxs-lookup"><span data-stu-id="c32ff-107">The script begins by loading two .NET Framework classes: **System.Drawing** and **System.Windows.Forms**.</span></span> <span data-ttu-id="c32ff-108">Indítsa el a .NET-keretrendszer osztály egy új példányát **System.Windows.Forms.Form**; amely biztosítja, hogy egy üres űrlapot vagy ablakban, amelyhez elkezdhet szabályozza.</span><span class="sxs-lookup"><span data-stu-id="c32ff-108">You then start a new instance of the .NET Framework class **System.Windows.Forms.Form**; that provides a blank form or window to which you can start adding controls.</span></span>

```powershell
Add-Type -AssemblyName System.Windows.Forms
Add-Type -AssemblyName System.Drawing
```

<span data-ttu-id="c32ff-109">Miután létrehozta az űrlap osztály egy példányát, értéket rendelni az osztály három tulajdonságot.</span><span class="sxs-lookup"><span data-stu-id="c32ff-109">After you create an instance of the Form class, assign values to three properties of this class.</span></span>

- <span data-ttu-id="c32ff-110">**Szöveg.**</span><span class="sxs-lookup"><span data-stu-id="c32ff-110">**Text.**</span></span> <span data-ttu-id="c32ff-111">Ez lesz az ablak címe.</span><span class="sxs-lookup"><span data-stu-id="c32ff-111">This becomes the title of the window.</span></span>

- <span data-ttu-id="c32ff-112">**Velikost.**</span><span class="sxs-lookup"><span data-stu-id="c32ff-112">**Size.**</span></span> <span data-ttu-id="c32ff-113">Ez a méretét az űrlap (képpontban).</span><span class="sxs-lookup"><span data-stu-id="c32ff-113">This is the size of the form, in pixels.</span></span> <span data-ttu-id="c32ff-114">A fenti szkript létrehoz egy képernyő, amely 300 képpont széles és 200 képpont magas.</span><span class="sxs-lookup"><span data-stu-id="c32ff-114">The preceding script creates a form that’s 300 pixels wide by 200 pixels tall.</span></span>

- <span data-ttu-id="c32ff-115">**Kezdőpozíció.**</span><span class="sxs-lookup"><span data-stu-id="c32ff-115">**StartingPosition.**</span></span> <span data-ttu-id="c32ff-116">Ez nem kötelező tulajdonsága **CenterScreen** az előző szkriptben.</span><span class="sxs-lookup"><span data-stu-id="c32ff-116">This optional property is set to **CenterScreen** in the preceding script.</span></span> <span data-ttu-id="c32ff-117">Ha nem ezt a tulajdonságot, a Windows kiválaszt egy helyet, az űrlap megnyitásakor.</span><span class="sxs-lookup"><span data-stu-id="c32ff-117">If you don’t add this property, Windows selects a location when the form is opened.</span></span> <span data-ttu-id="c32ff-118">Beállításával a **kezdőpozíció** való **CenterScreen**, akkor már automatikusan megjelenítése az űrlap a képernyő közepén minden alkalommal, amikor betölti.</span><span class="sxs-lookup"><span data-stu-id="c32ff-118">By setting the **StartingPosition** to **CenterScreen**, you’re automatically displaying the form in the middle of the screen each time it loads.</span></span>

```powershell
$form.Text = 'Select a Computer'
$form.Size = New-Object System.Drawing.Size(300,200)
$form.StartPosition = 'CenterScreen'
```

<span data-ttu-id="c32ff-119">Ezután hozzon létre egy **OK** gombot az űrlapon.</span><span class="sxs-lookup"><span data-stu-id="c32ff-119">Next, create an **OK** button for your form.</span></span> <span data-ttu-id="c32ff-120">Adja meg a méretét és viselkedését a **OK** gombra.</span><span class="sxs-lookup"><span data-stu-id="c32ff-120">Specify the size and behavior of the **OK** button.</span></span> <span data-ttu-id="c32ff-121">Ebben a példában a gomb elhelyezése, a képernyő felső széle 120 képpont 75 képpont bal szélétől.</span><span class="sxs-lookup"><span data-stu-id="c32ff-121">In this example, the button position is 120 pixels from the form’s top edge, and 75 pixels from the left edge.</span></span> <span data-ttu-id="c32ff-122">A gomb magassága 23 képpont, amíg a gomb hossza 75 képpont.</span><span class="sxs-lookup"><span data-stu-id="c32ff-122">The button height is 23 pixels, while the button length is 75 pixels.</span></span> <span data-ttu-id="c32ff-123">A szkript előre meghatározott Windows Forms-típusok a gomb viselkedés határozza meg.</span><span class="sxs-lookup"><span data-stu-id="c32ff-123">The script uses predefined Windows Forms types to determine the button behaviors.</span></span>

```powershell
$OKButton = New-Object System.Windows.Forms.Button
$OKButton.Location = New-Object System.Drawing.Point(75,120)
$OKButton.Size = New-Object System.Drawing.Size(75,23)
$OKButton.Text = 'OK'
$OKButton.DialogResult = [System.Windows.Forms.DialogResult]::OK
$form.AcceptButton = $OKButton
$form.Controls.Add($OKButton)
```

<span data-ttu-id="c32ff-124">Hasonlóképpen, létrehozhat egy **Mégse** gombra.</span><span class="sxs-lookup"><span data-stu-id="c32ff-124">Similarly, you create a **Cancel** button.</span></span> <span data-ttu-id="c32ff-125">A **Mégse** gombot a felső 120 képpont, de az ablak bal szélétől 150 pixeles.</span><span class="sxs-lookup"><span data-stu-id="c32ff-125">The **Cancel** button is 120 pixels from the top, but 150 pixels from the left edge of the window.</span></span>

```powershell
$CancelButton = New-Object System.Windows.Forms.Button
$CancelButton.Location = New-Object System.Drawing.Point(150,120)
$CancelButton.Size = New-Object System.Drawing.Size(75,23)
$CancelButton.Text = 'Cancel'
$CancelButton.DialogResult = [System.Windows.Forms.DialogResult]::Cancel
$form.CancelButton = $CancelButton
$form.Controls.Add($CancelButton)
```

<span data-ttu-id="c32ff-126">Következő lépésként adja meg az ablak, amely leírja az adatokat, adja meg a felhasználók a felirat szövege.</span><span class="sxs-lookup"><span data-stu-id="c32ff-126">Next, provide label text on your window that describes the information you want users to provide.</span></span> <span data-ttu-id="c32ff-127">Ebben az esetben érdemes a felhasználók számára, válasszon ki egy számítógépet.</span><span class="sxs-lookup"><span data-stu-id="c32ff-127">In this case, you want users to select a computer.</span></span>

```powershell
$label = New-Object System.Windows.Forms.Label
$label.Location = New-Object System.Drawing.Point(10,20)
$label.Size = New-Object System.Drawing.Size(280,20)
$label.Text = 'Please select a computer:'
$form.Controls.Add($label)
```

<span data-ttu-id="c32ff-128">Adja hozzá a vezérlő (ebben az esetben egy lista), amely lehetővé teszi a felhasználóknak adja meg az adatokat, akkor már ismertetett a felirat szövege.</span><span class="sxs-lookup"><span data-stu-id="c32ff-128">Add the control (in this case, a list box) that lets users provide the information you’ve described in your label text.</span></span> <span data-ttu-id="c32ff-129">Nincsenek alkalmazhat listák; mellett számos más vezérlők További vezérlők, lásd: [System.Windows.Forms Namespace](https://msdn.microsoft.com/library/k50ex0x9(v=vs.110).aspx) az MSDN Webhelyén.</span><span class="sxs-lookup"><span data-stu-id="c32ff-129">There are many other controls you can apply besides list boxes; for more controls, see [System.Windows.Forms Namespace](https://msdn.microsoft.com/library/k50ex0x9(v=vs.110).aspx) on MSDN.</span></span>

```powershell
$listBox = New-Object System.Windows.Forms.ListBox
$listBox.Location = New-Object System.Drawing.Point(10,40)
$listBox.Size = New-Object System.Drawing.Size(260,20)
$listBox.Height = 80
```

<span data-ttu-id="c32ff-130">A következő szakaszban adja meg a kívánt értékeket, a felhasználók számára megjelenítendő legördülő listából.</span><span class="sxs-lookup"><span data-stu-id="c32ff-130">In the next section, you specify the values you want the list box to display to users.</span></span>

> [!NOTE]
> <span data-ttu-id="c32ff-131">A legördülő listából a szkript által létrehozott csak egy kiválasztását teszi lehetővé.</span><span class="sxs-lookup"><span data-stu-id="c32ff-131">The list box created by this script allows only one selection.</span></span> <span data-ttu-id="c32ff-132">A lista vezérlőelem, amely lehetővé teszi, hogy több elem is választható létrehozásához adjon meg értéket a **SelectionMode** tulajdonságát, hasonlóan a következő: `$listBox.SelectionMode = 'MultiExtended'`.</span><span class="sxs-lookup"><span data-stu-id="c32ff-132">To create a list box control that allows multiple selections, specify a value for the **SelectionMode** property, similarly to the following:  `$listBox.SelectionMode = 'MultiExtended'`.</span></span> <span data-ttu-id="c32ff-133">További információkért lásd: [többszörös kijelölési lista](Multiple-selection-List-Boxes.md).</span><span class="sxs-lookup"><span data-stu-id="c32ff-133">For more information, see [Multiple-selection List Boxes](Multiple-selection-List-Boxes.md).</span></span>

```powershell
[void] $listBox.Items.Add('atl-dc-001')
[void] $listBox.Items.Add('atl-dc-002')
[void] $listBox.Items.Add('atl-dc-003')
[void] $listBox.Items.Add('atl-dc-004')
[void] $listBox.Items.Add('atl-dc-005')
[void] $listBox.Items.Add('atl-dc-006')
[void] $listBox.Items.Add('atl-dc-007')
```

<span data-ttu-id="c32ff-134">A lista vezérlőelem felvétele az űrlapot, és kérje meg a Windows más windows és a párbeszédpanelek interaktív irányítópultunkat képernyő megnyitásához, ha meg van nyitva.</span><span class="sxs-lookup"><span data-stu-id="c32ff-134">Add the list box control to your form, and instruct Windows to open the form atop other windows and dialog boxes when it’s opened.</span></span>

```powershell
$form.Controls.Add($listBox)
$form.Topmost = $true
```

<span data-ttu-id="c32ff-135">Adja hozzá az alábbi kódsort az űrlap megjelenítésére a Windows.</span><span class="sxs-lookup"><span data-stu-id="c32ff-135">Add the following line of code to display the form in Windows.</span></span>

```powershell
$result = $form.ShowDialog()
```

<span data-ttu-id="c32ff-136">Végül a kód belül a **Ha** blokk arra utasítja a Windows Mi a teendő az űrlapot, miután a felhasználók jelöljön ki egy lehetőséget a legördülő listából, és kattintson a **OK** gombra vagy nyomja le a **Enter**kulcsot.</span><span class="sxs-lookup"><span data-stu-id="c32ff-136">Finally, the code inside the **If** block instructs Windows what to do with the form after users select an option from the list box, and then click the **OK** button or press the **Enter** key.</span></span>

```powershell
if ($result -eq [System.Windows.Forms.DialogResult]::OK)
{
    $x = $listBox.SelectedItem
    $x
}
```

## <a name="see-also"></a><span data-ttu-id="c32ff-137">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="c32ff-137">See Also</span></span>

- [<span data-ttu-id="c32ff-138">Hey Scripting Guy:  Miért nem működnek a grafikus PowerShell-példákat?</span><span class="sxs-lookup"><span data-stu-id="c32ff-138">Hey Scripting Guy:  Why don’t these PowerShell GUI examples work?</span></span>](https://go.microsoft.com/fwlink/?LinkId=506644)
- [<span data-ttu-id="c32ff-139">GitHub: Dave Wyatt WinFormsExampleUpdates</span><span class="sxs-lookup"><span data-stu-id="c32ff-139">GitHub: Dave Wyatt's WinFormsExampleUpdates</span></span>](https://github.com/dlwyatt/WinFormsExampleUpdates)
- [<span data-ttu-id="c32ff-140">Windows PowerShell Tip of the Week:  Elemek kiválasztása egy listából</span><span class="sxs-lookup"><span data-stu-id="c32ff-140">Windows PowerShell Tip of the Week:  Selecting Items from a List Box</span></span>](https://technet.microsoft.com/library/ff730949.aspx)