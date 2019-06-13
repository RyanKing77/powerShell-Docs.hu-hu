---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: Objektumok rendezése
ms.openlocfilehash: ed78e7e333f3468781c9cd96df2194fbdfebe753
ms.sourcegitcommit: a6f13c16a535acea279c0ddeca72f1f0d8a8ce4c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2019
ms.locfileid: "67030771"
---
# <a name="sorting-objects"></a>Objektumok rendezése

A megjelenített adatok könnyebb vizsgálata használatával azt is rendszerezheti a `Sort-Object` parancsmagot. `Sort-Object` egy vagy több tulajdonságának rendezendő nevét veszi fel, és ezek a tulajdonságok értékei szerint rendezett adatok visszaadása.

## <a name="basic-sorting"></a>Alapszintű rendezése

Fontolja meg a probléma az aktuális könyvtárban található fájlokat és alkönyvtárakat listázása.
Amely szerint rendezni szeretnénk **LastWriteTime** , majd az **neve**, beírásával is tesszük azt:

```powershell
Get-ChildItem |
  Sort-Object -Property LastWriteTime, Name |
  Format-Table -Property LastWriteTime, Name
```

```output
LastWriteTime          Name
-------------          ----
11/6/2017 10:10:11 AM  .localization-config
11/6/2017 10:10:11 AM  .openpublishing.build.ps1
11/6/2017 10:10:11 AM  appveyor.yml
11/6/2017 10:10:11 AM  LICENSE
11/6/2017 10:10:11 AM  LICENSE-CODE
11/6/2017 10:10:11 AM  ThirdPartyNotices
11/6/2017 10:10:15 AM  tests
6/6/2018 7:58:59 PM    CONTRIBUTING.md
6/6/2018 7:58:59 PM    README.md
...
```

Is rendezheti az objektumok fordított sorrendben adja meg a **Descending** paraméter váltani.

```powershell
Get-ChildItem |
  Sort-Object -Property LastWriteTime, Name -Descending |
  Format-Table -Property LastWriteTime, Name
```

```output
LastWriteTime          Name
-------------          ----
12/1/2018 10:13:50 PM  reference
12/1/2018 10:13:50 PM  dsc
...
6/6/2018 7:58:59 PM    README.md
6/6/2018 7:58:59 PM    CONTRIBUTING.md
11/6/2017 10:10:15 AM  tests
11/6/2017 10:10:11 AM  ThirdPartyNotices
11/6/2017 10:10:11 AM  LICENSE-CODE
11/6/2017 10:10:11 AM  LICENSE
11/6/2017 10:10:11 AM  appveyor.yml
11/6/2017 10:10:11 AM  .openpublishing.build.ps1
11/6/2017 10:10:11 AM  .localization-config
```

## <a name="using-hash-tables"></a>Jelszókivonat-táblák használata

Eltérőek a különböző tulajdonságok tömbben kivonattáblák használatával lehet rendezni.
Minden egyes kivonattábla használ egy **kifejezés** kulcsot karakterláncként adja meg a tulajdonság nevét és a egy **növekvő** vagy **Descending** kulcsot adja meg a rendezési sorrend szerint `$true` vagy `$false`.
A **kifejezés** kulcs megadása kötelező.
A **növekvő** vagy **Descending** kulcsot nem kötelező megadni.

Az alábbi példa rendezése csökkenő objektumok **LastWriteTime** sorrendjét és növekvő **neve** sorrendben.

```powershell
Get-ChildItem |
  Sort-Object -Property @{ Expression = 'LastWriteTime'; Descending = $true }, @{ Expression = 'Name'; Ascending = $true } |
  Format-Table -Property LastWriteTime, Name
```

```output
LastWriteTime          Name
-------------          ----
12/1/2018 10:13:50 PM  dsc
12/1/2018 10:13:50 PM  reference
11/29/2018 6:56:01 PM  .openpublishing.redirection.json
11/29/2018 6:56:01 PM  gallery
11/24/2018 10:33:22 AM developer
11/20/2018 7:22:19 PM  .markdownlint.json
...
```

És a scriptblock kulcsszót is megadható a **kifejezés** kulcsot.
Ha fut a `Sort-Object` parancsmag hajtja végre a scriptblock kulcsszót, és az eredmények rendezéséhez használandó.

Az alábbi példa az objektumokat a időtartama szerint csökkenő sorrendben rendezi **CreationTime** és **LastWriteTime**.

```powershell
Get-ChildItem |
  Sort-Object -Property @{ Expression = { $_.LastWriteTime - $_.CreationTime }; Descending = $true } |
  Format-Table -Property LastWriteTime, CreationTime
```

```output
LastWriteTime          CreationTime
-------------          ------------
12/1/2018 10:13:50 PM  11/6/2017 10:10:11 AM
12/1/2018 10:13:50 PM  11/6/2017 10:10:11 AM
11/7/2018 6:52:24 PM   11/6/2017 10:10:11 AM
11/7/2018 6:52:24 PM   11/6/2017 10:10:15 AM
11/3/2018 9:58:17 AM   11/6/2017 10:10:11 AM
10/26/2018 4:50:21 PM  11/6/2017 10:10:11 AM
11/17/2018 1:10:57 PM  11/29/2017 5:48:30 PM
11/12/2018 6:29:53 PM  12/7/2017 7:57:07 PM
...
```

## <a name="tips"></a>Tipp

Kihagyhatja a **tulajdonság** paraméter neve megegyezik a következőket:

```powershell
Sort-Object LastWriteTime, Name
```

Emellett olvassa el `Sort-Object` által a beépített alias `sort`:

```powershell
sort LastWriteTime, Name
```

A rendezési kivonattáblák kulcsainak rövidíthető a következő:

```powershell
Sort-Object @{ e = 'LastWriteTime'; d = $true }, @{ e = 'Name'; a = $true }
```

Ebben a példában a **e** rövidítése **kifejezés**, a **d** rövidítése **Descending**, és a **egy** a rövidítése **növekvő**.

A jobb olvashatóság érdekében helyezze el a kivonattáblák egy külön változóba:

```powershell
$order = @(
  @{ Expression = 'LastWriteTime'; Descending = $true }
  @{ Expression = 'Name'; Ascending = $true }
)

Get-ChildItem |
  Sort-Object $order |
  Format-Table LastWriteTime, Name
```
