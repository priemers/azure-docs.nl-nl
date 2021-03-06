---
title: 'Overzicht van VPN Gateway: cross-premises VPN-verbindingen met virtuele Azure-netwerken maken| Microsoft Docs'
description: In dit overzicht van VPN Gateway worden de manieren besproken waarop u met een VPN-verbinding via internet verbinding kunt maken met een virtueel Azure-netwerk. U vindt hier ook schema&quot;s van basisverbindingsconfiguraties.
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 2358dd5a-cd76-42c3-baf3-2f35aadc64c8
ms.service: vpn-gateway
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/04/2017
ms.author: cherylmc
ms.translationtype: Human Translation
ms.sourcegitcommit: a3ca1527eee068e952f81f6629d7160803b3f45a
ms.openlocfilehash: afef396c17c62f5b980ac1ffdbfc7a7db7a8cdd2
ms.contentlocale: nl-nl
ms.lasthandoff: 04/27/2017


---
# <a name="about-vpn-gateway"></a>Informatie over VPN-gateway
Als u netwerkverkeer wilt verzenden tussen uw virtuele Azure-netwerk en uw on-premises site, moet u een virtuele netwerkgateway voor uw virtuele netwerk maken. Een VPN-gateway is een soort gateway voor virtuele netwerken die versleuteld verkeer verzendt via een openbare verbinding. U kunt VPN-gateways ook gebruiken om verkeer tussen virtuele Azure-netwerken te verzenden via het Microsoft-netwerk.

Er zijn twee types virtuele netwerkgateway's: 'ExpressRoute' en 'VPN'. Wanneer u een virtuele netwerkgateway maakt, geeft u het gatewaytype aan dat u wilt maken. Een VPN-gateway is een virtuele netwerkgateway die gebruikmaakt van het gatewaytype 'VPN'. 

Elk virtueel netwerk kan twee virtuele netwerkgateways hebben, maar slechts één van elk type. Afhankelijk van de instellingen die u kiest, kunt u meerdere verbindingen maken voor één VPN-gateway. Een voorbeeld hiervan is een configuratie met meerdere siteverbindingen. Wanneer u meerdere verbindingen naar dezelfde VPN-gateway hebt gemaakt, delen alle VPN-tunnels, met inbegrip van punt-naar-site-VPN-verbindingen, de bandbreedte die voor de gateway beschikbaar is.

## <a name="configuring-a-vpn-gateway"></a>Een VPN-gateway configureren
Een VPN-gatewayverbinding is afhankelijk van meerdere resources die zijn geconfigureerd met specifieke instellingen. De meeste resources kunnen afzonderlijk worden geconfigureerd, hoewel ze in sommige gevallen in een bepaalde volgorde moeten worden geconfigureerd.

###<a name="settings"></a>Instellingen
De instellingen die u voor elke resource hebt gekozen, zijn essentieel om een geslaagde verbinding te maken. Zie voor meer informatie over afzonderlijke resources en de instellingen voor VPN Gateway [Over VPN Gateway-instellingen](vpn-gateway-about-vpn-gateway-settings.md). Hier vindt u meer uitleg over de gatewaytypen, typen VPN-verbindingen, gatewaysubnetten, lokale netwerkgateways en verschillende andere resource-instellingen die u misschien wilt gebruiken.

###<a name="deployment-tools"></a>Implementatiehulpmiddelen
U kunt beginnen met het maken en configureren van resources met een configuratiehulpprogramma, zoals Azure Portal. U kunt later alsnog besluiten over te schakelen naar een ander hulpprogramma, zoals PowerShell, om aanvullende resources te configureren, of om desgewenst bestaande bronnen te wijzigen. Op dit moment is het niet mogelijk om elke resource en resource-instelling in Azure Portal te configureren. De instructies in de artikelen voor elke verbindingstopologie geven aan of een specifiek confihuratiehulpprogramma nodig is. 

###<a name="deployment-model"></a>Implementatiemodel
Wanneer u een VPN-gateway configureert, zijn de stappen die u moet volgen, afhankelijk van het implementatiemodel waarmee u het virtuele netwerk hebt gemaakt. Als u bijvoorbeeld uw VNet hebt gemaakt met het klassieke implementatiemodel, gebruikt u de richtlijnen en instructies voor het klassieke implementatiemodel om de VPN-gateway te maken en de instellingen te configureren. Zie [Het Resource Manager-implementatiemodel en het klassieke implementatiemodel begrijpen](../azure-resource-manager/resource-manager-deployment-model.md) voor meer informatie over de implementatiemodellen.

## <a name="diagrams"></a>Diagrammen over de verbindingstopologie
Het is belangrijk te weten dat er verschillende configuraties beschikbaar zijn voor VPN-gatewayverbindingen. U moet bepalen welke configuratie het beste aansluit bij uw behoeften. In de gedeelten hieronder kunt u informatie en topologiediagrammen over de volgende VPN-gatewayverbindingen bekijken. In de tabellen worden de volgende zaken weergegeven:

* Beschikbaar implementatiemodel
* Beschikbare configuratiehulpprogramma's
* Rechtstreekse koppelingen naar een artikel, indien beschikbaar

Gebruik de diagrammen en beschrijvingen als hulp bij het selecteren van de juiste verbindingstopologie voor uw vereisten. De diagrammen tonen de belangrijkste basistopologieën, maar het is mogelijk om met de diagrammen als richtlijn complexere configuraties te bouwen.

## <a name="site-to-site-and-multi-site-ipsecike-vpn-tunnel"></a>Site-naar-site en multi-site (IPsec-/IKE VPN-tunnel)
### <a name="S2S"></a>Site-naar-site
Een site-naar-site-VPN-gatewayverbinding (S2S) is een verbinding via een VPN-tunnel met IPsec/IKE (IKEv1 of IKEv2). Voor dit type verbinding moet er een VPN-apparaat on-premises aanwezig zijn waaraan een openbaar IP-adres is toegewezen en dat zich niet achter een NAT bevindt. S2S-verbindingen kunnen worden gebruikt voor cross-premises en hybride configuraties.   

![Voorbeeld van een site-naar-site-verbinding met Azure VPN Gateway](./media/vpn-gateway-about-vpngateways/vpngateway-site-to-site-connection-diagram.png)

### <a name="Multi"></a>Multi-site
Dit type verbinding is een variatie op de site-naar-site-verbinding. U maakt meer dan één VPN-verbinding vanaf uw virtuele netwerkgateway, meestal met verschillende on-premises sites. Als u met meerdere verbindingen werkt, moet u een op een route gebaseerd VPN-type (ook bekend als een dynamische gateway voor klassieke VNets) gebruiken. Omdat elk virtueel netwerk maar één VPN-gateway kan hebben, delen alle verbindingen via de gateway de beschikbare bandbreedte. Dit wordt vaak een multi-site-verbinding genoemd.

![Voorbeeld van een verbinding tussen meerdere locaties met Azure VPN Gateway](./media/vpn-gateway-about-vpngateways/vpngateway-multisite-connection-diagram.png)

### <a name="deployment-models-and-methods-for-site-to-site-and-multi-site"></a>Implementatiemodellen en -methoden voor site-naar-site en multi-site
[!INCLUDE [vpn-gateway-table-site-to-site](../../includes/vpn-gateway-table-site-to-site-include.md)]

## <a name="P2S"></a>Punt-naar-site (VPN via SSTP)
Met een punt-naar-site (P2S)-VPN-gatewayverbinding kunt u vanuit een afzonderlijke clientcomputer een beveiligde verbinding maken met uw virtueel netwerk. P2S is een VPN-verbinding via SSTP (Secure Socket Tunneling Protocol). Voor P2S-verbindingen hebt u geen VPN-apparaat of openbaar IP-adres nodig. U kunt de VPN-verbinding maken door deze vanaf de clientcomputer te starten. Dit is een uitstekende oplossing als u uw VNet vanaf een externe locatie, zoals vanaf thuis of een conferentie, wilt verbinden, of wanneer u slechts enkele clients hebt die verbinding moeten maken met een VNet. P2S-verbindingen kunnen worden gebruikt met S2S-verbindingen via dezelfde VPN-gateway, mits alle configuratievereisten voor beide verbindingen compatibel zijn.

![Voorbeeld van een punt-naar-site-verbinding met Azure VPN Gateway](./media/vpn-gateway-about-vpngateways/vpngateway-point-to-site-connection-diagram.png)

### <a name="deployment-models-and-methods-for-point-to-site"></a>Implementatiemodellen en -methoden voor punt-naar-site
[!INCLUDE [vpn-gateway-table-point-to-site](../../includes/vpn-gateway-table-point-to-site-include.md)]

## <a name="V2V"></a>VNet-naar-VNet-verbindingen (IPsec-/IKE VPN-tunnel)
Het verbinden van een virtueel netwerk met een ander virtueel netwerk (VNet-naar-VNet) lijkt op het verbinden van een VNet met een on-premises locatie. Voor beide connectiviteitstypen wordt een VPN-gateway gebruikt om een beveiligde tunnel met IPsec/IKE te bieden. U kunt zelfs VNet-naar-VNet-communicatie met multi-site-verbindingsconfiguraties combineren. Zo kunt u netwerktopologieën maken waarin cross-premises connectiviteit is gecombineerd met connectiviteit tussen virtuele netwerken.

U kunt de volgende VNets verbinden:

* in dezelfde of verschillende regio's
* in dezelfde of verschillende abonnementen 
* in dezelfde of verschillende implementatiemodellen

![Voorbeeld van een VNet-naar-VNet-verbinding met Azure VPN Gateway](./media/vpn-gateway-about-vpngateways/vpngateway-vnet-to-vnet-connection-diagram.png)

###<a name="connections-between-deployment-models"></a>Verbindingen tussen implementatiemodellen
Azure heeft momenteel twee implementatiemodellen: klassiek en Resource Manager. Als u al langer met Azure hebt gewerkt, hebt u waarschijnlijk Azure-VM's en -rolinstanties in een klassiek VNet. De nieuwere VM's en rolinstanties werken mogelijk in een VNet dat is gemaakt in Resource Manager. U kunt de VNets verbinden zodat de resources in het ene VNet direct met de resources in het andere kunnen communiceren.

###<a name="vnet-peering"></a>VNet-peering
Zolang het virtuele netwerk voldoet aan bepaalde vereisten, kunt u VNet-peering gebruiken om uw verbinding te maken. Bij VNet-peering wordt geen virtuele netwerkgateway gebruikt. Zie het artikel [VNet-peering](../virtual-network/virtual-network-peering-overview.md) voor meer informatie.

###<a name="deployment-models-and-methods-for-vnet-to-vnet"></a>Implementatiemodellen en -methoden voor VNet-naar-VNet
[!INCLUDE [vpn-gateway-table-vnet-to-vnet](../../includes/vpn-gateway-table-vnet-to-vnet-include.md)]

## <a name="ExpressRoute"></a>ExpressRoute (exclusieve privéverbinding)
Met Microsoft Azure ExpressRoute kunt u uw on-premises netwerken in de Microsoft Cloud uitbreiden via een speciale persoonlijke verbinding die wordt gefaciliteerd door een connectiviteitsprovider. Met ExpressRoute kunt u verbindingen tot stand brengen met Microsoft Cloud-services, zoals Microsoft Azure, Office 365 en CRM Online. Via een connectiviteitsprovider in een co-locatiefaciliteit is connectiviteit mogelijk vanuit een any-to-any (IP VPN) netwerk, een point-to-point Ethernet-netwerk of een virtuele overlappende verbinding.

ExpressRoute-verbindingen gaan niet via het openbare internet. Daardoor zijn ExpressRoute-verbindingen betrouwbaarder en sneller en hebben ze lagere latenties en betere beveiliging dan gewone verbindingen via internet.

Een ExpressRoute-verbinding gebruikt geen VPN-gateway. Er wordt echter wel een virtuele netwerkgateway gebruikt als onderdeel van de vereiste configuratie. In een ExpressRoute-verbinding wordt de virtuele netwerkgateway geconfigureerd met het gatewaytype 'ExpressRoute' in plaats van 'VPN'. Zie [Technical Overview](../expressroute/expressroute-introduction.md) (Technisch overzicht) voor meer informatie over ExpressRoute.

## <a name="coexisting"></a>Site-naar-site- en ExpressRoute-verbindingen naast elkaar
ExpressRoute is een directe, exclusieve verbinding van uw WAN (niet via het openbare internet) met Microsoft-services, waaronder Azure. Site-naar-site-VPN-verkeer verplaatst zich versleuteld via het openbare internet. De mogelijkheid om site-naar-site-VPN- en ExpressRoute-verbindingen voor hetzelfde virtuele netwerk te configureren, heeft verschillende voordelen.

U kunt een site-naar-site-VPN configureren als een beveiligd failoverpad voor ExpressRoute of site-naar-site-VPN’s gebruiken om verbinding te maken met sites die geen deel uitmaken van uw netwerk, maar zijn verbonden via ExpressRoute. Houd er rekening mee dat deze configuratie twee gateways vereist voor hetzelfde virtuele netwerk, één met gatewaytype 'VPN' en de andere met gatewaytype 'ExpressRoute'.

![Voorbeeld van ExpressRoute en VPN Gateway in eenzelfde implementatie](./media/vpn-gateway-about-vpngateways/expressroute-vpngateway-coexisting-connections-diagram.png)

### <a name="deployment-models-and-methods-for-s2s-and-expressroute"></a>Implementatiemodellen en -methoden voor S2S en ExpressRoute
[!INCLUDE [vpn-gateway-table-coexist](../../includes/vpn-gateway-table-coexist-include.md)]

## <a name="pricing"></a>Prijzen
[!INCLUDE [vpn-gateway-about-pricing-include](../../includes/vpn-gateway-about-pricing-include.md)]

## <a name="gateway-skus"></a>Gateway-SKU's
[!INCLUDE [vpn-gateway-gwsku-include](../../includes/vpn-gateway-gwsku-include.md)]

Zie [Gateway-SKU's](vpn-gateway-about-vpn-gateway-settings.md#gwsku) voor meer informatie over gateway-SKU's voor VPN Gateway.

### <a name="estimated-aggregate-throughput-by-sku"></a>Geschatte geaggregeerde doorvoer per SKU
[!INCLUDE [vpn-gateway-table-gwtype-aggthroughput](../../includes/vpn-gateway-table-gwtype-aggtput-include.md)]

## <a name="faq"></a>Veelgestelde vragen

Zie [Veelgestelde vragen VPN Gateway](vpn-gateway-vpn-faq.md) voor veelgestelde vragen over VPN Gateway.

## <a name="next-steps"></a>Volgende stappen
- De VPN-gatewayconfiguratie plannen. Zie [Planning en ontwerp voor VPN Gateway](vpn-gateway-plan-design.md).
- Zie de [Veelgestelde vragen over VPN Gateway](vpn-gateway-vpn-faq.md) voor meer informatie.
- Zie de [Abonnements- en servicebeperkingen](../azure-subscription-service-limits.md#networking-limits).


