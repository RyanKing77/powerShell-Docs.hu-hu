---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: Grafikus dátumválasztó létrehozása
ms.assetid: c1cb722c-41e9-4baa-be83-59b4653222e9
ms.openlocfilehash: d3b24af935e781a8a36fc346a6108baaed37b6db
ms.sourcegitcommit: 3f6002e7109373eda31cc65fc84d2600447cb7e9
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/11/2019
ms.locfileid: "59506801"
---
# <a name="creating-a-graphical-date-picker"></a><span data-ttu-id="2ad56-103">Grafikus dátumválasztó létrehozása</span><span class="sxs-lookup"><span data-stu-id="2ad56-103">Creating a Graphical Date Picker</span></span>

<span data-ttu-id="2ad56-104">A grafikus, naptár stílusú vezérlőelemmel, amely lehetővé teszi a felhasználóknak, válasszon ki egy napot a hónap egy űrlap létrehozásához használja a Windows PowerShell 3.0-s és újabb verziókban.</span><span class="sxs-lookup"><span data-stu-id="2ad56-104">Use Windows PowerShell 3.0 and later releases to create a form with a graphical, calendar-style control that lets users select a day of the month.</span></span>

## <a name="create-a-graphical-date-picker-control"></a><span data-ttu-id="2ad56-105">Grafikus Dátumválasztó vezérlőelem létrehozása</span><span class="sxs-lookup"><span data-stu-id="2ad56-105">Create a graphical date-picker control</span></span>

<span data-ttu-id="2ad56-106">Másolja, és ezután illessze be a következő Windows PowerShell ISE-ben, és mentse egy Windows PowerShell-parancsprogram (.ps1).</span><span class="sxs-lookup"><span data-stu-id="2ad56-106">Copy and then paste the following into Windows PowerShell ISE, and then save it as a Windows PowerShell script (.ps1).</span></span>

```powershell
Add-Type -AssemblyName System.Windows.Forms
Add-Type -AssemblyName System.Drawing

$form = New-Object Windows.Forms.Form -Property @{
    StartPosition = [Windows.Forms.FormStartPosition]::CenterScreen
    Size          = New-Object Drawing.Size 243, 230
    Text          = 'Select a Date'
    Topmost       = $true
}

$calendar = New-Object Windows.Forms.MonthCalendar -Property @{
    ShowTodayCircle   = $false
    MaxSelectionCount = 1
}
$form.Controls.Add($calendar)

$OKButton = New-Object Windows.Forms.Button -Property @{
    Location     = New-Object Drawing.Point 38, 165
    Size         = New-Object Drawing.Size 75, 23
    Text         = 'OK'
    DialogResult = [Windows.Forms.DialogResult]::OK
}
$form.AcceptButton = $OKButton
$form.Controls.Add($OKButton)

$CancelButton = New-Object Windows.Forms.Button -Property @{
    Location     = New-Object Drawing.Point 113, 165
    Size         = New-Object Drawing.Size 75, 23
    Text         = 'Cancel'
    DialogResult = [Windows.Forms.DialogResult]::Cancel
}
$form.CancelButton = $CancelButton
$form.Controls.Add($CancelButton)

$result = $form.ShowDialog()

if ($result -eq [Windows.Forms.DialogResult]::OK) {
    $date = $calendar.SelectionStart
    Write-Host "Date selected: $($date.ToShortDateString())"
}
```

<span data-ttu-id="2ad56-107">A szkript első lépése betöltése két .NET-osztályok: **System.Drawing** és **System.Windows.Forms**.</span><span class="sxs-lookup"><span data-stu-id="2ad56-107">The script begins by loading two .NET Framework classes: **System.Drawing** and **System.Windows.Forms**.</span></span>
<span data-ttu-id="2ad56-108">Indítsa el a .NET-keretrendszer osztály egy új példányát **Windows.Forms.Form**; amely biztosítja, hogy egy üres űrlapot vagy ablakban, amelyhez elkezdhet szabályozza.</span><span class="sxs-lookup"><span data-stu-id="2ad56-108">You then start a new instance of the .NET Framework class **Windows.Forms.Form**; that provides a blank form or window to which you can start adding controls.</span></span>

```powershell
$form = New-Object Windows.Forms.Form -Property @{
    StartPosition = [Windows.Forms.FormStartPosition]::CenterScreen
    Size          = New-Object Drawing.Size 243, 230
    Text          = 'Select a Date'
    Topmost       = $true
}
```

<span data-ttu-id="2ad56-109">Ebben a példában ez az osztály tulajdonságait négy értékeket rendelő használatával a **tulajdonság** tulajdonság és a kivonattábla kulcsa.</span><span class="sxs-lookup"><span data-stu-id="2ad56-109">This example assigns values to four properties of this class by using the **Property** property and hashtable.</span></span>

1. <span data-ttu-id="2ad56-110">**StartPosition**: Ha nem ezt a tulajdonságot, a Windows kiválaszt egy helyet, az űrlap megnyitásakor.</span><span class="sxs-lookup"><span data-stu-id="2ad56-110">**StartPosition**: If you don’t add this property, Windows selects a location when the form is opened.</span></span>
   <span data-ttu-id="2ad56-111">Úgy, hogy ez a tulajdonság **CenterScreen**, akkor már automatikusan megjelenítése az űrlap a képernyő közepén minden alkalommal, amikor betölti.</span><span class="sxs-lookup"><span data-stu-id="2ad56-111">By setting this property to **CenterScreen**, you’re automatically displaying the form in the middle of the screen each time it loads.</span></span>

2. <span data-ttu-id="2ad56-112">**Méret**: Ez a méretét az űrlap (képpontban).</span><span class="sxs-lookup"><span data-stu-id="2ad56-112">**Size**: This is the size of the form, in pixels.</span></span>
   <span data-ttu-id="2ad56-113">A fenti szkript létrehoz egy képernyő, amely 243 képpont szélességű és 230 képpont magas.</span><span class="sxs-lookup"><span data-stu-id="2ad56-113">The preceding script creates a form that’s 243 pixels wide by 230 pixels tall.</span></span>

3. <span data-ttu-id="2ad56-114">**Szöveg**: Ez lesz az ablak címe.</span><span class="sxs-lookup"><span data-stu-id="2ad56-114">**Text**: This becomes the title of the window.</span></span>

4. <span data-ttu-id="2ad56-115">**Legfelső**: Ez a tulajdonság beállításával `$true`, kényszerítheti az ablak megnyitásához nyissa meg a windows és a párbeszédpanelek interaktív irányítópultunkat.</span><span class="sxs-lookup"><span data-stu-id="2ad56-115">**Topmost**: By setting this property to `$true`, you can force the window to open atop other open windows and dialog boxes.</span></span>

<span data-ttu-id="2ad56-116">Következő lépésként hozzon létre, és adja hozzá a Naptár vezérlőelem a képernyőn.</span><span class="sxs-lookup"><span data-stu-id="2ad56-116">Next, create and then add a calendar control in your form.</span></span>
<span data-ttu-id="2ad56-117">Ebben a példában az aktuális nap nem kiemelt vagy bekarikázott.</span><span class="sxs-lookup"><span data-stu-id="2ad56-117">In this example, the current day is not highlighted or circled.</span></span>
<span data-ttu-id="2ad56-118">Felhasználók által választható csak egyetlen napon a naptárban egy időben.</span><span class="sxs-lookup"><span data-stu-id="2ad56-118">Users can select only one day on the calendar at one time.</span></span>

```powershell
$calendar = New-Object Windows.Forms.MonthCalendar -Property @{
    ShowTodayCircle   = $false
    MaxSelectionCount = 1
}
$form.Controls.Add($calendar)
```

<span data-ttu-id="2ad56-119">Ezután hozzon létre egy **OK** gombot az űrlapon.</span><span class="sxs-lookup"><span data-stu-id="2ad56-119">Next, create an **OK** button for your form.</span></span>
<span data-ttu-id="2ad56-120">Adja meg a méretét és viselkedését a **OK** gombra.</span><span class="sxs-lookup"><span data-stu-id="2ad56-120">Specify the size and behavior of the **OK** button.</span></span>
<span data-ttu-id="2ad56-121">Ebben a példában a gomb pozice je 165 a képernyő felső széle, és 38 képpontok bal szélétől.</span><span class="sxs-lookup"><span data-stu-id="2ad56-121">In this example, the button position is 165 pixels from the form’s top edge, and 38 pixels from the left edge.</span></span>
<span data-ttu-id="2ad56-122">A gomb magassága 23 képpont, amíg a gomb hossza 75 képpont.</span><span class="sxs-lookup"><span data-stu-id="2ad56-122">The button height is 23 pixels, while the button length is 75 pixels.</span></span>
<span data-ttu-id="2ad56-123">A szkript előre meghatározott Windows Forms-típusok a gomb viselkedés határozza meg.</span><span class="sxs-lookup"><span data-stu-id="2ad56-123">The script uses predefined Windows Forms types to determine the button behaviors.</span></span>

```powershell
$OKButton = New-Object Windows.Forms.Button -Property @{
    Location     = New-Object Drawing.Point 38, 165
    Size         = New-Object Drawing.Size 75, 23
    Text         = 'OK'
    DialogResult = [Windows.Forms.DialogResult]::OK
}
$form.AcceptButton = $OKButton
$form.Controls.Add($OKButton)
```

<span data-ttu-id="2ad56-124">Hasonlóképpen, létrehozhat egy **Mégse** gombra.</span><span class="sxs-lookup"><span data-stu-id="2ad56-124">Similarly, you create a **Cancel** button.</span></span>
<span data-ttu-id="2ad56-125">A **Mégse** gombot a felső 165 képpont, de az ablak bal szélétől 113 képpont.</span><span class="sxs-lookup"><span data-stu-id="2ad56-125">The **Cancel** button is 165 pixels from the top, but 113 pixels from the left edge of the window.</span></span>

```powershell
$CancelButton = New-Object Windows.Forms.Button -Property @{
    Location     = New-Object Drawing.Point 113, 165
    Size         = New-Object Drawing.Size 75, 23
    Text         = 'Cancel'
    DialogResult = [Windows.Forms.DialogResult]::Cancel
}
$form.CancelButton = $CancelButton
$form.Controls.Add($CancelButton)
```

<span data-ttu-id="2ad56-126">Adja hozzá az alábbi kódsort az űrlap megjelenítésére a Windows.</span><span class="sxs-lookup"><span data-stu-id="2ad56-126">Add the following line of code to display the form in Windows.</span></span>

```powershell
$result = $form.ShowDialog()
```

<span data-ttu-id="2ad56-127">Végül a kód belül a `if` blokk arra utasítja a Windows Mi a teendő az űrlapot, miután a felhasználók válasszon ki egy napot a naptárban, és kattintson a **OK** gombra vagy nyomja le a **Enter** kulcs.</span><span class="sxs-lookup"><span data-stu-id="2ad56-127">Finally, the code inside the `if` block instructs Windows what to do with the form after users select a day on the calendar, and then click the **OK** button or press the **Enter** key.</span></span>
<span data-ttu-id="2ad56-128">Windows PowerShell a választott dátum felhasználókat jeleníti meg.</span><span class="sxs-lookup"><span data-stu-id="2ad56-128">Windows PowerShell displays the selected date to users.</span></span>

```powershell
if ($result -eq [Windows.Forms.DialogResult]::OK) {
    $date = $calendar.SelectionStart
    Write-Host "Date selected: $($date.ToShortDateString())"
}
```

## <a name="see-also"></a><span data-ttu-id="2ad56-129">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="2ad56-129">See Also</span></span>

- [<span data-ttu-id="2ad56-130">Hey Scripting Guy:  Miért nem működnek a grafikus PowerShell-példákat?</span><span class="sxs-lookup"><span data-stu-id="2ad56-130">Hey Scripting Guy:  Why don’t these PowerShell GUI examples work?</span></span>](https://go.microsoft.com/fwlink/?LinkId=506644)
- [<span data-ttu-id="2ad56-131">GitHub: Dave Wyatt WinFormsExampleUpdates</span><span class="sxs-lookup"><span data-stu-id="2ad56-131">GitHub: Dave Wyatt's WinFormsExampleUpdates</span></span>](https://github.com/dlwyatt/WinFormsExampleUpdates)
- [<span data-ttu-id="2ad56-132">Windows PowerShell Tip of the Week:  Grafikus dátumválasztó létrehozása</span><span class="sxs-lookup"><span data-stu-id="2ad56-132">Windows PowerShell Tip of the Week:  Creating a Graphical Date Picker</span></span>](https://technet.microsoft.com/library/ff730942.aspx)