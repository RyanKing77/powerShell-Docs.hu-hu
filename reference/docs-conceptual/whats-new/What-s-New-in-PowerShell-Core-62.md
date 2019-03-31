---
title: A PowerShell Core 6.2 újdonságai
description: Új szolgáltatásaival és módosításaival, amely a PowerShell Core 6.2
ms.date: 03/28/2019
ms.openlocfilehash: 2224d23a244175059a705c07001e8ad8d6ab3aa0
ms.sourcegitcommit: 8dd4394cf867005a8b9ef0bb74b744c964fbc332
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/30/2019
ms.locfileid: "58750033"
---
# <a name="whats-new-in-powershell-core-62"></a><span data-ttu-id="e75c6-103">A PowerShell Core 6.2 újdonságai</span><span class="sxs-lookup"><span data-stu-id="e75c6-103">What's New in PowerShell Core 6.2</span></span>

<span data-ttu-id="e75c6-104">Alább néhány fontos új szolgáltatásokat és módosításokat vezettek be a PowerShell Core 6.2 egy kijelölt van.</span><span class="sxs-lookup"><span data-stu-id="e75c6-104">Below is a selection of some of the major new features and changes that have been introduced in PowerShell Core 6.2.</span></span>

<span data-ttu-id="e75c6-105">Is **tonna** "unalmas szolgáltatáshasználatot", amelyek gyorsabb és stabilabb (és sok és számos hibajavítás) PowerShell!</span><span class="sxs-lookup"><span data-stu-id="e75c6-105">There's also **tons** of "boring stuff" that make PowerShell faster and more stable (plus lots and lots of bug fixes)!</span></span>
<span data-ttu-id="e75c6-106">Változások teljes listájához tekintse meg a [a Githubon változásnaplójában](https://github.com/PowerShell/PowerShell/blob/master/CHANGELOG.md).</span><span class="sxs-lookup"><span data-stu-id="e75c6-106">For a full list of changes, check out our [changelog on GitHub](https://github.com/PowerShell/PowerShell/blob/master/CHANGELOG.md).</span></span>

<span data-ttu-id="e75c6-107">És közben ki az alábbi néhány nevet nevezzük, Köszönjük, hogy [összes a közösségi közreműködők](https://github.com/PowerShell/PowerShell/graphs/contributors) , amely ebben a kiadásban lehetővé tenni.</span><span class="sxs-lookup"><span data-stu-id="e75c6-107">And while we call out some names below, thank you to [all of the community contributors](https://github.com/PowerShell/PowerShell/graphs/contributors) that made this release possible.</span></span>

## <a name="engine-updates-and-fixes"></a><span data-ttu-id="e75c6-108">A motor-frissítések és javítások</span><span class="sxs-lookup"><span data-stu-id="e75c6-108">Engine Updates and Fixes</span></span>

- <span data-ttu-id="e75c6-109">Adja hozzá a PowerShell távoli eljáráshívás engedélyezését vagy letiltását a parancsmag a figyelmeztető üzenetek ([#9203][])</span><span class="sxs-lookup"><span data-stu-id="e75c6-109">Add PowerShell remoting enable/disable cmdlet warning messages ([#9203][])</span></span>
- <span data-ttu-id="e75c6-110">Javítás a `FormatTable` távoli deszerializálás regressziós ([#9116][])</span><span class="sxs-lookup"><span data-stu-id="e75c6-110">Fix for `FormatTable` remote deserialization regression ([#9116][])</span></span>
- <span data-ttu-id="e75c6-111">Frissítse a feladatalapú `async` PowerShell-lel közvetlenül egy feladat objektumot ad vissza hozzáadott API-k ([#9079][])</span><span class="sxs-lookup"><span data-stu-id="e75c6-111">Update the task-based `async` APIs added to PowerShell to return a Task object directly ([#9079][])</span></span>
- <span data-ttu-id="e75c6-112">Adja hozzá az 5 `InvokeAsync` túlterheléssel és `StopAsync` , a `PowerShell` típusa ([#8056][]) (Köszönjük, hogy @KirkMunro!)</span><span class="sxs-lookup"><span data-stu-id="e75c6-112">Add 5 `InvokeAsync` overloads and `StopAsync` to the `PowerShell` type ([#8056][]) (Thanks @KirkMunro!)</span></span>

## <a name="general-cmdlet-updates-and-fixes"></a><span data-ttu-id="e75c6-113">Általános parancsmag frissítések és javítások</span><span class="sxs-lookup"><span data-stu-id="e75c6-113">General Cmdlet Updates and Fixes</span></span>

- <span data-ttu-id="e75c6-114">Engedélyezése `SecureString` parancsmagok a Windows tárolja az egyszerű szöveg ([#9199][])</span><span class="sxs-lookup"><span data-stu-id="e75c6-114">Enable `SecureString` cmdlets for non-Windows by storing the plain text ([#9199][])</span></span>
- <span data-ttu-id="e75c6-115">Adja hozzá az elavult üzenetet `Send-MailMessage` ([#9178][])</span><span class="sxs-lookup"><span data-stu-id="e75c6-115">Add Obsolete message to `Send-MailMessage` ([#9178][])</span></span>
- <span data-ttu-id="e75c6-116">Javítsa ki `Restart-Computer` dolgozhatnak `localhost` amikor a Rendszerfelügyeleti webszolgáltatások nem szerepel ([#9160][])</span><span class="sxs-lookup"><span data-stu-id="e75c6-116">Fix `Restart-Computer` to work on `localhost` when WinRM is not present ([#9160][])</span></span>
- <span data-ttu-id="e75c6-117">Győződjön meg arról, `Start-Job` throw hibát, ha a PowerShell üzemeltetési ([#9128][])</span><span class="sxs-lookup"><span data-stu-id="e75c6-117">Make `Start-Job` throw terminating error when PowerShell is being hosted ([#9128][])</span></span>
- <span data-ttu-id="e75c6-118">-Es frissítési verziója `PowerShell.Native` és tesztek üzemeltetésére ([#8983][])</span><span class="sxs-lookup"><span data-stu-id="e75c6-118">Update version for `PowerShell.Native` and hosting tests ([#8983][])</span></span>

## <a name="breaking-changes"></a><span data-ttu-id="e75c6-119">Kompatibilitástörő változások</span><span class="sxs-lookup"><span data-stu-id="e75c6-119">Breaking Changes</span></span>

<span data-ttu-id="e75c6-120">Javítsa ki a - NoEnumerate viselkedése konzisztens, a Windows PowerShell Write-Output ([#9069][]) (Köszönjük, hogy @vexx32!)</span><span class="sxs-lookup"><span data-stu-id="e75c6-120">Fix -NoEnumerate behavior in Write-Output to be consistent with Windows PowerShell ([#9069][]) (Thanks @vexx32!)</span></span>

<!-- Link references -->
[#8056]: https://github.com/PowerShell/PowerShell/pull/8056
[#8983]: https://github.com/PowerShell/PowerShell/pull/8983
[#9069]: https://github.com/PowerShell/PowerShell/pull/9069
[#9079]: https://github.com/PowerShell/PowerShell/pull/9079
[#9116]: https://github.com/PowerShell/PowerShell/pull/9116
[#9128]: https://github.com/PowerShell/PowerShell/pull/9128
[#9160]: https://github.com/PowerShell/PowerShell/pull/9160
[#9178]: https://github.com/PowerShell/PowerShell/pull/9178
[#9199]: https://github.com/PowerShell/PowerShell/pull/9199
[#9203]: https://github.com/PowerShell/PowerShell/pull/9203
