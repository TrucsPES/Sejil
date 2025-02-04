# Sejil

Sejil is a library that enables you to capture, view and filter your ASP.net core app's log events right from your app. It supports structured logging, querying as well as saving log event queries.

This version let you centralize all your applications logs in one place.

## Quick Links

- [Getting started](#getting-started)
- [Features and Screenshots](#features-and-screenshots)
- [Building](#building)
- [License](#license)

## Getting started

1. Installing [Sejil](https://github.com/TrucsPES/Sejil/releases) package


2. Adding code
    Add below code to **Program.cs**:

    ```csharp
    public static IWebHost BuildWebHost(string[] args) =>
        WebHost.CreateDefaultBuilder(args)
            .AddSejil(new SejilSettings("/sejil", LogEventLevel.Debug));
            // ...
    ```

    Add below code to **Startup.cs**

    ```csharp
    using Sejil;

    public class Startup
    {    
        public void Configure(IApplicationBuilder app, IHostingEnvironment env)
        {
            app.UseSejil();
            // ...
        }
    }
    ```

    (Optional) To require authentication for viewing logs:

    ```csharp
        public void ConfigureServices(IServiceCollection services)
        {
            services.ConfigureSejil(options =>
            {
                options.AuthenticationScheme = /* Your authentication scheme */
            });
        }
    ```

    (Optional) To change the logs page title (Defaults to *Sejil* if not set):

    ```csharp
        public void ConfigureServices(IServiceCollection services)
        {
            services.ConfigureSejil(options =>
            {
                options.Title = "My title";
            });
        }
    ```
    
    (Optional) Hosted Service to cleanup logs DB:

    ```csharp
        public void ConfigureServices(IServiceCollection services)
        {
            services.AddSingleton<SejilService>();
            services.AddHostedService<SejilCleanupService>();
            services.ConfigureSejil(options =>
            {
                options.Title = "Logs";
                options.LogRetentionDays = 30;
            });
        }
    ```

3. Navigate to *http://your-app-url/sejil* to view your app's logs.

## Features and Screenshots

- View your app's logs

    <img src="./assets/001-screenshot-main_opt.jpg" width="800">

- View properties specific to a certain log entry

    <img src="./assets/002-screenshot-properties_opt.jpg" width="800">

- Query your logs

    <img src="./assets/003-screenshot-query_opt.jpg" width="800">

- Mix multiple filters with your query to further limit the results

    <img src="./assets/004-screenshot-query-and-filter_opt.jpg" width="800">

- Save your queries for later use

    <img src="./assets/005-screenshot-save-query_opt.jpg" width="800">

- Load your saved queries

    <img src="./assets/006-screenshot-load-query_opt.jpg" width="800">

## Building

To build the project, you just need to clone the repo then run the build command:

```powershell
git clone https://github.com/alaatm/Sejil.git
cd ./Sejil
./build.ps1  # If running Windows
./build.sh   # If running Linux/OSX
```

You can run one of the sample apps afterwards:

```powershell
cd ./sample/SampleBasic
dotnet run
```

## License

[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)

Copyright &copy; Alaa Masoud.

This project is provided as-is under the Apache 2.0 license. For more information see the [LICENSE file](https://github.com/alaatm/Sejil/blob/master/LICENSE).
