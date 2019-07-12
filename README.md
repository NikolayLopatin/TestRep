# Etalon-core
.Net Core backend for Etalon API

## Execution environment
1. .Net Core SDK 2.2.300 for (download as needed for your operating system: https://dotnet.microsoft.com/download/dotnet-core/2.2)
2. MySQL Server 8.0
3. nginx 1.17.1 (https://nginx.org)

## General description

The project consists of one assembly which includes three libraries.

* Etalon.Web - WebApi
* Etalon.Services - business logic
* Etalon.Data - data source access, description of data models

Solution file "Etalon.sln".

The Web API specification is implemented using "Swagger", which is the default page.

## Build project

Before build application you need installation .Net Core SDK 2.2.300.

To build and publish the project you need to run:
```
dotnet publish ./Etalon.Web/Etalon.Web.csproj  -c Release
```
The default path to results build: __Etalon.Web/bin/Release/netcoreapp2.2/publish__

Additional parameters of the command can be found in the link: https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-publish?tabs=netcore21


## Database

Add the Env variable __"DB_HOST"__ - host database IP or DNS 

Add the Env variable __"DB_PORT"__ - port for connection at database

Add the Env variable __"DB_NAME"__ - name of schema in database 

Add the Env variable __"DB_USER"__ - database user 

Add the Env variable __"DB_PASSWORD" - database user password

## Configuring authorization by tokens

Add the Env variable __"JWT__SITE"__ and set value:"http://www.security.org"
Add the Env variable __"JWT__SIGNINGKEY"__ - the key to sign the token, note the key value should not be in the public domain. Example: 
```
JWT__SIGNINGKEY="cecc8978-943d-4434-bfaa-2e7d4a803b2a"
```
Add the Env variable __"JWT__EXPIRYINMINUTESACCESS"__ - access token time, default time 30 minutes. 

Add the Env variable __"JWT__EXPIRYINMINUTESREFRESH"__ - refresh token time, default time 60 minutes. Example:

## Mail setup

Add the Env variable __"EMAIL__EMAIL"__ - the name of the mailbox that will be send email.

Add the Env variable __"EMAIL__PASSWORD"___ - the password of the mailbox.

## Running WebApi

To running  WebApi application need to run:

```
dotnet Etalon.Web.dll --urls "__URL__"
```
*__URL__ - set the IP address and port that will accept connections via http. 

It is recommended to set the value: --urls "http://127.0.0.1:5500". To set the default port, remove the --urls key (default URL: "http://localhost:5000"). Example: --urls "http://*:8000" (Listining all network interface on port 8000) or --urls "http://192.168.87.65:7000;http://192.168.87.65:7001" (Listining IP 192.168.87.65 on port 7000 and 7001)

The Etalon.Web.dll is in the directory: ./Etalon.Web/bin/Ralease/netcoreapp2.2/publish/

**Attention, you need to launch the application from its directory, otherwise the application will not be able to load the settings file.**

## Settings nginx

Install nginx and connect the ssl certificate.

In the __default.conf__ file (default path /etc/nginx/conf.d/), set:

```
server {
    listen        80;
    location / {
        proxy_pass         __URL_WEB_API__;
        proxy_http_version 1.1;
        proxy_set_header   Upgrade $http_upgrade;
        proxy_set_header   Connection keep-alive;
        proxy_set_header   Host $host;
        proxy_cache_bypass $http_upgrade;
        proxy_set_header   X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header   X-Forwarded-Proto $scheme;
    }
}

```
* __URL_WEB_API__ = value "__URL__" seted Running WebApi 

## Running tests

in developing...

## Development environment

Specify env variable **ASPNETCORE_ENVIRONMENT** to "Development" value. For VS Code it can be done via launch.json:

```json
"env": {
    "ASPNETCORE_ENVIRONMENT": "Development"
}
```

Add **appsettings.Development.json** manually to the project and specify connection string to your MySql:

```json
{
  "Logging": {
    "LogLevel": {
      "Default": "Debug",
      "System": "Information",
      "Microsoft": "Information"
    }
  },
  "ConnectionStrings": {
    "DefaultConnection": "server=127.0.0.1;port=3306;database=etalon;uid=root;password=123456"
  }
}
```

## Available Scripts

Solution includes all necessary dependencies. In case Visual Studio did not start restore the dependencies, restore them manually:

```
dotnet restore
```

Adding new migration need contain **-p Etalon.Data** and **-s Etalon.Web** args, because DbContext is created in Etalon.Web, but Context/Migration/Models are located in Etalon.Data

```
dotnet ef migrations add MigrationName -p Etalon.Data -s Etalon.Web
```

## Built With

* [.NET Core 2.2](https://dotnet.microsoft.com/download/dotnet-core/2.2) - .NET Core 2.2
* [MySQL](https://www.mysql.com/) - MySQL DB
* [Pomelo.EntityFrameworkCore.MySql](https://github.com/PomeloFoundation/Pomelo.EntityFrameworkCore.MySql) - Entity Framework Core provider
