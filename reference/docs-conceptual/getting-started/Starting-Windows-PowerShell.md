---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: A Windows PowerShell indítása
ms.openlocfilehash: d2cb77027f404c5b008a902c5147d018dd741a67
ms.sourcegitcommit: a6f13c16a535acea279c0ddeca72f1f0d8a8ce4c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2019
ms.locfileid: "67030457"
---
# <a name="starting-windows-powershell"></a><span data-ttu-id="b33f6-103">A Windows PowerShell indítása</span><span class="sxs-lookup"><span data-stu-id="b33f6-103">Starting Windows PowerShell</span></span>
<span data-ttu-id="b33f6-104">PowerShell parancsfájl-kezelési motor dll, amely több gazdagép be lesz ágyazva az.</span><span class="sxs-lookup"><span data-stu-id="b33f6-104">PowerShell is a scripting engine dll which is embedded into multiple hosts.</span></span>  <span data-ttu-id="b33f6-105">A leggyakoribb gazdagépet meg fogja kezdeni a következők: interaktív a PowerShell.exe parancssori és az interaktív parancsfájl-kezelési környezet PowerShell_ISE.exe.</span><span class="sxs-lookup"><span data-stu-id="b33f6-105">The most common host you will start are the interactive command line PowerShell.exe and the Interactive Scripting Environment PowerShell_ISE.exe.</span></span>

<span data-ttu-id="b33f6-106">A Windows Server® 2012 R2, Windows® 8.1, Windows Server 2012 és Windows 8 Windows PowerShell® indításához lásd: [általános felügyeleti feladatok és navigáció](https://technet.microsoft.com/library/hh831491.aspx).</span><span class="sxs-lookup"><span data-stu-id="b33f6-106">To start Windows PowerShell® on Windows Server® 2012 R2, Windows® 8.1, Windows Server 2012, and Windows 8, see [Common Management Tasks and Navigation](https://technet.microsoft.com/library/hh831491.aspx).</span></span>

## <a name="how-to-start-windows-powershell-on-earlier-versions-of-windows"></a><span data-ttu-id="b33f6-107">Windows PowerShell indítása a Windows korábbi verzióin</span><span class="sxs-lookup"><span data-stu-id="b33f6-107">How to Start Windows PowerShell on Earlier Versions of Windows</span></span>

<span data-ttu-id="b33f6-108">Ez a szakasz ismerteti a Windows PowerShell és a Windows PowerShell integrált parancsfájl-kezelési környezet (ISE) indítása a Windows® 7, Windows Server® 2008 R2 és Windows Server® 2008.</span><span class="sxs-lookup"><span data-stu-id="b33f6-108">This section explains how to start Windows PowerShell and Windows PowerShell Integrated Scripting Environment (ISE) on Windows® 7, Windows Server® 2008 R2, and Windows Server® 2008.</span></span> <span data-ttu-id="b33f6-109">Azt is bemutatja, hogyan engedélyezhető a választható szolgáltatás Windows PowerShell ISE-ben a Windows PowerShell 2.0 a Windows Server® 2008 R2 és Windows Server® 2008.</span><span class="sxs-lookup"><span data-stu-id="b33f6-109">It also explains how to enable the optional feature for Windows PowerShell ISE in Windows PowerShell 2.0 on Windows Server® 2008 R2 and Windows Server® 2008.</span></span>

<span data-ttu-id="b33f6-110">Az alábbi módszerek bármelyikét használatával indítsa el a Windows PowerShell 3.0 vagy a Windows PowerShell 4.0-s verzióját, ha vannak ilyenek.</span><span class="sxs-lookup"><span data-stu-id="b33f6-110">Use any of the following methods to start the installed version of Windows PowerShell 3.0, or Windows PowerShell 4.0, where applicable.</span></span>

#### <a name="from-the-start-menu"></a><span data-ttu-id="b33f6-111">A Start menüből</span><span class="sxs-lookup"><span data-stu-id="b33f6-111">From the Start Menu</span></span>

- <span data-ttu-id="b33f6-112">Kattintson a **Start**, típus **PowerShell**, és kattintson a **Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="b33f6-112">Click **Start**, type **PowerShell**, and then click **Windows PowerShell**.</span></span>
- <span data-ttu-id="b33f6-113">A a **Start** menüben kattintson **Start**, kattintson a **minden program**, kattintson a **Kellékek**, kattintson a **Windows PowerShell**  mappát, és kattintson **Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="b33f6-113">From the **Start** menu, click **Start**, click **All Programs**, click **Accessories**, click the **Windows PowerShell** folder, and then click **Windows PowerShell**.</span></span>

#### <a name="at-the-command-prompt"></a><span data-ttu-id="b33f6-114">A parancssorban</span><span class="sxs-lookup"><span data-stu-id="b33f6-114">At the Command Prompt</span></span>

<span data-ttu-id="b33f6-115">A Cmd.exe, a Windows PowerShell vagy a Windows PowerShell ISE-t indítsa el a Windows Powershellt, írja be:</span><span class="sxs-lookup"><span data-stu-id="b33f6-115">In Cmd.exe, Windows PowerShell, or Windows PowerShell ISE, to start Windows PowerShell, type:</span></span>

```
PowerShell
```

<span data-ttu-id="b33f6-116">A paraméterek a PowerShell.exe program segítségével testre szabhatja a munkamenetet.</span><span class="sxs-lookup"><span data-stu-id="b33f6-116">You can also use the parameters of the PowerShell.exe program to customize the session.</span></span> <span data-ttu-id="b33f6-117">További információkért lásd: [PowerShell.exe parancssori súgója](../core-powershell/console/PowerShell.exe-Command-Line-Help.md).</span><span class="sxs-lookup"><span data-stu-id="b33f6-117">For more information, see [PowerShell.exe Command-Line Help](../core-powershell/console/PowerShell.exe-Command-Line-Help.md).</span></span>

#### <a name="with-administrative-privileges-run-as-administrator"></a><span data-ttu-id="b33f6-118">A felügyeleti jogosultságok ("Futtatás rendszergazdaként")</span><span class="sxs-lookup"><span data-stu-id="b33f6-118">With Administrative privileges ("Run as administrator")</span></span>

<span data-ttu-id="b33f6-119">Kattintson a **Start**, típus **PowerShell**, kattintson a jobb gombbal **Windows PowerShell**, és kattintson a **Futtatás rendszergazdaként**.</span><span class="sxs-lookup"><span data-stu-id="b33f6-119">Click **Start**, type **PowerShell**, right-click **Windows PowerShell**, and then click **Run as administrator**.</span></span>

## <a name="how-to-start-windows-powershell-ise-on-earlier-releases-of-windows"></a><span data-ttu-id="b33f6-120">A Windows korábbi verzióiban elindítása a Windows PowerShell ISE-ben</span><span class="sxs-lookup"><span data-stu-id="b33f6-120">How to Start Windows PowerShell ISE on Earlier Releases of Windows</span></span>

<span data-ttu-id="b33f6-121">Az alábbi módszerek bármelyikét használatával indítsa el a Windows PowerShell ISE-ben.</span><span class="sxs-lookup"><span data-stu-id="b33f6-121">Use any of the following methods to start Windows PowerShell ISE.</span></span>

#### <a name="from-the-start-menu"></a><span data-ttu-id="b33f6-122">A Start menüből</span><span class="sxs-lookup"><span data-stu-id="b33f6-122">From the Start Menu</span></span>

- <span data-ttu-id="b33f6-123">Kattintson a **Start**, típus **ISE**, és kattintson a **Windows PowerShell ISE-ben**.</span><span class="sxs-lookup"><span data-stu-id="b33f6-123">Click **Start**, type **ISE**, and then click **Windows PowerShell ISE**.</span></span>
- <span data-ttu-id="b33f6-124">A a **Start** menüben kattintson **Start**, kattintson a **minden program**, kattintson a **Kellékek**, kattintson a **Windows PowerShell**  mappát, és kattintson **Windows PowerShell ISE-ben**.</span><span class="sxs-lookup"><span data-stu-id="b33f6-124">From the **Start** menu, click **Start**, click **All Programs**, click **Accessories**, click the **Windows PowerShell** folder, and then click **Windows PowerShell ISE**.</span></span>

#### <a name="at-the-command-prompt"></a><span data-ttu-id="b33f6-125">A parancssorban</span><span class="sxs-lookup"><span data-stu-id="b33f6-125">At the Command Prompt</span></span>

<span data-ttu-id="b33f6-126">A Cmd.exe, a Windows PowerShell vagy a Windows PowerShell ISE-t indítsa el a Windows Powershellt, írja be:</span><span class="sxs-lookup"><span data-stu-id="b33f6-126">In Cmd.exe, Windows PowerShell, or Windows PowerShell ISE, to start Windows PowerShell, type:</span></span>

```
PowerShell_ISE
```

<span data-ttu-id="b33f6-127">vagy a</span><span class="sxs-lookup"><span data-stu-id="b33f6-127">or</span></span>

```
ISE
```

#### <a name="with-administrative-privileges-run-as-administrator"></a><span data-ttu-id="b33f6-128">A felügyeleti jogosultságok ("Futtatás rendszergazdaként")</span><span class="sxs-lookup"><span data-stu-id="b33f6-128">With Administrative privileges ("Run as administrator")</span></span>

<span data-ttu-id="b33f6-129">Kattintson a **Start**, típus **ISE**, kattintson a jobb gombbal **Windows PowerShell ISE-ben**, és kattintson a **Futtatás rendszergazdaként**.</span><span class="sxs-lookup"><span data-stu-id="b33f6-129">Click **Start**, type **ISE**, right-click **Windows PowerShell ISE**, and then click **Run as administrator**.</span></span>

## <a name="how-to-enable-windows-powershell-ise-on-earlier-releases-of-windows"></a><span data-ttu-id="b33f6-130">Windows PowerShell ISE-ben a Windows korábbi verzióiban engedélyezése</span><span class="sxs-lookup"><span data-stu-id="b33f6-130">How to Enable Windows PowerShell ISE on Earlier Releases of Windows</span></span>

<span data-ttu-id="b33f6-131">A Windows PowerShell 4.0-s és a Windows PowerShell 3.0-s Windows PowerShell ISE-ben alapértelmezés szerint engedélyezve van Windows összes verzióján.</span><span class="sxs-lookup"><span data-stu-id="b33f6-131">In Windows PowerShell 4.0 and Windows PowerShell 3.0, Windows PowerShell ISE is enabled by default on all versions of Windows.</span></span> <span data-ttu-id="b33f6-132">Ha ez nem engedélyezett, Windows Management Framework 4.0 vagy a Windows Management Framework 3.0 lehetővé teszi, hogy azt.</span><span class="sxs-lookup"><span data-stu-id="b33f6-132">If it is not already enabled, Windows Management Framework 4.0 or Windows Management Framework 3.0 enables it.</span></span>

<span data-ttu-id="b33f6-133">A Windows PowerShell 2.0, Windows PowerShell ISE-ben alapértelmezés szerint engedélyezve van a Windows 7.</span><span class="sxs-lookup"><span data-stu-id="b33f6-133">In Windows PowerShell 2.0, Windows PowerShell ISE is enabled by default on Windows 7.</span></span> <span data-ttu-id="b33f6-134">Azonban a Windows Server 2008 R2 és Windows Server 2008, egy nem kötelező funkciót.</span><span class="sxs-lookup"><span data-stu-id="b33f6-134">However, on Windows Server 2008 R2 and Windows Server 2008, it is an optional feature.</span></span>

<span data-ttu-id="b33f6-135">Ahhoz, hogy a Windows PowerShell ISE-ben a Windows PowerShell 2.0 a Windows Server 2008 R2 vagy Windows Server 2008, az alábbi eljárással.</span><span class="sxs-lookup"><span data-stu-id="b33f6-135">To enable Windows PowerShell ISE in Windows PowerShell 2.0 on Windows Server 2008 R2 or Windows Server 2008, use the following procedure.</span></span>

#### <a name="to-enable-windows-powershell-integrated-scripting-environment-ise"></a><span data-ttu-id="b33f6-136">Windows PowerShell integrált parancsfájl-kezelési környezet (ISE) engedélyezése</span><span class="sxs-lookup"><span data-stu-id="b33f6-136">To enable Windows PowerShell Integrated Scripting Environment (ISE)</span></span>

1. <span data-ttu-id="b33f6-137">Indítsa el a Kiszolgálókezelőt.</span><span class="sxs-lookup"><span data-stu-id="b33f6-137">Start Server Manager.</span></span>
2. <span data-ttu-id="b33f6-138">Kattintson a **funkciók** majd **szolgáltatások hozzáadása**.</span><span class="sxs-lookup"><span data-stu-id="b33f6-138">Click **Features** and then click **Add Features**.</span></span>
3. <span data-ttu-id="b33f6-139">A szolgáltatások kiválasztása párbeszédpanelen kattintson a Windows PowerShell integrált parancsfájl-kezelési környezet (ISE).</span><span class="sxs-lookup"><span data-stu-id="b33f6-139">In Select Features, click Windows PowerShell Integrated Scripting Environment (ISE).</span></span>

## <a name="starting-the-32-bit-version-of-windows-powershell"></a><span data-ttu-id="b33f6-140">A Windows PowerShell 32 bites verziójának indítása</span><span class="sxs-lookup"><span data-stu-id="b33f6-140">Starting the 32-Bit Version of Windows PowerShell</span></span>

<span data-ttu-id="b33f6-141">Ha egy 64 bites számítógépen Windows PowerShell telepítése **Windows PowerShell (x86)** , egy Windows PowerShell 32 bites verziója van telepítve, mellett a 64 bites verziót.</span><span class="sxs-lookup"><span data-stu-id="b33f6-141">When you install Windows PowerShell on a 64-bit computer, **Windows PowerShell (x86)**, a 32-bit version of Windows PowerShell is installed in addition to the 64-bit version.</span></span> <span data-ttu-id="b33f6-142">Amikor futtatja a Windows PowerShell, a 64 bites verziót futtatja, alapértelmezés szerint.</span><span class="sxs-lookup"><span data-stu-id="b33f6-142">When you run Windows PowerShell, the 64-bit version runs by default.</span></span>

<span data-ttu-id="b33f6-143">Azonban néha szüksége lehet futtatni **Windows PowerShell (x86)** , például a modul használata esetén, amelyek 32 bites verzióját igényli, vagy ha távolról csatlakozik egy 32 bites számítógépen.</span><span class="sxs-lookup"><span data-stu-id="b33f6-143">However, you might occasionally need to run **Windows PowerShell (x86)**, such as when you are using a module that requires the 32-bit version or when you are connecting remotely to a 32-bit computer.</span></span>

<span data-ttu-id="b33f6-144">Egy Windows PowerShell 32 bites verziójának indítása, használja az alábbi eljárások valamelyikét.</span><span class="sxs-lookup"><span data-stu-id="b33f6-144">To start a 32-bit version of Windows PowerShell, use any of the following procedures.</span></span>

#### <a name="in-windows-server-2012-r2"></a><span data-ttu-id="b33f6-145">A Windows Server® 2012 R2-ben</span><span class="sxs-lookup"><span data-stu-id="b33f6-145">In Windows Server® 2012 R2</span></span>

- <span data-ttu-id="b33f6-146">Az a **Start** írja be **Windows PowerShell (x86)** .</span><span class="sxs-lookup"><span data-stu-id="b33f6-146">On the **Start** screen, type **Windows PowerShell (x86)**.</span></span> <span data-ttu-id="b33f6-147">Kattintson a **Windows PowerShell x86** csempére.</span><span class="sxs-lookup"><span data-stu-id="b33f6-147">Click the **Windows PowerShell x86** tile.</span></span>
- <span data-ttu-id="b33f6-148">A **Kiszolgálókezelő**, az a **eszközök** menüjében válassza **Windows PowerShell (x86)** .</span><span class="sxs-lookup"><span data-stu-id="b33f6-148">In **Server Manager**, from the **Tools** menu, select **Windows PowerShell (x86)**.</span></span>
- <span data-ttu-id="b33f6-149">Az asztalon vigye a kurzort a jobb felső sarokban, kattintson **keresési**, típus **PowerShell x86** majd **Windows PowerShell (x86)** .</span><span class="sxs-lookup"><span data-stu-id="b33f6-149">On the desktop, move the cursor to the upper right corner, click **Search**, type **PowerShell x86** and then click **Windows PowerShell (x86)**.</span></span>
- <span data-ttu-id="b33f6-150">A parancssorban adja meg: `%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`</span><span class="sxs-lookup"><span data-stu-id="b33f6-150">Via command line, enter: `%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`</span></span>

#### <a name="in-windows-server-2012"></a><span data-ttu-id="b33f6-151">In Windows Server® 2012</span><span class="sxs-lookup"><span data-stu-id="b33f6-151">In Windows Server® 2012</span></span>

- <span data-ttu-id="b33f6-152">Az a **Start** írja be **PowerShell** majd **Windows PowerShell (x86)** .</span><span class="sxs-lookup"><span data-stu-id="b33f6-152">On the **Start** screen, type **PowerShell** and then click **Windows PowerShell (x86)**.</span></span>
- <span data-ttu-id="b33f6-153">A **Kiszolgálókezelő**, az a **eszközök** menüjében válassza **Windows PowerShell (x86)** .</span><span class="sxs-lookup"><span data-stu-id="b33f6-153">In **Server Manager**, from the **Tools** menu, select **Windows PowerShell (x86)**.</span></span>
- <span data-ttu-id="b33f6-154">Az asztalon vigye a kurzort a jobb felső sarokban kattintson **keresési**, típusa **PowerShell** majd **Windows PowerShell (x86)** .</span><span class="sxs-lookup"><span data-stu-id="b33f6-154">On the desktop, move the cursor to the upper right corner, click **Search**, type **PowerShell** and then click **Windows PowerShell (x86)**.</span></span>
- <span data-ttu-id="b33f6-155">A parancssorban adja meg: `%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`</span><span class="sxs-lookup"><span data-stu-id="b33f6-155">Via command line, enter: `%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`</span></span>

#### <a name="in-windows-81"></a><span data-ttu-id="b33f6-156">A 8.1-es Windows®</span><span class="sxs-lookup"><span data-stu-id="b33f6-156">In Windows® 8.1</span></span>

- <span data-ttu-id="b33f6-157">Az a **Start** írja be **Windows PowerShell (x86)** .</span><span class="sxs-lookup"><span data-stu-id="b33f6-157">On the **Start** screen, type **Windows PowerShell (x86)**.</span></span> <span data-ttu-id="b33f6-158">Kattintson a **Windows PowerShell x86** csempére.</span><span class="sxs-lookup"><span data-stu-id="b33f6-158">Click the **Windows PowerShell x86** tile.</span></span>
- <span data-ttu-id="b33f6-159">Ha futtatja [távoli kiszolgálófelügyelet eszközei](https://go.microsoft.com/fwlink/?LinkID=304145) for Windows 8.1, szintén nyissa meg a Windows PowerShell x86 a a **kiszolgáló ManagerTools** menü.</span><span class="sxs-lookup"><span data-stu-id="b33f6-159">If you are running [Remote Server Administration Tools](https://go.microsoft.com/fwlink/?LinkID=304145) for Windows 8.1, you can also open Windows PowerShell x86 from the **Server ManagerTools** menu.</span></span>
  <span data-ttu-id="b33f6-160">Válassza ki **Windows PowerShell (x86)** .</span><span class="sxs-lookup"><span data-stu-id="b33f6-160">Select **Windows PowerShell (x86)**.</span></span>
- <span data-ttu-id="b33f6-161">Az asztalon vigye a kurzort a jobb felső sarokban, kattintson **keresési**, típus **PowerShell x86** majd **Windows PowerShell (x86)** .</span><span class="sxs-lookup"><span data-stu-id="b33f6-161">On the desktop, move the cursor to the upper right corner, click **Search**, type **PowerShell x86** and then click **Windows PowerShell (x86)**.</span></span>
- <span data-ttu-id="b33f6-162">A parancssorban adja meg: `%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`</span><span class="sxs-lookup"><span data-stu-id="b33f6-162">Via command line, enter: `%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`</span></span>

#### <a name="in-windows-8"></a><span data-ttu-id="b33f6-163">A 8 Windows®</span><span class="sxs-lookup"><span data-stu-id="b33f6-163">In Windows® 8</span></span>

- <span data-ttu-id="b33f6-164">A a **Start** képernyőn, vigye a kurzort a jobb felső sarokban, kattintson a **beállítások**, kattintson a **Csempék**, és helyezze a **felügyeleti eszközök megjelenítése** csúszka igen.</span><span class="sxs-lookup"><span data-stu-id="b33f6-164">On the **Start** screen, move the cursor to the upper right corner, click **Settings**, click **Tiles**, and then move the **Show Administrative Tools** slider to Yes.</span></span> <span data-ttu-id="b33f6-165">Ezután írja be a **PowerShell** kattintson **Windows PowerShell (x86)** .</span><span class="sxs-lookup"><span data-stu-id="b33f6-165">Then, type **PowerShell** and click **Windows PowerShell (x86)**.</span></span>
- <span data-ttu-id="b33f6-166">Ha futtatja [távoli kiszolgálófelügyelet eszközei](https://www.microsoft.com/download/details.aspx?id=28972) Windows 8, is nyissa meg a Windows Powershellt x86 származó a **kiszolgáló ManagerTools** menü.</span><span class="sxs-lookup"><span data-stu-id="b33f6-166">If you are running [Remote Server Administration Tools](https://www.microsoft.com/download/details.aspx?id=28972) for Windows 8, you can also open Windows PowerShell x86 from the **Server ManagerTools** menu.</span></span> <span data-ttu-id="b33f6-167">Válassza ki **Windows PowerShell (x86)** .</span><span class="sxs-lookup"><span data-stu-id="b33f6-167">Select **Windows PowerShell (x86)**.</span></span>
- <span data-ttu-id="b33f6-168">A a **Start** képernyőt vagy a desktopban, és írja be a **PowerShell (x86)** és kattintson a **Windows PowerShell (x86)** .</span><span class="sxs-lookup"><span data-stu-id="b33f6-168">On the **Start** screen or the desktop, type **PowerShell (x86)** and then click **Windows PowerShell (x86)**.</span></span>
- <span data-ttu-id="b33f6-169">A parancssorban adja meg: `%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`</span><span class="sxs-lookup"><span data-stu-id="b33f6-169">Via command line, enter: `%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`</span></span>
