---
ms.date: 06/12/2017
contributor: JKeithB
keywords: katalógus, a powershell, a parancsmag, a psgallery
title: Katalóguskeresési szintaxis
ms.openlocfilehash: aabcaa1f1b5b641ab5033c9ba2e358477c84a23b
ms.sourcegitcommit: e24525046dd37166b9d83eeecdc534726316f429
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/01/2018
ms.locfileid: "52742856"
---
# <a name="gallery-search-syntax"></a>Katalóguskeresési szintaxis

A PowerShell-galériából használatával kereshet a [PowerShell-galériából webhely](https://www.powershellgallery.com/).
PowerShell-galériából webhely kínál egy szöveges searchbox, ahol szavak, kifejezéseket és kulcsszó kifejezések használhatja meg a keresési eredmények szűkítéséhez.

## <a name="search-by-keywords"></a>Keresés kulcsszavak szerint

    dsc azure sql

Keresési megpróbálja megkeresni a megfelelő, az összes 3 kulcsszavakat tartalmazó dokumentumok, és megfelelő dokumentumokat.

## <a name="search-using-phrases-and-keywords"></a>Mondatok és a kulcsszavak keresése

    "azure sql" deployment

Írja be egy kifejezést idézőjelek között ("") módosítsa a keresési, keresse meg az adott kifejezést külön kulcsszavak helyett.
Egyező dokumentumok általában tartalmaznia kell a pontos kifejezés "az azure sql", így például a kis-és nagybetűk változata "Az azure SQL", és a "telepítés" szó általában is tartalmaznak.

## <a name="filtering-on-fields"></a>A mezők szűrése

Kereshet egy adott csomag azonosítója (vagy "Id" vagy "id"), vagy bizonyos más mezők illesztésével keresse a mező nevét a kifejezéseket.

A kereshető mezők jelenleg "Id", "Verziójú", "Címke", "Szerző", "Tulajdonos", "Függvények", 'Parancsmagok', "DscResources" és "PowerShellVersion".

[Mi a különbség a között Azonosítóját és címét? ID az a név, használja a konzolon. Cím értéke: Mi látható az oldal felső részén található a csomagot a keresési eredmények között.]

## <a name="examples"></a>Példák

    ID:PSReadline
    
megtalálja a csomagokat tartalmazó "PSReadline" azonosítóval.

    Id:"AzureRM.Profile"

az azonosító mezőben keresse meg a csomagokat az "AzureRM.Profile" egy másik módja van.

Az "Id" szűrő abban az esetben egy karakterláncrészletet egyeznek, így ha, keresse meg a következő:

    Id:"azure"

Ez biztosítja, hogy eredmények, amelyek tartalmazzák az AzureRM.Profile "és"Azure.Storage".

Egyetlen mezőben több kulcsszavak alapján is kereshet. 

    id:azure tags:intellisense

És kifejezés kereshet idézőjelek használata:

    id:"azure.storage"

DSC-címkével ellátott összes csomagok keresése.

    Tags:DSC

Keresés a megadott függvény az összes csomagot.

    Functions:Get-TreeSize

Keresés a megadott parancsmag az összes csomagot.

    Cmdlets:Get-AzureRmEnvironment

Keresés az összes csomag DSC erőforrás a megadott névvel.

    DscResources:xArchive

A megadott PowerShellVersion az összes csomag keresése

    PowerShellVersion:2.0

Végül ha egy mező nem támogatjuk, például a "parancs", azt fogja csak figyelmen kívül hagyhatja azt és a Keresés az összes mezőt. Ezért a következő lekérdezést

    commands:blobs storage

Az értelmezett pontosan ugyanaz, mint ez a lekérdezés:

    blobs storage
