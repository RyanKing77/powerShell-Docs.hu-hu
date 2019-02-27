---
title: Hogyan frissíthető a súgófájlok |} A Microsoft Docs
ms.custom: ''
ms.date: 09/12/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 495869a6-080e-4401-9ddc-16edd2f86857
caps.latest.revision: 6
ms.openlocfilehash: 2c1fbd70aab1f65f33ea206b7ab1e2bd3dfd8c7a
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56846479"
---
# <a name="how-to-update-help-files"></a>Súgófájlok frissítése

Ez a témakör bemutatja, hogyan súgófájlokat a modul, amely támogatja a frissíthető súgójának frissítéséhez.

## <a name="updating-help-files"></a>Súgó fájlok frissítése

Súgófájlokat, például a hibák javítása, egy fogalom megértéséhez tisztázhassuk, gyakran feltett kérdés megválaszolásával, új fájlok hozzáadásával vagy hozzáadása az új és hatékonyabb példák számos oka lehet.

A súgófájl frissítése:

1. Módosíthatja a fájlokat.

2. A fájlok lefordítása más felhasználói felületi kulturális környezetek.

3. Az összes Súgó-fájlok gyűjtése (új, módosított és változatlan) modul az egyes felhasználói felület kultúrafüggő részletei.

4. A fájlok ellen az XML-séma érvényesítése.

5. Építse újra a CAB-fájlok az egyes felhasználói felület kultúrafüggő részletei.

6. A HelpInfo XML-fájlban a verziószámok, a CAB-fájl számára minden egyes felhasználói felület kultúrafüggő részletei növelni.

7. Az új CAB-fájlok feltöltése a értéke által meghatározott helyre a **HelpContentUri** elem a HelpInfo XML-fájlban. Cserélje le a régebbi CAB-fájlok az új CAB-fájlok.

8. Töltse fel a frissített HelpInfo XML-fájlt a hely által meghatározott a **HelpInfoUri** kulcsfontosságú a moduljegyzékben. Cserélje le a régebbi HelpInfo XML-fájlt az új fájlt.