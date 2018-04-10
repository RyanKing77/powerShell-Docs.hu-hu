---
ms.date: 06/05/2017
keywords: PowerShell parancsmag
title: A Windows PowerShell indítása
ms.assetid: 59b649a2-c90c-4cf4-bf95-a740c59148e7
ms.openlocfilehash: b56ddc2f577225646729b99f3a2abcb8cc60d307
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="starting-windows-powershell"></a><span data-ttu-id="9fc45-103">A Windows PowerShell indítása</span><span class="sxs-lookup"><span data-stu-id="9fc45-103">Starting Windows PowerShell</span></span>
<span data-ttu-id="9fc45-104">PowerShell egy parancsfájl-kezelési motor dll, amely több gazdagép be van ágyazva.</span><span class="sxs-lookup"><span data-stu-id="9fc45-104">PowerShell is a scripting engine dll which is embedded into multiple hosts.</span></span>  <span data-ttu-id="9fc45-105">A leggyakrabban használt állomás hozzákezdhet a következők: interaktív parancssori PowerShell.exe és parancsfájl-kezelési környezet interaktív PowerShell_ISE.exe.</span><span class="sxs-lookup"><span data-stu-id="9fc45-105">The most common host you will start are the interactive command line PowerShell.exe and the Interactive Scripting Environment PowerShell_ISE.exe.</span></span>

<span data-ttu-id="9fc45-106">A Windows Server® 2012 R2, Windows® 8.1, Windows Server 2012 és Windows 8 Windows PowerShell® elindításához lásd: [általános kezelési feladatok és navigáció](http://technet.microsoft.com/library/hh831491.aspx).</span><span class="sxs-lookup"><span data-stu-id="9fc45-106">To start Windows PowerShell® on Windows Server® 2012 R2, Windows® 8.1, Windows Server 2012, and Windows 8, see [Common Management Tasks and Navigation](http://technet.microsoft.com/library/hh831491.aspx).</span></span>

## <a name="how-to-start-windows-powershell-on-earlier-versions-of-windows"></a><span data-ttu-id="9fc45-107">A Windows korábbi verzióiban Windows PowerShell indítása</span><span class="sxs-lookup"><span data-stu-id="9fc45-107">How to Start Windows PowerShell on Earlier Versions of Windows</span></span>

<span data-ttu-id="9fc45-108">Ez a szakasz ismerteti, hogyan kell elindítani a Windows PowerShell és a Windows PowerShell integrált parancsfájlkezelési környezet (ISE) a Windows® 7, Windows Server® 2008 R2 és Windows Server® 2008.</span><span class="sxs-lookup"><span data-stu-id="9fc45-108">This section explains how to start Windows PowerShell and Windows PowerShell Integrated Scripting Environment (ISE) on Windows® 7, Windows Server® 2008 R2, and Windows Server® 2008.</span></span> <span data-ttu-id="9fc45-109">A választható szolgáltatás engedélyezése a Windows PowerShell 2.0 a Windows Server® 2008 R2 és Windows Server® 2008 a Windows PowerShell ISE is ismerteti.</span><span class="sxs-lookup"><span data-stu-id="9fc45-109">It also explains how to enable the optional feature for Windows PowerShell ISE in Windows PowerShell 2.0 on Windows Server® 2008 R2 and Windows Server® 2008.</span></span>

<span data-ttu-id="9fc45-110">A következő módszerekkel segítségével adott esetben indítsa el a Windows PowerShell 3.0 vagy a Windows PowerShell 4.0-s verzióját.</span><span class="sxs-lookup"><span data-stu-id="9fc45-110">Use any of the following methods to start the installed version of Windows PowerShell 3.0, or Windows PowerShell 4.0, where applicable.</span></span>

#### <a name="from-the-start-menu"></a><span data-ttu-id="9fc45-111">A Start menüből</span><span class="sxs-lookup"><span data-stu-id="9fc45-111">From the Start Menu</span></span>

- <span data-ttu-id="9fc45-112">Kattintson a **Start**, típus **PowerShell**, és kattintson a **Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="9fc45-112">Click **Start**, type **PowerShell**, and then click **Windows PowerShell**.</span></span>
- <span data-ttu-id="9fc45-113">A a **Start** menüben kattintson **Start**, kattintson **minden program**, kattintson a **Kellékek**, kattintson a **Windows PowerShell**  mappa, és kattintson **Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="9fc45-113">From the **Start** menu, click **Start**, click **All Programs**, click **Accessories**, click the **Windows PowerShell** folder, and then click **Windows PowerShell**.</span></span>

#### <a name="at-the-command-prompt"></a><span data-ttu-id="9fc45-114">A parancssorba</span><span class="sxs-lookup"><span data-stu-id="9fc45-114">At the Command Prompt</span></span>

<span data-ttu-id="9fc45-115">A Cmd.exe, a Windows PowerShell vagy a Windows PowerShell ISE indítsa el a Windows Powershellt, írja be:</span><span class="sxs-lookup"><span data-stu-id="9fc45-115">In Cmd.exe, Windows PowerShell, or Windows PowerShell ISE, to start Windows PowerShell, type:</span></span>

```
PowerShell
```

<span data-ttu-id="9fc45-116">A paraméterek a PowerShell.exe program segítségével testre szabhatja a munkamenet.</span><span class="sxs-lookup"><span data-stu-id="9fc45-116">You can also use the parameters of the PowerShell.exe program to customize the session.</span></span> <span data-ttu-id="9fc45-117">További információkért lásd: [PowerShell.exe parancssori súgó](../core-powershell/console/PowerShell.exe-Command-Line-Help.md).</span><span class="sxs-lookup"><span data-stu-id="9fc45-117">For more information, see [PowerShell.exe Command-Line Help](../core-powershell/console/PowerShell.exe-Command-Line-Help.md).</span></span>

#### <a name="with-administrative-privileges-run-as-administrator"></a><span data-ttu-id="9fc45-118">A felügyeleti jogosultságok ("Futtatás rendszergazdaként")</span><span class="sxs-lookup"><span data-stu-id="9fc45-118">With Administrative privileges ("Run as administrator")</span></span>

<span data-ttu-id="9fc45-119">Kattintson a **Start**, típus **PowerShell**, kattintson a jobb gombbal **Windows PowerShell**, és kattintson a **Futtatás rendszergazdaként**.</span><span class="sxs-lookup"><span data-stu-id="9fc45-119">Click **Start**, type **PowerShell**, right-click **Windows PowerShell**, and then click **Run as administrator**.</span></span>

## <a name="how-to-start-windows-powershell-ise-on-earlier-releases-of-windows"></a><span data-ttu-id="9fc45-120">A Windows PowerShell ISE indítása a Windows operációs rendszerek régebbi kiadásaiban</span><span class="sxs-lookup"><span data-stu-id="9fc45-120">How to Start Windows PowerShell ISE on Earlier Releases of Windows</span></span>

<span data-ttu-id="9fc45-121">A Windows PowerShell ISE elindításához használja a következő módszerekkel.</span><span class="sxs-lookup"><span data-stu-id="9fc45-121">Use any of the following methods to start Windows PowerShell ISE.</span></span>

#### <a name="from-the-start-menu"></a><span data-ttu-id="9fc45-122">A Start menüből</span><span class="sxs-lookup"><span data-stu-id="9fc45-122">From the Start Menu</span></span>

- <span data-ttu-id="9fc45-123">Kattintson a **Start**, típus **ISE**, és kattintson a **Windows PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="9fc45-123">Click **Start**, type **ISE**, and then click **Windows PowerShell ISE**.</span></span>
- <span data-ttu-id="9fc45-124">A a **Start** menüben kattintson **Start**, kattintson **minden program**, kattintson a **Kellékek**, kattintson a **Windows PowerShell**  mappa, és kattintson **Windows PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="9fc45-124">From the **Start** menu, click **Start**, click **All Programs**, click **Accessories**, click the **Windows PowerShell** folder, and then click **Windows PowerShell ISE**.</span></span>

#### <a name="at-the-command-prompt"></a><span data-ttu-id="9fc45-125">A parancssorba</span><span class="sxs-lookup"><span data-stu-id="9fc45-125">At the Command Prompt</span></span>

<span data-ttu-id="9fc45-126">A Cmd.exe, a Windows PowerShell vagy a Windows PowerShell ISE indítsa el a Windows Powershellt, írja be:</span><span class="sxs-lookup"><span data-stu-id="9fc45-126">In Cmd.exe, Windows PowerShell, or Windows PowerShell ISE, to start Windows PowerShell, type:</span></span>

```
PowerShell_ISE
```

<span data-ttu-id="9fc45-127">vagy a</span><span class="sxs-lookup"><span data-stu-id="9fc45-127">or</span></span>

```
ISE
```

#### <a name="with-administrative-privileges-run-as-administrator"></a><span data-ttu-id="9fc45-128">A felügyeleti jogosultságok ("Futtatás rendszergazdaként")</span><span class="sxs-lookup"><span data-stu-id="9fc45-128">With Administrative privileges ("Run as administrator")</span></span>

<span data-ttu-id="9fc45-129">Kattintson a **Start**, típus **ISE**, kattintson a jobb gombbal **Windows PowerShell ISE**, és kattintson a **Futtatás rendszergazdaként**.</span><span class="sxs-lookup"><span data-stu-id="9fc45-129">Click **Start**, type **ISE**, right-click **Windows PowerShell ISE**, and then click **Run as administrator**.</span></span>

## <a name="how-to-enable-windows-powershell-ise-on-earlier-releases-of-windows"></a><span data-ttu-id="9fc45-130">A Windows korábbi verzióiban Windows PowerShell ISE engedélyezése</span><span class="sxs-lookup"><span data-stu-id="9fc45-130">How to Enable Windows PowerShell ISE on Earlier Releases of Windows</span></span>

<span data-ttu-id="9fc45-131">A Windows PowerShell 4.0-s verzióját és a Windows PowerShell 3.0, a Windows PowerShell ISE alapértelmezés szerint engedélyezve van a Windows összes verzióján.</span><span class="sxs-lookup"><span data-stu-id="9fc45-131">In Windows PowerShell 4.0 and Windows PowerShell 3.0, Windows PowerShell ISE is enabled by default on all versions of Windows.</span></span> <span data-ttu-id="9fc45-132">Ha már nincs engedélyezve, a Windows Management Framework 4.0 vagy a Windows Management Framework 3.0 engedélyezi.</span><span class="sxs-lookup"><span data-stu-id="9fc45-132">If it is not already enabled, Windows Management Framework 4.0 or Windows Management Framework 3.0 enables it.</span></span>

<span data-ttu-id="9fc45-133">A Windows PowerShell 2.0 a Windows PowerShell ISE alapértelmezés szerint engedélyezve van a Windows 7.</span><span class="sxs-lookup"><span data-stu-id="9fc45-133">In Windows PowerShell 2.0, Windows PowerShell ISE is enabled by default on Windows 7.</span></span> <span data-ttu-id="9fc45-134">Azonban a Windows Server 2008 R2 és Windows Server 2008, akkor választható lehetőség.</span><span class="sxs-lookup"><span data-stu-id="9fc45-134">However, on Windows Server 2008 R2 and Windows Server 2008, it is an optional feature.</span></span>

<span data-ttu-id="9fc45-135">Ahhoz, hogy a Windows PowerShell ISE a Windows PowerShell 2.0 a Windows Server 2008 R2 vagy Windows Server 2008, a következő eljárással.</span><span class="sxs-lookup"><span data-stu-id="9fc45-135">To enable Windows PowerShell ISE in Windows PowerShell 2.0 on Windows Server 2008 R2 or Windows Server 2008, use the following procedure.</span></span>

#### <a name="to-enable-windows-powershell-integrated-scripting-environment-ise"></a><span data-ttu-id="9fc45-136">Ahhoz, hogy a Windows PowerShell integrált parancsfájl-kezelési környezet (ISE)</span><span class="sxs-lookup"><span data-stu-id="9fc45-136">To enable Windows PowerShell Integrated Scripting Environment (ISE)</span></span>

1. <span data-ttu-id="9fc45-137">Indítsa el a Kiszolgálókezelőt.</span><span class="sxs-lookup"><span data-stu-id="9fc45-137">Start Server Manager.</span></span>
2. <span data-ttu-id="9fc45-138">Kattintson a **szolgáltatások** majd **szolgáltatások hozzáadása**.</span><span class="sxs-lookup"><span data-stu-id="9fc45-138">Click **Features** and then click **Add Features**.</span></span>
3. <span data-ttu-id="9fc45-139">A szolgáltatások kiválasztása párbeszédpanelen kattintson a Windows PowerShell integrált parancsfájlkezelési környezet (ISE).</span><span class="sxs-lookup"><span data-stu-id="9fc45-139">In Select Features, click Windows PowerShell Integrated Scripting Environment (ISE).</span></span>

## <a name="starting-the-32-bit-version-of-windows-powershell"></a><span data-ttu-id="9fc45-140">A 32 bites Windows PowerShell elindítása</span><span class="sxs-lookup"><span data-stu-id="9fc45-140">Starting the 32-Bit Version of Windows PowerShell</span></span>

<span data-ttu-id="9fc45-141">Ha egy 64 bites számítógépen, telepítse a Windows PowerShell **Windows PowerShell (x86)**, egy 32 bites Windows PowerShell mellett a 64 bites verziója telepítve van.</span><span class="sxs-lookup"><span data-stu-id="9fc45-141">When you install Windows PowerShell on a 64-bit computer, **Windows PowerShell (x86)**, a 32-bit version of Windows PowerShell is installed in addition to the 64-bit version.</span></span> <span data-ttu-id="9fc45-142">Amikor futtatja a Windows PowerShell, a 64 bites alapértelmezés szerint fut.</span><span class="sxs-lookup"><span data-stu-id="9fc45-142">When you run Windows PowerShell, the 64-bit version runs by default.</span></span>

<span data-ttu-id="9fc45-143">Azonban előfordulhat, hogy időnként futtatásához szükséges **Windows PowerShell (x86)**, például egy modul használata esetén, amely 32 bites verziója szükséges hozzá, vagy ha távolról csatlakozik egy 32 bites számítógépen.</span><span class="sxs-lookup"><span data-stu-id="9fc45-143">However, you might occasionally need to run **Windows PowerShell (x86)**, such as when you are using a module that requires the 32-bit version or when you are connecting remotely to a 32-bit computer.</span></span>

<span data-ttu-id="9fc45-144">Egy 32 bites Windows PowerShell indításához használja az alábbi eljárások valamelyikét.</span><span class="sxs-lookup"><span data-stu-id="9fc45-144">To start a 32-bit version of Windows PowerShell, use any of the following procedures.</span></span>

#### <a name="in-windows-server-2012-r2"></a><span data-ttu-id="9fc45-145">In Windows Server® 2012 R2</span><span class="sxs-lookup"><span data-stu-id="9fc45-145">In Windows Server® 2012 R2</span></span>

- <span data-ttu-id="9fc45-146">Az a **Start** írja be **Windows PowerShell (x86)**.</span><span class="sxs-lookup"><span data-stu-id="9fc45-146">On the **Start** screen, type **Windows PowerShell (x86)**.</span></span> <span data-ttu-id="9fc45-147">Kattintson a **Windows PowerShell x86** csempére.</span><span class="sxs-lookup"><span data-stu-id="9fc45-147">Click the **Windows PowerShell x86** tile.</span></span>
- <span data-ttu-id="9fc45-148">A **Kiszolgálókezelő**, az a **eszközök** menüjében válassza **Windows PowerShell (x86)**.</span><span class="sxs-lookup"><span data-stu-id="9fc45-148">In **Server Manager**, from the **Tools** menu, select **Windows PowerShell (x86)**.</span></span>
- <span data-ttu-id="9fc45-149">Az asztalon vigye a mutatót a jobb felső sarokban, kattintson a **keresési**, típus **PowerShell x86** majd **Windows PowerShell (x86)**.</span><span class="sxs-lookup"><span data-stu-id="9fc45-149">On the desktop, move the cursor to the upper right corner, click **Search**, type **PowerShell x86** and then click **Windows PowerShell (x86)**.</span></span>
- <span data-ttu-id="9fc45-150">A parancssorból írja be: `%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`</span><span class="sxs-lookup"><span data-stu-id="9fc45-150">Via command line, enter: `%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`</span></span>

#### <a name="in-windows-server-2012"></a><span data-ttu-id="9fc45-151">In Windows Server® 2012</span><span class="sxs-lookup"><span data-stu-id="9fc45-151">In Windows Server® 2012</span></span>

- <span data-ttu-id="9fc45-152">Az a **Start** írja be **PowerShell** majd **Windows PowerShell (x86)**.</span><span class="sxs-lookup"><span data-stu-id="9fc45-152">On the **Start** screen, type **PowerShell** and then click **Windows PowerShell (x86)**.</span></span>
- <span data-ttu-id="9fc45-153">A **Kiszolgálókezelő**, az a **eszközök** menüjében válassza **Windows PowerShell (x86)**.</span><span class="sxs-lookup"><span data-stu-id="9fc45-153">In **Server Manager**, from the **Tools** menu, select **Windows PowerShell (x86)**.</span></span>
- <span data-ttu-id="9fc45-154">Az asztalon vigye a mutatót a jobb felső sarokban, kattintson a **keresési**, típus **PowerShell** majd **Windows PowerShell (x86)**.</span><span class="sxs-lookup"><span data-stu-id="9fc45-154">On the desktop, move the cursor to the upper right corner, click **Search**, type **PowerShell** and then click **Windows PowerShell (x86)**.</span></span>
- <span data-ttu-id="9fc45-155">A parancssorból írja be: `%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`</span><span class="sxs-lookup"><span data-stu-id="9fc45-155">Via command line, enter: `%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`</span></span>

#### <a name="in-windows-81"></a><span data-ttu-id="9fc45-156">A Windows® 8.1</span><span class="sxs-lookup"><span data-stu-id="9fc45-156">In Windows® 8.1</span></span>

- <span data-ttu-id="9fc45-157">Az a **Start** írja be **Windows PowerShell (x86)**.</span><span class="sxs-lookup"><span data-stu-id="9fc45-157">On the **Start** screen, type **Windows PowerShell (x86)**.</span></span> <span data-ttu-id="9fc45-158">Kattintson a **Windows PowerShell x86** csempére.</span><span class="sxs-lookup"><span data-stu-id="9fc45-158">Click the **Windows PowerShell x86** tile.</span></span>
- <span data-ttu-id="9fc45-159">Ha futtatja [távoli kiszolgálófelügyelet eszközei](http://go.microsoft.com/fwlink/?LinkID=304145) a Windows 8.1, nyissa meg a Windows PowerShell x86 a a **Server ManagerTools** menü.</span><span class="sxs-lookup"><span data-stu-id="9fc45-159">If you are running [Remote Server Administration Tools](http://go.microsoft.com/fwlink/?LinkID=304145) for Windows 8.1, you can also open Windows PowerShell x86 from the **Server ManagerTools** menu.</span></span>
  <span data-ttu-id="9fc45-160">Válassza ki **Windows PowerShell (x86)**.</span><span class="sxs-lookup"><span data-stu-id="9fc45-160">Select **Windows PowerShell (x86)**.</span></span>
- <span data-ttu-id="9fc45-161">Az asztalon vigye a mutatót a jobb felső sarokban, kattintson a **keresési**, típus **PowerShell x86** majd **Windows PowerShell (x86)**.</span><span class="sxs-lookup"><span data-stu-id="9fc45-161">On the desktop, move the cursor to the upper right corner, click **Search**, type **PowerShell x86** and then click **Windows PowerShell (x86)**.</span></span>
- <span data-ttu-id="9fc45-162">A parancssorból írja be: `%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`</span><span class="sxs-lookup"><span data-stu-id="9fc45-162">Via command line, enter: `%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`</span></span>

#### <a name="in-windows-8"></a><span data-ttu-id="9fc45-163">In Windows® 8</span><span class="sxs-lookup"><span data-stu-id="9fc45-163">In Windows® 8</span></span>

- <span data-ttu-id="9fc45-164">A a **Start** képernyőn, a kurzor jobb felső sarokban, kattintson a **beállítások**, kattintson a **Csempék**, és anélkül helyezhet át a **felügyeleti eszközök megjelenítése** Igen csúszkát.</span><span class="sxs-lookup"><span data-stu-id="9fc45-164">On the **Start** screen, move the cursor to the upper right corner, click **Settings**, click **Tiles**, and then move the **Show Administrative Tools** slider to Yes.</span></span> <span data-ttu-id="9fc45-165">Írja be, **PowerShell** kattintson **Windows PowerShell (x86)**.</span><span class="sxs-lookup"><span data-stu-id="9fc45-165">Then, type **PowerShell** and click **Windows PowerShell (x86)**.</span></span>
- <span data-ttu-id="9fc45-166">Ha futtatja [távoli kiszolgálófelügyelet eszközei](http://www.microsoft.com/download/details.aspx?id=28972) a Windows 8, nyissa meg a Windows PowerShell x86 a a **Server ManagerTools** menü.</span><span class="sxs-lookup"><span data-stu-id="9fc45-166">If you are running [Remote Server Administration Tools](http://www.microsoft.com/download/details.aspx?id=28972) for Windows 8, you can also open Windows PowerShell x86 from the **Server ManagerTools** menu.</span></span> <span data-ttu-id="9fc45-167">Válassza ki **Windows PowerShell (x86)**.</span><span class="sxs-lookup"><span data-stu-id="9fc45-167">Select **Windows PowerShell (x86)**.</span></span>
- <span data-ttu-id="9fc45-168">A a **Start** képernyő vagy az asztal, írja be a **PowerShell (x86)** , majd **Windows PowerShell (x86)**.</span><span class="sxs-lookup"><span data-stu-id="9fc45-168">On the **Start** screen or the desktop, type **PowerShell (x86)** and then click **Windows PowerShell (x86)**.</span></span>
- <span data-ttu-id="9fc45-169">A parancssorból írja be: `%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`</span><span class="sxs-lookup"><span data-stu-id="9fc45-169">Via command line, enter: `%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`</span></span>