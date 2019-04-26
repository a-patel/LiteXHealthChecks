
# LiteX HealthChecks DynamoDB
> DynamoDB health checks package used to check the status of a DynamoDB service in ASP.NET Core applications.

LiteXHealthChecks is very small yet powerful and high-performance library used to check the status of a component in the application, such as a backend service, database or some internal state.


## Basic Usage

### Install the package

> Install via [Nuget](https://www.nuget.org/packages/LiteX.HealthChecks.DynamoDB/).

```Powershell
PM> Install-Package LiteX.HealthChecks.DynamoDB
```

##### AppSettings
```js
{  
  "DynamoDB": {
    "AccessKey": "--REPLACE WITH YOUR AccessKey--",
    "SecretKey": "--REPLACE WITH YOUR SecretKey--",
    //"RegionEndpoint": "--REPLACE WITH YOUR RegionEndpoint--"  // USE 'Amazon.RegionEndpoint.CNNorth1' in configuration code
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
                .AddDynamoDB(options =>
                {
                    options.AccessKey = Configuration["DynamoDB:AccessKey"];
                    options.SecretKey = Configuration["DynamoDB:SecretKey"];
                    options.RegionEndpoint = Amazon.RegionEndpoint.CNNorth1;
                }, name: "dynamodb");

            // OR
            // 2: With all optional configuration
            services.AddHealthChecks()
                .AddDynamoDB(options =>
                {
                    options.AccessKey = Configuration["DynamoDB:AccessKey"];
                    options.SecretKey = Configuration["DynamoDB:SecretKey"];
                    options.RegionEndpoint = Amazon.RegionEndpoint.CNNorth1;
                },
                name: "dynamodb",
                failureStatus: HealthStatus.Degraded,
                tags: new string[] { "nosql", "dynamodb", "aws-dynamodb", "amazon-dynamodb" });
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
