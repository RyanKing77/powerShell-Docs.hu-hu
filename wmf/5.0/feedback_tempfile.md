---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 08f431c27cd0ee769518b5246af2fa95aa499d54
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2018
---
# <a name="new-temporaryfile"></a><span data-ttu-id="4467e-102">New-TemporaryFile</span><span class="sxs-lookup"><span data-stu-id="4467e-102">New-TemporaryFile</span></span>
<span data-ttu-id="4467e-103">Egyes esetekben a parancsfájlokban kell létrehoznia egy ideiglenes fájlt.</span><span class="sxs-lookup"><span data-stu-id="4467e-103">Sometimes in your scripts, you must create a temporary file.</span></span> <span data-ttu-id="4467e-104">Könnyen ehhez a a **New-TemporaryFile** parancsmagot:</span><span class="sxs-lookup"><span data-stu-id="4467e-104">You can easily do this with the **New-TemporaryFile** cmdlet:</span></span>

<span data-ttu-id="4467e-105">PS C:\\ &gt; $tempFile = New-TemporaryFile</span><span class="sxs-lookup"><span data-stu-id="4467e-105">PS C:\\&gt; $tempFile = New-TemporaryFile</span></span>

<span data-ttu-id="4467e-106">PS C:\\ &gt; $tempFile.FullName</span><span class="sxs-lookup"><span data-stu-id="4467e-106">PS C:\\&gt; $tempFile.FullName</span></span>

<span data-ttu-id="4467e-107">C:\\felhasználók\\slee\\AppData\\helyi\\Temp\\tmp375.tmp</span><span class="sxs-lookup"><span data-stu-id="4467e-107">C:\\Users\\slee\\AppData\\Local\\Temp\\tmp375.tmp</span></span>
