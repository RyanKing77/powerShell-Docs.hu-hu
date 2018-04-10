---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 306241bc5ec854c0e2ed835009a79b21fc249f14
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="known-issues-and-limitations"></a>Ismert problémák és korlátozások

<a name="powershell-shortcuts-are-broken-when-used-for-the-first-time"></a>PowerShell parancsikonok nem működik, ha először használja
------------------------------------------------------------

**Megoldás:** hajtsa végre az alábbi műveletek egyikét:

1.  Kattintson a jobb gombbal a PowerShell helyi. Válassza ki a "Windows PowerShell" nem emelt szintű módban elindításához.
2.  Kattintson a jobb gombbal a PowerShell helyi. Kattintson jobb gombbal a "Windows PowerShell", és válassza a "Futtatás rendszergazdaként" elindítani egy emelt jogosultságszintű módban.

Miután elvégezte a fenti műveletek valamelyikét, a PowerShell parancsikonok fog működni. Ezeket a műveleteket kell csak egyszer hajtható végre.


<a name="powershell-modules-and-dsc-resources-report-errors-about-executionpolicy-on-windows-7"></a>PowerShell-modulok és a DSC-erőforrások hibákat vonatkozó végrehajtási házirend a Windows 7
-------------------------------------------------------------------------------------
A Windows 7 a PowerShell-modulok és a DSC-erőforrások ExecutionPolicy kapcsolatos jelentett hibákat eredményezhet.

**Megoldás:** a végrehajtási házirend beállítása remotesigned legyen a következő parancs futtatásával egy rendszergazda jogú PowerShell-munkamenetben (Futtatás rendszergazdaként):

```powershell
Set-ExecutionPolicy RemoteSigned
```

<a name="connecting-to-an-old-remote-exchange-endpoint-causes-a-crash"></a>Kapcsolódás a régi távoli Exchange végpont hatására crash
------------------------------------------------------------

A régi Exchange végpont átirányítja egy új végpontot. Legyen hiba a átirányítása logic adott eredmények crash.

**Megoldás:** közvetlenül kapcsolódjon az új végpont.


<a name="software-inventory-logging-feature-is-erroneously-stopped-after-wmf-50-installation-on-windows-server-2012-r2"></a>Szoftver szoftverleltár-naplózási szolgáltatás tévesen le van állítva a Windows Server 2012 R2 WMF 5.0 telepítése után
-------------------------------------------------------------------------------------------------------------

A Windows Server 2012 R2, a szoftverleltár-Naplózás már futó WMF 5.0 telepítésekor a szoftverleltár-naplózási szolgáltatás tévesen leáll a telepítés után.

**Megoldás:** futtassa a Start-SilLogging parancsmagot a WMF telepítése után egyszer, mivel a telepítési folyamat protokollüzenetet leállítja a szoftverleltár-naplózási szolgáltatás.

<a name="get-childitem-does-not-work-if--literalpath-and--recurse-are-used-together"></a>Get-ChildItem - LiteralPath és - Recurse együttes használatakor nem működik
--------------------------------------------------------------------------

Ha a könyvtár neve érvénytelen helyettesítő karaktert tartalmaz, majd Get-ChildItem fog nem megfelelő eredményeket ha egyaránt - LiteralPath és - Recurse együtt használja.

**Megoldás:** nem ideális, de a jelenlegi megoldás, hogy a rekurzió megvalósításához a parancsfájlban szereplő támaszkodnak a parancsmag helyett.


<a name="sysprep-fails-after-wmf-50-installation"></a>A Sysprep nem sikerül WMF 5.0 telepítése után
----------------------------------------

Két lehetséges megoldások a Windows Server futtatott verziójától függően probléma van.

**Megoldás:**
- Operációs rendszer **Windows Server 2008 R2**
  1. Nyissa meg a Powershellt rendszergazdaként
  2. A következő parancsot

  ```powershell
    Set-SilLogging –TargetUri https://BlankTarget –CertificateThumbprint 0123456789
  ```
  3. Futtassa a parancsot, és a hiba figyelmen kívül hagyja a rendszer megfelelően.

  ```powershell
    Publish-SilData
   ```
  4. A \Windows\System32\Logfiles\SIL\ könyvtárban található fájlok törlése

  ```powershell
    Remove-Item -Recurse $env:SystemRoot\System32\Logfiles\SIL\
  ```
  5. Az összes rendelkezésre álló fontos Windows-frissítések telepítéséhez, és a Sysyprep művelet általában megkezdéséhez.

- Operációs rendszer **Windows Server 2012-ben**
  1.    Miután telepítette a WMF 5.0 kell lennie a kiszolgálón a Sysprep d, rendszergazdaként jelentkezzen be.
  2.    Másolása Generize.xml directory \Windows\System32\Sysprep\ActionFiles\ kívül a Windows könyvtárban, a C:\ helyre például.
  3.    Nyissa meg a Generalize.xml másolása a Jegyzettömbbel.
  4.    Keresse meg, és távolítsa el a következő szöveg, amelyet minden kell törölni egy példányát (fogják a dokumentum végére mellett).

    ```
    <sysprepOrder order="0x3200"></sysprepOrder>
    <sysprepOrder order="0x3300"></sysprepOrder>
    ```

  5.    A Generalize.xml a módosított tartalom mentéséhez, majd zárja be a fájlt.
  6.    Nyisson meg egy parancssort rendszergazdaként
  7.    A következő parancsot a Generalize.xml fájl kihasználva saját tulajdonába vesz a system32 mappába:

    ```
    Takeown /f C:\Windows\System32\Sysprep\ActionFiles\Generalize.xml
    ```

  8.    A következő paranccsal állítsa be a megfelelő engedéllyel a fájlra:

    ```
    Cacls C:\Windows\System32\ Sysprep\ActionFiles\Generalize.xml /G `<AdministratorUserName>`:F
    ```
      * A parancssorba igennel válaszol megerősítést kér.
      * Vegye figyelembe, hogy `<AdministratorUserName>` a felhasználónév, a számítógépen rendszergazdai jogosultságokkal kell helyettesíteni. Például "Rendszergazda".

  9.    Másolja a fájlt, szerkeszteni és felülírta a Sysprep szolgáltatás segítségével a következő parancsot:

    ```
    xcopy C:\Generalize.xml C:\Windows\System32\Sysprep\ActionFiles\Generalize.xml
    ```
      * Igen választja, felülírja (vegye figyelembe, hogy ha felülírja, kérdés nélkül ellenőrizheti a megadott elérési).
      * Azt feltételezi, hogy a módosított tartalom Generalize.xml a C:\ lett másolva.

  10.   A megoldás generalize.XML most frissül. Futtassa a Sysprep a generalize beállítás engedélyezve van.