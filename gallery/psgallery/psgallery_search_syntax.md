---
ms.date: 2017-06-12
contributor: JKeithB
ms.topic: conceptual
keywords: "gyűjtemény, a powershell, a parancsmag, a psgallery"
title: psgallery_search_syntax
ms.openlocfilehash: 409ae607557af760f9cec4e3c54f39e51b5fac18
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
# <a name="gallery-search-syntax"></a>Gyűjteményelem keresési szintaxisának

PowerShell-galériában kínál a szöveg searchbox, ahol ugyanúgy használhatók szavak, kifejezések és kulcsszó kifejezések keresési eredmények szűkítéséhez.

## <a name="search-by-keywords"></a>Keresési kulcsszavakat

    dsc azure sql

Keresés a lehető legkedvezőbb módon vonatkozó összes 3 kulcsszavak tartalmazó dokumentumok kereséséhez tegye, és térjen vissza a megfelelő dokumentumok.

## <a name="search-using-phrases-and-keywords"></a>A keresés kifejezések és kulcsszavak használatával

    "azure sql" deployment

Írja be a kódját idézőjelek között ("") módosíthatja a keresés keresse meg az adott kifejezést külön kulcsszavak helyett.
Dokumentumok megfelelő általában tartalmaznia kell a pontos kifejezés "azure sql", így például a kis-és nagybetűk változata "Az azure SQL", és általában is a "telepítés" szót tartalmaz.

## <a name="filtering-on-fields"></a>A mezőkre szűrése

Kereshet egy adott cikk azonosítója (vagy "Id" vagy "id"), vagy bizonyos más mezők illesztésével végezzen keresést a mező nevét a kifejezéseket.

A kereshető mezők jelenleg "Id", "Version", "Címke", "Szerző", "Tulajdonos", "Függvények", "Parancsmagok", "DscResources" és "PowerShellVersion".

[Mi az a különbség azonosítója és a cím? Azonosító a konzol használata esetén. -E a keresési eredmények elem lap tetején látható.]

## <a name="examples"></a>Példák

    ID:"PSReadline"
    id:"AzureRM.Profile"

illetve talál "PSReadline" vagy "AzureRM.Profile" elemet az Azonosítót tartalmazó mezőt.

    Id:"AzureRM.Profile"

egy másik módja az azonosító mezőben "AzureRM.Profile" elemek kereséséhez.

Az "Id" szűrő karakterláncrész egyeznek, így ha a a következő:

    Id:"azure"
    
Például a "AzureRM.Profile" és "Azure.Storage" eredmények lesz.

Egy mező több kulcsszavak is kereshet. Vagy kombinációs mezőket.

    id:azure tags:intellisense
    id:azure id:storage

És kifejezés kereshet:

    id:"azure.storage"


A DSC-címkével ellátott összes elemek kereséséhez.

    Tags:"DSC"

A megadott függvény összes elemek kereséséhez.

    Functions:"Update-AzureRM"

A megadott parancsmaggal minden elem kereséséhez.
    
    Cmdlets:"Get-AzureRmEnvironment"

A megadott nevű DSC erőforrás minden elem kereséséhez.

    DscResources:"xArchive"

A megadott PowerShellVersion tartalmazó összes elemek kereséséhez

    PowerShellVersion:"5.0"
    PowerShellVersion:"3.0"
    PowerShellVersion:"2.0"


Végül egy mező nem támogatottak, például a "parancs" használata azt fogja csak figyelmen kívül hagyja, és keresse a mezőket. Ezért a következő lekérdezés

    commands:blobs storage
    
Az értelmezett pontosan ugyanaz, mint ez a lekérdezés:

    blobs storage

