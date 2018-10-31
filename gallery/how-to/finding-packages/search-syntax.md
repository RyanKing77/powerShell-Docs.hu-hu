---
ms.date: 06/12/2017
contributor: JKeithB
keywords: katalógus, a powershell, a parancsmag, a psgallery
title: Katalóguskeresési szintaxis
ms.openlocfilehash: 9aadb6771c85845cc3fa05cb56f0194b060d1c1b
ms.sourcegitcommit: 98b7cfd8ad5718efa8e320526ca76c3cc4141d78
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/25/2018
ms.locfileid: "50004078"
---
# <a name="gallery-search-syntax"></a>Katalóguskeresési szintaxis

PowerShell-galériából kínál egy szöveges searchbox, ahol szavak, kifejezéseket és kulcsszó kifejezések használhatja meg a keresési eredmények szűkítéséhez.

## <a name="search-by-keywords"></a>Keresés kulcsszavak szerint

    dsc azure sql

Keresés hajtsa végre az ajánlott annak érdekében, hogy az összes 3 kulcsszavakat tartalmazó megfelelő dokumentumok keresése, és megfelelő dokumentumokat.

## <a name="search-using-phrases-and-keywords"></a>Mondatok és a kulcsszavak keresése

    "azure sql" deployment

Írja be egy kifejezést idézőjelek között ("") módosítsa a keresési, keresse meg az adott kifejezést külön kulcsszavak helyett.
Egyező dokumentumok általában tartalmaznia kell a pontos kifejezés "az azure sql", így például a kis-és nagybetűk változata "Az azure SQL", és a "telepítés" szó általában is tartalmaznak.

## <a name="filtering-on-fields"></a>A mezők szűrése

Kereshet egy adott csomag azonosítója (vagy "Id" vagy "id"), vagy bizonyos más mezők illesztésével keresse a mező nevét a kifejezéseket.

A kereshető mezők jelenleg "Id", "Verziójú", "Címke", "Szerző", "Tulajdonos", "Függvények", 'Parancsmagok', "DscResources" és "PowerShellVersion".

[Mi a különbség a között Azonosítóját és címét? ID az a név, használja a konzolon. Cím értéke: Mi látható az oldal felső részén található a csomagot a keresési eredmények között.]

## <a name="examples"></a>Példák

    ID:"PSReadline"
    id:"AzureRM.Profile"

megtalálja a csomagokat az "PSReadline" vagy "AzureRM.Profile" az azonosító mezőben jelölik.

    Id:"AzureRM.Profile"

az azonosító mezőben keresse meg a csomagokat az "AzureRM.Profile" egy másik módja van.

Az "Id" szűrő abban az esetben egy karakterláncrészletet egyeznek, így ha, keresse meg a következő:

    Id:"azure"

Például a "AzureRM.Profile" és "Azure.Storage" eredményt fog kapni.

Egyetlen mezőben több kulcsszavak alapján is kereshet. Vagy keverheti a mezőket.

    id:azure tags:intellisense
    id:azure id:storage

És kifejezés kereshet:

    id:"azure.storage"


DSC-címkével ellátott összes csomagok keresése.

    Tags:"DSC"

Keresés a megadott függvény az összes csomagot.

    Functions:"Update-AzureRM"

Keresés a megadott parancsmag az összes csomagot.

    Cmdlets:"Get-AzureRmEnvironment"

Keresés az összes csomag DSC erőforrás a megadott névvel.

    DscResources:"xArchive"

A megadott PowerShellVersion az összes csomag keresése

    PowerShellVersion:"5.0"
    PowerShellVersion:"3.0"
    PowerShellVersion:"2.0"


Végül ha egy mező nem támogatjuk, például a "parancs", azt fogja csak figyelmen kívül hagyhatja azt és a Keresés az összes mezőt. Ezért a következő lekérdezést

    commands:blobs storage

Az értelmezett pontosan ugyanaz, mint ez a lekérdezés:

    blobs storage
