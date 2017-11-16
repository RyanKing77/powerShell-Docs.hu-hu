---
ms.date: 2017-06-12
contributor: JKeithB
ms.topic: conceptual
keywords: "gyűjtemény, a powershell, a parancsmag, a psgallery"
title: "PowerShell-galériában fiók létrehozása"
ms.openlocfilehash: e21575320f220c1ba7ecd9bd464a814b3ebf49d9
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
## <a name="creating-a-powershell-gallery-account"></a>PowerShell-galériában fiók létrehozása

A PowerShell-galériában fiók semmit a PowerShell-galériában való közzététele előtt kell létrehozni. A PowerShell-galériában fiókok össze kell kapcsolni egy Azure Active Directory levelezési fiók vagy egy Microsoft-fiók (tartománnyal rendelkező Outlook.com-os, hotmail.com, stb.)

Hozzon létre egy PowerShell-galériában fiókkal, Ugrás https://PowerShellGallery.com, majd kattintson a "Regisztrálása" (lásd az alábbi képen). 

![Új fiók regisztrálása](./images/CreatingAccount-Register.png)

A következő oldalon egy Azure Active Directory-fiókot használ, jelölje ki "Munkahelyi vagy iskolai fiók", és jelentkezzen be a fiókjával. Használja a Microsoft-fiók – például Hotmail.com vagy Outlook.com-os tartomány - válassza a "Személyes fiók", és jelentkezzen be. 

Ha már bejelentkezett, kérni fogja a PowerShell-galériában felhasználónevét létrehozásához. Tekintse át a használati feltételeket és adatvédelmi szabályzat a csatolt, adjon meg egy felhasználónevet, majd regisztrálja.

Megjegyzés: A fiók neve nem lehet módosítani, a már létrehozott.  
Lásd: [elem tulajdonosainak kezelése](https://msdn.microsoft.com/en-us/powershell/gallery/psgallery/managing-item-owners) az ezzel kapcsolatos további részletekért.

## <a name="recommended-practices-for-powershell-gallery-accounts"></a>Ajánlott eljárások a PowerShell-galériában fiókok

Fontos, hogy a PowerShell-galériában fiókjához használt e-mail fiókot felügyelhető aktívan.
A PowerShell gyűjteményelemek tulajdonosainak összes communiction az e-mailt a PowerShell-galériában fiókjához társított címen keresztül történik.
Ha azt nem lehet csatlakozni a tulajdonosa, a műveleti csapata előfordulhat, hogy kell bizonyos körülmények elem törlése.

A szervezeteknek, amelyek gyakran közzétételére a PowerShell-galériában egyedi fiók létrehozása az Outlook.com-os, vagy egy másik Microsoft-fiók tartománya erre a célra.
Sok esetben fiók nem rendszeresen figyeli a rendszer. Ebben az esetben ajánlott Outlook továbbítás használatára egy másik fiókot, a szervezeten belül, a cikk tulajdonos(ok) által figyelendő általában egy e-mail küldéséhez.

Ha egy elemhez tartozó több tulajdonosai, az összes kommunikáció a PowerShell-galériában érkező kerül minden tulajdonosai számára.
Lásd: [elem tulajdonosainak kezelése](https://msdn.microsoft.com/en-us/powershell/gallery/psgallery/managing-item-owners) további részleteket a tulajdonosok ad hozzá egy elemet. 

