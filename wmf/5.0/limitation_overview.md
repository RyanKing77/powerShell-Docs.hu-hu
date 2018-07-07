---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 4eb2f0bac4f2169a9a06d80cb4fa214a09cdfa86
ms.sourcegitcommit: 8b076ebde7ef971d7465bab834a3c2a32471ef6f
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/06/2018
ms.locfileid: "37892984"
---
# <a name="known-issues-and-limitations"></a>Ismert problémák és korlátozások

## <a name="powershell-shortcuts-are-broken-when-used-for-the-first-time"></a>PowerShell-parancsikon nem működik, ha először használja

**Megoldás:** hajtsa végre az alábbi műveletek egyikét:

1. Kattintson a jobb gombbal a PowerShell-parancsikon. Válassza ki a "Windows PowerShell" nem emelt szintű üzemmódban indult el.
2. Kattintson a jobb gombbal a PowerShell-parancsikon. A jobb gombbal a "Windows PowerShell", és válassza ki a "Futtatás rendszergazdaként" egy emelt jogosultságszintű módban indult el.

Miután elvégezte a fenti műveletek valamelyikét, a PowerShell-parancsikon fog működni. Ezek a műveletek kell csak egyszer kell elvégezni.

## <a name="powershell-modules-and-dsc-resources-report-errors-about-executionpolicy-on-windows-7"></a>Windows 7-es ExecutionPolicy kapcsolatos hibák PowerShell-modulok és a DSC-erőforrások jelentése

Windows 7, a PowerShell-modulok és a DSC-erőforrások használatának kapcsolatos ExecutionPolicy jelentett hibákat eredményezhet.

**Megoldás:** a végrehajtási házirend beállítása RemoteSigned értékre a következő parancs futtatásával egy rendszergazda jogú PowerShell-munkamenetben (Futtatás rendszergazdaként):

```powershell
Set-ExecutionPolicy RemoteSigned
```

## <a name="connecting-to-an-old-remote-exchange-endpoint-causes-a-crash"></a>Csatlakozik a távoli régi Exchange végpont hatására összeomlás

A régi Exchange végpont átirányítja a felhasználókat az új végpont. Nincs hibát az átirányítás logika az adott eredmények összeomlás.

**Megoldás:** közvetlenül csatlakozhat az új végpont.

## <a name="software-inventory-logging-feature-is-erroneously-stopped-after-wmf-50-installation-on-windows-server-2012-r2"></a>Szoftver a szoftverleltár-naplózás szolgáltatás hibásan le van állítva a Windows Server 2012 R2 a WMF 5.0-s a telepítést követően

A WMF 5.0 telepíti egy Windows Server 2012 R2, a szoftverleltár-Naplózás már futó, amikor a szoftverleltár-naplózás szolgáltatás hibásan leállt a telepítés után.

**Megoldás:** futtassa a Start-SilLogging parancsmagot a WMF telepítése után egyszer, mivel a telepítési folyamat protokollüzenetet le fog állni a szoftverleltár-naplózás funkció.

## <a name="get-childitem-does-not-work-if--literalpath-and--recurse-are-used-together"></a>`Get-ChildItem` nem működik – LiteralPath és - Recurse együttes használatakor

Ha a könyvtár neve érvénytelen helyettesítő karaktert tartalmaz, majd `Get-ChildItem` nem tudott várt eredmény, mind - LiteralPath és - Recurse együtt használva.

**Megoldás:** nem ideális, de a jelenlegi megkerülő megoldás az, hogy a rekurzió megvalósítása a szkriptben a parancsmag támaszkodjon helyett.

## <a name="sysprep-fails-after-wmf-50-installation"></a>A Sysprep nem sikerül, a WMF 5.0-s a telepítést követően

Nincsenek futtatja a Windows Server verziójától függően a probléma két lehetséges megoldásai.

**Megoldás:**

- Operációs rendszer **Windows Server 2008 R2**
  1. Nyissa meg a Powershellt rendszergazdaként
  2. A következő parancs futtatásával

     ```powershell
     Set-SilLogging –TargetUri https://BlankTarget –CertificateThumbprint 0123456789
     ```

  3. Futtassa a parancsot, és a hiba figyelmen kívül hagyja a rendszer elvárt.

     ```powershell
     Publish-SilData
     ```

  4. A \Windows\System32\Logfiles\SIL\ könyvtárban található fájlok törlése

     ```powershell
     Remove-Item -Recurse $env:SystemRoot\System32\Logfiles\SIL\
     ```

  5. Telepítse az összes rendelkezésre álló fontos Windows frissítést, és Sysyprep művelet általában megkezdéséhez.

- Operációs rendszer **Windows Server 2012**
  1. A kiszolgálóra, hogy a WMF 5.0 telepítését követően a Sysprep d, bejelentkezés rendszergazdaként.
  2. Másolja Generize.xml directory \Windows\System32\Sysprep\ActionFiles\ kívül a Windows könyvtárban, a C:\ helyre például.
  3. Nyissa meg a Generalize.xml Másolás a Jegyzettömb alkalmazásban.
  4. Keresse meg, és távolítsa el a következő szöveget, minden egyes kell törölni egy példányát (fogják a dokumentum végén).

     ```xml
     <sysprepOrder order="0x3200"></sysprepOrder>
     <sysprepOrder order="0x3300"></sysprepOrder>
     ```

  5. A módosított tartalom mentéséhez Generalize.xml, és zárja be a fájlt.
  6. Nyisson meg egy parancssort rendszergazdaként
  7. Futtassa a következő parancsot a system32 mappába a Generalize.xml fájl saját tulajdonba:

     ```powershell
     Takeown /f C:\Windows\System32\Sysprep\ActionFiles\Generalize.xml
     ```

  8. Futtassa a következő parancsot a fájl a megfelelő engedély beállítása:

     ```powershell
     Cacls C:\Windows\System32\ Sysprep\ActionFiles\Generalize.xml /G `<AdministratorUserName>`:F
     ```

     - Igennel amikor a rendszer megerősítést kér.
     - Vegye figyelembe, hogy `<AdministratorUserName>` a felhasználónevet, a rendszergazda a számítógépen kell helyettesíteni. Például "Administrator".

  9. Másolja a fájlt, szerkeszthetők, és a mentett keresztül a Sysprep-könyvtár a következő paranccsal:

     ```powershell
     xcopy C:\Generalize.xml C:\Windows\System32\Sysprep\ActionFiles\Generalize.xml
     ```

     - Igen választja, felülírja (vegye figyelembe, hogy ha a kérés nem azt felülírni, gondosan ellenőrizze a megadott elérési).
     - Azt feltételezi, hogy a Generalize.xml szerkesztett másolatát másolta C:\.

  10. Generalize.XML most frissült a megkerülő megoldás. Futtassa a Sysprep a generalize beállítás engedélyezve van.