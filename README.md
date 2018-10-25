# <a name="microsoft-open-source-code-of-conduct"></a>A Microsoft nyílt forráskóddal kapcsolatos viselkedési szabályzata

Ez a projekt [a Microsoft nyílt forráskóddal kapcsolatos viselkedési szabályzata](https://opensource.microsoft.com/codeofconduct/) alapján működik.
További információt a [viselkedési szabályzattal kapcsolatos gyakori kérdések oldalán](https://opensource.microsoft.com/codeofconduct/faq/) olvashat, kérdéseit és hozzászólásait pedig az [opencode@microsoft.com](mailto:opencode@microsoft.com) címen várjuk.

[![Létrehozási állapot](https://ci.appveyor.com/api/projects/status/onshefxnc4g4pv87/branch/staging?svg=true)](https://ci.appveyor.com/project/PowerShell/powershell-docs/branch/staging)

## <a name="powershell-documentation"></a>PowerShell-dokumentáció

Üdvözli a PowerShell-Docs tárház, lakáshelyzet, a PowerShell hivatalos dokumentációját.

## <a name="repository-structure"></a>Tárház szerkezete

A következő legfelső szintű mappák példakódokban mindegyike tartalmaz egy dokumentumkészlet közzétett [Microsoft Docs](https://docs.microsoft.com/powershell).

- [/Developer/](https://docs.microsoft.com/powershell/developer/) jövőbeli érhető el a PowerShell SDK-dokumentáció
  - Jelenleg is zajlik az MSDN-ről a tartalom
- [/DSC/](https://docs.microsoft.com/powershell/dsc/) van a Desired State Configuration szolgáltatáshoz
- [/Gallery/](https://docs.microsoft.com/powershell/gallery) szól a [PowerShell-galéria](https://www.powershellgallery.com/)
- [/jea/](https://docs.microsoft.com/powershell/jea/) a Just Enough Administration szolgáltatásának van
- [/Reference/](https://docs.microsoft.com/powershell/scripting/) olyan 3.0, 4.0-s verzióját, 5.0, 5.1 és 6.0-s verziója között PowerShell fogalmi témakörök és modulokra vonatkozó referenciák
  - Ez a tartalom egyben súgó tartalma által beolvasott forrását a `Get-Help` parancsmag
- [/WMF](https://docs.microsoft.com/powershell/wmf/readme) kibocsátási megjegyzéseket tartalmaz, a Windows Management Framework, a csomag terjesztése PowerShell új verziója a Windows korábbi verzióiban használt.

## <a name="contributing"></a>Közreműködő

Aktívan összevonása hozzájárulások keresztül a tárházba [pull-kérelem](https://help.github.com/articles/using-pull-requests/) be a *átmeneti* ágat.
Vegye figyelembe, hogy a lekéréses kérelem küldése előtt [aláírni a közreműködői licencszerződés](https://cla.microsoft.com/) annak biztosításához, hogy a Közösség beküldött anyagokért használata ingyenes.

A közreműködő további információért olvassa el a [a közreműködői útmutatóban](CONTRIBUTING.md).
A közreműködői útmutatóban hogyan működhet közre a dokumentáció, a javasolt eszközök és a stílus és a formázási követelmények részletes információkat tartalmaz.
A probléma és a Pull-kérési sablonok használja annak érdekében, hogy egységes dokumentáció verziója között.

## <a name="licenses"></a>Licencek

Két licenc fájlok vannak a projekthez.
Az MIT-licenccel vonatkozik a szabályzat, amely ebben a tárházban.
A dokumentáció a Creative Commons licencet vonatkozik.