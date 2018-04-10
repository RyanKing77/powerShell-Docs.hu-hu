---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 62cccabd7c63c6ba928fc2bf8addd3d11483e90f
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="get-childitem-has--depth-parameter"></a><span data-ttu-id="19465-102">Get-ChildItem - mélysége paraméterrel rendelkezik</span><span class="sxs-lookup"><span data-stu-id="19465-102">Get-ChildItem has -Depth parameter</span></span>
<span data-ttu-id="19465-103">**Get-ChildItem** most már rendelkezik egy **– mélysége** paraméter használata **– Recurse** a rekurzió korlátozása:</span><span class="sxs-lookup"><span data-stu-id="19465-103">**Get-ChildItem** now has a **–Depth** parameter you use with **–Recurse** to limit the recursion:</span></span>

<span data-ttu-id="19465-104">PS C:\\felhasználók\\slee\\letölti\\példa&gt; Get-ChildItem-Recurse - mélysége 0</span><span class="sxs-lookup"><span data-stu-id="19465-104">PS C:\\Users\\slee\\Downloads\\Example&gt; Get-ChildItem -Recurse -Depth 0</span></span>

<span data-ttu-id="19465-105">Könyvtár: C:\\felhasználók\\slee\\letölti\\– példa</span><span class="sxs-lookup"><span data-stu-id="19465-105">Directory: C:\\Users\\slee\\Downloads\\Example</span></span>

<span data-ttu-id="19465-106">Mód LastWriteTime hossza név</span><span class="sxs-lookup"><span data-stu-id="19465-106">Mode LastWriteTime Length Name</span></span>

---- ------------- ------ ----

<span data-ttu-id="19465-107">d---4 14 / / 2015 5:36 du Depth0</span><span class="sxs-lookup"><span data-stu-id="19465-107">d----- 4/14/2015 5:36 PM Depth0</span></span>

<span data-ttu-id="19465-108">-a---4/14/2015 1:19 PM 0 File1.txt</span><span class="sxs-lookup"><span data-stu-id="19465-108">-a---- 4/14/2015 1:19 PM 0 File1.txt</span></span>

<span data-ttu-id="19465-109">-a---4/14/2015 1:19 PM 0 fájl2.ref fájllal</span><span class="sxs-lookup"><span data-stu-id="19465-109">-a---- 4/14/2015 1:19 PM 0 File2.txt</span></span>

<span data-ttu-id="19465-110">-a---4/14/2015 1:19 PM 0 File3.txt</span><span class="sxs-lookup"><span data-stu-id="19465-110">-a---- 4/14/2015 1:19 PM 0 File3.txt</span></span>

<span data-ttu-id="19465-111">PS C:\\felhasználók\\slee\\letölti\\példa&gt; Get-ChildItem-Recurse - mélysége 1</span><span class="sxs-lookup"><span data-stu-id="19465-111">PS C:\\Users\\slee\\Downloads\\Example&gt; Get-ChildItem -Recurse -Depth 1</span></span>

<span data-ttu-id="19465-112">Könyvtár: C:\\felhasználók\\slee\\letölti\\– példa</span><span class="sxs-lookup"><span data-stu-id="19465-112">Directory: C:\\Users\\slee\\Downloads\\Example</span></span>

<span data-ttu-id="19465-113">Mód LastWriteTime hossza név</span><span class="sxs-lookup"><span data-stu-id="19465-113">Mode LastWriteTime Length Name</span></span>

---- ------------- ------ ----

<span data-ttu-id="19465-114">d---4 14 / / 2015 5:36 du Depth0</span><span class="sxs-lookup"><span data-stu-id="19465-114">d----- 4/14/2015 5:36 PM Depth0</span></span>

<span data-ttu-id="19465-115">-a---4/14/2015 1:19 PM 0 File1.txt</span><span class="sxs-lookup"><span data-stu-id="19465-115">-a---- 4/14/2015 1:19 PM 0 File1.txt</span></span>

<span data-ttu-id="19465-116">-a---4/14/2015 1:19 PM 0 fájl2.ref fájllal</span><span class="sxs-lookup"><span data-stu-id="19465-116">-a---- 4/14/2015 1:19 PM 0 File2.txt</span></span>

<span data-ttu-id="19465-117">-a---4/14/2015 1:19 PM 0 File3.txt</span><span class="sxs-lookup"><span data-stu-id="19465-117">-a---- 4/14/2015 1:19 PM 0 File3.txt</span></span>

<span data-ttu-id="19465-118">Könyvtár: C:\\felhasználók\\slee\\letölti\\példa\\Depth0</span><span class="sxs-lookup"><span data-stu-id="19465-118">Directory: C:\\Users\\slee\\Downloads\\Example\\Depth0</span></span>

<span data-ttu-id="19465-119">Mód LastWriteTime hossza név</span><span class="sxs-lookup"><span data-stu-id="19465-119">Mode LastWriteTime Length Name</span></span>

---- ------------- ------ ----

<span data-ttu-id="19465-120">d---4 14 / / 2015 5:33 PM Depth1</span><span class="sxs-lookup"><span data-stu-id="19465-120">d----- 4/14/2015 5:33 PM Depth1</span></span>