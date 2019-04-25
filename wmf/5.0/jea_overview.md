---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 0bc085588190f134c4a687c952509aa256b5f840
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62085201"
---
# <a name="just-enough-administration-jea"></a>Just Enough Administration (JEA)
Just Enough Administration új funkciója a WMF 5.0-s, amely lehetővé teszi, hogy a szerepkör alapú felügyelet a PowerShell távoli eljáráshívás segítségével.  Kibővíti a meglévő infrastruktúra korlátozott végpontot azáltal, hogy nem rendszergazdák számára a parancsok, parancsprogramok és végrehajtható fájlok futtassa rendszergazdaként.  Ez lehetővé teszi, hogy a rendszergazdák a környezetében számának csökkentése és a biztonság növelése.  A JEA működik minden felügyelt; Powershellen keresztül Ha valami, a PowerShell-lel is kezelni, JEA segítségére lehet így biztonságosan.  Just Enough Administration részletes tekintse meg, tekintse meg a [útmutató élmény](http://aka.ms/JEA).

Régi korlátozott végpontok, ellentétben a JEA egyszerűen beállítható példányközi hatékony.  JEA felhasználói képessége kínálja szabályozható, mely paraméterkészlettel és értékeket lehet adni egy bizonyos paranccsal korlátozása le. A felhasználói műveletek egy egyszeri virtuális fiók, amely rendelkezik jogosultságokkal a felügyeleti műveleteket végrehajtani a környezetében futnak.  A felhasználó által meghívott parancsokban a biztonsági eseményeket is naplózva.

A JEA azáltal, hogy speciálisan konfigurált korlátozott végpontok létrehozásához használható.  Ezeket a végpontokat néhány fontos jellemzőkkel rendelkeznek:

1. A felhasználó csatlakozik hozzájuk a "Futtatás mint" parancsot egy emelt szintű virtuális fiókot, hogy csak a távoli munkamenet időtartama létezik.  Alapértelmezés szerint ez a virtuális fiók tagja a beépített Rendszergazdák csoport, valamint a tartományvezérlőkön a tartományi rendszergazdák (Megjegyzés: ezeket az engedélyeket is konfigurálható). Egyik felhasználó összekapcsolása, és más, jogosultsággal rendelkező felhasználóként, engedélyezheti a nem kiemelt jogosultságú felhasználók számára, hogy elvégezzenek bizonyos rendszergazdai feladatokat ad nekik a rendszerek rendszergazdai jogosultságok nélkül.
2. A végpont zárolva van.  Ez azt jelenti, hogy nem nyelvmód PowerShell futtatást.  A felhasználó csak a konkrét parancsok, parancsprogramok és végrehajtható fájlok láthatók.
3. Különböző felhasználók csatlakoznak egy másik csoport tagsága alapján funkciójával együtt jelennek meg.  Megadhat különböző szerepkörök különböző képességeket, az azonos végponton.
