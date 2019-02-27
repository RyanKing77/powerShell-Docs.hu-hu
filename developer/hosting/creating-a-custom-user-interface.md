---
title: Egyéni felhasználói felület létrehozása |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: d7286443-eed4-43d5-b809-50cdcdcba088
caps.latest.revision: 4
ms.openlocfilehash: 23518c625fe1138e1bd2bcc895274cb21d7daf8a
ms.sourcegitcommit: c581c4c8036edf55147e7bce4b00c860da6c5a8b
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/25/2019
ms.locfileid: "56852212"
---
# <a name="creating-a-custom-user-interface"></a>Egyéni felhasználói felület létrehozása

Windows PowerShell az absztrakt osztályok és a felületek, amelyek lehetővé teszik, hogy hozzon létre egy egyéni interaktív felhasználói felület, amelyen a Windows PowerShell-motor biztosít. Az egyéni felhasználói felület létrehozása, meg kell valósítani a [System.Management.Automation.Host.PSHost](/dotnet/api/System.Management.Automation.Host.PSHost) osztály. Igény szerint is alkalmazhat a [System.Management.Automation.Host.Pshostrawuserinterface](/dotnet/api/System.Management.Automation.Host.PSHostRawUserInterface)és [System.Management.Automation.Host.Pshostuserinterface](/dotnet/api/System.Management.Automation.Host.PSHostUserInterface) osztályok és a [System.Management.Automation.Host.Ihostsupportsinteractivesession](/dotnet/api/System.Management.Automation.Host.IHostSupportsInteractiveSession) és [System.Management.Automation.Host.Ihostuisupportsmultiplechoiceselection](/dotnet/api/System.Management.Automation.Host.IHostUISupportsMultipleChoiceSelection) felületek.
