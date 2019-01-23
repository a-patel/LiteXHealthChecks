# LiteX HealthChecks Azure BlobStorage
> AzureBlobStorage health checks package used to check the status of a Azure Blob storage service in ASP.NET Core applications.

LiteXHealthChecks is very small yet powerful and high-performance library used to check the status of a component in the application, such as a backend service, database or some internal state.


## Basic Usage

### Install the package

> Install via [Nuget](https://www.nuget.org/packages/LiteX.HealthChecks.AzureStorage.Blob/).

```Powershell
PM> Install-Package LiteX.HealthChecks.AzureStorage.Blob
```

##### AppSettings
```js
{  
  "Data": {
    "ConnectionStrings": {
      "AzureBlobStorage": "--REPLACE WITH YOUR CONNECTION STRING--"
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
        //1: Use default configuration
        services.AddHealthChecks()
            .AddAzureBlobStorage(Configuration["Data:ConnectionStrings:AzureBlobStorage"]);

        //OR
        //2: With all optional configuration
        services.AddHealthChecks()
            .AddAzureBlobStorage(
                connectionString: Configuration["Data:ConnectionStrings:AzureBlobStorage"],
                name: "azure-blob-storage",
                failureStatus: HealthStatus.Degraded,
                tags: new string[] { "azure", "storage", "blob", "azure-blob-storage" });
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
