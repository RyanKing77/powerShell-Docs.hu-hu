---
title: Egy HelpInfo XML-fájl létrehozása |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 3971ce1f-271c-4938-a9d3-47ff3aaf7219
caps.latest.revision: 9
ms.openlocfilehash: 7df9764fd573b75f285fec592448a550e481bea3
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62082413"
---
# <a name="how-to-create-a-helpinfo-xml-file"></a>HelpInfo XML-fájl létrehozása

Ez a szakasz témakörei azt ismerteti, hogyan hozhat létre és tölthet fel egy Súgó információs fájl, egy "HelpInfo XML-fájl," a Windows PowerShell frissíthető súgójának szolgáltatás gyakran nevezik.

## <a name="helpinfo-xml-file-overview"></a>HelpInfo XML-fájl áttekintése

A HelpInfo XML-fájlt az kapcsolatos frissíthető súgó információit az sp_refresh_parameter_encryption elsődleges forrása. Ez magában foglalja a modulok, a felhasználói felület a támogatott kulturális környezetek és a verziószámokat, amely frissíthető súgó segítségével határozza meg, hogy a felhasználó rendelkezik-e a legújabb súgófájlokat a Súgó-fájlok helyét.

Minden egyes a modulnak csak egy HelpInfo XML-fájl, akkor is, ha a modul tartalmazza a felhasználói felület több országban több súgófájlok. A modul szerzőjének hoz létre a HelpInfo XML-fájlt, és elhelyezi által meghatározott internetes a helyen a **HelpInfoUri** kulcsfontosságú a moduljegyzékben. A modul súgófájlok frissítve, és a feltöltött, amikor a modul szerzőjének frissíti a HelpInfo XML-fájl, és felülírja az eredeti HelpInfo XML-fájlt az új verzióval.

Rendkívül fontos, hogy alaposan változatlan marad a HelpInfo XML-fájlt. Ha új fájlokat feltölteni, de a verziószámok növekedjenek felejtse el, frissíthető súgó nem letölti az új fájlok felhasználók számítógépein. Ha egy új felhasználói felület kulturális környezethez tartozó Súgó-fájlok hozzáadása, de nem frissítse a HelpInfo XML-fájlt vagy a megfelelő helyre, frissíthető súgó nem letölti az új fájlokat.

## <a name="in-this-section"></a>A szakasz tartalma

Ez a szakasz a következő témakörökből áll.

- [HelpInfo XML-séma](./helpinfo-xml-schema.md)

- [Mintafájl HelpInfo XML](./helpinfo-xml-sample-file.md)

- [Hogyan lehet egy HelpInfo XML-fájl neve](./how-to-name-a-helpinfo-xml-file.md)

- [HelpInfo XML-verziószámok beállítása](./how-to-set-helpinfo-xml-version-numbers.md)

## <a name="see-also"></a>Lásd még:

[Frissíthető súgó támogatása](./supporting-updatable-help.md)