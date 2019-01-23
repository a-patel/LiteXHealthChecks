# LiteX HealthChecks AzureServiceBus
> AzureServiceBus health checks package used to check the status of a Azure ServiceBus service in ASP.NET Core applications.

LiteXHealthChecks is very small yet powerful and high-performance library used to check the status of a component in the application, such as a backend service, database or some internal state.


## Basic Usage

### Install the package

> Install via [Nuget](https://www.nuget.org/packages/LiteX.HealthChecks.AzureServiceBus/).

```Powershell
PM> Install-Package LiteX.HealthChecks.AzureServiceBus
```

##### AppSettings
```js
{  
  "Data": {
    "ConnectionStrings": {
      "AzureServiceBus": "--REPLACE WITH YOUR CONNECTION STRING--"
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
        // Queue
        // 1: Use default configuration
        services.AddHealthChecks()
            .AddAzureServiceBusQueue(Configuration["Data:ConnectionStrings:AzureServiceBus"], "queue1");

        // OR
        // 2: With all optional configuration
        services.AddHealthChecks()
            .AddAzureServiceBusQueue(
                connectionString: Configuration["Data:ConnectionStrings:AzureServiceBus"],
                queueName: "queue1",
                name: "azure-servicebus-queue",
                failureStatus: HealthStatus.Degraded,
                tags: new string[] { "azure", "servicebus", "queue", "azure-servicebus-queue" });

        // Topic
        // 1: Use default configuration
        services.AddHealthChecks()
            .AddAzureServiceBusTopic(Configuration["Data:ConnectionStrings:AzureServiceBus"], "topic1");

        // OR
        // 2: With all optional configuration
        services.AddHealthChecks()
            .AddAzureServiceBusTopic(
                connectionString: Configuration["Data:ConnectionStrings:AzureServiceBus"],
                topicName: "topic1",
                name: "azure-servicebus-topic",
                failureStatus: HealthStatus.Degraded,
                tags: new string[] { "azure", "servicebus", "topic", "azure-servicebus-topic" });
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

