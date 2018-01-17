---
ms.date: 2017-10-31
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "A MOF-fájl védelme"
ms.openlocfilehash: fdb8fa17e9b5e92b56e0a62bf850529c241eee41
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 01/17/2018
---
# <a name="securing-the-mof-file"></a>A MOF-fájl védelme

>Vonatkozik: A Windows PowerShell 4.0-s verzióját, a Windows PowerShell 5.0

A DSC csomópontok konfigurációját úgy, hogy alkalmazza a MOF-fájlt, ahol a helyi Configuration Manager (LCM) valósítja meg a kívánt cél állapot tárolt információk kezeli.
Ez a fájl tartalmazza a konfiguráció részletes adatait, mert fontos biztonságának megőrzése.
Ez a témakör ismerteti a célcsomópont a fájl van titkosítva.

PowerShell 5.0-s verziójának kezdve a teljes MOF-fájl titkosítva van alapértelmezés szerint a csomópont történő alkalmazásakor a **Start-DSCConfiguration** parancsmag.
A cikkben leírt eljárás esetén szükséges csak egy megoldás, ha a tanúsítványok nem kezelt, annak érdekében, tölti le a célcsomópont konfigurációk visszafejteni, és olvassa el a rendszer, mielőtt a rendszer alkalmazza azokat a lekéréses szolgáltatás protokoll használatával (például a Windows Server rendszerben elérhető lekéréses szolgáltatás).
Csomópontok regisztrálva [Azure Automation DSC](https://docs.microsoft.com/en-us/azure/automation/automation-dsc-overview) lesz automatikusan tanúsítványok telepítése és kezeli a szolgáltatást, amely nem felügyeleti terheket szükséges.

>**Megjegyzés:** Ez a témakör ismerteti a titkosításhoz használt tanúsítvány.
>A titkosításhoz önaláírt tanúsítványt is elegendő, mert a titkos kulcsot mindig tartják a titkos kulcs és a titkosítás nem feltétlenül jelenti a dokumentum megbízhatósági.
>Önaláírt tanúsítványokat kell *nem* hitelesítési célokra lehetne felhasználni.
>Hitelesítési célú tanúsítványt a egy megbízható hitelesítésszolgáltató (CA) kell használnia.

## <a name="prerequisites"></a>Előfeltételek

Sikeresen titkosítsa a hitelesítő adatok használatával teszi biztonságossá a DSC-konfiguráció, győződjön meg arról, hogy a következő:

* **Néhány azt jelenti, hogy kiállító és tanúsítványok terjesztésére**. Ez a témakör és a példák azt feltételezik, Active Directory-hitelesítésszolgáltatót használ. Az Active Directory tanúsítványszolgáltatások további háttérinformációkat, lásd: [Active Directory tanúsítványszolgáltatások áttekintése](https://technet.microsoft.com/library/hh831740.aspx) és [a Windows Server 2008 Active Directory tanúsítványszolgáltatások](https://technet.microsoft.com/windowsserver/dd448615.aspx).
* **A cél csomópont egy vagy több felügyeleti hozzáférés**.
* **Minden cél fürtcsomópont egy titkosítási-kompatibilis tanúsítványt a személyes tárolójába mentett**. A Windows PowerShell a tároló elérési útja a Cert: \LocalMachine\My. Ebben a témakörben szereplő példák használhatja a "munkaállomás-hitelesítési" sablont, amely (együtt más tanúsítványsablonokat) található [alapértelmezett tanúsítványsablonokat](https://technet.microsoft.com/library/cc740061(v=WS.10).aspx).
* Ha a célcsomóponton eltérő számítógépen található ebben a konfigurációban futtatni **a tanúsítvány nyilvános kulcsának exportálásához**, majd importálja a konfigurációt fogja futtatni a számítógépen. Győződjön meg arról, hogy exportálás csak a **nyilvános** kulcs; a titkos kulcs biztonsága.

## <a name="overall-process"></a>Teljes folyamata

 1. A tanúsítványok, a kulcsok és a ujjlenyomatok, annak biztosítása, hogy minden célcsomóponttal a tanúsítvány másolatát, és a konfigurációs számítógépen van, a nyilvános kulcs és az ujjlenyomat beállítása.
 2. Hozzon létre egy konfigurációs adatblokkot, amely tartalmazza az elérési út és a nyilvános kulcs ujjlenyomata.
 3. Hozzon létre egy konfigurációs parancsfájl, amely határozza meg a kívánt konfiguráció célcsomóponton a és a célcsomópontokat visszafejtése beállítása szerint a helyi konfigurációs commanding a kezelő a tanúsítványt és annak ujjlenyomata a konfigurációs adatok visszafejtéséhez.
 4. Futtassa a konfigurációt, amely a helyi Configuration Manager beállításait, és indítsa el a DSC-konfiguráció.

![Diagram1](images/CredentialEncryptionDiagram1.png)

## <a name="certificate-requirements"></a>Tanúsítványkövetelmények

Hitelesítő adatok titkosításához kihirdeti, hogy a nyilvános kulcsú tanúsítvány rendelkezésre kell állnia a _Célcsomóponttal_ , amely **megbízható** a számítógép a DSC-konfiguráció létrehozásához használt.
A nyilvános kulcsú tanúsítvány virtualizálásra konkrét követelmények vonatkoznak, amíg a DSC-hitelesítő adatok titkosításához használható:
 1. **Kulcshasználat**:
   - Tartalmaznia kell: "KeyEncipherment" és "DataEncipherment".
   - Kell _nem_ tartalmaz: "Digitális aláírás".
 2. **Kibővített kulcshasználat**:
   - Tartalmaznia kell: dokumentum titkosítás (1.3.6.1.4.1.311.80.1).
   - Kell _nem_ tartalmaz: ügyfél-hitelesítés (1.3.6.1.5.5.7.3.2) és a kiszolgálói hitelesítés (1.3.6.1.5.5.7.3.1).
 3. A tanúsítvány titkos kulcsa megtalálható a * cél Node_.
 4. A **szolgáltató** a tanúsítványt nem lehet "Microsoft RSA SChannel Cryptographic Provider".
 
>**Ajánlott eljárás:** tanúsítvány használata a kulcshasználat "Digitális aláírás" vagy a kiszolgálóhitelesítési EKU egyikét tartalmazó, bár ez lehetővé teszi a titkosítási kulcs, hogy könnyebben hibásan használt és ki van téve a támadás. Ezért ajánlott kihagyja ezen kulcshasználat és az EKU-kat kifejezetten DSC hitelesítő adatok védelme céljából létrehozott tanúsítvány használatát is.
  
A meglévő tanúsítványt a _Célcsomóponttal_ , hogy megfelel-e ezek a feltételek segítségével biztonságos DSC hitelesítő adatokat.

## <a name="certificate-creation"></a>Tanúsítvány létrehozása

Kétféleképpen történő létrehozásáról és használatáról a szükséges titkosítási tanúsítványt (nyilvános-titkos kulcsból álló kulcspárt) is igénybe vehet.

1. Hozza létre a **Célcsomóponttal** és csak a nyilvános kulcsának exportálásához a **szerzői csomópont**
2. Hozza létre a **szerzői csomópont** és a teljes kulcspár exportálása az **Célcsomóponttal**

1. módszer ajánlott, mert mindig célcsomóponton marad a titkos kulcs használatával fejti vissza a MOF-felhasználó hitelesítő adatait.


### <a name="creating-the-certificate-on-the-target-node"></a>A tanúsítvány létrehozása a célcsomóponton

A titkos kulcs titkos, mert a megadott MOF visszafejt a kell tartani a **Célcsomóponttal** a legegyszerűbb, amely módja a titkos kulcsú tanúsítvány létrehozásához a **Célcsomóponttal**, és másolja a  **nyilvános kulcsú tanúsítvány** arra a számítógépre ahhoz, hogy a DSC-konfiguráció a MOF-fájlt használja.
Az alábbi példa:
 1. az olyan tanúsítványt hoz létre a **célcsomóponttal**
 2. a nyilvános kulcsú tanúsítvány exportálása a **célcsomóponttal**.
 3. a nyilvános kulcsú tanúsítvány importálása a **a** tanúsítványtárolójába a **szerzői műveletek munkaterület**.

#### <a name="on-the-target-node-create-and-export-the-certificate"></a>Célcsomóponton: hozzon létre, és a tanúsítvány exportálása
>Célcsomóponttal: Windows Server 2016 és Windows 10

```powershell
# note: These steps need to be performed in an Administrator PowerShell session
$cert = New-SelfSignedCertificate -Type DocumentEncryptionCertLegacyCsp -DnsName 'DscEncryptionCert' -HashAlgorithm SHA256
# export the public key certificate
$cert | Export-Certificate -FilePath "$env:temp\DscPublicKey.cer" -Force
```
Egyszer exportált, a ```DscPublicKey.cer``` kell átmásolni a **szerzői csomópont**.

>Célcsomóponttal: Windows Server 2012 R2 vagy Windows 8.1 és korábbi

Mivel a New-SelfSignedCertificate parancsmag a Windows operációs rendszer Windows 10 és Windows Server 2016 előtti nem támogatják a **típus** paraméter, a tanúsítvány létrehozása alternatív módszert ezek megadása szükséges operációs rendszerek.
Ebben az esetben használhatja ```makecert.exe``` vagy ```certutil.exe``` a tanúsítvány létrehozásához.

Egy másik módszer [a New-SelfSignedCertificateEx.ps1 parancsprogram letöltése a Microsoft Script Center](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6) , és hozzon létre helyette a tanúsítványt:
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
Egyszer exportált, a ```DscPublicKey.cer``` kell átmásolni a **szerzői csomópont**.

#### <a name="on-the-authoring-node-import-the-certs-public-key"></a>A szerzői műveletek csomóponton: a tanúsítvány nyilvános kulcsát importálnia
```powershell
# Import to the my store
Import-Certificate -FilePath "$env:temp\DscPublicKey.cer" -CertStoreLocation Cert:\LocalMachine\My
```

### <a name="creating-the-certificate-on-the-authoring-node"></a>A tanúsítvány létrehozása a szerzői műveletekhez csomóponton
Alternatív megoldásként a titkosítási tanúsítványhoz hozható létre a **szerzői csomópont**, az exportált a **titkos kulcs** , a PFX fájlt, és ezután importálja a **Célcsomóponttal**.
Ez a DSC-hitelesítő adatok titkosításához megvalósításához a jelenlegi mód _Nano Server_.
Bár a PFX jelszóval védett kell álljon biztonságos átvitel során.
Az alábbi példa:
 1. az olyan tanúsítványt hoz létre a **szerzői műveletek munkaterület**.
 2. exportálja a tanúsítványt a titkos kulcs is a **szerzői műveletek munkaterület**.
 3. eltávolítja a titkos kulcsot a **szerzői műveletek munkaterület**, tartja a nyilvános kulcsú tanúsítvány, de a **a** tárolja.
 4. a titkos kulcsú tanúsítvány importálása a gyökértanúsítvány-tárolójából a a **célcsomóponttal**.
   - akkor kell felvenni a gyökérszintű tárolóban. így az megbízható által a **célcsomóponttal**.

#### <a name="on-the-authoring-node-create-and-export-the-certificate"></a>A szerzői műveletek csomóponton: hozzon létre, és a tanúsítvány exportálása
>Célcsomóponttal: Windows Server 2016 és Windows 10

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
Egyszer exportált, a ```DscPrivateKey.pfx``` kell átmásolni a **Célcsomóponttal**.

>Célcsomóponttal: Windows Server 2012 R2 vagy Windows 8.1 és korábbi

Mivel a New-SelfSignedCertificate parancsmag a Windows operációs rendszer Windows 10 és Windows Server 2016 előtti nem támogatják a **típus** paraméter, a tanúsítvány létrehozása alternatív módszert ezek megadása szükséges operációs rendszerek.
Ebben az esetben használhatja ```makecert.exe``` vagy ```certutil.exe``` a tanúsítvány létrehozásához.

Egy másik módszer [a New-SelfSignedCertificateEx.ps1 parancsprogram letöltése a Microsoft Script Center](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6) , és hozzon létre helyette a tanúsítványt:
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

#### <a name="on-the-target-node-import-the-certs-private-key-as-a-trusted-root"></a>Célcsomóponton: a tanúsítvány titkos kulcsot a megbízható legfelső szintű importálása
```powershell
# Import to the root store so that it is trusted
$mypwd = ConvertTo-SecureString -String "YOUR_PFX_PASSWD" -Force -AsPlainText
Import-PfxCertificate -FilePath "$env:temp\DscPrivateKey.pfx" -CertStoreLocation Cert:\LocalMachine\My -Password $mypwd > $null
```

## <a name="configuration-data"></a>Konfigurációs adatok

A konfigurációs adatok blokk határozza meg, mely célcsomópontokat működik, hogy-e, vagy nem a hitelesítő adatokat, az azt jelenti, hogy a titkosítás és egyéb információk titkosítására. A konfigurációs adatok blokk további információkért lásd: [elválasztó konfigurációs és környezeti adatok](configData.md).

A hitelesítő adatok titkosítás kapcsolódó, az egyes csomópontok konfigurálható elemek a következők:
* **Csomópontnév** -a célcsomópont a hitelesítő adatok titkosításához a konfigurálni kívánt nevét.
* **PsDscAllowPlainTextPassword** - e a titkosított hitelesítő adatokat kell átadni ebben a csomópontban engedélyezve lesz. Ez az **nem ajánlott**.
* **Ujjlenyomat** – a felhasználó hitelesítő adatait a DSC-konfiguráció visszafejtése a használt tanúsítvány ujjlenyomata a _Célcsomóponttal_. **Ezt a tanúsítványt a helyi számítógép tanúsítványtárolójába a léteznie kell.**
* **CertificateFile** – a Tanúsítványfájl (csak a nyilvános kulcsot tartalmazó), amely a hitelesítő adatok titkosításához használandó a _Célcsomóponttal_. Ez lehet akár egy DER kódolású bináris X.509 vagy Base-64 kódolású X.509 formátum tanúsítványfájlt.

Ez a példa bemutatja egy konfigurációs adatblokk meghatározza, hogy a célcsomóponton való működésre elnevezett célcsomópont, a nyilvános kulcs tanúsítványfájljából (nevű targetNode.cer), és az ujjlenyomat a nyilvános kulcs elérési útja.

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


## <a name="configuration-script"></a>Konfigurációs parancsfájl

A konfigurációs parancsfájl önmagában, használja a `PsCredential` győződjön meg arról, hogy a hitelesítő adatokat kell tárolni a lehető legrövidebb idő alatt a paramétert. A megadott példa futtatásakor DSC kéri a hitelesítő adatokat, és majd titkosíthatja a MOF-fájlt, a társított konfigurációs adatblokk a célcsomóponton CertificateFile használatával. Ez a Kódpélda másolja át a fájl egy védett megosztást egy felhasználó számára.

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

## <a name="setting-up-decryption"></a>Visszafejtési beállítása

Mielőtt [ `Start-DscConfiguration` ](https://technet.microsoft.com/en-us/library/dn521623.aspx) is működik, hogy mely tanúsítványokat használja a hitelesítő adatok visszafejtése közölje a helyi Configuration Manager minden egyes cél csomóponton a CertificateID erőforrás ellenőrzése a tanúsítvány ujjlenyomata segítségével. Ez a példa funkció megkeresi a megfelelő helyi tanúsítvány (lehetséges, hogy testre szabhatja, így a pontos használni kívánt tanúsítványt keres, megtalálja a):

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

A tanúsítvány annak ujjlenyomata által azonosított a konfigurációs parancsfájl frissíthető értéket használja:

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

## <a name="running-the-configuration"></a>A konfiguráció futtatása

Ezen a ponton a konfigurációt, amely kimeneteként két fájlt is futtathatja:

 * A *. meta.mof fájl, amely a helyi Configuration Manager visszafejtése a hitelesítő adatokat, a tanúsítványt használ, amely a helyi számítógép tárolójában tárolja, és annak ujjlenyomata által azonosított konfigurálja. [`Set-DscLocalConfigurationManager`](https://technet.microsoft.com/en-us/library/dn521621.aspx)alkalmazza a *. meta.mof fájlt.
 * A MOF-fájlt, amely ténylegesen konfigurációjának alkalmazására szolgál. Start-DscConfiguration konfigurációjának alkalmazására szolgál.

Ezek a parancsok érnek el ezeket a lépéseket:

```powershell
Write-Host "Generate DSC Configuration..."
CredentialEncryptionExample -ConfigurationData $ConfigData -OutputPath .\CredentialEncryptionExample

Write-Host "Setting up LCM to decrypt credentials..."
Set-DscLocalConfigurationManager .\CredentialEncryptionExample -Verbose 
 
Write-Host "Starting Configuration..."
Start-DscConfiguration .\CredentialEncryptionExample -wait -Verbose
```

Ebben a példában a DSC-konfiguráció célcsomóponton való miatt.
A DSC-konfiguráció alkalmazható DSC lekéréses kiszolgálót használ, ha elérhető ilyen.

Lásd: [ügyféltelepítéshez DSC lekérési](pullClient.md) további információt a DSC-konfigurációk használata a DSC lekérési kiszolgálójával alkalmazása.

## <a name="credential-encryption-module-example"></a>Hitelesítő adatok titkosítás modul – példa

Íme egy teljes példa, amely magában foglalja a teljes ezeket a lépéseket, valamint segítő parancsmag exportálja, és másolja át a nyilvános kulcsok:

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

