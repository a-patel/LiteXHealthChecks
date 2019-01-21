# LiteX HealthChecks SqlServer
> LiteX.HealthChecks.SqlServer is a small library for health check of ASP.NET Core application.

This client library enables working with the Microsoft Azure Storage (Blob) service for storing binary/blob data. 

Small library to abstract storing files to Microsoft Azure. Quick setup for Azure Storage and very simple wrapper for the Azure Blob Storage to handle container instantiations. 

Very simple configuration in advanced ways. Purpose of this package is to bring a new level of ease to the developers who deal with Azure Blob Storage integration with their system.


## Basic Usage

### Install the package

> Install via [Nuget](https://www.nuget.org/packages/LiteX.HealthChecks.SqlServer/).

```Powershell
PM> Install-Package LiteX.HealthChecks.SqlServer
```

##### AppSettings
```js
{  
  "Data": {
    "ConnectionStrings": {
      "Sql": "Server=.;Initial Catalog=master1;Integrated Security=true"
    }
  }
}
```

##### Configure Startup Class
```cs
public class Startup
{
    public void ConfigureServices(IServiceCollection services)
    {
        // 1. Use default configuration from appsettings.json's 'AzureBlobConfig'
        services.AddHealthChecks()
                .AddSqlServer(Configuration["Data:ConnectionStrings:Sql"]);

        //OR
        // 2. Load configuration settings using options.
        services.AddHealthChecks()
              .AddSqlServer(
                  connectionString: Configuration["Data:ConnectionStrings:Sql"],
                  sqlQuery: "SELECT 1;",
                  name: "sql",
                  failureStatus: HealthStatus.Degraded,
                  tags: new string[] { "db", "sql", "sqlserver" });

    }
}
```

### Sample Usage Example
> Same for all providers. 

For more helpful information about LiteX Storage, Please click [here.](https://github.com/a-patel/LiteXStorage/blob/master/README.md#step-3--use-in-controller-or-business-layer-memo)

