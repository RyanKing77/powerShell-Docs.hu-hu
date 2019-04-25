---
ms.date: 08/23/2017
keywords: PowerShell, a parancsmag
title: a windows powershell-elérés eltávolítása
ms.openlocfilehash: 22c874d766445dccedd8494097daf16c30fa66ff
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62058153"
---
# <a name="uninstall-windows-powershell-web-access"></a><span data-ttu-id="00085-103">Windows PowerShell-elérés eltávolítása</span><span class="sxs-lookup"><span data-stu-id="00085-103">Uninstall Windows PowerShell Web Access</span></span>

<span data-ttu-id="00085-104">Frissítve: 2013. június 24-én</span><span class="sxs-lookup"><span data-stu-id="00085-104">Updated: June 24, 2013</span></span>

<span data-ttu-id="00085-105">A következőkre vonatkozik: Windows Server 2012 R2, Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="00085-105">Applies To: Windows Server 2012 R2, Windows Server 2012</span></span>

<span data-ttu-id="00085-106">Ebben a témakörben leírt lépéseket az átjárókiszolgáló, amelyre telepítve van a Windows PowerShell-elérés webhely és a megfelelő alkalmazás eltávolítása.</span><span class="sxs-lookup"><span data-stu-id="00085-106">The steps in this topic remove the Windows PowerShell Web Access website and corresponding application from the gateway server where it is installed.</span></span>

## <a name="notify-users"></a><span data-ttu-id="00085-107">Felhasználók értesítése</span><span class="sxs-lookup"><span data-stu-id="00085-107">Notify users</span></span>

<span data-ttu-id="00085-108">Mielőtt elkezdené, értesítse a felhasználókat a webalapú konzol, hogy a webhely eltávolításáról.</span><span class="sxs-lookup"><span data-stu-id="00085-108">Before you begin, notify users of the web-based console that you are removing the website.</span></span>

<span data-ttu-id="00085-109">Windows PowerShell-elérés eltávolítása nem távolítja el az IIS vagy bármely más olyan funkció, amely automatikusan telepített, mert a Windows PowerShell-elérés használatához szükséges azok futtatása.</span><span class="sxs-lookup"><span data-stu-id="00085-109">Uninstalling Windows PowerShell Web Access does not uninstall IIS or any other features that were installed automatically because Windows PowerShell Web Access requires them to run.</span></span>
<span data-ttu-id="00085-110">Az eltávolítási folyamat szolgáltatásai telepítve, amelyen a Windows PowerShell-elérés volt függő; maradnak. szükség esetén, külön eltávolíthatja ezeket a funkciókat.</span><span class="sxs-lookup"><span data-stu-id="00085-110">The uninstallation process leaves features installed upon which Windows PowerShell Web Access was dependent; you can uninstall those features separately if needed.</span></span>

## <a name="recommended-quick-uninstallation"></a><span data-ttu-id="00085-111">Ajánlott (gyors) Eltávolítás</span><span class="sxs-lookup"><span data-stu-id="00085-111">Recommended (quick) uninstallation</span></span>

<span data-ttu-id="00085-112">Ebben a szakaszban ismertetett eljárások segítségével távolíthatja el:</span><span class="sxs-lookup"><span data-stu-id="00085-112">Procedures in this section help you uninstall both:</span></span>

- <span data-ttu-id="00085-113">a Windows PowerShell-elérés webalkalmazás és</span><span class="sxs-lookup"><span data-stu-id="00085-113">the Windows PowerShell Web Access web application, and</span></span>
- <span data-ttu-id="00085-114">a Windows PowerShell-elérés szolgáltatás</span><span class="sxs-lookup"><span data-stu-id="00085-114">the Windows PowerShell Web Access feature</span></span>

<span data-ttu-id="00085-115">Windows PowerShell-parancsmagok használatával.</span><span class="sxs-lookup"><span data-stu-id="00085-115">by using Windows PowerShell cmdlets.</span></span>

### <a name="step-1-delete-the-web-application-using-cmdlets"></a><span data-ttu-id="00085-116">1. lépés: A webalkalmazás-parancsmagok használatával törlése</span><span class="sxs-lookup"><span data-stu-id="00085-116">Step 1: Delete the web application using cmdlets</span></span>

1. <span data-ttu-id="00085-117">Hajtsa végre az alábbi lépéseket egy Windows PowerShell-munkamenetet.</span><span class="sxs-lookup"><span data-stu-id="00085-117">Do one of the following to open a Windows PowerShell session.</span></span>

    -   <span data-ttu-id="00085-118">A Windows asztalon kattintson a jobb gombbal **Windows PowerShell** a tálcán.</span><span class="sxs-lookup"><span data-stu-id="00085-118">On the Windows desktop, right-click **Windows PowerShell** on the taskbar.</span></span>

    -   <span data-ttu-id="00085-119">A Windows a **Start** kattintson **Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="00085-119">On the Windows **Start** screen, click **Windows PowerShell**.</span></span>

2. <span data-ttu-id="00085-120">Típus `Uninstall-PswaWebApplication`, és nyomja le az **Enter**.</span><span class="sxs-lookup"><span data-stu-id="00085-120">Type `Uninstall-PswaWebApplication`, and then press **Enter**.</span></span>
   1. <span data-ttu-id="00085-121">Ha megadta a saját, egyéni webhelynevet, vegye fel a `-WebsiteName` paramétert a parancshoz, és adja meg a webhely nevét.</span><span class="sxs-lookup"><span data-stu-id="00085-121">If you have specified your own, custom website name, add the `-WebsiteName` parameter to your command, and specify the website name.</span></span>

        `Uninstall-PswaWebApplication -WebsiteName <web-site-name>`
   1. <span data-ttu-id="00085-122">Ha egyéni webalkalmazást használt (nem az alapértelmezett alkalmazás **pswa**, adja hozzá a `-WebApplicationName` paramétert a parancshoz, és adja meg a webalkalmazás nevét.</span><span class="sxs-lookup"><span data-stu-id="00085-122">If you have used a custom web application (not the default application, **pswa**, add the `-WebApplicationName` parameter to your command, and specify the name of the web application.</span></span>

        `Uninstall-PswaWebApplication -WebApplicationName <web-application-name>`
   1. <span data-ttu-id="00085-123">Ha teszttanúsítványt használ, adja hozzá a `DeleteTestCertificate` paramétert a parancsmaghoz, az alábbi példában látható módon.</span><span class="sxs-lookup"><span data-stu-id="00085-123">If you are using a test certificate, add the `DeleteTestCertificate` parameter to the cmdlet, as shown in the following example.</span></span>

        `Uninstall-PswaWebApplication -DeleteTestCertificate`

### <a name="step-2-uninstall-windows-powershell-web-access-using-cmdlets"></a><span data-ttu-id="00085-124">2. lépés: Windows-parancsmagok használatával PowerShell-elérés eltávolítása</span><span class="sxs-lookup"><span data-stu-id="00085-124">Step 2: Uninstall Windows PowerShell Web Access using cmdlets</span></span>

1. <span data-ttu-id="00085-125">Hajtsa végre az alábbi lépéseket egy Windows PowerShell-munkamenetet emelt szintű felhasználói jogosultsággal nyissa meg.</span><span class="sxs-lookup"><span data-stu-id="00085-125">Do one of the following to open a Windows PowerShell session with elevated user rights.</span></span> <span data-ttu-id="00085-126">Ha a munkamenet már meg nyitva, folytassa a következő lépéssel.</span><span class="sxs-lookup"><span data-stu-id="00085-126">If a session is already open, go on to the next step.</span></span>

    -   <span data-ttu-id="00085-127">A Windows asztalon kattintson a jobb gombbal **Windows PowerShell** a tálcán, és kattintson a **Futtatás rendszergazdaként**.</span><span class="sxs-lookup"><span data-stu-id="00085-127">On the Windows desktop, right-click **Windows PowerShell** on the taskbar, and then click **Run as Administrator**.</span></span>

    -   <span data-ttu-id="00085-128">A Windows a **Start** kattintson a jobb gombbal **Windows PowerShell**, és kattintson a **Futtatás rendszergazdaként**.</span><span class="sxs-lookup"><span data-stu-id="00085-128">On the Windows **Start** screen, right-click **Windows PowerShell**, and then click **Run as Administrator**.</span></span>

1. <span data-ttu-id="00085-129">Írja be a következőt, majd nyomja le **Enter**, ahol *számítógép_neve* egy távoli kiszolgálóra, amelyről el kívánja távolítani Windows PowerShell-elérés jelöli.</span><span class="sxs-lookup"><span data-stu-id="00085-129">Type the following, and then press **Enter**, where *computer_name* represents a remote server from which you want to remove Windows PowerShell Web Access.</span></span> <span data-ttu-id="00085-130">A `-Restart` paraméter automatikusan újraindítja a célkiszolgálót, ha szükséges a eltávolításához.</span><span class="sxs-lookup"><span data-stu-id="00085-130">The `-Restart` parameter automatically restarts destination servers if required by the removal.</span></span>

        Uninstall-WindowsFeature -Name WindowsPowerShellWebAccess -ComputerName <computer_name> -Restart

    <span data-ttu-id="00085-131">Eltávolítja a szerepkörök és szolgáltatások offline virtuális merevlemezről, hozzá kell adnia mind a `-ComputerName` paraméter és a `-VHD` paraméter.</span><span class="sxs-lookup"><span data-stu-id="00085-131">To remove roles and features from an offline VHD, you must add both the `-ComputerName` parameter and the `-VHD` parameter.</span></span> <span data-ttu-id="00085-132">A `-ComputerName` paraméter, amelyhez csatlakoztatni kívánja a VHD-t, a kiszolgáló nevét tartalmazza, és a `-VHD` paraméter tartalmazza a megadott kiszolgálón a VHD-fájl elérési útját.</span><span class="sxs-lookup"><span data-stu-id="00085-132">The `-ComputerName` parameter contains the name of the server on which to mount the VHD, and the `-VHD` parameter contains the path to the VHD file on the specified server.</span></span>

        Uninstall-WindowsFeature -Name WindowsPowerShellWebAccess -VHD <path> -ComputerName <computer_name> -Restart

1. <span data-ttu-id="00085-133">Eltávolítás befejezésekor ellenőrizze, hogy megnyitásával Windows PowerShell-elérés eltávolítása a **minden kiszolgáló** lapot a Kiszolgálókezelő, válassza ki a kiszolgálót, amelyről eltávolította a szolgáltatást, és megtekintése a **szerepkörök és Szolgáltatások** csempét a kiválasztott kiszolgálóhoz tartozó lapon.</span><span class="sxs-lookup"><span data-stu-id="00085-133">When removal is finished, verify that you removed Windows PowerShell Web Access by opening the **All Servers** page in Server Manager, selecting a server from which you removed the feature, and viewing the **Roles and Features** tile on the page for the selected server.</span></span>

    <span data-ttu-id="00085-134">Is futtathatja a `Get-WindowsFeature` parancsmag a kiválasztott kiszolgálóra (Get-WindowsFeature - ComputerName &lt; *számítógép_neve*&gt;) a szerepkörök és a kiszolgálón telepített szolgáltatások listájának megtekintéséhez.</span><span class="sxs-lookup"><span data-stu-id="00085-134">You can also run the `Get-WindowsFeature` cmdlet targeted at the selected server (Get-WindowsFeature -ComputerName &lt;*computer_name*&gt;) to view a list of roles and features that are installed on the server.</span></span>

## <a name="custom-uninstallation"></a><span data-ttu-id="00085-135">Egyéni Eltávolítás</span><span class="sxs-lookup"><span data-stu-id="00085-135">Custom uninstallation</span></span>

<span data-ttu-id="00085-136">Ebben a szakaszban ismertetett eljárások segítségével, távolítsa el a Windows PowerShell-elérés webalkalmazás és a Windows PowerShell-elérés funkció, a szerepkörök és szolgáltatások varázsló a Kiszolgálókezelőben, és eltávolítása az IIS-kezelő konzol használatával is.</span><span class="sxs-lookup"><span data-stu-id="00085-136">Procedures in this section help you uninstall both the Windows PowerShell Web Access web application and the Windows PowerShell Web Access feature by using the Remove Roles and Features Wizard in Server Manager, and the IIS Manager console.</span></span>

### <a name="step-1-delete-the-web-application-using-iis-manager"></a><span data-ttu-id="00085-137">1. lépés: A webalkalmazás az IIS-kezelő törlése</span><span class="sxs-lookup"><span data-stu-id="00085-137">Step 1: Delete the web application using IIS Manager</span></span>


1. <span data-ttu-id="00085-138">Nyissa meg az IIS-kezelő konzol a következő módszerek valamelyikével.</span><span class="sxs-lookup"><span data-stu-id="00085-138">Open the IIS Manager console by doing one of the following.</span></span> <span data-ttu-id="00085-139">Ha már meg nyitva, folytassa a következő lépéssel.</span><span class="sxs-lookup"><span data-stu-id="00085-139">If it is already open, go on to the next step.</span></span>

    -   <span data-ttu-id="00085-140">A Windows asztalon indítsa el a Kiszolgálókezelőt kattintva **Kiszolgálókezelő** a Windows tálcán.</span><span class="sxs-lookup"><span data-stu-id="00085-140">On the Windows desktop, start Server Manager by clicking **Server Manager** in the Windows taskbar.</span></span> <span data-ttu-id="00085-141">Az a **eszközök** menüjében a Kiszolgálókezelőben kattintson **Internet Information Services (IIS) kezelője**.</span><span class="sxs-lookup"><span data-stu-id="00085-141">On the **Tools** menu in Server Manager, click **Internet Information Services (IIS) Manager**.</span></span>

    -   <span data-ttu-id="00085-142">A Windows a **Start** írja be a nevének bármelyik részét **Internet Information Services (IIS) kezelője**.</span><span class="sxs-lookup"><span data-stu-id="00085-142">On the Windows **Start** screen, type any part of the name **Internet Information Services (IIS) Manager**.</span></span> <span data-ttu-id="00085-143">Kattintson a parancsikonra, amikor az megjelenik a **alkalmazások** eredményeket.</span><span class="sxs-lookup"><span data-stu-id="00085-143">Click the shortcut when it is displayed in the **Apps** results.</span></span>

1. <span data-ttu-id="00085-144">Az IIS-kezelő fát megjelenítő ablaktáblán válassza ki a Windows PowerShell-elérés webalkalmazást futtató webhelyet.</span><span class="sxs-lookup"><span data-stu-id="00085-144">In the IIS Manager tree pane, select the website that is running the Windows PowerShell Web Access web application.</span></span>

1. <span data-ttu-id="00085-145">Az a **műveletek** panel alatt **webhely kezelése**, kattintson a **leállítása**.</span><span class="sxs-lookup"><span data-stu-id="00085-145">In the **Actions** pane, under **Manage Website**, click **Stop**.</span></span>

1. <span data-ttu-id="00085-146">A fát megjelenítő ablaktáblán kattintson a jobb gombbal a webes alkalmazás a Windows PowerShell-elérés webalkalmazást futtató webhelyen, és kattintson **eltávolítása**.</span><span class="sxs-lookup"><span data-stu-id="00085-146">In the tree pane, right-click the web application in the website that is running the Windows PowerShell Web Access web application, and then click **Remove**.</span></span>

1. <span data-ttu-id="00085-147">A fát megjelenítő ablaktáblán válassza ki a **alkalmazáskészletek**, válassza ki a Windows PowerShell-elérés alkalmazáskészlet-mappáját, kattintson a **leállítása** a a **műveletek** ablaktáblán, majd  **Távolítsa el** a tartalompanelen.</span><span class="sxs-lookup"><span data-stu-id="00085-147">In the tree pane, select **Application Pools**, select the Windows PowerShell Web Access application pool folder, click **Stop** in the **Actions** pane, and then click **Remove** in the content pane.</span></span>

1. <span data-ttu-id="00085-148">Zárja be az IIS-kezelőt.</span><span class="sxs-lookup"><span data-stu-id="00085-148">Close IIS Manager.</span></span>

> <span data-ttu-id="00085-149">![Figyelmeztetés megjegyzés](images/SecurityNote.jpeg)**Megjegyzés**:</span><span class="sxs-lookup"><span data-stu-id="00085-149">![Warning note](images/SecurityNote.jpeg)**Note**:</span></span>
>
> <span data-ttu-id="00085-150">A tanúsítvány nem törlődik az eltávolítás során.</span><span class="sxs-lookup"><span data-stu-id="00085-150">The certificate is not deleted during uninstallation.</span></span>
>
> <span data-ttu-id="00085-151">Ha önaláírt tanúsítványt létrehozni vagy a használt teszttanúsítványt és eltávolíthatja azt, törölje a tanúsítványt az IIS-kezelőben.</span><span class="sxs-lookup"><span data-stu-id="00085-151">If you created a self-signed certificate or used a test certificate and want to remove it, delete the certificate in IIS Manager.</span></span>

### <a name="step-2-uninstall-windows-powershell-web-access-using-the-remove-roles-and-features-wizard"></a><span data-ttu-id="00085-152">2. lépés: Windows eltávolítása a szerepkörök és szolgáltatások varázsló PowerShell-elérés eltávolítása</span><span class="sxs-lookup"><span data-stu-id="00085-152">Step 2: Uninstall Windows PowerShell Web Access using the Remove Roles and Features Wizard</span></span>

1. <span data-ttu-id="00085-153">Ha a Kiszolgálókezelő már meg nyitva, folytassa a következő lépéssel.</span><span class="sxs-lookup"><span data-stu-id="00085-153">If Server Manager is already open, go on to the next step.</span></span> <span data-ttu-id="00085-154">Ha a Kiszolgálókezelő még nem nyitott, nyissa meg a következő módszerek valamelyikével.</span><span class="sxs-lookup"><span data-stu-id="00085-154">If Server Manager is not already open, open it by doing one of the following.</span></span>

    -   <span data-ttu-id="00085-155">A Windows asztalon indítsa el a Kiszolgálókezelőt kattintva **Kiszolgálókezelő** a Windows tálcán.</span><span class="sxs-lookup"><span data-stu-id="00085-155">On the Windows desktop, start Server Manager by clicking **Server Manager** in the Windows taskbar.</span></span>

    -   <span data-ttu-id="00085-156">A Windows a **Start** kattintson **Kiszolgálókezelő**.</span><span class="sxs-lookup"><span data-stu-id="00085-156">On the Windows **Start** screen, click **Server Manager**.</span></span>

1. <span data-ttu-id="00085-157">Az a **kezelés** menüben kattintson a **szerepkörök és szolgáltatások eltávolítása**.</span><span class="sxs-lookup"><span data-stu-id="00085-157">On the **Manage** menu, click **Remove Roles and Features**.</span></span>

1. <span data-ttu-id="00085-158">Az a **célkiszolgáló kijelölése** lapra, jelölje be a kiszolgáló vagy offline VHD-t, amelyről el kívánja távolítani a szolgáltatást.</span><span class="sxs-lookup"><span data-stu-id="00085-158">On the **Select destination server** page, select the server or offline VHD from which you want to remove the feature.</span></span> <span data-ttu-id="00085-159">Offline VHD kiválasztásához először válassza ki a kiszolgálót, amelyhez csatlakoztatni kívánja a VHD-t, és válassza ki a VHD-fájlt.</span><span class="sxs-lookup"><span data-stu-id="00085-159">To select an offline VHD, first select the server on which to mount the VHD, and then select the VHD file.</span></span> <span data-ttu-id="00085-160">Miután kiválasztotta a célkiszolgálón, kattintson a **tovább**.</span><span class="sxs-lookup"><span data-stu-id="00085-160">After you have selected the destination server, click **Next**.</span></span>

1. <span data-ttu-id="00085-161">Kattintson a **tovább** ugráshoz a **szolgáltatások eltávolítása** lapot.</span><span class="sxs-lookup"><span data-stu-id="00085-161">Click **Next** again to skip to the **Remove features** page.</span></span>

1. <span data-ttu-id="00085-162">Törölje a jelet a jelölőnégyzetből a **Windows PowerShell-elérés**, és kattintson a **tovább**.</span><span class="sxs-lookup"><span data-stu-id="00085-162">Clear the check box for **Windows PowerShell Web Access**, and then click **Next**.</span></span>

1. <span data-ttu-id="00085-163">Az a **Eltávolítandók megerősítése** kattintson **eltávolítása**.</span><span class="sxs-lookup"><span data-stu-id="00085-163">On the **Confirm removal selections** page, click **Remove**.</span></span>

## <a name="see-also"></a><span data-ttu-id="00085-164">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="00085-164">See Also</span></span>

- [<span data-ttu-id="00085-165">Telepítheti és használhatja a Windows PowerShell-Elérésbe</span><span class="sxs-lookup"><span data-stu-id="00085-165">Install and Use Windows PowerShell Web Access</span></span>](install-and-use-windows-powershell-web-access.md)
- [<span data-ttu-id="00085-166">Az IIS-kezelő 7.0 súgó</span><span class="sxs-lookup"><span data-stu-id="00085-166">IIS Manager 7.0 Help</span></span>](https://technet.microsoft.com/library/cc732664.aspx)