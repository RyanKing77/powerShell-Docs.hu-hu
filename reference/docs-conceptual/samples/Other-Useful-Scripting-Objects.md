---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: További hasznos parancsfájl-kezelési objektumok
ms.openlocfilehash: 8d1d10b518d1aadd6aec831b512802558f8fc075
ms.sourcegitcommit: a6f13c16a535acea279c0ddeca72f1f0d8a8ce4c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2019
ms.locfileid: "67030046"
---
# <a name="other-useful-scripting-objects"></a><span data-ttu-id="58ab5-103">További hasznos parancsfájl-kezelési objektumok</span><span class="sxs-lookup"><span data-stu-id="58ab5-103">Other Useful Scripting Objects</span></span>

<span data-ttu-id="58ab5-104">A következő objektumokat adja meg a Windows PowerShell ISE parancsfájl-kezelési funkciókat.</span><span class="sxs-lookup"><span data-stu-id="58ab5-104">The following objects provide additional scripting functionality in Windows PowerShell ISE.</span></span> <span data-ttu-id="58ab5-105">Nem része a **$psISE** hierarchia.</span><span class="sxs-lookup"><span data-stu-id="58ab5-105">They are not part of the **$psISE** hierarchy.</span></span>

## <a name="useful-scripting-objects"></a><span data-ttu-id="58ab5-106">Hasznos parancsfájlkezelés objektumok</span><span class="sxs-lookup"><span data-stu-id="58ab5-106">Useful Scripting objects</span></span>

### <a name="psunsupportedconsoleapplications"></a><span data-ttu-id="58ab5-107">$psUnsupportedConsoleApplications</span><span class="sxs-lookup"><span data-stu-id="58ab5-107">$psUnsupportedConsoleApplications</span></span>

<span data-ttu-id="58ab5-108">Vannak bizonyos korlátai, a Windows PowerShell ISE-ben és konzolalkalmazással együttműködését.</span><span class="sxs-lookup"><span data-stu-id="58ab5-108">There are some limitations on how Windows PowerShell ISE interacts with console applications.</span></span> <span data-ttu-id="58ab5-109">Egy parancs vagy egy automation-szkript, amely felhasználói beavatkozást igényel előfordulhat, hogy úgy működik, a Windows PowerShell-konzolon működik.</span><span class="sxs-lookup"><span data-stu-id="58ab5-109">A command or an automation script that requires user intervention might not work the way it works from the Windows PowerShell console.</span></span> <span data-ttu-id="58ab5-110">Érdemes ezen parancsok vagy parancsfájlok futtatását, a Windows PowerShell ISE-parancs panelen letiltása.</span><span class="sxs-lookup"><span data-stu-id="58ab5-110">You might want to block these commands or scripts from running in the Windows PowerShell ISE Command pane.</span></span> <span data-ttu-id="58ab5-111">A **$psUnsupportedConsoleApplications** objektum tartja az ilyen parancsok listája.</span><span class="sxs-lookup"><span data-stu-id="58ab5-111">The **$psUnsupportedConsoleApplications** object keeps a list of such commands.</span></span> <span data-ttu-id="58ab5-112">Futtassa a parancsokat a listában meg, ha azok nem támogatott üzenetet kap.</span><span class="sxs-lookup"><span data-stu-id="58ab5-112">If you try to run the commands in this list, you get a message that they are not supported.</span></span> <span data-ttu-id="58ab5-113">A következő parancsfájl egy bejegyzés hozzáadása a listához.</span><span class="sxs-lookup"><span data-stu-id="58ab5-113">The following script adds an entry to the list.</span></span>

```powershell
# List the unsupported commands
$psUnsupportedConsoleApplications

# Add a command to this list
$psUnsupportedConsoleApplications.Add('Mycommand')

# Show the augmented list of commands
$psUnsupportedConsoleApplications
```

### <a name="pslocalhelp"></a><span data-ttu-id="58ab5-114">$psLocalHelp</span><span class="sxs-lookup"><span data-stu-id="58ab5-114">$psLocalHelp</span></span>

<span data-ttu-id="58ab5-115">Ez a Súgó-témaköröket és a kapcsolódó hivatkozásokat a helyi lefordított HTML-súgó fájlban közötti környezetfüggő leképezi egy szótár objektumot.</span><span class="sxs-lookup"><span data-stu-id="58ab5-115">This is a dictionary object that maintains a context-sensitive mapping between Help topics and their associated links in the local compiled HTML Help file.</span></span> <span data-ttu-id="58ab5-116">Keresse meg a helyi súgó egy adott témakör szolgál.</span><span class="sxs-lookup"><span data-stu-id="58ab5-116">It is used to locate the local Help for a particular topic.</span></span> <span data-ttu-id="58ab5-117">Adja hozzá, vagy a témakörök törlése a listából.</span><span class="sxs-lookup"><span data-stu-id="58ab5-117">You can add or delete topics from this list.</span></span> <span data-ttu-id="58ab5-118">Az alábbi példakód bemutatja néhány példa található kulcs-érték párok `$psLocalHelp`.</span><span class="sxs-lookup"><span data-stu-id="58ab5-118">The following code example shows some example key-value pairs that are contained in `$psLocalHelp`.</span></span>

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

<span data-ttu-id="58ab5-119">A következő parancsfájl egy bejegyzés hozzáadása a listához.</span><span class="sxs-lookup"><span data-stu-id="58ab5-119">The following script adds an entry to the list.</span></span>

```powershell
$psLocalHelp.Add("get-myNoun", "c:\MyFolder\MyHelpChm.chm::/html/0198854a-1298-57ae-aa0c-87b5e5a84712.htm")
```

### <a name="psonlinehelp"></a><span data-ttu-id="58ab5-120">$psOnlineHelp</span><span class="sxs-lookup"><span data-stu-id="58ab5-120">$psOnlineHelp</span></span>

<span data-ttu-id="58ab5-121">Ez az egy szótárobjektum, amely a környezetfüggő leképezi a súgótémakörök címének és a kapcsolódó külső URL-címek között.</span><span class="sxs-lookup"><span data-stu-id="58ab5-121">This is a dictionary object that maintains a context-sensitive mapping between topic titles of Help topics and their associated external URLs.</span></span> <span data-ttu-id="58ab5-122">Keresse meg az adott témakörre súgója a weben szolgál.</span><span class="sxs-lookup"><span data-stu-id="58ab5-122">It is used to locate the Help for a particular topic on the web.</span></span> <span data-ttu-id="58ab5-123">Adja hozzá, vagy a témakörök törlése a listából.</span><span class="sxs-lookup"><span data-stu-id="58ab5-123">You can add or delete topics from this list.</span></span>

```powershell
$psOnlineHelp | Format-List
```

```output
Key   : Add-Computer
Value : http://go.microsoft.com/fwlink/p/?LinkID=135194

Key   : Add-Content
Value : http://go.microsoft.com/fwlink/p/?LinkID=113278
```

<span data-ttu-id="58ab5-124">A következő parancsfájl egy bejegyzés hozzáadása a listához.</span><span class="sxs-lookup"><span data-stu-id="58ab5-124">The following script adds an entry to the list.</span></span>

```powershell
$psOnlineHelp.Add("get-myNoun", "http://www.mydomain.com/MyNoun.html")
```

## <a name="see-also"></a><span data-ttu-id="58ab5-125">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="58ab5-125">See Also</span></span>

[<span data-ttu-id="58ab5-126">A Windows PowerShell ISE parancsfájl-kezelési objektummodelljének célja</span><span class="sxs-lookup"><span data-stu-id="58ab5-126">Purpose of the Windows PowerShell ISE Scripting Object Model</span></span>](../components/ise/object-model/Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
