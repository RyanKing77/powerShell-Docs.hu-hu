---
ms.date: 10/31/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: A MOF-fájl biztonságossá tétele
ms.openlocfilehash: 6c2aadb75ac617d9b845ef387f292b8156bb8889
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62079341"
---
# <a name="securing-the-mof-file"></a>A MOF-fájl biztonságossá tétele

> A következőkre vonatkozik: Windows PowerShell 4.0-s, a Windows PowerShell 5.0

DSC MOF-fájlt, ahol a helyi Configuration Manager (LCM) valósítja meg a kívánt cél állapot tárolt adatokat alkalmazása a konfigurációs kiszolgáló-csomópontok kezeli.
Ez a fájl tartalmazza a konfigurációs részleteit, mivel fontos tárolja biztonságos helyen.
Ez a témakör ismerteti, hogyan ellenőrizhető a célcsomópont a fájl titkosított.

PowerShell 5.0-s verzió verziótól kezdve a teljes MOF-fájl titkosítva van alapértelmezés szerint a csomópontra történő alkalmazásakor a `Start-DSCConfiguration` parancsmagot.
Ebben a cikkben ismertetett folyamatot kötelező, csak akkor, ha a lekéréses szolgáltatás protokoll használatával, ha a tanúsítványok nem felügyeli, a célcsomópont a letöltött konfigurációk visszafejteni, valamint lépésük előtt olvassa el a rendszer megoldás megvalósítása (például a Windows Server rendszerben elérhető lekéréses szolgáltatás).
Regisztrált csomópontok [Azure Automation DSC](https://docs.microsoft.com/azure/automation/automation-dsc-overview) automatikusan rendelkezik tanúsítványok telepítve van, és nincs adminisztrációs terhelést és a szolgáltatás által kezelt szükséges.

> [!NOTE]
> Ez a témakör ismerteti a titkosításhoz használt tanúsítvány.
> A titkosításhoz önaláírt tanúsítvány elegendő, mert a titkos kulcs titkos kulcs és a titkosítás mindig adatért nem jelenti azt, a dokumentum megbízhatósági.
> Önaláírt tanúsítványokat kell *nem* hitelesítési célokra használhatók.
> Hitelesítési célú tanúsítványt a megbízható hitelesítésszolgáltató (CA) kell használnia.

## <a name="prerequisites"></a>Előfeltételek

Sikerült titkosítani a DSC-konfiguráció védelmére használt hitelesítő adatokat, győződjön meg arról, hogy rendelkezik az alábbiakkal:

- **Néhány azt jelenti, hogy kiállító és tanúsítványok terjesztésére**. Ez a témakör és a példák azt feltételezik, az Active Directory-hitelesítésszolgáltatót használ. Az Active Directory tanúsítványszolgáltatások további háttér információ: [Active Directory tanúsítványszolgáltatások áttekintése](https://technet.microsoft.com/library/hh831740.aspx) és [Active Directory tanúsítványszolgáltatások a Windows Server 2008](https://technet.microsoft.com/windowsserver/dd448615.aspx).
- **A cél-csomóponthoz vagy csomópontokhoz a rendszergazdai hozzáférést**.
- **Minden egyes célcsomóponttal rendelkezik egy titkosítási képességgel tanúsítványt a személyes Store mentett**. A Windows PowerShell a tároló elérési útja a Cert: \LocalMachine\My. Ebben a témakörben szereplő példák az "munkaállomás-hitelesítési" sablon, amely annak (és más tanúsítványsablonokat) használatát [alapértelmezett tanúsítványsablonokat](https://technet.microsoft.com/library/cc740061(v=WS.10).aspx).
- Ha fog futni a konfiguráció a célcsomópont webkiszolgálótól eltérő számítógépen található **a tanúsítvány nyilvános kulcsának exportálásához**, majd importálja a számítógépen, a konfigurációt az futtatni fogja. Győződjön meg arról, hogy exportálja csak a **nyilvános** kulcs; a titkos kulcs biztonságának megőrzése.

## <a name="overall-process"></a>Általános folyamata

 1. Állítsa be a tanúsítványok, kulcsok és ujjlenyomatok, így arról, hogy minden cél csomópont van a tanúsítvány másolatát, és konfigurációs van-e a nyilvános kulcs és ujjlenyomatát.
 2. Hozzon létre egy konfigurációs adatblokk, amely tartalmazza az elérési út és a nyilvános kulcs ujjlenyomata.
 3. Hozzon létre egy konfigurációs parancsfájl, amely határozza meg a célcsomópont kívánt konfigurációját, és úgy, mint a helyi konfigurációs visszafejtési a cél-csomópontokon beállít manager visszafejteni a konfigurációs adatokat, a tanúsítvány és az ujjlenyomat használatával.
 4. Futtassa a konfiguráció, amely a helyi Configuration Manager beállításait, és indítsa el a DSC-konfiguráció.

![Diagram1](../images/CredentialEncryptionDiagram1.png)

## <a name="certificate-requirements"></a>Tanúsítványkövetelmények

Hitelesítő adatok titkosításához kihirdeti, hogy a nyilvános kulcsú tanúsítvány elérhetőnek kell lennie a _Célcsomóponttal_ , amely **megbízható** a DSC-konfiguráció létrehozásához használja a számítógép által.
A nyilvános kulcsú tanúsítvány ahhoz, hogy a DSC-hitelesítő adatok titkosításához használni meghatározott követelményekkel rendelkezik:

1. **Kulcshasználat**:
   - Tartalmaznia kell: "KeyEncipherment" és "DataEncipherment".
   - Érdemes _nem_ tartalmazza: "A digitális aláírás".
2. **Kibővített kulcshasználat**:
   - Tartalmaznia kell: A dokumentum titkosítása (1.3.6.1.4.1.311.80.1).
   - Érdemes _nem_ tartalmazza: Ügyfél-hitelesítés (1.3.6.1.5.5.7.3.2) és a kiszolgálói hitelesítés (1.3.6.1.5.5.7.3.1).
3. A tanúsítvány titkos kulcsa megtalálható a * cél Node_.
4. A **szolgáltató** a tanúsítványt a "Microsoft RSA SChannel Cryptographic Provider" kell lennie.

> [!IMPORTANT]
> Bár a kulcs használatát "Digitális aláírás" vagy a hitelesítési EKU valamelyik tartalmazó tanúsítványt is használ, ez lehetővé teszi a titkosítási kulcsot hibásan használt és téve a támadás könnyebben törhetők fel. Ezért ajánlott ezek kulcshasználat és az EKU-k az áttekinthetőség kedvéért kihagyja kifejezetten a DSC-hitelesítő adatok védelme céljából létrehozott tanúsítványt használjon.

Minden meglévő tanúsítványt a _Célcsomóponttal_ , hogy megfelel-e ezek a feltételek segítségével biztonságos DSC hitelesítő adatokat.

## <a name="certificate-creation"></a>Tanúsítvány létrehozása

Kétféleképpen hozhat létre és használhat a szükséges titkosítási tanúsítvány (nyilvános-titkos kulcspárt) is igénybe vehet.

1. Hozza létre a **Célcsomóponttal** , és csak a nyilvános kulcsának exportálásához a **szerzői csomópont**
2. Hozza létre a **szerzői csomópont** és a teljes kulcspár, exportálhatja a **Célcsomóponttal**

1. módszer használata javasolt, mert mindig célcsomóponton marad a titkos kulcs használatával fejti vissza az MOF hitelesítő adatait.

### <a name="creating-the-certificate-on-the-target-node"></a>A tanúsítvány létrehozásakor a célcsomóponton

A titkos kulcs titkos, mert fejti vissza az MOF meg kell tartani a **Célcsomóponttal** ennek legegyszerűbb módja az, hogy a titkos kulcsú tanúsítvány létrehozása a a **Célcsomóponttal**, és másolja a  **nyilvános kulcsú tanúsítvány** a MOF-fájlba a DSC-konfiguráció létrehozásához használt számítógépre.
Az alábbi példában:

1. a tanúsítványt hoz létre a **célcsomóponttal**
2. a nyilvános kulcsú tanúsítvány exportálása a **célcsomóponttal**.
3. a nyilvános kulcsú tanúsítványt importál a **saját** tanúsítványtárolójába a **szerzői műveletek csomópont**.

#### <a name="on-the-target-node-create-and-export-the-certificate"></a>A cél csomóponton: hozzon létre, és exportálja a tanúsítványt

> Cél csomópont: Windows Server 2016 és Windows 10

```powershell
# note: These steps need to be performed in an Administrator PowerShell session
$cert = New-SelfSignedCertificate -Type DocumentEncryptionCertLegacyCsp -DnsName 'DscEncryptionCert' -HashAlgorithm SHA256
# export the public key certificate
$cert | Export-Certificate -FilePath "$env:temp\DscPublicKey.cer" -Force
```

Az exportált egyszer, a `DscPublicKey.cer` kellene kell másolni a **szerzői csomópont**.

> Cél csomópont: A Windows Server 2012 R2 vagy Windows 8.1 és korábbi
> [!WARNING]
> Mivel a `New-SelfSignedCertificate` nem támogatják a parancsmag a Windows operációs rendszerek a Windows 10 és Windows Server 2016 előtt a **típus** paraméter, ez a tanúsítvány létrehozása egy alternatív módszer megadása szükséges. az említett operációs rendszerektől.
>
> Ebben az esetben használhatja `makecert.exe` vagy `certutil.exe` a tanúsítvány létrehozásához.
>
>Egy alternatív módszer [a New-SelfSignedCertificateEx.ps1 szkript letöltése a Microsoft Script Center](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6) , és ezzel hozzon létre helyette a tanúsítványt:

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

Az exportált egyszer, a ```DscPublicKey.cer``` kellene kell másolni a **szerzői csomópont**.

#### <a name="on-the-authoring-node-import-the-certs-public-key"></a>A szerzői műveletek csomóponton: importálja a tanúsítvány nyilvános kulcsa

```powershell
# Import to the my store
Import-Certificate -FilePath "$env:temp\DscPublicKey.cer" -CertStoreLocation Cert:\LocalMachine\My
```

### <a name="creating-the-certificate-on-the-authoring-node"></a>A tanúsítvány létrehozása az Authoring Tool csomóponton

Azt is megteheti, a titkosítási tanúsítvány hozható létre a a **szerzői csomópont**, az exportált a **titkos kulcs** , egy PFX fájlt, és ezután importálja, amelyen a **Célcsomóponttal**.
Ez a végrehajtási DSC hitelesítő adatok titkosításához az aktuális mód _Nano Server_.
Bár a PFX-jelszó védi, meg kell őrizni biztonságos átvitel során.
Az alábbi példában:

1. a tanúsítványt hoz létre a **szerzői műveletek csomópont**.
2. exportálja a tanúsítványt a titkos kulcs is a **szerzői műveletek csomópont**.
3. eltávolítja a titkos kulcsot a a **szerzői műveletek csomópont**, de megőrzi a nyilvános kulcsú tanúsítvány a **saját** tárolásához.
4. importálja a titkos kulcsú tanúsítványt a My(Personal) tanúsítványtárolójába a a **célcsomóponttal**.
   - azt hozzá kell adni a legfelső szintű tárolójában, hogy a rendszer megbízható a **célcsomóponttal**.

#### <a name="on-the-authoring-node-create-and-export-the-certificate"></a>A szerzői műveletek csomóponton: hozzon létre, és exportálja a tanúsítványt

> Cél csomópont: Windows Server 2016 és Windows 10

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

Az exportált egyszer, a `DscPrivateKey.pfx` kell átmásolni a **Célcsomóponttal**.

> Cél csomópont: A Windows Server 2012 R2 vagy Windows 8.1 és korábbi
> [!WARNING]
> Mivel a `New-SelfSignedCertificate` nem támogatják a parancsmag a Windows operációs rendszerek a Windows 10 és Windows Server 2016 előtt a **típus** paraméter, ez a tanúsítvány létrehozása egy alternatív módszer megadása szükséges. az említett operációs rendszerektől.
>
> Ebben az esetben használhatja `makecert.exe` vagy `certutil.exe` a tanúsítvány létrehozásához.
>
> Egy alternatív módszer [a New-SelfSignedCertificateEx.ps1 szkript letöltése a Microsoft Script Center](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6) , és ezzel hozzon létre helyette a tanúsítványt:

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

#### <a name="on-the-target-node-import-the-certs-private-key-as-a-trusted-root"></a>A cél csomóponton: importálja a tanúsítványt a titkos kulcsot a megbízható legfelső szintű

```powershell
# Import to the root store so that it is trusted
$mypwd = ConvertTo-SecureString -String "YOUR_PFX_PASSWD" -Force -AsPlainText
Import-PfxCertificate -FilePath "$env:temp\DscPrivateKey.pfx" -CertStoreLocation Cert:\LocalMachine\My -Password $mypwd > $null
```

## <a name="configuration-data"></a>Konfigurációs adatok

A konfigurációs adatok blokk határozza meg, melyik célcsomópontok alapján, hogy e, vagy nem a hitelesítő adatokat, az azt jelenti, hogy a titkosítás és egyéb információk titkosítására. A konfigurációs adatok blokk további információkért lásd: [szétválasztása konfigurációs és környezeti adatok](../configurations/configData.md).

Hitelesítőadat-titkosítás kapcsolatos, az egyes csomópontok konfigurálható elemek a következők:

- **NodeName** – a célcsomópont a hitelesítő adatok titkosításához a konfigurálni kívánt nevét.
- **PsDscAllowPlainTextPassword** - e a titkosítatlan hitelesítő adatok adható át ezen a csomóponton engedélyezni. Ez a **nem ajánlott**.
- **Ujjlenyomat** -a a DSC-konfiguráció a hitelesítő adatok visszafejtése a használt tanúsítvány ujjlenyomatát a _Célcsomóponttal_. **Ezt a tanúsítványt a helyi számítógép tanúsítványtárolójába a léteznie kell.**
- **CertificateFile** – a tanúsítványfájlt (csak a nyilvános kulcsot tartalmazó), amely a hitelesítő adatok titkosításához használandó a _Célcsomóponttal_. Ez lehet akár egy DER kódolású bináris X.509 vagy Base-64 kódolású X.509 formátumú tanúsítványfájlt.

Ez a példa bemutatja egy konfigurációs adatblokk, amely meghatározza egy célcsomóponttal való működésre az elnevezett targetNode, a nyilvános kulcsú tanúsítványfájlra (nevű targetNode.cer), és az ujjlenyomatot a nyilvános kulcs elérési útját.

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

Magát a konfigurációs parancsfájlt, használja a `PsCredential` paraméter segítségével győződjön meg arról, hogy a lehető legrövidebb idő alatt a hitelesítő adatokat tárolja. A megadott példa futtatásakor DSC kéri a hitelesítő adatokat, és majd titkosíthatja a MOF-fájlt a CertificateFile társított a célcsomópont a konfigurációs adatok blokk használatával. Ez a Kódpélda másol egy fájlt egy felhasználó védett megosztásból.

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

## <a name="setting-up-decryption"></a>A visszafejtés beállítása

Mielőtt [ `Start-DscConfiguration` ](https://technet.microsoft.com/library/dn521623.aspx) is működik, meg kell mondanunk a helyi Configuration Manager a cél-csomópontokon melyik tanúsítványt használja a hitelesítő adatok visszafejtése a CertificateID erőforrás segítségével ellenőrizze a tanúsítvány ujjlenyomata. Ez a példa a függvény megkeresi a megfelelő helyi tanúsítvány (szükség lehet testre szabni, így megtalálja a pontos tanúsítványt használni kívánt):

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

Az ujjlenyomat által azonosított tanúsítvánnyal a konfigurációs parancsfájl frissíthető értéket használja:

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

Ezen a ponton a konfigurációt, mivel a két fájlt kimenete futtathatja:

- A *. meta.mof fájlt, amely a hitelesítő adatok használatával, amely a helyi számítógép tárolóban tárolja, és azonosítja az ujjlenyomata a tanúsítvány visszafejtése a Local Configuration Manager konfigurálja. [`Set-DscLocalConfigurationManager`](https://technet.microsoft.com/library/dn521621.aspx) alkalmazza a *. meta.mof fájlt.
- MOF-fájlt, amely ténylegesen konfigurációjának alkalmazására szolgál. Start-DscConfiguration konfigurációjának alkalmazására szolgál.

Ezek a parancsok érnek el ezeket a lépéseket:

```powershell
Write-Host "Generate DSC Configuration..."
CredentialEncryptionExample -ConfigurationData $ConfigData -OutputPath .\CredentialEncryptionExample

Write-Host "Setting up LCM to decrypt credentials..."
Set-DscLocalConfigurationManager .\CredentialEncryptionExample -Verbose

Write-Host "Starting Configuration..."
Start-DscConfiguration .\CredentialEncryptionExample -wait -Verbose
```

Ebben a példában a DSC-konfiguráció miatt a cél csomópontra.
A DSC-konfiguráció használata a DSC lekéréses kiszolgálón, ha elérhető is alkalmazható.

Lásd: [DSC lekérési ügyfél beállítása](pullClient.md) további információt a DSC-konfigurációk DSC lekéréses kiszolgálót használ.

## <a name="credential-encryption-module-example"></a>Hitelesítő adatok titkosítási modul példa

Íme egy teljes példa, amely tartalmazza a teljes ezeket a lépéseket, valamint egy segítő parancsmag, amely exportálja, és másolja a nyilvános kulcsokat:

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
