
# LiteX HealthChecks Azure FileStorage
> AzureFileStorage health checks package used to check the status of a Azure File storage service in ASP.NET Core applications.

LiteXHealthChecks is very small yet powerful and high-performance library used to check the status of a component in the application, such as a backend service, database or some internal state.


## Basic Usage

### Install the package

> Install via [Nuget](https://www.nuget.org/packages/LiteX.HealthChecks.AzureStorage.File/).

```Powershell
PM> Install-Package LiteX.HealthChecks.AzureStorage.File
```

##### AppSettings
```js
{  
  "Data": {
    "ConnectionStrings": {
      "AzureFileStorage": "--REPLACE WITH YOUR CONNECTION STRING--"
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
            .AddAzureFileStorage(Configuration["Data:ConnectionStrings:AzureQueueStorage"]);

        // OR
        // 2: With all optional configuration
        services.AddHealthChecks()
            .AddAzureFileStorage(
                connectionString: Configuration["Data:ConnectionStrings:AzureQueueStorage"],
                name: "azure-file-storage",
                failureStatus: HealthStatus.Degraded,
                tags: new string[] { "azure", "storage", "file", "azure-file-storage" });
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
