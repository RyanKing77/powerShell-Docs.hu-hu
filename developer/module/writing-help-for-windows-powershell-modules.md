---
title: Windows PowerShell-modulok súgó írása |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f2b58fa5-01bc-426c-a043-5c700d6578e9
caps.latest.revision: 16
ms.openlocfilehash: 443bf5f693d2ab161668de25a1097347826cb5c2
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56845457"
---
# <a name="writing-help-for-windows-powershell-modules"></a>Windows PowerShell-modulok írása – súgó

Windows PowerShell-modulok Súgó-témaköröket a modult, valamint arról a modul tagjainak, például a parancsmagok, a szolgáltatók, a függvények és parancsfájlok tartalmazhatnak. A `Get-Help` parancsmag megjeleníti a modul súgótémakörök ugyanebben a formátumban, más Windows PowerShell-cikkek segítséget jeleníti meg, és a felhasználók használhatják a standard `Get-Help` parancsok beolvasni a Súgó-témaköröket.

Ez a dokumentum ismerteti a formátum és a megfelelő elhelyezési modul súgótémakörök, és azt sugallja, hogy a modul súgó tartalma irányelvek.

## <a name="types-of-module-help"></a>A modul Súgó

Egy modul súgó a következő típusú tartalmazhatnak.

- **A parancsmag súgójában**. A Súgó-témaköröket, amelyek ismertetik a modul parancsmagjai is XML-fájlok, amelyek a parancs segítségével séma

- **Szolgáltató súgó**. A Súgó-témaköröket, amelyek ismertetik egy modulban levő szolgáltatók olyan XML-fájlok, amelyek a szolgáltató segítségével séma.

- **Súgó függvény**. A Súgó-témaköröket, amelyek ismertetik a funkciók egy modulban levő lehet XML-fájlok, amelyek a parancs segítségével a séma vagy a Megjegyzés-alapú súgó-témaköröket a függvény vagy a parancsfájl vagy a modul skriptu

- **Parancsfájl-súgó**. A Súgó-témaköröket parancsfájlokat egy modulban levő leíró XML-fájlok, amelyek a parancs segítségével a séma vagy a Megjegyzés-alapú súgó-témaköröket a parancsfájl vagy a modul skriptu is lehet.

- **Fogalmi ("tudnivalók") Súgó**. Használhatja a fogalmi ("tudnivalók") Súgó-témakör írja le a modult és annak tagjait, és hogyan tagok együttes feladatait ismertetik. Fogalmi témakörök olyan szöveges fájlok, amelyek Unicode (UTF-8) kódolást. A fájl nevét kell használnia a `about_<name>.help.txt` formátumban, például a about_MyModule.help.txt. Alapértelmezés szerint a Windows PowerShell tartalmaz az alábbi információk segítségével fogalmi témakörök több mint 100, és az alábbi példához hasonlóan formázási.

  ```
  TOPIC
      about_<subject or module name>

  SHORT DESCRIPTION
      A short, one-line description of the topic contents.

  LONG DESCRIPTION
      A detailed, full description of the subject or purpose of the module.

  EXAMPLES
      Examples of how to use the module or how the subject feature works in practice.

  KEYWORDS
      Terms or titles on which you might expect your users to search for the information in this topic.

  SEE ALSO
      Text-only references for further reading. Hyperlinks cannot work in the Windows PowerShell console.

  ```

## <a name="placement-of-module-help"></a>Elhelyezési modul Súgó

A `Get-Help` parancsmag nyelvspecifikus alkönyvtárát modul modul Súgó-témakör fájlokat keres.

Például a következő könyvtár struktúra ábrán a súgótémakörök SampleModule modul helyét.

```
<ModulePath>
         \SampleModule
               \<en-US>
                     \about_SampleModule.help.txt
                     \SampleModule.dll-help.xml
                     \SampleNestedModule.dll-help.xml
               \<fr-FR>
                     \about_SampleModule.help.txt
                     \SampleModule.dll-help.xml
                     \SampleNestedModule.dll-help.xml

```

> [!NOTE]
> A példában a  *\<ModulePath >* helyőrző egyik szereplő elérési utakat a `PSModulePath` környezeti változót, például $home\Documents\Modules, $pshome\Modules vagy a felhasználó adja meg egyéni elérési utat.

## <a name="getting-module-help"></a>A modul Súgó

Amikor egy felhasználó egy munkamenetbe importálja a modult, a Súgó-témaköröket, hogy a modul importálásának a modullal együtt a munkamenetbe. Listázza a moduljegyzékben a fájllista kulcs értékét a Súgó-témakör fájlokat is, de nem érinti a Súgó-témaköröket a `Export-ModuleMember` parancsmagot.

Különböző nyelveken modul Súgó-témaköröket biztosíthat. A `Get-Help` parancsmag automatikusan megjeleníti a modul Súgó-témaköröket a nyelv, amely az aktuális felhasználó Vezérlőpult a területi és nyelvi beállítások elemben meg van adva. A Windows Vista és újabb verziók, Windows `Get-Help` nyelvspecifikus alkönyvtárát modul a Windows számára hoztak létre nyelvi tartalék szabványoknak megfelelően a súgótémakörök keres.

Windows PowerShell 3.0-s verziójával futó kezdve egy `Get-Help` parancs egy parancsmag vagy a függvény aktiválása automatikus importálja a modult. A `Get-Help` parancsmag azonnal megjeleníti a Súgó-témaköröket tartalmát a modulban.

Ha a modul nem tartalmaz Súgó-témaköröket, és nem a felhasználó számítógépén, a modulban lévő parancsokhoz tartozó Súgó-témaköröket vannak `Get-Help` automatikusan létrehozott Súgó megjelenítése. Az automatikusan létrehozott súgó a parancs szintaxisát, paramétereit és bemeneti és kimeneti típusokat tartalmazza, de nem tartalmaz semmilyen leírása. Az automatikusan létrehozott súgó tartalmaz szöveg, amely átirányítja a felhasználót, hogy próbálja meg használni a `Update-Help` parancsmaggal letöltheti a parancs az internetről vagy egy fájlmegosztás. Azt is használatát javasolja a **Online** paraméterében a `Get-Help` -parancsmaggal beolvasható a Súgó-témakör online verzióját.

## <a name="supporting-updatable-help"></a>Frissíthető súgó támogatása

A Windows PowerShell 3.0-felhasználók és a Windows PowerShell későbbi verziói is fájljainak letöltése és telepítése a frissített súgó egy modul az internetről vagy a helyi fájlmegosztásként. A `Update-Help` és `Save-Help` parancsmagok elrejtése a felhasználói felügyeleti adatait. Felhasználók futtassa a `Update-Help` parancsmagot, majd a `Get-Help` parancsmag használatával, olvassa el a legújabb súgófájlokat a modul a Windows PowerShell parancssorába. Felhasználóknak nem kell indítania Windows vagy a Windows PowerShell használatával.

Felhasználók tűzfalak és az Internet-hozzáférés nélküli mögött a frissíthető érdekében is. A rendszergazdák az Internet eléréséhez használja a `Save-Help` parancsmag használatával töltse le és telepítse a legújabb súgófájlokat azt a fájlmegosztást. Ezt követően a felhasználók használhatják a **elérési** paraméterében a `Update-Help` -parancsmaggal beolvasható a legújabb súgófájlokat a fájlmegosztásból.

A modul szerzők megadhatja súgófájlokat a modul és frissíthető súgójának használata a súgófájlokat, vagy hagyja ki a modulból súgófájlok és használja a frissíthető súgó telepítéséhez, és frissítse azokat.

Frissíthető súgó kapcsolatos további információkért lásd: [frissíthető súgó támogatása](./supporting-updatable-help.md).

## <a name="supporting-online-help"></a>Online súgó támogatása

Felhasználók, akik nem, vagy ne telepítse a frissített Súgó fájlokat a számítógépükön gyakran támaszkodnak az online változata annak modul Súgó-témaköröket. A **Online** paraméterében a `Get-Help` parancsmag egy parancsmag vagy a felhasználó speciális funkcióhoz Súgó-témakör online verzióját az alapértelmezett böngészőben nyílik meg.

A `Get-Help` parancsmag értékét használja a **HelpUri** tulajdonsága, a parancsmag vagy a függvényt, hogy a Súgó-témakör online verzióját.

A Windows PowerShell 3.0-es verziótól kezdve segíthet a HelpUri attribútumot a parancsmag osztályról definiálásával parancsmag és funkció Súgó-témaköröket online verziója található felhasználók vagy a **HelpUri** tulajdonságát a **CmdletBinding** attribútum. Az attribútum értéke értékét a **HelpUri** tulajdonság a parancsmag vagy függvény.

További információkért lásd: [Online súgó támogatása](./supporting-online-help.md).

## <a name="see-also"></a>Lásd még:

[Windows PowerShell-modul írása](./writing-a-windows-powershell-module.md)

[Frissíthető súgó támogatása](./supporting-updatable-help.md)

[Online súgó támogatása](./supporting-online-help.md)