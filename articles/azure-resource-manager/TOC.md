# Overzicht
## [Wat is Resource Manager?](resource-group-overview.md)
## [Ondersteunde services](resource-manager-supported-services.md)
## [Resource Manager en klassieke implementatie](resource-manager-deployment-model.md)
## [Abonnementsgovernance](resource-manager-subscription-governance.md)
## [Beheerde toepassingen](managed-application-overview.md)

# Aan de slag
## [Sjabloon exporteren](resource-manager-export-template.md)
## [Uw eerste sjabloon maken](resource-manager-create-first-template.md)
## [Visual Studio met Resource Manager](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md)

# Voorbeelden
## PowerShell
### [Sjabloon implementeren](resource-manager-samples-powershell-deploy.md)

## Azure CLI
### [Sjabloon implementeren](resource-manager-samples-cli-deploy.md)

# Procedures
## Sjablonen maken
### [Aanbevolen procedures voor sjablonen](resource-manager-template-best-practices.md)
### [Sjabloonsecties](resource-group-authoring-templates.md)
### [Koppeling naar andere sjablonen](resource-group-linked-templates.md)
### [Afhankelijkheid tussen resources definiëren](resource-group-define-dependencies.md)
### [Meerdere exemplaren maken](resource-group-create-multiple.md)
### [Locatie instellen](resource-manager-template-location.md)
### [Tags toewijzen](resource-manager-template-tags.md)
### [Naam en type van onderliggende resource instellen](resource-manager-template-child-resource.md)
### [Bron bijwerken](resource-manager-update.md)
### [Objecten voor parameters gebruiken](resource-manager-objects-as-parameters.md)
### [Status delen tussen gekoppelde sjablonen](best-practices-resource-manager-state.md)
### [Patronen voor het ontwerpen van sjablonen](best-practices-resource-manager-design-templates.md)

## Implementeren
### PowerShell
#### [Sjabloon implementeren](resource-group-template-deploy.md)
#### [Persoonlijke sjabloon met SAS-token implementeren](resource-manager-powershell-sas-token.md)
#### [Sjabloon exporteren en opnieuw distribueren](resource-manager-export-template-powershell.md)
### Azure CLI
#### [Sjabloon implementeren](resource-group-template-deploy-cli.md)
#### [Persoonlijke sjabloon met SAS-token implementeren](resource-manager-cli-sas-token.md)
#### [Sjabloon exporteren en opnieuw distribueren](resource-manager-export-template-cli.md)
### [Portal](resource-group-template-deploy-portal.md)
### [REST-API](resource-group-template-deploy-rest.md)
### [Implementatie in meerdere resourcegroepen](resource-manager-cross-resource-group-deployment.md)
### [Doorlopende integratie met Visual Studio Team Services](../vs-azure-tools-resource-groups-ci-in-vsts.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json)
### [Beveiligde waarden doorgeven tijdens implementatie](resource-manager-keyvault-parameter.md)

## Beheren
### [PowerShell](powershell-azure-resource-manager.md)
### [Azure CLI](xplat-cli-azure-resource-manager.md)
### [Portal](resource-group-portal.md)
### [REST-API](resource-manager-rest-api.md)
### [Tags gebruiken om resources te organiseren](resource-group-using-tags.md)
### [Resources verplaatsen naar nieuwe groep of abonnement](resource-group-move-resources.md)
### [Voorbeelden governance](resource-manager-subscription-examples.md)

## Toegang beheren
### Een service-principal maken
#### [PowerShell](resource-group-authenticate-service-principal.md)
#### [Azure CLI 2.0](/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json)
#### [Azure CLI 1.0](resource-group-authenticate-service-principal-cli.md)
#### [Portal](resource-group-create-service-principal-portal.md)
### [Verificatie-API om toegang te krijgen tot abonnementen](resource-manager-api-authentication.md)
### [Resources vergrendelen](resource-group-lock-resources.md)

## Resourcebeleid instellen
### [Wat is een resourcebeleid?](resource-manager-policy.md)
### [Beleidstoewijzing portal](resource-manager-policy-portal.md)
### [Beleidstoewijzing script](resource-manager-policy-create-assign.md)
### [Beleid voor resourcetags](resource-manager-policy-tags.md)
### [Opslagbeleid](resource-manager-policy-storage.md)
### [Beleid voor virtuele Linux-machines](../virtual-machines/linux/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json)
### [Beleid voor virtuele Windows-machines](../virtual-machines/windows/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json)

## Beheerde toepassingen gebruiken
### [Beheerde toepassing publiceren](managed-application-publishing.md)
### [Beheerde toepassing gebruiken](managed-application-consumption.md)
### [Interfacedefinities maken](managed-application-createuidefinition-overview.md)

## Controleren
### [Activiteitenlogboeken bekijken](resource-group-audit.md)
### [Implementatiebewerkingen bekijken](resource-manager-deployment-operations.md)

## Problemen oplossen
### [Veelvoorkomende implementatiefouten](resource-manager-common-deployment-errors.md)

# Naslaginformatie
## [Sjabloonindeling](/azure/templates/)
## [Sjabloonfuncties](resource-group-template-functions.md)
### [Matrix- en objectfuncties](resource-group-template-functions-array.md)
### [Vergelijkingsfuncties](resource-group-template-functions-comparison.md)
### [Implementatiefuncties](resource-group-template-functions-deployment.md)
### [Numerieke functies](resource-group-template-functions-numeric.md)
### [Resourcefuncties](resource-group-template-functions-resource.md)
### [Tekenreeksfuncties](resource-group-template-functions-string.md)
## [Functies voor interfacedefinitie](managed-application-createuidefinition-functions.md)
## [Elementen voor interfacedefinitie](managed-application-createuidefinition-elements.md)
### [Microsoft.Common.DropDown](managed-application-microsoft-common-dropdown.md)
### [Microsoft.Common.FileUpload](managed-application-microsoft-common-fileupload.md)
### [Microsoft.Common.OptionsGroup](managed-application-microsoft-common-optionsgroup.md)
### [Microsoft.Common.PasswordBox](managed-application-microsoft-common-passwordbox.md)
### [Microsoft.Common.Section](managed-application-microsoft-common-section.md)
### [Microsoft.Common.TextBox](managed-application-microsoft-common-textbox.md)
### [Microsoft.Compute.CredentialsCombo](managed-application-microsoft-compute-credentialscombo.md)
### [Microsoft.Compute.SizeSelector](managed-application-microsoft-compute-sizeselector.md)
### [Microsoft.Compute.UserNameTextBox](managed-application-microsoft-compute-usernametextbox.md)
### [Microsoft.Network.PublicIpAddressCombo](managed-application-microsoft-network-publicipaddresscombo.md)
### [Microsoft.Network.VirtualNetworkCombo](managed-application-microsoft-network-virtualnetworkcombo.md)
### [Microsoft.Storage.MultiStorageAccountCombo](managed-application-microsoft-storage-multistorageaccountcombo.md)
### [Microsoft.Storage.StorageAccountSelector](managed-application-microsoft-storage-storageaccountselector.md)
## [PowerShell](/powershell/module/azurerm.resources)
## [Azure CLI](/cli/azure/resource)
## [.NET](/dotnet/api/microsoft.azure.management.resourcemanager)
## [Java](/java/api/com.microsoft.azure.management.resources)
## [Python](http://azure-sdk-for-python.readthedocs.io/en/latest/resourcemanagement.html)
## [REST](/rest/api/resources/)

# Resources
## [Beperkingsaanvragen](resource-manager-request-limits.md)
## [Asynchrone bewerkingen bijhouden](resource-manager-async-operations.md)
## [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-resource-manager)
## [Video's](https://azure.microsoft.com/documentation/videos/index/?services=azure-resource-manager)
## [Service-updates](https://azure.microsoft.com/updates/?product=azure-resource-manager)
