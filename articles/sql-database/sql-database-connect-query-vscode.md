---
title: 'VS Code: verbinding maken met Azure SQL Database en query&quot;s uitvoeren voor gegevens | Microsoft Docs'
description: Ontdek hoe u verbinding maakt met SQL Database in Azure met behulp van Visual Studio Code. Voer daarna Transact-SQL-instructies (T-SQL) uit om query&quot;s uit te voeren voor gegevens en om gegevens te bewerken.
metacanonical: 
keywords: verbinding maken met sql-database
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 676bd799-a571-4bb8-848b-fb1720007866
ms.service: sql-database
ms.custom: quick start manage
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 04/17/2017
ms.author: carlrab
translationtype: Human Translation
ms.sourcegitcommit: 8c4e33a63f39d22c336efd9d77def098bd4fa0df
ms.openlocfilehash: 45405c7bb9993d1fd529b25b599c3cd7f459843c
ms.lasthandoff: 04/19/2017


---
# <a name="azure-sql-database-use-visual-studio-code-to-connect-and-query-data"></a>Azure SQL Database: Visual Studio Code gebruiken om verbinding te maken en query's uit te voeren voor gegevens

[Visual Studio Code](https://code.visualstudio.com/docs) is een grafische code-editor voor Linux, Mac OS en Windows die ondersteuning biedt voor extensies, waaronder de [mssql-extensie](https://aka.ms/mssql-marketplace) voor het uitvoeren van query's in Microsoft SQL Server, Azure SQL Database en SQL Data Warehouse. In deze Quick Start ziet u hoe u Visual Studio Code gebruikt om verbinding te maken met een Azure SQL-database en vervolgens Transact-SQL-instructies gebruikt om gegevens in de database te zoeken, in te voegen, bij te werken en te verwijderen.

In deze Quick Start wordt dit gebruikt als basis voor het maken van de resources die u hebt gemaakt in een van deze Quick Starts:

- [Database maken - Portal](sql-database-get-started-portal.md)
- [Database maken - CLI](sql-database-get-started-cli.md)

Voordat u begint, zorgt u ervoor dat u de nieuwste versie van [Visual Studio Code](https://code.visualstudio.com/Download) hebt geïnstalleerd en dat de [mssql-extensie](https://aka.ms/mssql-marketplace) is geladen. Zie [VS Code installeren](https://docs.microsoft.com/sql/linux/sql-server-linux-develop-use-vscode#install-vs-code) voor hulp bij het installeren van de mssql-extensie. Zie ook [mssql voor Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql). 

## <a name="configure-vs-code"></a>VS-code configureren 

### <a name="mac-os"></a>**Mac OS**
Voor Mac OS moet u OpenSSL installeren. Dit is een vereiste voor DotNet Core waarvan de mssql-extensie gebruikmaakt. Open de terminal en voer de volgende opdrachten in om **brew** en **OpenSSL** te installeren. 

```bash
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew update
brew install openssl
mkdir -p /usr/local/lib
ln -s /usr/local/opt/openssl/lib/libcrypto.1.0.0.dylib /usr/local/lib/
ln -s /usr/local/opt/openssl/lib/libssl.1.0.0.dylib /usr/local/lib/
```

### <a name="linux-ubuntu"></a>**Linux (Ubuntu)**

Er is geen speciale configuratie vereist.

### <a name="windows"></a>**Windows**

Er is geen speciale configuratie vereist.

## <a name="get-connection-information"></a>Verbindingsgegevens ophalen

Haal de verbindingsgegevens op die nodig zijn om verbinding te maken met de Azure SQL-database. U hebt de volledig gekwalificeerde servernaam, databasenaam en aanmeldingsgegevens in de volgende procedures nodig.

1. Meld u aan bij [Azure Portal](https://portal.azure.com/).
2. Selecteer **SQL-databases** in het menu links en klik op uw database op de pagina **SQL-databases**. 
3. Op de pagina **Overzicht** voor de database controleert u de volledig gekwalificeerde servernaam zoals in de volgende afbeelding wordt weergegeven. U kunt de cursor boven de servernaam houden om de optie **Klik om te kopiëren** naar boven te halen.

   ![verbindingsgegevens](./media/sql-database-connect-query-ssms/connection-information.png) 

4. Als u de aanmeldingsgegevens voor uw Azure SQL Database-server bent vergeten, gaat u naar de SQL Database-serverpagina om de beheerdersnaam voor de server weer te geven en, indien nodig, het wachtwoord opnieuw in te stellen. 

## <a name="set-language-mode-to-sql"></a>Taalmodus instellen op SQL

Zorg ervoor dat de taalmodus in Visual Studio Code is ingesteld op **SQL** om mssql-opdrachten en T-SQL IntelliSense in te schakelen.

1. Open een nieuw Visual Studio Code venster. 

2. Klik op **Tekst zonder opmaak** in de rechterbenedenhoek van de statusbalk.
3. In de vervolgkeuzelijst **Taalmodus selecteren** die wordt geopend, typt u **SQL** en drukt u vervolgens op **ENTER** om de taalmodus in te stellen op SQL. 

   ![SQL-taalmodus](./media/sql-database-connect-query-vscode/vscode-language-mode.png)

## <a name="connect-to-your-database-in-the-sql-database-logical-server"></a>Verbinding maken met uw database op de logische SQL Database-server

Gebruik Visual Studio Code om verbinding te maken met uw Azure SQL Database-server.

> [!IMPORTANT]
> Voordat u doorgaat, zorgt u ervoor dat u uw server-, database- en aanmeldingsgegevens bij de hand hebt. Wanneer u begint met het invoeren van de verbindingsprofielgegevens, moet u als u de focus van Visual Studio Code wijzigt, het maken van het verbindingsprofiel opnieuw starten.
>

1. In VS Code drukt u op **CTRL+SHIFT+P** (of **F1**) om het opdrachtenpalet te openen.

2. Typ **sqlcon** en druk op **ENTER**.

3. Druk op **ENTER** om **Verbindingsprofiel maken** te selecteren. Hiermee wordt een verbindingsprofiel gemaakt voor uw exemplaar van SQL Server.

4. Volg de aanwijzingen om de verbindingseigenschappen op te geven voor het nieuwe verbindingsprofiel. Wanneer u een waarde hebt ingevoerd, drukt u op **ENTER** om door te gaan. 

   In de volgende tabel worden de verbindingsprofieleigenschappen beschreven.

   | Instelling | Beschrijving |
   |-----|-----|
   | **Servernaam** | Voer de volledig gekwalificeerde servernaam in, zoals **mynewserver20170313.database.windows.net** |
   | **Databasenaam** | Voer de naam van uw database in, zoals **mySampleDatabase** |
   | **Verificatie** | Selecteer de SQL-aanmelding |
   | **Gebruikersnaam** | Gebruik het beheerdersaccount voor de server |
   | **Wachtwoord (SQL-aanmelding)** | Voer het wachtwoord in voor het beheerdersaccount voor de server | 
   | **Wachtwoord opslaan?** | Selecteer **Ja** of **Nee** |
   | **[Optioneel] Voer een naam in voor dit profiel** | Voer een verbindingsprofielnaam in, zoals **mySampleDatabase**. 

5. Druk op **ESC** om het bericht te sluiten met de informatie dat het profiel is gemaakt en verbonden.

6. Controleer in de statusbalk of er verbinding is gemaakt.

   ![Verbindingsstatus](./media/sql-database-connect-query-vscode/vscode-connection-status.png)

## <a name="query-data"></a>Querygegevens

Gebruik de volgende code om op categorie een query uit te voeren voor de 20 populairste producten. Gebruik de Transact-SQL-instructie [SELECT](https://msdn.microsoft.com/library/ms189499.aspx).

1. Voer in het venster **Editor** de volgende query in in het lege queryvenster:

   ```sql
   SELECT pc.Name as CategoryName, p.name as ProductName
   FROM [SalesLT].[ProductCategory] pc
   JOIN [SalesLT].[Product] p
   ON pc.productcategoryid = p.productcategoryid;
   ```

2. Druk op **CTRL+SHIFT+E** om gegevens op te halen uit de tabellen Product en ProductCategory.

    ![Query’s uitvoeren](./media/sql-database-connect-query-vscode/query.png)

## <a name="insert-data"></a>Gegevens invoegen

Gebruik de volgende code om een nieuw product in te voegen in de tabel SalesLT.Product. Gebruik de Transact-SQL-instructie [INSERT](https://msdn.microsoft.com/library/ms174335.aspx).

1. In het venster **Editor** verwijdert u de eerdere query en voert u de volgende query in:

   ```sql
   INSERT INTO [SalesLT].[Product]
           ( [Name]
           , [ProductNumber]
           , [Color]
           , [ProductCategoryID]
           , [StandardCost]
           , [ListPrice]
           , [SellStartDate]
           )
     VALUES
           ('myNewProduct'
           ,123456789
           ,'NewColor'
           ,1
           ,100
           ,100
           ,GETDATE() );
   ```

2. Druk op **CTRL+SHIFT+E** om een nieuwe rij in te voegen in de tabel Product.

## <a name="update-data"></a>Gegevens bijwerken

Gebruik de volgende code om het nieuwe product bij te werken dat u eerder hebt toegevoegd. Gebruik de Transact-SQL-instructie [UPDATE](https://msdn.microsoft.com/library/ms177523.aspx).

1.  In het venster **Editor** verwijdert u de eerdere query en voert u de volgende query in:

   ```sql
   UPDATE [SalesLT].[Product]
   SET [ListPrice] = 125
   WHERE Name = 'myNewProduct';
   ```

2. Druk op **CTRL+SHIFT+E** om de opgegeven rij in de tabel Product bij te werken.

## <a name="delete-data"></a>Gegevens verwijderen

Gebruik de volgende code om het nieuwe product te verwijderen dat u eerder hebt toegevoegd. Gebruik de Transact-SQL-instructie [DELETE](https://msdn.microsoft.com/library/ms189835.aspx).

1. In het venster **Editor** verwijdert u de eerdere query en voert u de volgende query in:

   ```sql
   DELETE FROM [SalesLT].[Product]
   WHERE Name = 'myNewProduct';
   ```

2. Druk op **CTRL+SHIFT+E** om de opgegeven rij in de tabel Product te verwijderen.

## <a name="next-steps"></a>Volgende stappen

- Als u verbinding wilt maken en query's wilt uitvoeren met behulp van SQL Server Management Studio, raadpleegt u [Verbinding maken en query's uitvoeren met SSMS](sql-database-connect-query-ssms.md)
- Zie [Verbinding maken en query’s uitvoeren met .NET](sql-database-connect-query-dotnet.md) als u verbinding wilt maken en query’s wilt uitvoeren met .NET.
- Zie [Verbinding maken en query's uitvoeren met PHP](sql-database-connect-query-php.md) als u verbinding wilt maken en query's wilt uitvoeren met PHP.
- Zie [Verbinding maken en query's uitvoeren met Node.js](sql-database-connect-query-nodejs.md) als u verbinding wilt maken en query's wilt uitvoeren met Node.js.
- Zie [Verbinding maken en query's uitvoeren met Java](sql-database-connect-query-java.md) als u verbinding wilt maken en query's wilt uitvoeren met Java.
- Zie [Verbinding maken en query's uitvoeren met Python](sql-database-connect-query-python.md) als u verbinding wilt maken en query's wilt uitvoeren met Python.
- Zie [Verbinding maken en query's uitvoeren met Ruby](sql-database-connect-query-ruby.md) als u verbinding wilt maken en query's wilt uitvoeren met Ruby.

