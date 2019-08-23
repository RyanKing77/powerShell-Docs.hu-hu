---
title: A PowerShell Core támogatási életciklusa
description: A PowerShell Core támogatását szabályozó házirendek
ms.date: 08/06/2018
ms.openlocfilehash: 60999ed54ca3be15232ffee3ab0c49cb94873a8f
ms.sourcegitcommit: 5a004064f33acc0145ccd414535763e95f998c89
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/23/2019
ms.locfileid: "69986735"
---
# <a name="powershell-core-support-lifecycle"></a>A PowerShell Core támogatási életciklusa

A PowerShell Core a Windows PowerShelltől különállóan szállított, telepített és konfigurált eszközök és összetevők különálló készlete. Így a PowerShell Core nem szerepel a Windows 7/8.1/10 vagy a Windows Server licencszerződésekben.

A PowerShell Core azonban a hagyományos Microsoft-támogatási szerződések keretében támogatott, beleértve a [Premier][], a [Microsoft][enterprise-agreement]nagyvállalati szerződéseit és a [Microsoft frissítési garanciát][assurance].
A PowerShell Core-hoz nyújtott [segítséget][] a támogatási kérelem bejelentésével is kifizetheti a problémához.

## <a name="community-support"></a>Közösségi támogatás

Emellett [közösségi támogatást][] is kínálunk a githubon, ahol a probléma, a hiba vagy a szolgáltatásra vonatkozó kérések is beszerezhetők.
Emellett a Közösség más tagjaitól is találhat segítséget az általános [Microsoft Közösség][] vagy a Microsoft [PowerShell-technikai Közösség][]számára. Nem vállalunk garanciát arra, hogy a Közösség kellő időben kezeli vagy megoldja a problémát. Ha probléma merül fel, azonnali figyelmet igényel, használja a hagyományos, fizetős támogatási lehetőségeket.

## <a name="lifecycle-of-powershell-core"></a>A PowerShell Core életciklusa

A PowerShell Core a [Microsoft modern életciklus][modern]-szabályzatát fogadja el. A támogatási életciklus célja, hogy az ügyfelek naprakészen maradjanak a legújabb verziókkal.

A PowerShell Core 6-os. x verziójú ága körülbelül hat havonta frissül (például: 6,0, 6,1, 6,2 stb.)

> [!IMPORTANT]
> Az új alverziók kiadása után hat hónapon belül frissítenie kell a támogatás folytatását.

Ha például a PowerShell Core 6,1-es verziójának kiadása a 2018-es július 1-jén történik, akkor a támogatás fenntartása érdekében várhatóan a PowerShell Core 6,1-ra kell frissítenie. január 2019 1-től.

> [!IMPORTANT]
> Az új javítások kiadása után 30 napon belül frissítenie kell a támogatást.

Ha például a PowerShell Core 6,1-et futtatja, és a 6.1.3 a 2019-es február 19-én adták ki, a PowerShell Core 6.1.3-re a 2019-as március 21-én kell frissíteni, amely a kiadás után 30 nappal a támogatás fenntartásához szükséges. Ha a rendszer a szükséges javításokat kéri, a javítások a következő összesített frissítésben jelennek meg.

A modern életciklus-szabályzat azt is megköveteli, hogy a Microsoft az ügyfelek számára 12 hónapos értesítést nyújtson a termék (azaz a PowerShell Core) támogatásának megszüntetése előtt.

Végül a PowerShell Core várhatóan a hosszú távú karbantartási megközelítést fogja alkalmazni. Ebben a karbantartási megközelítésben csak a karbantartási és biztonsági frissítéseket kell megkövetelni a 6. x adott ág/verziójának támogatásában.

## <a name="supported-platforms"></a>Támogatott platformok

Annak ellenőrzéséhez, hogy a PowerShell Core platformja és verziója hivatalosan támogatott-e, tekintse meg a következő táblázatot.

A Közösség bizonyos platformokhoz is felvette a csomagokat, de hivatalosan nem támogatott. Ezek a csomagok a táblázatban `Community` látható módon vannak megjelölve.

A felsorolt `Experimental` platformok nem támogatottak, de kísérletezéshez és visszajelzésekhez is elérhetők.

| Platform                                          | 6.1         | 6.2         |
|---------------------------------------------------|:-----------:|:-----------:|
| Windows 7, 8,1 és 10                            | Támogatott   | Támogatott   |
| Windows Server 2008 R2, 2012 R2, 2016             | Támogatott   | Támogatott   |
| [Windows Server féléves csatorna][semi-annual] | Támogatott   | Támogatott   |
| Ubuntu 16,04 és 18,04                            | Támogatott   | Támogatott   |
| Ubuntu 18,10 (snap-csomagon keresztül)                   | Közösségi   | Közösségi   |
| Ubuntu 19,04 (snap-csomagon keresztül)                   | Közösségi   | Közösségi   |
| Debian 9                                          | Támogatott   | Támogatott   |
| CentOS 7                                          | Támogatott   | Támogatott   |
| Red Hat Enterprise Linux 7                        | Támogatott   | Támogatott   |
| openSUSE 42,3                                     | Támogatott   | Támogatott   |
| Fedora 28                                         | Támogatott   | Támogatott   |
| macOS 10.12 +                                      | Támogatott   | Támogatott   |
| Arch                                              | Közösségi   | Közösségi   |
| Raspbian                                          | Közösségi   | Közösségi   |
| Kali                                              | Közösségi   | Közösségi   |
| AppImage (több Linux platformon is működik)      | Közösségi   | Közösségi   |
| [Csomag igazítása](https://snapcraft.io/powershell)   | Lásd: Megjegyzés    | Lásd: Megjegyzés    |

> [!NOTE]
> Az illesztési csomagok ugyanúgy működnek, mint a csomagot futtató disztribúció.

## <a name="powershell-releases-end-of-life"></a>A PowerShell élettartama megszűnik

A [PowerShell Core életciklusa](#lifecycle-of-powershell-core)alapján a következő táblázat felsorolja azokat a dátumokat, amikor a különböző kiadások már nem lesznek támogatottak.

| Verzió | Élettartam vége                   |
|---------|-------------------------------|
| 6.0     | Február 13., 2019             |
| 6.1     | Szeptember 28., 2019            |
| 6.2     | 6 hónappal 7 kiadás után     |

## <a name="unsupported-platforms"></a>Nem támogatott platformok

Ha egy platform verziója a platform tulajdonosa által meghatározott élettartamot ér el, a PowerShell Core is megszűnik a platform verziójának támogatásához. A korábban kiadott csomagok továbbra is elérhetők lesznek azon ügyfelek számára, akiknek hozzáférésre van szükségük, de a formális támogatás és az ilyen jellegű frissítések már nem lesznek biztosítva.

Így a terjesztési tulajdonosok a következő verziókra vonatkozóan befejezték a támogatást, és nem támogatottak.

| Platform | Verzió | Elhasználódott                                                                                 |
|----------|---------|---------------------------------------------------------------------------------------------|
| Fedora   | 24      | [Augusztus 2017](https://fedoramagazine.org/fedora-24-eol/)                                    |
| Fedora   | 25      | [December 2017](https://fedoramagazine.org/fedora-25-end-life/)                             |
| Fedora   | 26      | [2018. május](https://fedoramagazine.org/fedora-26-end-life/)                                  |
| openSUSE | 42.1    | [2017. május](https://lists.opensuse.org/opensuse-security-announce/2017-05/msg00053.html)     |
| openSUSE | 42,2    | [Január 2018](https://lists.opensuse.org/opensuse-security-announce/2017-11/msg00066.html) |
| Ubuntu   | 16,10   | [Július 2017](https://lists.ubuntu.com/archives/ubuntu-announce/2017-July/000223.html)        |
| Ubuntu   | 17,04   | [Január 2018](https://lists.ubuntu.com/archives/ubuntu-announce/2018-January.txt)          |
| Ubuntu   | 17,10   | [Július 2018](https://lists.ubuntu.com/archives/ubuntu-announce/2018-July/000232.html)        |
| Debian   | 8       | [Június 2018](https://lists.debian.org/debian-security-announce/2018/msg00132.html)           |
| Fedora   | 27      | [November 2018](https://fedoramagazine.org/fedora-27-end-of-life/)                          |
| Ubuntu   | 14.04   | [Április 2019](https://wiki.ubuntu.com/Releases)                                              |

## <a name="notes-on-licensing"></a>Megjegyzések a licenceléshez

A PowerShell Core az [mit licenc][]alatt jelenik meg. A licenc keretében és a fizetős támogatási szerződés nélkül a felhasználók a [közösségi támogatást][]korlátozódnak. A közösségi támogatással a Microsoft nem vállal garanciát a válaszadásra vagy a javításokra.

## <a name="windows-powershell-module"></a>Windows PowerShell-modul

A PowerShell Core-támogatás nem tartalmazza a termék moduljait, kivéve, ha ezek a modulok kifejezetten támogatják a PowerShell Core-t. Például a `ActiveDirectory` Windows Server részét képező modul használata nem támogatott forgatókönyv.

Bizonyos esetekben azonban a PowerShell Core-t nem támogató modulok is kompatibilisek lehetnek. A [`WindowsPSModulePath`][] modul telepítésével felveheti a Windows PowerShellt `PSModulePath` a PowerShell Core `PSModulePath`-ba.

Először telepítse a `WindowsPSModulePath` modult a PowerShell-galériaról:

```powershell
# Add `-Scope CurrentUser` if you're installing as non-admin
Install-Module WindowsPSModulePath -Force
```

A modul telepítése után a `Add-WindowsPSModulePath` parancsmag futtatásával adja hozzá a Windows PowerShellt `PSModulePath` a PowerShell Core-hoz:

```powershell
# Add this line to your profile if you always want Windows PowerShell PSModulePath
Add-WindowsPSModulePath
```

## <a name="experimental-features"></a>Kísérleti funkciók

A [kísérleti funkciók][] a [közösségi támogatásra](#community-support)korlátozódnak.

[Premier]: https://www.microsoft.com/en-us/microsoftservices/support.aspx
[enterprise-agreement]: https://www.microsoft.com/en-us/licensing/licensing-programs/enterprise.aspx
[assurance]: https://www.microsoft.com/en-us/licensing/licensing-programs/software-assurance-default.aspx
[közösségi támogatást]: https://github.com/powershell/powershell/issues
[Microsoft Közösség]: https://answers.microsoft.com/
[PowerShell-technikai Közösség]: https://techcommunity.microsoft.com/t5/PowerShell/ct-p/WindowsPowerShell
[segítséget]: https://support.microsoft.com/assistedsupportproducts
[modern]: https://support.microsoft.com/help/30881/modern-lifecycle-policy
[lifecycle-chart]: ./images/modern-lifecycle.png
[semi-annual]: https://docs.microsoft.com/windows-server/get-started/semi-annual-channel-overview
[MIT licenc]: https://github.com/PowerShell/PowerShell/blob/master/LICENSE.txt
['WindowsPSModulePath']: https://www.powershellgallery.com/packages/WindowsPSModulePath/
[Kísérleti funkciók]: /powershell/module/microsoft.powershell.core/about/about_powershell_config?view=powershell-6#experimentalfeatures
