---
title: Egyéni állomást mintát |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 55aee25b-bbcb-4d41-a4c0-fb8e30c4cdc1
caps.latest.revision: 11
ms.openlocfilehash: 1e58b74cf1c37c70ebfb0f4970cfbf8a8263ec5c
ms.sourcegitcommit: 5990f04b8042ef2d8e571bec6d5b051e64c9921c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/12/2019
ms.locfileid: "57794144"
---
# <a name="custom-host-samples"></a><span data-ttu-id="0407d-102">Egyéni gazdaminták</span><span class="sxs-lookup"><span data-stu-id="0407d-102">Custom Host Samples</span></span>

<span data-ttu-id="0407d-103">Ez a szakasz egy egyéni gazdagép írására szolgáló mintakód tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="0407d-103">This section includes sample code for writing a custom host.</span></span> <span data-ttu-id="0407d-104">Microsoft Visual Studio segítségével hozzon létre egy konzolalkalmazást, majd a kódot bemásolhatja a témakörei ebben a szakaszban a gazdaalkalmazást.</span><span class="sxs-lookup"><span data-stu-id="0407d-104">You can use Microsoft Visual Studio to create a console application and then copy the code from the topics in this section into your host application.</span></span>

## <a name="in-this-section"></a><span data-ttu-id="0407d-105">A szakasz tartalma</span><span class="sxs-lookup"><span data-stu-id="0407d-105">In This Section</span></span>

 <span data-ttu-id="0407d-106">[Host01 minta](./host01-sample.md) Ez a példa bemutatja, hogyan valósíthat meg egy alapszintű egyéni gazdagép használó gazdagép-alkalmazás.</span><span class="sxs-lookup"><span data-stu-id="0407d-106">[Host01 Sample](./host01-sample.md) This sample shows how to implement a host application that uses a basic custom host.</span></span>

 <span data-ttu-id="0407d-107">[Host02 minta](./host02-sample.md) Ez a példa bemutatja, hogyan írhat egy gazdagép egy egyéni gazdagép megvalósítás mellett a Windows PowerShell modul használó alkalmazás.</span><span class="sxs-lookup"><span data-stu-id="0407d-107">[Host02 Sample](./host02-sample.md) This sample shows how to write a host application that uses the Windows PowerShell runtime along with a custom host implementation.</span></span> <span data-ttu-id="0407d-108">A gazdaalkalmazást állítja be a gazdagép kulturális környezet német, lefut a [Get-Process](/powershell/module/Microsoft.PowerShell.Management/Get-Process) parancsmagot, és megjeleníti az eredményeket, látnák őket a német nyelven pwrsh.exe és majd jelenít meg az aktuális dátumát és időpontját.</span><span class="sxs-lookup"><span data-stu-id="0407d-108">The host application sets the host culture to German, runs the [Get-Process](/powershell/module/Microsoft.PowerShell.Management/Get-Process) cmdlet and displays the results as you would see them using pwrsh.exe, and then prints out the current data and time in German.</span></span>

 <span data-ttu-id="0407d-109">[Host03 minta](./host03-sample.md) Ez a példa bemutatja, hogyan hozhat létre olyan interaktív konzol-alapú gazdagép alkalmazás, amely beolvassa a parancsok a parancssorból, a parancsok végrehajtása és az eredményeket a konzolon jeleníti meg.</span><span class="sxs-lookup"><span data-stu-id="0407d-109">[Host03 Sample](./host03-sample.md) This sample shows how to build an interactive console-based host application that reads commands from the command line, executes the commands, and then displays the results to the console.</span></span>

 <span data-ttu-id="0407d-110">[Host04 minta](./host04-sample.md) Ez a példa bemutatja, hogyan hozhat létre olyan interaktív konzol-alapú gazdagép alkalmazás, amely beolvassa a parancsok a parancssorból, a parancsok végrehajtása és az eredményeket a konzolon jeleníti meg.</span><span class="sxs-lookup"><span data-stu-id="0407d-110">[Host04 Sample](./host04-sample.md) This sample shows how to build an interactive console-based host application that reads commands from the command line, executes the commands, and then displays the results to the console.</span></span> <span data-ttu-id="0407d-111">A gazdaalkalmazást megjelenítésének utasításokat, amelyek lehetővé teszik a felhasználó megadhatja a több lehetőség is támogatja.</span><span class="sxs-lookup"><span data-stu-id="0407d-111">This host application also supports displaying prompts that allow the user to specify multiple choices.</span></span>

 <span data-ttu-id="0407d-112">[Host05 minta](./host05-sample.md) Ez a példa bemutatja, hogyan hozhat létre olyan interaktív konzol-alapú gazdagép alkalmazás, amely beolvassa a parancsok a parancssorból, a parancsok végrehajtása és az eredményeket a konzolon jeleníti meg.</span><span class="sxs-lookup"><span data-stu-id="0407d-112">[Host05 Sample](./host05-sample.md) This sample shows how to build an interactive console-based host application that reads commands from the command line, executes the commands, and then displays the results to the console.</span></span> <span data-ttu-id="0407d-113">A gazdaalkalmazást is támogatja a távoli számítógépek hívásainak a [Enter-PsSession](/powershell/module/Microsoft.PowerShell.Core/Enter-PSSession) és [kilépési-PsSession](/powershell/module/Microsoft.PowerShell.Core/Exit-PSSession) parancsmagok</span><span class="sxs-lookup"><span data-stu-id="0407d-113">This host application also supports calls to remote computers by using the [Enter-PsSession](/powershell/module/Microsoft.PowerShell.Core/Enter-PSSession) and [Exit-PsSession](/powershell/module/Microsoft.PowerShell.Core/Exit-PSSession) cmdlets</span></span>

 <span data-ttu-id="0407d-114">[Host06 minta](./host06-sample.md) Ez a példa bemutatja, hogyan hozhat létre olyan interaktív konzol-alapú gazdagép alkalmazás, amely beolvassa a parancsok a parancssorból, a parancsok végrehajtása és az eredményeket a konzolon jeleníti meg.</span><span class="sxs-lookup"><span data-stu-id="0407d-114">[Host06 Sample](./host06-sample.md) This sample shows how to build an interactive console-based host application that reads commands from the command line, executes the commands, and then displays the results to the console.</span></span> <span data-ttu-id="0407d-115">Emellett ez a példa a jogkivonatokat létrehozó API-k segítségével adja meg a felhasználó által beírt szöveg színe.</span><span class="sxs-lookup"><span data-stu-id="0407d-115">In addition, this sample uses the Tokenizer APIs to specify the color of the text that is entered by the user.</span></span>

## <a name="see-also"></a><span data-ttu-id="0407d-116">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="0407d-116">See Also</span></span>
