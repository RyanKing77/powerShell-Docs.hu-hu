# <a name="powershell-core-support-lifecycle"></a>A PowerShell Core támogatási életciklusa

A PowerShell Core a meghatározott készletét eszközök és -összetevők, amely tartalmazza a szükséges, telepítve van, és külön konfigurálni a Windows Powershellből.
Ezért a PowerShell Core nem szerepel a Windows 7/8.1/10 vagy Windows Server licencelési megállapodások.

Azonban a PowerShell Core a hagyományos Microsoft támogatási szerződés, beleértve a támogatott [A Premier szintű][], [Microsoft Enterprise-megállapodások][enterprise-agreement], és [Microsoft frissítési garanciával rendelkező][assurance].
Is fizethet a szolgáltatásért [tanácsadással][] a PowerShell Core ügyfélszolgálatunknak küldött támogatási kérelmet a problémát.

Emellett [közösségi támogatás][] a Githubon, ahol egy problémát, programhiba vagy funkcióigénylés fájlt is.
Is előfordulhat, hogy megtalálja a Közösség más tagjai segítséget az általános [A Microsoft Community][] vagy a Microsoft [PowerShell technikai Közösség][].
Nem kínál nincs garancia van, hogy a probléma megoldásához címzett vagy időben fog állni.
Ha azonnali figyelmet igénylő problémával rendelkezik, használja a hagyományos, fizetős támogatási lehetőségek.

## <a name="lifecycle-of-powershell-core"></a>A PowerShell Core élettartama

A PowerShell Core kíván bevezetni a [Microsoft Modern életciklus-szabályzat][modern].
A támogatási életciklusa célja, hogy az ügyfelek naprakészen tartása a legújabb verzióra.

A PowerShell Core verzió 6.x ága körülbelül hat havonta frissül (pl. 6.0-s, 6.1, 6.2, stb.)

> [!IMPORTANT]
> Miután minden egyes új alverzió kiadási támogatás folytatásához hat hónapon belül kell frissíteni.

Például ha a PowerShell Core 6.1-es kiadás dátuma: 2018. július 1-től., akkor elvárják, hogy frissítheti a PowerShell Core 6.1-es verzióját 2019. január 1-től. a támogatás.

![A PowerShell Core ág életciklusa][lifecycle-chart]

A Modern életciklus-szabályzat is megköveteli, hogy a Microsoft értesítést ügyfelek 12 hónapig előtt megszűnő támogatás a termék (azaz a PowerShell Core).

Idővel várhatóan a alkalmazni a PowerShell Core, a "hosszú távú karbantartási" megközelítést kellene, hogy csak a karbantartási és biztonsági frissítések belül egy adott ág/verzióját 6.x támogatását.

## <a name="supported-platforms"></a>Támogatott platformok

Tekintse át az alábbi táblázat megtekintéséhez használja a PowerShell Core verziója hivatalosan támogatott platform.

Közösségünkhöz is hozzájárult a csomagokat, az egyes platformok esetében, de ez nem hivatalosan támogatott.
Ezek a csomagok vannak megjelölve `Community` a táblában.

Felsorolt platformok `Experimental` hivatalosan nem támogatottak, de a Kísérletezési és visszajelzés elérhető.

|                                                   | 6.0         | 6.1         |
|---------------------------------------------------|:-----------:|:-----------:|
| Windows 7, 8.1 és 10                            | Támogatott   | Támogatott   |
| Windows Server 2008 R2, 2012 R2, 2016             | Támogatott   | Támogatott   |
| [A Windows Server féléves csatorna][semi-annual] | Támogatott   | Támogatott   |
| Ubuntu 14.04, és 16.04                           | Támogatott   | Támogatott   |
| Ubuntu 17.10 és 18.04                           |             | Támogatott   |
| Debian 8.7 + és 9                                | Támogatott   | Támogatott   |
| CentOS 7                                          | Támogatott   | Támogatott   |
| Red Hat Enterprise Linux 7                        | Támogatott   | Támogatott   |
| OpenSUSE 42.3                                     | Támogatott   | Támogatott   |
| Fedora 27                                         | Támogatott   | Támogatott   |
| 28 Fedora                                         |             | Támogatott   |
| macOS 10.12 +                                      | Támogatott   | Támogatott   |
| Arch                                              | Közösség   | Közösség   |
| Raspbian                                          | Kísérleti| Közösség   |
| Kali                                              | Közösség   | Közösség   |
| AppImage (több Linux platformon működik)     | Közösség   | Közösség   |

## <a name="platform-which-are-out-of-support"></a>Platform, amely nem támogatott

Amikor egy platformverzió eléri a teljes életciklusa a platform tulajdonosa által meghatározott, a PowerShell Core is megszűnik támogatást nyújt a platform verziója. Korábban kiadott csomagok továbbra is elérhető marad a hozzáférés, de a hivatalos támogatási ügyfeleket, és bármilyen típusú frissítések már nem adható meg.

Ezért támogatja a következő verziók által a terjesztési tulajdonosok befejeződött, és nem támogatottak.

| Operációs rendszer       | Verzió | Élettartam végéhez közeledik                                                                                 |
|----------|---------|---------------------------------------------------------------------------------------------|
| Fedora   | 26      | [2018. május](https://fedoramagazine.org/fedora-26-end-life/)                                  |
| Fedora   | 25      | [2017. december](https://fedoramagazine.org/fedora-25-end-life/)                             |
| Fedora   | 24      | [2017. augusztus](https://fedoramagazine.org/fedora-24-eol/)                                    |
| OpenSUSE | 42.2    | [2018. január](https://lists.opensuse.org/opensuse-security-announce/2017-11/msg00066.html) |
| OpenSUSE | 42.1    | [2017. május](https://lists.opensuse.org/opensuse-security-announce/2017-05/msg00053.html)     |
| Ubuntu   | 17.04   | [2018. január](https://lists.ubuntu.com/archives/ubuntu-announce/2018-January.txt)          |
| Ubuntu   | 16.10   | [2017. július](https://lists.ubuntu.com/archives/ubuntu-announce/2017-July/000223.html)        |

## <a name="notes-on-licensing"></a>Tudnivalók a licencelés

A PowerShell Core alatt jelent a [MIT licenccel][].
Jelen licenc, és a egy fizetős támogatási szerződés hiányában a felhasználók korlátozva, [közösségi támogatás][].
Közösségi támogatás, a Microsoft nem vállal garanciát válaszkészségének vagy javításokat nem.

## <a name="windows-powershell-module"></a>Windows PowerShell-modul

Támogatja a PowerShell Core nem terjed ki a többi termék modulok, ha az ilyen modulokhoz explicit módon támogatja a PowerShell Core.
Például a `ActiveDirectory` modul részét képező Windows Server része nem támogatott forgatókönyv szerint.

Előfordulhat azonban, a PowerShell Core explicit módon nem támogató modulok kompatibilis bizonyos esetekben.
Telepítse a [ `WindowsPSModulePath` ][] modult, fűzze hozzá a Windows PowerShell `PSModulePath` , a PowerShell Core `PSModulePath`.

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

[A Premier szintű]: https://www.microsoft.com/en-us/microsoftservices/support.aspx
[enterprise-agreement]: https://www.microsoft.com/en-us/licensing/licensing-programs/enterprise.aspx
[assurance]: https://www.microsoft.com/en-us/licensing/licensing-programs/software-assurance-default.aspx
[közösségi támogatás]: https://github.com/powershell/powershell/issues
[A Microsoft Community]: https://answers.microsoft.com/
[PowerShell technikai Közösség]: https://techcommunity.microsoft.com/t5/PowerShell/ct-p/WindowsPowerShell
[tanácsadással]: https://support.microsoft.com/assistedsupportproducts
[modern]: https://support.microsoft.com/help/30881/modern-lifecycle-policy
[lifecycle-chart]: ./images/modern-lifecycle.png
[semi-annual]: https://docs.microsoft.com/windows-server/get-started/semi-annual-channel-overview
[MIT licenccel]: https://github.com/PowerShell/PowerShell/blob/master/LICENSE.txt
["WindowsPSModulePath"]: https://www.powershellgallery.com/packages/WindowsPSModulePath/
