---
title: Parancsmagok modulok importálása |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: a41d9e5f-de6f-47b7-9601-c108609320d0
caps.latest.revision: 8
ms.openlocfilehash: c007bb11324e10ffd100797dccd9e6ab0d09a73e
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62067977"
---
# <a name="how-to-import-cmdlets-using-modules"></a>Parancsmagok importálása modulokkal

Ez a témakör ismerteti a parancsmagok importálása a Windows PowerShell-munkamenethez bináris modul használatával.

> [!NOTE]
> Modulok tagjai lehetnek parancsmagok, szolgáltatók, függvények, változókat, aliasok és még sok más. Beépülő modulok csak parancsmagok és szolgáltatók tartalmazhat.

## <a name="how-to-load-cmdlets-using-a-module"></a>Betöltés parancsmagok egy modul használatával

1. Hozzon létre egy modul, amely ugyanazzal a névvel rendelkezik a szerelvényfájl, amelyben a parancsmagok vannak megvalósítva. Ebben az eljárásban a modul mappában jön létre a a `system32` mappát.

   `%SystemRoot%\system32\WindowsPowerShell\v1.0\Modules\mymodule`

2. Győződjön meg arról, hogy a `PSModulePath` környezeti változó tartalmazza az új modul mappa elérési útját. Alapértelmezés szerint a mappa már része a `PSModulePath` környezeti változót.

3. A modul a parancsmag szerelvény másolja.

4. Futtassa a következő parancsot, adja hozzá a munkamenet a parancsmagokat:

   `import-module [Module_Name]`

   Ez az eljárás használható a parancsmagok teszteléséhez. Minden parancsmag hozzáadja a szerelvényben a munkamenethez. Modulok, a különböző módokon betölteni a modulok és a egy modul exportálja, elemeinek korlátozása a különböző típusú modulokkal kapcsolatos további információkért lásd [Windows PowerShell-modul írása](../module/writing-a-windows-powershell-module.md).

## <a name="see-also"></a>Lásd még:

[Egy Windows PowerShell-parancsmag írása](./writing-a-windows-powershell-cmdlet.md)

[Modulok telepítése](../module/installing-a-powershell-module.md)