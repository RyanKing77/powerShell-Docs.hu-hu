---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: További hasznos parancsfájl-kezelési objektumok
ms.assetid: 4d781196-720b-4ccc-90d2-c570e5e719f5
ms.openlocfilehash: ff494f375c0d43d83b2a067dbe4f2ab35a90d564
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62086204"
---
# <a name="other-useful-scripting-objects"></a>További hasznos parancsfájl-kezelési objektumok

A következő objektumokat adja meg a Windows PowerShell ISE parancsfájl-kezelési funkciókat. Nem része a **$psISE** hierarchia.

## <a name="useful-scripting-objects"></a>Hasznos parancsfájlkezelés objektumok

### <a name="psunsupportedconsoleapplications"></a>$psUnsupportedConsoleApplications

Vannak bizonyos korlátai, a Windows PowerShell ISE-ben és konzolalkalmazással együttműködését. Egy parancs vagy egy automation-szkript, amely felhasználói beavatkozást igényel előfordulhat, hogy úgy működik, a Windows PowerShell-konzolon működik. Érdemes ezen parancsok vagy parancsfájlok futtatását, a Windows PowerShell ISE-parancs panelen letiltása. A **$psUnsupportedConsoleApplications** objektum tartja az ilyen parancsok listája. Futtassa a parancsokat a listában meg, ha azok nem támogatott üzenetet kap. A következő parancsfájl egy bejegyzés hozzáadása a listához.

```powershell
# List the unsupported commands
$psUnsupportedConsoleApplications

# Add a command to this list
$psUnsupportedConsoleApplications.Add('Mycommand')

# Show the augmented list of commands
$psUnsupportedConsoleApplications
```

### <a name="pslocalhelp"></a>$psLocalHelp

Ez a Súgó-témaköröket és a kapcsolódó hivatkozásokat a helyi lefordított HTML-súgó fájlban közötti környezetfüggő leképezi egy szótár objektumot. Keresse meg a helyi súgó egy adott témakör szolgál. Adja hozzá, vagy a témakörök törlése a listából. Az alábbi példakód bemutatja néhány példa található kulcs-érték párok `$psLocalHelp`.

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

A következő parancsfájl egy bejegyzés hozzáadása a listához.

```powershell
$psLocalHelp.Add("get-myNoun", "c:\MyFolder\MyHelpChm.chm::/html/0198854a-1298-57ae-aa0c-87b5e5a84712.htm")
```

### <a name="psonlinehelp"></a>$psOnlineHelp

Ez az egy szótárobjektum, amely a környezetfüggő leképezi a súgótémakörök címének és a kapcsolódó külső URL-címek között. Keresse meg az adott témakörre súgója a weben szolgál. Adja hozzá, vagy a témakörök törlése a listából.

```powershell
$psOnlineHelp | Format-List
```

```output
Key   : Add-Computer
Value : http://go.microsoft.com/fwlink/p/?LinkID=135194

Key   : Add-Content
Value : http://go.microsoft.com/fwlink/p/?LinkID=113278
```

A következő parancsfájl egy bejegyzés hozzáadása a listához.

```powershell
$psOnlineHelp.Add("get-myNoun", "http://www.mydomain.com/MyNoun.html")
```

## <a name="see-also"></a>Lásd még:

[A Windows PowerShell ISE parancsfájl-kezelési objektummodelljének célja](../components/ise/object-model/Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)