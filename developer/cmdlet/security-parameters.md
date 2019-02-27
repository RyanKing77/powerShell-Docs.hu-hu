---
title: Biztonsági paramétereket |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: e199bba3-90d3-41ca-9d78-cb502e58508d
caps.latest.revision: 6
ms.openlocfilehash: bdf88de0258af75c01739f30a71fb4914cac3a9a
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56849027"
---
# <a name="security-parameters"></a><span data-ttu-id="5f312-102">Biztonsági paraméterek</span><span class="sxs-lookup"><span data-stu-id="5f312-102">Security Parameters</span></span>

<span data-ttu-id="5f312-103">Az alábbi táblázat a javasolt nevek és a egy művelet, például a tanúsítvány kulcs és a jogosultsági információk megadásához használható paraméterek, a biztonsági információk nyújtásához paraméterek funkciók.</span><span class="sxs-lookup"><span data-stu-id="5f312-103">The following table lists the recommended names and functionality for parameters used to provide security information for an operation, such as parameters that specify certificate key and privilege information.</span></span>

<span data-ttu-id="5f312-104">ACL-adattípus: Sztring</span><span class="sxs-lookup"><span data-stu-id="5f312-104">ACL Data type: String</span></span>

<span data-ttu-id="5f312-105">Ezzel a paraméterrel adja meg a hozzáférést vezérlő szintjét védelmének a katalógus és a egy egységes erőforrás-azonosító (URI) megvalósítása.</span><span class="sxs-lookup"><span data-stu-id="5f312-105">Implement this parameter to specify the access control level of protection for a catalog or for a Uniform Resource Identifier (URI).</span></span>

<span data-ttu-id="5f312-106">Tanúsítványfájl adattípus: Sztring</span><span class="sxs-lookup"><span data-stu-id="5f312-106">CertFile Data type: String</span></span>

<span data-ttu-id="5f312-107">Végrehajtja ezt a paramétert, úgy, hogy a felhasználó megadhatja a következők egyikét tartalmazó fájl neve:</span><span class="sxs-lookup"><span data-stu-id="5f312-107">Implement this parameter so that the user can specify the name of a file that contains one of the following:</span></span>

- <span data-ttu-id="5f312-108">A Base64 vagy használjon Distinguished Encoding Rules (DER) kódolású x.509-tanúsítvány</span><span class="sxs-lookup"><span data-stu-id="5f312-108">A Base64 or Distinguished Encoding Rules (DER) encoded x.509 certificate</span></span>

- <span data-ttu-id="5f312-109">Legalább egy tanúsítványt és kulcsot tartalmazó nyilvános kulcs titkosítási szabványok (PKCS) #12-fájl</span><span class="sxs-lookup"><span data-stu-id="5f312-109">A Public Key Cryptography Standards (PKCS) #12 file that contains at least one certificate and key</span></span>

<span data-ttu-id="5f312-110">CertIssuerName adattípus: Sztring</span><span class="sxs-lookup"><span data-stu-id="5f312-110">CertIssuerName Data type: String</span></span>

<span data-ttu-id="5f312-111">Ez a paraméter valósítja meg, hogy a felhasználó megadhatja a tanúsítvány kibocsátójának nevét, vagy úgy, hogy a felhasználó megadhatja a karakterláncrészletet.</span><span class="sxs-lookup"><span data-stu-id="5f312-111">Implement this parameter so that the user can specify the name of the issuer of a certificate or so that the user can specify a substring.</span></span>

<span data-ttu-id="5f312-112">CertRequestFile adattípus: Sztring</span><span class="sxs-lookup"><span data-stu-id="5f312-112">CertRequestFile Data type: String</span></span>

<span data-ttu-id="5f312-113">Ez a paraméter egy Base64 vagy DER kódolású PKCS #10 tanúsítványkérelmet tartalmazó fájl nevének megadására megvalósításához.</span><span class="sxs-lookup"><span data-stu-id="5f312-113">Implement this parameter to specify the name of a file that contains a Base64 or DER-encoded PKCS #10 certificate request.</span></span>

<span data-ttu-id="5f312-114">CertSerialNumber adattípus: Sztring</span><span class="sxs-lookup"><span data-stu-id="5f312-114">CertSerialNumber Data type: String</span></span>

<span data-ttu-id="5f312-115">Ezzel a paraméterrel adja meg a hitelesítésszolgáltató által kiállított sorozatszám megvalósításához.</span><span class="sxs-lookup"><span data-stu-id="5f312-115">Implement this parameter to specify the serial number that was issued by the certification authority.</span></span>

<span data-ttu-id="5f312-116">CertStoreLocation Data type: Sztring</span><span class="sxs-lookup"><span data-stu-id="5f312-116">CertStoreLocation Data type: String</span></span>

<span data-ttu-id="5f312-117">Ez a paraméter valósítja meg, hogy a felhasználó megadhatja a helyét, a tanúsítványtárolóban.</span><span class="sxs-lookup"><span data-stu-id="5f312-117">Implement this parameter so that the user can specify the location of the certificate store.</span></span> <span data-ttu-id="5f312-118">A hely az általában egy fájl elérési útját.</span><span class="sxs-lookup"><span data-stu-id="5f312-118">The location is typically a file path.</span></span>

<span data-ttu-id="5f312-119">CertSubjectName adattípus: Sztring</span><span class="sxs-lookup"><span data-stu-id="5f312-119">CertSubjectName Data type: String</span></span>

<span data-ttu-id="5f312-120">Ez a paraméter valósítja meg, hogy a felhasználó megadhatja a tanúsítvány kiállítója, vagy úgy, hogy a felhasználó megadhatja a karakterláncrészletet.</span><span class="sxs-lookup"><span data-stu-id="5f312-120">Implement this parameter so that the user can specify the issuer of a certificate or so that the user can specify a substring.</span></span>

<span data-ttu-id="5f312-121">CertUsage adattípus: Sztring</span><span class="sxs-lookup"><span data-stu-id="5f312-121">CertUsage Data type: String</span></span>

<span data-ttu-id="5f312-122">Ez a paraméter adja meg a kulcs használata vagy a kibővített kulcshasználat megvalósításához.</span><span class="sxs-lookup"><span data-stu-id="5f312-122">Implement this parameter to specify the key usage or the enhanced key usage.</span></span> <span data-ttu-id="5f312-123">A kulcs által megjeleníthető egy kicsit maszkolja, egy kicsit objektumazonosító (OID), vagy egy karakterláncot.</span><span class="sxs-lookup"><span data-stu-id="5f312-123">The key can be represented as a bit mask, a bit, an object identifier (OID), or a string.</span></span>

<span data-ttu-id="5f312-124">Írja be a hitelesítő adatok: [System.Management.Automation.Pscredential](/dotnet/api/System.Management.Automation.PSCredential)</span><span class="sxs-lookup"><span data-stu-id="5f312-124">Credential Data type: [System.Management.Automation.Pscredential](/dotnet/api/System.Management.Automation.PSCredential)</span></span>

<span data-ttu-id="5f312-125">Ez a paraméter valósítja meg, hogy a parancsmag automatikusan kérni fogja a felhasználótól a felhasználónevet vagy jelszót.</span><span class="sxs-lookup"><span data-stu-id="5f312-125">Implement this parameter so that the cmdlet will automatically prompt the user for a user name or password.</span></span> <span data-ttu-id="5f312-126">Mindkettő egy kérés jelenik meg, ha egy teljes hitelesítő adat nem közvetlenül tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="5f312-126">A prompt for both is displayed if a full credential is not supplied directly.</span></span>

<span data-ttu-id="5f312-127">Csp_név adattípus: Sztring</span><span class="sxs-lookup"><span data-stu-id="5f312-127">CSPName Data type: String</span></span>

<span data-ttu-id="5f312-128">Ez a paraméter valósítja meg, hogy a felhasználó megadhatja a tanúsítvány-szolgáltató (CSP) nevét.</span><span class="sxs-lookup"><span data-stu-id="5f312-128">Implement this parameter so that the user can specify the name of the certificate service provider (CSP).</span></span>

<span data-ttu-id="5f312-129">CSPType adattípus: Integer</span><span class="sxs-lookup"><span data-stu-id="5f312-129">CSPType Data type: Integer</span></span>

<span data-ttu-id="5f312-130">Ez a paraméter valósítja meg, hogy a felhasználó megadhatja a kriptográfiai Szolgáltató típusát.</span><span class="sxs-lookup"><span data-stu-id="5f312-130">Implement this parameter so that the user can specify the type of CSP.</span></span>

<span data-ttu-id="5f312-131">Írja be a csoport adatai: Sztring</span><span class="sxs-lookup"><span data-stu-id="5f312-131">Group Data type: String</span></span>

<span data-ttu-id="5f312-132">Ez a paraméter valósítja meg, hogy a felhasználó megadhatja a hozzáféréshez egyszerű gyűjteménye.</span><span class="sxs-lookup"><span data-stu-id="5f312-132">Implement this parameter so that the user can specify a collection of principals for access.</span></span> <span data-ttu-id="5f312-133">További információkért tekintse meg a leírását az `Principal` paraméter.</span><span class="sxs-lookup"><span data-stu-id="5f312-133">For more information, see the description of the `Principal` parameter.</span></span>

<span data-ttu-id="5f312-134">KeyAlgorithm adattípus: Sztring</span><span class="sxs-lookup"><span data-stu-id="5f312-134">KeyAlgorithm Data type: String</span></span>

<span data-ttu-id="5f312-135">Ez a paraméter valósítja meg, hogy a felhasználó megadhatja a kulcs létrehozásának algoritmus használandó. a biztonság.</span><span class="sxs-lookup"><span data-stu-id="5f312-135">Implement this parameter so that the user can specify the key generation algorithm to use for security.</span></span>

<span data-ttu-id="5f312-136">Kulcstárolónév adattípus: Sztring</span><span class="sxs-lookup"><span data-stu-id="5f312-136">KeyContainerName Data type: String</span></span>

<span data-ttu-id="5f312-137">Ez a paraméter valósítja meg, hogy a felhasználó megadhatja a kulcstároló nevével.</span><span class="sxs-lookup"><span data-stu-id="5f312-137">Implement this parameter so that the user can specify the name of the key container.</span></span>

<span data-ttu-id="5f312-138">Kulcshossz adattípus: Integer</span><span class="sxs-lookup"><span data-stu-id="5f312-138">KeyLength Data type: Integer</span></span>

<span data-ttu-id="5f312-139">Ez a paraméter valósítja meg, hogy a felhasználó úgy adhat meg a kulcs hosszát bitekben.</span><span class="sxs-lookup"><span data-stu-id="5f312-139">Implement this parameter so that the user can specify the length of the key in bits.</span></span>

<span data-ttu-id="5f312-140">A művelet adattípus: Sztring</span><span class="sxs-lookup"><span data-stu-id="5f312-140">Operation Data type: String</span></span>

<span data-ttu-id="5f312-141">Ez a paraméter valósítja meg, hogy a felhasználó megadhatja a védett objektumon végrehajtott műveletet.</span><span class="sxs-lookup"><span data-stu-id="5f312-141">Implement this parameter so that the user can specify an action that can be performed on a protected object.</span></span>

<span data-ttu-id="5f312-142">Egyszerű adattípus: Sztring</span><span class="sxs-lookup"><span data-stu-id="5f312-142">Principal Data type: String</span></span>

<span data-ttu-id="5f312-143">Ez a paraméter valósítja meg, hogy a felhasználó megadhatja a hozzáféréshez egy egyedi azonosítható entitást.</span><span class="sxs-lookup"><span data-stu-id="5f312-143">Implement this parameter so that the user can specify a unique identifiable entity for access.</span></span>

<span data-ttu-id="5f312-144">Írja be a jogosultsági adatokat: Sztring</span><span class="sxs-lookup"><span data-stu-id="5f312-144">Privilege Data type: String</span></span>

<span data-ttu-id="5f312-145">Ez a paraméter valósítja meg, hogy a felhasználó megadhatja a jobb oldalon, a parancsmag egy művelettel egy adott entitás van szüksége.</span><span class="sxs-lookup"><span data-stu-id="5f312-145">Implement this parameter so that the user can specify the right a cmdlet needs to perform an operation for a particular entity.</span></span>

<span data-ttu-id="5f312-146">Jogosultságok adattípus: Jogosultságok tömbje</span><span class="sxs-lookup"><span data-stu-id="5f312-146">Privileges Data type: Array of privileges</span></span>

<span data-ttu-id="5f312-147">Ez a paraméter valósítja meg, hogy a felhasználó megadhatja, hogy a parancsmag kell végrehajtani a műveletet egy adott tétel.</span><span class="sxs-lookup"><span data-stu-id="5f312-147">Implement this parameter so that the user can specify the rights that a cmdlet needs to perform its operation for a particular entry.</span></span>

<span data-ttu-id="5f312-148">Szerepkör-adattípus: Sztring</span><span class="sxs-lookup"><span data-stu-id="5f312-148">Role Data type: String</span></span>

<span data-ttu-id="5f312-149">Ez a paraméter valósítja meg, hogy a felhasználó úgy adhat meg az entitás által végrehajtott műveletek készletét.</span><span class="sxs-lookup"><span data-stu-id="5f312-149">Implement this parameter so that the user can specify a set of operations that can be performed by an entity.</span></span>

<span data-ttu-id="5f312-150">SaveCred adattípus: SwitchParameter</span><span class="sxs-lookup"><span data-stu-id="5f312-150">SaveCred Data type: SwitchParameter</span></span>

<span data-ttu-id="5f312-151">Ez a paraméter valósítja meg, hogy a felhasználó által korábban mentett hitelesítő adatok használandó, ha a paraméter meg van adva.</span><span class="sxs-lookup"><span data-stu-id="5f312-151">Implement this parameter so that credentials that were previously saved by the user will be used when the parameter is specified.</span></span>

<span data-ttu-id="5f312-152">Hatókör-adattípus: Sztring</span><span class="sxs-lookup"><span data-stu-id="5f312-152">Scope Data type: String</span></span>

<span data-ttu-id="5f312-153">Ez a paraméter valósítja meg, hogy a felhasználó megadhatja a parancsmag védett objektumok csoportja.</span><span class="sxs-lookup"><span data-stu-id="5f312-153">Implement this parameter so that the user can specify the group of protected objects for the cmdlet.</span></span>

<span data-ttu-id="5f312-154">SID-adattípus: Sztring</span><span class="sxs-lookup"><span data-stu-id="5f312-154">SID Data type: String</span></span>

<span data-ttu-id="5f312-155">Ez a paraméter valósítja meg, hogy a felhasználó úgy adhat meg a rendszerbiztonsági tag képviselő egyedi azonosítója.</span><span class="sxs-lookup"><span data-stu-id="5f312-155">Implement this parameter so that the user can specify a unique identifier that represents a principal.</span></span>

<span data-ttu-id="5f312-156">A megbízható adattípus: SwitchParameter</span><span class="sxs-lookup"><span data-stu-id="5f312-156">Trusted Data type: SwitchParameter</span></span>

<span data-ttu-id="5f312-157">Ez a paraméter valósítja meg, hogy a megbízhatósági szintek támogatottak, ha a paraméter meg van adva.</span><span class="sxs-lookup"><span data-stu-id="5f312-157">Implement this parameter so that trust levels are supported when the parameter is specified.</span></span>

<span data-ttu-id="5f312-158">TrustLevel adattípus: Kulcsszó</span><span class="sxs-lookup"><span data-stu-id="5f312-158">TrustLevel Data type: Keyword</span></span>

<span data-ttu-id="5f312-159">Ez a paraméter valósítja meg, hogy a felhasználó megadhatja a megbízhatósági szint támogatott.</span><span class="sxs-lookup"><span data-stu-id="5f312-159">Implement this parameter so that the user can specify the trust level that is supported.</span></span> <span data-ttu-id="5f312-160">Például lehetséges értékek a következők fulltrust, internetes és intranetes.</span><span class="sxs-lookup"><span data-stu-id="5f312-160">For example, possible values include internet, intranet, and fulltrust.</span></span>

## <a name="see-also"></a><span data-ttu-id="5f312-161">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="5f312-161">See Also</span></span>

[<span data-ttu-id="5f312-162">Parancsmag-paraméterek</span><span class="sxs-lookup"><span data-stu-id="5f312-162">Cmdlet Parameters</span></span>](./cmdlet-parameters.md)

[<span data-ttu-id="5f312-163">Egy Windows PowerShell-parancsmag írása</span><span class="sxs-lookup"><span data-stu-id="5f312-163">Writing a Windows PowerShell Cmdlet</span></span>](./writing-a-windows-powershell-cmdlet.md)

[<span data-ttu-id="5f312-164">Windows PowerShell SDK</span><span class="sxs-lookup"><span data-stu-id="5f312-164">Windows PowerShell SDK</span></span>](../windows-powershell-reference.md)
