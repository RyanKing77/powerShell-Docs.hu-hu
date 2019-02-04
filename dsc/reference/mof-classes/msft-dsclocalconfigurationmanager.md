---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: MSFT_DSCLocalConfigurationManager osztály
ms.openlocfilehash: 7f6aaf209601e99b0120407eb301d32fcfda9eb8
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55685395"
---
# <a name="msftdsclocalconfigurationmanager-class"></a>MSFT_DSCLocalConfigurationManager osztály

A helyi Configuration Manager (LCM) Konfigurálása, amely az államok konfigurációs fájlja vezérli, és a konfiguráció alkalmazása a konfigurációs ügynök használatával.

A következő szintaxist Managed Object Format (MOF) kódból egyszerűsödött, és tartalmazza az összes örökölt tulajdonságait.

## <a name="syntax"></a>Szintaxis

```
[ClassVersion("1.0.0"), dynamic, provider("dsccore"), AMENDMENT]
class MSFT_DSCLocalConfigurationManager
{
};
```

## <a name="members"></a>Tagok

A **MSFT_DSCLocalConfigurationManager** osztályt a következő tagja van:

- [Módszerek] []

### <a name="methods"></a>Metódusok

A **MSFT_DSCLocalConfigurationManager** osztály rendelkezik, ezek a módszerek.

|Módszer |Leírás |
|:--- |:---|
| [ApplyConfiguration](msft-dsclocalconfigurationmanager-applyconfiguration.md)| A konfigurációs ügynök használja a alkalmazni a konfigurációt, amely függőben van.|
| [DisableDebugConfiguration](msft-dsclocalconfigurationmanager-disabledebugconfiguration.md)| Letiltja a DSC-erőforrás hibakeresés.|
| [EnableDebugConfiguration](msft-dsclocalconfigurationmanager-enabledebugconfiguration.md)| Lehetővé teszi a DSC-erőforrás hibakeresés.|
| [GetConfiguration](msft-dsclocalconfigurationmanager-getconfiguration.md)| A konfigurációs dokumentum küldése a felügyelt csomóponthoz, és használja a **első** metódus a alkalmazni a konfigurációt a konfigurációs ügynök.|
| [GetConfigurationResultOutput](msft-dsclocalconfigurationmanager-getconfigurationresultoutput.md)| Lekéri egy adott feladat vonatkozó konfigurációs ügynök kimenetét.|
| [GetConfigurationStatus](msft-dsclocalconfigurationmanager-getconfigurationstatus.md)| A konfigurációs ügyfélállapot előzményeinek lekérése.|
| [GetMetaConfiguration](msft-dsclocalconfigurationmanager-getmetaconfiguration.md)| Szabályozhatja a konfigurációs ügynök LCM beállítások beolvasása.|
| [PerformRequiredConfigurationChecks](msft-dsclocalconfigurationmanager-performrequiredconfigurationchecks.md)| A konzisztencia-ellenőrzés indítása.|
| [RemoveConfiguration](msft-dsclocalconfigurationmanager-removeconfiguration.md)| Eltávolítja a konfigurációs fájlokat.|
| [ResourceGet](msft-dsclocalconfigurationmanager-resourceget.md)| Közvetlenül meghívja a **első** metódus a DSC-erőforrás.|
| [ResourceSet](msft-dsclocalconfigurationmanager-resourceset.md)| Közvetlenül meghívja a **beállítása** metódus a DSC-erőforrás.|
| [ResourceTest](msft-dsclocalconfigurationmanager-resourcetest.md)| Közvetlenül meghívja a **teszt** metódus a DSC-erőforrás.|
| [Visszaállítás](msft-dsclocalconfigurationmanager-rollback.md)| Vissza az előző konfigurációs tekercsben.|
| [SendConfiguration](msft-dsclocalconfigurationmanager-sendconfiguration.md)| A konfigurációs dokumentum a felügyelt csomópont küld, és menti azt egy függőben lévő módosítást.|
| [SendConfigurationApply](msft-dsclocalconfigurationmanager-sendconfigurationapply.md)| A konfigurációs dokumentum a felügyelt csomópont küld, és a konfigurációs ügynök használja a alkalmazni a konfigurációt.|
| [SendConfigurationApplyAsync](msft-dsclocalconfigurationmanager-sendconfigurationapplyasync.md)| A konfigurációs dokumentum küldése a felügyelt csomóponthoz, és indítsa el a alkalmazni a konfigurációt a konfigurációs ügynök használatával. GetConfigurationResultOutput használatával lekérheti az eredmény kimeneti.|
| [SendMetaConfigurationApply](msft-dsclocalconfigurationmanager-sendmetaconfigurationapply.md)| Az LCM beállítások, amelyek segítségével szabályozhatja a konfigurációs ügynök beállítása.|
| [StopConfiguration](msft-dsclocalconfigurationmanager-stopconfiguration.md)| Leállítja a konfigurációt, hogy folyamatban van.|
| [TestConfiguration](msft-dsclocalconfigurationmanager-testconfiguration.md)| A konfigurációs dokumentum a felügyelt csomópont küld, és ellenőrzi az aktuális konfiguráció ellen a dokumentumot.|

## <a name="requirements"></a>Követelmények

**MOF:** DscCore.mof

**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration