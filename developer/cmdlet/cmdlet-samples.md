---
title: Parancsmag-minták |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: b99d53fc-0af9-426b-82ce-09955e031d4b
caps.latest.revision: 13
ms.openlocfilehash: d919d4ad8554e762230c1448d81b50e27c38ba99
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56851967"
---
# <a name="cmdlet-samples"></a>Parancsmagminták

Ez a szakasz ismerteti, amelyek a Windows PowerShell 2.0 SDK-ban van megadva. Ez a szakasz témakörei a kód másolásához, vagy nyissa meg a forrásfájlokat, az SDK-val telepített. A [Windows PowerShell 2.0-s Software Development Kit (SDK)](https://www.microsoft.com/en-us/download/details.aspx?id=2560) információs fájljaiban, forrásfájlokat és a Visual Studio soubory projektu minden mintához. Az SDK-val telepített, részben találhat példákat talál a `<Drive>:\Program Files (x86)\Microsoft SDKs\Windows\v7.0\Samples\sysmgmt\WindowsPowerShell\` mappát.

## <a name="in-this-section"></a>A szakasz tartalma

[GetProcessSample01 minta](./getprocesssample01-sample.md) Ez a példa bemutatja, hogyan írhat olyan parancsmagot, amely lekéri a folyamatok a helyi számítógépen.

[GetProcessSample02 minta](./getprocesssample02-sample.md) Ez a példa bemutatja, hogyan írhat olyan parancsmagot, amely lekéri a folyamatok a helyi számítógépen. A Name paraméter, amely segítségével adja meg a lekérdezni kívánt folyamatokat tartalmaz.

[GetProcessSample03 minta](./getprocesssample03-sample.md) Ez a példa bemutatja, hogyan írhat olyan parancsmagot, amely lekéri a folyamatok a helyi számítógépen. Biztosít egy Name paraméter, amely elfogadja a folyamat egy objektumot, vagy egy értéket egy tulajdonságot egy objektum, amelynek tulajdonság neve megegyezik a paraméter neve.

[GetProcessSample04 minta](./getprocesssample04-sample.md) Ez a példa bemutatja, hogyan írhat olyan parancsmagot, amely lekéri a folyamatok a helyi számítógépen. Ha hiba történik egy folyamat beolvasása közben nonterminating hiba állít elő.

[GetProcessSample05 minta](./getprocesssample05-sample.md) Ez a példa bemutatja egy a Get-Proc parancsmag teljes verzióját.

[StopProcessSample01 minta](./stopprocesssample01-sample.md) Ez a példa bemutatja, hogyan írható olyan parancsmagot, amely visszajelzést kér a felhasználó előtt megkísérli leállítani a folyamatot, és hogyan valósíthat meg egy `PassThru` paraméter, amely azt jelzi, hogy a felhasználó szeretne a parancsmag adja vissza egy az objektum.

[StopProcessSample02 minta](./stopprocesssample02-sample.md) Ez a példa bemutatja, hogyan írható olyan parancsmagot, amely megjeleníti a verbose, a debug és figyelmeztető üzenetek a helyi számítógépen lévő folyamatok leállítása közben.

[StopProcessSample03 minta](./stopprocesssample03-sample.md) Ez a példa bemutatja, hogyan írhat, amelyek paraméterei aliasokat, és hogy rendelkezik a parancsmag támogatja a helyettesítő karaktereket.

[StopProcessSample04 minta](./stopprocesssample04-sample.md) Ez a példa bemutatja, hogyan írhat olyan parancsmagot, amely paraméterkészlettel nyilatkozik, adja meg az alapértelmezett paraméter beállítása, és egy bemeneti objektumot tud fogadni.

[Events01 minta](./events01-sample.md) Ez a példa bemutatja, hogyan hozhat létre olyan parancsmagot, amely lehetővé teszi, hogy a felhasználó regisztrálhatja az események által kiváltott [System.IO.Filesystemwatcher](/dotnet/api/System.IO.FileSystemWatcher). Ezzel a parancsmaggal felhasználók, például regisztrálhatnak egy művelet hajtható végre, ha létrejön egy fájl egy adott könyvtárban. Ez a minta származik a [Microsoft.Powershell.Commands.Objecteventregistrationbase](/dotnet/api/Microsoft.PowerShell.Commands.ObjectEventRegistrationBase) alaposztály.

## <a name="see-also"></a>Lásd még:

[Egy Windows PowerShell-parancsmag írása](./writing-a-windows-powershell-cmdlet.md)
