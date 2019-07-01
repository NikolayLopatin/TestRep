# Etalon-core
.Net Core backend for Etalon API
## Execution environment
1. .Net Core SDK 2.2.300 for (download as needed for your operating system: https://dotnet.microsoft.com/download/dotnet-core/2.2)
2. MySQL Server 8.0

## General description

The project consists of one assembly which includes three libraries.

* Etalon.Web - WebApi
* Etalon.Services - business logic
* Etalon.Data - data source access, description of data models

Solution file "Etalon.sln".

To build and publish the project you need to run:
```
dotnet publish Etalon.sln  -c Release
```
The default path to results build: __Etalon.Web\bin\Release\netcoreapp2.2\publish__

Additional parameters of the command can be found in the link: https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-publish?tabs=netcore21


## Database access settings

In the appsettings.json file (default path Etalon.Web\bin\Release\netcoreapp2.2\publish), set the connection string to the database in the area:
```
"ConnectionStrings": {
    "DefaultConnection": "server=__NetworkAddress__;port=__Port__;database=__NameDb__;uid=root;password=__PWD__;Treat Tiny As Boolean=false;Convert Zero Datetime = true"
  }  
```
* __NetworkAddress__ - host database IP or DNS 
* __Port__ -  port for connection at database
* __NameDb__ - name of schema in database
* __PWD__ - database user password

## Configuring authorization by tokens

In the appsettings.json (default path Etalon.Web\bin\Release\netcoreapp2.2\publish) file, set the parameters in the area:
```
"Jwt": {
    "Site": "http://www.security.org",
    "SigningKey": "__SigningKey__",
    "ExpiryInMinutesAccess": "__MinutesAccessToken__",
    "ExpiryInMinutesRefresh": "__MinutesRefreshToken__"
  }
```
* __SigningKey__ - the key to sign the token, note the key value should not be in the public domain. Example: 
```
"SigningKey": "cecc8978-943d-4434-bfaa-2e7d4a803b2a",
```
* __MinutesAccessToken__ - access token time, default time 30 minutes. Example:
```
"ExpiryInMinutesAccess": "30",
```
* __MinutesRefreshToken__ - refresh token time, default time 60 minutes. Example:
```
"ExpiryInMinutesRefresh": "60",
```

## Running tests

in developing...
