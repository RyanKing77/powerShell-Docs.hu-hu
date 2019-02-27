---
title: CAB-fájlok feltöltése és létrehozása |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 8d35f233-5447-48a2-a961-9fbca763262b
caps.latest.revision: 7
ms.openlocfilehash: 9928a0b31a57d42eb39cea1af0509613c483caf7
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56848663"
---
# <a name="how-to-create-and-upload-cab-files"></a>CAB-fájlok létrehozása és feltöltése

Ez a témakör bemutatja, hogyan frissíthető súgó CAB-fájlok létrehozása, és feltölteni őket a helyet, ahol a-parancsmagok frissíthető súgójának elérheti őket.

## <a name="how-to-create-and-upload-updatable-help-cab-files"></a>Frissíthető súgó CAB-fájlok feltöltése és létrehozása

A frissíthető súgó szolgáltatás segítségével a több nyelv és kulturális környezetek egy modul új vagy frissített súgó-fájljait. Egy modul frissíthető súgó csomagját áll egy HelpInfo XML-fájl és a egy vagy több kabinetfájlból (. CAB-fájl) fájlok. Minden egyes CAB-fájl tartalmazza a modul egy felhasználói felület kultúrafüggő részletei a súgófájlok. Az alábbi eljárással hozhat létre a CAB-fájlok frissíthető súgó.

1. Felhasználói felület kultúrafüggő részletei jellemzők szerint rendezik a súgófájlok modul. Minden egyes frissíthető súgó CAB-fájl egy-egy felhasználói felület kultúrafüggő részletei modulja súgó fájljait tartalmazza. Több segítséget nyújthasson CAB-fájlok a modult, egyenként egy másik felhasználói felület kultúrafüggő részletei.

2. Győződjön meg arról, hogy a súgófájlok csak olyan fájltípusokat szerepeltessen a frissíthető súgó engedélyezett és a egy Súgó fájl séma ellenőrzi őket. Ha a `Update-Help` parancsmag egy fájlt, amely érvénytelen vagy nem engedélyezett típusú észlel, nem telepíti a érvénytelen fájlt, és leállítja a cab-fájl a fájlok telepítése. Megengedett fájltípusok listáját lásd: [egy frissíthető súgó CAB-fájl az engedélyezett típusok fájl](./file-types-permitted-in-an-updatable-help-cab-file.md).

3. A súgófájlok digitális aláírása. Digitális aláírások nem szükségesek, de azok az ajánlott eljárás.

4. Összes Súgó culture, nem csak az új fájlok újdonságai és változásai a modul a felhasználói felület fájljait tartalmazzák. A CAB-fájl nem fejeződött be, ha a felhasználók, akik a súgófájlok letöltéséhez először, vagy ne töltse le minden frissítés nem fog összes modul Súgó fájlt.

5. Használjon, amely létrehozza a kabinetfájlok, például MakeCab.exe segédprogramot. Windows PowerShell parancsmagok azonosítóértékeiként CAB-fájlok nem tartalmazza.

6. Adjon nevet a CAB-fájlok. További információkért lásd: [egy frissíthető súgó CAB-fájl elnevezése](./how-to-name-an-updatable-help-cab-file.md).

7. A modul a CAB-fájlok feltöltése a megadott helyre a **HelpContentUri** elem a modul HelpInfo XML-fájlban. A hely által meghatározott majd feltölti a HelpInfo XML-fájlt a **HelpInfoUri** kulcsa a moduljegyzékben. A **HelpContentUri** és **HelpInfoUri** , ha ugyanazon a helyen.

> [!CAUTION]
> Értékét a **HelpInfoUri** kulcs és a **HelpContentUri** elem "http" vagy "https" kell kezdődnie. Az értéket meg kell jelölnie az interneten található, és a egy fájl neve nem tartalmazhat.