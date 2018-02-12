# [Áttekintés](overview.md)

## [A célállapot-konfiguráció áttekintése döntéshozók számára](decisionMaker.md)

## [A célállapot-konfiguráció áttekintése mérnökök számára](DscForEngineers.md)

## [DSC – első lépések](quickStart.md)

# [Konfigurációk](configurations.md)

## [Konfigurációk életbe léptetése](enactingConfigurations.md)

## [Konfigurációs és környezeti adatok szétválasztása](separatingEnvData.md)

## [Eltérő verziójú erőforrások használata](sxsResource.md)

## [A DSC futtatása felhasználói hitelesítő adatokkal](runAsUser.md)

## [Csomópontok közötti függőségek megadása](crossNodeDependencies.md)

## [Konfigurációs adatok](configData.md)

### [A konfigurációs adatok hitelesítőadat-beállításai](configDataCredentials.md)

## [Konfigurációs adatok beágyazása](compositeConfigs.md)

## [A konfigurációs MOF-fájl biztonságossá tétele](secureMOF.md)

## [Részleges konfigurációk](partialConfigs.md)

## [DSC-konfigurációk súgóinak összeállítása](configHelp.md)

## [Virtuális gép konfigurálása DSC-vel az első indításkor](bootstrapDsc.md)

### [DSCAutomationHostEnabled beállításkulcs](DSCAutomationHostEnabled.md)

# [Erőforrások](resources.md)

## [Beépített erőforrások](builtInResource.md)

### [Archív erőforrás](archiveResource.md)

### [Környezeti erőforrás](environmentResource.md)

### [File erőforrás](fileResource.md)

### [Group erőforrás](groupResource.md)

### [GroupSet erőforrás](groupSetResource.md)

### [Log erőforrás](logResource.md)

### [Package erőforrás](packageResource.md)

### [ProcessSet erőforrás](processSetResource.md)

### [Registry erőforrás](registryResource.md)

### [Script erőforrás](scriptResource.md)

### [Service erőforrás](serviceResource.md)

### [ServiceSet erőforrás](serviceSetResource.md)

### [User erőforrás](userResource.md)

### [WaitForAllResource](waitForAllResource.md)

### [WaitForAnyResource](waitForAnyResource.md)

### [WaitForSomeResource](waitForSomeResource.md)

### [WindowsFeature erőforrás](windowsfeatureResource.md)

### [WindowsFeatureSet erőforrás](windowsFeatureSetResource.md)

### [WindowsOptionalFeature erőforrás](windowsOptionalFeatureResource.md)

### [WindowsOptionalFeatureSet erőforrás](windowsOptionalFeatureSetResource.md)

### [WindowsPackageCab erőforrás](windowsPackageCabResource.md)

### [WindowsProcess erőforrás](windowsProcessResource.md)

## [Egyéni erőforrások készítése](authoringResource.md) 

### [MOF-alapú egyéni erőforrások](authoringResourceMOF.md)

#### [MOF-alapú erőforrás C#-ban](authoringResourceMofCS.md)

### [Osztályalapú egyéni erőforrások](authoringResourceClass.md)

### [Összetett erőforrások](authoringResourceComposite.md)

### [Egypéldányos DSC-erőforrás írása (ajánlott eljárás)](singleInstance.md)

### [Erőforrás-készítési ellenőrzőlista](resourceAuthoringChecklist.md)

## [ DSC-erőforrások hibakeresése](debugResource.md)

## [DSC-erőforrások metódusainak közvetlen hívása](directCallResource.md)

# Local Configuration Manager

## [A Local Configuration Manager (LCM) konfigurálása](metaConfig.md)

## [Az LCM konfigurálása a PowerShell 4.0-ban](metaConfig4.md)

# A DSC lekéréses modellje

## [DSC Pull Service](pullServer.md)

## [A DSC SMB-lekérési kiszolgálójának beállítása](pullServerSMB.md)

## [Lekérési ügyfél beállítása](pullClient.md)

### [Lekérési ügyfél beállítása konfigurációs nevekkel](pullClientConfigNames.md)

### [Lekérési ügyfél beállítása konfigurációs azonosítóval](pullClientConfigID.md)

## [A DSC jelentéskészítő kiszolgálójának használata](reportServer.md)

## [Lekérési kiszolgáló – ajánlott eljárások](secureServer.md)

# [DSC-példák](dscExamples.md)

## [Folyamatos integrációs és folyamatos üzembe helyezési folyamat fejlesztése a DSC, a Pester és a Visual Studio Team Services szolgáltatással](dscCiCd.md)

## [Konfigurációs és környezeti adatok szétválasztása](separatingEnvData.md)

# [A DSC hibaelhárítása](troubleshooting.md)

# [A DSC használata a Nano Serveren](nanoDsc.md)

# DSC Linuxon

## [Linuxhoz készült DSC – első lépések](lnxGettingStarted.md)

## [Linuxos beépített erőforrások](lnxBuiltInResources.md)

### [nxArchive erőforrás](lnxArchiveResource.md)

### [nxEnvironment erőforrás](lnxEnvironmentResource.md)

### [nxFile erőforrás](lnxFileResource.md)

### [nxFileLine erőforrás](lnxFileLineResource.md)

### [nxGroup erőforrás](lnxGroupResource.md)

### [nxPackage erőforrás](lnxPackageResource.md)

### [nxService erőforrás](lnxServiceResource.md)

### [nxSshAuthorizedKeys erőforrás](lnxSshAuthorizedKeysResource.md)

### [nxUser erőforrás](lnxUserResource.md)

# [A DSC használata a Microsoft Azure-ban](azureDsc.md)

# DSC MOF – referencia

## [MSFT_DSCLocalConfigurationManager osztály](msft-dsclocalconfigurationmanager.md)

### [Az MSFT_DSCLocalConfigurationManager osztály ApplyConfiguration metódusa](msft-dsclocalconfigurationmanager-applyconfiguration.md)

### [Az MSFT_DSCLocalConfigurationManager osztály DisableDebugConfiguration metódusa](msft-dsclocalconfigurationmanager-disabledebugconfiguration.md)

### [Az MSFT_DSCLocalConfigurationManager osztály EnableDebugConfiguration metódusa](msft-dsclocalconfigurationmanager-enabledebugconfiguration.md)

### [Az MSFT_DSCLocalConfigurationManager osztály GetConfiguration metódusa](msft-dsclocalconfigurationmanager-getconfiguration.md)

### [Az MSFT_DSCLocalConfigurationManager osztály GetConfigurationResultOutput metódusa](msft-dsclocalconfigurationmanager-getconfigurationresultoutput.md)

### [Az MSFT_DSCLocalConfigurationManager osztály GetConfigurationStatus metódusa](msft-dsclocalconfigurationmanager-getconfigurationstatus.md)

### [Az MSFT_DSCLocalConfigurationManager osztály GetMetaConfiguration metódusa](msft-dsclocalconfigurationmanager-getmetaconfiguration.md)

### [Az MSFT_DSCLocalConfigurationManager osztály PerformRequiredConfigurationChecks metódusa](msft-dsclocalconfigurationmanager-performrequiredconfigurationchecks.md)

### [Az MSFT_DSCLocalConfigurationManager osztály RemoveConfiguration metódusa](msft-dsclocalconfigurationmanager-removeconfiguration.md)

### [Az MSFT_DSCLocalConfigurationManager osztály ResourceGet metódusa](msft-dsclocalconfigurationmanager-resourceget.md)

### [Az MSFT_DSCLocalConfigurationManager osztály ResourceSet metódusa](msft-dsclocalconfigurationmanager-resourceset.md)

### [Az MSFT_DSCLocalConfigurationManager osztály ResourceTest metódusa](msft-dsclocalconfigurationmanager-resourcetest.md)

### [Az MSFT_DSCLocalConfigurationManager osztály RollBack metódusa](msft-dsclocalconfigurationmanager-rollback.md)

### [Az MSFT_DSCLocalConfigurationManager osztály SendConfiguration metódusa](msft-dsclocalconfigurationmanager-sendconfiguration.md)

### [Az MSFT_DSCLocalConfigurationManager osztály SendConfigurationApply metódusa](msft-dsclocalconfigurationmanager-sendconfigurationapply.md)

### [Az MSFT_DSCLocalConfigurationManager osztály SendConfigurationApplyAsync metódusa](msft-dsclocalconfigurationmanager-sendconfigurationapplyasync.md)

### [Az MSFT_DSCLocalConfigurationManager osztály SendMetaConfigurationApply metódusa](msft-dsclocalconfigurationmanager-sendmetaconfigurationapply.md)

### [Az MSFT_DSCLocalConfigurationManager osztály StopConfiguration metódusa](msft-dsclocalconfigurationmanager-stopconfiguration.md)

### [Az MSFT_DSCLocalConfigurationManager osztály TestConfiguration metódusa](msft-dsclocalconfigurationmanager-testconfiguration.md)

# További források

## [Tanulmányok](whitepapers.md)
