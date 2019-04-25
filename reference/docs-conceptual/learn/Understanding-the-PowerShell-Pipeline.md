---
ms.date: 08/23/2018
keywords: PowerShell, a parancsmag
title: PowerShell-folyamatok ismertetése
ms.assetid: 6be50926-7943-4ef7-9499-4490d72a63fb
ms.openlocfilehash: 05ab98b7261f4d41ade1788a924193eccda6318c
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62086442"
---
# <a name="understanding-pipelines"></a>A folyamatok ismertetése

A folyamatok cső csatlakoztatott szegmenseinek sorozata úgy működik. Elemek áthelyezése során a folyamat minden egyes szegmens halad át. Folyamat létrehozása a PowerShell, a függőleges vonal operátor együtt parancsok csatlakozás "|}". Minden parancs kimenete a következő parancs bemenetként szolgál.

A folyamatokhoz használt jelölés más parancskörnyezet használt jelölés hasonlít. Első ránézésre nem lehet nyilvánvaló hogyan folyamatok különböznek a PowerShellben. A képernyőn látható szöveg, bár a PowerShell csövek objektumokat, nem szöveg parancsok között.

## <a name="the-powershell-pipeline"></a>A PowerShell-adatcsatorna

A folyamatok olyan tartják a legértékesebb fogalma a parancssori felületen használt. Ha megfelelően használja, a folyamatok egyszerűsíteni az összetett parancsokkal, és könnyebben tekintse meg a parancsok a munkafolyamat. Egy folyamat (nevezett folyamat prvek) lévő összes parancs a következő parancsot a folyamat továbbítja a kimenetét-elemenként. Parancsok nem kell egyszerre egynél több elem kezelni. Csökkentett erőforrás-használat és a kimenet első azonnali megkezdéséhez képességét jön létre.

Ha például a `Out-Host` parancsmag a lap-lapon megjeleníti a kimenetet egy másik parancsba, a kimeneti úgy tűnik, csak a normál, lapok felosztani, a képernyőn megjelenő szöveg, például:

```powershell
Get-ChildItem -Path C:\WINDOWS\System32 | Out-Host -Paging
```

```Output
    Directory: C:\WINDOWS\system32

Mode                LastWriteTime         Length Name
----                -------------         ------ ----
d-----        4/12/2018   2:15 AM                0409
d-----        5/13/2018  11:31 PM                1033
d-----        4/11/2018   4:38 PM                AdvancedInstallers
d-----        5/13/2018  11:13 PM                af-ZA
d-----        5/13/2018  11:13 PM                am-et
d-----        4/11/2018   4:38 PM                AppLocker
d-----        5/13/2018  11:31 PM                appmgmt
d-----        7/11/2018   2:05 AM                appraiser
d---s-        4/12/2018   2:20 AM                AppV
d-----        5/13/2018  11:10 PM                ar-SA
d-----        5/13/2018  11:13 PM                as-IN
d-----        8/14/2018   9:03 PM                az-Latn-AZ
d-----        5/13/2018  11:13 PM                be-BY
d-----        5/13/2018  11:10 PM                BestPractices
d-----        5/13/2018  11:10 PM                bg-BG
d-----        5/13/2018  11:13 PM                bn-BD
d-----        5/13/2018  11:13 PM                bn-IN
d-----        8/14/2018   9:03 PM                Boot
d-----        8/14/2018   9:03 PM                bs-Latn-BA
d-----        4/11/2018   4:38 PM                Bthprops
d-----        4/12/2018   2:19 AM                ca-ES
d-----        8/14/2018   9:03 PM                ca-ES-valencia
d-----        5/13/2018  10:46 PM                CatRoot
d-----        8/23/2018   5:07 PM                catroot2
<SPACE> next page; <CR> next line; Q quit
...
```

CPU-kihasználtság lapozást is csökkenti, mert a feldolgozás továbbítja a `Out-Host` megjelenítésére készen álló teljes oldal, ha a parancsmagot. A parancsmagok, a folyamat az azt megelőző végrehajtási szüneteltetése, amíg a kimenet a következő lapra érhető el.

A különbség a Windows Feladatkezelő figyelése a PowerShell által használt Processzor- és tekintheti meg. Futtassa a következő parancsot: `Get-ChildItem C:\Windows -Recurse`. A parancs a Processzor- és használati összehasonlítása: `Get-ChildItem C:\Windows -Recurse | Out-Host -Paging`.

> [!NOTE]
> A **lapozás** paraméter minden PowerShell-gazdagép nem támogatja. Például, amikor a próbálja használni a **lapozás** paramétert a PowerShell ISE-ben, az alábbi hibát látja:
>
> ```Output
> out-lineoutput : The method or operation is not implemented.
> At line:1 char:1
> + Get-ChildItem C:\Windows -Recurse | Out-Host -Paging
> + ~~~~~~~~~~~~~~~~~~~~~~~~~~~
>     + CategoryInfo          : NotSpecified: (:) [out-lineoutput], NotImplementedException
>     + FullyQualifiedErrorId : System.NotImplementedException,Microsoft.PowerShell.Commands.OutLineOutputCommand
> ```

## <a name="objects-in-the-pipeline"></a>A folyamat objektumok

A PowerShell-parancsmag futtatásakor a szöveges kimenet látja, mert a szükséges objektumokat képviseli a konzolablakban szövegként. A szöveges kimenet előfordulhat, hogy nem jeleníthető meg az összes, a kimeneti objektum tulajdonságait.

Vegyük példaként a `Get-Location` parancsmagot. Ha `Get-Location` közben az aktuális tartózkodási helyét a C meghajtó gyökérkönyvtárában, a következő eredmény látható:

```
PS> Get-Location

Path
----
C:\
```

A szöveges kimenet található egy összefoglaló az információ nem teljes reprezentációját által visszaadott objektum `Get-Location`. A címsor a kimenetben, a folyamat, amely formázza az adatokat a képernyőn megjelenítendő egészül ki.

Amikor irányítsa a kimenetét a `Get-Member` parancsmag által visszaadott objektumra vonatkozó információ első `Get-Location`.

```powershell
Get-Location | Get-Member
```

```Output
   TypeName: System.Management.Automation.PathInfo

Name         MemberType Definition
----         ---------- ----------
Equals       Method     bool Equals(System.Object obj)
GetHashCode  Method     int GetHashCode()
GetType      Method     type GetType()
ToString     Method     string ToString()
Drive        Property   System.Management.Automation.PSDriveInfo Drive {get;}
Path         Property   string Path {get;}
Provider     Property   System.Management.Automation.ProviderInfo Provider {get;}
ProviderPath Property   string ProviderPath {get;}
```

`Get-Location` Visszaadja egy **PathInfo** objektum, amely tartalmazza az aktuális elérés úton és egyéb információkat.
