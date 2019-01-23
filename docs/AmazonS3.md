
# LiteX HealthChecks AmazonS3
> AmazonS3 health checks package used to check the status of a Amazon S3 service in ASP.NET Core applications.

LiteXHealthChecks is very small yet powerful and high-performance library used to check the status of a component in the application, such as a backend service, database or some internal state.


## Basic Usage

### Install the package

> Install via [Nuget](https://www.nuget.org/packages/LiteX.HealthChecks.AmazonS3/).

```Powershell
PM> Install-Package LiteX.HealthChecks.AmazonS3
```

##### AppSettings
```js
{  
  "AmazonS3": {
    "AccessKey": "--REPLACE WITH YOUR AccessKey--",
    "SecretKey": "--REPLACE WITH YOUR SecretKey--",
    "BucketName": "--REPLACE WITH YOUR BucketName--"
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
            .AddAmazonS3(options =>
            {
                options.AccessKey = Configuration["AmazonS3:AccessKey"];
                options.SecretKey = Configuration["AmazonS3:SecretKey"];
                options.BucketName = Configuration["AmazonS3:BucketName"];
            }, name: "amazon-s3");

        // OR
        // 2: With all optional configuration
        services.AddHealthChecks()
            .AddAmazonS3(options =>
            {
                options.AccessKey = Configuration["AmazonS3:AccessKey"];
                options.SecretKey = Configuration["AmazonS3:SecretKey"];
                options.BucketName = Configuration["AmazonS3:BucketName"];
            },
            name: "amazon-s3",
            failureStatus: HealthStatus.Degraded,
            tags: new string[] { "amazon-s3", "aws-s3", "s3", "amazon-s3" });
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
