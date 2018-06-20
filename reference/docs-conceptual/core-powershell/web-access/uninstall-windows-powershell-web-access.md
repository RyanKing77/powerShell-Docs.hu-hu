---
ms.date: 08/23/2017
keywords: PowerShell parancsmag
title: a windows powershell webes elérés eltávolítása
ms.openlocfilehash: 22c874d766445dccedd8494097daf16c30fa66ff
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
ms.locfileid: "30952953"
---
# <a name="uninstall-windows-powershell-web-access"></a>Webes Windows PowerShell-elérés eltávolítása

Frissített: Június 24 2013.

Vonatkozik: Windows Server 2012 R2, Windows Server 2012-ben

A témakörben leírt lépések az átjárókiszolgáló, amelyen telepítve van a Windows PowerShell Web Access webhely és a megfelelő alkalmazás eltávolítása.

## <a name="notify-users"></a>A felhasználók értesítése

Mielőtt hozzákezdene, értesítse a webalapú konzol felhasználóit a webhely eltávolításáról.

A Windows PowerShell Web Access eltávolítása nem távolítja el az IIS vagy bármely más, amelyeket automatikusan telepített, mert a Windows PowerShell Web Access használatához szükséges azok futtatása.
Az eltávolítási folyamat kilép, amelyre Windows PowerShell Web Access függő; nem telepített szolgáltatások szükség esetén, külön eltávolíthatja azokat a funkciókat.

## <a name="recommended-quick-uninstallation"></a>Ajánlott (gyors) eltávolítás

Ebben a szakaszban ismertetett eljárások segítségével távolíthatja el:

- a Windows PowerShell Web Access webalkalmazás és
- a Windows PowerShell Web Access szolgáltatás

a Windows PowerShell-parancsmagok használatával.

### <a name="step-1-delete-the-web-application-using-cmdlets"></a>1. lépés: A webalkalmazás-parancsmagok használatával törlése

1. Hajtsa végre az alábbi Windows PowerShell-munkamenet megnyitásához.

    -   A Windows asztalon kattintson a jobb gombbal **Windows PowerShell** a tálcán.

    -   A Windows **Start** kattintson **Windows PowerShell**.

2. Típus `Uninstall-PswaWebApplication`, majd nyomja le az **Enter**.
   1. Ha megadott egy saját, egyéni webhelynevet, a parancshoz adja hozzá a `-WebsiteName` paramétert, és adja meg a webhely nevét.

        `Uninstall-PswaWebApplication -WebsiteName <web-site-name>`
   1. Ha egyéni webalkalmazást használt (nem az alapértelmezett alkalmazás **pswa**, adja hozzá a `-WebApplicationName` paramétert a parancshoz, és adja meg a webalkalmazás nevét.

        `Uninstall-PswaWebApplication -WebApplicationName <web-application-name>`
   1. Ha teszttanúsítványt használ, a parancsmaghoz adja hozzá a `DeleteTestCertificate` paramétert, az alábbi példában látható módon.

        `Uninstall-PswaWebApplication -DeleteTestCertificate`

### <a name="step-2-uninstall-windows-powershell-web-access-using-cmdlets"></a>2. lépés: Távolítsa el a Windows PowerShell Web Access-parancsmagok használatával

1. Hajtsa végre az alábbi Windows PowerShell-munkamenetet emelt szintű felhasználói jogosultsággal nyissa meg. Ha a munkamenet már meg van nyitva, folytassa a következő lépéssel.

    -   A Windows asztalon kattintson a jobb gombbal **Windows PowerShell** a tálcán, és kattintson a **Futtatás rendszergazdaként**.

    -   A Windows **Start** kattintson a jobb gombbal **Windows PowerShell**, és kattintson a **Futtatás rendszergazdaként**.

1. Írja be a következőt, és nyomja le az **Enter**, ahol *számítógép_neve* egy távoli kiszolgálón, amelyről el szeretné távolítani a Windows PowerShell Web Access jelöli. A `-Restart` paraméter automatikusan újraindítja a célkiszolgálót, ha az eltávolításhoz ez szükséges.

        Uninstall-WindowsFeature -Name WindowsPowerShellWebAccess -ComputerName <computer_name> -Restart

    Szerepkörök és szolgáltatások offline virtuális merevlemezről történő eltávolításához adja hozzá a `-ComputerName` és a `-VHD` paramétert is. A(z) `-ComputerName` paraméter a kiszolgáló nevét tartalmazza, amelyhez a VHD-t csatlakoztatni kívánja, a(z) `-VHD` paraméter pedig a VHD-fájl elérési útvonalát tartalmazza a megadott kiszolgálón.

        Uninstall-WindowsFeature -Name WindowsPowerShellWebAccess -VHD <path> -ComputerName <computer_name> -Restart

1. Eltávolítás befejezésekor ellenőrizze, hogy a Windows PowerShell Web Access megnyitásával el a **kiszolgálóinak** lapot a Kiszolgálókezelő, válassza ki a kiszolgálót, amelyről eltávolította a szolgáltatást, és megtekintése a **szerepkörök és Szolgáltatások** csempét a kiválasztott kiszolgálóhoz tartozó lapon.

    Futtathatja a `Get-WindowsFeature` parancsmagot is a kiválasztott kiszolgálóra (Get-WindowsFeature - ComputerName &lt; *számítógép_neve*&gt;) megtekintéséhez a szerepkörök és a kiszolgálón telepítendő szolgáltatásokat.

## <a name="custom-uninstallation"></a>Egyéni eltávolítás

Ebben a szakaszban ismertetett eljárások segítségével távolítsa el a Windows PowerShell Web Access webalkalmazás és az a Windows PowerShell Web Access szolgáltatást a szerepkörök és szolgáltatások varázslót a Kiszolgálókezelőben és az IIS-kezelő konzol használatával.

### <a name="step-1-delete-the-web-application-using-iis-manager"></a>1. lépés: A webalkalmazás, az IIS-kezelő törlése


1. Nyissa meg az IIS-kezelő konzolját a következő módszerek valamelyikével. Ha már meg van nyitva, folytassa a következő lépéssel.

    -   A Windows asztalon indítsa el a Kiszolgálókezelőt kattintva **Kiszolgálókezelő** a Windows tálcán. Az a **eszközök** a Kiszolgálókezelő menüjében kattintson **Internet Information Services (IIS) Manager**.

    -   A Windows **Start** írja be a nevek **Internet Information Services (IIS) Manager**. Kattintson a parancsikonra, amikor az megjelenik a **alkalmazások** eredmények.

1. Az IIS-kezelő fát megjelenítő ablaktáblán válassza ki a Windows PowerShell Web Access webalkalmazást futtató webhelyet.

1. Az a **műveletek** ablaktáblán, a **webhely kezelése**, kattintson a **leállítása**.

1. A fát megjelenítő ablaktáblán kattintson a jobb gombbal a Windows PowerShell Web Access webalkalmazást futtató webhelyen található, és kattintson **eltávolítása**.

1. A fát megjelenítő ablaktáblán jelölje ki **alkalmazáskészletek**válassza ki a Windows PowerShell Web Access alkalmazáskészlet-mappáját **leállítása** a a **műveletek** ablaktáblán, majd  **Távolítsa el** a tartalompanelen.

1. Zárja be az IIS-kezelőt.

> ![Figyelmeztetés megjegyzés](images/SecurityNote.jpeg)**Megjegyzés**:
>
> Az eltávolítás során a rendszer nem törli a tanúsítványt.
>
> Ha önaláírt tanúsítványt hozott létre, vagy a használt teszttanúsítványt el kívánja távolítani, törölje a tanúsítványt az IIS-kezelőben.

### <a name="step-2-uninstall-windows-powershell-web-access-using-the-remove-roles-and-features-wizard"></a>2. lépés: Távolítsa el a Windows PowerShell Web Access szerepkörök és szolgáltatások varázsló segítségével

1. Ha a Kiszolgálókezelő már meg nyitva, folytassa a következő lépéssel. Ha a Kiszolgálókezelő még nincs megnyitva, nyissa meg a következő módszerek valamelyikével.

    -   A Windows asztalon indítsa el a Kiszolgálókezelőt kattintva **Kiszolgálókezelő** a Windows tálcán.

    -   A Windows **Start** kattintson **Kiszolgálókezelő**.

1. Az a **kezelése** menüben kattintson a **szerepkörök és szolgáltatások eltávolítása**.

1. Az a **jelölje be a célkiszolgáló** lapon, válassza ki a kiszolgáló vagy offline VHD-t, amelyről el szeretné távolítani a szolgáltatást. Offline VHD kiválasztásához először válassza ki a kiszolgálót, amelyhez csatlakoztatni kívánja a VHD-t, majd válassza ki a VHD-fájlt. Miután kiválasztotta a célkiszolgálón, kattintson a **következő**.

1. Kattintson a **következő** újra a ugorjon a **szolgáltatások eltávolítása** lap.

1. Törölje a jelölést az **Windows PowerShell Web Access**, és kattintson a **következő**.

1. Az a **erősítse meg a beállításokat** kattintson **eltávolítása**.

## <a name="see-also"></a>Lásd még:

- [Telepítheti és használhatja a Windows PowerShell Web Access](install-and-use-windows-powershell-web-access.md)
- [Az IIS-kezelő 7.0 súgó](https://technet.microsoft.com/library/cc732664.aspx)