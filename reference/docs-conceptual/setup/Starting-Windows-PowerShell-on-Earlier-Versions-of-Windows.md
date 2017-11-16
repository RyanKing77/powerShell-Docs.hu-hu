---
ms.date: 2017-06-05
keywords: PowerShell parancsmag
title: "A Windows korábbi verzióiban Windows PowerShell indítása"
ms.assetid: 57125436-3d1e-4e7f-b5c4-8f0ecb49d642
ms.openlocfilehash: 52e3acc1fd3009ecad3b7134008e38d4edfb5ca7
ms.sourcegitcommit: d6ab9ab5909ed59cce4ce30e29457e0e75c7ac12
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/08/2017
---
# <a name="starting-windows-powershell-on-earlier-versions-of-windows"></a><span data-ttu-id="05789-103">A Windows korábbi verzióiban Windows PowerShell indítása</span><span class="sxs-lookup"><span data-stu-id="05789-103">Starting Windows PowerShell on Earlier Versions of Windows</span></span>
<span data-ttu-id="05789-104">Ez a szakasz ismerteti, hogyan kell elindítani a Windows PowerShell és a Windows PowerShell integrált parancsfájlkezelési környezet (ISE) a Windows® 7, Windows Server® 2008 R2 és Windows Server® 2008.</span><span class="sxs-lookup"><span data-stu-id="05789-104">This section explains how to start Windows PowerShell and Windows PowerShell Integrated Scripting Environment (ISE) on Windows® 7, Windows Server® 2008 R2, and Windows Server® 2008.</span></span> <span data-ttu-id="05789-105">A választható szolgáltatás engedélyezése a Windows PowerShell 2.0 a Windows Server® 2008 R2 és Windows Server® 2008 a Windows PowerShell ISE is ismerteti.</span><span class="sxs-lookup"><span data-stu-id="05789-105">It also explains how to enable the optional feature for Windows PowerShell ISE in Windows PowerShell 2.0 on Windows Server® 2008 R2 and Windows Server® 2008.</span></span>

<span data-ttu-id="05789-106">A Windows PowerShell 4.0 telepítése támogatott rendszeren, töltse le és telepítse [Windows Management Framework 4.0](http://go.microsoft.com/fwlink/?LinkID=293881).</span><span class="sxs-lookup"><span data-stu-id="05789-106">To install Windows PowerShell 4.0 on supported systems, download and install [Windows Management Framework 4.0](http://go.microsoft.com/fwlink/?LinkID=293881).</span></span> <span data-ttu-id="05789-107">További információkért lásd: [Windows PowerShell telepítése](Installing-Windows-PowerShell.md).</span><span class="sxs-lookup"><span data-stu-id="05789-107">For more information, see [Installing Windows PowerShell](Installing-Windows-PowerShell.md).</span></span>

<span data-ttu-id="05789-108">Telepítse a Windows PowerShell 3.0 támogatott rendszeren, töltse le és telepítse [Windows Management Framework 3.0](http://go.microsoft.com/fwlink/?LinkID=240290).</span><span class="sxs-lookup"><span data-stu-id="05789-108">To install Windows PowerShell 3.0 on supported systems, download and install [Windows Management Framework 3.0](http://go.microsoft.com/fwlink/?LinkID=240290).</span></span> <span data-ttu-id="05789-109">További információkért lásd: [Windows PowerShell telepítése](Installing-Windows-PowerShell.md).</span><span class="sxs-lookup"><span data-stu-id="05789-109">For more information, see [Installing Windows PowerShell](Installing-Windows-PowerShell.md).</span></span>

## <a name="how-to-start-windows-powershell-on-earlier-versions-of-windows"></a><span data-ttu-id="05789-110">A Windows korábbi verzióiban Windows PowerShell indítása</span><span class="sxs-lookup"><span data-stu-id="05789-110">How to Start Windows PowerShell on Earlier Versions of Windows</span></span>
<span data-ttu-id="05789-111">A következő módszerekkel segítségével adott esetben indítsa el a Windows PowerShell 3.0 vagy a Windows PowerShell 4.0-s verzióját.</span><span class="sxs-lookup"><span data-stu-id="05789-111">Use any of the following methods to start the installed version of Windows PowerShell 3.0, or Windows PowerShell 4.0, where applicable.</span></span>

#### <a name="from-the-start-menu"></a><span data-ttu-id="05789-112">A Start menüből</span><span class="sxs-lookup"><span data-stu-id="05789-112">From the Start Menu</span></span>

- <span data-ttu-id="05789-113">Kattintson a **Start**, típus **PowerShell**, és kattintson a **Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="05789-113">Click **Start**, type **PowerShell**, and then click **Windows PowerShell**.</span></span>

- <span data-ttu-id="05789-114">A a **Start** menüben kattintson **Start**, kattintson **minden program**, kattintson a **Kellékek**, kattintson a **Windows PowerShell**  mappa, és kattintson **Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="05789-114">From the **Start** menu, click **Start**, click **All Programs**, click **Accessories**, click the **Windows PowerShell** folder, and then click **Windows PowerShell**.</span></span>

#### <a name="at-the-command-prompt"></a><span data-ttu-id="05789-115">A parancssorba</span><span class="sxs-lookup"><span data-stu-id="05789-115">At the Command Prompt</span></span>

- <span data-ttu-id="05789-116">A Cmd.exe, a Windows PowerShell vagy a Windows PowerShell ISE indítsa el a Windows Powershellt, írja be:</span><span class="sxs-lookup"><span data-stu-id="05789-116">In Cmd.exe, Windows PowerShell, or Windows PowerShell ISE, to start Windows PowerShell, type:</span></span>

    ```
    PowerShell
    ```

    <span data-ttu-id="05789-117">A paraméterek a PowerShell.exe program segítségével testre szabhatja a munkamenet.</span><span class="sxs-lookup"><span data-stu-id="05789-117">You can also use the parameters of the PowerShell.exe program to customize the session.</span></span> <span data-ttu-id="05789-118">További információkért lásd: [PowerShell.exe parancssori súgó](../core-powershell/console/PowerShell.exe-Command-Line-Help.md).</span><span class="sxs-lookup"><span data-stu-id="05789-118">For more information, see [PowerShell.exe Command-Line Help](../core-powershell/console/PowerShell.exe-Command-Line-Help.md).</span></span>

#### <a name="with-administrative-privileges-run-as-administrator"></a><span data-ttu-id="05789-119">A felügyeleti jogosultságok ("Futtatás rendszergazdaként")</span><span class="sxs-lookup"><span data-stu-id="05789-119">With Administrative privileges ("Run as administrator")</span></span>

1. <span data-ttu-id="05789-120">Kattintson a **Start**, típus **PowerShell**, kattintson a jobb gombbal **Windows PowerShell**, és kattintson a **Futtatás rendszergazdaként**.</span><span class="sxs-lookup"><span data-stu-id="05789-120">Click **Start**, type **PowerShell**, right-click **Windows PowerShell**, and then click **Run as administrator**.</span></span>

## <a name="how-to-start-windows-powershell-ise-on-earlier-releases-of-windows"></a><span data-ttu-id="05789-121">A Windows PowerShell ISE indítása a Windows operációs rendszerek régebbi kiadásaiban</span><span class="sxs-lookup"><span data-stu-id="05789-121">How to Start Windows PowerShell ISE on Earlier Releases of Windows</span></span>
<span data-ttu-id="05789-122">A Windows PowerShell ISE elindításához használja a következő módszerekkel.</span><span class="sxs-lookup"><span data-stu-id="05789-122">Use any of the following methods to start Windows PowerShell ISE.</span></span>

#### <a name="from-the-start-menu"></a><span data-ttu-id="05789-123">A Start menüből</span><span class="sxs-lookup"><span data-stu-id="05789-123">From the Start Menu</span></span>

- <span data-ttu-id="05789-124">Kattintson a **Start**, típus **ISE**, és kattintson a **Windows PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="05789-124">Click **Start**, type **ISE**, and then click **Windows PowerShell ISE**.</span></span>

- <span data-ttu-id="05789-125">A a **Start** menüben kattintson **Start**, kattintson **minden program**, kattintson a **Kellékek**, kattintson a **Windows PowerShell**  mappa, és kattintson **Windows PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="05789-125">From the **Start** menu, click **Start**, click **All Programs**, click **Accessories**, click the **Windows PowerShell** folder, and then click **Windows PowerShell ISE**.</span></span>

#### <a name="at-the-command-prompt"></a><span data-ttu-id="05789-126">A parancssorba</span><span class="sxs-lookup"><span data-stu-id="05789-126">At the Command Prompt</span></span>

- <span data-ttu-id="05789-127">A Cmd.exe, a Windows PowerShell vagy a Windows PowerShell ISE indítsa el a Windows Powershellt, írja be:</span><span class="sxs-lookup"><span data-stu-id="05789-127">In Cmd.exe, Windows PowerShell, or Windows PowerShell ISE, to start Windows PowerShell, type:</span></span>

    ```
    PowerShell_ISE
    ```

    <span data-ttu-id="05789-128">vagy a</span><span class="sxs-lookup"><span data-stu-id="05789-128">or</span></span>

    ```
    ISE
    ```

#### <a name="with-administrative-privileges-run-as-administrator"></a><span data-ttu-id="05789-129">A felügyeleti jogosultságok ("Futtatás rendszergazdaként")</span><span class="sxs-lookup"><span data-stu-id="05789-129">With Administrative privileges ("Run as administrator")</span></span>

1. <span data-ttu-id="05789-130">Kattintson a **Start**, típus **ISE**, kattintson a jobb gombbal **Windows PowerShell ISE**, és kattintson a **Futtatás rendszergazdaként**.</span><span class="sxs-lookup"><span data-stu-id="05789-130">Click **Start**, type **ISE**, right-click **Windows PowerShell ISE**, and then click **Run as administrator**.</span></span>

## <a name="how-to-enable-windows-powershell-ise-on-earlier-releases-of-windows"></a><span data-ttu-id="05789-131">A Windows korábbi verzióiban Windows PowerShell ISE engedélyezése</span><span class="sxs-lookup"><span data-stu-id="05789-131">How to Enable Windows PowerShell ISE on Earlier Releases of Windows</span></span>
<span data-ttu-id="05789-132">A Windows PowerShell 4.0-s verzióját és a Windows PowerShell 3.0, a Windows PowerShell ISE alapértelmezés szerint engedélyezve van a Windows összes verzióján.</span><span class="sxs-lookup"><span data-stu-id="05789-132">In Windows PowerShell 4.0 and Windows PowerShell 3.0, Windows PowerShell ISE is enabled by default on all versions of Windows.</span></span> <span data-ttu-id="05789-133">Ha már nincs engedélyezve, a Windows Management Framework 4.0 vagy a Windows Management Framework 3.0 engedélyezi.</span><span class="sxs-lookup"><span data-stu-id="05789-133">If it is not already enabled, Windows Management Framework 4.0 or Windows Management Framework 3.0 enables it.</span></span>

<span data-ttu-id="05789-134">A Windows PowerShell 2.0 a Windows PowerShell ISE alapértelmezés szerint engedélyezve van a Windows 7.</span><span class="sxs-lookup"><span data-stu-id="05789-134">In Windows PowerShell 2.0, Windows PowerShell ISE is enabled by default on Windows 7.</span></span> <span data-ttu-id="05789-135">Azonban a Windows Server 2008 R2 és Windows Server 2008, akkor választható lehetőség.</span><span class="sxs-lookup"><span data-stu-id="05789-135">However, on Windows Server 2008 R2 and Windows Server 2008, it is an optional feature.</span></span>

<span data-ttu-id="05789-136">Ahhoz, hogy a Windows PowerShell ISE a Windows PowerShell 2.0 a Windows Server 2008 R2 vagy Windows Server 2008, a következő eljárással.</span><span class="sxs-lookup"><span data-stu-id="05789-136">To enable Windows PowerShell ISE in Windows PowerShell 2.0 on Windows Server 2008 R2 or Windows Server 2008, use the following procedure.</span></span>

#### <a name="to-enable-windows-powershell-integrated-scripting-environment-ise"></a><span data-ttu-id="05789-137">Ahhoz, hogy a Windows PowerShell integrált parancsfájl-kezelési környezet (ISE)</span><span class="sxs-lookup"><span data-stu-id="05789-137">To enable Windows PowerShell Integrated Scripting Environment (ISE)</span></span>

1. <span data-ttu-id="05789-138">Indítsa el a Kiszolgálókezelőt.</span><span class="sxs-lookup"><span data-stu-id="05789-138">Start Server Manager.</span></span>

2. <span data-ttu-id="05789-139">Kattintson a **szolgáltatások** majd **szolgáltatások hozzáadása**.</span><span class="sxs-lookup"><span data-stu-id="05789-139">Click **Features** and then click **Add Features**.</span></span>

3. <span data-ttu-id="05789-140">A szolgáltatások kiválasztása párbeszédpanelen kattintson a Windows PowerShell integrált parancsfájlkezelési környezet (ISE).</span><span class="sxs-lookup"><span data-stu-id="05789-140">In Select Features, click Windows PowerShell Integrated Scripting Environment (ISE).</span></span>

