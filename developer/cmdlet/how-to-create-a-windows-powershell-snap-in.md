---
title: Egy Windows PowerShell beépülő modul létrehozása |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- snap-ins [PowerShell SDK], examples
ms.assetid: 71bd9b2c-5f2e-4aa8-b5fe-08c956540d37
caps.latest.revision: 10
ms.openlocfilehash: 73834cea1d90943cf954728d6295d8eb33e14f57
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56849440"
---
# <a name="how-to-create-a-windows-powershell-snap-in"></a>Windows PowerShelles beépülő modul létrehozása

Egy Windows PowerShell beépülő modul lehetővé teszi a parancsmagok és a egy másik Windows PowerShell-szolgáltató regisztrálása a rendszerhéj, így kiterjesztése a rendszerhéj működését. A Windows PowerShell beépülő modult is regisztrálhat a parancsmagok és szolgáltatók egyetlen szerelvényt, vagy hogy regisztrálni tudjon a parancsmagok és szolgáltatók adott listáját.

Beépülő modul szerelvényeket egy védett könyvtárban kell telepíteni, ugyanúgy, mint más operációs rendszerekkel lennének. Ellenkező esetben a rosszindulatú felhasználók is cserélje le egy szerelvény nem biztonságos kódra.

## <a name="windows-powershell-snap-in-classes"></a>Windows PowerShell beépülő modul osztályai

Minden Windows PowerShell beépülő modul osztályai célosztályából származik a [System.Management.Automation.Pssnapin](/dotnet/api/System.Management.Automation.PSSnapIn) vagy [System.Management.Automation.Custompssnapin](/dotnet/api/System.Management.Automation.CustomPSSnapIn) osztályokat.

## <a name="examples"></a>Példák

[Egy Windows PowerShell beépülő modul írása](./writing-a-windows-powershell-snap-in.md): Ez a példa bemutatja, hogyan hozhat létre, amellyel a parancsmagok és szolgáltatók regisztrálása egy szerelvény beépülő.

[Egy egyéni Windows PowerShell beépülő modul írása](./writing-a-custom-windows-powershell-snap-in.md): Ez a példa bemutatja, hogyan hozhat létre egy egyéni beépülő modul, amely egyetlen szerelvényben parancsmagok és szolgáltatók, amely már nem létezik, vagy egy meghatározott készletének regisztrálásához használatos.

## <a name="see-also"></a>Lásd még:

[System.Management.Automation.Pssnapin](/dotnet/api/System.Management.Automation.PSSnapIn)

[System.Management.Automation.Custompssnapin](/dotnet/api/System.Management.Automation.CustomPSSnapIn)

[Parancsmagok regisztrálása](./registering-cmdlets.md)

[Windows PowerShell Shell SDK](../windows-powershell-reference.md)
