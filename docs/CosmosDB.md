# LiteX HealthChecks CosmosDB
> CosmosDB health checks package used to check the status of a CosmosDB in ASP.NET Core applications.

LiteXHealthChecks is very small yet powerful and high-performance library used to check the status of a component in the application, such as a backend service, database or some internal state.


## Basic Usage

### Install the package

> Install via [Nuget](https://www.nuget.org/packages/LiteX.HealthChecks.CosmosDB/).

```Powershell
PM> Install-Package LiteX.HealthChecks.CosmosDB
```

##### AppSettings
```js
{  
  "Data": {
    "ConnectionStrings": {
      "CosmosDB": "--REPLACE WITH YOUR CONNECTION STRING--",
    }
  }
}
```

##### Configure Startup Class
```cs
public class Startup
{
    public IConfiguration Configuration { get; }

    public Startup(IConfiguration configuration)
    {
        Configuration = configuration;
    }

    public void ConfigureServices(IServiceCollection services)
    {
        // 1: Use default configuration
        services.AddHealthChecks()
            .AddCosmosDB(Configuration["Data:ConnectionStrings:CosmosDB"]);

        // OR
        // 2: With all optional configuration
        services.AddHealthChecks()
            .AddCosmosDB(
                connectionString: Configuration["Data:ConnectionStrings:CosmosDB"],
                name: "cosmosdb",
                failureStatus: HealthStatus.Unhealthy,
                tags: new string[] { "db", "nosql", "mongodb" });

        // OR
        // 3: With all optional configuration
        services.AddHealthChecks()
            .AddCosmosDB(
                connectionString: Configuration["Data:ConnectionStrings:CosmosDB"],
                databaseName: "cosmosdbname",
                name: "cosmosdb",
                failureStatus: HealthStatus.Unhealthy,
                tags: new string[] { "db", "nosql", "cosmosdb" });
    }

    public void Configure(IApplicationBuilder app, IHostingEnvironment env)
    {
        app.UseHealthChecks("/health");
    }
}
```

### Sample Usage Example
> Sample for other services. 

For more helpful information about LiteX HealthChecks, Please click [here.](https://github.com/a-patel/LiteXHealthChecks#22--configure-startup-class)

