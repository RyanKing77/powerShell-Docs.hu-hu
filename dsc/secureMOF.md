---
ms.date: 10/31/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: A MOF-fájl biztonságossá tétele
ms.openlocfilehash: f17c95c951151c0c11057ac0bce172c4ec73c91d
ms.sourcegitcommit: 8b076ebde7ef971d7465bab834a3c2a32471ef6f
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/06/2018
ms.locfileid: "37893263"
---
# <a name="securing-the-mof-file"></a><span data-ttu-id="c1f22-103">A MOF-fájl biztonságossá tétele</span><span class="sxs-lookup"><span data-stu-id="c1f22-103">Securing the MOF File</span></span>

> <span data-ttu-id="c1f22-104">A következőkre vonatkozik: Windows PowerShell 4.0-s, a Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="c1f22-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="c1f22-105">DSC MOF-fájlt, ahol a helyi Configuration Manager (LCM) valósítja meg a kívánt cél állapot tárolt adatokat alkalmazása a konfigurációs kiszolgáló-csomópontok kezeli.</span><span class="sxs-lookup"><span data-stu-id="c1f22-105">DSC manages the configuration of server nodes by applying information stored in a MOF file, where the Local Configuration Manager (LCM) implements the desired end state.</span></span>
<span data-ttu-id="c1f22-106">Ez a fájl tartalmazza a konfigurációs részleteit, mivel fontos tárolja biztonságos helyen.</span><span class="sxs-lookup"><span data-stu-id="c1f22-106">Because this file contains the details of the configuration, it’s important to keep it secure.</span></span>
<span data-ttu-id="c1f22-107">Ez a témakör ismerteti, hogyan ellenőrizhető a célcsomópont a fájl titkosított.</span><span class="sxs-lookup"><span data-stu-id="c1f22-107">This topic describes how to ensure the target node has encrypted the file.</span></span>

<span data-ttu-id="c1f22-108">PowerShell 5.0-s verzió verziótól kezdve a teljes MOF-fájl titkosítva van alapértelmezés szerint a csomópontra történő alkalmazásakor a `Start-DSCConfiguration` parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="c1f22-108">Beginning with PowerShell version 5.0, the entire MOF file is encrypted by default when it is applied to the node using the `Start-DSCConfiguration` cmdlet.</span></span>
<span data-ttu-id="c1f22-109">Ebben a cikkben ismertetett folyamatot kötelező, csak akkor, ha a lekéréses szolgáltatás protokoll használatával, ha a tanúsítványok nem felügyeli, a célcsomópont a letöltött konfigurációk visszafejteni, valamint lépésük előtt olvassa el a rendszer megoldás megvalósítása (például a Windows Server rendszerben elérhető lekéréses szolgáltatás).</span><span class="sxs-lookup"><span data-stu-id="c1f22-109">The process described in this article is required only when implementing a solution using the pull service protocol if certificates are not managed, to ensure configurations downloaded by the target node can be decrypted and read by the system before they are applied (for example, the pull service available in Windows Server).</span></span>
<span data-ttu-id="c1f22-110">Regisztrált csomópontok [Azure Automation DSC](https://docs.microsoft.com/azure/automation/automation-dsc-overview) automatikusan rendelkezik tanúsítványok telepítve van, és nincs adminisztrációs terhelést és a szolgáltatás által kezelt szükséges.</span><span class="sxs-lookup"><span data-stu-id="c1f22-110">Nodes registered to [Azure Automation DSC](https://docs.microsoft.com/azure/automation/automation-dsc-overview) will automatically have certificates installed and managed by the service with no administrative overhead required.</span></span>

> [!NOTE]
> <span data-ttu-id="c1f22-111">Ez a témakör ismerteti a titkosításhoz használt tanúsítvány.</span><span class="sxs-lookup"><span data-stu-id="c1f22-111">This topic discusses certificates used for encryption.</span></span>
> <span data-ttu-id="c1f22-112">A titkosításhoz önaláírt tanúsítvány elegendő, mert a titkos kulcs titkos kulcs és a titkosítás mindig adatért nem jelenti azt, a dokumentum megbízhatósági.</span><span class="sxs-lookup"><span data-stu-id="c1f22-112">For encryption, a self-signed certificate is sufficient, because the private key is always kept secret and encryption does not imply trust of the document.</span></span>
> <span data-ttu-id="c1f22-113">Önaláírt tanúsítványokat kell *nem* hitelesítési célokra használhatók.</span><span class="sxs-lookup"><span data-stu-id="c1f22-113">Self-signed certificates should *not* be used for authentication purposes.</span></span>
> <span data-ttu-id="c1f22-114">Hitelesítési célú tanúsítványt a megbízható hitelesítésszolgáltató (CA) kell használnia.</span><span class="sxs-lookup"><span data-stu-id="c1f22-114">You should use a certificate from a trusted Certification Authority (CA) for any authentication purposes.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c1f22-115">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="c1f22-115">Prerequisites</span></span>

<span data-ttu-id="c1f22-116">Sikerült titkosítani a DSC-konfiguráció védelmére használt hitelesítő adatokat, győződjön meg arról, hogy rendelkezik az alábbiakkal:</span><span class="sxs-lookup"><span data-stu-id="c1f22-116">To successfully encrypt the credentials used to secure a DSC configuration, make sure you have the following:</span></span>

- <span data-ttu-id="c1f22-117">**Néhány azt jelenti, hogy kiállító és tanúsítványok terjesztésére**.</span><span class="sxs-lookup"><span data-stu-id="c1f22-117">**Some means of issuing and distributing certificates**.</span></span> <span data-ttu-id="c1f22-118">Ez a témakör és a példák azt feltételezik, az Active Directory-hitelesítésszolgáltatót használ.</span><span class="sxs-lookup"><span data-stu-id="c1f22-118">This topic and its examples assume you are using Active Directory Certification Authority.</span></span> <span data-ttu-id="c1f22-119">Az Active Directory tanúsítványszolgáltatások további háttér információ: [Active Directory tanúsítványszolgáltatások áttekintése](https://technet.microsoft.com/library/hh831740.aspx) és [Active Directory tanúsítványszolgáltatások a Windows Server 2008](https://technet.microsoft.com/windowsserver/dd448615.aspx).</span><span class="sxs-lookup"><span data-stu-id="c1f22-119">For more background information on Active Directory Certificate Services, see [Active Directory Certificate Services Overview](https://technet.microsoft.com/library/hh831740.aspx) and [Active Directory Certificate Services in Windows Server 2008](https://technet.microsoft.com/windowsserver/dd448615.aspx).</span></span>
- <span data-ttu-id="c1f22-120">**A cél-csomóponthoz vagy csomópontokhoz a rendszergazdai hozzáférést**.</span><span class="sxs-lookup"><span data-stu-id="c1f22-120">**Administrative access to the target node or nodes**.</span></span>
- <span data-ttu-id="c1f22-121">**Minden egyes célcsomóponttal rendelkezik egy titkosítási képességgel tanúsítványt a személyes Store mentett**.</span><span class="sxs-lookup"><span data-stu-id="c1f22-121">**Each target node has an encryption-capable certificate saved its Personal Store**.</span></span> <span data-ttu-id="c1f22-122">A Windows PowerShell a tároló elérési útja a Cert: \LocalMachine\My.</span><span class="sxs-lookup"><span data-stu-id="c1f22-122">In Windows PowerShell, the path to the store is Cert:\LocalMachine\My.</span></span> <span data-ttu-id="c1f22-123">Ebben a témakörben szereplő példák az "munkaállomás-hitelesítési" sablon, amely annak (és más tanúsítványsablonokat) használatát [alapértelmezett tanúsítványsablonokat](https://technet.microsoft.com/library/cc740061(v=WS.10).aspx).</span><span class="sxs-lookup"><span data-stu-id="c1f22-123">The examples in this topic use the “workstation authentication” template, which you can find (along with other certificate templates) at [Default Certificate Templates](https://technet.microsoft.com/library/cc740061(v=WS.10).aspx).</span></span>
- <span data-ttu-id="c1f22-124">Ha fog futni a konfiguráció a célcsomópont webkiszolgálótól eltérő számítógépen található **a tanúsítvány nyilvános kulcsának exportálásához**, majd importálja a számítógépen, a konfigurációt az futtatni fogja.</span><span class="sxs-lookup"><span data-stu-id="c1f22-124">If you will be running this configuration on a computer other than the target node, **export the public key of the certificate**, and then import it to the computer you will run the configuration from.</span></span> <span data-ttu-id="c1f22-125">Győződjön meg arról, hogy exportálja csak a **nyilvános** kulcs; a titkos kulcs biztonságának megőrzése.</span><span class="sxs-lookup"><span data-stu-id="c1f22-125">Make sure that you export only the **public** key; keep the private key secure.</span></span>

## <a name="overall-process"></a><span data-ttu-id="c1f22-126">Általános folyamata</span><span class="sxs-lookup"><span data-stu-id="c1f22-126">Overall process</span></span>

 1. <span data-ttu-id="c1f22-127">Állítsa be a tanúsítványok, kulcsok és ujjlenyomatok, így arról, hogy minden cél csomópont van a tanúsítvány másolatát, és konfigurációs van-e a nyilvános kulcs és ujjlenyomatát.</span><span class="sxs-lookup"><span data-stu-id="c1f22-127">Set up the certificates, keys, and thumbprints, making sure that each target node has copies of the certificate and the configuration computer has the public key and thumbprint.</span></span>
 2. <span data-ttu-id="c1f22-128">Hozzon létre egy konfigurációs adatblokk, amely tartalmazza az elérési út és a nyilvános kulcs ujjlenyomata.</span><span class="sxs-lookup"><span data-stu-id="c1f22-128">Create a configuration data block that contains the path and thumbprint of the public key.</span></span>
 3. <span data-ttu-id="c1f22-129">Hozzon létre egy konfigurációs parancsfájl, amely határozza meg a célcsomópont kívánt konfigurációját, és úgy, mint a helyi konfigurációs visszafejtési a cél-csomópontokon beállít manager visszafejteni a konfigurációs adatokat, a tanúsítvány és az ujjlenyomat használatával.</span><span class="sxs-lookup"><span data-stu-id="c1f22-129">Create a configuration script that defines your desired configuration for the target node and sets up decryption on the target nodes by commanding the Local Configuration manager to decrypt the configuration data using the certificate and its thumbprint.</span></span>
 4. <span data-ttu-id="c1f22-130">Futtassa a konfiguráció, amely a helyi Configuration Manager beállításait, és indítsa el a DSC-konfiguráció.</span><span class="sxs-lookup"><span data-stu-id="c1f22-130">Run the configuration, which will set the Local Configuration Manager settings and start the DSC configuration.</span></span>

![Diagram1](images/CredentialEncryptionDiagram1.png)

## <a name="certificate-requirements"></a><span data-ttu-id="c1f22-132">Tanúsítványkövetelmények</span><span class="sxs-lookup"><span data-stu-id="c1f22-132">Certificate Requirements</span></span>

<span data-ttu-id="c1f22-133">Hitelesítő adatok titkosításához kihirdeti, hogy a nyilvános kulcsú tanúsítvány elérhetőnek kell lennie a _Célcsomóponttal_ , amely **megbízható** a DSC-konfiguráció létrehozásához használja a számítógép által.</span><span class="sxs-lookup"><span data-stu-id="c1f22-133">To enact credential encryption, a public key certificate must be available on the _Target Node_ that is **trusted** by the computer being used to author the DSC configuration.</span></span>
<span data-ttu-id="c1f22-134">A nyilvános kulcsú tanúsítvány ahhoz, hogy a DSC-hitelesítő adatok titkosításához használni meghatározott követelményekkel rendelkezik:</span><span class="sxs-lookup"><span data-stu-id="c1f22-134">This public key certificate has specific requirements for it to be used for DSC credential encryption:</span></span>

1. <span data-ttu-id="c1f22-135">**Kulcshasználat**:</span><span class="sxs-lookup"><span data-stu-id="c1f22-135">**Key Usage**:</span></span>
   - <span data-ttu-id="c1f22-136">Tartalmaznia kell: "KeyEncipherment" és "DataEncipherment".</span><span class="sxs-lookup"><span data-stu-id="c1f22-136">Must contain: 'KeyEncipherment' and 'DataEncipherment'.</span></span>
   - <span data-ttu-id="c1f22-137">Érdemes _nem_ tartalmaz: "A digitális aláírás".</span><span class="sxs-lookup"><span data-stu-id="c1f22-137">Should _not_ contain: 'Digital Signature'.</span></span>
2. <span data-ttu-id="c1f22-138">**Kibővített kulcshasználat**:</span><span class="sxs-lookup"><span data-stu-id="c1f22-138">**Enhanced Key Usage**:</span></span>
   - <span data-ttu-id="c1f22-139">Tartalmaznia kell: dokumentum titkosítása (1.3.6.1.4.1.311.80.1).</span><span class="sxs-lookup"><span data-stu-id="c1f22-139">Must contain: Document Encryption (1.3.6.1.4.1.311.80.1).</span></span>
   - <span data-ttu-id="c1f22-140">Érdemes _nem_ tartalmaznak: ügyfél-hitelesítés (1.3.6.1.5.5.7.3.2) és a kiszolgálói hitelesítés (1.3.6.1.5.5.7.3.1).</span><span class="sxs-lookup"><span data-stu-id="c1f22-140">Should _not_ contain: Client Authentication (1.3.6.1.5.5.7.3.2) and Server Authentication (1.3.6.1.5.5.7.3.1).</span></span>
3. <span data-ttu-id="c1f22-141">A tanúsítvány titkos kulcsa megtalálható a \* cél Node_.</span><span class="sxs-lookup"><span data-stu-id="c1f22-141">The Private Key for the certificate is available on the \*Target Node_.</span></span>
4. <span data-ttu-id="c1f22-142">A **szolgáltató** a tanúsítványt a "Microsoft RSA SChannel Cryptographic Provider" kell lennie.</span><span class="sxs-lookup"><span data-stu-id="c1f22-142">The **Provider** for the certificate must be "Microsoft RSA SChannel Cryptographic Provider".</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c1f22-143">Bár a kulcs használatát "Digitális aláírás" vagy a hitelesítési EKU valamelyik tartalmazó tanúsítványt is használ, ez lehetővé teszi a titkosítási kulcsot hibásan használt és téve a támadás könnyebben törhetők fel.</span><span class="sxs-lookup"><span data-stu-id="c1f22-143">Although you can use a certificate with containing a Key Usage of 'Digital Signature' or one of the Authentication EKU's, this will enable the encryption key to be more easily misused and vulnerable to attack.</span></span> <span data-ttu-id="c1f22-144">Ezért ajánlott ezek kulcshasználat és az EKU-k az áttekinthetőség kedvéért kihagyja kifejezetten a DSC-hitelesítő adatok védelme céljából létrehozott tanúsítványt használjon.</span><span class="sxs-lookup"><span data-stu-id="c1f22-144">So it is best practice to use a certificate created specifically for the purpose of securing DSC credentials that omits these Key Usage and EKUs.</span></span>

<span data-ttu-id="c1f22-145">Minden meglévő tanúsítványt a _Célcsomóponttal_ , hogy megfelel-e ezek a feltételek segítségével biztonságos DSC hitelesítő adatokat.</span><span class="sxs-lookup"><span data-stu-id="c1f22-145">Any existing certificate on the _Target Node_ that meets these criteria can be used to secure DSC credentials.</span></span>

## <a name="certificate-creation"></a><span data-ttu-id="c1f22-146">Tanúsítvány létrehozása</span><span class="sxs-lookup"><span data-stu-id="c1f22-146">Certificate creation</span></span>

<span data-ttu-id="c1f22-147">Kétféleképpen hozhat létre és használhat a szükséges titkosítási tanúsítvány (nyilvános-titkos kulcspárt) is igénybe vehet.</span><span class="sxs-lookup"><span data-stu-id="c1f22-147">There are two approaches you can take to create and use the required Encryption Certificate (public-private key pair).</span></span>

1. <span data-ttu-id="c1f22-148">Hozza létre a **Célcsomóponttal** , és csak a nyilvános kulcsának exportálásához a **szerzői csomópont**</span><span class="sxs-lookup"><span data-stu-id="c1f22-148">Create it on the **Target Node** and export just the public key to the **Authoring Node**</span></span>
2. <span data-ttu-id="c1f22-149">Hozza létre a **szerzői csomópont** és a teljes kulcspár, exportálhatja a **Célcsomóponttal**</span><span class="sxs-lookup"><span data-stu-id="c1f22-149">Create it on the **Authoring Node** and export the entire key pair to the **Target Node**</span></span>

<span data-ttu-id="c1f22-150">1. módszer használata javasolt, mert mindig célcsomóponton marad a titkos kulcs használatával fejti vissza az MOF hitelesítő adatait.</span><span class="sxs-lookup"><span data-stu-id="c1f22-150">Method 1 is recommended because the private key used to decrypt credentials in the MOF stays on the Target Node at all times.</span></span>

### <a name="creating-the-certificate-on-the-target-node"></a><span data-ttu-id="c1f22-151">A tanúsítvány létrehozásakor a célcsomóponton</span><span class="sxs-lookup"><span data-stu-id="c1f22-151">Creating the Certificate on the Target Node</span></span>

<span data-ttu-id="c1f22-152">A titkos kulcs titkos, mert fejti vissza az MOF meg kell tartani a **Célcsomóponttal** ennek legegyszerűbb módja az, hogy a titkos kulcsú tanúsítvány létrehozása a a **Célcsomóponttal**, és másolja a  **nyilvános kulcsú tanúsítvány** a MOF-fájlba a DSC-konfiguráció létrehozásához használt számítógépre.</span><span class="sxs-lookup"><span data-stu-id="c1f22-152">The private key must be kept secret, because is used to decrypt the MOF on the **Target Node** The easiest way to do that is to create the private key certificate on the **Target Node**, and copy the **public key certificate** to the computer being used to author the DSC configuration into a MOF file.</span></span>
<span data-ttu-id="c1f22-153">Az alábbi példában:</span><span class="sxs-lookup"><span data-stu-id="c1f22-153">The following example:</span></span>

1. <span data-ttu-id="c1f22-154">a tanúsítványt hoz létre a **célcsomóponttal**</span><span class="sxs-lookup"><span data-stu-id="c1f22-154">creates a certificate on the **Target node**</span></span>
2. <span data-ttu-id="c1f22-155">a nyilvános kulcsú tanúsítvány exportálása a **célcsomóponttal**.</span><span class="sxs-lookup"><span data-stu-id="c1f22-155">exports the public key certificate on the **Target node**.</span></span>
3. <span data-ttu-id="c1f22-156">a nyilvános kulcsú tanúsítványt importál a **saját** tanúsítványtárolójába a **szerzői műveletek csomópont**.</span><span class="sxs-lookup"><span data-stu-id="c1f22-156">imports the public key certificate into the **my** certificate store on the **Authoring node**.</span></span>

#### <a name="on-the-target-node-create-and-export-the-certificate"></a><span data-ttu-id="c1f22-157">A cél csomóponton: hozzon létre, és exportálja a tanúsítványt</span><span class="sxs-lookup"><span data-stu-id="c1f22-157">On the Target Node: create and export the certificate</span></span>

> <span data-ttu-id="c1f22-158">Célcsomópont: Windows Server 2016 és Windows 10-es</span><span class="sxs-lookup"><span data-stu-id="c1f22-158">Target Node: Windows Server 2016 and Windows 10</span></span>

```powershell
# note: These steps need to be performed in an Administrator PowerShell session
$cert = New-SelfSignedCertificate -Type DocumentEncryptionCertLegacyCsp -DnsName 'DscEncryptionCert' -HashAlgorithm SHA256
# export the public key certificate
$cert | Export-Certificate -FilePath "$env:temp\DscPublicKey.cer" -Force
```

<span data-ttu-id="c1f22-159">Az exportált egyszer, a `DscPublicKey.cer` kellene kell másolni a **szerzői csomópont**.</span><span class="sxs-lookup"><span data-stu-id="c1f22-159">Once exported, the `DscPublicKey.cer` would need to be copied to the **Authoring Node**.</span></span>

> <span data-ttu-id="c1f22-160">Célcsomópont: Windows Server 2012 R2 vagy Windows 8.1 és korábbi</span><span class="sxs-lookup"><span data-stu-id="c1f22-160">Target Node: Windows Server 2012 R2/Windows 8.1 and earlier</span></span>
> [!WARNING]
> <span data-ttu-id="c1f22-161">Mivel a `New-SelfSignedCertificate` nem támogatják a parancsmag a Windows operációs rendszerek a Windows 10 és Windows Server 2016 előtt a **típus** paraméter, ez a tanúsítvány létrehozása egy alternatív módszer megadása szükséges. az említett operációs rendszerektől.</span><span class="sxs-lookup"><span data-stu-id="c1f22-161">Because the `New-SelfSignedCertificate` cmdlet on Windows Operating Systems prior to Windows 10 and Windows Server 2016 do not support the **Type** parameter, an alternate method of creating this certificate is required on these operating systems.</span></span>
>
> <span data-ttu-id="c1f22-162">Ebben az esetben használhatja `makecert.exe` vagy `certutil.exe` a tanúsítvány létrehozásához.</span><span class="sxs-lookup"><span data-stu-id="c1f22-162">In this case you can use `makecert.exe` or `certutil.exe` to create the certificate.</span></span>
>
><span data-ttu-id="c1f22-163">Egy alternatív módszer [a New-SelfSignedCertificateEx.ps1 szkript letöltése a Microsoft Script Center](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6) , és ezzel hozzon létre helyette a tanúsítványt:</span><span class="sxs-lookup"><span data-stu-id="c1f22-163">An alternate method is to [download the New-SelfSignedCertificateEx.ps1 script from Microsoft Script Center](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6) and use it to create the certificate instead:</span></span>

```powershell
# note: These steps need to be performed in an Administrator PowerShell session
# and in the folder that contains New-SelfSignedCertificateEx.ps1
. .\New-SelfSignedCertificateEx.ps1
New-SelfsignedCertificateEx `
    -Subject "CN=${ENV:ComputerName}" `
    -EKU 'Document Encryption' `
    -KeyUsage 'KeyEncipherment, DataEncipherment' `
    -SAN ${ENV:ComputerName} `
    -FriendlyName 'DSC Credential Encryption certificate' `
    -Exportable `
    -StoreLocation 'LocalMachine' `
    -KeyLength 2048 `
    -ProviderName 'Microsoft Enhanced Cryptographic Provider v1.0' `
    -AlgorithmName 'RSA' `
    -SignatureAlgorithm 'SHA256'
# Locate the newly created certificate
$Cert = Get-ChildItem -Path cert:\LocalMachine\My | Where-Object {
        ($_.FriendlyName -eq 'DSC Credential Encryption certificate') -and ($_.Subject -eq "CN=${ENV:ComputerName}")
    } | Select-Object -First 1
# export the public key certificate
$cert | Export-Certificate -FilePath "$env:temp\DscPublicKey.cer" -Force
```

<span data-ttu-id="c1f22-164">Az exportált egyszer, a ```DscPublicKey.cer``` kellene kell másolni a **szerzői csomópont**.</span><span class="sxs-lookup"><span data-stu-id="c1f22-164">Once exported, the ```DscPublicKey.cer``` would need to be copied to the **Authoring Node**.</span></span>

#### <a name="on-the-authoring-node-import-the-certs-public-key"></a><span data-ttu-id="c1f22-165">A szerzői műveletek csomóponton: importálja a tanúsítvány nyilvános kulcsa</span><span class="sxs-lookup"><span data-stu-id="c1f22-165">On the Authoring Node: import the cert’s public key</span></span>

```powershell
# Import to the my store
Import-Certificate -FilePath "$env:temp\DscPublicKey.cer" -CertStoreLocation Cert:\LocalMachine\My
```

### <a name="creating-the-certificate-on-the-authoring-node"></a><span data-ttu-id="c1f22-166">A tanúsítvány létrehozása az Authoring Tool csomóponton</span><span class="sxs-lookup"><span data-stu-id="c1f22-166">Creating the Certificate on the Authoring Node</span></span>

<span data-ttu-id="c1f22-167">Azt is megteheti, a titkosítási tanúsítvány hozható létre a a **szerzői csomópont**, az exportált a **titkos kulcs** , egy PFX fájlt, és ezután importálja, amelyen a **Célcsomóponttal**.</span><span class="sxs-lookup"><span data-stu-id="c1f22-167">Alternately, the encryption certificate can be created on the **Authoring Node**, exported with the **private key** as a PFX file and then imported on the **Target Node**.</span></span>
<span data-ttu-id="c1f22-168">Ez a végrehajtási DSC hitelesítő adatok titkosításához az aktuális mód _Nano Server_.</span><span class="sxs-lookup"><span data-stu-id="c1f22-168">This is the current method for implementing DSC credential encryption on _Nano Server_.</span></span>
<span data-ttu-id="c1f22-169">Bár a PFX-jelszó védi, meg kell őrizni biztonságos átvitel során.</span><span class="sxs-lookup"><span data-stu-id="c1f22-169">Although the PFX is secured with a password it should be kept secure during transit.</span></span>
<span data-ttu-id="c1f22-170">Az alábbi példában:</span><span class="sxs-lookup"><span data-stu-id="c1f22-170">The following example:</span></span>

1. <span data-ttu-id="c1f22-171">a tanúsítványt hoz létre a **szerzői műveletek csomópont**.</span><span class="sxs-lookup"><span data-stu-id="c1f22-171">creates a certificate on the **Authoring node**.</span></span>
2. <span data-ttu-id="c1f22-172">exportálja a tanúsítványt a titkos kulcs is a **szerzői műveletek csomópont**.</span><span class="sxs-lookup"><span data-stu-id="c1f22-172">exports the certificate including the private key on the **Authoring node**.</span></span>
3. <span data-ttu-id="c1f22-173">eltávolítja a titkos kulcsot a a **szerzői műveletek csomópont**, de megőrzi a nyilvános kulcsú tanúsítvány a **saját** tárolásához.</span><span class="sxs-lookup"><span data-stu-id="c1f22-173">removes the private key from the **Authoring node**, but keeps the public key certificate in the **my** store.</span></span>
4. <span data-ttu-id="c1f22-174">importálja a titkos kulcsú tanúsítványt a My(Personal) tanúsítványtárolójába a a **célcsomóponttal**.</span><span class="sxs-lookup"><span data-stu-id="c1f22-174">imports the private key certificate into the My(Personal) certificate store on the **Target node**.</span></span>
   - <span data-ttu-id="c1f22-175">azt hozzá kell adni a legfelső szintű tárolójában, hogy a rendszer megbízható a **célcsomóponttal**.</span><span class="sxs-lookup"><span data-stu-id="c1f22-175">it must be added to the root store so that it will be trusted by the **Target node**.</span></span>

#### <a name="on-the-authoring-node-create-and-export-the-certificate"></a><span data-ttu-id="c1f22-176">A szerzői műveletek csomóponton: hozzon létre, és exportálja a tanúsítványt</span><span class="sxs-lookup"><span data-stu-id="c1f22-176">On the Authoring Node: create and export the certificate</span></span>

> <span data-ttu-id="c1f22-177">Célcsomópont: Windows Server 2016 és Windows 10-es</span><span class="sxs-lookup"><span data-stu-id="c1f22-177">Target Node: Windows Server 2016 and Windows 10</span></span>

```powershell
# note: These steps need to be performed in an Administrator PowerShell session
$cert = New-SelfSignedCertificate -Type DocumentEncryptionCertLegacyCsp -DnsName 'DscEncryptionCert' -HashAlgorithm SHA256
# export the private key certificate
$mypwd = ConvertTo-SecureString -String "YOUR_PFX_PASSWD" -Force -AsPlainText
$cert | Export-PfxCertificate -FilePath "$env:temp\DscPrivateKey.pfx" -Password $mypwd -Force
# remove the private key certificate from the node but keep the public key certificate
$cert | Export-Certificate -FilePath "$env:temp\DscPublicKey.cer" -Force
$cert | Remove-Item -Force
Import-Certificate -FilePath "$env:temp\DscPublicKey.cer" -CertStoreLocation Cert:\LocalMachine\My
```

<span data-ttu-id="c1f22-178">Az exportált egyszer, a `DscPrivateKey.pfx` kell átmásolni a **Célcsomóponttal**.</span><span class="sxs-lookup"><span data-stu-id="c1f22-178">Once exported, the `DscPrivateKey.pfx` would need to be copied to the **Target Node**.</span></span>

> <span data-ttu-id="c1f22-179">Célcsomópont: Windows Server 2012 R2 vagy Windows 8.1 és korábbi</span><span class="sxs-lookup"><span data-stu-id="c1f22-179">Target Node: Windows Server 2012 R2/Windows 8.1 and earlier</span></span>
> [!WARNING]
> <span data-ttu-id="c1f22-180">Mivel a `New-SelfSignedCertificate` nem támogatják a parancsmag a Windows operációs rendszerek a Windows 10 és Windows Server 2016 előtt a **típus** paraméter, ez a tanúsítvány létrehozása egy alternatív módszer megadása szükséges. az említett operációs rendszerektől.</span><span class="sxs-lookup"><span data-stu-id="c1f22-180">Because the `New-SelfSignedCertificate` cmdlet on Windows Operating Systems prior to Windows 10 and Windows Server 2016 do not support the **Type** parameter, an alternate method of creating this certificate is required on these operating systems.</span></span>
>
> <span data-ttu-id="c1f22-181">Ebben az esetben használhatja `makecert.exe` vagy `certutil.exe` a tanúsítvány létrehozásához.</span><span class="sxs-lookup"><span data-stu-id="c1f22-181">In this case you can use `makecert.exe` or `certutil.exe` to create the certificate.</span></span>
>
> <span data-ttu-id="c1f22-182">Egy alternatív módszer [a New-SelfSignedCertificateEx.ps1 szkript letöltése a Microsoft Script Center](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6) , és ezzel hozzon létre helyette a tanúsítványt:</span><span class="sxs-lookup"><span data-stu-id="c1f22-182">An alternate method is to [download the New-SelfSignedCertificateEx.ps1 script from Microsoft Script Center](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6) and use it to create the certificate instead:</span></span>

```powershell
# note: These steps need to be performed in an Administrator PowerShell session
# and in the folder that contains New-SelfSignedCertificateEx.ps1
. .\New-SelfSignedCertificateEx.ps1
New-SelfsignedCertificateEx `
    -Subject "CN=${ENV:ComputerName}" `
    -EKU 'Document Encryption' `
    -KeyUsage 'KeyEncipherment, DataEncipherment' `
    -SAN ${ENV:ComputerName} `
    -FriendlyName 'DSC Credential Encryption certificate' `
    -Exportable `
    -StoreLocation 'LocalMachine' `
    -KeyLength 2048 `
    -ProviderName 'Microsoft Enhanced Cryptographic Provider v1.0' `
    -AlgorithmName 'RSA' `
    -SignatureAlgorithm 'SHA256'
# Locate the newly created certificate
$Cert = Get-ChildItem -Path cert:\LocalMachine\My | Where-Object {
        ($_.FriendlyName -eq 'DSC Credential Encryption certificate') -and ($_.Subject -eq "CN=${ENV:ComputerName}")
    } | Select-Object -First 1
# export the public key certificate
$mypwd = ConvertTo-SecureString -String "YOUR_PFX_PASSWD" -Force -AsPlainText
$cert | Export-PfxCertificate -FilePath "$env:temp\DscPrivateKey.pfx" -Password $mypwd -Force
# remove the private key certificate from the node but keep the public key certificate
$cert | Export-Certificate -FilePath "$env:temp\DscPublicKey.cer" -Force
$cert | Remove-Item -Force
Import-Certificate -FilePath "$env:temp\DscPublicKey.cer" -CertStoreLocation Cert:\LocalMachine\My
```

#### <a name="on-the-target-node-import-the-certs-private-key-as-a-trusted-root"></a><span data-ttu-id="c1f22-183">A cél csomóponton: importálja a tanúsítványt a titkos kulcsot a megbízható legfelső szintű</span><span class="sxs-lookup"><span data-stu-id="c1f22-183">On the Target Node: import the cert’s private key as a trusted root</span></span>

```powershell
# Import to the root store so that it is trusted
$mypwd = ConvertTo-SecureString -String "YOUR_PFX_PASSWD" -Force -AsPlainText
Import-PfxCertificate -FilePath "$env:temp\DscPrivateKey.pfx" -CertStoreLocation Cert:\LocalMachine\My -Password $mypwd > $null
```

## <a name="configuration-data"></a><span data-ttu-id="c1f22-184">Konfigurációs adatok</span><span class="sxs-lookup"><span data-stu-id="c1f22-184">Configuration data</span></span>

<span data-ttu-id="c1f22-185">A konfigurációs adatok blokk határozza meg, melyik célcsomópontok alapján, hogy e, vagy nem a hitelesítő adatokat, az azt jelenti, hogy a titkosítás és egyéb információk titkosítására.</span><span class="sxs-lookup"><span data-stu-id="c1f22-185">The configuration data block defines which target nodes to operate on, whether or not to encrypt the credentials, the means of encryption, and other information.</span></span> <span data-ttu-id="c1f22-186">A konfigurációs adatok blokk további információkért lásd: [szétválasztása konfigurációs és környezeti adatok](configData.md).</span><span class="sxs-lookup"><span data-stu-id="c1f22-186">For more information on the configuration data block, see [Separating Configuration and Environment Data](configData.md).</span></span>

<span data-ttu-id="c1f22-187">Hitelesítőadat-titkosítás kapcsolatos, az egyes csomópontok konfigurálható elemek a következők:</span><span class="sxs-lookup"><span data-stu-id="c1f22-187">The elements that can be configured for each node that are related to credential encryption are:</span></span>

- <span data-ttu-id="c1f22-188">**NodeName** – a célcsomópont a hitelesítő adatok titkosításához a konfigurálni kívánt nevét.</span><span class="sxs-lookup"><span data-stu-id="c1f22-188">**NodeName** - the name of the target node that the credential encryption is being configured for.</span></span>
- <span data-ttu-id="c1f22-189">**PsDscAllowPlainTextPassword** - e a titkosítatlan hitelesítő adatok adható át ezen a csomóponton engedélyezni.</span><span class="sxs-lookup"><span data-stu-id="c1f22-189">**PsDscAllowPlainTextPassword** - whether unencrypted credentials will be allowed to be passed to this node.</span></span> <span data-ttu-id="c1f22-190">Ez a **nem ajánlott**.</span><span class="sxs-lookup"><span data-stu-id="c1f22-190">This is **not recommended**.</span></span>
- <span data-ttu-id="c1f22-191">**Ujjlenyomat** -a a DSC-konfiguráció a hitelesítő adatok visszafejtése a használt tanúsítvány ujjlenyomatát a _Célcsomóponttal_.</span><span class="sxs-lookup"><span data-stu-id="c1f22-191">**Thumbprint** - the thumbprint of the certificate that will be used to decrypt the credentials in the DSC Configuration on the _Target Node_.</span></span> <span data-ttu-id="c1f22-192">**Ezt a tanúsítványt a helyi számítógép tanúsítványtárolójába a léteznie kell.**</span><span class="sxs-lookup"><span data-stu-id="c1f22-192">**This certificate must exist in the Local Machine certificate store on the Target Node.**</span></span>
- <span data-ttu-id="c1f22-193">**CertificateFile** – a tanúsítványfájlt (csak a nyilvános kulcsot tartalmazó), amely a hitelesítő adatok titkosításához használandó a _Célcsomóponttal_.</span><span class="sxs-lookup"><span data-stu-id="c1f22-193">**CertificateFile** - the certificate file (containing the public key only) that should be used to encrypt the credentials for the _Target Node_.</span></span> <span data-ttu-id="c1f22-194">Ez lehet akár egy DER kódolású bináris X.509 vagy Base-64 kódolású X.509 formátumú tanúsítványfájlt.</span><span class="sxs-lookup"><span data-stu-id="c1f22-194">This must be either a DER encoded binary X.509 or Base-64 encoded X.509 format certificate file.</span></span>

<span data-ttu-id="c1f22-195">Ez a példa bemutatja egy konfigurációs adatblokk, amely meghatározza egy célcsomóponttal való működésre az elnevezett targetNode, a nyilvános kulcsú tanúsítványfájlra (nevű targetNode.cer), és az ujjlenyomatot a nyilvános kulcs elérési útját.</span><span class="sxs-lookup"><span data-stu-id="c1f22-195">This example shows a configuration data block that specifies a target node to act on named targetNode, the path to the public key certificate file (named targetNode.cer), and the thumbprint for the public key.</span></span>

```powershell
$ConfigData= @{
    AllNodes = @(
            @{
                # The name of the node we are describing
                NodeName = "targetNode"

                # The path to the .cer file containing the
                # public key of the Encryption Certificate
                # used to encrypt credentials for this node
                CertificateFile = "C:\publicKeys\targetNode.cer"


                # The thumbprint of the Encryption Certificate
                # used to decrypt the credentials on target node
                Thumbprint = "AC23EA3A9E291A75757A556D0B71CBBF8C4F6FD8"
            };
        );
    }
```

## <a name="configuration-script"></a><span data-ttu-id="c1f22-196">Konfigurációs parancsfájl</span><span class="sxs-lookup"><span data-stu-id="c1f22-196">Configuration script</span></span>

<span data-ttu-id="c1f22-197">Magát a konfigurációs parancsfájlt, használja a `PsCredential` paraméter segítségével győződjön meg arról, hogy a lehető legrövidebb idő alatt a hitelesítő adatokat tárolja.</span><span class="sxs-lookup"><span data-stu-id="c1f22-197">In the configuration script itself, use the `PsCredential` parameter to ensure that credentials are stored for the shortest possible time.</span></span> <span data-ttu-id="c1f22-198">A megadott példa futtatásakor DSC kéri a hitelesítő adatokat, és majd titkosíthatja a MOF-fájlt a CertificateFile társított a célcsomópont a konfigurációs adatok blokk használatával.</span><span class="sxs-lookup"><span data-stu-id="c1f22-198">When you run the supplied example, DSC will prompt you for credentials and then encrypt the MOF file using the CertificateFile that is associated with the target node in the configuration data block.</span></span> <span data-ttu-id="c1f22-199">Ez a Kódpélda másol egy fájlt egy felhasználó védett megosztásból.</span><span class="sxs-lookup"><span data-stu-id="c1f22-199">This code example copies a file from a share that is secured to a user.</span></span>

```powershell
configuration CredentialEncryptionExample
{
    param(
        [Parameter(Mandatory=$true)]
        [ValidateNotNullorEmpty()]
        [PsCredential] $credential
        )


    Node $AllNodes.NodeName
    {
        File exampleFile
        {
            SourcePath = "\\Server\share\path\file.ext"
            DestinationPath = "C:\destinationPath"
            Credential = $credential
        }
    }
}
```

## <a name="setting-up-decryption"></a><span data-ttu-id="c1f22-200">A visszafejtés beállítása</span><span class="sxs-lookup"><span data-stu-id="c1f22-200">Setting up decryption</span></span>

<span data-ttu-id="c1f22-201">Mielőtt [ `Start-DscConfiguration` ](https://technet.microsoft.com/library/dn521623.aspx) is működik, meg kell mondanunk a helyi Configuration Manager a cél-csomópontokon melyik tanúsítványt használja a hitelesítő adatok visszafejtése a CertificateID erőforrás segítségével ellenőrizze a tanúsítvány ujjlenyomata.</span><span class="sxs-lookup"><span data-stu-id="c1f22-201">Before [`Start-DscConfiguration`](https://technet.microsoft.com/library/dn521623.aspx) can work, you have to tell the Local Configuration Manager on each target node which certificate to use to decrypt the credentials, using the CertificateID resource to verify the certificate’s thumbprint.</span></span> <span data-ttu-id="c1f22-202">Ez a példa a függvény megkeresi a megfelelő helyi tanúsítvány (szükség lehet testre szabni, így megtalálja a pontos tanúsítványt használni kívánt):</span><span class="sxs-lookup"><span data-stu-id="c1f22-202">This example function will find the appropriate local certificate (you might have to customize it so it will find the exact certificate you want to use):</span></span>

```powershell
# Get the certificate that works for encryption
function Get-LocalEncryptionCertificateThumbprint
{
    (dir Cert:\LocalMachine\my) | %{
        # Verify the certificate is for Encryption and valid
        if ($_.PrivateKey.KeyExchangeAlgorithm -and $_.Verify())
        {
            return $_.Thumbprint
        }
    }
}
```

<span data-ttu-id="c1f22-203">Az ujjlenyomat által azonosított tanúsítvánnyal a konfigurációs parancsfájl frissíthető értéket használja:</span><span class="sxs-lookup"><span data-stu-id="c1f22-203">With the certificate identified by its thumbprint, the configuration script can be updated to use the value:</span></span>

```powershell
configuration CredentialEncryptionExample
{
    param(
        [Parameter(Mandatory=$true)]
        [ValidateNotNullorEmpty()]
        [PsCredential] $credential
        )


    Node $AllNodes.NodeName
    {
        File exampleFile
        {
            SourcePath = "\\Server\share\path\file.ext"
            DestinationPath = "C:\destinationPath"
            Credential = $credential
        }

        LocalConfigurationManager
        {
             CertificateId = $node.Thumbprint
        }
    }
}
```

## <a name="running-the-configuration"></a><span data-ttu-id="c1f22-204">A konfiguráció futtatása</span><span class="sxs-lookup"><span data-stu-id="c1f22-204">Running the configuration</span></span>

<span data-ttu-id="c1f22-205">Ezen a ponton a konfigurációt, mivel a két fájlt kimenete futtathatja:</span><span class="sxs-lookup"><span data-stu-id="c1f22-205">At this point, you can run the configuration, which will output two files:</span></span>

- <span data-ttu-id="c1f22-206">A \*. meta.mof fájlt, amely a hitelesítő adatok használatával, amely a helyi számítógép tárolóban tárolja, és azonosítja az ujjlenyomata a tanúsítvány visszafejtése a Local Configuration Manager konfigurálja.</span><span class="sxs-lookup"><span data-stu-id="c1f22-206">A \*.meta.mof file that configures the Local Configuration Manager to decrypt the credentials using the certificate that is stored on the local machine store and identified by its thumbprint.</span></span> <span data-ttu-id="c1f22-207">[`Set-DscLocalConfigurationManager`](https://technet.microsoft.com/library/dn521621.aspx) alkalmazza a \*. meta.mof fájlt.</span><span class="sxs-lookup"><span data-stu-id="c1f22-207">[`Set-DscLocalConfigurationManager`](https://technet.microsoft.com/library/dn521621.aspx) applies the \*.meta.mof file.</span></span>
- <span data-ttu-id="c1f22-208">MOF-fájlt, amely ténylegesen konfigurációjának alkalmazására szolgál.</span><span class="sxs-lookup"><span data-stu-id="c1f22-208">A MOF file that actually applies the configuration.</span></span> <span data-ttu-id="c1f22-209">Start-DscConfiguration konfigurációjának alkalmazására szolgál.</span><span class="sxs-lookup"><span data-stu-id="c1f22-209">Start-DscConfiguration applies the configuration.</span></span>

<span data-ttu-id="c1f22-210">Ezek a parancsok érnek el ezeket a lépéseket:</span><span class="sxs-lookup"><span data-stu-id="c1f22-210">These commands will accomplish those steps:</span></span>

```powershell
Write-Host "Generate DSC Configuration..."
CredentialEncryptionExample -ConfigurationData $ConfigData -OutputPath .\CredentialEncryptionExample

Write-Host "Setting up LCM to decrypt credentials..."
Set-DscLocalConfigurationManager .\CredentialEncryptionExample -Verbose

Write-Host "Starting Configuration..."
Start-DscConfiguration .\CredentialEncryptionExample -wait -Verbose
```

<span data-ttu-id="c1f22-211">Ebben a példában a DSC-konfiguráció miatt a cél csomópontra.</span><span class="sxs-lookup"><span data-stu-id="c1f22-211">This example would push the DSC configuration to the target node.</span></span>
<span data-ttu-id="c1f22-212">A DSC-konfiguráció használata a DSC lekéréses kiszolgálón, ha elérhető is alkalmazható.</span><span class="sxs-lookup"><span data-stu-id="c1f22-212">The DSC configuration can also be applied using a DSC Pull Server if one is available.</span></span>

<span data-ttu-id="c1f22-213">Lásd: [DSC lekérési ügyfél beállítása](pullClient.md) további információt a DSC-konfigurációk DSC lekéréses kiszolgálót használ.</span><span class="sxs-lookup"><span data-stu-id="c1f22-213">See [Setting up a DSC pull client](pullClient.md) for more information on applying DSC configurations using a DSC Pull Server.</span></span>

## <a name="credential-encryption-module-example"></a><span data-ttu-id="c1f22-214">Hitelesítő adatok titkosítási modul példa</span><span class="sxs-lookup"><span data-stu-id="c1f22-214">Credential Encryption Module Example</span></span>

<span data-ttu-id="c1f22-215">Íme egy teljes példa, amely tartalmazza a teljes ezeket a lépéseket, valamint egy segítő parancsmag, amely exportálja, és másolja a nyilvános kulcsokat:</span><span class="sxs-lookup"><span data-stu-id="c1f22-215">Here is a full example that incorporates all of these steps, plus a helper cmdlet that exports and copies the public keys:</span></span>

```powershell
# A simple example of using credentials
configuration CredentialEncryptionExample
{
    param(
        [Parameter(Mandatory=$true)]
        [ValidateNotNullorEmpty()]
        [PsCredential] $credential
        )


    Node $AllNodes.NodeName
    {
        File exampleFile
        {
            SourcePath = "\\server\share\file.txt"
            DestinationPath = "C:\Users\user"
            Credential = $credential
        }

        LocalConfigurationManager
        {
            CertificateId = $node.Thumbprint
        }
    }
}

# A Helper to invoke the configuration, with the correct public key
# To encrypt the configuration credentials
function Start-CredentialEncryptionExample
{
    [CmdletBinding()]
    param ($computerName)


    [string] $thumbprint = Get-EncryptionCertificate -computerName $computerName -Verbose
    Write-Verbose "using cert: $thumbprint"

    $certificatePath = join-path -Path "$env:SystemDrive\$script:publicKeyFolder" -childPath "$computername.EncryptionCertificate.cer"

    $ConfigData=    @{
        AllNodes = @(
                        @{
                            # The name of the node we are describing
                            NodeName = "$computerName"

                            # The path to the .cer file containing the
                            # public key of the Encryption Certificate
                            CertificateFile = "$certificatePath"

                            # The thumbprint of the Encryption Certificate
                            # used to decrypt the credentials
                            Thumbprint = $thumbprint
                        };
                    );
    }

    Write-Verbose "Generate DSC Configuration..."
    CredentialEncryptionExample -ConfigurationData $ConfigData -OutputPath .\CredentialEncryptionExample `
        -credential (Get-Credential -UserName "$env:USERDOMAIN\$env:USERNAME" -Message "Enter credentials for configuration")

    Write-Verbose "Setting up LCM to decrypt credentials..."
    Set-DscLocalConfigurationManager .\CredentialEncryptionExample -Verbose

    Write-Verbose "Starting Configuration..."
    Start-DscConfiguration .\CredentialEncryptionExample -wait -Verbose

}


#region HelperFunctions

# The folder name for the exported public keys
$script:publicKeyFolder = "publicKeys"

# Get the certificate that works for encryptions
function Get-EncryptionCertificate
{
    [CmdletBinding()]
    param ($computerName)
    $returnValue= Invoke-Command -ComputerName $computerName -ScriptBlock {
            $certificates = dir Cert:\LocalMachine\my

            $certificates | %{
                    # Verify the certificate is for Encryption and valid
                    if ($_.PrivateKey.KeyExchangeAlgorithm -and $_.Verify())
                    {
                        # Create the folder to hold the exported public key
                        $folder= Join-Path -Path $env:SystemDrive\ -ChildPath $using:publicKeyFolder
                        if (! (Test-Path $folder))
                        {
                            md $folder | Out-Null
                        }

                        # Export the public key to a well known location
                        $certPath = Export-Certificate -Cert $_ -FilePath (Join-Path -path $folder -childPath "EncryptionCertificate.cer")

                        # Return the thumbprint, and exported certificate path
                        return @($_.Thumbprint,$certPath);
                    }
                  }
        }
    Write-Verbose "Identified and exported cert..."
    # Copy the exported certificate locally
    $destinationPath = join-path -Path "$env:SystemDrive\$script:publicKeyFolder" -childPath "$computername.EncryptionCertificate.cer"
    Copy-Item -Path (join-path -path \\$computername -childPath $returnValue[1].FullName.Replace(":","$"))  $destinationPath | Out-Null

    # Return the thumbprint
    return $returnValue[0]
}

Start-CredentialEncryptionExample
```