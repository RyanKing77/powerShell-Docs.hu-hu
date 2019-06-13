---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: Egyéni beviteli mező létrehozása
ms.openlocfilehash: 9c1c3c72482157e849c0259e7d2e25ed969a4aab
ms.sourcegitcommit: a6f13c16a535acea279c0ddeca72f1f0d8a8ce4c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2019
ms.locfileid: "67030227"
---
# <a name="creating-a-custom-input-box"></a><span data-ttu-id="0734c-103">Egyéni beviteli mező létrehozása</span><span class="sxs-lookup"><span data-stu-id="0734c-103">Creating a Custom Input Box</span></span>

<span data-ttu-id="0734c-104">A Microsoft .NET-keretrendszer űrlap-összeállító szolgáltatások a Windows PowerShell 3.0-s és újabb kiadásaiban a grafikus egyéni beviteli mező-szkript.</span><span class="sxs-lookup"><span data-stu-id="0734c-104">Script a graphical custom input box by using Microsoft .NET Framework form-building features in Windows PowerShell 3.0 and later releases.</span></span>

## <a name="create-a-custom-graphical-input-box"></a><span data-ttu-id="0734c-105">Egy egyéni, grafikus beviteli mező létrehozása</span><span class="sxs-lookup"><span data-stu-id="0734c-105">Create a custom, graphical input box</span></span>

<span data-ttu-id="0734c-106">Másolja, és ezután illessze be a következő Windows PowerShell ISE-ben, és mentse egy Windows PowerShell-parancsprogram (.ps1).</span><span class="sxs-lookup"><span data-stu-id="0734c-106">Copy and then paste the following into Windows PowerShell ISE, and then save it as a Windows PowerShell script (.ps1).</span></span>

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

<span data-ttu-id="0734c-107">A szkript első lépése betöltése két .NET-osztályok: **System.Drawing** és **System.Windows.Forms**.</span><span class="sxs-lookup"><span data-stu-id="0734c-107">The script begins by loading two .NET Framework classes: **System.Drawing** and **System.Windows.Forms**.</span></span> <span data-ttu-id="0734c-108">Indítsa el a .NET-keretrendszer osztály egy új példányát **System.Windows.Forms.Form**; amely biztosítja, hogy egy üres űrlapot vagy ablakban, amelyhez elkezdhet szabályozza.</span><span class="sxs-lookup"><span data-stu-id="0734c-108">You then start a new instance of the .NET Framework class **System.Windows.Forms.Form**; that provides a blank form or window to which you can start adding controls.</span></span>

```powershell
$form = New-Object System.Windows.Forms.Form
```

<span data-ttu-id="0734c-109">Miután létrehozta az űrlap osztály egy példányát, értéket rendelni az osztály három tulajdonságot.</span><span class="sxs-lookup"><span data-stu-id="0734c-109">After you create an instance of the Form class, assign values to three properties of this class.</span></span>

- <span data-ttu-id="0734c-110">**Szöveg.**</span><span class="sxs-lookup"><span data-stu-id="0734c-110">**Text.**</span></span> <span data-ttu-id="0734c-111">Ez lesz az ablak címe.</span><span class="sxs-lookup"><span data-stu-id="0734c-111">This becomes the title of the window.</span></span>

- <span data-ttu-id="0734c-112">**Velikost.**</span><span class="sxs-lookup"><span data-stu-id="0734c-112">**Size.**</span></span> <span data-ttu-id="0734c-113">Ez a méretét az űrlap (képpontban).</span><span class="sxs-lookup"><span data-stu-id="0734c-113">This is the size of the form, in pixels.</span></span> <span data-ttu-id="0734c-114">A fenti szkript létrehoz egy képernyő, amely 300 képpont széles és 200 képpont magas.</span><span class="sxs-lookup"><span data-stu-id="0734c-114">The preceding script creates a form that’s 300 pixels wide by 200 pixels tall.</span></span>

- <span data-ttu-id="0734c-115">**Kezdőpozíció.**</span><span class="sxs-lookup"><span data-stu-id="0734c-115">**StartingPosition.**</span></span> <span data-ttu-id="0734c-116">Ez nem kötelező tulajdonsága **CenterScreen** az előző szkriptben.</span><span class="sxs-lookup"><span data-stu-id="0734c-116">This optional property is set to **CenterScreen** in the preceding script.</span></span> <span data-ttu-id="0734c-117">Ha nem ezt a tulajdonságot, a Windows kiválaszt egy helyet, az űrlap megnyitásakor.</span><span class="sxs-lookup"><span data-stu-id="0734c-117">If you don’t add this property, Windows selects a location when the form is opened.</span></span> <span data-ttu-id="0734c-118">Beállításával a **kezdőpozíció** való **CenterScreen**, akkor már automatikusan megjelenítése az űrlap a képernyő közepén minden alkalommal, amikor betölti.</span><span class="sxs-lookup"><span data-stu-id="0734c-118">By setting the **StartingPosition** to **CenterScreen**, you’re automatically displaying the form in the middle of the screen each time it loads.</span></span>

```powershell
$form.Text = 'Data Entry Form'
$form.Size = New-Object System.Drawing.Size(300,200)
$form.StartPosition = 'CenterScreen'
```

<span data-ttu-id="0734c-119">Ezután hozzon létre egy **OK** gombot az űrlapon.</span><span class="sxs-lookup"><span data-stu-id="0734c-119">Next, create an **OK** button for your form.</span></span> <span data-ttu-id="0734c-120">Adja meg a méretét és viselkedését a **OK** gombra.</span><span class="sxs-lookup"><span data-stu-id="0734c-120">Specify the size and behavior of the **OK** button.</span></span> <span data-ttu-id="0734c-121">Ebben a példában a gomb elhelyezése, a képernyő felső széle 120 képpont 75 képpont bal szélétől.</span><span class="sxs-lookup"><span data-stu-id="0734c-121">In this example, the button position is 120 pixels from the form’s top edge, and 75 pixels from the left edge.</span></span> <span data-ttu-id="0734c-122">A gomb magassága 23 képpont, amíg a gomb hossza 75 képpont.</span><span class="sxs-lookup"><span data-stu-id="0734c-122">The button height is 23 pixels, while the button length is 75 pixels.</span></span> <span data-ttu-id="0734c-123">A szkript előre meghatározott Windows Forms-típusok a gomb viselkedés határozza meg.</span><span class="sxs-lookup"><span data-stu-id="0734c-123">The script uses predefined Windows Forms types to determine the button behaviors.</span></span>

```powershell
$OKButton = New-Object System.Windows.Forms.Button
$OKButton.Location = New-Object System.Drawing.Point(75,120)
$OKButton.Size = New-Object System.Drawing.Size(75,23)
$OKButton.Text = 'OK'
$OKButton.DialogResult = [System.Windows.Forms.DialogResult]::OK
$form.AcceptButton = $OKButton
$form.Controls.Add($OKButton)
```

<span data-ttu-id="0734c-124">Hasonlóképpen, létrehozhat egy **Mégse** gombra.</span><span class="sxs-lookup"><span data-stu-id="0734c-124">Similarly, you create a **Cancel** button.</span></span> <span data-ttu-id="0734c-125">A **Mégse** gombot a felső 120 képpont, de az ablak bal szélétől 150 pixeles.</span><span class="sxs-lookup"><span data-stu-id="0734c-125">The **Cancel** button is 120 pixels from the top, but 150 pixels from the left edge of the window.</span></span>

```powershell
$CancelButton = New-Object System.Windows.Forms.Button
$CancelButton.Location = New-Object System.Drawing.Point(150,120)
$CancelButton.Size = New-Object System.Drawing.Size(75,23)
$CancelButton.Text = 'Cancel'
$CancelButton.DialogResult = [System.Windows.Forms.DialogResult]::Cancel
$form.CancelButton = $CancelButton
$form.Controls.Add($CancelButton)
```

<span data-ttu-id="0734c-126">Következő lépésként adja meg az ablak, amely leírja az adatokat, adja meg a felhasználók a felirat szövege.</span><span class="sxs-lookup"><span data-stu-id="0734c-126">Next, provide label text on your window that describes the information you want users to provide.</span></span>

```powershell
$label = New-Object System.Windows.Forms.Label
$label.Location = New-Object System.Drawing.Point(10,20)
$label.Size = New-Object System.Drawing.Size(280,20)
$label.Text = 'Please enter the information in the space below:'
$form.Controls.Add($label)
```

<span data-ttu-id="0734c-127">Adja hozzá a vezérlő (ebben az esetben a szövegmezőbe), amely lehetővé teszi a felhasználóknak adja meg az adatokat, akkor már ismertetett a felirat szövege.</span><span class="sxs-lookup"><span data-stu-id="0734c-127">Add the control (in this case, a text box) that lets users provide the information you’ve described in your label text.</span></span> <span data-ttu-id="0734c-128">Nincsenek alkalmazhat szövegmezők; mellett számos más vezérlők További vezérlők, lásd: [System.Windows.Forms Namespace](https://msdn.microsoft.com/library/k50ex0x9(v=vs.110).aspx) az MSDN Webhelyén.</span><span class="sxs-lookup"><span data-stu-id="0734c-128">There are many other controls you can apply besides text boxes; for more controls, see [System.Windows.Forms Namespace](https://msdn.microsoft.com/library/k50ex0x9(v=vs.110).aspx) on MSDN.</span></span>

```powershell
$textBox = New-Object System.Windows.Forms.TextBox
$textBox.Location = New-Object System.Drawing.Point(10,40)
$textBox.Size = New-Object System.Drawing.Size(260,20)
$form.Controls.Add($textBox)
```

<span data-ttu-id="0734c-129">Állítsa be a **Topmost** tulajdonságot **$true** kényszerítése az ablak megnyitásához nyissa meg a windows és a párbeszédpanelek interaktív irányítópultunkat.</span><span class="sxs-lookup"><span data-stu-id="0734c-129">Set the **Topmost** property to **$true** to force the window to open atop other open windows and dialog boxes.</span></span>

```powershell
$form.Topmost = $true
```

<span data-ttu-id="0734c-130">Ezután adja hozzá a kódsort az űrlap aktiválásához, és a fókuszt a szövegdobozba, amelyet Ön hozott létre.</span><span class="sxs-lookup"><span data-stu-id="0734c-130">Next, add this line of code to activate the form, and set the focus to the text box that you created.</span></span>

```powershell
$form.Add_Shown({$textBox.Select()})
```

<span data-ttu-id="0734c-131">Adja hozzá az alábbi kódsort az űrlap megjelenítésére a Windows.</span><span class="sxs-lookup"><span data-stu-id="0734c-131">Add the following line of code to display the form in Windows.</span></span>

```powershell
$result = $form.ShowDialog()
```

<span data-ttu-id="0734c-132">Végül a kód belül a **Ha** blokk arra utasítja a Windows Mi a teendő az űrlapot, miután a felhasználók adjon meg szöveget a szövegmezőbe, és kattintson a **OK** gombra vagy nyomja le a **Enter** kulcs.</span><span class="sxs-lookup"><span data-stu-id="0734c-132">Finally, the code inside the **If** block instructs Windows what to do with the form after users provide text in the text box, and then click the **OK** button or press the **Enter** key.</span></span>

```powershell
if ($result -eq [System.Windows.Forms.DialogResult]::OK)
{
    $x = $textBox.Text
    $x
}
```

## <a name="see-also"></a><span data-ttu-id="0734c-133">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="0734c-133">See Also</span></span>

- [<span data-ttu-id="0734c-134">Hey Scripting Guy:  Miért nem működnek a grafikus PowerShell-példákat?</span><span class="sxs-lookup"><span data-stu-id="0734c-134">Hey Scripting Guy:  Why don’t these PowerShell GUI examples work?</span></span>](https://go.microsoft.com/fwlink/?LinkId=506644)
- [<span data-ttu-id="0734c-135">GitHub: Dave Wyatt WinFormsExampleUpdates</span><span class="sxs-lookup"><span data-stu-id="0734c-135">GitHub: Dave Wyatt's WinFormsExampleUpdates</span></span>](https://github.com/dlwyatt/WinFormsExampleUpdates)
- [<span data-ttu-id="0734c-136">Windows PowerShell Tip of the Week:  Egyéni beviteli mező létrehozása</span><span class="sxs-lookup"><span data-stu-id="0734c-136">Windows PowerShell Tip of the Week:  Creating a Custom Input Box</span></span>](https://technet.microsoft.com/library/ff730941.aspx)
