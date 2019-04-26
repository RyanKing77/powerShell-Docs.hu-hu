---
title: A PowerShell Core támogatási életciklusa
description: A PowerShell Core támogatási szabályzatok betartatását
ms.date: 08/06/2018
ms.openlocfilehash: 178e5c43520f9a392ca219b9f785eb18b1ec5436
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62086974"
---
# <a name="powershell-core-support-lifecycle"></a>A PowerShell Core támogatási életciklusa

A PowerShell Core a meghatározott készletét eszközök és -összetevők, amely tartalmazza a szükséges, telepítve van, és külön konfigurálni a Windows Powershellből.
Így a PowerShell Core nem szerepel a Windows 7/8.1/10 vagy Windows Server licencelési megállapodások.

Azonban a PowerShell Core a hagyományos Microsoft támogatási szerződés, beleértve a támogatott [A Premier szintű][], [Microsoft Enterprise-megállapodások][enterprise-agreement], és [Microsoft frissítési garanciával rendelkező][assurance].
Is fizethet a szolgáltatásért [tanácsadással][] a PowerShell Core ügyfélszolgálatunknak küldött támogatási kérelmet a problémát.

## <a name="community-support"></a>Közösségi támogatás

Emellett [közösségi támogatás][] a Githubon, ahol egy problémát, programhiba vagy funkcióigénylés fájlt is.
Ezenkívül előfordulhat, a Közösség más tagjai segítséget az általános [A Microsoft Community][] vagy a Microsoft [PowerShell technikai Közösség][].
Nincs garancia van, hogy a Közösség cím vagy a probléma megoldásához időben nem kínál.
Ha azonnali figyelmet igénylő problémával rendelkezik, használja a hagyományos, fizetős támogatási lehetőségek.

## <a name="lifecycle-of-powershell-core"></a>A PowerShell Core élettartama

A PowerShell Core kíván bevezetni a [Microsoft Modern életciklus-szabályzat][modern].
A támogatási életciklusa célja, hogy az ügyfelek naprakészen tartása a legújabb verzióra.

A PowerShell Core verzió 6.x ága körülbelül hat havonta frissül (példák: 6.0-s, 6.1, 6.2, stb.)

> [!IMPORTANT]
> Miután minden egyes új alverzió kiadási támogatás folytatásához hat hónapon belül kell frissíteni.

Például ha a PowerShell Core 6.1-es kiadás dátuma: 2018. július 1., elvárják, hogy a PowerShell Core 6.1-es verzióját 2019. január 1. támogatás frissítéséhez.

> [!IMPORTANT]
> Minden egyes új javítás verziója engedje támogatás folytatásához követő 30 napon belül kell frissíteni.

Például ha futtatja a PowerShell Core 6.1-es és 6.1.3 fel lett oldva, a 2019. február 19., akkor elvárják, hogy a PowerShell Core 6.1.3 által 2019. március 21., amely támogatás a kiadása után 30 nappal való frissítéséhez.
Ha bármely javításokat szükség talál, a javítások a következő összegző frissítés elérhető lesz.

![A PowerShell Core ág életciklusa][lifecycle-chart]

A Modern életciklus-szabályzat is megköveteli, hogy a Microsoft értesítést ügyfelek 12 hónapig előtt megszűnő támogatás a termék (azaz a PowerShell Core).

Idővel várhatóan a alkalmazni a PowerShell Core, a "hosszú távú karbantartási" megközelítést.
A karbantartási módszert használja, az csak karbantartási és biztonsági frissítések belül egy adott ág/verzióját 6.x támogatását lenne szükség van.

## <a name="supported-platforms"></a>Támogatott platformok

Az alábbi táblázat segítségével tekintse meg a platform a verzióját használja a PowerShell Core hivatalosan támogatott.

Közösségünkhöz is hozzájárult a csomagokat, az egyes platformok esetében, de ez nem hivatalosan támogatott.
Ezek a csomagok vannak megjelölve `Community` a táblában.

Felsorolt platformok `Experimental` hivatalosan nem támogatottak, de a Kísérletezési és visszajelzés elérhető.

|                                                   | 6.1         | 6.2         |
|---------------------------------------------------|:-----------:|:-----------:|
| Windows 7, 8.1 és 10                            | Támogatott   | Támogatott   |
| Windows Server 2008 R2, 2012 R2, 2016             | Támogatott   | Támogatott   |
| [A Windows Server féléves csatorna][semi-annual] | Támogatott   | Támogatott   |
| Ubuntu 16.04 és 18.04                            | Támogatott   | Támogatott   |
| Ubuntu 18.10 (keresztül Számértékekhez igazodnak, a csomag)                   | Közösségi   | Közösségi   |
| Debian 9                                          | Támogatott   | Támogatott   |
| CentOS 7                                          | Támogatott   | Támogatott   |
| Red Hat Enterprise Linux 7                        | Támogatott   | Támogatott   |
| openSUSE 42.3                                     | Támogatott   | Támogatott   |
| Fedora 28                                         | Támogatott   | Támogatott   |
| macOS 10.12 +                                      | Támogatott   | Támogatott   |
| Arch                                              | Közösségi   | Közösségi   |
| Raspbian                                          | Közösségi   | Közösségi   |
| Kali                                              | Közösségi   | Közösségi   |
| AppImage (több Linux platformon működik)     | Közösségi   | Közösségi   |
| [Oszlopokhoz illesztés csomag](https://snapcraft.io/powershell)   | Lásd a megjegyzést    | Lásd a megjegyzést    |

> [!NOTE]
> Oszlopokhoz illesztés csomagok támogatottak ugyanaz, mint a terjesztési futtat a csomagot.

## <a name="powershell-release-end-of-life"></a>PowerShell kiadás végéhez közeledik

Alapján [a PowerShell Core életciklus](#lifecycle-of-powershell-core), az alábbi táblázat tartalmazza a dátumokat, amikor különböző kiadás már nem lesz támogatott.

| Verzió | Élettartam végéhez közeledik                   |
|---------|-------------------------------|
| 6.0     | 2019. február 13.             |
| 6.1     | 2019. szeptember 28.            |
| 6.2     | 6 hónapon belül 6.3-kiadások   |

## <a name="platforms-which-are-out-of-support"></a>A nem támogatott platformokon

Amikor egy platformverzió eléri a teljes életciklusa, a platform tulajdonosa által meghatározott, a PowerShell Core is megszűnik a platform verzió támogatására.
Korábban kiadott csomagok továbbra is elérhető marad a hozzáférés, de a hivatalos támogatási ügyfeleket, és bármilyen típusú frissítések már nem adható meg.

Így a terjesztési tulajdonosai a következő verziók támogatása véget ért, és nem támogatottak.

| Operációs rendszer       | Verzió | Élettartam végéhez közeledik                                                                                 |
|----------|---------|---------------------------------------------------------------------------------------------|
| Fedora   | 24      | [2017. augusztus](https://fedoramagazine.org/fedora-24-eol/)                                    |
| Fedora   | 25      | [2017. december](https://fedoramagazine.org/fedora-25-end-life/)                             |
| Fedora   | 26      | [2018. május](https://fedoramagazine.org/fedora-26-end-life/)                                  |
| openSUSE | 42.1    | [2017. május](https://lists.opensuse.org/opensuse-security-announce/2017-05/msg00053.html)     |
| openSUSE | 42.2    | [2018. január](https://lists.opensuse.org/opensuse-security-announce/2017-11/msg00066.html) |
| Ubuntu   | 16.10   | [2017. július](https://lists.ubuntu.com/archives/ubuntu-announce/2017-July/000223.html)        |
| Ubuntu   | 17.04   | [2018. január](https://lists.ubuntu.com/archives/ubuntu-announce/2018-January.txt)          |
| Ubuntu   | 17.10   | [2018. július](https://lists.ubuntu.com/archives/ubuntu-announce/2018-July/000232.html)        |
| Debian   | 8       | [2018. június](https://lists.debian.org/debian-security-announce/2018/msg00132.html)           |
| Fedora   | 27      | [A 2018. november](https://fedoramagazine.org/fedora-27-end-of-life/)                          |
| Ubuntu   | 14.04   | [Április 2019](https://wiki.ubuntu.com/Releases)                                              |

## <a name="notes-on-licensing"></a>Tudnivalók a licencelés

A PowerShell Core alatt jelent a [MIT licenccel][].
Jelen licenc, és egy fizetős támogatási megállapodás nélkül, a felhasználók korlátozva, [közösségi támogatás][].
Közösségi támogatás, a Microsoft nem vállal garanciát válaszkészségének vagy javításokat nem.

## <a name="windows-powershell-module"></a>Windows PowerShell-modul

Támogatja a PowerShell Core nem tartalmazza a termék-modulok, ha az ilyen modulokhoz explicit módon támogatja a PowerShell Core.
Például a `ActiveDirectory` modul részét képező Windows Server része nem támogatott forgatókönyv szerint.

Előfordulhat azonban, a PowerShell Core explicit módon nem támogató modulok kompatibilis bizonyos esetekben.
Telepítse a [ `WindowsPSModulePath` ][] modult, hozzáadhatja a Windows PowerShell `PSModulePath` , a PowerShell Core `PSModulePath`.

Először telepítse a `WindowsPSModulePath` modul a PowerShell-galériából:

```powershell
# Add `-Scope CurrentUser` if you're installing as non-admin
Install-Module WindowsPSModulePath -Force
```

Ez a modul telepítése után futtassa a `Add-WindowsPSModulePath` adja hozzá a Windows PowerShell-parancsmagot `PSModulePath` a PowerShell Core:

```powershell
# Add this line to your profile if you always want Windows PowerShell PSModulePath
Add-WindowsPSModulePath
```

## <a name="experimental-features"></a>Kísérleti funkciók

[Kísérleti funkciók][] korlátozódnak [közösségi támogatás](#community-support).

[A Premier szintű]: https://www.microsoft.com/en-us/microsoftservices/support.aspx
[enterprise-agreement]: https://www.microsoft.com/en-us/licensing/licensing-programs/enterprise.aspx
[assurance]: https://www.microsoft.com/en-us/licensing/licensing-programs/software-assurance-default.aspx
[Közösségi támogatás]: https://github.com/powershell/powershell/issues
[A Microsoft Community]: https://answers.microsoft.com/
[PowerShell technikai Közösség]: https://techcommunity.microsoft.com/t5/PowerShell/ct-p/WindowsPowerShell
[tanácsadással]: https://support.microsoft.com/assistedsupportproducts
[modern]: https://support.microsoft.com/help/30881/modern-lifecycle-policy
[lifecycle-chart]: ./images/modern-lifecycle.png
[semi-annual]: https://docs.microsoft.com/windows-server/get-started/semi-annual-channel-overview
[MIT licenccel]: https://github.com/PowerShell/PowerShell/blob/master/LICENSE.txt
[`WindowsPSModulePath`]: https://www.powershellgallery.com/packages/WindowsPSModulePath/
[Kísérleti funkciók]: /powershell/module/microsoft.powershell.core/about/about_powershell_config?view=powershell-6#experimentalfeatures
