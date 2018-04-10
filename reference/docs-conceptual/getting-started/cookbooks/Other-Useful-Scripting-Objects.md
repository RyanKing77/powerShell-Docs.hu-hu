---
ms.date: 06/05/2017
keywords: PowerShell parancsmag
title: További hasznos parancsfájl-kezelési objektumok
ms.assetid: 4d781196-720b-4ccc-90d2-c570e5e719f5
ms.openlocfilehash: 0e87e9919199e011ab5abec5b07dccc8494ad64a
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="other-useful-scripting-objects"></a>További hasznos parancsfájl-kezelési objektumok

A következő objektumok nyújt további parancsfájl-kezelési szolgáltatásokat a Windows PowerShell ISE. Nem része a **$psISE** hierarchia.

## <a name="useful-scripting-objects"></a>Hasznos Scripting objektum

### <a name="psunsupportedconsoleapplications"></a>$psUnsupportedConsoleApplications

A Windows PowerShell ISE konzolon alkalmazások és együttműködését bizonyos korlátozások is. Egy parancs vagy egy felhasználói beavatkozást igénylő automatizálási parancsfájl nem működik a Windows PowerShell-konzolon működési. Érdemes letiltása, hogy a parancsok vagy parancsfájlok futtatását, a Windows PowerShell ISE parancs ablaktáblán. A **$psUnsupportedConsoleApplications** objektum tartja az ilyen parancsok listáját. Futtassa a parancsokat a listában szereplő kísérli meg, ha azok nem támogatott üzenet jelenik meg. A következő parancsfájl egy bejegyzést ad hozzá a listához.

```powershell
# List the unsupported commands
$psUnsupportedConsoleApplications

# Add a command to this list
$psUnsupportedConsoleApplications.Add('Mycommand')

# Show the augmented list of commands
$psUnsupportedConsoleApplications
```

### <a name="pslocalhelp"></a>$psLocalHelp

Ez az egy dictionary objektum, amely a környezetfüggő Súgó-témaköröket és a kapcsolódó hivatkozások a helyi lefordított HTML-súgófájl közötti leképezéseket kezeli. Keresse meg a helyi súgó adott témakörre szolgál. Adja hozzá, vagy témakörök törlése a listáról. Az alábbi példakód mutatja néhány példa található kulcs-érték párok **$psLocalHelp**.

```powershell
# See the local help map
$psLocalHelp | Format-List
```

### <a name="sample-output"></a>Kimenetminta

|||
|-|-|
|Kulcs:-Számítógép hozzáadása|Value : WindowsPowerShellHelp.chm::/html/093f660c-b8d5-43cf-aa0c-54e5e54e76f9.htm|
|Kulcs:-Tartalom|Value : WindowsPowerShellHelp.chm::/html/0c836a1b-f389-4e9a-9325-0f415686d194.htm|

A következő parancsfájl egy bejegyzést ad hozzá a listához.

```powershell
$psLocalHelp.Add("get-myNoun", "c:\MyFolder\MyHelpChm.chm::/html/0198854a-1298-57ae-aa0c-87b5e5a84712.htm")
```

### <a name="psonlinehelp"></a>$psOnlineHelp

Ez az egy dictionary objektum, amely egy környezetfüggő leképezése súgótémakörök címének és a hozzájuk társított külső URL-címeket tart fenn. Keresse meg a Súgó gombra egy adott témakör a weben szolgál. Adja hozzá, vagy témakörök törlése a listáról.

```powershell
$psOnlineHelp | Format-List
```

### <a name="sample-output"></a>Kimenetminta

|||
|-|-|
|Kulcs:-Számítógép hozzáadása|Érték: http://go.microsoft.com/fwlink/p/?LinkID=135194|
|Kulcs:-Tartalom|Érték: http://go.microsoft.com/fwlink/p/?LinkID=113278|

 A következő parancsfájl egy bejegyzést ad hozzá a listához.

```powershell
$psOnlineHelp.Add("get-myNoun", "http://www.mydomain.com/MyNoun.html")
```

## <a name="see-also"></a>Lásd még:

- [A Windows PowerShell ISE objektummodell Scripting célja](../../core-powershell/ise/Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)