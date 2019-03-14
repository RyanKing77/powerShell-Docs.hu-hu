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
ms.openlocfilehash: 1513d340cdadc5cb7622e791cc3c163ff39dfe1d
ms.sourcegitcommit: 5990f04b8042ef2d8e571bec6d5b051e64c9921c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/12/2019
ms.locfileid: "57795402"
---
# <a name="credential-attribute-declaration"></a><span data-ttu-id="2a612-102">Hitelesítő adatok attribútumdeklarációja</span><span class="sxs-lookup"><span data-stu-id="2a612-102">Credential Attribute Declaration</span></span>

<span data-ttu-id="2a612-103">A hitelesítő adatok attribútum értéke, amely a hitelesítő adat típusú paraméterek együtt nem kötelező attribútum [System.Management.Automation.Pscredential](/dotnet/api/System.Management.Automation.PSCredential) úgy, hogy egy karakterlánc is adható át argumentumként a paramétert.</span><span class="sxs-lookup"><span data-stu-id="2a612-103">The Credential attribute is an optional attribute that can be used with credential parameters of type [System.Management.Automation.Pscredential](/dotnet/api/System.Management.Automation.PSCredential) so that a string can also be passed as an argument to the parameter.</span></span> <span data-ttu-id="2a612-104">Deklarace parametru hozzáadta ezt az attribútumot, ha a Windows PowerShell be a karakterláncot tartalmazó bemeneti alakít egy [System.Management.Automation.Pscredential](/dotnet/api/System.Management.Automation.PSCredential) objektum.</span><span class="sxs-lookup"><span data-stu-id="2a612-104">When this attribute is added to a parameter declaration, Windows PowerShell converts the string input into a [System.Management.Automation.Pscredential](/dotnet/api/System.Management.Automation.PSCredential) object.</span></span> <span data-ttu-id="2a612-105">Ha például a [Get-Credential](/powershell/module/Microsoft.PowerShell.Security/Get-Credential) parancsmag rendelkezik készítése a Windows PowerShell ezt az attribútumot használja a [System.Management.Automation.Pscredential](/dotnet/api/System.Management.Automation.PSCredential) a parancsmag által visszaadott objektumot.</span><span class="sxs-lookup"><span data-stu-id="2a612-105">For example, the [Get-Credential](/powershell/module/Microsoft.PowerShell.Security/Get-Credential) cmdlet uses this attribute to have Windows PowerShell generate the [System.Management.Automation.Pscredential](/dotnet/api/System.Management.Automation.PSCredential) object that is returned by the cmdlet.</span></span>

## <a name="syntax"></a><span data-ttu-id="2a612-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="2a612-106">Syntax</span></span>

```csharp
[Credential]
```

## <a name="remarks"></a><span data-ttu-id="2a612-107">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="2a612-107">Remarks</span></span>

- <span data-ttu-id="2a612-108">Általában ez az attribútum típusú paraméterek által használt [System.Management.Automation.Pscredential](/dotnet/api/System.Management.Automation.PSCredential) úgy, hogy egy karakterlánc is adható át argumentumként a paramétert.</span><span class="sxs-lookup"><span data-stu-id="2a612-108">Typically this attribute is used by parameters of type [System.Management.Automation.Pscredential](/dotnet/api/System.Management.Automation.PSCredential) so that a string can also be passed as an argument to the parameter.</span></span> <span data-ttu-id="2a612-109">Ha egy [System.Management.Automation.Pscredential](/dotnet/api/System.Management.Automation.PSCredential) objektum átadott paraméter, a Windows PowerShell nem csinál semmit.</span><span class="sxs-lookup"><span data-stu-id="2a612-109">When a [System.Management.Automation.Pscredential](/dotnet/api/System.Management.Automation.PSCredential) object is passed to the parameter, Windows PowerShell does nothing.</span></span>

- <span data-ttu-id="2a612-110">Amikor létrehozza a [System.Management.Automation.Pscredential](/dotnet/api/System.Management.Automation.PSCredential) objektumot, a Windows PowerShell a az aktuális állomás használatával jeleníti meg a megfelelő utasításokat a felhasználó számára.</span><span class="sxs-lookup"><span data-stu-id="2a612-110">When creating the [System.Management.Automation.Pscredential](/dotnet/api/System.Management.Automation.PSCredential) object, Windows PowerShell uses the current Host to display the appropriate prompts to the user.</span></span> <span data-ttu-id="2a612-111">Például az alapértelmezett gazdagép jeleníti meg egy felhasználónevet és jelszót kérni, ha ez az attribútum.</span><span class="sxs-lookup"><span data-stu-id="2a612-111">For example, the default Host displays a prompt for a user name and password when this attribute is used.</span></span> <span data-ttu-id="2a612-112">Ha egy egyéni gazdagépre használja, amely meghatározza, hogy egy másik parancssort, majd a kérés jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="2a612-112">However, if a custom host is being used that defines a different prompt then that prompt would be displayed.</span></span>

- <span data-ttu-id="2a612-113">Ez az attribútum a paraméter-attribútumhoz használnak.</span><span class="sxs-lookup"><span data-stu-id="2a612-113">This attribute is used with the Parameter attribute.</span></span> <span data-ttu-id="2a612-114">Ezt az attribútumot kapcsolatos további információkért lásd: [paraméter típusattribútum-deklaráció](./parameter-attribute-declaration.md).</span><span class="sxs-lookup"><span data-stu-id="2a612-114">For more information about that attribute, see [Parameter Attribute Declaration](./parameter-attribute-declaration.md).</span></span>

- <span data-ttu-id="2a612-115">A hitelesítő adatok attribútum határozza meg a [System.Management.Automation.Credentialattribute](/dotnet/api/System.Management.Automation.CredentialAttribute) osztály.</span><span class="sxs-lookup"><span data-stu-id="2a612-115">The credential attribute is defined by the [System.Management.Automation.Credentialattribute](/dotnet/api/System.Management.Automation.CredentialAttribute) class.</span></span>

## <a name="see-also"></a><span data-ttu-id="2a612-116">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="2a612-116">See Also</span></span>

[<span data-ttu-id="2a612-117">A paraméter-aliasok</span><span class="sxs-lookup"><span data-stu-id="2a612-117">Parameter Aliases</span></span>](./parameter-aliases.md)

[<span data-ttu-id="2a612-118">Deklarace parametru attribútum</span><span class="sxs-lookup"><span data-stu-id="2a612-118">Parameter Attribute Declaration</span></span>](./parameter-attribute-declaration.md)

[<span data-ttu-id="2a612-119">Egy Windows PowerShell-parancsmag írása</span><span class="sxs-lookup"><span data-stu-id="2a612-119">Writing a Windows PowerShell Cmdlet</span></span>](./writing-a-windows-powershell-cmdlet.md)
