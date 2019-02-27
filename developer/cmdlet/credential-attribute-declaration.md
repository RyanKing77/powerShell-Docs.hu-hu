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
ms.openlocfilehash: abdd6e915b768b8ac688b6fc8c3194723961765e
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56851988"
---
# <a name="credential-attribute-declaration"></a><span data-ttu-id="9dde9-102">Hitelesítő adatok attribútumdeklarációja</span><span class="sxs-lookup"><span data-stu-id="9dde9-102">Credential Attribute Declaration</span></span>

<span data-ttu-id="9dde9-103">A hitelesítő adatok attribútum értéke, amely a hitelesítő adat típusú paraméterek együtt nem kötelező attribútum [System.Management.Automation.Pscredential](/dotnet/api/System.Management.Automation.PSCredential) úgy, hogy egy karakterlánc is adható át argumentumként a paramétert.</span><span class="sxs-lookup"><span data-stu-id="9dde9-103">The Credential attribute is an optional attribute that can be used with credential parameters of type [System.Management.Automation.Pscredential](/dotnet/api/System.Management.Automation.PSCredential) so that a string can also be passed as an argument to the parameter.</span></span> <span data-ttu-id="9dde9-104">Deklarace parametru hozzáadta ezt az attribútumot, ha a Windows PowerShell be a karakterláncot tartalmazó bemeneti alakít egy [System.Management.Automation.Pscredential](/dotnet/api/System.Management.Automation.PSCredential) objektum.</span><span class="sxs-lookup"><span data-stu-id="9dde9-104">When this attribute is added to a parameter declaration, Windows PowerShell converts the string input into a [System.Management.Automation.Pscredential](/dotnet/api/System.Management.Automation.PSCredential) object.</span></span> <span data-ttu-id="9dde9-105">Ha például a [Get-Credential](/powershell/module/Microsoft.PowerShell.Security/Get-Credential) parancsmag rendelkezik készítése a Windows PowerShell ezt az attribútumot használja a [System.Management.Automation.Pscredential](/dotnet/api/System.Management.Automation.PSCredential) a parancsmag által visszaadott objektumot.</span><span class="sxs-lookup"><span data-stu-id="9dde9-105">For example, the [Get-Credential](/powershell/module/Microsoft.PowerShell.Security/Get-Credential) cmdlet uses this attribute to have Windows PowerShell generate the [System.Management.Automation.Pscredential](/dotnet/api/System.Management.Automation.PSCredential) object that is returned by the cmdlet.</span></span>
<span data-ttu-id="9dde9-106">A hitelesítő adatok attribútum értéke, amely a hitelesítő adat típusú paraméterek együtt nem kötelező attribútum [System.Management.Automation.Pscredential](/dotnet/api/System.Management.Automation.PSCredential) úgy, hogy egy karakterlánc is adható át argumentumként a paramétert.</span><span class="sxs-lookup"><span data-stu-id="9dde9-106">The Credential attribute is an optional attribute that can be used with credential parameters of type [System.Management.Automation.Pscredential](/dotnet/api/System.Management.Automation.PSCredential) so that a string can also be passed as an argument to the parameter.</span></span> <span data-ttu-id="9dde9-107">Deklarace parametru hozzáadta ezt az attribútumot, ha a Windows PowerShell be a karakterláncot tartalmazó bemeneti alakít egy [System.Management.Automation.Pscredential](/dotnet/api/System.Management.Automation.PSCredential) objektum.</span><span class="sxs-lookup"><span data-stu-id="9dde9-107">When this attribute is added to a parameter declaration, Windows PowerShell converts the string input into a [System.Management.Automation.Pscredential](/dotnet/api/System.Management.Automation.PSCredential) object.</span></span> <span data-ttu-id="9dde9-108">Ha például a [Get-Credential](/powershell/module/Microsoft.PowerShell.Security/Get-Credential) parancsmag rendelkezik készítése a Windows PowerShell ezt az attribútumot használja a [System.Management.Automation.Pscredential](/dotnet/api/System.Management.Automation.PSCredential) a parancsmag által visszaadott objektumot.</span><span class="sxs-lookup"><span data-stu-id="9dde9-108">For example, the [Get-Credential](/powershell/module/Microsoft.PowerShell.Security/Get-Credential) cmdlet uses this attribute to have Windows PowerShell generate the [System.Management.Automation.Pscredential](/dotnet/api/System.Management.Automation.PSCredential) object that is returned by the cmdlet.</span></span>

## <a name="syntax"></a><span data-ttu-id="9dde9-109">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="9dde9-109">Syntax</span></span>

```csharp
[Credential]
```

## <a name="remarks"></a><span data-ttu-id="9dde9-110">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="9dde9-110">Remarks</span></span>

- <span data-ttu-id="9dde9-111">Általában ez az attribútum típusú paraméterek által használt [System.Management.Automation.Pscredential](/dotnet/api/System.Management.Automation.PSCredential) úgy, hogy egy karakterlánc is adható át argumentumként a paramétert.</span><span class="sxs-lookup"><span data-stu-id="9dde9-111">Typically this attribute is used by parameters of type [System.Management.Automation.Pscredential](/dotnet/api/System.Management.Automation.PSCredential) so that a string can also be passed as an argument to the parameter.</span></span> <span data-ttu-id="9dde9-112">Ha egy [System.Management.Automation.Pscredential](/dotnet/api/System.Management.Automation.PSCredential) objektum átadott paraméter, a Windows PowerShell nem csinál semmit.</span><span class="sxs-lookup"><span data-stu-id="9dde9-112">When a [System.Management.Automation.Pscredential](/dotnet/api/System.Management.Automation.PSCredential) object is passed to the parameter, Windows PowerShell does nothing.</span></span>

- <span data-ttu-id="9dde9-113">Amikor létrehozza a [System.Management.Automation.Pscredential](/dotnet/api/System.Management.Automation.PSCredential) objektumot, a Windows PowerShell a az aktuális állomás használatával jeleníti meg a megfelelő utasításokat a felhasználó számára.</span><span class="sxs-lookup"><span data-stu-id="9dde9-113">When creating the [System.Management.Automation.Pscredential](/dotnet/api/System.Management.Automation.PSCredential) object, Windows PowerShell uses the current Host to display the appropriate prompts to the user.</span></span> <span data-ttu-id="9dde9-114">Például az alapértelmezett gazdagép jeleníti meg egy felhasználónevet és jelszót kérni, ha ez az attribútum.</span><span class="sxs-lookup"><span data-stu-id="9dde9-114">For example, the default Host displays a prompt for a user name and password when this attribute is used.</span></span> <span data-ttu-id="9dde9-115">Ha egy egyéni gazdagépre használja, amely meghatározza, hogy egy másik parancssort, majd a kérés jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="9dde9-115">However, if a custom host is being used that defines a different prompt then that prompt would be displayed.</span></span>

- <span data-ttu-id="9dde9-116">Ez az attribútum a paraméter-attribútumhoz használnak.</span><span class="sxs-lookup"><span data-stu-id="9dde9-116">This attribute is used with the Parameter attribute.</span></span> <span data-ttu-id="9dde9-117">Ezt az attribútumot kapcsolatos további információkért lásd: [paraméter típusattribútum-deklaráció](./parameter-attribute-declaration.md).</span><span class="sxs-lookup"><span data-stu-id="9dde9-117">For more information about that attribute, see [Parameter Attribute Declaration](./parameter-attribute-declaration.md).</span></span>

- <span data-ttu-id="9dde9-118">A hitelesítő adatok attribútum határozza meg a [System.Management.Automation.Credentialattribute](/dotnet/api/System.Management.Automation.CredentialAttribute) osztály.</span><span class="sxs-lookup"><span data-stu-id="9dde9-118">The credential attribute is defined by the [System.Management.Automation.Credentialattribute](/dotnet/api/System.Management.Automation.CredentialAttribute) class.</span></span>

## <a name="see-also"></a><span data-ttu-id="9dde9-119">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="9dde9-119">See Also</span></span>

[<span data-ttu-id="9dde9-120">A paraméter-aliasok</span><span class="sxs-lookup"><span data-stu-id="9dde9-120">Parameter Aliases</span></span>](./parameter-aliases.md)

[<span data-ttu-id="9dde9-121">Deklarace parametru attribútum</span><span class="sxs-lookup"><span data-stu-id="9dde9-121">Parameter Attribute Declaration</span></span>](./parameter-attribute-declaration.md)

[<span data-ttu-id="9dde9-122">Egy Windows PowerShell-parancsmag írása</span><span class="sxs-lookup"><span data-stu-id="9dde9-122">Writing a Windows PowerShell Cmdlet</span></span>](./writing-a-windows-powershell-cmdlet.md)
