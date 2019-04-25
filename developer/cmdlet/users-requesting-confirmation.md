---
title: Felhasználói jóváhagyás kérése |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 6f337498-c534-40ed-968a-09d4d9ca3849
caps.latest.revision: 8
ms.openlocfilehash: ed9ff9fc1668a89e1ac0ceac8f0800a15b349226
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62067218"
---
# <a name="users-requesting-confirmation"></a>Megerősítést kérő felhasználók

Érték megadása `true` számára a `SupportsShouldProcess` paramétert, a parancsmag attribútum nyilatkozat, a felhasználók megadhatják a `Confirm` paraméter a parancssorban.

Az alapértelmezett környezetben a felhasználók megadhatják a `Confirm` paraméter vagy `"-Confirm:$true` megerősítési kérés érkezett, hogy amikor a [System.Management.Automation.Cmdlet.ShouldProcess](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) módszert hívja meg. Ez nincs hatással lévő [System.Management.Automation.Cmdlet.ShouldProcess](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) eseménymegerősítési kéréseknek, akár nagy hatású műveletek esetében.

Ha `Confirm` nincs megadva, a [System.Management.Automation.Cmdlet.ShouldProcess](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) hívás megerősítését kéri, ha a `$ConfirmPreference` preferenciaváltozó egyenlő vagy nagyobb, mint a `ConfirmImpact` beállításaként a a parancsmag vagy szolgáltató. A beállítás alapértelmezett értékét `$ConfirmPreference` magas. Ezért az alapértelmezett környezet csak a parancsmagok és szolgáltatók, amely nagy hatású művelet megadása kér megerősítést.

Ha `Confirm` false (hamis), vagy ha `"-Confirm:$false` meg van adva, a [System.Management.Automation.Cmdlet.ShouldProcess](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) hívás megerősítését kéri a felhasználótól, és a `$ConfirmPreference` felületváltozóban a rendszer figyelmen kívül hagyja.

## <a name="remarks"></a>Megjegyzés

- A parancsmagok és szolgáltatók által megadott `SupportsShouldProcess`, azonban nem `ConfirmImpact`, műveletek kezelése "közepes hatású" műveleteket, és nem alapértelmezés szerint fogja kérni. A hatás szintje nem éri el az alapértelmezett beállítás, a `$ConfirmPreference` preferenciaváltozót.

- Ha a felhasználó adja meg a `Verbose` paramétert, akkor értesítjük a művelet akkor is, ha azok nem megerősítést kér.

## <a name="see-also"></a>Lásd még:

[Egy Windows PowerShell-parancsmag írása](./writing-a-windows-powershell-cmdlet.md)
