---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: aa2e9540af8b3d4c5de5e00377a84e0e5edd6e4a
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55685115"
---
# <a name="new-temporaryfile"></a><span data-ttu-id="1c0ba-102">New-TemporaryFile</span><span class="sxs-lookup"><span data-stu-id="1c0ba-102">New-TemporaryFile</span></span>
<span data-ttu-id="1c0ba-103">Egyes esetekben a parancsfájlok kell létrehoznia egy ideiglenes fájlt.</span><span class="sxs-lookup"><span data-stu-id="1c0ba-103">Sometimes in your scripts, you must create a temporary file.</span></span> <span data-ttu-id="1c0ba-104">Könnyedén megteheti az ezt a **New-TemporaryFile** parancsmagot:</span><span class="sxs-lookup"><span data-stu-id="1c0ba-104">You can easily do this with the **New-TemporaryFile** cmdlet:</span></span>

<span data-ttu-id="1c0ba-105">PS C:\\ &gt; $tempFile = New-TemporaryFile</span><span class="sxs-lookup"><span data-stu-id="1c0ba-105">PS C:\\&gt; $tempFile = New-TemporaryFile</span></span>

<span data-ttu-id="1c0ba-106">PS C:\\&gt; $tempFile.FullName</span><span class="sxs-lookup"><span data-stu-id="1c0ba-106">PS C:\\&gt; $tempFile.FullName</span></span>

<span data-ttu-id="1c0ba-107">C:\\felhasználók\\slee\\AppData\\helyi\\Temp\\tmp375.tmp</span><span class="sxs-lookup"><span data-stu-id="1c0ba-107">C:\\Users\\slee\\AppData\\Local\\Temp\\tmp375.tmp</span></span>
