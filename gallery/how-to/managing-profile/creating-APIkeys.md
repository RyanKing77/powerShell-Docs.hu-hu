---
ms.date: 09/10/2018
contributor: JKeithB
keywords: katalógus, a powershell, a parancsmag, a psgallery
title: API-kulcsok kezelése
ms.openlocfilehash: 954eb27c25babdb8efe50c13caf5f2d287c6b3e3
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55687719"
---
# <a name="managing-api-keys"></a>API-kulcsok kezelése

A PowerShell-galériából támogatja a közzététel követelményeinek számos támogatásához több API-kulcsok létrehozása. API-kulcs egy vagy több csomagot is alkalmazhat, bizonyos jogokat biztosít, és lejárati dátummal rendelkezik.

> [!IMPORTANT]
> Felhasználók számára hatókörrel rendelkező API-kulcsok bevezetése előtt a PowerShell-galériában közzétett egy "teljes hozzáférés API-kulcs" lesz. A teljes hozzáférési kulcsok nem rendelkezik a hatókörrel rendelkező API-kulcsok beépített biztonsági fejlesztések. Soha nem a teljes hozzáférési kulcsok lejár, és a alkalmazni a minden felhasználó a tulajdonosuk. Ha törli ezt a kulcsot, akkor nem kell újra létrehoznia.

Az alábbi képen látható a rendelkezésre álló lehetőségeket, egy hatókörrel rendelkező API-kulcs létrehozása során.

![API-kulcsok létrehozása](../../Images/PSGallery_KeyScoped.png)

Ebben a példában létrehoztunk egy API-kulcs nevű **AzureRMDataFactory**. Ezt a kulcsértéket olyan nevekkel, amelyek "AzureRM.DataFactory" előtaggal kell kezdődnie, és 365 napig érvényes a csomagok leküldéses használható. Ez akkor jellemzően olyan helyzetben, amikor a az ugyanazon szervezeten belüli különböző csapatok dolgoznak a különböző csomagok. A csapat tagjai egy kulcsot, amely engedélyezi őket az adott csomag működnek a jogosultságokkal rendelkezik.
A lejárati értéke megakadályozza, hogy az elavult vagy elfelejtett kulcsok használatát.

## <a name="using-glob-patterns"></a>Helyettesítése mintázatok használatával

Ha a több csomagokat dolgozik, helyettesítés mintákat használhat a több csomag megfelelő csoportként. API-engedélyek vonatkoznak a helyettesítése mintának megfelelő minden új csomagokat. Például az előző példában egy **helyettesítése minta** "AzureRM.DataFactory*" értékét. Ezt a kulcsot használva, mert a csomag megfelel a helyettesítése mintának AzureRm.DataFactoryV2.Netcore nevű csomag küldhet.

## <a name="create-api-keys-securely"></a>Biztonságos API-kulcsok létrehozása

A biztonság érdekében egy újonnan létrehozott kulcs értékét a képernyő nem jelenik meg, és csak akkor érhető el a Másolás gombra kattintva, ahogy az alábbi.

![Új API-kulcs értéke beszerzése](../../Images/PSGallery_CopyCreatedKey.png)

> [!IMPORTANT]
> Után azonnal létrehozása vagy frissítése, azt csak az API-kulcs értéke lehet másolni. Nem jelenik meg, és nem lesz elérhető újra után az oldal frissítésekor. Ha elveszíti a kulcs értékét, Regenerate használja, és az után azt újra létrehozzák azok másolására.

## <a name="key-permissions-and-expiration"></a>Beállításkulcs-engedélyeit és a lejárata

Hatókörrel rendelkező API-kulcsok rendelhet hozzá a következő engedélyek:

- Küldje le az új csomagok
- Új leküldéses vagy -csomagok frissítése
- Csomagok unlist

Minden új kulcsot egy lejárati rendelkezik. A lejárati értéke napokban mérjük. A lejárati lehetséges értékei a következők:

- 1 nap
- 90 nap
- 180 nap
- 270 naponta
- 365 nap (alapértelmezett)

Ezek a beállítások nem lehet módosítani, a kulcs létrehozása után. Nem hozhat létre egy új kulcsot, soha nem jár le.

## <a name="editing-and-deleting-existing-api-keys"></a>Szerkesztés és törlés meglévő API-kulcsok

Módosíthatja a meglévő kulcs bizonyos beállítások. Fent említetteknek nem módosítja a meglévő API-kulcsot a biztonsági hatókörhöz vagy módosítsa a lejárati. A módosítható beállítások az alábbi képernyőfelvételen látható:

![Új API-kulcs értéke beszerzése](../../Images/PSGallery_EditAPIKey.png)

A csomagok szabályozza a kulcs módosításához válassza ki az egyes csomagokat a listából, vagy módosítsa a helyettesítése minta.

Kattintson a **újragenerálása** létrehoz egy új kulcs értéket. Ugyanúgy, mint ha kezdetben hozta létre a kulcsot, akkor meg kell **másolási** közvetlenül a frissítés után a kulcs értékét. A **másolási** lehetőség nem érhető el, ha elhagyja az oldalt.

Kattintson a **törlése** egy megerősítő üzenetet jelenít meg. A törölt egy kulcs használhatatlan lesz.

## <a name="key-expiration"></a>Kulcsának lejárati dátuma

A lejárat előtt 10 nappal a PowerShell-galériából figyelmeztető e-mailt küld a fióktulajdonos az API-kulcs. Követően a kulcs nem használható. Az API kulcskezelés oldaláról, mely kulcsok már nem érvényesek tetején figyelmeztető üzenet jelenik meg. Létrehozhat egy új kulcs értékét.
