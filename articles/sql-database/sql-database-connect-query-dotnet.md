---
title: Verbinding maken met Azure SQL Database via .NET (C#) | Microsoft Docs
description: Is een .NET-codevoorbeeld dat u kunt gebruiken om verbinding te maken met en gegevens op te vragen uit Azure SQL Database
services: sql-database
documentationcenter: 
author: ajlam
manager: jhubbard
editor: 
ms.assetid: 7faca033-24b4-4f64-9301-b4de41e73dfd
ms.service: sql-database
ms.custom: quick start connect
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 05/07/2017
ms.author: andrela;sstein;carlrab
ms.translationtype: Human Translation
ms.sourcegitcommit: 2db2ba16c06f49fd851581a1088df21f5a87a911
ms.openlocfilehash: 0dff167c370fcd2df40aa2ac302d0f09990e1d41
ms.contentlocale: nl-nl
ms.lasthandoff: 05/08/2017


---
# <a name="azure-sql-database-use-net-c-to-connect-and-query-data"></a>Azure SQL Database: .NET (C#) gebruiken om verbinding te maken en query's uit te voeren voor gegevens

In deze Quick Start ziet u hoe u [C# en ADO.NET](https://msdn.microsoft.com/library/kb9s9ks0.aspx) gebruikt om verbinding te maken met een Azure SQL-database en vervolgens Transact-SQL-instructies gebruikt om gegevens in de database te zoeken, in te voegen, bij te werken en te verwijderen vanaf het Windows-, Mac OS- en Ubuntu Linux-platform.

In deze Quick Start wordt dit gebruikt als basis voor het maken van de resources die u hebt gemaakt in een van deze Quick Starts:

- [Database maken - Portal](sql-database-get-started-portal.md)
- [Database maken - CLI](sql-database-get-started-cli.md)

## <a name="install-net"></a>.NET installeren

Voor de stappen in dit gedeelte wordt ervan uitgegaan dat u bekend bent met het ontwikkelen met .NET, maar geen ervaring hebt met het werken met Azure SQL Database. Als u niet bekend bent met ontwikkelen met .NET, gaat u naar [Een app bouwen met SQL Server](https://www.microsoft.com/en-us/sql-server/developer-get-started/) en selecteert u **C#**. Selecteer vervolgens uw besturingssysteem.

### <a name="windows-net-framework-and-net-core"></a>**Windows .NET Framework en .NET Core**

Visual Studio 2017 Community is een volledig functionele, uitbreidbare en gratis IDE voor het maken van moderne toepassingen voor Android, iOS en Windows, voor web- en databasetoepassingen, en voor cloudservices. U kunt het .NET Framework volledig installeren of alleen .NET Core. De codefragmenten in de Quick Start werken in beide gevallen. Als Visual Studio al is geïnstalleerd op uw computer, kunt u de volgende stappen overslaan.

1. Download het [installatieprogramma voor Visual Studio 2017](https://www.visualstudio.com/thank-you-downloading-visual-studio/?sku=Community&rel=15). 
2. Voer het installatieprogramma uit en volg de weergegeven opdrachten om de installatie te voltooien.

### <a name="mac-os"></a>**Mac OS**
Open de terminal en navigeer naar een map waar u van plan bent een .NET Core-project te maken. Voer de volgende opdrachten in voor het installeren van **Brew**, **OpenSSL** en **.NET Core**. 

```bash
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew update
brew install openssl
mkdir -p /usr/local/lib
ln -s /usr/local/opt/openssl/lib/libcrypto.1.0.0.dylib /usr/local/lib/
ln -s /usr/local/opt/openssl/lib/libssl.1.0.0.dylib /usr/local/lib/
```

Installeer .NET Core op Mac OS. Download het [officiële installatieprogramma](https://go.microsoft.com/fwlink/?linkid=843444). Met dit installatieprogramma installeert u de hulpprogramma's en plaats u ze op het PAD, zodat u dotnet kunt uitvoeren vanuit de console

### <a name="linux-ubuntu"></a>**Linux (Ubuntu)**
Open de terminal en navigeer naar een map waar u van plan bent een .NET Core-project te maken. Voer de volgende opdrachten in om **.NET Core** te installeren.

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ xenial main" > /etc/apt/sources.list.d/dotnetdev.list'
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
sudo apt-get update
sudo apt-get install dotnet-dev-1.0.1
```

## <a name="get-connection-information"></a>Verbindingsgegevens ophalen

Haal de verbindingsgegevens op die nodig zijn om verbinding te maken met de Azure SQL-database. U hebt de volledig gekwalificeerde servernaam, databasenaam en aanmeldingsgegevens in de volgende procedures nodig.

1. Meld u aan bij [Azure Portal](https://portal.azure.com/).
2. Selecteer **SQL-databases** in het menu links en klik op uw database op de pagina **SQL-databases**. 
3. Op de pagina **Overzicht** voor de database controleert u de volledig gekwalificeerde servernaam zoals in de onderstaande afbeelding wordt weergegeven. U kunt de cursor boven de servernaam houden om de optie **Klik om te kopiëren** naar boven te halen. 

   ![servernaam](./media/sql-database-connect-query-dotnet/server-name.png) 

4. Als u de aanmeldingsgegevens voor uw Azure SQL Database-server bent vergeten, gaat u naar de SQL Database-serverpagina om de beheerdersnaam voor de server weer te geven en, indien nodig, het wachtwoord opnieuw in te stellen.

5. Klik op **Databaseverbindingsreeksen tonen**.

6. Bekijk de volledige**ADO.NET**-verbindingsreeks.

    ![ADO.NET-verbindingsreeks](./media/sql-database-connect-query-dotnet/adonet-connection-string.png)
  
## <a name="add-systemdatasqlclient"></a>System.Data.SqlClient toevoegen
Als u gebruikmaakt van .NET Core, voegt u System.Data.SqlClient als een afhankelijkheid toe aan het ***.csproj***-bestand van het project.

```xml
<ItemGroup>
    <PackageReference Include="System.Data.SqlClient" Version="4.3.0" />
</ItemGroup>
```

## <a name="select-data"></a>Gegevens selecteren

1. Open een leeg codebestand in uw ontwikkelingsomgeving.
2. Voeg ```using System.Data.SqlClient``` toe aan uw codebestand ([naamruimte System.Data.SqlClient](https://msdn.microsoft.com/library/system.data.sqlclient.aspx)). 

3. Gebruik de volgende code om op categorie een query uit te voeren voor de 20 populairste producten. Gebruik de opdracht [SqlCommand.ExecuteReader](https://msdn.microsoft.com/library/system.data.sqlclient.sqlcommand.executereader.aspx) met de Transact-SQL-instructie [SELECT](https://msdn.microsoft.com/library/ms189499.aspx). Voeg de juiste waarden toe voor uw server, database, gebruiker en wachtwoord.

```csharp
using System;
using System.Data;
using System.Data.SqlClient;

namespace ConsoleApplication1
{
    class Program
    {
        static void Main(string[] args)
        {
            try 
            { 
                SqlConnectionStringBuilder builder = new SqlConnectionStringBuilder();
                builder.DataSource = "your_server.database.windows.net"; 
                builder.UserID = "your_user";            
                builder.Password = "your_password";     
                builder.InitialCatalog = "your_database";

                using (SqlConnection connection = new SqlConnection(builder.ConnectionString))
                {
                    Console.WriteLine("\nQuery data example:");
                    Console.WriteLine("=========================================\n");
                    
                    connection.Open();       
                    StringBuilder sb = new StringBuilder();
                    sb.Append("SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName ");
                    sb.Append("FROM [SalesLT].[ProductCategory] pc ");
                    sb.Append("JOIN [SalesLT].[Product] p ");
                    sb.Append("ON pc.productcategoryid = p.productcategoryid;");
                    String sql = sb.ToString();

                    using (SqlCommand command = new SqlCommand(sql, connection))
                    {
                        using (SqlDataReader reader = command.ExecuteReader())
                        {
                            while (reader.Read())
                            {
                                Console.WriteLine("{0} {1}", reader.GetString(0), reader.GetString(1));
                            }
                        }
                    }                    
                }
            }
            catch (SqlException e)
            {
                Console.WriteLine(e.ToString());
            }
        }
    }
}
```

## <a name="insert-data"></a>Gegevens invoegen

Gebruik de volgende code om een nieuw product in te voegen in de tabel SalesLT.Product. Gebruik de opdracht [SqlCommand.ExecuteNonQuery](https://msdn.microsoft.com/library/system.data.sqlclient.sqlcommand.executenonquery.aspx) met de Transact-SQL-instructie [INSERT](https://msdn.microsoft.com/library/ms174335.aspx). Voeg de juiste waarden toe voor uw server, database, gebruiker en wachtwoord.

```csharp
using System;
using System.Data;
using System.Data.SqlClient;

namespace ConsoleApplication1
{
    class Program
    {
        static void Main(string[] args)
        {
            try 
            { 
                SqlConnectionStringBuilder builder = new SqlConnectionStringBuilder();
                builder.DataSource = "your_server.database.windows.net"; 
                builder.UserID = "your_user";            
                builder.Password = "your_password";     
                builder.InitialCatalog = "your_database";

                using (SqlConnection connection = new SqlConnection(builder.ConnectionString))
                {
                    Console.WriteLine("\nInsert data example:");
                    Console.WriteLine("=========================================\n");

                    connection.Open();       
                    StringBuilder sb = new StringBuilder();
                    sb.Append("INSERT INTO [SalesLT].[Product] ([Name], [ProductNumber], [Color], [StandardCost], [ListPrice], [SellStartDate]) ");
                    sb.Append("VALUES (@Name, @ProductNumber, @Color, @StandardCost, @ListPrice, @SellStartDate);");
                    String sql = sb.ToString();
                    using (SqlCommand command = new SqlCommand(sql, connection))
                    {
                        command.Parameters.AddWithValue("@Name", "BrandNewProduct");
                        command.Parameters.AddWithValue("@ProductNumber", "200989");
                        command.Parameters.AddWithValue("@Color", "Blue");
                        command.Parameters.AddWithValue("@StandardCost", 75);
                        command.Parameters.AddWithValue("@ListPrice", 80);
                        command.Parameters.AddWithValue("@SellStartDate", "7/1/2016");
                        int rowsAffected = command.ExecuteNonQuery();
                        Console.WriteLine(rowsAffected + " row(s) inserted");
                    }         
                }
            }
            catch (SqlException e)
            {
                Console.WriteLine(e.ToString());
            }
        }
    }
}
```

## <a name="update-data"></a>Gegevens bijwerken

Gebruik de volgende code om het nieuwe product bij te werken dat u eerder hebt toegevoegd. Gebruik de opdracht [SqlCommand.ExecuteNonQuery](https://msdn.microsoft.com/library/system.data.sqlclient.sqlcommand.executenonquery.aspx) met de Transact-SQL-instructie [UPDATE](https://msdn.microsoft.com/library/ms177523.aspx). Voeg de juiste waarden toe voor uw server, database, gebruiker en wachtwoord.

```csharp
using System;
using System.Data;
using System.Data.SqlClient;

namespace ConsoleApplication1
{
    class Program
    {
        static void Main(string[] args)
        {
            try 
            { 
                SqlConnectionStringBuilder builder = new SqlConnectionStringBuilder();
                builder.DataSource = "your_server.database.windows.net"; 
                builder.UserID = "your_user";            
                builder.Password = "your_password";     
                builder.InitialCatalog = "your_database";

                using (SqlConnection connection = new SqlConnection(builder.ConnectionString))
                {
                    Console.WriteLine("\nUpdate data example");
                    Console.WriteLine("=========================================\n");

                    connection.Open();       
                    StringBuilder sb = new StringBuilder();
                    sb.Append("UPDATE [SalesLT].[Product] SET ListPrice = @ListPrice WHERE Name = @Name;");
                    String sql = sb.ToString();
                    using (SqlCommand command = new SqlCommand(sql, connection))
                    {
                        command.Parameters.AddWithValue("@Name", "BrandNewProduct");
                        command.Parameters.AddWithValue("@ListPrice", 500);
                        int rowsAffected = command.ExecuteNonQuery();
                        Console.WriteLine(rowsAffected + " row(s) updated");
                    }         
                }
            }
            catch (SqlException e)
            {
                Console.WriteLine(e.ToString());
            }
        }
    }
}
```

## <a name="delete-data"></a>Gegevens verwijderen

Gebruik de volgende code om het nieuwe product te verwijderen dat u eerder hebt toegevoegd. Gebruik de opdracht [SqlCommand.ExecuteNonQuery](https://msdn.microsoft.com/library/system.data.sqlclient.sqlcommand.executenonquery.aspx) met de Transact-SQL-instructie [DELETE](https://msdn.microsoft.com/library/ms189835.aspx). Voeg de juiste waarden toe voor uw server, database, gebruiker en wachtwoord.

```csharp
using System;
using System.Data;
using System.Data.SqlClient;

namespace ConsoleApplication1
{
    class Program
    {
        static void Main(string[] args)
        {
            try 
            { 
                SqlConnectionStringBuilder builder = new SqlConnectionStringBuilder();
                builder.DataSource = "your_server.database.windows.net"; 
                builder.UserID = "your_user";            
                builder.Password = "your_password";     
                builder.InitialCatalog = "your_database";

                using (SqlConnection connection = new SqlConnection(builder.ConnectionString))
                {
                    Console.WriteLine("\nDelete data example");
                    Console.WriteLine("=========================================\n");

                    connection.Open();       
                    StringBuilder sb = new StringBuilder();
                    sb.Append("DELETE FROM SalesLT.Product WHERE Name = @Name;");
                    String sql = sb.ToString();
                    using (SqlCommand command = new SqlCommand(sql, connection))
                    {
                        command.Parameters.AddWithValue("@Name", "BrandNewProduct");
                        int rowsAffected = command.ExecuteNonQuery();
                        Console.WriteLine(rowsAffected + " row(s) deleted");
                    }         
                }
            }
            catch (SqlException e)
            {
                Console.WriteLine(e.ToString());
            }
        }
    }
}
```

## <a name="next-steps"></a>Volgende stappen
- [Uw eerste Azure SQL-database ontwerpen](sql-database-design-first-database.md)
- [.NET-documentatie](https://docs.microsoft.com/dotnet/).
- [Verbinding maken en query's uitvoeren met SSMS](sql-database-connect-query-ssms.md)
- [Verbinding maken en query's uitvoeren met Visual Studio Code](sql-database-connect-query-vscode.md).


