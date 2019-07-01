# Etalon-core
.Net Core backend for Etalon API
## Execution environment
1. .Net Core SDK 2.2.300 for (download as needed for your operating system: https://dotnet.microsoft.com/download/dotnet-core/2.2)
2. MySQL Server 8.0

## Database access settings

In the appsettings.json file, set the connection string to the database in the format:
```
"ConnectionStrings": {
    "DefaultConnection": "server=127.0.0.1;port=3306;database=etalonbd;uid=root;password=33Tyjnf;Treat Tiny As Boolean=false;Convert Zero Datetime = true"
  }
  
```
