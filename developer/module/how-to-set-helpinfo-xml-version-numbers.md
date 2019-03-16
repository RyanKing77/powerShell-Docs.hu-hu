---
title: Hogyan állíthatja be a verziószámok HelpInfo XML |} A Microsoft Docs
ms.custom: ''
ms.date: 09/12/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 93a00463-af58-41c8-b088-450909fa1d05
caps.latest.revision: 6
ms.openlocfilehash: b98e6879bbfe0e3ec1a9ab37496dde44caf523a4
ms.sourcegitcommit: caac7d098a448232304c9d6728e7340ec7517a71
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/16/2019
ms.locfileid: "58054135"
---
# <a name="how-to-set-helpinfo-xml-version-numbers"></a>HelpInfo XML-verziószámok beállítása

Ez a témakör azt ismerteti, hogyan állítsa be, és a egy frissíthető súgó információs fájlban, a "HelpInfo XML-fájl." néven a verziószámok növelése

## <a name="how-to-set-helpinfo-xml-version-numbers"></a>HelpInfo XML-verziószámok beállítása

Egy HelpInfo XML-fájlban a verziószámok létfontosságúak frissíthető súgó működését.
A [Update-Help](/powershell/module/Microsoft.PowerShell.Core/Update-Help) és [Save-Help](/powershell/module/Microsoft.PowerShell.Core/Save-Help) parancsmagok új súgófájlok letöltéséhez, csak akkor, ha egy felhasználói felületi kulturális környezet a távoli HelpInfo XML-fájlban a verziószám nagyobb, mint a verziószáma az adott felhasználói felület kultúrafüggő részletei a helyi HelpInfo XML, vagy nincs helyi HelpInfo XML-fájl.

A HelpInfo XML-fájlt használ a 4 részből verziószámot, amely van definiálva a **System.Version** a Microsoft .NET-keretrendszer osztályát. A formátum `N1.N2.N3.N4`. Modul szerzők bármely verzióját, amely lehetővé teszi számozási használhatják a **System.Version** osztály. Frissíthető súgó csak ehhez meg kell adni a verziószám felhasználói felületi kulturális környezet növeléséhez a CAB-fájl, a felhasználói felület kulturális környezethez tartozó új verziója, a hely által meghatározott feltöltésekor a **HelpContentURI** elem a HelpInfo XML-fájlban.

Az alábbi példa a német (de-DE) felhasználói felület culture, ha a verzió 2.15.0.10 HelpInfo XML-fájl elemeinek megjeleníti.

```xml

<UICulture>
  <UICultureName>de-DE</UICultureName>
  <UICultureVersion>2.15.0.10</UICultureVersion>
</UICulture>
```

A verziószám egy felhasználói felületi kulturális környezet tükrözi az adott felhasználói felület kultúrafüggő részletei a CAB-fájl verzióját. A verziószámot a teljes CAB-fájl vonatkozik. A CAB-fájl nem beállíthat különböző verziószámokat a különböző fájlok. A verziószám az egyes felhasználói felület kultúrafüggő részletei egymástól függetlenül ki lesz értékelve, és nem kell kapcsolódnak a verziószámokat a többi felhasználói felületi kulturális környezetek, a modul által támogatott.