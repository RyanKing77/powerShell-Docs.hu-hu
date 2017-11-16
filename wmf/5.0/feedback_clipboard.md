---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "WMF, a powershell, a beállítása"
ms.openlocfilehash: 8d5f8cc8c85d584b195483e464e878857629a78e
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
# <a name="clipboard-cmdlets"></a>Vágólap-parancsmagok
**Get-vágólapra** és **Set-vágólapra** megkönnyítik a tartalomátvitelt a és a Windows PowerShell-munkamenetben. Például, ha a Windows Intéző segítségével három fájlok másolása a vágólapra (jelölje ki őket, és nyomja le `ctrl-c`, például), majd egyszerűen elérhetők a vágólap tartalmát, a fájlok listáját:

```powershell 
PS C:\\&gt; Get-Clipboard -Format FileDropList

Directory: C:\\Users\\slee\\Downloads\\Example

Mode LastWriteTime Length Name

---- ------------- ------ ----

-a---- 4/14/2015 1:19 PM 0 File2.txt

-a---- 4/14/2015 1:19 PM 0 File3.txt

-a---- 4/14/2015 1:19 PM 0 File1.txt
```


A vágólap parancsmagok támogatja a képek, a hangfájlok, a fájl listák és a szöveg.

