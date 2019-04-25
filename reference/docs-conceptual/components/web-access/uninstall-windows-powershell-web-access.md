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
# <a name="uninstall-windows-powershell-web-access"></a>Windows PowerShell-elérés eltávolítása

Frissítve: 2013. június 24-én

A következőkre vonatkozik: Windows Server 2012 R2, Windows Server 2012

Ebben a témakörben leírt lépéseket az átjárókiszolgáló, amelyre telepítve van a Windows PowerShell-elérés webhely és a megfelelő alkalmazás eltávolítása.

## <a name="notify-users"></a>Felhasználók értesítése

Mielőtt elkezdené, értesítse a felhasználókat a webalapú konzol, hogy a webhely eltávolításáról.

Windows PowerShell-elérés eltávolítása nem távolítja el az IIS vagy bármely más olyan funkció, amely automatikusan telepített, mert a Windows PowerShell-elérés használatához szükséges azok futtatása.
Az eltávolítási folyamat szolgáltatásai telepítve, amelyen a Windows PowerShell-elérés volt függő; maradnak. szükség esetén, külön eltávolíthatja ezeket a funkciókat.

## <a name="recommended-quick-uninstallation"></a>Ajánlott (gyors) Eltávolítás

Ebben a szakaszban ismertetett eljárások segítségével távolíthatja el:

- a Windows PowerShell-elérés webalkalmazás és
- a Windows PowerShell-elérés szolgáltatás

Windows PowerShell-parancsmagok használatával.

### <a name="step-1-delete-the-web-application-using-cmdlets"></a>1. lépés: A webalkalmazás-parancsmagok használatával törlése

1. Hajtsa végre az alábbi lépéseket egy Windows PowerShell-munkamenetet.

    -   A Windows asztalon kattintson a jobb gombbal **Windows PowerShell** a tálcán.

    -   A Windows a **Start** kattintson **Windows PowerShell**.

2. Típus `Uninstall-PswaWebApplication`, és nyomja le az **Enter**.
   1. Ha megadta a saját, egyéni webhelynevet, vegye fel a `-WebsiteName` paramétert a parancshoz, és adja meg a webhely nevét.

        `Uninstall-PswaWebApplication -WebsiteName <web-site-name>`
   1. Ha egyéni webalkalmazást használt (nem az alapértelmezett alkalmazás **pswa**, adja hozzá a `-WebApplicationName` paramétert a parancshoz, és adja meg a webalkalmazás nevét.

        `Uninstall-PswaWebApplication -WebApplicationName <web-application-name>`
   1. Ha teszttanúsítványt használ, adja hozzá a `DeleteTestCertificate` paramétert a parancsmaghoz, az alábbi példában látható módon.

        `Uninstall-PswaWebApplication -DeleteTestCertificate`

### <a name="step-2-uninstall-windows-powershell-web-access-using-cmdlets"></a>2. lépés: Windows-parancsmagok használatával PowerShell-elérés eltávolítása

1. Hajtsa végre az alábbi lépéseket egy Windows PowerShell-munkamenetet emelt szintű felhasználói jogosultsággal nyissa meg. Ha a munkamenet már meg nyitva, folytassa a következő lépéssel.

    -   A Windows asztalon kattintson a jobb gombbal **Windows PowerShell** a tálcán, és kattintson a **Futtatás rendszergazdaként**.

    -   A Windows a **Start** kattintson a jobb gombbal **Windows PowerShell**, és kattintson a **Futtatás rendszergazdaként**.

1. Írja be a következőt, majd nyomja le **Enter**, ahol *számítógép_neve* egy távoli kiszolgálóra, amelyről el kívánja távolítani Windows PowerShell-elérés jelöli. A `-Restart` paraméter automatikusan újraindítja a célkiszolgálót, ha szükséges a eltávolításához.

        Uninstall-WindowsFeature -Name WindowsPowerShellWebAccess -ComputerName <computer_name> -Restart

    Eltávolítja a szerepkörök és szolgáltatások offline virtuális merevlemezről, hozzá kell adnia mind a `-ComputerName` paraméter és a `-VHD` paraméter. A `-ComputerName` paraméter, amelyhez csatlakoztatni kívánja a VHD-t, a kiszolgáló nevét tartalmazza, és a `-VHD` paraméter tartalmazza a megadott kiszolgálón a VHD-fájl elérési útját.

        Uninstall-WindowsFeature -Name WindowsPowerShellWebAccess -VHD <path> -ComputerName <computer_name> -Restart

1. Eltávolítás befejezésekor ellenőrizze, hogy megnyitásával Windows PowerShell-elérés eltávolítása a **minden kiszolgáló** lapot a Kiszolgálókezelő, válassza ki a kiszolgálót, amelyről eltávolította a szolgáltatást, és megtekintése a **szerepkörök és Szolgáltatások** csempét a kiválasztott kiszolgálóhoz tartozó lapon.

    Is futtathatja a `Get-WindowsFeature` parancsmag a kiválasztott kiszolgálóra (Get-WindowsFeature - ComputerName &lt; *számítógép_neve*&gt;) a szerepkörök és a kiszolgálón telepített szolgáltatások listájának megtekintéséhez.

## <a name="custom-uninstallation"></a>Egyéni Eltávolítás

Ebben a szakaszban ismertetett eljárások segítségével, távolítsa el a Windows PowerShell-elérés webalkalmazás és a Windows PowerShell-elérés funkció, a szerepkörök és szolgáltatások varázsló a Kiszolgálókezelőben, és eltávolítása az IIS-kezelő konzol használatával is.

### <a name="step-1-delete-the-web-application-using-iis-manager"></a>1. lépés: A webalkalmazás az IIS-kezelő törlése


1. Nyissa meg az IIS-kezelő konzol a következő módszerek valamelyikével. Ha már meg nyitva, folytassa a következő lépéssel.

    -   A Windows asztalon indítsa el a Kiszolgálókezelőt kattintva **Kiszolgálókezelő** a Windows tálcán. Az a **eszközök** menüjében a Kiszolgálókezelőben kattintson **Internet Information Services (IIS) kezelője**.

    -   A Windows a **Start** írja be a nevének bármelyik részét **Internet Information Services (IIS) kezelője**. Kattintson a parancsikonra, amikor az megjelenik a **alkalmazások** eredményeket.

1. Az IIS-kezelő fát megjelenítő ablaktáblán válassza ki a Windows PowerShell-elérés webalkalmazást futtató webhelyet.

1. Az a **műveletek** panel alatt **webhely kezelése**, kattintson a **leállítása**.

1. A fát megjelenítő ablaktáblán kattintson a jobb gombbal a webes alkalmazás a Windows PowerShell-elérés webalkalmazást futtató webhelyen, és kattintson **eltávolítása**.

1. A fát megjelenítő ablaktáblán válassza ki a **alkalmazáskészletek**, válassza ki a Windows PowerShell-elérés alkalmazáskészlet-mappáját, kattintson a **leállítása** a a **műveletek** ablaktáblán, majd  **Távolítsa el** a tartalompanelen.

1. Zárja be az IIS-kezelőt.

> ![Figyelmeztetés megjegyzés](images/SecurityNote.jpeg)**Megjegyzés**:
>
> A tanúsítvány nem törlődik az eltávolítás során.
>
> Ha önaláírt tanúsítványt létrehozni vagy a használt teszttanúsítványt és eltávolíthatja azt, törölje a tanúsítványt az IIS-kezelőben.

### <a name="step-2-uninstall-windows-powershell-web-access-using-the-remove-roles-and-features-wizard"></a>2. lépés: Windows eltávolítása a szerepkörök és szolgáltatások varázsló PowerShell-elérés eltávolítása

1. Ha a Kiszolgálókezelő már meg nyitva, folytassa a következő lépéssel. Ha a Kiszolgálókezelő még nem nyitott, nyissa meg a következő módszerek valamelyikével.

    -   A Windows asztalon indítsa el a Kiszolgálókezelőt kattintva **Kiszolgálókezelő** a Windows tálcán.

    -   A Windows a **Start** kattintson **Kiszolgálókezelő**.

1. Az a **kezelés** menüben kattintson a **szerepkörök és szolgáltatások eltávolítása**.

1. Az a **célkiszolgáló kijelölése** lapra, jelölje be a kiszolgáló vagy offline VHD-t, amelyről el kívánja távolítani a szolgáltatást. Offline VHD kiválasztásához először válassza ki a kiszolgálót, amelyhez csatlakoztatni kívánja a VHD-t, és válassza ki a VHD-fájlt. Miután kiválasztotta a célkiszolgálón, kattintson a **tovább**.

1. Kattintson a **tovább** ugráshoz a **szolgáltatások eltávolítása** lapot.

1. Törölje a jelet a jelölőnégyzetből a **Windows PowerShell-elérés**, és kattintson a **tovább**.

1. Az a **Eltávolítandók megerősítése** kattintson **eltávolítása**.

## <a name="see-also"></a>Lásd még:

- [Telepítheti és használhatja a Windows PowerShell-Elérésbe](install-and-use-windows-powershell-web-access.md)
- [Az IIS-kezelő 7.0 súgó](https://technet.microsoft.com/library/cc732664.aspx)