---
title: 'Frissíthető súgó írása: Részletes |} A Microsoft Docs'
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 10098160-c6b4-4339-b8ff-2c4f8cc0699b
caps.latest.revision: 13
ms.openlocfilehash: fbc77cc0fafce93d239da1c459d4b761b21ef3cb
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56849832"
---
# <a name="updatable-help-authoring-step-by-step"></a>Frissíthető súgó írása: Részletes útmutató

A dokumentumok frissíthető súgó szerzői lépéseit sorolja fel.

## <a name="authoring-updatable-help-step-by-step"></a>Frissíthető súgó szerzői: Részletes útmutató

Frissíthető súgó célja a végfelhasználók számára, de jelentős előnyöket is kínál, a modul szerzőknek súgó írók, lehetővé teszi, hogy tartalmat, beleértve javítsa a hibákat, alatt több felhasználói felületi kulturális környezetek, valamint választ után mennyi ideig felhasználói megjegyzések és a kérelmek, a a modul postáztuk. Ez a témakör azt ismerteti, hogyan csomag és a feltöltés súgó, hogy a felhasználók letöltheti és telepítheti azokat a fájlokat a [Update-Help](/powershell/module/Microsoft.PowerShell.Core/Update-Help) és [Save-Help](/powershell/module/Microsoft.PowerShell.Core/Save-Help) parancsmagok.

Az alábbi lépéseket nyújt áttekintést a folyamat a frissíthető súgó támogatása.

### <a name="step-1-find-an-internet-site-for-your-help-files"></a>1. lépés: A súgófájlok internetes hely keresése

Frissíthető súgó létrehozásának első lépése, hogy az interneten található, a modul Súgó fájlok megtalálja. Valójában két különböző helyen is használhatja. A modul súgó információs fájl (HelpInfo XML - alább ismertetett) is megőrizheti az Internet egyetlen helyen, és a súgó tartalom CAB-fájlok internetes egy másik helyen. Súgó CAB tartozó összes tartalomfájlt modul ugyanazon a helyen kell lennie. Súgó tartalma CAB-fájlok eltérő modulok helyezheti ugyanazon a helyen.

### <a name="step-2-add-a-helpinfouri-key-to-your-module-manifest"></a>2. lépés: A moduljegyzék HelpInfoURI kulcs hozzáadása

Adjon hozzá egy **HelpInfoURI** a moduljegyzék kulcs. A kulcs értéke az egységes erőforrás-azonosító (URI) annak a helynek a modul HelpInfo XML-információs fájl. A biztonság érdekében a címet kell kezdődniük "http" vagy "https". Az URI-t kell megadnia az interneten található, de a HelpInfo XML-fájl neve nem tartalmazhat.

Például:

```powershell

@{
RootModule = TestModule.psm1
ModuleVersion = '2.0'
HelpInfoURI = 'http://go.microsoft.com/fwlink/?LinkID=0123'
}
```

### <a name="step-3-create-a-helpinfo-xml-file"></a>3. lépés: Egy HelpInfo XML-fájl létrehozása

A HelpInfo XML fájl tartalmaz URI-ját a súgófájlok és a legújabb súgófájlokat, az egyes támogatott felhasználói felület kultúrafüggő részletei a modul verziószámát az Internet helyét. Minden Windows PowerShell-modul egy HelpInfo XML-fájlt tartalmaz. Amikor frissíti a súgófájlokat, szerkesztheti, vagy cserélje le a HelpInfo XML-fájl; nem adhat meg egy másikat. További információkért lásd: [HelpInfo XML-fájl létrehozása](./how-to-create-a-helpinfo-xml-file.md).

### <a name="step-4-sign-your-help-files"></a>4. lépés: A súgófájlok aláírása

Digitális aláírások nem szükségesek, de azok egy ajánlott eljárásokat javaslatot, amikor osztanak meg fájlokat.

### <a name="step-5-create-cab-files"></a>5. lépés: CAB-fájlok létrehozása

Megfelelő eszköz, amely létrehozza a kabinetfájlban (.cab) fájlok, például MakeCab.exe hozhat létre egy. CAB-fájl, amely a modul súgó fájljait tartalmazza. Hozzon létre egy külön CAB fájljának a súgófájlok minden támogatott felhasználói felület kultúrafüggő részletei. További információkért lásd: [előkészítése frissíthető súgó CAB-fájlok hogyan](./how-to-prepare-updatable-help-cab-files.md).

### <a name="step-6-upload-your-files"></a>6. lépés: A fájlok feltöltése

Új vagy frissített Súgó-fájlok közzétételét, az Internet által megadott helyen a CAB-fájlok feltöltése a **HelpContentUri** elem a HelpInfo XML-fájlban. Ezután töltse fel a HelpInfo XML-fájlt a értéke által meghatározott internetes helyre a **HelpInfoUri** kulcsfontosságú a moduljegyzékben.
