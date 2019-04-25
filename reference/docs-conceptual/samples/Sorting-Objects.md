---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: Objektumok rendezése
ms.assetid: 8530caa8-3ed4-4c56-aed7-1295dd9ba199
ms.openlocfilehash: 06aa15d89888f1ecbe60b8e1dfb4efebb1d73673
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62086051"
---
# <a name="sorting-objects"></a><span data-ttu-id="7765b-103">Objektumok rendezése</span><span class="sxs-lookup"><span data-stu-id="7765b-103">Sorting Objects</span></span>

<span data-ttu-id="7765b-104">A megjelenített adatok könnyebb vizsgálata használatával azt is rendszerezheti a `Sort-Object` parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="7765b-104">We can organize displayed data to make it easier to scan by using the `Sort-Object` cmdlet.</span></span> <span data-ttu-id="7765b-105">`Sort-Object` egy vagy több tulajdonságának rendezendő nevét veszi fel, és ezek a tulajdonságok értékei szerint rendezett adatok visszaadása.</span><span class="sxs-lookup"><span data-stu-id="7765b-105">`Sort-Object` takes the name of one or more properties to sort on, and returns data sorted by the values of those properties.</span></span>

## <a name="basic-sorting"></a><span data-ttu-id="7765b-106">Alapszintű rendezése</span><span class="sxs-lookup"><span data-stu-id="7765b-106">Basic sorting</span></span>

<span data-ttu-id="7765b-107">Fontolja meg a probléma az aktuális könyvtárban található fájlokat és alkönyvtárakat listázása.</span><span class="sxs-lookup"><span data-stu-id="7765b-107">Consider the problem of listing subdirectories and files in the current directory.</span></span>
<span data-ttu-id="7765b-108">Amely szerint rendezni szeretnénk **LastWriteTime** , majd az **neve**, beírásával is tesszük azt:</span><span class="sxs-lookup"><span data-stu-id="7765b-108">If we want to sort by **LastWriteTime** and then by **Name**, we can do it by typing:</span></span>

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

<span data-ttu-id="7765b-109">Is rendezheti az objektumok fordított sorrendben adja meg a **Descending** paraméter váltani.</span><span class="sxs-lookup"><span data-stu-id="7765b-109">You can also sort the objects in reverse order by specifying the **Descending** switch parameter.</span></span>

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

## <a name="using-hash-tables"></a><span data-ttu-id="7765b-110">Jelszókivonat-táblák használata</span><span class="sxs-lookup"><span data-stu-id="7765b-110">Using hash tables</span></span>

<span data-ttu-id="7765b-111">Eltérőek a különböző tulajdonságok tömbben kivonattáblák használatával lehet rendezni.</span><span class="sxs-lookup"><span data-stu-id="7765b-111">You can sort different properties in different orders by using hash tables in an array.</span></span>
<span data-ttu-id="7765b-112">Minden egyes kivonattábla használ egy **kifejezés** kulcsot karakterláncként adja meg a tulajdonság nevét és a egy **növekvő** vagy **Descending** kulcsot adja meg a rendezési sorrend szerint `$true` vagy `$false`.</span><span class="sxs-lookup"><span data-stu-id="7765b-112">Each hash table uses an **Expression** key to specify the property name as string and an **Ascending** or **Descending** key to specify the sort order by `$true` or `$false`.</span></span>
<span data-ttu-id="7765b-113">A **kifejezés** kulcs megadása kötelező.</span><span class="sxs-lookup"><span data-stu-id="7765b-113">The **Expression** key is mandatory.</span></span>
<span data-ttu-id="7765b-114">A **növekvő** vagy **Descending** kulcsot nem kötelező megadni.</span><span class="sxs-lookup"><span data-stu-id="7765b-114">The **Ascending** or **Descending** key is optional.</span></span>

<span data-ttu-id="7765b-115">Az alábbi példa rendezése csökkenő objektumok **LastWriteTime** sorrendjét és növekvő **neve** sorrendben.</span><span class="sxs-lookup"><span data-stu-id="7765b-115">The following example sorts objects in descending **LastWriteTime** order and ascending **Name** order.</span></span>

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

<span data-ttu-id="7765b-116">És a scriptblock kulcsszót is megadható a **kifejezés** kulcsot.</span><span class="sxs-lookup"><span data-stu-id="7765b-116">You can also set a scriptblock to the **Expression** key.</span></span>
<span data-ttu-id="7765b-117">Ha fut a `Sort-Object` parancsmag hajtja végre a scriptblock kulcsszót, és az eredmények rendezéséhez használandó.</span><span class="sxs-lookup"><span data-stu-id="7765b-117">When running the `Sort-Object` cmdlet, the scriptblock is executed and the result is used for sorting.</span></span>

<span data-ttu-id="7765b-118">Az alábbi példa az objektumokat a időtartama szerint csökkenő sorrendben rendezi **CreationTime** és **LastWriteTime**.</span><span class="sxs-lookup"><span data-stu-id="7765b-118">The following example sorts objects in descending order by the time span between **CreationTime** and **LastWriteTime**.</span></span>

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

## <a name="tips"></a><span data-ttu-id="7765b-119">Tipp</span><span class="sxs-lookup"><span data-stu-id="7765b-119">Tips</span></span>

<span data-ttu-id="7765b-120">Kihagyhatja a **tulajdonság** paraméter neve megegyezik a következőket:</span><span class="sxs-lookup"><span data-stu-id="7765b-120">You can omit the **Property** parameter name as following:</span></span>

```powershell
Sort-Object LastWriteTime, Name
```

<span data-ttu-id="7765b-121">Emellett olvassa el `Sort-Object` által a beépített alias `sort`:</span><span class="sxs-lookup"><span data-stu-id="7765b-121">Besides, you can refer to `Sort-Object` by its built-in alias, `sort`:</span></span>

```powershell
sort LastWriteTime, Name
```

<span data-ttu-id="7765b-122">A rendezési kivonattáblák kulcsainak rövidíthető a következő:</span><span class="sxs-lookup"><span data-stu-id="7765b-122">The keys in the hash tables for sorting can be abbreviated as following:</span></span>

```powershell
Sort-Object @{ e = 'LastWriteTime'; d = $true }, @{ e = 'Name'; a = $true }
```

<span data-ttu-id="7765b-123">Ebben a példában a **e** rövidítése **kifejezés**, a **d** rövidítése **Descending**, és a **egy** a rövidítése **növekvő**.</span><span class="sxs-lookup"><span data-stu-id="7765b-123">In this example, the **e** stands for **Expression**, the **d** stands for **Descending**, and the **a** stands for **Ascending**.</span></span>

<span data-ttu-id="7765b-124">A jobb olvashatóság érdekében helyezze el a kivonattáblák egy külön változóba:</span><span class="sxs-lookup"><span data-stu-id="7765b-124">To improve readability, you can place the hash tables into a separate variable:</span></span>

```powershell
$order = @(
  @{ Expression = 'LastWriteTime'; Descending = $true }
  @{ Expression = 'Name'; Ascending = $true }
)

Get-ChildItem |
  Sort-Object $order |
  Format-Table LastWriteTime, Name
```