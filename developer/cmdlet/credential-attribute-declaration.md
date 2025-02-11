---
title: Hitelesítőadat-típusattribútum-deklaráció |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 96a5dcad-faed-44d8-8c80-321f10499710
caps.latest.revision: 6
ms.openlocfilehash: 49a62ccb09f06f77862d4737199e58293e7fbe0a
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62068317"
---
# <a name="credential-attribute-declaration"></a>Hitelesítő adatok attribútumdeklarációja

A hitelesítő adatok attribútum értéke, amely a hitelesítő adat típusú paraméterek együtt nem kötelező attribútum [System.Management.Automation.PSCredential](/dotnet/api/System.Management.Automation.PSCredential) úgy, hogy egy karakterlánc is adható át argumentumként a paramétert. Deklarace parametru hozzáadta ezt az attribútumot, ha a Windows PowerShell be a karakterláncot tartalmazó bemeneti alakít egy [System.Management.Automation.PSCredential](/dotnet/api/System.Management.Automation.PSCredential) objektum. Ha például a [Get-Credential](/powershell/module/Microsoft.PowerShell.Security/Get-Credential) parancsmag rendelkezik készítése a Windows PowerShell ezt az attribútumot használja a [System.Management.Automation.PSCredential](/dotnet/api/System.Management.Automation.PSCredential) a parancsmag által visszaadott objektumot.

## <a name="syntax"></a>Szintaxis

```csharp
[Credential]
```

## <a name="remarks"></a>Megjegyzés

- Általában ez az attribútum típusú paraméterek által használt [System.Management.Automation.PSCredential](/dotnet/api/System.Management.Automation.PSCredential) úgy, hogy egy karakterlánc is adható át argumentumként a paramétert. Ha egy [System.Management.Automation.PSCredential](/dotnet/api/System.Management.Automation.PSCredential) objektum átadott paraméter, a Windows PowerShell nem csinál semmit.

- Amikor létrehozza a [System.Management.Automation.PSCredential](/dotnet/api/System.Management.Automation.PSCredential) objektumot, a Windows PowerShell a az aktuális állomás használatával jeleníti meg a megfelelő utasításokat a felhasználó számára. Például az alapértelmezett gazdagép jeleníti meg egy felhasználónevet és jelszót kérni, ha ez az attribútum. Ha egy egyéni gazdagépre használja, amely meghatározza, hogy egy másik parancssort, majd a kérés jelenik meg.

- Ez az attribútum a paraméter-attribútumhoz használnak. Ezt az attribútumot kapcsolatos további információkért lásd: [paraméter típusattribútum-deklaráció](./parameter-attribute-declaration.md).

- A hitelesítő adatok attribútum határozza meg a [System.Management.Automation.Credentialattribute](/dotnet/api/System.Management.Automation.CredentialAttribute) osztály.

## <a name="see-also"></a>Lásd még:

[A paraméter-aliasok](./parameter-aliases.md)

[Deklarace parametru attribútum](./parameter-attribute-declaration.md)

[Egy Windows PowerShell-parancsmag írása](./writing-a-windows-powershell-cmdlet.md)
