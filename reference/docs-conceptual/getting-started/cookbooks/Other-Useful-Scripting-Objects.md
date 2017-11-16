---
ms.date: 2017-06-05
keywords: PowerShell parancsmag
title: "Egyéb hasznos parancsfájl-kezelési objektumok"
ms.assetid: 4d781196-720b-4ccc-90d2-c570e5e719f5
ms.openlocfilehash: 8334d0b346e59dea3643a93bf52b780b361d1945
ms.sourcegitcommit: 74255f0b5f386a072458af058a15240140acb294
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/03/2017
---
# <a name="other-useful-scripting-objects"></a><span data-ttu-id="746ab-103">Egyéb hasznos parancsfájl-kezelési objektumok</span><span class="sxs-lookup"><span data-stu-id="746ab-103">Other Useful Scripting Objects</span></span>
  <span data-ttu-id="746ab-104">A következő objektumok nyújt további parancsfájl-kezelési szolgáltatásokat a Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="746ab-104">The following objects provide additional scripting functionality in Windows PowerShell ISE.</span></span> <span data-ttu-id="746ab-105">Nem része a **$psISE** hierarchia.</span><span class="sxs-lookup"><span data-stu-id="746ab-105">They are not part of the **$psISE** hierarchy.</span></span>

## <a name="useful-scripting-objects"></a><span data-ttu-id="746ab-106">Hasznos Scripting objektum</span><span class="sxs-lookup"><span data-stu-id="746ab-106">Useful Scripting objects</span></span>

### <a name="psunsupportedconsoleapplications"></a><span data-ttu-id="746ab-107">$psUnsupportedConsoleApplications</span><span class="sxs-lookup"><span data-stu-id="746ab-107">$psUnsupportedConsoleApplications</span></span>
 <span data-ttu-id="746ab-108">A Windows PowerShell ISE konzolon alkalmazások és együttműködését bizonyos korlátozások is.</span><span class="sxs-lookup"><span data-stu-id="746ab-108">There are some limitations on how Windows PowerShell ISE interacts with console applications.</span></span> <span data-ttu-id="746ab-109">Egy parancs vagy egy felhasználói beavatkozást igénylő automatizálási parancsfájl nem működik a Windows PowerShell-konzolon működési.</span><span class="sxs-lookup"><span data-stu-id="746ab-109">A command or an automation script that requires user intervention might not work the way it works from the Windows PowerShell console.</span></span> <span data-ttu-id="746ab-110">Érdemes letiltása, hogy a parancsok vagy parancsfájlok futtatását, a Windows PowerShell ISE parancs ablaktáblán.</span><span class="sxs-lookup"><span data-stu-id="746ab-110">You might want to block these commands or scripts from running in the Windows PowerShell ISE Command pane.</span></span> <span data-ttu-id="746ab-111">A **$psUnsupportedConsoleApplications** objektum tartja az ilyen parancsok listáját.</span><span class="sxs-lookup"><span data-stu-id="746ab-111">The **$psUnsupportedConsoleApplications** object keeps a list of such commands.</span></span> <span data-ttu-id="746ab-112">Futtassa a parancsokat a listában szereplő kísérli meg, ha azok nem támogatott üzenet jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="746ab-112">If you try to run the commands in this list, you get a message that they are not supported.</span></span> <span data-ttu-id="746ab-113">A következő parancsfájl egy bejegyzést ad hozzá a listához.</span><span class="sxs-lookup"><span data-stu-id="746ab-113">The following script adds an entry to the list.</span></span>

```
# List the unsupported commands
psUnsupportedConsoleApplications
# Add a command to this list
psUnsupportedConsoleApplications.Add(“Mycommand”)
#Show the augmented list of commands
psUnsupportedConsoleApplications

```

### <a name="pslocalhelp"></a><span data-ttu-id="746ab-114">$psLocalHelp</span><span class="sxs-lookup"><span data-stu-id="746ab-114">$psLocalHelp</span></span>
 <span data-ttu-id="746ab-115">Ez az egy dictionary objektum, amely a környezetfüggő Súgó-témaköröket és a kapcsolódó hivatkozások a helyi lefordított HTML-súgófájl közötti leképezéseket kezeli.</span><span class="sxs-lookup"><span data-stu-id="746ab-115">This is a dictionary object that maintains a context-sensitive mapping between Help topics and their associated links in the local compiled HTML Help file.</span></span> <span data-ttu-id="746ab-116">Keresse meg a helyi súgó adott témakörre szolgál.</span><span class="sxs-lookup"><span data-stu-id="746ab-116">It is used to locate the local Help for a particular topic.</span></span> <span data-ttu-id="746ab-117">Adja hozzá, vagy témakörök törlése a listáról.</span><span class="sxs-lookup"><span data-stu-id="746ab-117">You can add or delete topics from this list.</span></span> <span data-ttu-id="746ab-118">Az alábbi példakód mutatja néhány példa található kulcs-érték párok **$psLocalHelp**.</span><span class="sxs-lookup"><span data-stu-id="746ab-118">The following code example shows some example key-value pairs that are contained in **$psLocalHelp**.</span></span>

```
# See the local help map
$psLocalHelp | Format-List

```

### <a name="sample-output"></a><span data-ttu-id="746ab-119">Kimenetminta</span><span class="sxs-lookup"><span data-stu-id="746ab-119">Sample Output</span></span>

|||
|-|-|
|<span data-ttu-id="746ab-120">Kulcs:-Számítógép hozzáadása</span><span class="sxs-lookup"><span data-stu-id="746ab-120">Key : Add-Computer</span></span>|<span data-ttu-id="746ab-121">Érték: WindowsPowerShellHelp.chm::/html/093f660c-b8d5-43cf-aa0c-54e5e54e76f9.htm</span><span class="sxs-lookup"><span data-stu-id="746ab-121">Value : WindowsPowerShellHelp.chm::/html/093f660c-b8d5-43cf-aa0c-54e5e54e76f9.htm</span></span>|
|<span data-ttu-id="746ab-122">Kulcs:-Tartalom</span><span class="sxs-lookup"><span data-stu-id="746ab-122">Key : Add-Content</span></span>|<span data-ttu-id="746ab-123">Érték: WindowsPowerShellHelp.chm::/html/0c836a1b-f389-4e9a-9325-0f415686d194.htm</span><span class="sxs-lookup"><span data-stu-id="746ab-123">Value : WindowsPowerShellHelp.chm::/html/0c836a1b-f389-4e9a-9325-0f415686d194.htm</span></span>|

 <span data-ttu-id="746ab-124">A következő parancsfájl egy bejegyzést ad hozzá a listához.</span><span class="sxs-lookup"><span data-stu-id="746ab-124">The following script adds an entry to the list.</span></span>

```
$psLocalHelp.Add("get-myNoun","c:\MyFolder\MyHelpChm.chm::/html/0198854a-1298-57ae-aa0c-87b5e5a84712.htm")
```

### <a name="psonlinehelp"></a><span data-ttu-id="746ab-125">$psOnlineHelp</span><span class="sxs-lookup"><span data-stu-id="746ab-125">$psOnlineHelp</span></span>
 <span data-ttu-id="746ab-126">Ez az egy dictionary objektum, amely egy környezetfüggő leképezése súgótémakörök címének és a hozzájuk társított külső URL-címeket tart fenn.</span><span class="sxs-lookup"><span data-stu-id="746ab-126">This is a dictionary object that maintains a context-sensitive mapping between topic titles of Help topics and their associated external URLs.</span></span> <span data-ttu-id="746ab-127">Keresse meg a Súgó gombra egy adott témakör a weben szolgál.</span><span class="sxs-lookup"><span data-stu-id="746ab-127">It is used to locate the Help for a particular topic on the web.</span></span> <span data-ttu-id="746ab-128">Adja hozzá, vagy témakörök törlése a listáról.</span><span class="sxs-lookup"><span data-stu-id="746ab-128">You can add or delete topics from this list.</span></span>

```
$psOnlineHelp | Format-List

```

### <a name="sample-output"></a><span data-ttu-id="746ab-129">Kimenetminta</span><span class="sxs-lookup"><span data-stu-id="746ab-129">Sample Output</span></span>

|||
|-|-|
|<span data-ttu-id="746ab-130">Kulcs:-Számítógép hozzáadása</span><span class="sxs-lookup"><span data-stu-id="746ab-130">Key : Add-Computer</span></span>|<span data-ttu-id="746ab-131">Érték: http://go.microsoft.com/fwlink/p/?LinkID=135194</span><span class="sxs-lookup"><span data-stu-id="746ab-131">Value : http://go.microsoft.com/fwlink/p/?LinkID=135194</span></span>|
|<span data-ttu-id="746ab-132">Kulcs:-Tartalom</span><span class="sxs-lookup"><span data-stu-id="746ab-132">Key : Add-Content</span></span>|<span data-ttu-id="746ab-133">Érték: http://go.microsoft.com/fwlink/p/?LinkID=113278</span><span class="sxs-lookup"><span data-stu-id="746ab-133">Value : http://go.microsoft.com/fwlink/p/?LinkID=113278</span></span>|

 <span data-ttu-id="746ab-134">A következő parancsfájl egy bejegyzést ad hozzá a listához.</span><span class="sxs-lookup"><span data-stu-id="746ab-134">The following script adds an entry to the list.</span></span>

```
$psOnlineHelp.Add("get-myNoun","http://www.mydomain.com/MyNoun.html")
```

## <a name="see-also"></a><span data-ttu-id="746ab-135">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="746ab-135">See Also</span></span>
- [<span data-ttu-id="746ab-136">A Windows PowerShell ISE Scripting Hálózatiobjektum-modellje</span><span class="sxs-lookup"><span data-stu-id="746ab-136">The Windows PowerShell ISE Scripting Object Model</span></span>](../../core-powershell/ise/The-Windows-PowerShell-ISE-Scripting-Object-Model.md)

  
