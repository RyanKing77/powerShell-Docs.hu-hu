---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: cc5d2d799c1292f68de5fb2360fcba220c2c010b
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62085292"
---
# <a name="get-childitem-has--depth-parameter"></a><span data-ttu-id="8f379-102">Get-ChildItem rendelkezik - Depth paraméterrel</span><span class="sxs-lookup"><span data-stu-id="8f379-102">Get-ChildItem has -Depth parameter</span></span>
<span data-ttu-id="8f379-103">**Get-ChildItem** most már rendelkezik egy **– mélysége** paraméter használata **– Recurse** a rekurzió korlátozása:</span><span class="sxs-lookup"><span data-stu-id="8f379-103">**Get-ChildItem** now has a **–Depth** parameter you use with **–Recurse** to limit the recursion:</span></span>

<span data-ttu-id="8f379-104">PS C:\\felhasználók\\slee\\letölti\\példa&gt; Get-ChildItem-Recurse - 0 mélysége</span><span class="sxs-lookup"><span data-stu-id="8f379-104">PS C:\\Users\\slee\\Downloads\\Example&gt; Get-ChildItem -Recurse -Depth 0</span></span>

<span data-ttu-id="8f379-105">Könyvtár: C:\\felhasználók\\slee\\letölti\\példa</span><span class="sxs-lookup"><span data-stu-id="8f379-105">Directory: C:\\Users\\slee\\Downloads\\Example</span></span>

<span data-ttu-id="8f379-106">Mód LastWriteTime hosszúságú név</span><span class="sxs-lookup"><span data-stu-id="8f379-106">Mode LastWriteTime Length Name</span></span>

---- ------------- ------ ----

<span data-ttu-id="8f379-107">d---4/14/2015 17:36 közötti Depth0</span><span class="sxs-lookup"><span data-stu-id="8f379-107">d----- 4/14/2015 5:36 PM Depth0</span></span>

<span data-ttu-id="8f379-108">-a---4/14/2015 1:19 PM 0 File1.txt</span><span class="sxs-lookup"><span data-stu-id="8f379-108">-a---- 4/14/2015 1:19 PM 0 File1.txt</span></span>

<span data-ttu-id="8f379-109">-a---4/14/2015 1:19 PM 0 fájl2.ref fájllal</span><span class="sxs-lookup"><span data-stu-id="8f379-109">-a---- 4/14/2015 1:19 PM 0 File2.txt</span></span>

<span data-ttu-id="8f379-110">-a---4/14/2015 1:19 PM 0 File3.txt</span><span class="sxs-lookup"><span data-stu-id="8f379-110">-a---- 4/14/2015 1:19 PM 0 File3.txt</span></span>

<span data-ttu-id="8f379-111">PS C:\\felhasználók\\slee\\letölti\\példa&gt; Get-ChildItem-Recurse - mélysége 1</span><span class="sxs-lookup"><span data-stu-id="8f379-111">PS C:\\Users\\slee\\Downloads\\Example&gt; Get-ChildItem -Recurse -Depth 1</span></span>

<span data-ttu-id="8f379-112">Könyvtár: C:\\felhasználók\\slee\\letölti\\példa</span><span class="sxs-lookup"><span data-stu-id="8f379-112">Directory: C:\\Users\\slee\\Downloads\\Example</span></span>

<span data-ttu-id="8f379-113">Mód LastWriteTime hosszúságú név</span><span class="sxs-lookup"><span data-stu-id="8f379-113">Mode LastWriteTime Length Name</span></span>

---- ------------- ------ ----

<span data-ttu-id="8f379-114">d---4/14/2015 17:36 közötti Depth0</span><span class="sxs-lookup"><span data-stu-id="8f379-114">d----- 4/14/2015 5:36 PM Depth0</span></span>

<span data-ttu-id="8f379-115">-a---4/14/2015 1:19 PM 0 File1.txt</span><span class="sxs-lookup"><span data-stu-id="8f379-115">-a---- 4/14/2015 1:19 PM 0 File1.txt</span></span>

<span data-ttu-id="8f379-116">-a---4/14/2015 1:19 PM 0 fájl2.ref fájllal</span><span class="sxs-lookup"><span data-stu-id="8f379-116">-a---- 4/14/2015 1:19 PM 0 File2.txt</span></span>

<span data-ttu-id="8f379-117">-a---4/14/2015 1:19 PM 0 File3.txt</span><span class="sxs-lookup"><span data-stu-id="8f379-117">-a---- 4/14/2015 1:19 PM 0 File3.txt</span></span>

<span data-ttu-id="8f379-118">Könyvtár: C:\\felhasználók\\slee\\letölti\\példa\\Depth0</span><span class="sxs-lookup"><span data-stu-id="8f379-118">Directory: C:\\Users\\slee\\Downloads\\Example\\Depth0</span></span>

<span data-ttu-id="8f379-119">Mód LastWriteTime hosszúságú név</span><span class="sxs-lookup"><span data-stu-id="8f379-119">Mode LastWriteTime Length Name</span></span>

---- ------------- ------ ----

<span data-ttu-id="8f379-120">d---4/14/2015 Délután 5:33 Depth1</span><span class="sxs-lookup"><span data-stu-id="8f379-120">d----- 4/14/2015 5:33 PM Depth1</span></span>
