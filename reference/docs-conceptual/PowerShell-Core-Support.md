# <a name="powershell-core-support-lifecycle"></a>PowerShell Core támogatási életciklusa

PowerShell Core egy meghatározott készletét eszközök és összetevők rendszerrel szállított, telepített, és a Windows PowerShell külön kell beállítani.
Ezért a PowerShell Core nem szerepel a Windows 7/8.1/10 vagy Windows Server licencelési szerződést.

Azonban esetében támogatott a PowerShell Core hagyományos a Microsoft támogatási szerződésből, beleértve a [Premier][], [Microsofttal kötött nagyvállalati szerződése][enterprise-agreement], és [Microsoft Szoftverbiztosítással][assurance].
Is is kell fizetnie [tanácsadással][] a PowerShell Core által tervátalakítási a problémára vonatkozó támogatási kérelmet.

Is kínál [közösségi támogatás][] a Githubon, ahol egy problémát, a hiba, vagy a szolgáltatás kérése fájlt is.
Azt is megteheti, előfordulhat, hogy talál segítséget a Közösség más tagjai az általános [Microsoft Community][] vagy a Microsoft [PowerShell műszaki közösségi][].
Azt garanciát nem létezik, hogy a probléma címzett vagy időben feloldva.
Ha a probléma azonnali figyelmet igénylő, használja a hagyományos fizetős támogatási lehetőségeket.

## <a name="lifecycle-of-powershell-core"></a>A PowerShell Core életciklusa

PowerShell Core bevezetni a [Microsoft Modern életciklusra vonatkozó szabályzata][modern].
Támogatási életciklus célja, hogy naprakészen tartsák az ügyfelek legújabb verziójú.

PowerShell Core verzió 6.x ága frissíti körülbelül hat havonta (pl. 6.0, 6.1, 6.2, stb.)

> [!IMPORTANT]
> Után minden új alverzió kiadásáról továbbra is megkapja az támogatási hat hónapban frissíteni kell.

Például ha PowerShell Core 6.1 van szabadítva. július 1., 2018, várhatóan frissíteni a PowerShell Core 6.1 2019. január 1-jétől. támogatási fenntartásához.

![PowerShell Core fiókirodai életciklusa][lifecycle-chart]

A Modern életciklusra vonatkozó szabályzata is szükséges, hogy a Microsoft értesítést küldenek az ügyfelek 12 hónapon keresztül megszűnő támogatás (azaz a PowerShell Core) termék előtt.

Végül várhatóan PowerShell Core fogad el, a "hosszú távú karbantartási" megközelítést, ahol azt igényel csak karbantartása és biztonsági frissítések támogatását a meghatározott fiókirodai/verzióját 6.x belül.

## <a name="supported-platforms"></a>Támogatott platformok

PowerShell Core hivatalosan a következő platformokon támogatott:

* Windows 7, 8.1 és 10
* Windows Server 2008 R2, 2012 R2-ben 2016
* [Windows Server pontosvesszővel éves csatorna][semi-annual]
* Ubuntu 14.04, 16.04 és 17.04
* Debian 8.7 + és 9
* CentOS 7
* Red Hat Enterprise Linux 7
* OpenSUSE 42.2
* Fedora 25, 26
* macOS 10.12 +

A Közösség emellett hozzájárult csomagok a következő platformokat, de nem hivatalosan suppported:

* Linux architektúrája
* Kali Linux
* AppImage (működik a több Linux platformon)

## <a name="notes-on-licensing"></a>Tudnivalók a licencelés

PowerShell Core alatt megjelenik a [MIT licenccel][].
A licenc, és egy fizetős támogatási megállapodás hiányában, a felhasználók korlátozva [közösségi támogatás][].
Közösségi-támogatással rendelkező Microsoft teszi nincs garancia válaszkészsége vagy javításokat.

## <a name="windows-powershell-module"></a>A Windows PowerShell-modul

Támogatja a PowerShell Core nem terjed ki a más termék modulok kivéve, ha az ilyen modulokhoz explicit módon támogatja a PowerShell Core.
Használata esetén például a `ActiveDirectory` modul részét képező, mert a Windows Server részét egy nem támogatott forgatókönyvet.

Előfordulhat azonban, modulokat, amelyek kifejezetten nem támogatják a PowerShell Core kompatibilis bizonyos esetekben.
Telepítse a [ `WindowsPSModulePath`][] modul, fűzze hozzá a Windows PowerShell `PSModulePath` a PowerShell képességének `PSModulePath`.

Először telepítse a `WindowsPSModulePath` a PowerShell-galériából modul:

```powershell
# Add `-Scope CurrentUser` if you're installing as non-admin 
Install-Module WindowsPSModulePath -Force
```

Ez a modul telepítése után futtassa a `Add-WindowsPSModulePath` parancsmaggal adja hozzá a Windows PowerShell `PSModulePath` képességének PowerShell:

```powershell
# Add this line to your profile if you always want Windows PowerShell PSModulePath
Add-WindowsPSModulePath
```

[Premier]: https://www.microsoft.com/en-us/microsoftservices/support.aspx
[enterprise-agreement]: https://www.microsoft.com/en-us/licensing/licensing-programs/enterprise.aspx
[assurance]: https://www.microsoft.com/en-us/licensing/licensing-programs/software-assurance-default.aspx
[közösségi támogatás]: https://github.com/powershell/powershell/issues
[Microsoft Community]: https://answers.microsoft.com/
[PowerShell műszaki közösségi]: https://techcommunity.microsoft.com/t5/PowerShell/ct-p/WindowsPowerShell
[tanácsadással]: https://support.microsoft.com/assistedsupportproducts
[modern]: https://support.microsoft.com/help/30881/modern-lifecycle-policy
[lifecycle-chart]: ./images/modern-lifecycle.png
[semi-annual]: https://docs.microsoft.com/windows-server/get-started/semi-annual-channel-overview
[MIT licenccel]: https://github.com/PowerShell/PowerShell/blob/master/LICENSE.txt
["WindowsPSModulePath"]: https://www.powershellgallery.com/packages/WindowsPSModulePath/
