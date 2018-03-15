---
ms.date: 2017-10-31
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "A MOF-fájl védelme"
ms.openlocfilehash: 1bb257f3237344f32c9035f3836dd317b75eef0a
ms.sourcegitcommit: 99227f62dcf827354770eb2c3e95c5cf6a3118b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/15/2018
---
# <a name="securing-the-mof-file"></a><span data-ttu-id="6dcdd-103">A MOF-fájl védelme</span><span class="sxs-lookup"><span data-stu-id="6dcdd-103">Securing the MOF File</span></span>

><span data-ttu-id="6dcdd-104">Vonatkozik: A Windows PowerShell 4.0-s verzióját, a Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="6dcdd-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="6dcdd-105">A DSC csomópontok konfigurációját úgy, hogy alkalmazza a MOF-fájlt, ahol a helyi Configuration Manager (LCM) valósítja meg a kívánt cél állapot tárolt információk kezeli.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-105">DSC manages the configuration of server nodes by applying information stored in a MOF file, where the Local Configuration Manager (LCM) implements the desired end state.</span></span>
<span data-ttu-id="6dcdd-106">Ez a fájl tartalmazza a konfiguráció részletes adatait, mert fontos biztonságának megőrzése.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-106">Because this file contains the details of the configuration, it’s important to keep it secure.</span></span>
<span data-ttu-id="6dcdd-107">Ez a témakör ismerteti a célcsomópont a fájl van titkosítva.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-107">This topic describes how to ensure the target node has encrypted the file.</span></span>

<span data-ttu-id="6dcdd-108">PowerShell 5.0-s verziójának kezdve a teljes MOF-fájl titkosítva van alapértelmezés szerint a csomópont történő alkalmazásakor a **Start-DSCConfiguration** parancsmag.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-108">Beginning with PowerShell version 5.0, the entire MOF file is encrypted by default when it is applied to the node using the **Start-DSCConfiguration** cmdlet.</span></span>
<span data-ttu-id="6dcdd-109">A cikkben leírt eljárás esetén szükséges csak egy megoldás, ha a tanúsítványok nem kezelt, annak érdekében, tölti le a célcsomópont konfigurációk visszafejteni, és olvassa el a rendszer, mielőtt a rendszer alkalmazza azokat a lekéréses szolgáltatás protokoll használatával (például a Windows Server rendszerben elérhető lekéréses szolgáltatás).</span><span class="sxs-lookup"><span data-stu-id="6dcdd-109">The process described in this article is required only when implementing a solution using the pull service protocol if certificates are not managed, to ensure configurations downloaded by the target node can be decrypted and read by the system before they are applied (for example, the pull service available in Windows Server).</span></span>
<span data-ttu-id="6dcdd-110">Csomópontok regisztrálva [Azure Automation DSC](https://docs.microsoft.com/azure/automation/automation-dsc-overview) lesz automatikusan tanúsítványok telepítése és kezeli a szolgáltatást, amely nem felügyeleti terheket szükséges.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-110">Nodes registered to [Azure Automation DSC](https://docs.microsoft.com/azure/automation/automation-dsc-overview) will automatically have certificates installed and managed by the service with no administrative overhead required.</span></span>

><span data-ttu-id="6dcdd-111">**Megjegyzés:** Ez a témakör ismerteti a titkosításhoz használt tanúsítvány.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-111">**Note:** This topic discusses certificates used for encryption.</span></span>
><span data-ttu-id="6dcdd-112">A titkosításhoz önaláírt tanúsítványt is elegendő, mert a titkos kulcsot mindig tartják a titkos kulcs és a titkosítás nem feltétlenül jelenti a dokumentum megbízhatósági.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-112">For encryption, a self-signed certificate is sufficient, because the private key is always kept secret and encryption does not imply trust of the document.</span></span>
><span data-ttu-id="6dcdd-113">Önaláírt tanúsítványokat kell *nem* hitelesítési célokra lehetne felhasználni.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-113">Self-signed certificates should *not* be used for authentication purposes.</span></span>
><span data-ttu-id="6dcdd-114">Hitelesítési célú tanúsítványt a egy megbízható hitelesítésszolgáltató (CA) kell használnia.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-114">You should use a certificate from a trusted Certification Authority (CA) for any authentication purposes.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6dcdd-115">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="6dcdd-115">Prerequisites</span></span>

<span data-ttu-id="6dcdd-116">Sikeresen titkosítsa a hitelesítő adatok használatával teszi biztonságossá a DSC-konfiguráció, győződjön meg arról, hogy a következő:</span><span class="sxs-lookup"><span data-stu-id="6dcdd-116">To successfully encrypt the credentials used to secure a DSC configuration, make sure you have the following:</span></span>

* <span data-ttu-id="6dcdd-117">**Néhány azt jelenti, hogy kiállító és tanúsítványok terjesztésére**.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-117">**Some means of issuing and distributing certificates**.</span></span> <span data-ttu-id="6dcdd-118">Ez a témakör és a példák azt feltételezik, Active Directory-hitelesítésszolgáltatót használ.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-118">This topic and its examples assume you are using Active Directory Certification Authority.</span></span> <span data-ttu-id="6dcdd-119">Az Active Directory tanúsítványszolgáltatások további háttérinformációkat, lásd: [Active Directory tanúsítványszolgáltatások áttekintése](https://technet.microsoft.com/library/hh831740.aspx) és [a Windows Server 2008 Active Directory tanúsítványszolgáltatások](https://technet.microsoft.com/windowsserver/dd448615.aspx).</span><span class="sxs-lookup"><span data-stu-id="6dcdd-119">For more background information on Active Directory Certificate Services, see [Active Directory Certificate Services Overview](https://technet.microsoft.com/library/hh831740.aspx) and [Active Directory Certificate Services in Windows Server 2008](https://technet.microsoft.com/windowsserver/dd448615.aspx).</span></span>
* <span data-ttu-id="6dcdd-120">**A cél csomópont egy vagy több felügyeleti hozzáférés**.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-120">**Administrative access to the target node or nodes**.</span></span>
* <span data-ttu-id="6dcdd-121">**Minden cél fürtcsomópont egy titkosítási-kompatibilis tanúsítványt a személyes tárolójába mentett**.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-121">**Each target node has an encryption-capable certificate saved its Personal Store**.</span></span> <span data-ttu-id="6dcdd-122">A Windows PowerShell a tároló elérési útja a Cert: \LocalMachine\My.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-122">In Windows PowerShell, the path to the store is Cert:\LocalMachine\My.</span></span> <span data-ttu-id="6dcdd-123">Ebben a témakörben szereplő példák használhatja a "munkaállomás-hitelesítési" sablont, amely (együtt más tanúsítványsablonokat) található [alapértelmezett tanúsítványsablonokat](https://technet.microsoft.com/library/cc740061(v=WS.10).aspx).</span><span class="sxs-lookup"><span data-stu-id="6dcdd-123">The examples in this topic use the “workstation authentication” template, which you can find (along with other certificate templates) at [Default Certificate Templates](https://technet.microsoft.com/library/cc740061(v=WS.10).aspx).</span></span>
* <span data-ttu-id="6dcdd-124">Ha a célcsomóponton eltérő számítógépen található ebben a konfigurációban futtatni **a tanúsítvány nyilvános kulcsának exportálásához**, majd importálja a konfigurációt fogja futtatni a számítógépen.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-124">If you will be running this configuration on a computer other than the target node, **export the public key of the certificate**, and then import it to the computer you will run the configuration from.</span></span> <span data-ttu-id="6dcdd-125">Győződjön meg arról, hogy exportálás csak a **nyilvános** kulcs; a titkos kulcs biztonsága.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-125">Make sure that you export only the **public** key; keep the private key secure.</span></span>

## <a name="overall-process"></a><span data-ttu-id="6dcdd-126">Teljes folyamata</span><span class="sxs-lookup"><span data-stu-id="6dcdd-126">Overall process</span></span>

 1. <span data-ttu-id="6dcdd-127">A tanúsítványok, a kulcsok és a ujjlenyomatok, annak biztosítása, hogy minden célcsomóponttal a tanúsítvány másolatát, és a konfigurációs számítógépen van, a nyilvános kulcs és az ujjlenyomat beállítása.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-127">Set up the certificates, keys, and thumbprints, making sure that each target node has copies of the certificate and the configuration computer has the public key and thumbprint.</span></span>
 2. <span data-ttu-id="6dcdd-128">Hozzon létre egy konfigurációs adatblokkot, amely tartalmazza az elérési út és a nyilvános kulcs ujjlenyomata.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-128">Create a configuration data block that contains the path and thumbprint of the public key.</span></span>
 3. <span data-ttu-id="6dcdd-129">Hozzon létre egy konfigurációs parancsfájl, amely határozza meg a kívánt konfiguráció célcsomóponton a és a célcsomópontokat visszafejtése beállítása szerint a helyi konfigurációs commanding a kezelő a tanúsítványt és annak ujjlenyomata a konfigurációs adatok visszafejtéséhez.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-129">Create a configuration script that defines your desired configuration for the target node and sets up decryption on the target nodes by commanding the Local Configuration manager to decrypt the configuration data using the certificate and its thumbprint.</span></span>
 4. <span data-ttu-id="6dcdd-130">Futtassa a konfigurációt, amely a helyi Configuration Manager beállításait, és indítsa el a DSC-konfiguráció.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-130">Run the configuration, which will set the Local Configuration Manager settings and start the DSC configuration.</span></span>

![Diagram1](images/CredentialEncryptionDiagram1.png)

## <a name="certificate-requirements"></a><span data-ttu-id="6dcdd-132">Tanúsítványkövetelmények</span><span class="sxs-lookup"><span data-stu-id="6dcdd-132">Certificate Requirements</span></span>

<span data-ttu-id="6dcdd-133">Hitelesítő adatok titkosításához kihirdeti, hogy a nyilvános kulcsú tanúsítvány rendelkezésre kell állnia a _Célcsomóponttal_ , amely **megbízható** a számítógép a DSC-konfiguráció létrehozásához használt.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-133">To enact credential encryption, a public key certificate must be available on the _Target Node_ that is **trusted** by the computer being used to author the DSC configuration.</span></span>
<span data-ttu-id="6dcdd-134">A nyilvános kulcsú tanúsítvány virtualizálásra konkrét követelmények vonatkoznak, amíg a DSC-hitelesítő adatok titkosításához használható:</span><span class="sxs-lookup"><span data-stu-id="6dcdd-134">This public key certificate has specific requirements for it to be used for DSC credential encryption:</span></span>
 1. <span data-ttu-id="6dcdd-135">**Kulcshasználat**:</span><span class="sxs-lookup"><span data-stu-id="6dcdd-135">**Key Usage**:</span></span>
   - <span data-ttu-id="6dcdd-136">Tartalmaznia kell: "KeyEncipherment" és "DataEncipherment".</span><span class="sxs-lookup"><span data-stu-id="6dcdd-136">Must contain: 'KeyEncipherment' and 'DataEncipherment'.</span></span>
   - <span data-ttu-id="6dcdd-137">Kell _nem_ tartalmaz: "Digitális aláírás".</span><span class="sxs-lookup"><span data-stu-id="6dcdd-137">Should _not_ contain: 'Digital Signature'.</span></span>
 2. <span data-ttu-id="6dcdd-138">**Kibővített kulcshasználat**:</span><span class="sxs-lookup"><span data-stu-id="6dcdd-138">**Enhanced Key Usage**:</span></span>
   - <span data-ttu-id="6dcdd-139">Tartalmaznia kell: dokumentum titkosítás (1.3.6.1.4.1.311.80.1).</span><span class="sxs-lookup"><span data-stu-id="6dcdd-139">Must contain: Document Encryption (1.3.6.1.4.1.311.80.1).</span></span>
   - <span data-ttu-id="6dcdd-140">Kell _nem_ tartalmaz: ügyfél-hitelesítés (1.3.6.1.5.5.7.3.2) és a kiszolgálói hitelesítés (1.3.6.1.5.5.7.3.1).</span><span class="sxs-lookup"><span data-stu-id="6dcdd-140">Should _not_ contain: Client Authentication (1.3.6.1.5.5.7.3.2) and Server Authentication (1.3.6.1.5.5.7.3.1).</span></span>
 3. <span data-ttu-id="6dcdd-141">A tanúsítvány titkos kulcsa megtalálható a \* cél Node_.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-141">The Private Key for the certificate is available on the \*Target Node_.</span></span>
 4. <span data-ttu-id="6dcdd-142">A **szolgáltató** a tanúsítványt nem lehet "Microsoft RSA SChannel Cryptographic Provider".</span><span class="sxs-lookup"><span data-stu-id="6dcdd-142">The **Provider** for the certificate must be "Microsoft RSA SChannel Cryptographic Provider".</span></span>
 
><span data-ttu-id="6dcdd-143">**Ajánlott eljárás:** tanúsítvány használata a kulcshasználat "Digitális aláírás" vagy a kiszolgálóhitelesítési EKU egyikét tartalmazó, bár ez lehetővé teszi a titkosítási kulcs, hogy könnyebben hibásan használt és ki van téve a támadás.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-143">**Recommended Best Practice:** Although you can use a certificate with containing a Key Usage of 'Digital Signature' or one of the Authentication EKU's, this will enable the encryption key to be more easily misused and vulnerable to attack.</span></span> <span data-ttu-id="6dcdd-144">Ezért ajánlott kihagyja ezen kulcshasználat és az EKU-kat kifejezetten DSC hitelesítő adatok védelme céljából létrehozott tanúsítvány használatát is.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-144">So it is best practice to use a certificate created specifically for the purpose of securing DSC credentials that omits these Key Usage and EKUs.</span></span>
  
<span data-ttu-id="6dcdd-145">A meglévő tanúsítványt a _Célcsomóponttal_ , hogy megfelel-e ezek a feltételek segítségével biztonságos DSC hitelesítő adatokat.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-145">Any existing certificate on the _Target Node_ that meets these criteria can be used to secure DSC credentials.</span></span>

## <a name="certificate-creation"></a><span data-ttu-id="6dcdd-146">Tanúsítvány létrehozása</span><span class="sxs-lookup"><span data-stu-id="6dcdd-146">Certificate creation</span></span>

<span data-ttu-id="6dcdd-147">Kétféleképpen történő létrehozásáról és használatáról a szükséges titkosítási tanúsítványt (nyilvános-titkos kulcsból álló kulcspárt) is igénybe vehet.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-147">There are two approaches you can take to create and use the required Encryption Certificate (public-private key pair).</span></span>

1. <span data-ttu-id="6dcdd-148">Hozza létre a **Célcsomóponttal** és csak a nyilvános kulcsának exportálásához a **szerzői csomópont**</span><span class="sxs-lookup"><span data-stu-id="6dcdd-148">Create it on the **Target Node** and export just the public key to the **Authoring Node**</span></span>
2. <span data-ttu-id="6dcdd-149">Hozza létre a **szerzői csomópont** és a teljes kulcspár exportálása az **Célcsomóponttal**</span><span class="sxs-lookup"><span data-stu-id="6dcdd-149">Create it on the **Authoring Node** and export the entire key pair to the **Target Node**</span></span>

<span data-ttu-id="6dcdd-150">1. módszer ajánlott, mert mindig célcsomóponton marad a titkos kulcs használatával fejti vissza a MOF-felhasználó hitelesítő adatait.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-150">Method 1 is recommended because the private key used to decrypt credentials in the MOF stays on the Target Node at all times.</span></span>


### <a name="creating-the-certificate-on-the-target-node"></a><span data-ttu-id="6dcdd-151">A tanúsítvány létrehozása a célcsomóponton</span><span class="sxs-lookup"><span data-stu-id="6dcdd-151">Creating the Certificate on the Target Node</span></span>

<span data-ttu-id="6dcdd-152">A titkos kulcs titkos, mert a megadott MOF visszafejt a kell tartani a **Célcsomóponttal** a legegyszerűbb, amely módja a titkos kulcsú tanúsítvány létrehozásához a **Célcsomóponttal**, és másolja a  **nyilvános kulcsú tanúsítvány** arra a számítógépre ahhoz, hogy a DSC-konfiguráció a MOF-fájlt használja.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-152">The private key must be kept secret, because is used to decrypt the MOF on the **Target Node** The easiest way to do that is to create the private key certificate on the **Target Node**, and copy the **public key certificate** to the computer being used to author the DSC configuration into a MOF file.</span></span>
<span data-ttu-id="6dcdd-153">Az alábbi példa:</span><span class="sxs-lookup"><span data-stu-id="6dcdd-153">The following example:</span></span>
 1. <span data-ttu-id="6dcdd-154">az olyan tanúsítványt hoz létre a **célcsomóponttal**</span><span class="sxs-lookup"><span data-stu-id="6dcdd-154">creates a certificate on the **Target node**</span></span>
 2. <span data-ttu-id="6dcdd-155">a nyilvános kulcsú tanúsítvány exportálása a **célcsomóponttal**.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-155">exports the public key certificate on the **Target node**.</span></span>
 3. <span data-ttu-id="6dcdd-156">a nyilvános kulcsú tanúsítvány importálása a **a** tanúsítványtárolójába a **szerzői műveletek munkaterület**.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-156">imports the public key certificate into the **my** certificate store on the **Authoring node**.</span></span>

#### <a name="on-the-target-node-create-and-export-the-certificate"></a><span data-ttu-id="6dcdd-157">Célcsomóponton: hozzon létre, és a tanúsítvány exportálása</span><span class="sxs-lookup"><span data-stu-id="6dcdd-157">On the Target Node: create and export the certificate</span></span>
><span data-ttu-id="6dcdd-158">Célcsomóponttal: Windows Server 2016 és Windows 10</span><span class="sxs-lookup"><span data-stu-id="6dcdd-158">Target Node: Windows Server 2016 and Windows 10</span></span>

```powershell
# note: These steps need to be performed in an Administrator PowerShell session
$cert = New-SelfSignedCertificate -Type DocumentEncryptionCertLegacyCsp -DnsName 'DscEncryptionCert' -HashAlgorithm SHA256
# export the public key certificate
$cert | Export-Certificate -FilePath "$env:temp\DscPublicKey.cer" -Force
```
<span data-ttu-id="6dcdd-159">Egyszer exportált, a ```DscPublicKey.cer``` kell átmásolni a **szerzői csomópont**.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-159">Once exported, the ```DscPublicKey.cer``` would need to be copied to the **Authoring Node**.</span></span>

><span data-ttu-id="6dcdd-160">Célcsomóponttal: Windows Server 2012 R2 vagy Windows 8.1 és korábbi</span><span class="sxs-lookup"><span data-stu-id="6dcdd-160">Target Node: Windows Server 2012 R2/Windows 8.1 and earlier</span></span>

<span data-ttu-id="6dcdd-161">Mivel a New-SelfSignedCertificate parancsmag a Windows operációs rendszer Windows 10 és Windows Server 2016 előtti nem támogatják a **típus** paraméter, a tanúsítvány létrehozása alternatív módszert ezek megadása szükséges operációs rendszerek.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-161">Because the New-SelfSignedCertificate cmdlet on Windows Operating Systems prior to Windows 10 and Windows Server 2016 do not support the **Type** parameter, an alternate method of creating this certificate is required on these operating systems.</span></span>
<span data-ttu-id="6dcdd-162">Ebben az esetben használhatja ```makecert.exe``` vagy ```certutil.exe``` a tanúsítvány létrehozásához.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-162">In this case you can use ```makecert.exe``` or ```certutil.exe``` to create the certificate.</span></span>

<span data-ttu-id="6dcdd-163">Egy másik módszer [a New-SelfSignedCertificateEx.ps1 parancsprogram letöltése a Microsoft Script Center](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6) , és hozzon létre helyette a tanúsítványt:</span><span class="sxs-lookup"><span data-stu-id="6dcdd-163">An alternate method is to [download the New-SelfSignedCertificateEx.ps1 script from Microsoft Script Center](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6) and use it to create the certificate instead:</span></span>
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
$Cert = Get-ChildItem -Path cert:\LocalMachine\My `
    | Where-Object {
        ($_.FriendlyName -eq 'DSC Credential Encryption certificate') `
        -and ($_.Subject -eq "CN=${ENV:ComputerName}")
    } | Select-Object -First 1
# export the public key certificate
$cert | Export-Certificate -FilePath "$env:temp\DscPublicKey.cer" -Force
```
<span data-ttu-id="6dcdd-164">Egyszer exportált, a ```DscPublicKey.cer``` kell átmásolni a **szerzői csomópont**.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-164">Once exported, the ```DscPublicKey.cer``` would need to be copied to the **Authoring Node**.</span></span>

#### <a name="on-the-authoring-node-import-the-certs-public-key"></a><span data-ttu-id="6dcdd-165">A szerzői műveletek csomóponton: a tanúsítvány nyilvános kulcsát importálnia</span><span class="sxs-lookup"><span data-stu-id="6dcdd-165">On the Authoring Node: import the cert’s public key</span></span>
```powershell
# Import to the my store
Import-Certificate -FilePath "$env:temp\DscPublicKey.cer" -CertStoreLocation Cert:\LocalMachine\My
```

### <a name="creating-the-certificate-on-the-authoring-node"></a><span data-ttu-id="6dcdd-166">A tanúsítvány létrehozása a szerzői műveletekhez csomóponton</span><span class="sxs-lookup"><span data-stu-id="6dcdd-166">Creating the Certificate on the Authoring Node</span></span>
<span data-ttu-id="6dcdd-167">Alternatív megoldásként a titkosítási tanúsítványhoz hozható létre a **szerzői csomópont**, az exportált a **titkos kulcs** , a PFX fájlt, és ezután importálja a **Célcsomóponttal**.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-167">Alternately, the encryption certificate can be created on the **Authoring Node**, exported with the **private key** as a PFX file and then imported on the **Target Node**.</span></span>
<span data-ttu-id="6dcdd-168">Ez a DSC-hitelesítő adatok titkosításához megvalósításához a jelenlegi mód _Nano Server_.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-168">This is the current method for implementing DSC credential encryption on _Nano Server_.</span></span>
<span data-ttu-id="6dcdd-169">Bár a PFX jelszóval védett kell álljon biztonságos átvitel során.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-169">Although the PFX is secured with a password it should be kept secure during transit.</span></span>
<span data-ttu-id="6dcdd-170">Az alábbi példa:</span><span class="sxs-lookup"><span data-stu-id="6dcdd-170">The following example:</span></span>
 1. <span data-ttu-id="6dcdd-171">az olyan tanúsítványt hoz létre a **szerzői műveletek munkaterület**.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-171">creates a certificate on the **Authoring node**.</span></span>
 2. <span data-ttu-id="6dcdd-172">exportálja a tanúsítványt a titkos kulcs is a **szerzői műveletek munkaterület**.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-172">exports the certificate including the private key on the **Authoring node**.</span></span>
 3. <span data-ttu-id="6dcdd-173">eltávolítja a titkos kulcsot a **szerzői műveletek munkaterület**, tartja a nyilvános kulcsú tanúsítvány, de a **a** tárolja.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-173">removes the private key from the **Authoring node**, but keeps the public key certificate in the **my** store.</span></span>
 4. <span data-ttu-id="6dcdd-174">a titkos kulcsú tanúsítvány importálása a gyökértanúsítvány-tárolójából a a **célcsomóponttal**.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-174">imports the private key certificate into the root certificate store on the **Target node**.</span></span>
   - <span data-ttu-id="6dcdd-175">akkor kell felvenni a gyökérszintű tárolóban. így az megbízható által a **célcsomóponttal**.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-175">it must be added to the root store so that it will be trusted by the **Target node**.</span></span>

#### <a name="on-the-authoring-node-create-and-export-the-certificate"></a><span data-ttu-id="6dcdd-176">A szerzői műveletek csomóponton: hozzon létre, és a tanúsítvány exportálása</span><span class="sxs-lookup"><span data-stu-id="6dcdd-176">On the Authoring Node: create and export the certificate</span></span>
><span data-ttu-id="6dcdd-177">Célcsomóponttal: Windows Server 2016 és Windows 10</span><span class="sxs-lookup"><span data-stu-id="6dcdd-177">Target Node: Windows Server 2016 and Windows 10</span></span>

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
<span data-ttu-id="6dcdd-178">Egyszer exportált, a ```DscPrivateKey.pfx``` kell átmásolni a **Célcsomóponttal**.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-178">Once exported, the ```DscPrivateKey.pfx``` would need to be copied to the **Target Node**.</span></span>

><span data-ttu-id="6dcdd-179">Célcsomóponttal: Windows Server 2012 R2 vagy Windows 8.1 és korábbi</span><span class="sxs-lookup"><span data-stu-id="6dcdd-179">Target Node: Windows Server 2012 R2/Windows 8.1 and earlier</span></span>

<span data-ttu-id="6dcdd-180">Mivel a New-SelfSignedCertificate parancsmag a Windows operációs rendszer Windows 10 és Windows Server 2016 előtti nem támogatják a **típus** paraméter, a tanúsítvány létrehozása alternatív módszert ezek megadása szükséges operációs rendszerek.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-180">Because the New-SelfSignedCertificate cmdlet on Windows Operating Systems prior to Windows 10 and Windows Server 2016 do not support the **Type** parameter, an alternate method of creating this certificate is required on these operating systems.</span></span>
<span data-ttu-id="6dcdd-181">Ebben az esetben használhatja ```makecert.exe``` vagy ```certutil.exe``` a tanúsítvány létrehozásához.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-181">In this case you can use ```makecert.exe``` or ```certutil.exe``` to create the certificate.</span></span>

<span data-ttu-id="6dcdd-182">Egy másik módszer [a New-SelfSignedCertificateEx.ps1 parancsprogram letöltése a Microsoft Script Center](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6) , és hozzon létre helyette a tanúsítványt:</span><span class="sxs-lookup"><span data-stu-id="6dcdd-182">An alternate method is to [download the New-SelfSignedCertificateEx.ps1 script from Microsoft Script Center](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6) and use it to create the certificate instead:</span></span>
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
$Cert = Get-ChildItem -Path cert:\LocalMachine\My `
    | Where-Object {
        ($_.FriendlyName -eq 'DSC Credential Encryption certificate') `
        -and ($_.Subject -eq "CN=${ENV:ComputerName}")
    } | Select-Object -First 1
# export the public key certificate
$mypwd = ConvertTo-SecureString -String "YOUR_PFX_PASSWD" -Force -AsPlainText
$cert | Export-PfxCertificate -FilePath "$env:temp\DscPrivateKey.pfx" -Password $mypwd -Force
# remove the private key certificate from the node but keep the public key certificate
$cert | Export-Certificate -FilePath "$env:temp\DscPublicKey.cer" -Force
$cert | Remove-Item -Force
Import-Certificate -FilePath "$env:temp\DscPublicKey.cer" -CertStoreLocation Cert:\LocalMachine\My
```

#### <a name="on-the-target-node-import-the-certs-private-key-as-a-trusted-root"></a><span data-ttu-id="6dcdd-183">Célcsomóponton: a tanúsítvány titkos kulcsot a megbízható legfelső szintű importálása</span><span class="sxs-lookup"><span data-stu-id="6dcdd-183">On the Target Node: import the cert’s private key as a trusted root</span></span>
```powershell
# Import to the root store so that it is trusted
$mypwd = ConvertTo-SecureString -String "YOUR_PFX_PASSWD" -Force -AsPlainText
Import-PfxCertificate -FilePath "$env:temp\DscPrivateKey.pfx" -CertStoreLocation Cert:\LocalMachine\My -Password $mypwd > $null
```

## <a name="configuration-data"></a><span data-ttu-id="6dcdd-184">Konfigurációs adatok</span><span class="sxs-lookup"><span data-stu-id="6dcdd-184">Configuration data</span></span>

<span data-ttu-id="6dcdd-185">A konfigurációs adatok blokk határozza meg, mely célcsomópontokat működik, hogy-e, vagy nem a hitelesítő adatokat, az azt jelenti, hogy a titkosítás és egyéb információk titkosítására.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-185">The configuration data block defines which target nodes to operate on, whether or not to encrypt the credentials, the means of encryption, and other information.</span></span> <span data-ttu-id="6dcdd-186">A konfigurációs adatok blokk további információkért lásd: [elválasztó konfigurációs és környezeti adatok](configData.md).</span><span class="sxs-lookup"><span data-stu-id="6dcdd-186">For more information on the configuration data block, see [Separating Configuration and Environment Data](configData.md).</span></span>

<span data-ttu-id="6dcdd-187">A hitelesítő adatok titkosítás kapcsolódó, az egyes csomópontok konfigurálható elemek a következők:</span><span class="sxs-lookup"><span data-stu-id="6dcdd-187">The elements that can be configured for each node that are related to credential encryption are:</span></span>
* <span data-ttu-id="6dcdd-188">**Csomópontnév** -a célcsomópont a hitelesítő adatok titkosításához a konfigurálni kívánt nevét.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-188">**NodeName** - the name of the target node that the credential encryption is being configured for.</span></span>
* <span data-ttu-id="6dcdd-189">**PsDscAllowPlainTextPassword** - e a titkosított hitelesítő adatokat kell átadni ebben a csomópontban engedélyezve lesz.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-189">**PsDscAllowPlainTextPassword** - whether unencrypted credentials will be allowed to be passed to this node.</span></span> <span data-ttu-id="6dcdd-190">Ez az **nem ajánlott**.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-190">This is **not recommended**.</span></span>
* <span data-ttu-id="6dcdd-191">**Ujjlenyomat** – a felhasználó hitelesítő adatait a DSC-konfiguráció visszafejtése a használt tanúsítvány ujjlenyomata a _Célcsomóponttal_.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-191">**Thumbprint** - the thumbprint of the certificate that will be used to decrypt the credentials in the DSC Configuration on the _Target Node_.</span></span> <span data-ttu-id="6dcdd-192">**Ezt a tanúsítványt a helyi számítógép tanúsítványtárolójába a léteznie kell.**</span><span class="sxs-lookup"><span data-stu-id="6dcdd-192">**This certificate must exist in the Local Machine certificate store on the Target Node.**</span></span>
* <span data-ttu-id="6dcdd-193">**CertificateFile** – a Tanúsítványfájl (csak a nyilvános kulcsot tartalmazó), amely a hitelesítő adatok titkosításához használandó a _Célcsomóponttal_.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-193">**CertificateFile** - the certificate file (containing the public key only) that should be used to encrypt the credentials for the _Target Node_.</span></span> <span data-ttu-id="6dcdd-194">Ez lehet akár egy DER kódolású bináris X.509 vagy Base-64 kódolású X.509 formátum tanúsítványfájlt.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-194">This must be either a DER encoded binary X.509 or Base-64 encoded X.509 format certificate file.</span></span>

<span data-ttu-id="6dcdd-195">Ez a példa bemutatja egy konfigurációs adatblokk meghatározza, hogy a célcsomóponton való működésre elnevezett célcsomópont, a nyilvános kulcs tanúsítványfájljából (nevű targetNode.cer), és az ujjlenyomat a nyilvános kulcs elérési útja.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-195">This example shows a configuration data block that specifies a target node to act on named targetNode, the path to the public key certificate file (named targetNode.cer), and the thumbprint for the public key.</span></span>

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


## <a name="configuration-script"></a><span data-ttu-id="6dcdd-196">Konfigurációs parancsfájl</span><span class="sxs-lookup"><span data-stu-id="6dcdd-196">Configuration script</span></span>

<span data-ttu-id="6dcdd-197">A konfigurációs parancsfájl önmagában, használja a `PsCredential` győződjön meg arról, hogy a hitelesítő adatokat kell tárolni a lehető legrövidebb idő alatt a paramétert.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-197">In the configuration script itself, use the `PsCredential` parameter to ensure that credentials are stored for the shortest possible time.</span></span> <span data-ttu-id="6dcdd-198">A megadott példa futtatásakor DSC kéri a hitelesítő adatokat, és majd titkosíthatja a MOF-fájlt, a társított konfigurációs adatblokk a célcsomóponton CertificateFile használatával.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-198">When you run the supplied example, DSC will prompt you for credentials and then encrypt the MOF file using the CertificateFile that is associated with the target node in the configuration data block.</span></span> <span data-ttu-id="6dcdd-199">Ez a Kódpélda másolja át a fájl egy védett megosztást egy felhasználó számára.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-199">This code example copies a file from a share that is secured to a user.</span></span>

```
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

## <a name="setting-up-decryption"></a><span data-ttu-id="6dcdd-200">Visszafejtési beállítása</span><span class="sxs-lookup"><span data-stu-id="6dcdd-200">Setting up decryption</span></span>

<span data-ttu-id="6dcdd-201">Mielőtt [ `Start-DscConfiguration` ](https://technet.microsoft.com/library/dn521623.aspx) is működik, hogy mely tanúsítványokat használja a hitelesítő adatok visszafejtése közölje a helyi Configuration Manager minden egyes cél csomóponton a CertificateID erőforrás ellenőrzése a tanúsítvány ujjlenyomata segítségével.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-201">Before [`Start-DscConfiguration`](https://technet.microsoft.com/library/dn521623.aspx) can work, you have to tell the Local Configuration Manager on each target node which certificate to use to decrypt the credentials, using the CertificateID resource to verify the certificate’s thumbprint.</span></span> <span data-ttu-id="6dcdd-202">Ez a példa funkció megkeresi a megfelelő helyi tanúsítvány (lehetséges, hogy testre szabhatja, így a pontos használni kívánt tanúsítványt keres, megtalálja a):</span><span class="sxs-lookup"><span data-stu-id="6dcdd-202">This example function will find the appropriate local certificate (you might have to customize it so it will find the exact certificate you want to use):</span></span>

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

<span data-ttu-id="6dcdd-203">A tanúsítvány annak ujjlenyomata által azonosított a konfigurációs parancsfájl frissíthető értéket használja:</span><span class="sxs-lookup"><span data-stu-id="6dcdd-203">With the certificate identified by its thumbprint, the configuration script can be updated to use the value:</span></span>

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

## <a name="running-the-configuration"></a><span data-ttu-id="6dcdd-204">A konfiguráció futtatása</span><span class="sxs-lookup"><span data-stu-id="6dcdd-204">Running the configuration</span></span>

<span data-ttu-id="6dcdd-205">Ezen a ponton a konfigurációt, amely kimeneteként két fájlt is futtathatja:</span><span class="sxs-lookup"><span data-stu-id="6dcdd-205">At this point, you can run the configuration, which will output two files:</span></span>

 * <span data-ttu-id="6dcdd-206">A \*. meta.mof fájl, amely a helyi Configuration Manager visszafejtése a hitelesítő adatokat, a tanúsítványt használ, amely a helyi számítógép tárolójában tárolja, és annak ujjlenyomata által azonosított konfigurálja.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-206">A \*.meta.mof file that configures the Local Configuration Manager to decrypt the credentials using the certificate that is stored on the local machine store and identified by its thumbprint.</span></span> <span data-ttu-id="6dcdd-207">[`Set-DscLocalConfigurationManager`](https://technet.microsoft.com/library/dn521621.aspx) alkalmazza a \*. meta.mof fájlt.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-207">[`Set-DscLocalConfigurationManager`](https://technet.microsoft.com/library/dn521621.aspx) applies the \*.meta.mof file.</span></span>
 * <span data-ttu-id="6dcdd-208">A MOF-fájlt, amely ténylegesen konfigurációjának alkalmazására szolgál.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-208">A MOF file that actually applies the configuration.</span></span> <span data-ttu-id="6dcdd-209">Start-DscConfiguration konfigurációjának alkalmazására szolgál.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-209">Start-DscConfiguration applies the configuration.</span></span>

<span data-ttu-id="6dcdd-210">Ezek a parancsok érnek el ezeket a lépéseket:</span><span class="sxs-lookup"><span data-stu-id="6dcdd-210">These commands will accomplish those steps:</span></span>

```powershell
Write-Host "Generate DSC Configuration..."
CredentialEncryptionExample -ConfigurationData $ConfigData -OutputPath .\CredentialEncryptionExample

Write-Host "Setting up LCM to decrypt credentials..."
Set-DscLocalConfigurationManager .\CredentialEncryptionExample -Verbose 
 
Write-Host "Starting Configuration..."
Start-DscConfiguration .\CredentialEncryptionExample -wait -Verbose
```

<span data-ttu-id="6dcdd-211">Ebben a példában a DSC-konfiguráció célcsomóponton való miatt.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-211">This example would push the DSC configuration to the target node.</span></span>
<span data-ttu-id="6dcdd-212">A DSC-konfiguráció alkalmazható DSC lekéréses kiszolgálót használ, ha elérhető ilyen.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-212">The DSC configuration can also be applied using a DSC Pull Server if one is available.</span></span>

<span data-ttu-id="6dcdd-213">Lásd: [ügyféltelepítéshez DSC lekérési](pullClient.md) további információt a DSC-konfigurációk használata a DSC lekérési kiszolgálójával alkalmazása.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-213">See [Setting up a DSC pull client](pullClient.md) for more information on applying DSC configurations using a DSC Pull Server.</span></span>

## <a name="credential-encryption-module-example"></a><span data-ttu-id="6dcdd-214">Hitelesítő adatok titkosítás modul – példa</span><span class="sxs-lookup"><span data-stu-id="6dcdd-214">Credential Encryption Module Example</span></span>

<span data-ttu-id="6dcdd-215">Íme egy teljes példa, amely magában foglalja a teljes ezeket a lépéseket, valamint segítő parancsmag exportálja, és másolja át a nyilvános kulcsok:</span><span class="sxs-lookup"><span data-stu-id="6dcdd-215">Here is a full example that incorporates all of these steps, plus a helper cmdlet that exports and copies the public keys:</span></span>

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

