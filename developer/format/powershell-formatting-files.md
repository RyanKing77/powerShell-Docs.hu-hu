---
title: Windows PowerShell fájlok formázása |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 5d4c8f84-ebd2-4405-bb10-cfc5400d4ad6
caps.latest.revision: 6
ms.openlocfilehash: 49344d32dfcef36a904772b4a7237646a63cb12a
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62065378"
---
# <a name="windows-powershell-formatting-files"></a>Windows PowerShelles formázási fájlok

Windows PowerShell biztosít több formázási fájlt (. format.ps1xml), amely a telepítési könyvtárban találhatók (`$pshome`). A fájlok mindegyike meghatározza, hogy a .NET-objektumokká meghatározott készletének az alapértelmezett megjelenítést. Soha nem kell módosítani ezeket a fájlokat. Azonban használhatja őket referenciaként a saját egyéni formázási fájlok létrehozásához.

Certificate.Format.ps1xml azt határozza meg a megjelenített objektumok a tanúsítványtárolóban, például az x.509-tanúsítványokat és a tanúsítványtárolókat.

DotNetTypes.Format.ps1xml határozza meg az egyéb .NET-objektumokat, például CultureInfo FileVersionInfo és EventLogEntry objektumok megjelenítéséhez.

FileSystem.Format.ps1xml fájlrendszerobjektumok, például a fájl- és objektumok megjelenítését határozza meg.

A különböző nézetek által használt Help.Format.ps1xml Defines a [Get-Help](/powershell/module/Microsoft.PowerShell.Core/Get-Help) parancsmagot, például a részletes, teljes, a paraméterek és nézeteket.

PowerShellCore.Format.ps1xml határozza meg a Windows PowerShell core parancsmagok, például által visszaadott objektumokhoz által létrehozott objektumok megjelenítéséhez a [Get-Member](/powershell/module/Microsoft.PowerShell.Utility/Get-Member) és [Get-előzmények](/powershell/module/Microsoft.PowerShell.Core/Get-History) parancsmagok.

PowerShellTrace.Format.ps1xml meghatározza a nyomkövetési objektumok, például a rendszer által létrehozott megjelenítését a [nyomkövetési-parancs](/powershell/module/Microsoft.PowerShell.Utility/Trace-Command) parancsmagot.

Registry.Format.ps1xml határozza meg, például a kulcs és a bejegyzés objektumok beállításjegyzék-objektumok megjelenítéséhez.

## <a name="see-also"></a>Lásd még:

[Egy Windows PowerShell-parancsmag írása](../cmdlet/writing-a-windows-powershell-cmdlet.md)
