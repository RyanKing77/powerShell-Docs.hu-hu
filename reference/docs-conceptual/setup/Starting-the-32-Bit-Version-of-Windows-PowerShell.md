---
ms.date: 2017-06-05
keywords: PowerShell parancsmag
title: "A 32 bites verzióját a Windows PowerShell elindítása"
ms.assetid: 12b31890-2609-4a76-8c24-0ebe78084f50
ms.openlocfilehash: d682ce45ebc92cda3a9008ab608bacf9ef8eba57
ms.sourcegitcommit: d6ab9ab5909ed59cce4ce30e29457e0e75c7ac12
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/08/2017
---
# <a name="starting-the-32-bit-version-of-windows-powershell"></a><span data-ttu-id="770dd-103">A 32 bites Windows PowerShell elindítása</span><span class="sxs-lookup"><span data-stu-id="770dd-103">Starting the 32-Bit Version of Windows PowerShell</span></span>
<span data-ttu-id="770dd-104">Ha egy 64 bites számítógépen, telepítse a Windows PowerShell **Windows PowerShell (x86)**, egy 32 bites Windows PowerShell mellett a 64 bites verziója telepítve van.</span><span class="sxs-lookup"><span data-stu-id="770dd-104">When you install Windows PowerShell on a 64-bit computer, **Windows PowerShell (x86)**, a 32-bit version of Windows PowerShell is installed in addition to the 64-bit version.</span></span> <span data-ttu-id="770dd-105">Amikor futtatja a Windows PowerShell, a 64 bites alapértelmezés szerint fut.</span><span class="sxs-lookup"><span data-stu-id="770dd-105">When you run Windows PowerShell, the 64-bit version runs by default.</span></span>

<span data-ttu-id="770dd-106">Azonban előfordulhat, hogy időnként futtatásához szükséges **Windows PowerShell (x86)**, például egy modul használata esetén, amely 32 bites verziója szükséges hozzá, vagy ha távolról csatlakozik egy 32 bites számítógépen.</span><span class="sxs-lookup"><span data-stu-id="770dd-106">However, you might occasionally need to run **Windows PowerShell (x86)**, such as when you are using a module that requires the 32-bit version or when you are connecting remotely to a 32-bit computer.</span></span>

<span data-ttu-id="770dd-107">Egy 32 bites Windows PowerShell indításához használja az alábbi eljárások valamelyikét.</span><span class="sxs-lookup"><span data-stu-id="770dd-107">To start a 32-bit version of Windows PowerShell, use any of the following procedures.</span></span>

#### <a name="in-windows-server-2012-r2"></a><span data-ttu-id="770dd-108">A Windows Server® 2012 R2-ben</span><span class="sxs-lookup"><span data-stu-id="770dd-108">In Windows Server® 2012 R2</span></span>

- <span data-ttu-id="770dd-109">Az a **Start** írja be **Windows PowerShell (x86)**.</span><span class="sxs-lookup"><span data-stu-id="770dd-109">On the **Start** screen, type **Windows PowerShell (x86)**.</span></span> <span data-ttu-id="770dd-110">Kattintson a **Windows PowerShell x86** csempére.</span><span class="sxs-lookup"><span data-stu-id="770dd-110">Click the **Windows PowerShell x86** tile.</span></span>

- <span data-ttu-id="770dd-111">A **Kiszolgálókezelő**, az a **eszközök** menüjében válassza **Windows PowerShell (x86)**.</span><span class="sxs-lookup"><span data-stu-id="770dd-111">In **Server Manager**, from the **Tools** menu, select **Windows PowerShell (x86)**.</span></span>

- <span data-ttu-id="770dd-112">Az asztalon vigye a mutatót a jobb felső sarokban, kattintson a **keresési**, típus **PowerShell x86** majd **Windows PowerShell (x86)**.</span><span class="sxs-lookup"><span data-stu-id="770dd-112">On the desktop, move the cursor to the upper right corner, click **Search**, type **PowerShell x86** and then click **Windows PowerShell (x86)**.</span></span>

- <span data-ttu-id="770dd-113">A parancssorból írja be:`%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`</span><span class="sxs-lookup"><span data-stu-id="770dd-113">Via command line, enter: `%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`</span></span>

#### <a name="in-windows-server-2012"></a><span data-ttu-id="770dd-114">A Windows Server® 2012</span><span class="sxs-lookup"><span data-stu-id="770dd-114">In Windows Server® 2012</span></span>

- <span data-ttu-id="770dd-115">Az a **Start** írja be **PowerShell** majd **Windows PowerShell (x86)**.</span><span class="sxs-lookup"><span data-stu-id="770dd-115">On the **Start** screen, type **PowerShell** and then click **Windows PowerShell (x86)**.</span></span>

- <span data-ttu-id="770dd-116">A **Kiszolgálókezelő**, az a **eszközök** menüjében válassza **Windows PowerShell (x86)**.</span><span class="sxs-lookup"><span data-stu-id="770dd-116">In **Server Manager**, from the **Tools** menu, select **Windows PowerShell (x86)**.</span></span>

- <span data-ttu-id="770dd-117">Az asztalon vigye a mutatót a jobb felső sarokban, kattintson a **keresési**, típus **PowerShell** majd **Windows PowerShell (x86)**.</span><span class="sxs-lookup"><span data-stu-id="770dd-117">On the desktop, move the cursor to the upper right corner, click **Search**, type **PowerShell** and then click **Windows PowerShell (x86)**.</span></span>

- <span data-ttu-id="770dd-118">A parancssorból írja be:`%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`</span><span class="sxs-lookup"><span data-stu-id="770dd-118">Via command line, enter: `%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`</span></span>

#### <a name="in-windows-81"></a><span data-ttu-id="770dd-119">A Windows® 8.1</span><span class="sxs-lookup"><span data-stu-id="770dd-119">In Windows® 8.1</span></span>

- <span data-ttu-id="770dd-120">Az a **Start** írja be **Windows PowerShell (x86)**.</span><span class="sxs-lookup"><span data-stu-id="770dd-120">On the **Start** screen, type **Windows PowerShell (x86)**.</span></span> <span data-ttu-id="770dd-121">Kattintson a **Windows PowerShell x86** csempére.</span><span class="sxs-lookup"><span data-stu-id="770dd-121">Click the **Windows PowerShell x86** tile.</span></span>

- <span data-ttu-id="770dd-122">Ha futtatja [távoli kiszolgálófelügyelet eszközei](http://go.microsoft.com/fwlink/?LinkID=304145) a Windows 8.1, nyissa meg a Windows PowerShell x86 a a **Server ManagerTools** menü.</span><span class="sxs-lookup"><span data-stu-id="770dd-122">If you are running [Remote Server Administration Tools](http://go.microsoft.com/fwlink/?LinkID=304145) for Windows 8.1, you can also open Windows PowerShell x86 from the **Server ManagerTools** menu.</span></span> <span data-ttu-id="770dd-123">Válassza ki **Windows PowerShell (x86)**.</span><span class="sxs-lookup"><span data-stu-id="770dd-123">Select **Windows PowerShell (x86)**.</span></span>

- <span data-ttu-id="770dd-124">Az asztalon vigye a mutatót a jobb felső sarokban, kattintson a **keresési**, típus **PowerShell x86** majd **Windows PowerShell (x86)**.</span><span class="sxs-lookup"><span data-stu-id="770dd-124">On the desktop, move the cursor to the upper right corner, click **Search**, type **PowerShell x86** and then click **Windows PowerShell (x86)**.</span></span>
   
- <span data-ttu-id="770dd-125">A parancssorból írja be:`%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`</span><span class="sxs-lookup"><span data-stu-id="770dd-125">Via command line, enter: `%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`</span></span>

#### <a name="in-windows-8"></a><span data-ttu-id="770dd-126">A Windows® 8</span><span class="sxs-lookup"><span data-stu-id="770dd-126">In Windows® 8</span></span>

- <span data-ttu-id="770dd-127">A a **Start** képernyőn, a kurzor jobb felső sarokban, kattintson a **beállítások**, kattintson a **Csempék**, és anélkül helyezhet át a **felügyeleti eszközök megjelenítése** Igen csúszkát.</span><span class="sxs-lookup"><span data-stu-id="770dd-127">On the **Start** screen, move the cursor to the upper right corner, click **Settings**, click **Tiles**, and then move the **Show Administrative Tools** slider to Yes.</span></span> <span data-ttu-id="770dd-128">Írja be, **PowerShell** kattintson **Windows PowerShell (x86)**.</span><span class="sxs-lookup"><span data-stu-id="770dd-128">Then, type **PowerShell** and click **Windows PowerShell (x86)**.</span></span>

- <span data-ttu-id="770dd-129">Ha futtatja [távoli kiszolgálófelügyelet eszközei](http://www.microsoft.com/download/details.aspx?id=28972) a Windows 8, nyissa meg a Windows PowerShell x86 a a **Server ManagerTools** menü.</span><span class="sxs-lookup"><span data-stu-id="770dd-129">If you are running [Remote Server Administration Tools](http://www.microsoft.com/download/details.aspx?id=28972) for Windows 8, you can also open Windows PowerShell x86 from the **Server ManagerTools** menu.</span></span> <span data-ttu-id="770dd-130">Válassza ki **Windows PowerShell (x86)**.</span><span class="sxs-lookup"><span data-stu-id="770dd-130">Select **Windows PowerShell (x86)**.</span></span>

- <span data-ttu-id="770dd-131">A a **Start** képernyő vagy az asztal, írja be a **PowerShell (x86)** , majd **Windows PowerShell (x86)**.</span><span class="sxs-lookup"><span data-stu-id="770dd-131">On the **Start** screen or the desktop, type **PowerShell (x86)** and then click **Windows PowerShell (x86)**.</span></span>

- <span data-ttu-id="770dd-132">A parancssorból írja be:`%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`</span><span class="sxs-lookup"><span data-stu-id="770dd-132">Via command line, enter: `%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`</span></span>

