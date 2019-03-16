---
title: Frissíthető Súgó – áttekintés |} A Microsoft Docs
ms.custom: ''
ms.date: 03/22/2012
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Windows PowerShell 3.0
ms.assetid: 3f7388a9-9fa8-42bc-b294-538c9a01e30a
caps.latest.revision: 12
ms.openlocfilehash: f2dfb9642ba2dde38124142b659b425bbbb00f37
ms.sourcegitcommit: caac7d098a448232304c9d6728e7340ec7517a71
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/16/2019
ms.locfileid: "58057603"
---
# <a name="updatable-help-overview"></a>Frissíthető súgó – áttekintés

Ez a dokumentum a tervezési és a Windows PowerShell frissíthető súgójának funkció működésének alapszintű bevezetést nyújt. Modul szerzők és mások számára a Windows PowerShell-Súgó-témaköröket biztosíthat a felhasználók számára tervezték.

## <a name="introduction"></a>Bevezetés

Windows PowerShell-Súgó-témaköröket a Windows PowerShell-tapasztalata szerves részét képezik. Windows PowerShell-modulok, például súgótémakörök folyamatosan frissített és továbbfejlesztett a szerzők és a hozzájárulások a Windows PowerShell-felhasználók a Közösség által.

A *frissíthető súgó* , a Windows PowerShell 3.0-ban bevezetett szolgáltatás biztosítja, hogy felhasználók a legújabb Súgó-témaköröket parancsot a parancssorba, még a beépített Windows PowerShell-parancsok új modulok letöltése nélkül, vagy Windows Update futtatása. Frissíthető súgó leegyszerűsíti frissítése azáltal, hogy a legújabb Súgó-témaköröket letöltése az internetről, és telepítse őket a megfelelő alkönyvtáraiban találhatóak a felhasználó helyi számítógép-parancsmagokkal. Tűzfal mögött található még akkor is, akik az új parancsmagok segítségével frissített segítséget kérhet egy belső fájlmegosztásra.

Frissíthető súgó teljes mértékben támogatja a Windows® 8 és Windows Server® 2012 minden Windows PowerShell-modulok, és a funkciók érhetők el a Windows PowerShell-modul összes Szerző. Frissíthető súgó csak az XML-alapú súgó-fájlokat támogatja. Megjegyzés-alapú súgó nem támogatja.

Frissíthető súgó a következő szolgáltatásokat tartalmazza.

- A [Update-Help](/powershell/module/Microsoft.PowerShell.Core/Update-Help) parancsmagot, amely meghatározza, hogy felhasználók rendelkeznek-e a legújabb súgó modul-fájlokat, és ha nem, letölti a legújabb súgófájlokat az internetről, kicsomagolja őket, és telepíti őket a megfelelő modul alkönyvtáraiban találhatóak a felhasználó számítógépén.
  A felhasználók használhatják a [Get-Help](/powershell/module/Microsoft.PowerShell.Core/Get-Help) parancsmag azonnal az újonnan telepített segítő súgótémakörök megjelenítéséhez.
  Ezek nem kell újraindítani a PowerShell.

- A [Save-Help](/powershell/module/Microsoft.PowerShell.Core/Save-Help) parancsmagot, amely letölti a legújabb Súgó fájlokat az internetről, és menti azokat egy fájl rendszer könyvtárban. A felhasználók használhatják a `Update-Help` parancsmag súgófájlok kérhet a rendszer könyvtárát, és csomagolja ki, és telepítheti a modul alkönyvtáraiban találhatóak a felhasználó számítógépén. A `Save-Help` parancsmag célja a felhasználók, akik csak korlátozottan vagy nincs Internet-hozzáférés és a vállalatok számára, akik szívesebben Internet-hozzáférés korlátozása.

- **Egy modul segítségével**. Egy modul súgófájlok felügyelt és egy egységként kézbesíti, így felhasználók mindegyikét a súgófájlokat, a modulok használják a. Frissíthető súgó csak modulok, a Windows PowerShell beépülő modulok nem támogatott.

- **Támogatott verziók**. Frissíthető súgó használ standard négy-pozíciója (N1. N2. N3. N4) verziószáma. Frissíthető súgó súgófájlok letölti a súgót verziószáma fájlok a felhasználó (vagy a a `Save-Help` könyvtár) kisebb, mint a súgófájlokat, az internetes helyen verziószáma.

- **Több nyelv támogatása**. Frissíthető súgó modul súgófájlok támogatja a több felhasználói felületi kulturális környezetek. Frissíthető Súgó fájl nevek a következők standard nyelvkódokról, például az "en-US" és "ja-JP", és a `Update-Help` és `Save-Help` parancsmagok a súgófájlok helyezze a nyelvspecifikus alkönyvtárát modul.

- **Automatikusan létrehozott súgó**. A [Get-Help](/powershell/module/Microsoft.PowerShell.Core/Get-Help) parancsmag megjeleníti, hogy a parancsok, amelyek nem rendelkeznek a súgófájlok alapszintű segítséget. Az automatikusan létrehozott súgó a parancs szintaxisát és aliasok és az online Súgó és frissíthető súgó vonatkozó utasításokat tartalmazza.

- **Online súgó fokozott**. Online súgó is egyszerű hozzáférést a súgófájlok már nem igényel. A **Online** paraméterében a `Get-Help` parancsmag most olvas be az URL-címét az online súgó-témakör értékét a **HelpUri** minden parancs, ha nem talál egy súgófájlban az online súgó URL-cím tulajdonságát. Fel lehet tölteni a **HelpUri** hozzáadásával tulajdonság egy **HelpUri** parancsmagok, a functions és a CIM-parancsok, vagy használja a kód attribútum a **. Hivatkozás** Megjegyzés-alapú súgó irányelv a munkafolyamatok és parancsfájlok.

  Ahhoz, hogy a súgófájlok frissíthető, a Windows PowerShell-modul a Windows 8 és Windows Server vNext súgófájlok nem tartoznak. Felhasználók segítségével frissíthető súgó súgófájlok telepítheti és frissítheti őket. Más modulok készítői súgófájlok belefoglalhat modulokban vagy hagyja őket. Frissíthető súgó támogatása nem, nem kötelező, de ajánlott.
