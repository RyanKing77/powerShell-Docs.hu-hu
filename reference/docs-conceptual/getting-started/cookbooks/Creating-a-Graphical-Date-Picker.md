---
ms.date: 06/05/2017
keywords: PowerShell parancsmag
title: Grafikus dátumválasztó létrehozása
ms.assetid: c1cb722c-41e9-4baa-be83-59b4653222e9
ms.openlocfilehash: 3727c90c314a6fc1b3a338ec60e44259f153d954
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="creating-a-graphical-date-picker"></a><span data-ttu-id="d06f4-103">Grafikus dátumválasztó létrehozása</span><span class="sxs-lookup"><span data-stu-id="d06f4-103">Creating a Graphical Date Picker</span></span>

<span data-ttu-id="d06f4-104">Egy grafikus, naptár-stílusú Control, amely lehetővé teszi a felhasználóknak, válassza ki a hónap napját űrlapok létrehozásához használja a Windows PowerShell 3.0-s és újabb verziókban.</span><span class="sxs-lookup"><span data-stu-id="d06f4-104">Use Windows PowerShell 3.0 and later releases to create a form with a graphical, calendar-style control that lets users select a day of the month.</span></span>

## <a name="create-a-graphical-date-picker-control"></a><span data-ttu-id="d06f4-105">Hozzon létre egy grafikus dátumválasztó-vezérlő</span><span class="sxs-lookup"><span data-stu-id="d06f4-105">Create a graphical date-picker control</span></span>

<span data-ttu-id="d06f4-106">Másolja és illessze be a következő Windows PowerShell ISE-be, és mentse egy Windows PowerShell-parancsfájlt (.ps1).</span><span class="sxs-lookup"><span data-stu-id="d06f4-106">Copy and then paste the following into Windows PowerShell ISE, and then save it as a Windows PowerShell script (.ps1).</span></span>

```powershell
Add-Type -AssemblyName System.Windows.Forms
Add-Type -AssemblyName System.Drawing

$form = New-Object Windows.Forms.Form

$form.Text = 'Select a Date'
$form.Size = New-Object Drawing.Size @(243,230)
$form.StartPosition = 'CenterScreen'

$calendar = New-Object System.Windows.Forms.MonthCalendar
$calendar.ShowTodayCircle = $false
$calendar.MaxSelectionCount = 1
$form.Controls.Add($calendar)

$OKButton = New-Object System.Windows.Forms.Button
$OKButton.Location = New-Object System.Drawing.Point(38,165)
$OKButton.Size = New-Object System.Drawing.Size(75,23)
$OKButton.Text = 'OK'
$OKButton.DialogResult = [System.Windows.Forms.DialogResult]::OK
$form.AcceptButton = $OKButton
$form.Controls.Add($OKButton)

$CancelButton = New-Object System.Windows.Forms.Button
$CancelButton.Location = New-Object System.Drawing.Point(113,165)
$CancelButton.Size = New-Object System.Drawing.Size(75,23)
$CancelButton.Text = 'Cancel'
$CancelButton.DialogResult = [System.Windows.Forms.DialogResult]::Cancel
$form.CancelButton = $CancelButton
$form.Controls.Add($CancelButton)

$form.Topmost = $true

$result = $form.ShowDialog()

if ($result -eq [System.Windows.Forms.DialogResult]::OK)
{
    $date = $calendar.SelectionStart
    Write-Host "Date selected: $($date.ToShortDateString())"
}
```

<span data-ttu-id="d06f4-107">A parancsfájl első lépése két .NET-keretrendszer osztály betöltése: **System.Drawing** és **System.Windows.Forms**.</span><span class="sxs-lookup"><span data-stu-id="d06f4-107">The script begins by loading two .NET Framework classes: **System.Drawing** and **System.Windows.Forms**.</span></span> <span data-ttu-id="d06f4-108">Majd indítsa el a .NET-keretrendszer osztály új példánya **Windows.Forms.Form**; biztosítja az üres űrlapból, vagy ablak, amelyhez elkezdhet szabályozza.</span><span class="sxs-lookup"><span data-stu-id="d06f4-108">You then start a new instance of the .NET Framework class **Windows.Forms.Form**; that provides a blank form or window to which you can start adding controls.</span></span>

```powershell
$form = New-Object Windows.Forms.Form
```

<span data-ttu-id="d06f4-109">Az űrlap osztály példányának létrehozása után értéket hozzárendelni az osztály három tulajdonságot.</span><span class="sxs-lookup"><span data-stu-id="d06f4-109">After you create an instance of the Form class, assign values to three properties of this class.</span></span>

- <span data-ttu-id="d06f4-110">**Text.**</span><span class="sxs-lookup"><span data-stu-id="d06f4-110">**Text.**</span></span> <span data-ttu-id="d06f4-111">Ez lesz az ablak címe.</span><span class="sxs-lookup"><span data-stu-id="d06f4-111">This becomes the title of the window.</span></span>

- <span data-ttu-id="d06f4-112">**Size.**</span><span class="sxs-lookup"><span data-stu-id="d06f4-112">**Size.**</span></span> <span data-ttu-id="d06f4-113">Ez az az űrlap képpontban méretét.</span><span class="sxs-lookup"><span data-stu-id="d06f4-113">This is the size of the form, in pixels.</span></span> <span data-ttu-id="d06f4-114">Az előző parancsfájl, amely 243 x széles 230 képpont magas űrlap hoz létre.</span><span class="sxs-lookup"><span data-stu-id="d06f4-114">The preceding script creates a form that’s 243 pixels wide by 230 pixels tall.</span></span>

- <span data-ttu-id="d06f4-115">**StartingPosition.**</span><span class="sxs-lookup"><span data-stu-id="d06f4-115">**StartingPosition.**</span></span> <span data-ttu-id="d06f4-116">Ez nem kötelező tulajdonság értéke **CenterScreen** az előző parancsfájlban.</span><span class="sxs-lookup"><span data-stu-id="d06f4-116">This optional property is set to **CenterScreen** in the preceding script.</span></span> <span data-ttu-id="d06f4-117">Ez a tulajdonság nem ad hozzá, ha a Windows kiválaszt egy helyet, az űrlap megnyitásakor.</span><span class="sxs-lookup"><span data-stu-id="d06f4-117">If you don’t add this property, Windows selects a location when the form is opened.</span></span> <span data-ttu-id="d06f4-118">Úgy, hogy a **StartingPosition** való **CenterScreen**, akkor program automatikusan jeleníti meg az űrlap közepén a képernyő minden alkalommal, amikor betölti a.</span><span class="sxs-lookup"><span data-stu-id="d06f4-118">By setting the **StartingPosition** to **CenterScreen**, you’re automatically displaying the form in the middle of the screen each time it loads.</span></span>

```powershell
$form.Text = 'Select a Date'
$form.Size = New-Object Drawing.Size @(243,230)
$form.StartPosition = 'CenterScreen'
```

<span data-ttu-id="d06f4-119">Ezután hozzon létre, és adja hozzá a havinaptár-vezérlőben a képernyőn.</span><span class="sxs-lookup"><span data-stu-id="d06f4-119">Next, create and then add a calendar control in your form.</span></span> <span data-ttu-id="d06f4-120">Ebben a példában az aktuális nap nem a kijelölt vagy körben.</span><span class="sxs-lookup"><span data-stu-id="d06f4-120">In this example, the current day is not highlighted or circled.</span></span> <span data-ttu-id="d06f4-121">Csak egy nap a naptár egy időben bejelölésével.</span><span class="sxs-lookup"><span data-stu-id="d06f4-121">Users can select only one day on the calendar at one time.</span></span>

```powershell
$calendar = New-Object System.Windows.Forms.MonthCalendar
$calendar.ShowTodayCircle = $false
$calendar.MaxSelectionCount = 1
$form.Controls.Add($calendar)
```

<span data-ttu-id="d06f4-122">Ezután hozzon létre egy **OK** gombra az űrlap.</span><span class="sxs-lookup"><span data-stu-id="d06f4-122">Next, create an **OK** button for your form.</span></span> <span data-ttu-id="d06f4-123">Adja meg a méretét és viselkedését a **OK** gombra.</span><span class="sxs-lookup"><span data-stu-id="d06f4-123">Specify the size and behavior of the **OK** button.</span></span> <span data-ttu-id="d06f4-124">Ebben a példában a gomb pozíciója 165 a képernyő felső szélétől, és 38 képpontok bal szélétől.</span><span class="sxs-lookup"><span data-stu-id="d06f4-124">In this example, the button position is 165 pixels from the form’s top edge, and 38 pixels from the left edge.</span></span> <span data-ttu-id="d06f4-125">A gomb magassága 23 képpont, amíg a gomb hossza 75 képpontban megadva.</span><span class="sxs-lookup"><span data-stu-id="d06f4-125">The button height is 23 pixels, while the button length is 75 pixels.</span></span> <span data-ttu-id="d06f4-126">A parancsfájl előre meghatározott Windows Forms-típusok gombra viselkedésmódját meghatározására használja.</span><span class="sxs-lookup"><span data-stu-id="d06f4-126">The script uses predefined Windows Forms types to determine the button behaviors.</span></span>

```powershell
$OKButton = New-Object System.Windows.Forms.Button
$OKButton.Location = New-Object System.Drawing.Point(38,165)
$OKButton.Size = New-Object System.Drawing.Size(75,23)
$OKButton.Text = 'OK'
$OKButton.DialogResult = [System.Windows.Forms.DialogResult]::OK
$form.AcceptButton = $OKButton
$form.Controls.Add($OKButton)
```

<span data-ttu-id="d06f4-127">Hasonlóképpen, létrehozhat egy **Mégse** gombra.</span><span class="sxs-lookup"><span data-stu-id="d06f4-127">Similarly, you create a **Cancel** button.</span></span> <span data-ttu-id="d06f4-128">A **Mégse** gomb, a lista elejéről 165 képpont, de az ablak bal szélétől 113 képpont.</span><span class="sxs-lookup"><span data-stu-id="d06f4-128">The **Cancel** button is 165 pixels from the top, but 113 pixels from the left edge of the window.</span></span>

```powershell
$CancelButton = New-Object System.Windows.Forms.Button
$CancelButton.Location = New-Object System.Drawing.Point(113,165)
$CancelButton.Size = New-Object System.Drawing.Size(75,23)
$CancelButton.Text = 'Cancel'
$CancelButton.DialogResult = [System.Windows.Forms.DialogResult]::Cancel
$form.CancelButton = $CancelButton
$form.Controls.Add($CancelButton)
```

<span data-ttu-id="d06f4-129">Állítsa be a **Topmost** tulajdonságot **$true** azzal kényszerítheti a az ablak elveire más nyissa meg a windows és a párbeszédpanel megnyitásához.</span><span class="sxs-lookup"><span data-stu-id="d06f4-129">Set the **Topmost** property to **$true** to force the window to open atop other open windows and dialog boxes.</span></span>

```powershell
$form.Topmost = $true
```

<span data-ttu-id="d06f4-130">Adja hozzá a következő kódsort a képernyőn megjelenő Windows.</span><span class="sxs-lookup"><span data-stu-id="d06f4-130">Add the following line of code to display the form in Windows.</span></span>

```powershell
$result = $form.ShowDialog()
```

<span data-ttu-id="d06f4-131">Végezetül, a kódot a **Ha** blokk utasítja Windows Mi a teendő az űrlapot, miután a felhasználók válasszon ki egy napot a naptárban, és kattintson a **OK** gombra vagy nyomja meg a **Enter** kulcs.</span><span class="sxs-lookup"><span data-stu-id="d06f4-131">Finally, the code inside the **If** block instructs Windows what to do with the form after users select a day on the calendar, and then click the **OK** button or press the **Enter** key.</span></span> <span data-ttu-id="d06f4-132">A Windows PowerShell a felhasználók számára kijelölt dátumának megjelenítése.</span><span class="sxs-lookup"><span data-stu-id="d06f4-132">Windows PowerShell displays the selected date to users.</span></span>

```powershell
if ($result -eq [System.Windows.Forms.DialogResult]::OK)
{
    $date = $calendar.SelectionStart
    Write-Host "Date selected: $($date.ToShortDateString())"
}
```

## <a name="see-also"></a><span data-ttu-id="d06f4-133">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="d06f4-133">See Also</span></span>

- [<span data-ttu-id="d06f4-134">Hey Scripting Guy: Miért nem PowerShell grafikus felhasználói Felülettel példákban használhatók?</span><span class="sxs-lookup"><span data-stu-id="d06f4-134">Hey Scripting Guy:  Why don’t these PowerShell GUI examples work?</span></span>](http://go.microsoft.com/fwlink/?LinkId=506644)
- [<span data-ttu-id="d06f4-135">GitHub: Dave Wyatt WinFormsExampleUpdates</span><span class="sxs-lookup"><span data-stu-id="d06f4-135">GitHub: Dave Wyatt's WinFormsExampleUpdates</span></span>](https://github.com/dlwyatt/WinFormsExampleUpdates)
- [<span data-ttu-id="d06f4-136">A hét Windows PowerShell tipp: grafikus Dátumválasztó létrehozása</span><span class="sxs-lookup"><span data-stu-id="d06f4-136">Windows PowerShell Tip of the Week:  Creating a Graphical Date Picker</span></span>](http://technet.microsoft.com/library/ff730942.aspx)