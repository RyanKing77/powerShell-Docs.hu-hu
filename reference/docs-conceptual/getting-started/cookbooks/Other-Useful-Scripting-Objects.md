---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: További hasznos parancsfájl-kezelési objektumok
ms.assetid: 4d781196-720b-4ccc-90d2-c570e5e719f5
ms.openlocfilehash: 58acfd05ff1ae1d9aa5f3a3576b8fb320ba4abbd
ms.sourcegitcommit: 77f62a55cac8c13d69d51eef5fade18f71d66955
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/17/2018
ms.locfileid: "39093905"
---
# <a name="other-useful-scripting-objects"></a><span data-ttu-id="407ac-103">További hasznos parancsfájl-kezelési objektumok</span><span class="sxs-lookup"><span data-stu-id="407ac-103">Other Useful Scripting Objects</span></span>

<span data-ttu-id="407ac-104">A következő objektumokat adja meg a Windows PowerShell ISE parancsfájl-kezelési funkciókat.</span><span class="sxs-lookup"><span data-stu-id="407ac-104">The following objects provide additional scripting functionality in Windows PowerShell ISE.</span></span> <span data-ttu-id="407ac-105">Nem része a **$psISE** hierarchia.</span><span class="sxs-lookup"><span data-stu-id="407ac-105">They are not part of the **$psISE** hierarchy.</span></span>

## <a name="useful-scripting-objects"></a><span data-ttu-id="407ac-106">Hasznos parancsfájlkezelés objektumok</span><span class="sxs-lookup"><span data-stu-id="407ac-106">Useful Scripting objects</span></span>

### <a name="psunsupportedconsoleapplications"></a><span data-ttu-id="407ac-107">$psUnsupportedConsoleApplications</span><span class="sxs-lookup"><span data-stu-id="407ac-107">$psUnsupportedConsoleApplications</span></span>

<span data-ttu-id="407ac-108">Vannak bizonyos korlátai, a Windows PowerShell ISE-ben és konzolalkalmazással együttműködését.</span><span class="sxs-lookup"><span data-stu-id="407ac-108">There are some limitations on how Windows PowerShell ISE interacts with console applications.</span></span> <span data-ttu-id="407ac-109">Egy parancs vagy egy automation-szkript, amely felhasználói beavatkozást igényel előfordulhat, hogy úgy működik, a Windows PowerShell-konzolon működik.</span><span class="sxs-lookup"><span data-stu-id="407ac-109">A command or an automation script that requires user intervention might not work the way it works from the Windows PowerShell console.</span></span> <span data-ttu-id="407ac-110">Érdemes ezen parancsok vagy parancsfájlok futtatását, a Windows PowerShell ISE-parancs panelen letiltása.</span><span class="sxs-lookup"><span data-stu-id="407ac-110">You might want to block these commands or scripts from running in the Windows PowerShell ISE Command pane.</span></span> <span data-ttu-id="407ac-111">A **$psUnsupportedConsoleApplications** objektum tartja az ilyen parancsok listája.</span><span class="sxs-lookup"><span data-stu-id="407ac-111">The **$psUnsupportedConsoleApplications** object keeps a list of such commands.</span></span> <span data-ttu-id="407ac-112">Futtassa a parancsokat a listában meg, ha azok nem támogatott üzenetet kap.</span><span class="sxs-lookup"><span data-stu-id="407ac-112">If you try to run the commands in this list, you get a message that they are not supported.</span></span> <span data-ttu-id="407ac-113">A következő parancsfájl egy bejegyzés hozzáadása a listához.</span><span class="sxs-lookup"><span data-stu-id="407ac-113">The following script adds an entry to the list.</span></span>

```powershell
# List the unsupported commands
$psUnsupportedConsoleApplications

# Add a command to this list
$psUnsupportedConsoleApplications.Add('Mycommand')

# Show the augmented list of commands
$psUnsupportedConsoleApplications
```

### <a name="pslocalhelp"></a><span data-ttu-id="407ac-114">$psLocalHelp</span><span class="sxs-lookup"><span data-stu-id="407ac-114">$psLocalHelp</span></span>

<span data-ttu-id="407ac-115">Ez a Súgó-témaköröket és a kapcsolódó hivatkozásokat a helyi lefordított HTML-súgó fájlban közötti környezetfüggő leképezi egy szótár objektumot.</span><span class="sxs-lookup"><span data-stu-id="407ac-115">This is a dictionary object that maintains a context-sensitive mapping between Help topics and their associated links in the local compiled HTML Help file.</span></span> <span data-ttu-id="407ac-116">Keresse meg a helyi súgó egy adott témakör szolgál.</span><span class="sxs-lookup"><span data-stu-id="407ac-116">It is used to locate the local Help for a particular topic.</span></span> <span data-ttu-id="407ac-117">Adja hozzá, vagy a témakörök törlése a listából.</span><span class="sxs-lookup"><span data-stu-id="407ac-117">You can add or delete topics from this list.</span></span> <span data-ttu-id="407ac-118">Az alábbi példakód bemutatja néhány példa található kulcs-érték párok `$psLocalHelp`.</span><span class="sxs-lookup"><span data-stu-id="407ac-118">The following code example shows some example key-value pairs that are contained in `$psLocalHelp`.</span></span>

```powershell
# See the local help map
$psLocalHelp | Format-List
```

```output
Key   : Add-Computer
Value : WindowsPowerShellHelp.chm::/html/093f660c-b8d5-43cf-aa0c-54e5e54e76f9.htm

Key   : Add-Content
Value : WindowsPowerShellHelp.chm::/html/0c836a1b-f389-4e9a-9325-0f415686d194.htm
```

<span data-ttu-id="407ac-119">A következő parancsfájl egy bejegyzés hozzáadása a listához.</span><span class="sxs-lookup"><span data-stu-id="407ac-119">The following script adds an entry to the list.</span></span>

```powershell
$psLocalHelp.Add("get-myNoun", "c:\MyFolder\MyHelpChm.chm::/html/0198854a-1298-57ae-aa0c-87b5e5a84712.htm")
```

### <a name="psonlinehelp"></a><span data-ttu-id="407ac-120">$psOnlineHelp</span><span class="sxs-lookup"><span data-stu-id="407ac-120">$psOnlineHelp</span></span>

<span data-ttu-id="407ac-121">Ez az egy szótárobjektum, amely a környezetfüggő leképezi a súgótémakörök címének és a kapcsolódó külső URL-címek között.</span><span class="sxs-lookup"><span data-stu-id="407ac-121">This is a dictionary object that maintains a context-sensitive mapping between topic titles of Help topics and their associated external URLs.</span></span> <span data-ttu-id="407ac-122">Keresse meg az adott témakörre súgója a weben szolgál.</span><span class="sxs-lookup"><span data-stu-id="407ac-122">It is used to locate the Help for a particular topic on the web.</span></span> <span data-ttu-id="407ac-123">Adja hozzá, vagy a témakörök törlése a listából.</span><span class="sxs-lookup"><span data-stu-id="407ac-123">You can add or delete topics from this list.</span></span>

```powershell
$psOnlineHelp | Format-List
```

```output
Key   : Add-Computer
Value : http://go.microsoft.com/fwlink/p/?LinkID=135194

Key   : Add-Content
Value : http://go.microsoft.com/fwlink/p/?LinkID=113278
```

<span data-ttu-id="407ac-124">A következő parancsfájl egy bejegyzés hozzáadása a listához.</span><span class="sxs-lookup"><span data-stu-id="407ac-124">The following script adds an entry to the list.</span></span>

```powershell
$psOnlineHelp.Add("get-myNoun", "http://www.mydomain.com/MyNoun.html")
```

## <a name="see-also"></a><span data-ttu-id="407ac-125">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="407ac-125">See Also</span></span>

[<span data-ttu-id="407ac-126">A Windows PowerShell ISE parancsfájl-kezelési objektummodelljének célja</span><span class="sxs-lookup"><span data-stu-id="407ac-126">Purpose of the Windows PowerShell ISE Scripting Object Model</span></span>](../../core-powershell/ise/Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)