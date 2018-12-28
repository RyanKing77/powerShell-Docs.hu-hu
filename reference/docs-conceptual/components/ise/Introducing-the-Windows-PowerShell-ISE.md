---
ms.date: 08/14/2018
keywords: PowerShell, a parancsmag
title: A Windows PowerShell ISE bemutatása
ms.openlocfilehash: 09a28b295855fd2a3c62bba8a681399dae3454f8
ms.sourcegitcommit: 3402a478cf118c11a5642038eb117bc76553e3ab
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/14/2018
ms.locfileid: "53411582"
---
# <a name="the-windows-powershell-ise"></a>A Windows PowerShell ISE-ben

A Windows PowerShell integrált parancsfájl-kezelési környezet (ISE) egy Windows PowerShell-alkalmazásokhoz. Az ISE-ben futtassa a parancsokat és írási, tesztelési, és szkriptek hibakeresése a egy olyan Windows-alapú grafikus felhasználói felületet. Az ISE jobbról balra író nyelvek többsoros szerkesztését, a tabulátoros kiegészítést, a szintaxis színezést, a szelektív végrehajtási, a környezetfüggő súgó és a támogatást biztosít. A menüelemek és billentyűparancsok több feladatot, amely a Windows PowerShell-konzolon teheti vannak leképezve. Például hibakeresése a parancsfájl az ISE-ben, akkor a jobb gombbal egy sor kódot a Szerkesztés panelre, hogy állítson be egy töréspontot a.

## <a name="support"></a>Támogatás

Az ISE-ben bevezetett Windows PowerShell V2 és újratervezett PowerShell V3. Az ISE-ben támogatott Windows Powershellt, és többek között a Windows PowerShell V5.1 összes támogatott verzióján. Az ISE-ben azonban maintennce módban van, és nincs tervben új szolgáltatások valószínűleg hozzá kell adni.
Emellett nincs rendszer nem támogatja az ISE-ben a PowerShell 6-os verziója és más alkalmazásokhoz. Gondolja át, egy grafikus eszköz, amellyel kezelheti a PowerShell scrips, és így tovább, aki a felhasználók [Visual Studio Code](https://code.visualstudio.com/).

## <a name="key-features"></a>A legfontosabb jellemzők

Főbb funkciók a Windows PowerShell ISE-ben a következők:

- Többsoros szerkesztése: Alatt az aktuális sor egy üres sort beszúrni a parancs ablaktáblán, nyomja le a SHIFT + ENTER billentyűkombinációt.
- Szelektív végrehajtása: Parancsfájl futtatásához jelölje ki a szöveget, szeretné futtatni, és kattintson a **parancsfájl futtatása** gombra. Másik lehetőségként nyomja le az F5 billentyűt.
- Környezetfüggő súgó: Típus **Invoke-cikk**, és nyomja le az F1 billentyűt. A súgófájl megnyitja a cikk a **Invoke-cikk** parancsmagot.

A Windows PowerShell ISE teszi lehetővé testre szabhatja annak megjelenését egyes funkcióit. A saját Windows PowerShell-profil parancsfájlt is rendelkezik.

## <a name="to-start-the-windows-powershell-ise"></a>A Windows PowerShell ISE-ben lehetőségre

Kattintson a **Start**válassza **Windows PowerShell**, és kattintson a **Windows PowerShell ISE-ben**.
Másik lehetőségként beírhatja `powershell_ise.exe` minden olyan parancs-rendszerhéjban, vagy a Futtatás mezőbe.

## <a name="to-get-help-in-the-windows-powershell-ise"></a>Segítség a Windows PowerShell ISE-ben

Az a **súgó** menüben kattintson a **Windows PowerShell súgójára**. Másik lehetőségként nyomja le az F1 billentyűt. A megnyíló fájl ismerteti a Windows PowerShell ISE-ben és a Windows PowerShell-lel, beleértve az összes elérhető a Get-Help parancsmag segítségével.
