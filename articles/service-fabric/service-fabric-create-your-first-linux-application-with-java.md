---
title: Uw eerste Azure-microservices-app in Linux maken met behulp van Java | Microsoft Docs
description: Een Service Fabric-toepassing maken en implementeren met behulp van Java
services: service-fabric
documentationcenter: java
author: seanmck
manager: timlt
editor: 
ms.assetid: 02b51f11-5d78-4c54-bb68-8e128677783e
ms.service: service-fabric
ms.devlang: java
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 01/05/2017
ms.author: seanmck
translationtype: Human Translation
ms.sourcegitcommit: 9553c9ed02fa198d210fcb64f4657f84ef3df801
ms.openlocfilehash: eedddf7a40acfba7513efd810d115f1afe2f224d
ms.lasthandoff: 03/23/2017


---
# <a name="create-your-first-azure-service-fabric-application"></a>Uw eerste Azure Service Fabric-toepassing maken
> [!div class="op_single_selector"]
> * [C# - Windows](service-fabric-create-your-first-application-in-visual-studio.md)
> * [Java - Linux](service-fabric-create-your-first-linux-application-with-java.md)
> * [C# - Linux](service-fabric-create-your-first-linux-application-with-csharp.md)
>
>

Service Fabric biedt SDK's voor het bouwen van services in Linux in zowel .NET Core als Java. In deze zelfstudie worden een toepassing voor Linux en een service gemaakt met behulp van Java.  

> [!NOTE]
> Java wordt als eersteklas ingebouwde programmeertaal alleen ondersteund voor het Linux-voorbeeld (ondersteuning in Windows wordt gepland). Alle toepassingen, waaronder Java-toepassingen, kunnen echter worden uitgevoerd als uitvoerbare gastbestanden of in containers op Windows of Linux. Zie voor meer informatie [Een bestaand uitvoerbaar bestand implementeren naar Azure Service Fabric](service-fabric-deploy-existing-app.md) en [Containers implementeren naar Service Fabric](service-fabric-deploy-container.md).
>

## <a name="video-tutorial"></a>Zelfstudievideo

De volgende video van Microsoft Virtual Academy leidt u door het proces voor het maken van een Java-app op een Linux-systeem:  
<center><a target="\_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=DOX8K86yC_206218965">  
<img src="./media/service-fabric-create-your-first-linux-application-with-java/LinuxVid.png" WIDTH="360" HEIGHT="244">  
</a></center>


## <a name="prerequisites"></a>Vereisten
Zorg voordat u begint ervoor dat u [uw Linux-ontwikkelingsomgeving hebt ingesteld](service-fabric-get-started-linux.md). Als u Mac OS X gebruikt, kunt u [een Linux one-box omgeving instellen op een virtuele machine met behulp van Vagrant](service-fabric-get-started-mac.md).

## <a name="create-the-application"></a>De toepassing maken
Een Service Fabric-toepassing kan een of meer services bevatten, elk met een specifieke functie met betrekking tot het leveren van de functionaliteit van de toepassing. De Service Fabric-SDK voor Linux bevat een [Yeoman](http://yeoman.io/)-generator waarmee u gemakkelijk uw eerste service kunt maken en er later meer kunt toevoegen. We gebruiken Yeoman om een toepassing te maken met één service.

1. Typ in een terminal ``yo azuresfjava``.
2. Geef uw toepassing een naam.
3. Kies het type van uw eerste service en geef de service een naam. In deze zelfstudie kiezen we voor een Reliable Actor Service.

   ![Service Fabric Yeoman-generator voor Java][sf-yeoman]

> [!NOTE]
> Zie [Service Fabric programming model overview](service-fabric-choose-framework.md) (Overzicht van het Service Fabric-programmeermodel) voor meer informatie over de opties.
>

## <a name="build-the-application"></a>De toepassing bouwen
De Service Fabric Yeoman-sjablonen bevatten een bouwscript voor [Gradle](https://gradle.org/), dat u kunt gebruiken om de app via de terminal te maken.

  ```bash
  cd myapp
  gradle
  ```

## <a name="deploy-the-application"></a>De toepassing implementeren
Als de toepassing is gemaakt, kunt u deze kunt implementeren in het lokale cluster met behulp van de Azure CLI.

1. Maak verbinding met het lokale cluster van Service Fabric.

    ```bash
    azure servicefabric cluster connect
    ```

2. Gebruik het installatiescript dat is opgegeven in de sjabloon om het toepassingspakket te kopiëren naar de installatiekopieopslag van het cluster, het toepassingstype te registreren en een exemplaar van de toepassing te maken.

    ```bash
    ./install.sh
    ```

3. Open een browser en navigeer naar de Service Fabric Explorer op http://localhost:19080/Explorer (vervang localhost door het privé IP-adres van de virtuele machine als u Vagrant in Mac OS X gebruikt).

4. Vouw het knooppunt Toepassingen uit. U ziet dat er nu een vermelding is voor uw toepassingstype en nog een voor het eerste exemplaar van dat type.

## <a name="start-the-test-client-and-perform-a-failover"></a>De testclient starten en een failover uitvoeren
Actorprojecten doen niets uit zichzelf. Ze hebben een andere service of client nodig die hen berichten stuurt. De actorsjabloon bevat een eenvoudig testscript dat u kunt gebruiken om te communiceren met de actorservice.

1. Voer het script uit met behulp van het controleprogramma om de uitvoer van de actorservice te bekijken.

    ```bash
    cd myactorsvcTestClient
    watch -n 1 ./testclient.sh
    ```

2. Zoek in Service Fabric Explorer het knooppunt op dat als host fungeert voor de primaire replica voor de actorservice. In de onderstaande schermafbeelding is dit knooppunt 3.

    ![Zoeken naar de primaire replica in Service Fabric Explorer][sfx-primary]

3. Klik op het knooppunt dat u hebt gevonden in de vorige stap en selecteer vervolgens **Deactiveren (opnieuw starten)** in het menu Acties. Met deze actie wordt een van de vijf knooppunten in uw lokale cluster opnieuw gestart en een failover afgedwongen op een van de secundaire replica's die worden uitgevoerd op een ander knooppunt. Let terwijl u deze actie uitvoert op de uitvoer van de testclient en houd er rekening mee dat de teller blijft toenemen ondanks de failover.

## <a name="create-and-deploy-an-application-with-the-eclipse-neon-plugin"></a>Een toepassing maken en implementeren met behulp van de invoegtoepassing Eclipse Neon

Service Fabric biedt u ook de mogelijkheid om de Service Fabric Java-toepassing te maken, te bouwen en te implementeren met behulp van Eclipse. Kies bij het installeren van Eclipse voor **Eclipse IDE voor Java-ontwikkelaars**. Service Fabric biedt momenteel ook ondersteuning voor de invoegtoepassing voor Eclipse **Neon**. Raadpleeg de gedetailleerde documentatie [Uw eerste Service Fabric Java-toepassing maken en implementeren met behulp van de Service Fabric-invoegtoepassing voor Eclipse op Linux](service-fabric-get-started-eclipse.md)

## <a name="adding-more-services-to-an-existing-application"></a>Meer services toevoegen aan een bestaande toepassing

### <a name="using-command-line-utility"></a>Met behulp van het opdrachtregelhulpprogramma
Voer de volgende stappen uit als u nog een service wilt toevoegen aan een toepassing die al is gemaakt met `yo`:
1. Stel de directory in op de hoofdmap van de bestaande toepassing.  Bijvoorbeeld `cd ~/YeomanSamples/MyApplication` als `MyApplication` de toepassing is die is gemaakt door Yeoman.
2. Voer `yo azuresfjava:AddService` uit.

### <a name="using-service-fabric-eclipse-plugin-for-java-on-linux"></a>De Service Fabric Eclipse-invoegtoepassing voor Java op Linux gebruiken
Als u service wilt toevoegen aan een bestaande toepassing die is gemaakt met behulp van de Eclipse-invoegtoepassing voor Service Fabric, raadpleegt u de documentatie [hier](service-fabric-get-started-eclipse.md#add-a-service-fabric-service-to-your-service-fabric-application).

## <a name="next-steps"></a>Volgende stappen
* [Uw eerste Service Fabric Java-toepassing maken en implementeren met behulp van de Service Fabric-invoegtoepassing voor Eclipse op Linux](service-fabric-get-started-eclipse.md)
* [Meer informatie over Reliable Actors](service-fabric-reliable-actors-introduction.md)
* [Interactie aangaan met Service Fabric-clusters met de Azure-CLI](service-fabric-azure-cli.md)
* [Problemen met implementatie oplossen](service-fabric-azure-cli.md#troubleshooting)
* Meer informatie over [ondersteuningsopties voor Service Fabric](service-fabric-support.md)

<!-- Images -->
[sf-yeoman]: ./media/service-fabric-create-your-first-linux-application-with-java/sf-yeoman.png
[sfx-primary]: ./media/service-fabric-create-your-first-linux-application-with-java/sfx-primary.png
[sf-eclipse-templates]: ./media/service-fabric-create-your-first-linux-application-with-java/sf-eclipse-templates.png

