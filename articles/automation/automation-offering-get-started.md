---
title: Aan de slag met Azure Automation | Microsoft Docs
description: Als voorbereiding om de service aan te bieden via Azure Marketplace, vindt u in dit artikel een overzicht van de Azure Automation-service. Hier worden de belangrijkste concepten en implementatiegegevens doorgenomen.
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/02/2017
ms.author: magoedte
ms.translationtype: Human Translation
ms.sourcegitcommit: 97fa1d1d4dd81b055d5d3a10b6d812eaa9b86214
ms.openlocfilehash: 9b4982ffece9283304ad3ab3c82a471ac1dbd463
ms.contentlocale: nl-nl
ms.lasthandoff: 05/11/2017

---

## <a name="getting-started-with-azure-automation"></a>Aan de slag met Azure Automation

Deze introductiehandleiding introduceert de belangrijkste concepten met betrekking tot de implementatie van Azure Automation. Als u niet bekend bent met Automation in Azure of ervaring hebt met werkstroomautomatiseringssoftware als System Center Orchestrator, zal deze handleiding u helpen om aan de slag te gaan met concepten en implementatiegerelateerde details.

## <a name="key-concepts"></a>Belangrijkste concepten

### <a name="automation-service"></a>Automation-service
Automation is een Azure-service die gebruikmaakt van Windows PowerShell en Azure-technologieën om u te helpen het beheer van uw Azure-, cloud- en on-premises-infrastructuur en -toepassingen te controleren.  Met Azure Automation kunt u de volledige levenscyclus van uw services en toepassingen beheren met behulp van geautomatiseerde implementatie met procesautomatisering, besturingssysteemconfiguratie met PowerShell Desired State Configuration, voortdurende updates en controle met updatebeheer en Wijzigingen bijhouden, en geautomatiseerde probleemoplossing en herstel.

### <a name="automation-account"></a>Automation-account
Een Automation-account is een Azure-resource die u maakt.  U kunt al uw Azure-, cloud- en on-premises resources beheren met één Automation-account.  Een Automation-account is een container voor de items die u voor Automation moet maken: runbooks, modules, assets zoals referenties en schema's, en configuraties. U kunt meerdere Automation-accounts gebruiken als u resources wilt scheiden in afzonderlijke logische omgevingen, zoals ontwikkeling, testen en productie, of in geografische regio's.  

### <a name="hybrid-runbook-worker"></a>Hybrid Runbook Worker
Als u runbooks wilt uitvoeren op fysieke of virtuele systemen in uw lokale datacentrum, Azure of andere cloudprovider, kunt u deze lokale resources met de functie Hybrid Runbook Worker openen en beheren.     

### <a name="automation-desired-state-configuration"></a>Automation Desired State Configuration
Met Automation Desired State Configuration (DSC), gebaseerd op PowerShell DSC, kunt u de gewenste status van uw besturingssystemen die worden gehost in Azure, on-premises of in een andere cloud, configureren, controleren en automatisch bijwerken.  

### <a name="management-solutions"></a>Beheeroplossingen
Beheeroplossingen, zoals Updates beheren en Wijzigingen bijhouden, breiden de functionaliteit van Azure Automation uit; ze worden gebruikt met Log Analytics.  Ze kunnen worden toegepast op meerdere bronnen die een bepaald beheerscenario ondersteunen, zoals Automation-runbooks, vooraf gedefinieerde Log Analytics-zoekquery's en -waarschuwingen, en visualisaties.  

## <a name="architecture-overview"></a>Overzicht van de architectuur

Azure Automation is een SaaS-toepassing (Software als een service) die een schaalbare en betrouwbare multitenant-omgeving biedt om processen met runbooks te automatiseren en configuratiewijzigingen op Windows- en Linux-systemen te beheren met Desired State Configuration (DSC) in Azure, andere cloudservices of on-premises. Entiteiten in uw Automation-account, zoals runbooks, assets en Uitvoeren als-accounts, zijn geïsoleerd van andere Automation-accounts in uw abonnement en andere abonnementen.  

Runbooks die u uitvoert in Azure, worden uitgevoerd op Automation-sandboxes, die op het Azure-platform als een virtuele PaaS-machine (platform als een service) worden gehost.  Automation-sandboxes bieden isolatie van tenants voor alle aspecten van de uitvoering van runbooks: modules, opslag, geheugen, netwerkcommunicatie, taakstromen enzovoort. Deze rol wordt beheerd door de service. U kunt deze niet beheren vanuit uw Azure- of Azure Automation-account.         

Als u de implementatie en het beheer van resources in uw lokale datacenter of andere cloudservices wilt automatiseren, kunt u een of meer computers aanwijzen om de HRW-rol (Hybrid Runbook Worker) uit te voeren.  Op elke HRW moet de Microsoft Management Agent (MMA) zijn geïnstalleerd. Deze moet een verbinding hebben met een Log Analytics-werkruimte en een Automation-account.  Log Analytics wordt gebruikt om de installatie te starten, de MMA-agent te onderhouden en de functionaliteit van de HRW te controleren.  De levering van runbooks en de instructie om ze uit te voeren, worden verzorgd door Azure Automation.

U kunt meerdere HRW’s implementeren voor hoge beschikbaarheid voor uw runbooks, voor een gelijkmatige verdeling van runbooktaken en (in sommige gevallen) om ze toe te wijzen aan bepaalde workloads of omgevingen.  HRW communiceert met de Automation-service via uitgaande TCP-poort 443.  Wanneer er een runbook op een HRW in uw datacenter wordt uitgevoerd en u het runbook ook beheertaken voor andere computers of services in het datacenter wilt laten uitvoeren, moet u het runbook mogelijk ook toegang geven tot andere poorten.  Als het IT-beveiligingsbeleid niet toestaat dat computers in het netwerk verbinding maken met internet, raadpleegt u het artikel [OMS-gateway](../log-analytics/log-analytics-oms-gateway.md). De gateway fungeert als een proxy voor de HRW om taakstatusinformatie te verzamelen en configuratiegegevens van uw Automation-account te ontvangen.

Runbooks die op een HRW worden uitgevoerd, werken in de context van het lokale systeemaccount op de computer. Dit is de aanbevolen beveiligingscontext voor het uitvoeren van beheertaken op de lokale Windows-computer. Als u het runbook taken wilt laten uitvoeren voor resources buiten de lokale computer, moet u mogelijk beveiligde referentieassets in het Automation-account definiëren. U moet deze referenties vanuit het runbook kunnen gebruiken voor verificatie bij de externe resource. U kunt de assets [Referentie](automation-credentials.md), [Certificaat](automation-certificates.md) en [Verbinding](automation-connections.md) in uw runbook gebruiken met cmdlets waarmee u referenties kunt opgeven, zodat u ze kunt verifiëren.

DSC-configuraties die zijn opgeslagen in Azure Automation, kunnen rechtstreeks worden toegepast op virtuele Azure-machines. Voor andere fysieke en virtuele machines kunnen configuraties via de pull-server van Azure Automation DSC zijn vereist.  Voor het beheer van configuraties van uw on-premises fysieke of virtuele Windows- en Linux-systemen hoeft u geen infrastructuur te implementeren ter ondersteuning van de Automation DSC pull-server. U hoeft alleen uitgaande internettoegang in te stellen vanaf elk systeem dat u wilt beheren met Automation DSC en dat via TCP-poort 443 met de OMS-service communiceert.   

![Overzicht van Azure Automation](media/automation-offering-get-started/automation-infradiagram-networkcomms.png)

## <a name="prerequisites"></a>Vereisten

### <a name="automation-dsc"></a>Automation DSC
Azure Automation DSC kan worden gebruikt voor het beheer van verschillende machines:

* Virtuele machines van Azure (klassiek) met Windows of Linux
* Virtuele machines van Azure met Windows of Linux
* Virtuele AWS-machines (Amazon Web Services) met Windows of Linux
* Fysieke/virtuele Windows-computers on-premises of in een andere cloud dan Azure of AWS
* Fysieke/virtuele Linux-computers on-premises of in een andere cloud dan Azure of AWS

Op de PowerShell DSC-agent moet de meest recente versie van WMF 5 worden geïnstalleerd, anders kan Windows niet communiceren met Azure Automation. De meest recente versie van de [PowerShell DSC-agent voor Linux](https://www.microsoft.com/en-us/download/details.aspx?id=49150) moet worden geïnstalleerd, anders kan Linux niet communiceren met Azure Automation.

### <a name="hybrid-runbook-worker"></a>Hybrid Runbook Worker  
De computer waarop u hybride runbooktaken wilt uitvoeren, moet over het volgende beschikken:

* Windows Server 2012 of hoger
* Windows PowerShell 4.0 of hoger.  Voor extra betrouwbaarheid is het raadzaam om Windows PowerShell 5.0 op de computer te installeren. U kunt de nieuwe versie downloaden via het [Microsoft Downloadcentrum](https://www.microsoft.com/download/details.aspx?id=50395)
* Minimaal twee kernen
* Minimaal 4 GB aan RAM-geheugen

## <a name="security"></a>Beveiliging
Met Azure Automation kunt u taken automatiseren voor bronnen in Azure, on-premises en bij andere cloudproviders.  Om een runbook in staat te stellen de vereiste acties uit te voeren, moet het machtigingen hebben om veilig toegang te krijgen tot de resources met de minimale rechten die vereist zijn binnen het abonnement.  

### <a name="automation-account"></a>Automation-account
Alle automatiseringstaken die u met behulp van de Azure-cmdlets in Azure Automation voor resources uitvoert, moeten worden geverifieerd bij Azure met behulp van verificatie op basis van organisatie-identiteitreferenties van Azure Active Directory.  Een Automation-account is gescheiden van het account waarmee u zich aanmeldt bij de portal om Azure-resources te configureren en te gebruiken.  

De Automation-resources voor elk Automation-account zijn gekoppeld aan één Azure-regio, maar Automation-accounts kunnen alle resources in uw abonnement beheren. U kunt Automation-accounts in verschillende regio's maken als u te maken hebt met beleidsregels die bepalen dat gegevens en resources moeten worden geïsoleerd in een specifieke regio.

> [!NOTE]
> Automation-accounts, en de resources die deze bevatten die in de Azure-portal worden gemaakt, zijn niet toegankelijk via de klassieke Azure-portal. Als u deze accounts of de bijbehorende resources wilt beheren met Windows PowerShell, moet u gebruikmaken van de Azure Resource Manager-modules.
>

Wanneer u in Azure Portal een Automation-account maakt, worden er automatisch twee accounts gemaakt:

* Een Uitvoeren als-account. Door dit account worden een service-principal in Azure Active Directory (Azure AD) en een certificaat gemaakt. Ook wordt door dit account de inzender voor op rollen gebaseerd toegangsbeheer (RBAC) toegewezen, die resources van Resource Manager beheert met runbooks.
* Een klassiek Uitvoeren als-account. Door dit account wordt een beheercertificaat geüpload, dat wordt gebruikt om klassieke resources te beheren met runbooks.

Op rollen gebaseerd toegangsbeheer is beschikbaar in Azure Resource Manager voor het toekennen van toegestane acties aan een Azure AD-gebruikersaccount en Uitvoeren als-account, en om die service-principal te verifiëren.  Lees het artikel [Op rollen gebaseerd toegangsbeheer in Azure Automation](automation-role-based-access-control.md) voor meer informatie die u helpt bij het ontwikkelen van een model voor het beheren van machtigingen in Automation.  

#### <a name="authentication-methods"></a>Verificatiemethoden
De volgende tabel bevat een overzicht van de verschillende verificatiemethoden voor elke omgeving die wordt ondersteund door Azure Automation.

| Methode | Omgeving
| --- | --- |
| Uitvoeren als-account van Azure en klassiek Uitvoeren als-account |Azure Resource Manager en klassieke Azure-implementatie |  
| Azure AD-gebruikersaccount |Azure Resource Manager en klassieke Azure-implementatie |  
| Windows-verificatie |Lokaal datacenter of een andere cloudprovider met de Hybrid Runbook Worker |  
| AWS-referenties |Amazon Web Services |  

In de sectie **Procedures\Verificatie en beveiliging** vindt u ondersteunende artikelen met een overzicht en de implementatiestappen om verificatie te configureren voor deze omgevingen, met een bestaand account of een nieuw account dat u speciaal aan die omgeving hebt toegewezen.  Voor het Uitvoeren als-account van Azure en het klassieke Uitvoeren als-account raadpleegt u het onderwerp [Update Automation Run As account using PowerShell](automation-update-account-powershell.md) (Automation Uitvoeren als-account bijwerken met PowerShell). Hierin wordt beschreven hoe u een bestaand Automation-account met een Uitvoeren als-account bijwerkt met behulp van PowerShell als het oorspronkelijk niet is geconfigureerd met een Uitvoeren als- of klassiek Uitvoeren als-account.   

## <a name="network"></a>Netwerk
De Hybrid Runbook Worker kan alleen verbinding maken met en zich registreren bij Microsoft Operations Management Suite (OMS) als het toegang heeft tot het poortnummer en de URL's die hieronder worden beschreven.  Dit is in aanvulling op de [poorten en URL's die vereist zijn voor de Microsoft Monitoring Agent](../log-analytics/log-analytics-windows-agents.md) om verbinding te maken met OMS. Als u een proxyserver gebruikt voor communicatie tussen de agent en de OMS-service, moet u controleren of de juiste resources toegankelijk zijn. Als u een firewall gebruikt om toegang tot internet te beperken, moet u uw firewall zodanig configureren dat toegang wordt toegestaan.

In de onderstaande informatie vindt u de poort en URL's die nodig zijn om de Hybrid Runbook Worker te laten communiceren met Automation.

* Poort: alleen TCP 443 is vereist voor uitgaande toegang tot internet
* Algemene URL: *.azure-automation.net

Als u een Automation-account voor een specifieke regio hebt gedefinieerd en de communicatie met dat regionaal datacenter wilt beperken, vindt u in de volgende tabel de DNS-record voor elke regio.

| **Regio** | **DNS-record** |
| --- | --- |
| Zuid-centraal VS |scus-jobruntimedata-prod-su1.azure-automation.net |
| VS - oost 2 |eus2-jobruntimedata-prod-su1.azure-automation.net |
| West-centraal VS | wcus-jobruntimedata-prod-su1.azure-automation.net |
| West-Europa |we-jobruntimedata-prod-su1.azure-automation.net |
| Noord-Europa |ne-jobruntimedata-prod-su1.azure-automation.net |
| Canada - midden |cc-jobruntimedata-prod-su1.azure-automation.net |
| Zuidoost-Azië |sea-jobruntimedata-prod-su1.azure-automation.net |
| Centraal-India |cid-jobruntimedata-prod-su1.azure-automation.net |
| Japan - oost |jpe-jobruntimedata-prod-su1.azure-automation.net |
| Australië - zuidoost |ase-jobruntimedata-prod-su1.azure-automation.net |
| Verenigd Koninkrijk Zuid | uks-jobruntimedata-prod-su1.azure-automation.net |
| VS (overheid) - Virginia | usge-jobruntimedata-prod-su1.azure-automation.us |

Voor een lijst met IP-adressen in plaats van namen downloadt en bekijkt u het XML-bestand met [Azure-datacenter-IP-adressen](https://www.microsoft.com/download/details.aspx?id=41653) in het Microsoft Downloadcentrum.

> [!NOTE]
> Dit bestand bevat de IP-adresbereiken (inclusief bereiken voor Compute, SQL en Storage) die worden gebruikt in de Microsoft Azure-datacenters. Er wordt wekelijks een bijgewerkt bestand geplaatst waarin staat welke bereiken momenteel zijn geïmplementeerd en welke wijzigingen in de toekomst aan de IP-bereiken zullen worden aangebracht. Nieuwe bereiken in het bestand worden gedurende ten minste één week nog niet in de datacenters gebruikt. Download elke week het nieuwe XML-bestand en voer de benodigde wijzigingen uit op uw site om de services die in Azure worden uitgevoerd correct te identificeren. Express Route-gebruikers zullen merken dat dit bestand wordt gebruikt om in de eerste week van elke maand de BGP-advertenties van Azure-ruimte bij te werken.
>


## <a name="implementation"></a>Implementatie

### <a name="creating-an-automation-account"></a>Een Automation-account maken

Er zijn verschillende manieren waarop u in Azure Portal een Automation-account kunt maken.  In de volgende tabel worden de diverse typen implementatie-ervaring en de verschillen daartussen geïntroduceerd.  

|Methode | Beschrijving |
|-------|-------------|
| Selecteer Automation en besturing in Marketplace | Een aanbieding waarmee een Automation-account en een OMS-werkruimte worden gemaakt die zijn gekoppeld in dezelfde resourcegroep en regio.  Hiermee worden standaard ook de oplossingen Wijzigingen bijhouden en Updatebeheer geïmplementeerd. |
| Selecteer Automation in Marketplace | Hiermee wordt in een nieuwe of bestaande resourcegroep een Automation-account gemaakt dat niet is gekoppeld aan een OMS-werkruimte en geen beschikbare oplossingen bevat uit de aanbieding Automation en beheer. Dit is een basisconfiguratie om kennis te maken met Automation en te leren hoe u runbooks schrijft, DSC configureert en de mogelijkheden van de service gebruikt. |
| Geselecteerde beheeroplossingen | Als u een oplossing selecteert (**[Updatebeheer](../operations-management-suite/oms-solution-update-management.md)**, **[VM's buiten de bedrijfsuren starten/stoppen](automation-solution-vm-management.md)** of **[Wijzigingen bijhouden](../log-analytics/log-analytics-change-tracking.md)**), wordt u gevraagd een bestaande Automation- en OMS-werkruimte te selecteren of krijgt u de mogelijkheid om beide te maken als dat nodig is voor de oplossing die u in uw abonnement wilt implementeren. |

In dit onderwerp doorloopt u de stappen voor het maken van een Automation-account en de OMS-werkruimte door de aanbieding Automation en beheer te implementeren.  Als u een zelfstandig Automation-account wilt maken om de service te testen of te bekijken, raadpleegt u het artikel [Create standalone Automation account](automation-create-standalone-account.md) (Een zelfstandig Automation-account maken).  

### <a name="create-automation-account-integrated-with-log-analytics"></a>Een Automation-account maken dat is geïntegreerd met Log Analytics
De aanbevolen methode om Automation te implementeren, is door de aanbieding Automation en beheer te selecteren in Marketplace.  In dat geval wordt dan zowel een Automation-account gemaakt als de integratie met een OMS-werkruimte tot stand gebracht. Daarnaast krijgt u de mogelijkheid om de beheeroplossingen te installeren die met de aanbieding beschikbaar zijn.  

>[!NOTE]
>Voor het maken van een Automation-account moet u lid zijn van de rol Servicebeheerders of medebeheerder zijn van het abonnement dat toegang verleent tot het abonnement. U moet ook als gebruiker worden toegevoegd aan het standaard Active Directory-exemplaar van dat abonnement. Aan het account hoeft geen bevoorrechte rol te worden toegewezen.
>
>Als u geen lid bent van het Active Directory-exemplaar van het abonnement voordat u wordt toegevoegd aan de rol van medebeheerder van het abonnement, wordt u als gast toegevoegd aan Active Directory. In dat geval wordt de waarschuwing 'U hebt geen machtigingen voor het maken...' weergegeven op de blade **Automation-account toevoegen**.
>
>Gebruikers die zijn toegevoegd aan de rol Medebeheerder, kunnen worden verwijderd uit het Active Directory-exemplaar van het abonnement en opnieuw worden toegevoegd, zodat ze een volledige gebruiker worden in Active Directory. U kunt deze situatie controleren in het deelvenster **Azure Active Directory** in Azure Portal door **Gebruikers en groepen** te selecteren. Selecteer vervolgens **Alle gebruikers**, daarna de specifieke gebruiker en tot slot **Profiel**. De waarde van het kenmerk **Gebruikerstype** onder het gebruikersprofiel mag niet gelijk zijn aan **Gast**.

1. Meld u aan bij Azure Portal met een account dat lid is van de rol Abonnementsbeheerders en dat medebeheerder is van het abonnement.

2. Klik op **Nieuw**.<br><br> ![De optie Nieuw selecteren in Azure Portal](media/automation-offering-get-started/automation-portal-martketplacestart.png)<br>  

3. Zoek naar **Automation** en klik in de zoekresultaten op **Automation en beheer***.<br><br> ![Zoek naar en selecteer Automation en beheer in Marketplace](media/automation-offering-get-started/automation-portal-martketplace-select-automationandcontrol.png).<br>   

4. Lees de beschrijving van de aanbieding en klik op **Maken**.  

5. Selecteer op de blade met instellingen voor **Automation en beheer** de optie **OMS-werkruimte**.  Selecteer op de blade **OMS-werkruimte** een OMS-werkruimte die is gekoppeld aan hetzelfde Azure-abonnement als dat van het Automation-account of maak een nieuwe OMS-werkruimte.  Als u geen OMS-werkruimte hebt, selecteert u **Nieuwe werkruimte maken** en voert u op de blade **OMS-werkruimte** het volgende uit:
   - Geef een naam op voor de nieuwe **OMS-werkruimte**.
   - Selecteer een **abonnement** om te koppelen door een selectie in de vervolgkeuzelijst te maken als de geselecteerde standaardwaarde niet juist is.
   - Voor **Resourcegroep** kunt u een resourcegroep maken of een bestaande resourcegroep selecteren.  
   - Selecteer een **locatie**.  Momenteel zijn alleen de locaties **Australië - zuidoost**, **VS - oost**, **Zuidoost-Azië**, **West-centraal VS** en **West-Europa** beschikbaar.
   - Selecteer een **prijscategorie**.  De oplossing wordt in twee prijscategorieën aangeboden: Gratis en Per knooppunt (OMS).  De gratis categorie heeft een limiet op de hoeveelheid gegevens die dagelijks wordt verzameld, op de retentieperiode en op de runtimeminuten van runbooktaken.  De categorie Per knooppunt (OMS) kent geen limiet voor de hoeveelheid gegevens die dagelijks wordt verzameld.  
   - Selecteer **Automation-account**.  Als u een nieuwe OMS-werkruimte maakt, moet u ook een Automation-account maken dat is gekoppeld aan de nieuwe OMS-werkruimte die eerder is opgegeven, inclusief uw Azure-abonnement, resourcegroep en regio.  U kunt **Een Automation-account maken** selecteren en het volgende opgeven op de blade **Automation-account**:
  - Voer in het veld **Naam** de naam van het Automation-account in.

    Alle overige opties worden automatisch ingevuld op basis van de geselecteerde OMS-werkruimte. Deze opties kunnen niet worden gewijzigd.  Een Uitvoeren als-account van Azure is de standaardmethode voor verificatie voor de aanbieding.  Nadat u op **OK** hebt geklikt, worden de configuratieopties gevalideerd en wordt het Automation-account gemaakt.  U kunt de voortgang bijhouden onder **Meldingen** in het menu.

    Selecteer anders een bestaand Automation Uitvoeren als-account.  Het account dat u selecteert, mag nog niet aan een andere OMS-werkruimte zijn gekoppeld, anders wordt er een melding op de blade weergegeven.  Als het account al is gekoppeld, moet u een ander Automation Uitvoeren als-account selecteren of een account maken.

    Klik na het opgeven van de vereiste informatie op **Maken**.  De informatie wordt gecontroleerd en het Automation-Account en Uitvoeren als-account worden gemaakt.  U keert automatisch terug naar de blade **OMS-werkruimte**.  

6. Nadat u de vereiste gegevens hebt opgegeven op de blade **OMS-werkruimte**, klikt u op **Maken**.  Terwijl de gegevens worden geverifieerd en de werkruimte wordt gemaakt, kunt u de voortgang bijhouden onder **Meldingen** in het menu.  U keert terug naar de blade **Oplossing toevoegen**.  

7. Op de blade **Automation en beheer** bevestigt u dat u de aanbevolen vooraf geselecteerde oplossingen wilt installeren. Als u een oplossing uitschakelt, kunt u deze later afzonderlijk installeren.  

8. Klik op **Maken** om verder te gaan met de implementatie van Automation en een OMS-werkruimte. Alle instellingen worden gecontroleerd en daarna wordt geprobeerd de aanbieding in uw abonnement te implementeren.  Dit proces kan enkele seconden duren en u kunt de voortgang bijhouden onder **Meldingen** in het menu.

Wanneer de aanbieding is geïmplementeerd, kunt u runbooks gaan maken, de beheeroplossingen gebruiken die u hebt ingeschakeld of aan de slag gaan met [Log Analytics](https://docs.microsoft.com/azure/log-analytics) en gegevens verzamelen die zijn gegenereerd door resources in uw cloud- of on-premises omgeving.   

## <a name="next-steps"></a>Volgende stappen
* Raadpleeg [Runbooks verifiëren met een Azure Uitvoeren als-account](automation-verify-runas-authentication.md) als u wilt controleren of uw nieuwe Azure Automation-account kan worden geverifieerd met Azure-resources.
* Zie [Mijn eerste PowerShell-runbook](automation-first-runbook-textual-powershell.md) om aan de slag te gaan met PowerShell-runbooks.
* Zie voor meer informatie over grafisch ontwerpen [Grafisch ontwerpen in Azure Automation](automation-graphical-authoring-intro.md).

