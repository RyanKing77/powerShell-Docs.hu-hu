---
title: Általános munkafolyamat-paraméterek |} A Microsoft Docs
ms.custom: ''
ms.date: 09/12/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: d5891467-8e13-484d-b7af-32e6bffab35d
caps.latest.revision: 4
ms.openlocfilehash: b2e8f272a82ee03de306fd8eac45e109142f6284
ms.sourcegitcommit: caac7d098a448232304c9d6728e7340ec7517a71
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/16/2019
ms.locfileid: "58054798"
---
# <a name="common-workflow-parameters"></a>Gyakori munkafolyamat-paraméterek

Egy Windows PowerShell-parancsmag által létrehozott munkafolyamat-tevékenység, amely közös paraméterek számát, az összes tevékenység határozza meg. Ezeket a paramétereket egy részét adható meg, hogy a munkafolyamat-szerzők szabhatja testre a tevékenységek. Egy másik részével ezeket a paramétereket a felhasználó által adható meg a tevékenység meghívásakor.

Az általános munkafolyamat-paraméterek kategóriákba vannak rendezve, számos módon.

## <a name="connectivity-parameters"></a>Kapcsolódási paraméterek

|Név|Típus|Leírás|Végfelhasználók által a végrehajtás során adható meg?|A munkafolyamat szerzői a létrehozáskor megadott?|A példányosítás munkafolyamat Szerző szerint adható meg?|
|----------|----------|-----------------|-----------------------------------------------------|------------------------------------------------------------|-----------------------------------------------------------|
|PSComputerName|String]|Számítógép nevének, amelyek esetében szeretne indítsa el a feladatok listáját.|Igen|Igen|Igen|
|PSCredential|[System.Management.Automation.PSCredential](/dotnet/api/System.Management.Automation.PSCredential)|A hitelesítő adatok használata a bejelentkezéshez a PSComputerName paraméter által megadott számítógépekre. Ez a paraméter csak akkor, ha a megadott PSComputerName érvényességét.|Igen|Igen|Igen|
|PSPort|UInt32|A munkafolyamat futtatásához használt port.|Igen|Igen|Igen|
|PSUseSSL|Boolean|A távoli számítógép a munkafolyamat futtatási biztonságos kapcsolatot létesíteni a Secure Sockets Layer (SSL) protokoll használatával.|Igen|Igen|Igen|
|PSConfigurationName|Sztring|A munkamenet-konfiguráció a munkafolyamat futtatásához használt.|Igen|Igen|Igen|
|PSApplicationName|Sztring|Az alkalmazás neve része, a munkafolyamat-végrehajtási létesített kapcsolat URI. Használja ezt a paramétert csak akkor, amikor nem használja a ConnectionURI paramétert.|Igen|Igen|Igen|
|PSThrottleLimit|UInt32|A munkafolyamat futtatási létrehozható egyidejű kapcsolatok maximális száma.|Igen|TBD|Igen|
|PSConnectionURI|String]|Teljes URI-azonosítókat adja meg a végpontokat az interaktív munkamenet során a munkafolyamat futtatásához használt tömbje.|Igen|Igen|Igen|
|PSAllowRedirection|Boolean|Megadja, hogy a munkafolyamat futtatásához egy másik URI-t, a kapcsolat átirányításához.|Igen|Igen|Igen|
|PSSessionOption|[System.Management.Automation.Remoting.Pssessionoption](/dotnet/api/System.Management.Automation.Remoting.PSSessionOption)|A munkafolyamat futtatásához használt munkamenet speciális beállítások.|Igen|Igen|Igen|
|PSAuthentication|[System.Management.Automation.Runspaces.Authenticationmechanism](/dotnet/api/System.Management.Automation.Runspaces.AuthenticationMechanism)|Érték a [System.Management.Automation.Runspaces.Authenticationmechanism](/dotnet/api/System.Management.Automation.Runspaces.AuthenticationMechanism) enumerálása, amely megadja a hitelesítési mechanizmus a hitelesítéshez a felhasználó hitelesítő adatait.|Igen|Igen|Igen|
|PSCertificateThumbprint|Sztring|A digitális nyilvános kulcsú tanúsítvány (X509) egy felhasználói fiók, amely a munkafolyamat futtatási engedéllyel rendelkezik.|Igen|Igen|Igen|

### <a name="behavior-parameters"></a>Viselkedés paraméterek