# Etalon-core
.Net Core backend for Etalon API
## Execution environment
1. .Net Core SDK 2.2.300 for (download as needed for your operating system: https://dotnet.microsoft.com/download/dotnet-core/2.2)
2. MySQL Server 8.0

## Database access settings

In the appsettings.json file, set the connection string to the database in the format:
```
"ConnectionStrings": {
    "DefaultConnection": "server=__NetworkAddress__;port=__Port__;database=__NameDb__;uid=root;password=__PWD__;Treat Tiny As Boolean=false;Convert Zero Datetime = true"
  }  
```
* __NetworkAddress__ - host database IP or DNS 
* __Port__ -  port for connection at database
* __NameDb__ - name of schema in database
* __PWD__ - database user password

