---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: Grafikus dátumválasztó létrehozása
ms.assetid: c1cb722c-41e9-4baa-be83-59b4653222e9
ms.openlocfilehash: 6dd43a3b1f4c67633ad1755de3db88eb8c6772c8
ms.sourcegitcommit: 221b7daab7f597f8b2e4864cf9b5d9dda9b9879b
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 11/27/2018
ms.locfileid: "52320329"
---
# <a name="creating-a-graphical-date-picker"></a><span data-ttu-id="39546-103">Grafikus dátumválasztó létrehozása</span><span class="sxs-lookup"><span data-stu-id="39546-103">Creating a Graphical Date Picker</span></span>

<span data-ttu-id="39546-104">A grafikus, naptár stílusú vezérlőelemmel, amely lehetővé teszi a felhasználóknak, válasszon ki egy napot a hónap egy űrlap létrehozásához használja a Windows PowerShell 3.0-s és újabb verziókban.</span><span class="sxs-lookup"><span data-stu-id="39546-104">Use Windows PowerShell 3.0 and later releases to create a form with a graphical, calendar-style control that lets users select a day of the month.</span></span>

## <a name="create-a-graphical-date-picker-control"></a><span data-ttu-id="39546-105">Grafikus Dátumválasztó vezérlőelem létrehozása</span><span class="sxs-lookup"><span data-stu-id="39546-105">Create a graphical date-picker control</span></span>

<span data-ttu-id="39546-106">Másolja, és ezután illessze be a következő Windows PowerShell ISE-ben, és mentse egy Windows PowerShell-parancsprogram (.ps1).</span><span class="sxs-lookup"><span data-stu-id="39546-106">Copy and then paste the following into Windows PowerShell ISE, and then save it as a Windows PowerShell script (.ps1).</span></span>

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

<span data-ttu-id="39546-107">A szkript első lépése két .NET-keretrendszer osztály betöltésekor: **System.Drawing** és **System.Windows.Forms**.</span><span class="sxs-lookup"><span data-stu-id="39546-107">The script begins by loading two .NET Framework classes: **System.Drawing** and **System.Windows.Forms**.</span></span> <span data-ttu-id="39546-108">Indítsa el a .NET-keretrendszer osztály egy új példányát **Windows.Forms.Form**; amely biztosítja, hogy egy üres űrlapot vagy ablakban, amelyhez elkezdhet szabályozza.</span><span class="sxs-lookup"><span data-stu-id="39546-108">You then start a new instance of the .NET Framework class **Windows.Forms.Form**; that provides a blank form or window to which you can start adding controls.</span></span>

```powershell
$form = New-Object Windows.Forms.Form
```

<span data-ttu-id="39546-109">Miután létrehozta az űrlap osztály egy példányát, értéket rendelni az osztály három tulajdonságot.</span><span class="sxs-lookup"><span data-stu-id="39546-109">After you create an instance of the Form class, assign values to three properties of this class.</span></span>

- <span data-ttu-id="39546-110">**Szöveg.**</span><span class="sxs-lookup"><span data-stu-id="39546-110">**Text.**</span></span> <span data-ttu-id="39546-111">Ez lesz az ablak címe.</span><span class="sxs-lookup"><span data-stu-id="39546-111">This becomes the title of the window.</span></span>

- <span data-ttu-id="39546-112">**Velikost.**</span><span class="sxs-lookup"><span data-stu-id="39546-112">**Size.**</span></span> <span data-ttu-id="39546-113">Ez a méretét az űrlap (képpontban).</span><span class="sxs-lookup"><span data-stu-id="39546-113">This is the size of the form, in pixels.</span></span> <span data-ttu-id="39546-114">A fenti szkript létrehoz egy képernyő, amely 243 képpont szélességű és 230 képpont magas.</span><span class="sxs-lookup"><span data-stu-id="39546-114">The preceding script creates a form that’s 243 pixels wide by 230 pixels tall.</span></span>

- <span data-ttu-id="39546-115">**Kezdőpozíció.**</span><span class="sxs-lookup"><span data-stu-id="39546-115">**StartingPosition.**</span></span> <span data-ttu-id="39546-116">Ez nem kötelező tulajdonsága **CenterScreen** az előző szkriptben.</span><span class="sxs-lookup"><span data-stu-id="39546-116">This optional property is set to **CenterScreen** in the preceding script.</span></span> <span data-ttu-id="39546-117">Ha nem ezt a tulajdonságot, a Windows kiválaszt egy helyet, az űrlap megnyitásakor.</span><span class="sxs-lookup"><span data-stu-id="39546-117">If you don’t add this property, Windows selects a location when the form is opened.</span></span> <span data-ttu-id="39546-118">Beállításával a **kezdőpozíció** való **CenterScreen**, akkor már automatikusan megjelenítése az űrlap a képernyő közepén minden alkalommal, amikor betölti.</span><span class="sxs-lookup"><span data-stu-id="39546-118">By setting the **StartingPosition** to **CenterScreen**, you’re automatically displaying the form in the middle of the screen each time it loads.</span></span>

```powershell
$form.Text = 'Select a Date'
$form.Size = New-Object Drawing.Size @(243,230)
$form.StartPosition = 'CenterScreen'
```

<span data-ttu-id="39546-119">Következő lépésként hozzon létre, és adja hozzá a Naptár vezérlőelem a képernyőn.</span><span class="sxs-lookup"><span data-stu-id="39546-119">Next, create and then add a calendar control in your form.</span></span> <span data-ttu-id="39546-120">Ebben a példában az aktuális nap nem kiemelt vagy bekarikázott.</span><span class="sxs-lookup"><span data-stu-id="39546-120">In this example, the current day is not highlighted or circled.</span></span> <span data-ttu-id="39546-121">Felhasználók által választható csak egyetlen napon a naptárban egy időben.</span><span class="sxs-lookup"><span data-stu-id="39546-121">Users can select only one day on the calendar at one time.</span></span>

```powershell
$calendar = New-Object System.Windows.Forms.MonthCalendar
$calendar.ShowTodayCircle = $false
$calendar.MaxSelectionCount = 1
$form.Controls.Add($calendar)
```

<span data-ttu-id="39546-122">Ezután hozzon létre egy **OK** gombot az űrlapon.</span><span class="sxs-lookup"><span data-stu-id="39546-122">Next, create an **OK** button for your form.</span></span> <span data-ttu-id="39546-123">Adja meg a méretét és viselkedését a **OK** gombra.</span><span class="sxs-lookup"><span data-stu-id="39546-123">Specify the size and behavior of the **OK** button.</span></span> <span data-ttu-id="39546-124">Ebben a példában a gomb pozice je 165 a képernyő felső széle, és 38 képpontok bal szélétől.</span><span class="sxs-lookup"><span data-stu-id="39546-124">In this example, the button position is 165 pixels from the form’s top edge, and 38 pixels from the left edge.</span></span> <span data-ttu-id="39546-125">A gomb magassága 23 képpont, amíg a gomb hossza 75 képpont.</span><span class="sxs-lookup"><span data-stu-id="39546-125">The button height is 23 pixels, while the button length is 75 pixels.</span></span> <span data-ttu-id="39546-126">A szkript előre meghatározott Windows Forms-típusok a gomb viselkedés határozza meg.</span><span class="sxs-lookup"><span data-stu-id="39546-126">The script uses predefined Windows Forms types to determine the button behaviors.</span></span>

```powershell
$OKButton = New-Object System.Windows.Forms.Button
$OKButton.Location = New-Object System.Drawing.Point(38,165)
$OKButton.Size = New-Object System.Drawing.Size(75,23)
$OKButton.Text = 'OK'
$OKButton.DialogResult = [System.Windows.Forms.DialogResult]::OK
$form.AcceptButton = $OKButton
$form.Controls.Add($OKButton)
```

<span data-ttu-id="39546-127">Hasonlóképpen, létrehozhat egy **Mégse** gombra.</span><span class="sxs-lookup"><span data-stu-id="39546-127">Similarly, you create a **Cancel** button.</span></span> <span data-ttu-id="39546-128">A **Mégse** gombot a felső 165 képpont, de az ablak bal szélétől 113 képpont.</span><span class="sxs-lookup"><span data-stu-id="39546-128">The **Cancel** button is 165 pixels from the top, but 113 pixels from the left edge of the window.</span></span>

```powershell
$CancelButton = New-Object System.Windows.Forms.Button
$CancelButton.Location = New-Object System.Drawing.Point(113,165)
$CancelButton.Size = New-Object System.Drawing.Size(75,23)
$CancelButton.Text = 'Cancel'
$CancelButton.DialogResult = [System.Windows.Forms.DialogResult]::Cancel
$form.CancelButton = $CancelButton
$form.Controls.Add($CancelButton)
```

<span data-ttu-id="39546-129">Állítsa be a **Topmost** tulajdonságot **$true** kényszerítése az ablak megnyitásához nyissa meg a windows és a párbeszédpanelek interaktív irányítópultunkat.</span><span class="sxs-lookup"><span data-stu-id="39546-129">Set the **Topmost** property to **$true** to force the window to open atop other open windows and dialog boxes.</span></span>

```powershell
$form.Topmost = $true
```

<span data-ttu-id="39546-130">Adja hozzá az alábbi kódsort az űrlap megjelenítésére a Windows.</span><span class="sxs-lookup"><span data-stu-id="39546-130">Add the following line of code to display the form in Windows.</span></span>

```powershell
$result = $form.ShowDialog()
```

<span data-ttu-id="39546-131">Végül a kód belül a **Ha** blokk arra utasítja a Windows Mi a teendő az űrlapot, miután a felhasználók válasszon ki egy napot a naptárban, és kattintson a **OK** gombra vagy nyomja le a **Enter** kulcs.</span><span class="sxs-lookup"><span data-stu-id="39546-131">Finally, the code inside the **If** block instructs Windows what to do with the form after users select a day on the calendar, and then click the **OK** button or press the **Enter** key.</span></span> <span data-ttu-id="39546-132">Windows PowerShell a választott dátum felhasználókat jeleníti meg.</span><span class="sxs-lookup"><span data-stu-id="39546-132">Windows PowerShell displays the selected date to users.</span></span>

```powershell
if ($result -eq [System.Windows.Forms.DialogResult]::OK)
{
    $date = $calendar.SelectionStart
    Write-Host "Date selected: $($date.ToShortDateString())"
}
```

## <a name="see-also"></a><span data-ttu-id="39546-133">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="39546-133">See Also</span></span>

- [<span data-ttu-id="39546-134">Hey Scripting Guy: Miért nem a grafikus PowerShell-példákat működnek?</span><span class="sxs-lookup"><span data-stu-id="39546-134">Hey Scripting Guy:  Why don’t these PowerShell GUI examples work?</span></span>](https://go.microsoft.com/fwlink/?LinkId=506644)
- [<span data-ttu-id="39546-135">GitHub: Dave Wyatt WinFormsExampleUpdates</span><span class="sxs-lookup"><span data-stu-id="39546-135">GitHub: Dave Wyatt's WinFormsExampleUpdates</span></span>](https://github.com/dlwyatt/WinFormsExampleUpdates)
- [<span data-ttu-id="39546-136">Windows PowerShell Tip of the Week: grafikus Dátumválasztó létrehozása</span><span class="sxs-lookup"><span data-stu-id="39546-136">Windows PowerShell Tip of the Week:  Creating a Graphical Date Picker</span></span>](https://technet.microsoft.com/library/ff730942.aspx)