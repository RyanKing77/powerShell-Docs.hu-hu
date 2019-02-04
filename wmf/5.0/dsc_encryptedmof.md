---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 9af931a1a2b545ba36826246c4155f42052a16bf
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55688433"
---
# <a name="mof-documents-are-encrypted-by-default"></a>Alapértelmezés szerint titkosított MOF-dokumentumok

Konfigurációs dokumentumok bizalmas információkat tartalmaznak. Korábbi verzióiban a DSC és a egy konfigurációs hitelesítő adatai védelmére tanúsítványok kezelése is szükséges. Több egy jelentős felügyeleti terheket volt és még az összes, a munka ideig tartott ehhez még maradtak bizonyos konfigurációs adatait, amely nem volt, és nem védett.

Amely már nem így mert **összes konfigurációs MOF-fájlok biztonságáról az alapértelmezett**. Nincsenek tanúsítványok vagy metaadat-konfigurációs beállítások szükségesek. Amikor a konfigurációs MOF mentett szerint a helyi Configuration Manager (LCM) Konfigurálása a cél csomópont lemezre, titkosított. A MOF-fájlok segítségével titkosítja [DPAPI](https://msdn.microsoft.com/library/ms995355.aspx). **Megjegyzés:** Egy konfigurációs parancsfájl által előállított MOF-fájlok nincsenek titkosítva.

**Példa:** Leküldési módban titkosítási ![MOF-titkosítás](../images/MOF_Encryption.jpg)

Ha már használja a tanúsítvány metódus jelszavak titkosításához, vagy ha további biztonsági a jelszavak, a [meglévő módszert a tanúsítványalapú titkosítás](https://msdn.microsoft.com/powershell/dsc/securemof) továbbra is működni fog. Az eredmény lesz lehetnek a DPAPIs használatával teljes mértékben titkosított MOF dokumentumot, és emellett jelszavak titkosítva tárolja azt.

A titkosítás csak a konfigurációs MOF dokumentumok (pending.mof, current.mof, previous.mof és részleges MOF-fájlok) vonatkozik. Meta-konfigurációs MOF-fájlok továbbra is mentése egyszerű szövegként, mivel valószínűleg kevesebb titkokat tartalmazzák.
