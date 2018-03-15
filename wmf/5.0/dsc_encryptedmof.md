---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "WMF, powershell, beállítás"
ms.openlocfilehash: 60abe525ca1bdcebca570f2ef3656f32dca3747f
ms.sourcegitcommit: 99227f62dcf827354770eb2c3e95c5cf6a3118b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/15/2018
---
# <a name="mof-documents-are-encrypted-by-default"></a>Alapértelmezés szerint titkosított MOF dokumentumok

Konfigurációs dokumentumok bizalmas információkat tartalmaznak. Korábbi verzióiban DSC kellett terjeszthetők és kezelhetők a tanúsítványok ahhoz, hogy a biztonságos hitelesítő adatok olyan konfigurációs belül. Több ez volt a jelentős felügyeleti terheket, és akár az összes munkafolyamat által ehhez még maradtak bizonyos konfigurációs adatokat, amelyeket nem volt, és nem védett. 

Ez már nem a helyzet mert **összes konfigurációs MOF-ot által biztosított alapértelmezett**. Nincs tanúsítványokat vagy metaadat-konfigurációs beállítások szükségesek. Amikor mentett MOF konfiguráció szerint a helyi Configuration Manager (LCM) a cél csomópont lemezre, titkosítva van. A MOF-ot titkosítása használatával [DPAPI](https://msdn.microsoft.com/library/ms995355.aspx). **Megjegyzés:** MOF-ot egy konfigurációs parancsfájl által generált nincs titkosítva.

**Példa:** titkosítást leküldéses módban ![MOF-titkosítás](../images/MOF_Encryption.jpg)

Ha a tanúsítvány metódus már használja a jelszavak titkosítása, vagy ha további biztonsági kell a jelszót a [meglévő módszert a tanúsítványalapú titkosítás](https://msdn.microsoft.com/powershell/dsc/securemof) továbbra is működni fog. Az eredményt a rendszer teljes mértékben titkosítja a DPAPIs MOF dokumentumot, majd továbbá jelszavai belül titkosított.

A titkosítás csak érvényes konfigurációs MOF dokumentumok (pending.mof, current.mof, previous.mof és részleges MOF-ot). Meta-konfigurációs MOF-ot továbbra is mentése egyszerű szövegként óta titkok kevésbé valószínű tartalmaznak.

