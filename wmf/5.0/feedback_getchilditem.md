---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "WMF, a powershell, a beállítása"
ms.openlocfilehash: 4185d9395f2f3e5ba1c8daa0c365cb2bf322936b
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
# <a name="get-childitem-has--depth-parameter"></a><span data-ttu-id="2fa04-102">Get-ChildItem - mélysége paraméterrel rendelkezik</span><span class="sxs-lookup"><span data-stu-id="2fa04-102">Get-ChildItem has -Depth parameter</span></span>
<span data-ttu-id="2fa04-103">**Get-ChildItem** most már rendelkezik egy **– mélysége** paraméter használata **– Recurse** a rekurzió korlátozása:</span><span class="sxs-lookup"><span data-stu-id="2fa04-103">**Get-ChildItem** now has a **–Depth** parameter you use with **–Recurse** to limit the recursion:</span></span>

<span data-ttu-id="2fa04-104">PS C:\\felhasználók\\slee\\letölti\\példa&gt; Get-ChildItem-Recurse - mélysége 0</span><span class="sxs-lookup"><span data-stu-id="2fa04-104">PS C:\\Users\\slee\\Downloads\\Example&gt; Get-ChildItem -Recurse -Depth 0</span></span>

<span data-ttu-id="2fa04-105">Könyvtár: C:\\felhasználók\\slee\\letölti\\– példa</span><span class="sxs-lookup"><span data-stu-id="2fa04-105">Directory: C:\\Users\\slee\\Downloads\\Example</span></span>

<span data-ttu-id="2fa04-106">Mód LastWriteTime hossza név</span><span class="sxs-lookup"><span data-stu-id="2fa04-106">Mode LastWriteTime Length Name</span></span>

---- ------------- ------ ----

<span data-ttu-id="2fa04-107">d---4 14 / / 2015 5:36 du Depth0</span><span class="sxs-lookup"><span data-stu-id="2fa04-107">d----- 4/14/2015 5:36 PM Depth0</span></span>

<span data-ttu-id="2fa04-108">-a---4/14/2015 1:19 PM 0 File1.txt</span><span class="sxs-lookup"><span data-stu-id="2fa04-108">-a---- 4/14/2015 1:19 PM 0 File1.txt</span></span>

<span data-ttu-id="2fa04-109">-a---4/14/2015 1:19 PM 0 fájl2.ref fájllal</span><span class="sxs-lookup"><span data-stu-id="2fa04-109">-a---- 4/14/2015 1:19 PM 0 File2.txt</span></span>

<span data-ttu-id="2fa04-110">-a---4/14/2015 1:19 PM 0 File3.txt</span><span class="sxs-lookup"><span data-stu-id="2fa04-110">-a---- 4/14/2015 1:19 PM 0 File3.txt</span></span>

<span data-ttu-id="2fa04-111">PS C:\\felhasználók\\slee\\letölti\\példa&gt; Get-ChildItem-Recurse - mélysége 1</span><span class="sxs-lookup"><span data-stu-id="2fa04-111">PS C:\\Users\\slee\\Downloads\\Example&gt; Get-ChildItem -Recurse -Depth 1</span></span>

<span data-ttu-id="2fa04-112">Könyvtár: C:\\felhasználók\\slee\\letölti\\– példa</span><span class="sxs-lookup"><span data-stu-id="2fa04-112">Directory: C:\\Users\\slee\\Downloads\\Example</span></span>

<span data-ttu-id="2fa04-113">Mód LastWriteTime hossza név</span><span class="sxs-lookup"><span data-stu-id="2fa04-113">Mode LastWriteTime Length Name</span></span>

---- ------------- ------ ----

<span data-ttu-id="2fa04-114">d---4 14 / / 2015 5:36 du Depth0</span><span class="sxs-lookup"><span data-stu-id="2fa04-114">d----- 4/14/2015 5:36 PM Depth0</span></span>

<span data-ttu-id="2fa04-115">-a---4/14/2015 1:19 PM 0 File1.txt</span><span class="sxs-lookup"><span data-stu-id="2fa04-115">-a---- 4/14/2015 1:19 PM 0 File1.txt</span></span>

<span data-ttu-id="2fa04-116">-a---4/14/2015 1:19 PM 0 fájl2.ref fájllal</span><span class="sxs-lookup"><span data-stu-id="2fa04-116">-a---- 4/14/2015 1:19 PM 0 File2.txt</span></span>

<span data-ttu-id="2fa04-117">-a---4/14/2015 1:19 PM 0 File3.txt</span><span class="sxs-lookup"><span data-stu-id="2fa04-117">-a---- 4/14/2015 1:19 PM 0 File3.txt</span></span>

<span data-ttu-id="2fa04-118">Könyvtár: C:\\felhasználók\\slee\\letölti\\példa\\Depth0</span><span class="sxs-lookup"><span data-stu-id="2fa04-118">Directory: C:\\Users\\slee\\Downloads\\Example\\Depth0</span></span>

<span data-ttu-id="2fa04-119">Mód LastWriteTime hossza név</span><span class="sxs-lookup"><span data-stu-id="2fa04-119">Mode LastWriteTime Length Name</span></span>

---- ------------- ------ ----

<span data-ttu-id="2fa04-120">d---4 14 / / 2015 5:33 PM Depth1</span><span class="sxs-lookup"><span data-stu-id="2fa04-120">d----- 4/14/2015 5:33 PM Depth1</span></span>

